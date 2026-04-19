# Date and Time Helpers

Practical notes and snippets for developers who need to handle dates, time spans, Unix timestamps, ISO week numbers, and age calculations without getting tripped up by edge cases.

This repository is intentionally small. Each guide covers one recurring date/time task with copyable examples and quick checks.

## Guides

- [Unix timestamp conversion](unix-timestamps.md)
- [Adding and subtracting dates](date-add-subtract.md)
- [Counting days between dates](days-between-dates.md)
- [ISO week numbers](iso-week-numbers.md)
- [Age calculation rules](age-calculation.md)
- [JavaScript date snippets](javascript-date-snippets.md)
- [Testing date and time code](date-time-testing-checklist.md)

## Useful online checks

When you want to verify a result by hand, these browser tools are useful:

- [Unix timestamp to date converter](https://freeonlinenosignup.com/date-time/unix-timestamp)
- [Add or subtract days from a date](https://freeonlinenosignup.com/date-time/date-add)
- [Days between dates calculator](https://freeonlinenosignup.com/date-time/days-between)
- [ISO week number calculator](https://freeonlinenosignup.com/date-time/week-number)
- [Current week number](https://freeonlinenosignup.com/date-time/current-week-number)
- [Exact age calculator](https://freeonlinenosignup.com/date-time/age)

The broader collection is available at [free date and time calculators](https://freeonlinenosignup.com/date-time).

## Principles

- Store instants in UTC when the value represents a moment in time.
- Store plain dates as dates, not as midnight timestamps, when time of day is irrelevant.
- Be explicit about whether an end date is inclusive or exclusive.
- Avoid assuming that every day has exactly 24 local hours.
- Use ISO 8601 week rules only when that is actually the business requirement.

