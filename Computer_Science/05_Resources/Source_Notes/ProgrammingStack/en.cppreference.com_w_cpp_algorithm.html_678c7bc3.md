Title: Algorithms library - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/algorithm.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:06:55+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# Algorithms library

[cpp](https://en.cppreference.com/cpp.html)

The algorithms library defines functions for a variety of purposes (e.g. searching, sorting, counting, manipulating) that operate on ranges of elements. Note that a [range](https://en.cppreference.com/iterator.html#Ranges) is defined as `[`

first`, `

last`)`

where last refers to the element *past* the last element to inspect or modify.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=1)] [Constrained algorithms](https://en.cppreference.com/algorithm/ranges.html) (since C++20)

C++20 provides [constrained](https://en.cppreference.com/language/constraints.html) versions of most algorithms in the namespace `std::ranges`

. In these algorithms, a [range](https://en.cppreference.com/iterator.html#Ranges) can be specified as either an [iterator](https://en.cppreference.com/iterator/input_or_output_iterator.html)-[sentinel](https://en.cppreference.com/iterator/sentinel_for.html) pair or as a single [ range](https://en.cppreference.com/ranges/range.html) argument, and projections and pointer-to-member callables are supported. Additionally, the

[return types](https://en.cppreference.com/algorithm/ranges.html#Return_types)of most algorithms have been changed to return all potentially useful information computed during the execution of the algorithm.

[std::vector]<int> v{7, 1, 4, 0, -1}; std::[ranges::sort](v); // constrained algorithm

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=2)] Execution policies (since C++17)

Most algorithms have overloads that accept execution policies. The standard library algorithms support several [execution policies](https://en.cppreference.com/algorithm/execution_policy_tag_t.html), and the library provides corresponding execution policy types and objects. Users may select an execution policy statically by invoking a parallel algorithm with an [execution policy object](https://en.cppreference.com/algorithm/execution_policy_tag.html) of the corresponding type.

Standard library implementations (but not the users) may define additional execution policies as an extension. The semantics of parallel algorithms invoked with an execution policy object of implementation-defined type is implementation-defined.

Parallel version of algorithms (except for [std::for_each](https://en.cppreference.com/algorithm/for_each.html) and [std::for_each_n](https://en.cppreference.com/algorithm/for_each_n.html)) are allowed to make arbitrary copies of elements from ranges, as long as both [std::is_trivially_copy_constructible_v](https://en.cppreference.com/types/is_copy_constructible.html)<T> and [std::is_trivially_destructible_v](https://en.cppreference.com/types/is_destructible.html)<T> are true, where `T`

is the type of elements.

| Defined in header
| |
| Defined in namespace
`std::execution` | |
| (C++17)(C++17)(C++17)(C++20) |
execution policy types (class) |
| (C++17)(C++17)(C++17)(C++20) |
global execution policy objects (constant) |
| Defined in namespace
`std` | |
| (C++17) |
test whether a class represents an execution policy (class template) |

|
|---|

`__cpp_lib_parallel_algorithm`

`201603L`

`__cpp_lib_execution`

`201603L`

`201902L`

[std::execution::unsequenced_policy](https://en.cppreference.com/algorithm/execution_policy_tag_t.html)### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=3)] Non-modifying sequence operations

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=4)] Batch operations

| Defined in header
| |
| applies a unary
(function template) |

[function object](https://en.cppreference.com/named_req/FunctionObject.html)to elements from a[range](https://en.cppreference.com/iterator.html#Ranges)(algorithm function object)

(function template)

(algorithm function object)

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=5)] Search operations

| Defined in header
| |
| (C++11)(C++11)(C++11) |
checks if a predicate is true for all, any or none of the elements in a range (function template) |
| (C++20)(C++20)(C++20) |
checks if a predicate is true for all, any or none of the elements in a range (algorithm function object) |
| (C++23)(C++23) |
checks if the range contains the given element or subrange (algorithm function object) |
| (C++11) |
finds the first element satisfying specific criteria (function template) |
| (C++20)(C++20)(C++20) |
finds the first element satisfying specific criteria (algorithm function object) |
| (C++23)(C++23)(C++23) |
finds the last element satisfying specific criteria (algorithm function object) |
| finds the last sequence of elements in a certain range (function template) | |
| (C++20) |
finds the last sequence of elements in a certain range (algorithm function object) |
| searches for any one of a set of elements (function template) | |
| (C++20) |
searches for any one of a set of elements (algorithm function object) |
| finds the first two adjacent items that are equal (or satisfy a given predicate) (function template) | |
| (C++20) |
finds the first two adjacent items that are equal (or satisfy a given predicate) (algorithm function object) |
| returns the number of elements satisfying specific criteria (function template) | |
| (C++20)(C++20) |
returns the number of elements satisfying specific criteria (algorithm function object) |
| finds the first position where two ranges differ (function template) | |
| (C++20) |
finds the first position where two ranges differ (algorithm function object) |
| determines if two sets of elements are the same (function template) | |
| (C++20) |
determines if two sets of elements are the same (algorithm function object) |
| searches for the first occurrence of a range of elements (function template) | |
| (C++20) |
searches for the first occurrence of a range of elements (algorithm function object) |
| searches for the first occurrence of a number consecutive copies of an element in a range (function template) | |
| (C++20) |
searches for the first occurrence of a number consecutive copies of an element in a range (algorithm function object) |
| (C++23) |
checks whether a range starts with another range (algorithm function object) |
| (C++23) |
checks whether a range ends with another range (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=6)] Fold operations (since C++23)

| Defined in header
| |
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

[pair](https://en.cppreference.com/algorithm/ranges/return_types/in_value_result.html)(iterator,[optional](https://en.cppreference.com/utility/optional.html))(algorithm function object)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=7)] Modifying sequence operations

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=8)] Copy operations

| Defined in header
| |
| (C++11) |
copies a range of elements to a new location (function template) |
| (C++20)(C++20) |
copies a range of elements to a new location (algorithm function object) |
| (C++11) |
copies a number of elements to a new location (function template) |
| (C++20) |
copies a number of elements to a new location (algorithm function object) |
| copies a range of elements in backwards order (function template) | |
| (C++20) |
copies a range of elements in backwards order (algorithm function object) |
| (C++11) |
moves a range of elements to a new location (function template) |
| (C++20) |
moves a range of elements to a new location (algorithm function object) |
| (C++11) |
moves a range of elements to a new location in backwards order (function template) |
| (C++20) |
moves a range of elements to a new location in backwards order (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=9)] Swap operations

