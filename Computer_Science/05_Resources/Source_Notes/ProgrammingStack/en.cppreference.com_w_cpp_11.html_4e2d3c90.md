Title: C++11 - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/11.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:06:43+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# C++11

[cpp](https://en.cppreference.com/cpp.html)

**C++11** is the second major version of C++ and the most important update since C++98. A large number of changes were introduced to both standardize existing practices and improve the abstractions available to the C++ programmers.

Before it was finally approved by ISO on 12 August 2011, the name 'C++0x' was used because it was expected to be published before 2010. It took 8 years between C++03 and C++11, so it has become the longest interval between versions so far. Since then, currently, C++ updates every 3 years regularly.

| This section is incomplete |

Following features were merged into C++11:

- From
[TR1](https://en.cppreference.com/experimental.html): all of TR1 except[Special Functions](https://en.cppreference.com/numeric/special_math.html). - From Boost:
[The thread library](https://en.cppreference.com/atomic.html),,`exception_ptr`and`error_code`, iterator improvements (`error_condition`,`begin`,`end`,`next`)`prev` - From C: C-style Unicode conversion functions

## Contents |

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/11&action=edit§ion=1)] Core language features

-
and`auto``decltype` -
[defaulted](https://en.cppreference.com/language/function.html#Function_definition)and[deleted](https://en.cppreference.com/language/function.html#Deleted_functions)functions -
and`final``override` -
[trailing return type](https://en.cppreference.com/language/function.html#Function_declaration) -
[rvalue references](https://en.cppreference.com/language/reference.html) -
[move constructors](https://en.cppreference.com/language/move_constructor.html)and[move assignment operators](https://en.cppreference.com/language/move_operator.html) -
[scoped enums](https://en.cppreference.com/language/enum.html) -
and`constexpr`[literal types](https://en.cppreference.com/named_req/LiteralType.html) -
[list initialization](https://en.cppreference.com/language/list_initialization.html) -
[delegating](https://en.cppreference.com/language/initializer_list.html#Delegating_constructor)and[inherited](https://en.cppreference.com/language/using_declaration.html)constructors - brace-or-equal
[initializers](https://en.cppreference.com/language/initialization.html) -
`nullptr` -
`long long` -
[char16_t and char32_t](https://en.cppreference.com/language/types.html#Character_types) -
[type aliases](https://en.cppreference.com/language/type_alias.html) -
[variadic templates](https://en.cppreference.com/language/parameter_pack.html) -
[generalized (non-trivial) unions](https://en.cppreference.com/language/union.html) -
[generalized PODs](https://en.cppreference.com/named_req/PODType.html)([trivial types](https://en.cppreference.com/named_req/TrivialType.html)and[standard-layout types](https://en.cppreference.com/named_req/StandardLayoutType.html)) -
[Unicode string literals](https://en.cppreference.com/language/string_literal.html) -
[user-defined literals](https://en.cppreference.com/language/user_literal.html) -
[attributes](https://en.cppreference.com/language/attributes.html) -
[lambda expressions](https://en.cppreference.com/language/lambda.html) -
specifier and`noexcept`operator`noexcept` -
and`alignof``alignas` - multithreaded
[memory model](https://en.cppreference.com/language/memory_model.html) -
[thread-local storage](https://en.cppreference.com/language/storage_duration.html#Storage_duration) -
[GC interface](https://en.cppreference.com/memory.html#Garbage_collector_support_.28until_C.2B.2B23.29)(removed in C++23) -
[range-for](https://en.cppreference.com/language/range-for.html)(based on Boost library) -
(based on Boost library)`static_assert`

| This section is incomplete |

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/11&action=edit§ion=2)] Library features

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/11&action=edit§ion=3)] Headers

-
`<array>` -
`<atomic>` -
`<cfenv>` -
`<chrono>` -
`<cinttypes>` -
`<condition_variable>` -
`<cstdint>` -
`<cuchar>` -
`<forward_list>` -
`<future>` -
`<initializer_list>` -
`<mutex>` -
`<random>` -
`<ratio>` -
`<regex>` -
`<scoped_allocator>` -
`<system_error>` -
`<thread>` -
`<tuple>` -
`<typeindex>` -
`<type_traits>` -
`<unordered_map>` -
`<unordered_set>`

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/11&action=edit§ion=4)] Library features

-
[concurrency support library](https://en.cppreference.com/atomic.html) -
`emplace()`

and other use of rvalue references throughout all parts of the existing library -
[std::unique_ptr](https://en.cppreference.com/memory/unique_ptr.html) -
[std::move_iterator](https://en.cppreference.com/iterator/move_iterator.html) -
[std::initializer_list](https://en.cppreference.com/utility/initializer_list.html) -
[stateful](https://en.cppreference.com/named_req/Allocator.html#Stateful_and_stateless_allocators)and[scoped](https://en.cppreference.com/memory/scoped_allocator_adaptor.html)allocators -
[std::forward_list](https://en.cppreference.com/container/forward_list.html) -
[chrono library](https://en.cppreference.com/chrono.html) -
[ratio library](https://en.cppreference.com/utility/ratio.html) - new
[algorithms](https://en.cppreference.com/algorithm.html):

-
[std::all_of](https://en.cppreference.com/algorithm/none_of.html),[std::any_of](https://en.cppreference.com/algorithm/none_of.html),[std::none_of](https://en.cppreference.com/algorithm/none_of.html), -
[std::find_if_not](https://en.cppreference.com/algorithm/find.html), -
[std::copy_if](https://en.cppreference.com/algorithm/copy.html),[std::copy_n](https://en.cppreference.com/algorithm/copy_n.html), -
,`std::move`[std::move_backward](https://en.cppreference.com/algorithm/move_backward.html), -
[std::random_shuffle](https://en.cppreference.com/algorithm/random_shuffle.html),[std::shuffle](https://en.cppreference.com/algorithm/random_shuffle.html), -
[std::is_partitioned](https://en.cppreference.com/algorithm/is_partitioned.html),[std::partition_copy](https://en.cppreference.com/algorithm/partition_copy.html),[std::partition_point](https://en.cppreference.com/algorithm/partition_point.html), -
[std::is_sorted](https://en.cppreference.com/algorithm/is_sorted.html),[std::is_sorted_until](https://en.cppreference.com/algorithm/is_sorted_until.html), -
[std::is_heap](https://en.cppreference.com/algorithm/is_heap.html),[std::is_heap_until](https://en.cppreference.com/algorithm/is_heap_until.html), -
[std::minmax](https://en.cppreference.com/algorithm/minmax.html),[std::minmax_element](https://en.cppreference.com/algorithm/minmax_element.html), -
[std::is_permutation](https://en.cppreference.com/algorithm/is_permutation.html), -
[std::iota](https://en.cppreference.com/algorithm/iota.html), -
[std::uninitialized_copy_n](https://en.cppreference.com/memory/uninitialized_copy_n.html)

-

-
[Unicode conversion facets](https://en.cppreference.com/locale.html#Locale-independent_unicode_conversion_facets) -
[std::function](https://en.cppreference.com/utility/functional/function.html) -
[std::exception_ptr](https://en.cppreference.com/error/exception_ptr.html) -
[std::error_code](https://en.cppreference.com/error/error_code.html)and[std::error_condition](https://en.cppreference.com/error/error_condition.html) -
[iterator](https://en.cppreference.com/iterator.html)improvements:

| This section is incomplete |

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/11&action=edit§ion=5)] Defect reports

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/11&action=edit§ion=6)] Compiler support

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/11&action=edit§ion=T-1)] C++11 core language features

| C++11 feature |
Paper(s) |
GCC |
Clang |
MSVC |
Apple Clang |
EDG eccp |
Intel C++ |
Nvidia HPC C++ (ex PGI)* |
Nvidia nvcc |
Cray |
Embarcadero C++ Builder |
IBM Open XL C++ for AIX |
IBM Open XL C++ for z/OS |
IBM XL C++ |
Sun/Oracle C++ |
HP aCC |
Digital Mars C++ |
|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| C99
|

[N1653](https://wg21.link/N1653)19.26*

[(](https://en.cppreference.com/language/static_assert.html)`static_assert`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_static_assert))*[N1720](https://wg21.link/N1720)[N1757](https://wg21.link/N1757)[declarations](https://en.cppreference.com/language/friend.html)`friend`[N1791](https://wg21.link/N1791)12.0

[long long](https://en.cppreference.com/language/types.html#long_long)

[N1811](https://wg21.link/N1811)`auto`[N1984](https://wg21.link/N1984)12.0

[Delegating constructors](https://en.cppreference.com/language/initializer_list.html#Delegating_constructor)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_delegating_constructors))*[N1986](https://wg21.link/N1986)[N1987](https://wg21.link/N1987)[(](https://en.cppreference.com/language/constexpr.html)`constexpr`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))*[N2235](https://wg21.link/N2235)14.0

13.1

[char16_t](https://en.cppreference.com/language/types.html#char16_t)

and [char32_t](https://en.cppreference.com/language/types.html#char32_t)

([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_unicode_characters))*[N2249](https://wg21.link/N2249)14.0

[type traits](https://en.cppreference.com/meta.html#Type_traits). N2255*[N2255](https://wg21.link/N2255)[N2984](https://wg21.link/N2984)[N3142](https://wg21.link/N3142)4.8 (partial)*

5

(partial)*

19.0 (2015)*

[Template aliases](https://en.cppreference.com/language/type_alias.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_alias_templates))*[N2258](https://wg21.link/N2258)`alignas`[N2341](https://wg21.link/N2341)`alignof`[N2341](https://wg21.link/N2341)[N2346](https://wg21.link/N2346)[Strongly-typed](https://en.cppreference.com/language/enum.html#Scoped_enumerations)`enum`

[N2347](https://wg21.link/N2347)17.0*

[Atomic operations](https://en.cppreference.com/atomic.html#Atomic_operations)[N2427](https://wg21.link/N2427)`nullptr`[N2431](https://wg21.link/N2431)[conversion operators](https://en.cppreference.com/language/cast_operator.html)[N2437](https://wg21.link/N2437)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_ref_qualifiers))*[N2439](https://wg21.link/N2439)[string literals](https://en.cppreference.com/language/string_literal.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_raw_strings))*[N2442](https://wg21.link/N2442)13.1.1*

[string literals](https://en.cppreference.com/language/string_literal.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_unicode_literals))*[N2442](https://wg21.link/N2442)[Inline namespaces](https://en.cppreference.com/language/namespace.html#Inline_namespaces)[N2535](https://wg21.link/N2535)[Inheriting constructors](https://en.cppreference.com/language/using_declaration.html#Inheriting_constructors)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_inheriting_constructors))*[N2540](https://wg21.link/N2540)[Trailing function return types](https://en.cppreference.com/language/function.html#Function_declaration)[N2541](https://wg21.link/N2541)`union`s[N2544](https://wg21.link/N2544)[Variadic templates](https://en.cppreference.com/language/parameter_pack.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_variadic_templates))*[N2242](https://wg21.link/N2242)[N2555](https://wg21.link/N2555)4.4

4.3

[Expression SFINAE](https://en.cppreference.com/language/sfinae.html#Expression_SFINAE)[N2634](https://wg21.link/N2634)[N2657](https://wg21.link/N2657)[Thread-local storage](https://en.cppreference.com/language/storage_duration.html)[N2659](https://wg21.link/N2659)4.8

19.0 (2015)*

15.0*

13.1.2 (partial)*

[magic statics](https://en.cppreference.com/language/storage_duration.html#Static_local_variables)) ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_threadsafe_static_init))*[N2660](https://wg21.link/N2660)[N2670](https://wg21.link/N2670)[Initializer lists](https://en.cppreference.com/language/list_initialization.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_initializer_lists))*[N2672](https://wg21.link/N2672)14.0

[Non-static data member initializers](https://en.cppreference.com/language/data_members.html#Member_initialization)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_nsdmi))*[N2756](https://wg21.link/N2756)[Attributes](https://en.cppreference.com/language/attributes.html),`[[`[noreturn](https://en.cppreference.com/language/attributes/noreturn.html)]]

([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_attributes))*[N2761](https://wg21.link/N2761)`[[`[carries_dependency](https://en.cppreference.com/language/attributes/carries_dependency.html)]]

[N2556](https://wg21.link/N2556)[N2643](https://wg21.link/N2643)[Forward (opaque)](https://en.cppreference.com/language/enum.html)`enum`

declarations[N2764](https://wg21.link/N2764)14.0

[User-defined literals](https://en.cppreference.com/language/user_literal.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_user_defined_literals))*[N2765](https://wg21.link/N2765)[Rvalue references](https://en.cppreference.com/language/reference.html#Rvalue_references)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_rvalue_references))*[N2118](https://wg21.link/N2118)[N2844](https://wg21.link/N2844)[CWG1138](https://wg21.link/CWG1138)4.5

17.0*

12.0 (partial)*

14.0

[Lambda expressions](https://en.cppreference.com/language/lambda.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lambdas))*[N2550](https://wg21.link/N2550)[N2658](https://wg21.link/N2658)[N2927](https://wg21.link/N2927)17.0*

[Range-for loop](https://en.cppreference.com/language/range-for.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_range_based_for))*[N2930](https://wg21.link/N2930)[N3271](https://wg21.link/N3271)`noexcept`[N3050](https://wg21.link/N3050)[special](https://en.cppreference.com/language/member_functions.html#Special_member_functions)[member](https://en.cppreference.com/language/move_constructor.html)[functions](https://en.cppreference.com/language/move_operator.html)[N3053](https://wg21.link/N3053)[and](https://en.cppreference.com/language/override.html)`override``final`[N2928](https://wg21.link/N2928)[N3206](https://wg21.link/N3206)[N3272](https://wg21.link/N3272)17.0*

14.0

[(](https://en.cppreference.com/language/decltype.html)`decltype`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_decltype))*[N2343](https://wg21.link/N2343)[N3276](https://wg21.link/N3276)4.8.1

17.0*

4.8

12.0

C++11 feature

Paper(s)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/11&action=edit§ion=T-2)] C++11 library features

| C++11 feature |
Paper(s) |
GCC libstdc++ |
Clang libc++ |
MSVC STL |
Apple Clang* |
IBM Open XL C/C++ for AIX* |
Sun/Oracle C++* |
Embarcadero C++ Builder* |
|
|---|---|---|---|---|---|---|---|---|---|
|

[N1429](https://wg21.link/N1429)[Type traits](https://en.cppreference.com/meta.html#Type_traits). N1836*[N1836](https://wg21.link/N1836)[N2240](https://wg21.link/N2240)[N2244](https://wg21.link/N2244)[N2255](https://wg21.link/N2255)[N2342](https://wg21.link/N2342)[N2984](https://wg21.link/N2984)[N3142](https://wg21.link/N3142)4.8 (partial)*

5

(partial)*

19.0 (2015)*

`cbegin`

, `cend`

, `crbegin`

, and `crend`

of containers
[N1913](https://wg21.link/N1913)[LWG1192](https://wg21.link/LWG1192)4.5

[Garbage Collection](https://en.cppreference.com/header/memory.html#Functions)and Reachability-Based Leak Detection ([library support](https://en.cppreference.com/memory.html#Garbage_collector_support))[N2670](https://wg21.link/N2670)(no-op)*

(no-op)*

(no-op)*

(no-op)*

[Money, Time, and hexfloat I/O manipulators](https://en.cppreference.com/io/manip.html)[N2071](https://wg21.link/N2071)[N2072](https://wg21.link/N2072)[COW (copy-on-write)](https://en.cppreference.com/language/acronyms.html)[std::basic_string](https://en.cppreference.com/string/basic_string.html)[N2668](https://wg21.link/N2668)C++11 feature

Paper(s)

* - hover over a cell marked with the star * to see additional pop-up notes.

DR*nn* - the number *nn* after "DR" denotes target C++ revision the Defect Report is applied to, e.g., DR20 → C++20.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/11&action=edit§ion=7)] External links

| 1. |
|
