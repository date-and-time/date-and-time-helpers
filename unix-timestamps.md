# Unix Timestamp Conversion

A Unix timestamp is a count of elapsed time since `1970-01-01T00:00:00Z`. The most common formats are seconds and milliseconds.

## Seconds vs milliseconds

Many APIs return timestamps in seconds:

```js
const seconds = 1712345678
const date = new Date(seconds * 1000)
```

JavaScript `Date` expects milliseconds:

```js
const milliseconds = 1712345678000
const date = new Date(milliseconds)
```

If a timestamp is around 10 digits, it is probably seconds. If it is around 13 digits, it is probably milliseconds. For manual checks, use a [Unix timestamp converter](https://freeonlinenosignup.com/date-time/unix-timestamp).

## Convert date to timestamp

```js
const date = new Date("2026-04-19T12:00:00Z")

const seconds = Math.floor(date.getTime() / 1000)
const milliseconds = date.getTime()
```

Use `Math.floor` for Unix seconds unless you have a clear reason to round. Rounding can push a timestamp into the next second.

## Convert timestamp to ISO string

```js
function unixSecondsToIso(seconds) {
  return new Date(seconds * 1000).toISOString()
}
```

## Common pitfalls

- Passing Unix seconds directly into `new Date()` creates a date near January 1970.
- Parsing a date string without a timezone can be interpreted in local time.
- Displaying a UTC timestamp in local time can change the calendar date.
- Databases and APIs may disagree on seconds vs milliseconds.

## Quick verification

Before shipping timestamp logic, test at least:

- A current timestamp.
- A timestamp near midnight UTC.
- A timestamp during daylight saving changes for the target locale.
- A known historical timestamp.

The online [Unix timestamp tool](https://freeonlinenosignup.com/date-time/unix-timestamp) shows UTC, local time, ISO 8601, seconds, and milliseconds in one place.