| Defined in header
| |
| swaps the values of two objects (function template) | |
| Defined in header
| |
| swaps two ranges of elements (function template) | |
| (C++20) |
swaps two ranges of elements (algorithm function object) |
| swaps the elements pointed to by two iterators (function template) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=10)] Transformation operations

| Defined in header
| |
| applies a function to a range of elements, storing results in a destination range (function template) | |
| (C++20) |
applies a function to a range of elements (algorithm function object) |
| replaces all values satisfying specific criteria with another value (function template) | |
| (C++20)(C++20) |
replaces all values satisfying specific criteria with another value (algorithm function object) |
| copies a range, replacing elements satisfying specific criteria with another value (function template) | |
| (C++20)(C++20) |
copies a range, replacing elements satisfying specific criteria with another value (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=11)] Generation operations

| Defined in header
| |
| copy-assigns the given value to every element in a range (function template) | |
| (C++20) |
assigns a range of elements a certain value (algorithm function object) |
| copy-assigns the given value to N elements in a range (function template) | |
| (C++20) |
assigns a value to a number of elements (algorithm function object) |
| assigns the results of successive function calls to every element in a range (function template) | |
| (C++20) |
saves the result of a function in a range (algorithm function object) |
| assigns the results of successive function calls to N elements in a range (function template) | |
| (C++20) |
saves the result of N applications of a function (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=12)] Removing operations

| Defined in header
| |
| removes elements satisfying specific criteria (function template) | |
| (C++20)(C++20) |
removes elements satisfying specific criteria (algorithm function object) |
| copies a range of elements omitting those that satisfy specific criteria (function template) | |
| (C++20)(C++20) |
copies a range of elements omitting those that satisfy specific criteria (algorithm function object) |
| removes consecutive duplicate elements in a range (function template) | |
| (C++20) |
removes consecutive duplicate elements in a range (algorithm function object) |
| creates a copy of some range of elements that contains no consecutive duplicates (function template) | |
| (C++20) |
creates a copy of some range of elements that contains no consecutive duplicates (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=13)] Order-changing operations

