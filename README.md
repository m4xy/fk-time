# fk-time

Days on the calendar, and moments where a clock says them, for fckt, alongside the standard
library's `Instant`, `Duration` and `Clock`.

```kotlin
import uk.m4xy.time.*
import uk.m4xy.time.Dates.*
import uk.m4xy.time.DateTimes.*

Date(2026, 10, 31).weekday                 // Saturday
Date(2024, 1, 31).plusMonths(1)            // 2024-02-29, the month's last day
Date(2026, 1, 1).daysUntil(Date(2027, 1, 1))  // 365
iso(now(), Offset(60))                     // 2026-10-31T10:30:00.250+01:00
DateTimes.parse("1969-07-20T20:17:00Z")    // Some(Instant(-14182980000))
```

A `Date` is a year, a month and a day of the Gregorian calendar, every year back and forward;
`Dates.of` says whether there's such a day, and `Dates.parse` reads one as ISO 8601 writes it,
`2026-10-31`, which `.iso` writes. A day's `epochDay` counts days from 1970-01-01, as Howard
Hinnant's algorithms count them, so its `weekday`, `dayOfYear`, `plusDays`, `plusMonths`, which
keeps the day of the month or takes the month's last, `plusYears` and `daysUntil` are right for any
year.

An `Offset` says how far ahead of UTC a clock is, in minutes, and `DateTimes.at` gives the
`DateTime`, a `Date` and a `Time` of day, an `Instant` is where it is; `.instant` goes back.
`DateTimes.iso` writes an instant as ISO 8601 does, `2026-10-31T09:30:00Z`, and `DateTimes.parse`
reads one, with `Z` or an offset, its seconds and their fraction optional. `today` asks the `Clock`
what day it is, so a test says what day it is by handling it.

Time zones with rules, as Europe/London's summer time, aren't in it: an offset is fixed.

## Building

```sh
kiln build          # compiles and tests it
kiln publishLocal   # for other projects: library("uk.m4xy:fk-time:0.1.0")
```
