# ISO Week Numbers

ISO week dates are used in reporting, operations, logistics, payroll, and planning. They do not always match the calendar year.

## Core rules

ISO 8601 weeks follow these rules:

- Weeks start on Monday.
- Week 1 is the week containing the first Thursday of the calendar year.
- An ISO week year can differ from the calendar year near January 1 and December 31.
- Some ISO week years have 53 weeks.

For manual lookup, use the [ISO week number calculator](https://freeonlinenosignup.com/date-time/week-number). For the current value, use [what week number is it today](https://freeonlinenosignup.com/date-time/current-week-number).

## JavaScript implementation

```js
function getIsoWeek(date) {
  const d = new Date(Date.UTC(date.getFullYear(), date.getMonth(), date.getDate()))
  const day = d.getUTCDay() || 7

  d.setUTCDate(d.getUTCDate() + 4 - day)

  const isoYear = d.getUTCFullYear()
  const yearStart = new Date(Date.UTC(isoYear, 0, 1))
  const week = Math.ceil(((d - yearStart) / 86400000 + 1) / 7)

  return { isoYear, week }
}
```

## Why ISO years matter

`2021-01-01` belongs to ISO week `2020-W53`, not `2021-W01`. If your database stores only `week = 53`, reports around year boundaries can group records into the wrong year.

Store both values:

```txt
iso_week_year = 2020
iso_week_number = 53
```

## Test cases

| Date | ISO week year | ISO week |
| --- | ---: | ---: |
| 2021-01-01 | 2020 | 53 |
| 2021-01-04 | 2021 | 1 |
| 2024-12-30 | 2025 | 1 |
| 2026-04-19 | 2026 | 16 |

If your output differs, check whether your code is using Sunday-start calendar weeks instead of ISO weeks.

