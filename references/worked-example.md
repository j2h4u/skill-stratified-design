# Worked example: publish eligible recordings

This is an original teaching example. It shows one complete behavior path.
All functions can stay in one module. No new package or framework is required.

## Contract

Each input row is a valid `(name, seconds, blocked)` tuple. Names are strings,
durations are nonnegative integers, and `blocked` is a boolean. Publish a
recording only when it is not blocked and its duration is at least 30 seconds.
An empty name is valid.

Process rows in input order, including rows from a single-pass iterator.
Return the publisher's receipts unchanged. If publication fails, propagate
the error and stop before reading the next row. Do not change the input rows.

## Before

```python
from collections.abc import Callable, Iterable

Row = tuple[str, int, bool]


def publish_ready(rows: Iterable[Row], publish: Callable[[str], object]) -> list[object]:
    receipts = []
    for row in rows:
        name, seconds, blocked = row
        if blocked or seconds < 30:
            continue
        receipts.append(publish(name))
    return receipts
```

The public operation owns tuple decoding, eligibility, and publication.
A reader must understand the row fields to follow its policy and effects.
Renaming the loop or forwarding its arguments would leave that knowledge
with the same caller.

## After

```python
from collections.abc import Callable, Iterable
from dataclasses import dataclass

Row = tuple[str, int, bool]


@dataclass(frozen=True)
class Recording:
    name: str
    seconds: int
    blocked: bool


def as_recording(row: Row) -> Recording:
    return Recording(*row)


def can_publish(recording: Recording) -> bool:
    return not recording.blocked and recording.seconds >= 30


def publish_ready(rows: Iterable[Row], publish: Callable[[str], object]) -> list[object]:
    receipts = []
    for row in rows:
        recording = as_recording(row)
        if can_publish(recording):
            receipts.append(publish(recording.name))
    return receipts
```

`as_recording` converts the row representation to named recording facts.
`can_publish` owns the eligibility rule. `publish_ready` combines these
operations and owns the publication order. Its body no longer unpacks tuples
or compares duration thresholds. The conversion and rule are calculations;
publication remains an action.

Keep the original loop while moving these boundaries. Do not decode all rows
before publication. Keep the caller interface and check behavior after each
boundary change with the same focused cases below.

The original condition rejects a row. The new predicate accepts a recording.
Changing `if blocked or seconds < 30: continue` requires the opposite condition
before publication. Check both outcomes and the exact threshold.

## Check the benefit

If the minimum duration changes, update `can_publish` and its behavior cases.
Publication order and tuple decoding keep their current owners.

If rows change to mappings, update `Row`, `as_recording`, row producers, and
input fixtures. Eligibility and publication can keep their recording interface.
The public input format still has callers; this boundary does not remove
the cost of changing that contract.

The record and predicate have a purpose here: they separate representation
from policy. They are not required additions to every small loop. A helper
such as `def keep(flag): return flag` would leave the complete eligibility
decision with its caller. Stop adding operations when further boundaries
do not make the task easier.

## Shared behavior checks

Use the same checks with either implementation. Expected names are explicit;
the checks do not repeat the eligibility formula or call private helpers.

```python
def check_publication_contract(operation: Callable[..., list[object]]) -> None:
    rows = [
        ("short", 29, False),
        ("blocked", 45, True),
        ("both", 0, True),
        ("", 30, False),
        ("ready", 45, False),
    ]
    original_rows = list(rows)
    names = []
    receipts = [object(), object()]

    def publish(name: str) -> object:
        names.append(name)
        return receipts[len(names) - 1]

    assert operation(iter(rows), publish) == receipts
    assert names == ["", "ready"]
    assert rows == original_rows
    assert operation(iter(()), publish) == []
    assert names == ["", "ready"]

    failure = OSError("publication failed")

    def fail(name: str) -> object:
        raise failure

    def input_rows() -> Iterable[Row]:
        yield ("first", 30, False)
        raise AssertionError("Read another row after a failed publication")

    try:
        operation(input_rows(), fail)
    except OSError as error:
        assert error is failure
    else:
        raise AssertionError("Publication failure did not propagate")
```

The failure case also detects eager input collection. The two accepted rows
check result order and receipt identity. Real publisher integration is a
separate check when an implementation is available. See [testing.md](testing.md)
for the complete test strategy and [design.md](design.md) for other hazards.
