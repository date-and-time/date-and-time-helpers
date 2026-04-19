# Adding and Subtracting Dates

Date arithmetic looks simple until month ends, leap years, daylight saving time, and local timezones enter the picture.

## Add days in JavaScript

For plain calendar dates, work from year/month/day parts and let JavaScript normalize the result.

```js
function addDays(date, days) {
  const result = new Date(date)
  result.setDate(result.getDate() + days)
  return result
}

const start = new Date("2026-04-19T00:00:00")
const result = addDays(start, 14)
```

This preserves local calendar behavior. If you are adding fixed durations to an instant, use milliseconds instead.

```js
const twoHoursLater = new Date(start.getTime() + 2 * 60 * 60 * 1000)
```

## Add months carefully

Adding one month to January 31 is ambiguous. Depending on product rules, the result might be February 28, March 3, or an error.

```js
function addMonthsClamped(date, months) {
  const year = date.getFullYear()
  const month = date.getMonth()
  const day = date.getDate()

  const target = new Date(year, month + months + 1, 0)
  const lastDay = target.getDate()

  return new Date(year, month + months, Math.min(day, lastDay))
}
```

This clamps to the last valid day of the target month.

## Business rule checklist

Before adding dates, define:

- Are weekends counted?
- Are holidays counted?
- Is the start date included?
- What happens at the end of a short month?
- Should calculations use local time or UTC?

For one-off checks, use the [date add/subtract calculator](https://freeonlinenosignup.com/date-time/date-add).

## Examples

| Input | Operation | Typical clamped result |
| --- | --- | --- |
| 2024-01-31 | +1 month | 2024-02-29 |
| 2025-01-31 | +1 month | 2025-02-28 |
| 2026-04-19 | +14 days | 2026-05-03 |
| 2026-04-19 | -30 days | 2026-03-20 |

When product teams ask for "one month later", confirm the intended rule before implementing it.