| Defined in header
| |
| reverses the order of elements in a range (function template) | |
| (C++20) |
reverses the order of elements in a range (algorithm function object) |
| creates a copy of a range that is reversed (function template) | |
| (C++20) |
creates a copy of a range that is reversed (algorithm function object) |
| rotates the order of elements in a range (function template) | |
| (C++20) |
rotates the order of elements in a range (algorithm function object) |
| copies and rotate a range of elements (function template) | |
| (C++20) |
copies and rotate a range of elements (algorithm function object) |
| (C++20) |
shifts elements in a range (function template) |
| shifts elements in a range (algorithm function object) | |
| (until C++17)(C++11) |
randomly re-orders elements in a range (function template) |
| (C++20) |
randomly re-orders elements in a range (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=14)] Sampling operations

| Defined in header
| |
| (C++17) |
selects N random elements from a sequence (function template) |
| (C++20) |
selects N random elements from a sequence (algorithm function object) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=15)]

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=16)] Requirements

Some algorithms require the sequence represented by the arguments to be âsortedâ or âpartitionedâ. The behavior is undefined if the requirement is not met.

|
A sequence is
.
|
(until C++20) |
|
A sequence is
is false.
A sequence is |
(since C++20) |

A sequence `[`

start`, `

finish`)`

is *partitioned with respect to an expression f(e)* if there exists an integer n such that for all i in `[`

â0â`, `

[std::distance](https://en.cppreference.com/iterator/distance.html)(start, finish)`)`

, f(*(start + i)) [1] is true if and only if i < n.

- â
[1.0](https://en.cppreference.com/algorithm.html#cite_ref-plus_1-0)[1.1](https://en.cppreference.com/algorithm.html#cite_ref-plus_1-1)[1.2](https://en.cppreference.com/algorithm.html#cite_ref-plus_1-2)[1.3](https://en.cppreference.com/algorithm.html#cite_ref-plus_1-3)iter + n simply means âthe result of iter being incremented n timesâ, regardless of whether iter is a random access iterator.[1.4](https://en.cppreference.com/algorithm.html#cite_ref-plus_1-4)

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=17)] Partitioning operations

| Defined in header
| |
| (C++11) |
determines if the range is partitioned by the given predicate (function template) |
| (C++20) |
determines if the range is partitioned by the given predicate (algorithm function object) |
| divides a range of elements into two groups (function template) | |
| (C++20) |
divides a range of elements into two groups (algorithm function object) |
| (C++11) |
copies a range dividing the elements into two groups (function template) |
| (C++20) |
copies a range dividing the elements into two groups (algorithm function object) |
| divides elements into two groups while preserving their relative order (function template) | |
| (C++20) |
divides elements into two groups while preserving their relative order (algorithm function object) |
| (C++11) |
locates the partition point of a partitioned range (function template) |
| (C++20) |
locates the partition point of a partitioned range (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=18)] Sorting operations

| Defined in header
| |
| sorts a range into ascending order (function template) | |
| (C++20) |
sorts a range into ascending order (algorithm function object) |
| sorts a range of elements while preserving order between equal elements (function template) | |
| (C++20) |
sorts a range of elements while preserving order between equal elements (algorithm function object) |
| sorts the first N elements of a range (function template) | |
| (C++20) |
sorts the first N elements of a range (algorithm function object) |
| copies and partially sorts a range of elements (function template) | |
| (C++20) |
copies and partially sorts a range of elements (algorithm function object) |
| (C++11) |
checks whether a range is sorted into ascending order (function template) |
| (C++20) |
checks whether a range is sorted into ascending order (algorithm function object) |
| (C++11) |
finds the largest sorted subrange (function template) |
| (C++20) |
finds the largest sorted subrange (algorithm function object) |
| partially sorts the given range making sure that it is partitioned by the given element (function template) | |
| (C++20) |
partially sorts the given range making sure that it is partitioned by the given element (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=19)] Binary search operations (on partitioned ranges)

| Defined in header
| |
returns an iterator to the first element not less than the given value (function template) | |
| (C++20) |
returns an iterator to the first element not less than the given value(algorithm function object) |
returns an iterator to the first element greater than a certain value (function template) | |
| (C++20) |
returns an iterator to the first element greater than a certain value(algorithm function object) |
| returns range of elements matching a specific key (function template) | |
| (C++20) |
returns range of elements matching a specific key (algorithm function object) |
| determines if an element exists in a partially-ordered range (function template) | |
| (C++20) |
determines if an element exists in a partially-ordered range (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=20)] Set operations (on sorted ranges)

