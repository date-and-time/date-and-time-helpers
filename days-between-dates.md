# Days Between Dates

Counting days between two dates requires one decision up front: is the end date included?

## Exclusive end date

Most programming APIs use an exclusive end date. The range starts at `start` and stops before `end`.

```js
function daysBetweenUtcDates(startDate, endDate) {
  const start = Date.UTC(
    startDate.getUTCFullYear(),
    startDate.getUTCMonth(),
    startDate.getUTCDate()
  )
  const end = Date.UTC(
    endDate.getUTCFullYear(),
    endDate.getUTCMonth(),
    endDate.getUTCDate()
  )

  return Math.round((end - start) / 86400000)
}
```

`2026-04-01` to `2026-04-02` is 1 day with this rule.

## Inclusive date ranges

Human-facing reports sometimes include both dates.

```js
const inclusiveDays = daysBetweenUtcDates(start, end) + 1
```

Only do this after validating that `end >= start`.

## Business days

For a simple Monday-Friday count:

```js
function businessDaysBetween(startDate, endDate) {
  let count = 0
  const cursor = new Date(startDate)

  while (cursor < endDate) {
    const day = cursor.getDay()
    if (day !== 0 && day !== 6) count += 1
    cursor.setDate(cursor.getDate() + 1)
  }

  return count
}
```

This ignores holidays. Add a holiday calendar if payroll, billing, shipping, or compliance depends on it.

## Verification

Use a [days between dates calculator](https://freeonlinenosignup.com/date-time/days-between) to compare:

- Calendar days.
- Weeks.
- Approximate months.
- Monday-Friday business days.

## Pitfalls

- Subtracting local midnight timestamps can be wrong across daylight saving changes.
- Inclusive ranges are easy to overcount.
- "Business day" usually needs a regional holiday calendar.
- Date strings like `04/05/2026` are ambiguous across locales.

