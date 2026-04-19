# Date and Time Testing Checklist

Date/time code needs more than happy-path tests. Use this checklist before shipping scheduling, billing, analytics, reporting, reminders, trials, date filters, or eligibility logic.

## Inputs

- Empty date field.
- Invalid date string.
- Ambiguous local date string such as `04/05/2026`.
- Date-only value such as `2026-04-19`.
- Date-time with explicit timezone.
- Unix timestamp in seconds.
- Unix timestamp in milliseconds.

## Boundaries

- Start of day.
- End of day.
- End of month.
- End of year.
- Leap day.
- Daylight saving transition.
- ISO week year boundary.

## Business rules

- Inclusive vs exclusive end dates.
- Calendar days vs business days.
- Local timezone vs UTC.
- Fixed duration vs calendar duration.
- Month-end behavior when adding months.
- Leap day policy for age calculation.

## Manual verification tools

- [Unix timestamp converter](https://freeonlinenosignup.com/date-time/unix-timestamp)
- [Date add/subtract calculator](https://freeonlinenosignup.com/date-time/date-add)
- [Days between dates calculator](https://freeonlinenosignup.com/date-time/days-between)
- [ISO week number calculator](https://freeonlinenosignup.com/date-time/week-number)
- [Exact age calculator](https://freeonlinenosignup.com/date-time/age)

## Suggested test fixtures

| Case | Example |
| --- | --- |
| Leap day | `2024-02-29` |
| Non-leap February end | `2025-02-28` |
| ISO week crossover | `2021-01-01` |
| Month end add | `2026-01-31 + 1 month` |
| Unix seconds | `1712345678` |
| Unix milliseconds | `1712345678000` |

## Review questions

- Can the frontend and backend parse the same date format?
- Is the stored value an instant or a calendar date?
- Does the UI explain timezone-sensitive output?
- Are reports grouped by the same week rule everywhere?
- Do tests run deterministically regardless of the machine timezone?

