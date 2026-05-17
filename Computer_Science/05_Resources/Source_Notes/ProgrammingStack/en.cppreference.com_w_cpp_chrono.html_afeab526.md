Title: Date and time library - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/chrono.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:07:05+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# Date and time library

[cpp](https://en.cppreference.com/cpp.html)

C++ includes support for two types of time manipulation:

- The
[chrono library](https://en.cppreference.com/chrono.html#chrono_library), a flexible collection of types that track time with varying degrees of precision (e.g.,[std::chrono::time_point](https://en.cppreference.com/chrono/time_point.html)). -
[C-style date and time library](https://en.cppreference.com/chrono.html#C-style_date_and_time_library)(e.g.,[std::time](https://en.cppreference.com/chrono/c/time.html)).

## Contents |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=1)] [Chrono library](https://en.cppreference.com/header/chrono.html) (since C++11)

The `chrono`

library defines several main types as well as utility functions and common typedefs:

| (since C++20) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=2)] Clocks

A clock consists of a starting point (or epoch) and a tick rate. For example, a clock may have an epoch of January 1, 1970 and tick every second. C++ defines several clock types:

| Defined in header
| |
| Defined in namespace
`std::chrono` | |
| (C++11) |
wall clock time from the system-wide realtime clock (class) |
| (C++11) |
monotonic clock that will never be adjusted (class) |
| (C++11) |
the clock with the shortest tick period available (class) |
| (C++20) |
determines if a type is a
(class template) (variable template) |

[Clock](https://en.cppreference.com/named_req/Clock.html)for Coordinated Universal Time (UTC)(class)

[Clock](https://en.cppreference.com/named_req/Clock.html)for International Atomic Time (TAI)(class)

[Clock](https://en.cppreference.com/named_req/Clock.html)for GPS time(class)

[Clock](https://en.cppreference.com/named_req/Clock.html)used for[file time](https://en.cppreference.com/filesystem/file_time_type.html)(typedef)

(class)

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=3)] Time point

A time point is a duration of time that has passed since the epoch of a specific clock.

| Defined in header
| |
| Defined in namespace
`std::chrono` | |
| (C++11) |
a point in time (class template) |
| (C++20) |
traits class defining how to convert time points of one clock to another (class template) |
| (C++20) |
convert time points of one clock to another (function template) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=4)] Duration

A duration consists of a span of time, defined as some number of ticks of some time unit. For example, "42 seconds" could be represented by a duration consisting of 42 ticks of a 1-second time unit.

| Defined in header
| |
| Defined in namespace
`std::chrono` | |
| (C++11) |
a time interval (class template) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=5)] Time of day (since C++20)

`hh_mm_ss`

splits a duration representing time elapsed since midnight into hours, minutes, seconds, and fractional seconds, as applicable. It is primarily a formatting tool.

| Defined in header
| |
| Defined in namespace
`std::chrono` | |
| (C++20) |
represents a time of day (class template) |
| (C++20) |
translates between a 12h/24h format time of day (function) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=6)] Calendar (since C++20)

| Defined in header
| |
| Defined in namespace
`std::chrono` | |
| (C++20) |
tag class indicating the last day or weekday in a month (class) |
| (C++20) |
represents a day of a month (class) |
| (C++20) |
represents a month of a year (class) |
| (C++20) |
represents a year in the Gregorian calendar (class) |
| (C++20) |
represents a day of the week in the Gregorian calendar (class) |
| (C++20) |
represents the nth
weekday |
| (C++20) |
represents the last
weekday |

(class)