| Defined in header
| |
| returns true if one sequence is a subsequence of another (function template) | |
| (C++20) |
returns true if one sequence is a subsequence of another (algorithm function object) |
| computes the union of two sets (function template) | |
| (C++20) |
computes the union of two sets (algorithm function object) |
| computes the intersection of two sets (function template) | |
| (C++20) |
computes the intersection of two sets (algorithm function object) |
| computes the difference between two sets (function template) | |
| (C++20) |
computes the difference between two sets (algorithm function object) |
| computes the symmetric difference between two sets (function template) | |
| computes the symmetric difference between two sets (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=21)] Merge operations (on sorted ranges)

| Defined in header
| |
| merges two sorted ranges (function template) | |
| (C++20) |
merges two sorted ranges (algorithm function object) |
| merges two ordered ranges in-place (function template) | |
| (C++20) |
merges two ordered ranges in-place (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=22)] Heap operations

|
A random access |
(until C++20) |
|
A random access A random access |
(since C++20) |

A heap can be created by [std::make_heap](https://en.cppreference.com/algorithm/make_heap.html) and [ranges::make_heap](https://en.cppreference.com/algorithm/ranges/make_heap.html)(since C++20).

For more properties of heap, see [max heap](https://en.wikipedia.org/wiki/Binary_heap).

| Defined in header
| |
| adds an element to a max heap (function template) | |
| (C++20) |
adds an element to a max heap (algorithm function object) |
| removes the largest element from a max heap (function template) | |
| (C++20) |
removes the largest element from a max heap (algorithm function object) |
| creates a max heap out of a range of elements (function template) | |
| (C++20) |
creates a max heap out of a range of elements (algorithm function object) |
| turns a max heap into a range of elements sorted in ascending order (function template) | |
| (C++20) |
turns a max heap into a range of elements sorted in ascending order (algorithm function object) |
| (C++11) |
checks if the given range is a max heap (function template) |
| (C++20) |
checks if the given range is a max heap (algorithm function object) |
| (C++11) |
finds the largest subrange that is a max heap (function template) |
| (C++20) |
finds the largest subrange that is a max heap (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=23)] Minimum/maximum operations

| Defined in header
| |
| returns the greater of the given values (function template) | |
| (C++20) |
returns the greater of the given values (algorithm function object) |
| returns the largest element in a range (function template) | |
| (C++20) |
returns the largest element in a range (algorithm function object) |
| returns the smaller of the given values (function template) | |
| (C++20) |
returns the smaller of the given values (algorithm function object) |
| returns the smallest element in a range (function template) | |
| (C++20) |
returns the smallest element in a range (algorithm function object) |
| (C++11) |
returns the smaller and larger of two elements (function template) |
| (C++20) |
returns the smaller and larger of two elements (algorithm function object) |
| (C++11) |
returns the smallest and the largest elements in a range (function template) |
| (C++20) |
returns the smallest and the largest elements in a range (algorithm function object) |
| (C++17) |
clamps a value between a pair of boundary values (function template) |
| (C++20) |
clamps a value between a pair of boundary values (algorithm function object) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=24)] Lexicographical comparison operations

| Defined in header
| |
| returns true if one range is lexicographically less than another (function template) | |
| returns true if one range is lexicographically less than another (algorithm function object) | |
| compares two ranges using three-way comparison (function template) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=25)] Permutation operations

| Defined in header
| |
| generates the next greater lexicographic permutation of a range of elements (function template) | |
| (C++20) |
generates the next greater lexicographic permutation of a range of elements (algorithm function object) |
| generates the next smaller lexicographic permutation of a range of elements (function template) | |
| (C++20) |
generates the next smaller lexicographic permutation of a range of elements (algorithm function object) |
| (C++11) |
determines if a sequence is a permutation of another sequence (function template) |
| (C++20) |
determines if a sequence is a permutation of another sequence (algorithm function object) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=26)] Numeric operations

| Defined in header
| |
| (C++11) |
fills a range with successive increments of the starting value (function template) |
| (C++23) |
fills a range with successive increments of the starting value (algorithm function object) |
| sums up or folds a range of elements (function template) | |
| computes the inner product of two ranges of elements (function template) | |
| computes the differences between adjacent elements in a range (function template) | |
| computes the partial sum of a range of elements (function template) | |
| (C++17) |
similar to
(function template) |

