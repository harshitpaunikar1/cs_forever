Title: Constrained algorithms (since C++20) - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/algorithm/ranges.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:06:57+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# Constrained algorithms (since C++20)

C++20 provides [constrained](https://en.cppreference.com/language/constraints.html) versions of most algorithms in the namespace `std::ranges`

. In these algorithms, a range can be specified as either an [iterator](https://en.cppreference.com/iterator/input_or_output_iterator.html)-[sentinel](https://en.cppreference.com/iterator/sentinel_for.html) pair or as a single [ range](https://en.cppreference.com/ranges/range.html) argument, and projections and pointer-to-member callables are supported. Additionally, the

[return types](https://en.cppreference.com/ranges.html#Return_types)of most algorithms have been changed to return all potentially useful information computed during the execution of the algorithm.

## Contents |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm/ranges&action=edit§ion=1)] Algorithm function objects

An *algorithm function object* (AFO), informally known as *niebloid*, is a [customization point object](https://en.cppreference.com/ranges/cpo.html) (CPO) that is specified as one or more overloaded function templates. The name of these function templates designates the corresponding algorithm function object.

For an algorithm function object o, let `S`

be the corresponding set of function templates. Then for any sequence of arguments args..., o(args...) is [expression-equivalent](https://en.cppreference.com/language/expressions.html#Expression-equivalence) to s(args...), where the result of name lookup for s is the overload set `S`

.

The constrained algorithms in the namespace `std::ranges`

are defined as algorithm function objects. As a result:

- Explicit template argument lists cannot be specified when calling any of them.
- None of them are visible to
[argument-dependent lookup](https://en.cppreference.com/language/adl.html). - When any of them are found by
[normal unqualified lookup](https://en.cppreference.com/language/unqualified_lookup.html)as the name to the left of the function-call operator,[argument-dependent lookup](https://en.cppreference.com/language/adl.html)is inhibited.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm/ranges&action=edit§ion=2)] Constrained algorithms

| Defined in header
| |
| Defined in namespace
`std::ranges` | |
## Non-modifying sequence operations | |
| (C++20)(C++20)(C++20) |
checks if a predicate is true for all, any or none of the elements in a range (algorithm function object) |
| (C++20) |
applies a unary
(algorithm function object) |

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

##### Modifying sequence operations

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

##### Partitioning operations

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

##### Sorting operations

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

##### Binary search operations (on sorted ranges)

*not less*than the given value(algorithm function object)

*greater*than a certain value(algorithm function object)

(algorithm function object)

(algorithm function object)

##### Set operations (on sorted ranges)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

##### Heap operations

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

##### Minimum/maximum operations

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

##### Permutation operations

(algorithm function object)

(algorithm function object)

(algorithm function object)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm/ranges&action=edit§ion=3)] Constrained numeric operations

| Defined in header
| |
| Defined in namespace
`std::ranges` | |
| (C++23) |
fills a range with successive increments of the starting value (algorithm function object) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm/ranges&action=edit§ion=4)] Constrained fold operations

| Defined in header
| |
| Defined in namespace
`std::ranges` | |
| (C++23) |
left-folds a range of elements (algorithm function object) |
| (C++23) |
left-folds a range of elements using the first element as an initial value (algorithm function object) |
| (C++23) |
right-folds a range of elements (algorithm function object) |
| (C++23) |
right-folds a range of elements using the last element as an initial value (algorithm function object) |
| (C++23) |
left-folds a range of elements, and returns a
(algorithm function object) |

[pair](https://en.cppreference.com/ranges/return_types/in_value_result.html)(iterator,[optional](https://en.cppreference.com/utility/optional.html))(algorithm function object)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm/ranges&action=edit§ion=5)] Constrained uninitialized memory algorithms

| Defined in header
| |
| Defined in namespace
`std::ranges` | |
| (C++20) |
copies a range of objects to an uninitialized area of memory (algorithm function object) |
| (C++20) |
copies a number of objects to an uninitialized area of memory (algorithm function object) |
| (C++20) |
copies an object to an uninitialized area of memory, defined by a range (algorithm function object) |
| (C++20) |
copies an object to an uninitialized area of memory, defined by a start and a count (algorithm function object) |
| (C++20) |
moves a range of objects to an uninitialized area of memory (algorithm function object) |
| (C++20) |
moves a number of objects to an uninitialized area of memory (algorithm function object) |
| constructs objects by
(algorithm function object) |

[default-initialization](https://en.cppreference.com/language/default_initialization.html)in an uninitialized area of memory, defined by a start and count(algorithm function object)

[value-initialization](https://en.cppreference.com/language/value_initialization.html)in an uninitialized area of memory, defined by a range(algorithm function object)

[value-initialization](https://en.cppreference.com/language/value_initialization.html)in an uninitialized area of memory, defined by a start and a count(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

(algorithm function object)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm/ranges&action=edit§ion=6)] Constrained random number algorithms

| Defined in header
| |
| Defined in namespace
`std::ranges` | |
| (C++26) |
fills a range with random numbers from a uniform random bit generator (algorithm function object) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm/ranges&action=edit§ion=7)] Return types

| Defined in header
| |
| Defined in namespace
`std::ranges` | |
| (C++20) |
provides a way to store an iterator and a function object as a single unit (class template) |
| (C++20) |
provides a way to store two iterators as a single unit (class template) |
| (C++20) |
provides a way to store two iterators as a single unit (class template) |
| (C++20) |
provides a way to store three iterators as a single unit (class template) |
| (C++20) |
provides a way to store three iterators as a single unit (class template) |
| (C++20) |
provides a way to store two objects or references of the same type as a single unit (class template) |
| (C++20) |
provides a way to store an iterator and a boolean flag as a single unit (class template) |
| (C++23) |
provides a way to store an iterator and a value as a single unit (class template) |
| (C++23) |
provides a way to store an iterator and a value as a single unit (class template) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm/ranges&action=edit§ion=8)] Notes

|
|---|

`__cpp_lib_algorithm_default_value_type`

`202403L`

[List-initialization](https://en.cppreference.com/language/list_initialization.html)for algorithms`__cpp_lib_ranges`

`201911L`

[Ranges library](https://en.cppreference.com/ranges.html)and[constrained algorithms](https://en.cppreference.com/ranges.html#Top)`__cpp_lib_ranges_contains`

`202207L`

`__cpp_lib_ranges_find_last`

`202207L`

`__cpp_lib_ranges_fold`

`202207L`

`std::ranges`

[fold algorithms](https://en.cppreference.com/ranges.html#Constrained_fold_operations)`__cpp_lib_ranges_iota`

`202202L`

`__cpp_lib_ranges_starts_ends_with`

`202106L`

`__cpp_lib_shift`

`201806L`

`202202L`

`__cpp_lib_ranges_generate_random`

`202403L`

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm/ranges&action=edit§ion=9)] Defect reports

The following behavior-changing defect reports were applied retroactively to previously published C++ standards.

| DR | Applied to | Behavior as published | Correct behavior |
|---|---|---|---|
|

other than function objects
