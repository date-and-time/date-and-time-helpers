# Age Calculation

Age is not just a difference in milliseconds. For humans, age is usually expressed in completed calendar years, months, and days.

## Completed years

```js
function ageInYears(dateOfBirth, onDate = new Date()) {
  let age = onDate.getFullYear() - dateOfBirth.getFullYear()

  const birthdayThisYear = new Date(
    onDate.getFullYear(),
    dateOfBirth.getMonth(),
    dateOfBirth.getDate()
  )

  if (onDate < birthdayThisYear) age -= 1

  return age
}
```

This handles the common "has the birthday happened yet this year?" rule.

## Leap day birthdays

People born on February 29 need a policy for non-leap years. Common rules are:

- Treat February 28 as the birthday.
- Treat March 1 as the birthday.
- Follow a jurisdiction-specific legal rule.

Do not hard-code this silently if eligibility, insurance, benefits, age gates, or contracts depend on it.

## Years, months, and days

For display, calculate in calendar units instead of dividing by average year length.

```txt
2020-02-29 to 2026-04-19
= 6 years, 1 month, 21 days
```

Use an [exact age calculator](https://freeonlinenosignup.com/date-time/age) to verify tricky dates, including leap years and future comparison dates.

## Testing checklist

- Birthday today.
- Birthday tomorrow.
- Birthday yesterday.
- Born on February 29.
- Comparison date before birth date.
- User timezone differs from server timezone.

## Product notes

Ask which age rule applies before implementing age checks. "Age at midnight", "age at the exact birth time", and "age on calendar date" can produce different answers in edge cases.

