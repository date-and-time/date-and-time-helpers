# JavaScript Date Snippets

Small copyable snippets for common date and time tasks.

## Current Unix timestamp

```js
const unixSeconds = Math.floor(Date.now() / 1000)
const unixMilliseconds = Date.now()
```

Check the output with a [Unix timestamp converter](https://freeonlinenosignup.com/date-time/unix-timestamp).

## Start of local day

```js
function startOfLocalDay(date = new Date()) {
  return new Date(date.getFullYear(), date.getMonth(), date.getDate())
}
```

## Start of UTC day

```js
function startOfUtcDay(date = new Date()) {
  return new Date(Date.UTC(
    date.getUTCFullYear(),
    date.getUTCMonth(),
    date.getUTCDate()
  ))
}
```

## Format as YYYY-MM-DD

```js
function toDateOnly(date) {
  const year = date.getFullYear()
  const month = String(date.getMonth() + 1).padStart(2, "0")
  const day = String(date.getDate()).padStart(2, "0")

  return `${year}-${month}-${day}`
}
```

## Add calendar days

```js
function addCalendarDays(date, days) {
  const result = new Date(date)
  result.setDate(result.getDate() + days)
  return result
}
```

Use the [date add/subtract calculator](https://freeonlinenosignup.com/date-time/date-add) to validate outputs around month ends.

## Difference in whole UTC days

```js
function diffUtcDays(a, b) {
  const start = Date.UTC(a.getUTCFullYear(), a.getUTCMonth(), a.getUTCDate())
  const end = Date.UTC(b.getUTCFullYear(), b.getUTCMonth(), b.getUTCDate())
  return Math.round((end - start) / 86400000)
}
```

For human verification, compare with a [days between dates calculator](https://freeonlinenosignup.com/date-time/days-between).

## ISO week number

```js
function isoWeek(date) {
  const d = new Date(Date.UTC(date.getFullYear(), date.getMonth(), date.getDate()))
  const day = d.getUTCDay() || 7
  d.setUTCDate(d.getUTCDate() + 4 - day)

  const year = d.getUTCFullYear()
  const yearStart = new Date(Date.UTC(year, 0, 1))
  const week = Math.ceil(((d - yearStart) / 86400000 + 1) / 7)

  return { year, week }
}
```

The matching browser checker is the [ISO week number calculator](https://freeonlinenosignup.com/date-time/week-number).

