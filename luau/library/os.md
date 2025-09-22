# os

## clock

```lua
function os.clock(): number
```

Returns a high-precision timestamp (in seconds) that doesn't have a defined baseline, but can be used to measure duration with sub-microsecond precision.

## date

```lua
function os.date(s: string?, t: number?): table | string
```

Returns the table or string representation of the time specified as `t` (defaults to current time) according to `s` format string.

When `s` starts with `!`, the result uses UTC, otherwise it uses the current timezone.

If `s` is equal to `*t` (or `!*t`), a table representation of the date is returned, with keys `sec`/`min`/`hour` for the time (using 24-hour clock), `day`/`month`/`year` for the date, `wday` for week day (1..7), `yday` for year day (1..366) and `isdst` indicating whether the timezone is currently using daylight savings.

Otherwise, `s` is interpreted as a [date format string](https://www.cplusplus.com/reference/ctime/strftime/), with the valid specifiers including any of `aAbBcdHIjmMpSUwWxXyYzZ` or `%`. `s` defaults to `"%c"` so `os.date()` returns the human-readable representation of the current date in local timezone.

## difftime

```lua
function os.difftime(a: number, b: number): number
```

Calculates the difference in seconds between `a` and `b`; provided for compatibility only. Please use `a - b` instead.

## time

```lua
function os.time(t: table?): number
```

When called without arguments, returns the current date/time as a Unix timestamp. When called with an argument, expects it to be a table that contains `sec`/`min`/`hour`/`day`/`month`/`year` keys and returns the Unix timestamp of the specified date/time in UTC.