[of a specific](https://en.cppreference.com/chrono/day.html)`day``month`(class)

`month`(class)

th[of a specific](https://en.cppreference.com/chrono/weekday.html)`weekday``month`(class)

[of a specific](https://en.cppreference.com/chrono/weekday.html)`weekday``month`(class)

[of a specific](https://en.cppreference.com/chrono/month.html)`month``year`(class)

[,](https://en.cppreference.com/chrono/year.html)`year`[, and](https://en.cppreference.com/chrono/month.html)`month``day`(class)

[and](https://en.cppreference.com/chrono/year.html)`year``month`(class)

th[of a specific](https://en.cppreference.com/chrono/weekday.html)`weekday`[and](https://en.cppreference.com/chrono/year.html)`year``month`(class)

[of a specific](https://en.cppreference.com/chrono/weekday.html)`weekday`[and](https://en.cppreference.com/chrono/year.html)`year``month`(class)

(function)

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=7)] Time zone (since C++20)

| Defined in header
| |
| Defined in namespace
`std::chrono` | |
| (C++20) |
describes a copy of the
(class) |

`tzdb`(class)

(function)

[based on its name](https://en.cppreference.com/chrono/time_zone.html)`time_zone`(function)

`time_zone`(function)

(class)

(class)

(class)

(enum)

`zoned_time`(class template)

(class)

(class)

(class)

`utc_time`

object (function template)

(class)

(class)

(class)

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=8)] Literals (since C++14)

| Defined in header
| |
| Defined in inline namespace
`std::literals::chrono_literals` | |
| (C++20) |
a std::chrono::year literal representing a particular year (function) |
| (C++20) |
a std::chrono::day literal representing a day of a month (function) |
| (C++14) |
a
(function) |

[std::chrono::duration](https://en.cppreference.com/chrono/duration.html)literal representing minutes(function)

[std::chrono::duration](https://en.cppreference.com/chrono/duration.html)literal representing seconds(function)

[std::chrono::duration](https://en.cppreference.com/chrono/duration.html)literal representing milliseconds(function)

[std::chrono::duration](https://en.cppreference.com/chrono/duration.html)literal representing microseconds(function)

[std::chrono::duration](https://en.cppreference.com/chrono/duration.html)literal representing nanoseconds(function)

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=9)] Chrono I/O (since C++20)

| Defined in header
| |
| Defined in namespace
`std::chrono` | |
| (C++20) |
parses a `chrono` object from a stream (function template) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=10)] Notes

|
|---|

`__cpp_lib_chrono`

`201510L`

[std::chrono::duration](https://en.cppreference.com/chrono/duration.html)and[std::chrono::time_point](https://en.cppreference.com/chrono/time_point.html)`201611L`

[std::chrono::duration](https://en.cppreference.com/chrono/duration.html)and[std::chrono::time_point](https://en.cppreference.com/chrono/time_point.html)`201907L`

[Calendars](https://en.cppreference.com/chrono.html#Calendar)and[Time zones](https://en.cppreference.com/chrono.html#Time_zone)`202306L`

[Hashing](https://en.cppreference.com/utility/hash.html)support for`std::chrono`

value classes
### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=11)] [C-style date and time library](https://en.cppreference.com/chrono/c.html)

Also provided are the C-style date and time functions, such as [std::time_t](https://en.cppreference.com/chrono/c/time_t.html), [std::difftime](https://en.cppreference.com/chrono/c/difftime.html), and [CLOCKS_PER_SEC](https://en.cppreference.com/chrono/c/CLOCKS_PER_SEC.html).

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/chrono&action=edit§ion=12)] Example

#include <chrono> #include <iostream> long Fibonacci(unsigned n) { return n < 2 ? n : Fibonacci(n - 1) + Fibonacci(n - 2); } int main() { // Measures and displays an execution time of a function call. const auto start{[std::chrono::steady_clock::now]()}; const auto fb{Fibonacci(42)}; const auto finish{[std::chrono::steady_clock::now]()}; const[std::chrono::duration]<double> elapsed_seconds{finish - start};[std::cout]<< "Fibonacci(42): " << fb << "\nElapsed time: "; // std::cout << elapsed_seconds.count() << "s\n"; // Before C++20[std::cout]<< elapsed_seconds << '\n'; // C++20's chrono::duration operator<< // Prints UTC and local time. const auto tp_utc{[std::chrono::system_clock::now]()};[std::cout]<< "Current time 'UTC' is: " << tp_utc << "\n" "Current time 'Local' is: " <<[std::chrono::current_zone]()->to_local(tp_utc) << '\n'; }

Possible output:

Fibonacci(42): 267914296 Elapsed time: 0.728532s Current time 'UTC' is: 2025-02-10 06:22:39.420666960 Current time 'Local' is: 2025-02-10 09:22:39.420666960