[std::partial_sum](https://en.cppreference.com/algorithm/partial_sum.html), excludes the ithinput element from the ithsum(function template)

[std::partial_sum](https://en.cppreference.com/algorithm/partial_sum.html), includes the ithinput element in the ithsum(function template)

(function template)

(function template)

(function template)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=27)] Operations on uninitialized memory

| Defined in header
| |
| copies a range of objects to an uninitialized area of memory (function template) | |
| (C++20) |
copies a range of objects to an uninitialized area of memory (algorithm function object) |
| (C++11) |
copies a number of objects to an uninitialized area of memory (function template) |
| (C++20) |
copies a number of objects to an uninitialized area of memory (algorithm function object) |
| copies an object to an uninitialized area of memory, defined by a range (function template) | |
| (C++20) |
copies an object to an uninitialized area of memory, defined by a range (algorithm function object) |
| copies an object to an uninitialized area of memory, defined by a start and a count (function template) | |
| (C++20) |
copies an object to an uninitialized area of memory, defined by a start and a count (algorithm function object) |
| (C++17) |
moves a range of objects to an uninitialized area of memory (function template) |
| (C++20) |
moves a range of objects to an uninitialized area of memory (algorithm function object) |
| (C++17) |
moves a number of objects to an uninitialized area of memory (function template) |
| (C++20) |
moves a number of objects to an uninitialized area of memory (algorithm function object) |
| constructs objects by
(function template) |

[default-initialization](https://en.cppreference.com/language/default_initialization.html)in an uninitialized area of memory, defined by a range(algorithm function object)

[default-initialization](https://en.cppreference.com/language/default_initialization.html)in an uninitialized area of memory, defined by a start and a count(function template)

[default-initialization](https://en.cppreference.com/language/default_initialization.html)in an uninitialized area of memory, defined by a start and count(algorithm function object)

[value-initialization](https://en.cppreference.com/language/value_initialization.html)in an uninitialized area of memory, defined by a range(function template)

[value-initialization](https://en.cppreference.com/language/value_initialization.html)in an uninitialized area of memory, defined by a range(algorithm function object)

[value-initialization](https://en.cppreference.com/language/value_initialization.html)in an uninitialized area of memory, defined by a start and a count(function template)

[value-initialization](https://en.cppreference.com/language/value_initialization.html)in an uninitialized area of memory, defined by a start and a count(algorithm function object)

(function template)

(algorithm function object)

(function template)

(algorithm function object)

(function template)

(algorithm function object)

(function template)

(algorithm function object)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=28)] Random number generation (since C++26)

| Defined in header
| |
| (C++26) |
fills a range with random numbers from a uniform random bit generator (algorithm function object) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=29)] Notes

|
|---|

`__cpp_lib_algorithm_iterator_requirements`

`202207L`

`__cpp_lib_clamp`

`201603L`

[std::clamp](https://en.cppreference.com/algorithm/clamp.html)`__cpp_lib_constexpr_algorithms`

`201806L`

`202306L`

`__cpp_lib_algorithm_default_value_type`

`202403L`

[List-initialization](https://en.cppreference.com/language/list_initialization.html)for algorithms`__cpp_lib_freestanding_algorithm`

`202311L`

`<algorithm>``__cpp_lib_robust_nonmodifying_seq_ops`

`201304L`

[std::mismatch](https://en.cppreference.com/algorithm/mismatch.html),[std::equal](https://en.cppreference.com/algorithm/equal.html)and std::is_permutation)`__cpp_lib_sample`

`201603L`

[std::sample](https://en.cppreference.com/algorithm/sample.html)`__cpp_lib_shift`

`201806L`

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=30)] C library

| Defined in header
| |
| sorts a range of elements with unspecified type (function) | |
| searches an array for an element of unspecified type (function) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=31)] Defect reports

The following behavior-changing defect reports were applied retroactively to previously published C++ standards.

| DR | Applied to | Behavior as published | Correct behavior |
|---|---|---|---|
|

equal to *first

[LWG 2150](https://cplusplus.github.io/LWG/issue2150)[LWG 2166](https://cplusplus.github.io/LWG/issue2166)definition of

[max heap](https://en.wikipedia.org/wiki/Binary_heap)closely enough### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/algorithm&action=edit§ion=32)] See also

|
|
