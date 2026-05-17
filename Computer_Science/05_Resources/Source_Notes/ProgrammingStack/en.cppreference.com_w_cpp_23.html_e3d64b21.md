Title: C++23 - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/23.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:06:50+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# C++23

From cppreference.com

<

[cpp](https://en.cppreference.com/cpp.html)The current revision of the C++ standard.

| This section is incomplete Reason: Check that all significant features are mentioned (using the Compiler Support tables below). Add more links and maybe regroup some lines. |

## Contents |

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=1)] New language features

- New
[language feature testing macros](https://en.cppreference.com/experimental/feature_test.html#Language_features) -
[Explicit object parameter](https://en.cppreference.com/language/function.html#Explicit_object_parameter),[explicit object member functions](https://en.cppreference.com/language/member_functions.html#Explicit_object_member_functions), a.k.a. "deducing this" ([P0847R7](https://wg21.link/P0847R7)) -
[Multidimensional subscript operator](https://en.cppreference.com/language/operators.html#Array_subscript_operator)(e.g. v[1, 3, 7] = 42;) ([P2128R6](https://wg21.link/P2128R6)) - static operator[] (
[P2589R1](https://wg21.link/P2589R1)), static operator(), and static lambdas ([P1169R4](https://wg21.link/P1169R4)) - auto(x) and auto{x}:
[decay-copy](https://en.cppreference.com/language/explicit_cast.html#Syntax)in the language ([P0849R8](https://wg21.link/P0849R8)) - Assumptions via new attribute
`[[`

([assume](https://en.cppreference.com/language/attributes/assume.html)(*expression*)]][P1774R8](https://wg21.link/P1774R8)) - Attributes on
[lambda-expressions](https://en.cppreference.com/language/lambda.html#Syntax)([P2173R1](https://wg21.link/P2173R1)) - Optional
[extended floating-point types](https://en.cppreference.com/types/floating-point.html): std::float{16|32|64|128}_t, and[std::bfloat16_t](https://en.cppreference.com/types/floating-point.html)([P1467R9](https://wg21.link/P1467R9)) - New preprocessor directives:
(`#elifdef`

,`#elifndef`

[P2334R1](https://wg21.link/P2334R1)), and(`#warning`[P2437R1](https://wg21.link/P2437R1)) -
[Literal suffix '](https://en.cppreference.com/language/integer_literal.html#The_type_of_the_literal)for (signed)`Z`

'/'`z`

'[std::size_t](https://en.cppreference.com/types/size_t.html)literals ([P0330R8](https://wg21.link/P0330R8)), e.g. auto ouz = 0uz; - White-spaces trimming before line splicing. (
[P2223R2](https://wg21.link/P2223R2)) - Simpler implicit move (
[P2266R3](https://wg21.link/P2266R3)) - Extending the lifetime of temporaries in range-based for loop initializer (
[P2718R0](https://wg21.link/P2718R0)) - CTAD from inherited constructors (
[P2582R1](https://wg21.link/P2582R1)) - Labels at the end of compound statements (
[P2324R2](https://wg21.link/P2324R2)), e.g.

- void f(int& x)

{

if (x)

goto END;

x = 42;

END:

}

- Alias declarations (using) in init-statements (
[P2360R0](https://wg21.link/P2360R0)), e.g.

- for (using T = int; T e : v)

/* ... */

- Make

more optional for lambda expressions (**()**[P1102R2](https://wg21.link/P1102R2)) - Narrowing contextual conversions to bool in static_assert and if constexpr (
[P1401R5](https://wg21.link/P1401R5)) - Make declaration order layout (of non-static class data members) mandated (
[P1847R4](https://wg21.link/P1847R4)) - Text encoding changes:
-
[Character sets and encodings](https://en.cppreference.com/language/charset.html)([P2314R4](https://wg21.link/P2314R4)) - Consistent character literal encoding (
[P2316R2](https://wg21.link/P2316R2)) -
[Named universal character escapes](https://en.cppreference.com/language/escape.html#Named_universal_character_escapes), e.g. "\N{CAT FACE}" for "ð±" ([P2071R2](https://wg21.link/P2071R2)) -
[Delimited escape sequences](https://en.cppreference.com/language/escape.html), e.g. "\o{7777}", "\x{C0DE}", "\u{CAFE}" ([P2290R3](https://wg21.link/P2290R3)) -
[Support for UTF-8 as a portable source file encoding](https://en.cppreference.com/language/translation_phases.html#Phase_1)([P2295R6](https://wg21.link/P2295R6))

-
-
/`if consteval`(`if not consteval`[P1938R3](https://wg21.link/P1938R3)) - constexpr changes:
- Non-literal variables, labels, and gotos in constexpr functions (
[P2242R3](https://wg21.link/P2242R3)) - Permitting static and thread_local variables in constant expressions in constexpr functions (
[P2647R1](https://wg21.link/P2647R1)) - constexpr function does not need its return type and parameter types to be literal type (
[P2448R2](https://wg21.link/P2448R2)) - constexpr function for which no invocation satisfies the requirements of a core constant expression (
[P2448R2](https://wg21.link/P2448R2))

- Non-literal variables, labels, and gotos in constexpr functions (

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=2)] New library features

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=3)] New modules

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=4)] New headers

C compatibility headers:

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=5)] Library features

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=6)] General Utilities

-
[std::expected](https://en.cppreference.com/utility/expected.html): a new vocabulary type to return a function's result () (`<expected>`[P0323R12](https://wg21.link/P0323R12),[P2549R1](https://wg21.link/P2549R1)) -
[std::move_only_function](https://en.cppreference.com/utility/functional/move_only_function.html): a move-only callable wrapper ([P0288R9](https://wg21.link/P0288R9)) -
[std::bind_back](https://en.cppreference.com/utility/functional/bind_front.html): a call wrapper ([P2387R3](https://wg21.link/p2387r3)) -
[std::byteswap](https://en.cppreference.com/numeric/byteswap.html): reverses the bytes ([P1272R4](https://wg21.link/P1272R4)) -
[std::forward_like](https://en.cppreference.com/utility/forward_like.html)([P2445R1](https://wg21.link/P2445R1)) -
[std::invoke_r](https://en.cppreference.com/utility/functional/invoke.html): invokes a[Callable](https://en.cppreference.com/named_req/Callable.html)object ([P2136R3](https://wg21.link/p2136r3)) -
[std::to_underlying](https://en.cppreference.com/utility/to_underlying.html): a utility function to get the underlying value of enum ([P1682R3](https://wg21.link/P1682R3)) -
[std::unreachable](https://en.cppreference.com/utility/unreachable.html): a function to mark unreachable code ([P0627R6](https://wg21.link/p0627r6)) - Monadic operations (
`transform`

,`or_else`

, and`and_then`

) for[std::optional](https://en.cppreference.com/utility/optional.html)([P0798R8](https://wg21.link/P0798R8)) and[std::expected](https://en.cppreference.com/utility/expected.html)([P2505R5](https://wg21.link/P2505R5)) -
[std::tuple](https://en.cppreference.com/utility/tuple.html)is compatible with other tuple-like objects ([P2165R4](https://wg21.link/p2165r4)) - Adding default arguments for
[std::pair](https://en.cppreference.com/utility/pair.html)'s forwarding constructor ([P2718R0](https://wg21.link/p2718r0)) -
[std::basic_common_reference](https://en.cppreference.com/types/common_reference.html)specialization for[std::reference_wrapper](https://en.cppreference.com/utility/functional/reference_wrapper.html)yielding reference types ([P2655R3](https://wg21.link/p2655r3))

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=7)] Coroutine Library

-
[std::generator](https://en.cppreference.com/coroutine/generator.html): synchronous[coroutine](https://en.cppreference.com/language/coroutines.html)generator for ranges ([P2502R2](https://wg21.link/P2502R2),[P2787R0](https://wg21.link/P2787R0))

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=8)] Diagnostic

-
[Stacktrace](https://en.cppreference.com/error.html#Stacktrace)library ([P0881R7](https://wg21.link/p0881r7))

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=9)] Algorithm, Iterators, and Ranges

- New range adaptors:
-
[views::adjacent](https://en.cppreference.com/ranges/adjacent_view.html)and[views::adjacent_transform](https://en.cppreference.com/ranges/adjacent_transform_view.html)([P2321R2](https://wg21.link/P2321R2)) -
[views::as_const](https://en.cppreference.com/ranges/as_const_view.html)([P2278R4](https://wg21.link/P2278R4)) -
[views::as_rvalue](https://en.cppreference.com/ranges/as_rvalue_view.html)([P2446R2](https://wg21.link/P2446R2)) -
[views::cartesian_product](https://en.cppreference.com/ranges/cartesian_product_view.html)([P2374R4](https://wg21.link/p2374r4)) -
[views::chunk_by](https://en.cppreference.com/ranges/chunk_by_view.html)([P2443R1](https://wg21.link/P2443R1)) -
[views::chunk](https://en.cppreference.com/ranges/chunk_view.html)([P2442R1](https://wg21.link/P2442R1)) - views::enumerate (
[P2164R9](https://wg21.link/p2164r9)) -
[views::join_with](https://en.cppreference.com/ranges/join_with_view.html)([P2441R2](https://wg21.link/p2441r2)) -
[views::repeat](https://en.cppreference.com/ranges/repeat_view.html)([P2474R2](https://wg21.link/p2474r2)) -
[views::slide](https://en.cppreference.com/ranges/slide_view.html)([P2442R1](https://wg21.link/P2442R1)) -
[views::stride](https://en.cppreference.com/ranges/stride_view.html)([P1899R3](https://wg21.link/p1899r3)) -
[views::zip](https://en.cppreference.com/ranges/zip_view.html),[views::zip_transform](https://en.cppreference.com/ranges/zip_transform_view.html)([P2321R2](https://wg21.link/P2321R2))

-
-
[ranges::range_adaptor_closure](https://en.cppreference.com/ranges/range_adaptor_closure.html): a helper for program-defined range adaptor closures ([P2387R3](https://wg21.link/p2387r3)) -
[ranges::to](https://en.cppreference.com/ranges/to.html): a range conversion function ([P1206R7](https://wg21.link/p1206r7)) - New constrained ranges algorithm:
-
[ranges::starts_with](https://en.cppreference.com/algorithm/ranges/starts_with.html)and[ranges::ends_with](https://en.cppreference.com/algorithm/ranges/ends_with.html)([P1659R3](https://wg21.link/p1659r3)) -
[ranges::contains](https://en.cppreference.com/algorithm/ranges/contains.html)and[ranges::contains_subrange](https://en.cppreference.com/algorithm/ranges/contains.html)([P2302R4](https://wg21.link/p2302r4)) -
[ranges::find_last](https://en.cppreference.com/algorithm/ranges/find_last.html),[ranges::find_last_if](https://en.cppreference.com/algorithm/ranges/find_last.html), and[ranges::find_last_if_not](https://en.cppreference.com/algorithm/ranges/find_last.html)([P1223R5](https://wg21.link/p1223r5)) -
[ranges::iota](https://en.cppreference.com/algorithm/ranges/iota.html),[ranges::shift_left](https://en.cppreference.com/algorithm/ranges/shift.html), and[ranges::shift_right](https://en.cppreference.com/algorithm/ranges/shift.html): rangified versions of non-constrained algorithms ([P2440R1](https://wg21.link/p2440r1)) -
[ranges::fold_left](https://en.cppreference.com/algorithm/ranges/fold_left.html)etc.:[range fold algorithms](https://en.cppreference.com/algorithm/ranges.html#Constrained_fold_operations)([P2322R6](https://wg21.link/p2322r6))

-
- Rectifying constant iterators, sentinels, and ranges, that is,
[ranges::cbegin](https://en.cppreference.com/ranges/cbegin.html)and other similar utilities returning constant iterators should be fully guaranteed even for shallow-const views (such as[std::span](https://en.cppreference.com/container/span.html)) ([P2278R4](https://wg21.link/p2278r4)) - Making multi-param constructors of some views explicit (
[P2711R1](https://wg21.link/p2711r1)) - Ranges iterators as inputs to non-ranges algorithms (
[P2408R5](https://wg21.link/p2408r5)) - Relaxing range adaptors to allow for move-only types (
[P2494R2](https://wg21.link/p2494r2))

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=10)] Containers

-
[std::mdspan](https://en.cppreference.com/container/mdspan.html): a non-owning multidimensional array reference ([P0009R18](https://wg21.link/P0009R18),[P2599R2](https://wg21.link/P2599R2),[P2604R0](https://wg21.link/P2604R0),[P2613R1](https://wg21.link/P2613R1),[P2763R1](https://wg21.link/P2763R1)) - Constructibility and assignability of containers from other compatible ranges (
[P1206R7](https://wg21.link/p1206r7)) -
[std::flat_set](https://en.cppreference.com/container/flat_set.html),[std::flat_multiset](https://en.cppreference.com/container/flat_multiset.html)([P1222R4](https://wg21.link/P1222R4)),[std::flat_map](https://en.cppreference.com/container/flat_map.html),[std::flat_multimap](https://en.cppreference.com/container/flat_multimap.html)([P0429R9](https://wg21.link/P0429R9)): flat sets and flat maps - container adaptors wrapping underlying sorted random-access containers - Allowing iterator pair construction in
[std::stack](https://en.cppreference.com/container/stack.html)and[std::queue](https://en.cppreference.com/container/queue.html)([P1425R4](https://wg21.link/p1425r4)) - Heterogeneous erasure overloads for associative containers (
[P2077R2](https://wg21.link/p2077r2)) - Non-deduction context for allocators in container deduction guides (
[P1518R2](https://wg21.link/p1518r2)) - Requiring
[std::span](https://en.cppreference.com/container/span.html)and[std::basic_string_view](https://en.cppreference.com/string/basic_string_view.html)to be trivially copyable ([P2251R1](https://wg21.link/p2251r1))

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=11)] Compile-time support

- constexpr support for:
-
[std::bitset](https://en.cppreference.com/utility/bitset.html)([P2417R2](https://wg21.link/p2417r2)) -
[std::unique_ptr](https://en.cppreference.com/memory/unique_ptr.html)([P2273R3](https://wg21.link/p2273r3)) -
(`std::type_info::operator==`[P1328R1](https://wg21.link/p1328r1)) - Some
functions (`<cmath>`[P0533R9](https://wg21.link/p0533r9)) - Integral overloads of
[std::to_chars](https://en.cppreference.com/utility/to_chars.html)and[std::from_chars](https://en.cppreference.com/utility/from_chars.html)([P2291R3](https://wg21.link/p2291r3))

-
-
[Metaprogramming](https://en.cppreference.com/meta.html)utilities:- Adding move-only types support for comparison concepts (
[P2404R3](https://wg21.link/p2404r3)) - Type traits:

- Adding move-only types support for comparison concepts (

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=12)] Memory Management

-
[std::out_ptr](https://en.cppreference.com/memory/out_ptr_t/out_ptr.html)and[std::inout_ptr](https://en.cppreference.com/memory/inout_ptr_t/inout_ptr.html): smart pointer adaptors for C interoperability ([P1132R7](https://wg21.link/p1132r7)) - std::allocate_at_least and std::allocator::allocate_at_least (
[P0401R6](https://wg21.link/p0401r6)) -
[std::start_lifetime_as](https://en.cppreference.com/memory/start_lifetime_as.html): an explicit lifetime management function for implicit-lifetime types ([P2590R2](https://wg21.link/p2590r2)) - Disallowing user specialization of
[std::allocator_traits](https://en.cppreference.com/memory/allocator_traits.html)([P2652R2](https://wg21.link/p2652r2))

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=13)] String and Text Processing

- New member functions and changes in string types:
- std::basic_string::contains and std::basic_string_view::contains (
[P1679R3](https://wg21.link/p1679r3)) - Disabling construction from nullptr for
[std::basic_string](https://en.cppreference.com/string/basic_string.html)and[std::basic_string_view](https://en.cppreference.com/string/basic_string_view.html)([P2166R1](https://wg21.link/p2166r1)) - Explicit range constructor for
[std::basic_string_view](https://en.cppreference.com/string/basic_string_view.html)([P1989R2](https://wg21.link/p1989r2)) - std::basic_string::resize_and_overwrite (
[P1072R10](https://wg21.link/p1072r10)) - Rvalue reference overload of std::basic_string::substr for efficient slicing (
[P2438R2](https://wg21.link/p2438r2))

- std::basic_string::contains and std::basic_string_view::contains (
- Formatting ranges, tuples, escaped presentation of characters and strings,
[std::thread::id](https://en.cppreference.com/thread/thread/id.html), and[stacktraces](https://en.cppreference.com/error.html#Stacktrace). ([P2286R8](https://wg21.link/p2286r8)) ([P2585R1](https://wg21.link/p2585r1)) ([P2693R1](https://wg21.link/p2693r1))

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=14)] I/O and print

- Formatted output functions
[std::print](https://en.cppreference.com/io/print.html)and[std::println](https://en.cppreference.com/io/println.html)provided in header(`<print>`[P2093R14](https://wg21.link/p2093r14)) -
`spanstream`

library ([std::span](https://en.cppreference.com/container/span.html)-based string stream) provided in header(`<spanstream>`[P0448R4](https://wg21.link/p0448r4)) - Support exclusive mode in std::fstreams (
[P2467R1](https://wg21.link/p2467r1)) - Support of printing volatile T*: std::basic_ostream::operator<<(const volatile void*) (
[P1147R1](https://wg21.link/P1147R1))

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=15)] Obsolete features

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=16)] Removed features

- Garbage collection support and reachability-based leak detection. (
[P2186R2](https://wg21.link/P2186R2)) - Mixed wide string literals
[concatenation](https://en.cppreference.com/language/string_literal.html#Concatenation)support, e.g., const auto* no = u"q" U"p" is ill-formed. ([P2201R1](https://wg21.link/P2201R1)) - Non-encodable wide character literals and multicharacter wide character literals, e.g. wchar_t x = 'db' is ill-formed. (
[P2362R3](https://wg21.link/P2362R3))

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=17)] Deprecated features

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=18)] Reverted deprecations

- The operator, (comma operator) in subscript expressions (but the semantics has been changed to support overloadable multidimensional subscript operator[]).
- Some C headers (the corresponding
`<*.h>`

headers for compatibility with C) ([P2340R1](https://wg21.link/P2340R1))

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=19)] Defect reports

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=20)] Compiler support

Main Article: [C++23 compiler support](https://en.cppreference.com/compiler_support.html#C.2B.2B23_features)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/23&action=edit§ion=T-1)] C++23 core language features

| C++23 feature |
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
|
|---|---|---|---|---|---|---|---|---|---|---|---|
size_t |

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_size_t_suffix))*

[P0330R8](https://wg21.link/P0330R8)**()**

more optional for [lambdas](https://en.cppreference.com/language/lambda.html)[P1102R2](https://wg21.link/P1102R2)[(](https://en.cppreference.com/language/if.html#Consteval_if)`if consteval`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_if_consteval))*[P1938R3](https://wg21.link/P1938R3)[P2186R2](https://wg21.link/P2186R2)[and](https://en.cppreference.com/language/static_assert.html)`static_assert`[constexpr if](https://en.cppreference.com/language/if.html#Constexpr_if)[P1401R5](https://wg21.link/P1401R5)14

[P2223R2](https://wg21.link/P2223R2)[P1847R4](https://wg21.link/P1847R4)[concatenation](https://en.cppreference.com/language/string_literal.html#Concatenation)[P2201R1](https://wg21.link/P2201R1)[Explicit object member functions](https://en.cppreference.com/language/member_functions.html#Explicit_object_member_functions)(deducing this) ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_explicit_this_parameter))*[P0847R7](https://wg21.link/P0847R7)19*

(partial)*

19.43*

[(](https://en.cppreference.com/language/explicit_cast.html)`auto(x)`

and `auto{x}`

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_auto_cast))*[P0849R8](https://wg21.link/P0849R8)`#elifdef`

and `#elifndef`

[P2334R1](https://wg21.link/P2334R1)[functions (](https://en.cppreference.com/language/constexpr.html)`constexpr`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))*[P2242R3](https://wg21.link/P2242R3)[P2316R2](https://wg21.link/P2316R2)[Character sets and encodings](https://en.cppreference.com/language/charset.html)[P2314R4](https://wg21.link/P2314R4)[) to allow](https://en.cppreference.com/language/for.html#Syntax)`for`

loop[alias-declaration](https://en.cppreference.com/language/type_alias.html)[P2360R0](https://wg21.link/P2360R0)[subscript operator](https://en.cppreference.com/language/operators.html#Array_subscript_operator)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_multidimensional_subscript))*[P2128R6](https://wg21.link/P2128R6)[lambdas](https://en.cppreference.com/language/lambda.html)[P2173R1](https://wg21.link/P2173R1)`#warning`

[P2437R1](https://wg21.link/P2437R1)[P2362R3](https://wg21.link/P2362R3)[P2324R2](https://wg21.link/P2324R2)[Delimited escape sequences](https://en.cppreference.com/language/escape.html)[P2290R3](https://wg21.link/P2290R3)[Named universal character escapes](https://en.cppreference.com/language/escape.html#Named_universal_character_escapes)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_named_character_escapes))*[P2071R2](https://wg21.link/P2071R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))*[P2448R2](https://wg21.link/P2448R2)19

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_implicit_move))*[P2266R3](https://wg21.link/P2266R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_static_call_operator))*[P1169R4](https://wg21.link/P1169R4)[extended floating-point types](https://en.cppreference.com/types/floating-point.html)[P1467R9](https://wg21.link/P1467R9)[P2582R1](https://wg21.link/P2582R1)`[[`[assume](https://en.cppreference.com/language/attributes/assume.html)]]

[P1774R8](https://wg21.link/P1774R8)[UTF-8 as a portable source file encoding](https://en.cppreference.com/language/translation_phases.html#Phase_1)[P2295R6](https://wg21.link/P2295R6)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_multidimensional_subscript))*[P2589R1](https://wg21.link/P2589R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))*[P2647R1](https://wg21.link/P2647R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_range_based_for))*[P2644R1](https://wg21.link/P2644R1)[P2718R0](https://wg21.link/P2718R0)[CWG2659](https://wg21.link/CWG2659)[P1787R6](https://wg21.link/P1787R6)[lambda](https://en.cppreference.com/language/lambda.html#Syntax)trailing-return-type[P2036R3](https://wg21.link/P2036R3)[P2579R0](https://wg21.link/P2579R0)[P2615R1](https://wg21.link/P2615R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_consteval))*[P2564R3](https://wg21.link/P2564R3)[P1949R7](https://wg21.link/P1949R7)[attributes](https://en.cppreference.com/language/attributes.html#Syntax)[P2156R1](https://wg21.link/P2156R1)`__cpp_concepts`

[P2493R0](https://wg21.link/P2493R0)[Relax requirements on wchar_t](https://en.cppreference.com/language/types.html#Defect_reports)to match existing practices[P2460R2](https://wg21.link/P2460R2)[P2280R4](https://wg21.link/P2280R4)[P2468R2](https://wg21.link/P2468R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_char8_t))*[P2513R4](https://wg21.link/P2513R4)[diagnostic directives](https://en.cppreference.com/preprocessor/warning.html)and allow static_assert of non-value-dependent expressions in a template context[CWG2518](https://wg21.link/CWG2518)(partial)*

19.40*

C++23 feature

Paper(s)

GCC

Clang

MSVC

Apple Clang

EDG eccp

Intel C++

Nvidia HPC C++ (ex PGI)*

Nvidia nvcc

Cray

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/23&action=edit§ion=T-2)] C++23 library features

| C++23 feature |
Paper(s) |
GCC libstdc++ |
Clang libc++ |
MSVC STL |
Apple Clang* |
|
|---|---|---|---|---|---|---|
|

[P0881R7](https://wg21.link/P0881R7)[P2301R1](https://wg21.link/P2301R1)14*

[(](https://en.cppreference.com/header/stdatomic.h.html)`<stdatomic.h>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_stdatomic_h))*[P0943R6](https://wg21.link/P0943R6)[(](https://en.cppreference.com/types/is_scoped_enum.html)`std::is_scoped_enum`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_scoped_enum))*[P1048R1](https://wg21.link/P1048R1)[,](https://en.cppreference.com/string/basic_string/contains.html)`std::basic_string::contains()`[(](https://en.cppreference.com/string/basic_string_view/contains.html)`std::basic_string_view::contains()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_string_contains))*[P1679R3](https://wg21.link/P1679R3)[(](https://en.cppreference.com/utility/to_underlying.html)`std::to_underlying`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_to_underlying))*[P1682R3](https://wg21.link/P1682R3)[time_point<>::clock](https://en.cppreference.com/chrono/time_point.html)[P2212R2](https://wg21.link/P2212R2)[Providing size feedback](https://en.cppreference.com/memory/allocator_traits/allocate_at_least.html)in the Allocator interface ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_allocate_at_least))*[P0401R6](https://wg21.link/P0401R6)[: string-stream with](https://en.cppreference.com/header/spanstream.html)`<spanstream>`[-based buffer (](https://en.cppreference.com/container/span.html)`std::span`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_spanstream))*[P0448R4](https://wg21.link/P0448R4)[,](https://en.cppreference.com/memory/out_ptr_t/out_ptr.html)`std::out_ptr()`[(](https://en.cppreference.com/memory/inout_ptr_t/inout_ptr.html)`std::inout_ptr()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_out_ptr))*[P1132R8](https://wg21.link/P1132R8)[(](https://en.cppreference.com/types/type_info/operator_cmp.html)`type_info::operator==()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_typeinfo))*[P1328R1](https://wg21.link/P1328R1)19.34*

[and](https://en.cppreference.com/container/stack/stack.html)`std::stack`[(](https://en.cppreference.com/container/queue/queue.html)`std::queue`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_adaptor_iterator_pair_constructor))*[P1425R4](https://wg21.link/P1425R4)[P1518R2](https://wg21.link/P1518R2)[and](https://en.cppreference.com/algorithm/ranges/starts_with.html)`ranges::starts_with()`[(](https://en.cppreference.com/algorithm/ranges/ends_with.html)`ranges::ends_with()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_starts_ends_with))*[P1659R3](https://wg21.link/P1659R3)18

[std::basic_string](https://en.cppreference.com/string/basic_string.html)and[std::basic_string_view](https://en.cppreference.com/string/basic_string_view.html)construction from`nullptr`[P2166R1](https://wg21.link/P2166R1)[(](https://en.cppreference.com/utility/functional/invoke.html)`std::invoke_r()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_invoke_r))*[P2136R3](https://wg21.link/P2136R3)[constructor](https://en.cppreference.com/string/basic_string_view/basic_string_view.html)for[std::basic_string_view](https://en.cppreference.com/string/basic_string_view.html)[P1989R2](https://wg21.link/P1989R2)[std::pair](https://en.cppreference.com/utility/pair.html)'s forwarding[constructor](https://en.cppreference.com/utility/pair/pair.html)[P1951R1](https://wg21.link/P1951R1)[library support](https://en.cppreference.com/memory.html#Garbage_collector_support))[P2186R2](https://wg21.link/P2186R2)[,](https://en.cppreference.com/ranges/zip_view.html)`views::zip`[,](https://en.cppreference.com/ranges/zip_transform_view.html)`views::zip_transform`[, and](https://en.cppreference.com/ranges/adjacent_view.html)`views::adjacent`[(](https://en.cppreference.com/ranges/adjacent_transform_view.html)`views::adjacent_transform`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_zip))*[P2321R2](https://wg21.link/P2321R2)19.37*

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_associative_heterogeneous_erasure))*[P2077R3](https://wg21.link/P2077R3)[(](https://en.cppreference.com/numeric/byteswap.html)`std::byteswap()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_byteswap))*[P1272R4](https://wg21.link/P1272R4)[Printing](https://en.cppreference.com/io/basic_ostream/operator_ltlt.html)volatile T*[P1147R1](https://wg21.link/P1147R1)[(](https://en.cppreference.com/string/basic_string/resize_and_overwrite.html)`basic_string::resize_and_overwrite()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_string_resize_and_overwrite))*[P1072R10](https://wg21.link/P1072R10)[std::optional](https://en.cppreference.com/utility/optional.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_optional))*[P0798R8](https://wg21.link/P0798R8)[(](https://en.cppreference.com/utility/functional/move_only_function.html)`std::move_only_function`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_move_only_function))*[P0288R9](https://wg21.link/P0288R9)[std::exchange](https://en.cppreference.com/utility/exchange.html)[P2401R0](https://wg21.link/P2401R0)[&](https://en.cppreference.com/container/span.html)`std::span`[std::basic_string_view](https://en.cppreference.com/string/basic_string_view.html)to be[TriviallyCopyable](https://en.cppreference.com/named_req/TriviallyCopyable.html)[P2251R1](https://wg21.link/P2251R1)[P2340R1](https://wg21.link/P2340R1)[(](https://en.cppreference.com/header/expected.html)`<expected>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_expected))*[P0323R12](https://wg21.link/P0323R12)[P2549R1](https://wg21.link/P2549R1)[and](https://en.cppreference.com/header/cmath.html)`<cmath>`[(](https://en.cppreference.com/header/cstdlib.html)`<cstdlib>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_cmath))*[P0533R9](https://wg21.link/P0533R9)[(](https://en.cppreference.com/utility/unreachable.html)`std::unreachable()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_unreachable))*[P0627R6](https://wg21.link/P0627R6)[std::aligned_storage](https://en.cppreference.com/types/aligned_storage.html)and[std::aligned_union](https://en.cppreference.com/types/aligned_union.html)[P1413R3](https://wg21.link/P1413R3)[&](https://en.cppreference.com/types/reference_constructs_from_temporary.html)`std::reference_constructs_from_temporary`[(](https://en.cppreference.com/types/reference_converts_from_temporary.html)`std::reference_converts_from_temporary`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_reference_from_temporary))*[P2255R2](https://wg21.link/P2255R2)14

[std::unique_ptr](https://en.cppreference.com/memory/unique_ptr.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_memory))*[P2273R3](https://wg21.link/P2273R3)[, tagged constructors, insert and assign member functions (](https://en.cppreference.com/ranges/to.html)`ranges::to()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_containers_ranges))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_to_container))*[P1206R7](https://wg21.link/P1206R7)15

[,](https://en.cppreference.com/ranges/range_adaptor_closure.html)`ranges::range_adaptor_closure`[) (](https://en.cppreference.com/utility/functional/bind_front.html)`std::bind_back`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_bind_back))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges))*[P2387R3](https://wg21.link/P2387R3)14

[,](https://en.cppreference.com/algorithm/ranges/iota.html)`ranges::iota()`[, and](https://en.cppreference.com/algorithm/ranges/shift.html)`ranges::shift_left()`[(](https://en.cppreference.com/algorithm/ranges/shift.html)`ranges::shift_right()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_iota))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_shift))*[P2440R1](https://wg21.link/P2440R1)[(](https://en.cppreference.com/ranges/join_with_view.html)`views::join_with`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_join_with))*[P2441R2](https://wg21.link/P2441R2)[and](https://en.cppreference.com/ranges/chunk_view.html)`views::chunk`[(](https://en.cppreference.com/ranges/slide_view.html)`views::slide`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_chunk))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_slide))*[P2442R1](https://wg21.link/P2442R1)[(](https://en.cppreference.com/ranges/chunk_by_view.html)`views::chunk_by`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_chunk_by))*[P2443R1](https://wg21.link/P2443R1)[: a non-owning multidimensional array reference (](https://en.cppreference.com/container/mdspan.html)`std::mdspan`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_mdspan))*[P0009R18](https://wg21.link/P0009R18)[P2599R2](https://wg21.link/P2599R2)[P2604R0](https://wg21.link/P2604R0)[P2613R1](https://wg21.link/P2613R1)[P2763R1](https://wg21.link/P2763R1)18

[(](https://en.cppreference.com/header/flat_map.html)`<flat_map>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_flat_map))*[P0429R9](https://wg21.link/P0429R9)[(](https://en.cppreference.com/header/flat_set.html)`<flat_set>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_flat_set))*[P1222R4](https://wg21.link/P1222R4)[,](https://en.cppreference.com/algorithm/ranges/find_last.html)`ranges::find_last()`[, and](https://en.cppreference.com/algorithm/ranges/find_last.html)`ranges::find_last_if()`[(](https://en.cppreference.com/algorithm/ranges/find_last.html)`ranges::find_last_if_not()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_find_last))*[P1223R5](https://wg21.link/P1223R5)[,](https://en.cppreference.com/header/utility.html)`<utility>`[, and](https://en.cppreference.com/header/ranges.html)`<ranges>``<iterator>`[P1642R11](https://wg21.link/P1642R11)[(](https://en.cppreference.com/ranges/stride_view.html)`views::stride`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_stride))*[P1899R3](https://wg21.link/P1899R3)[std::tuple](https://en.cppreference.com/utility/tuple.html)and tuple-like objects ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_tuple_like))*[P2165R4](https://wg21.link/P2165R4)19.37*

[views::as_const](https://en.cppreference.com/ranges/as_const_view.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_as_const))*[P2278R4](https://wg21.link/P2278R4)19.36*

[Formatting](https://en.cppreference.com/utility/format.html)Ranges ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format_ranges))*[P2286R8](https://wg21.link/P2286R8)15.2

19.39*(partial)*

19.41*(partial)*

19.42*

[formatting](https://en.cppreference.com/utility/format.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format_ranges))*[P2585R1](https://wg21.link/P2585R1)17

[(](https://en.cppreference.com/header/print.html)`<print>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_print))*[P2093R14](https://wg21.link/P2093R14)[P2539R4](https://wg21.link/P2539R4)18

16.0.0*

[Formatting](https://en.cppreference.com/utility/format.html)[std::thread::id](https://en.cppreference.com/thread/thread/id.html)and[(](https://en.cppreference.com/utility/basic_stacktrace.html)`std::stacktrace`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_formatters))*[P2693R1](https://wg21.link/P2693R1)[and](https://en.cppreference.com/utility/to_chars.html)`std::to_chars()`[(](https://en.cppreference.com/utility/from_chars.html)`std::from_chars()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_charconv))*[P2291R3](https://wg21.link/P2291R3)[and](https://en.cppreference.com/algorithm/ranges/contains.html)`ranges::contains()`[(](https://en.cppreference.com/algorithm/ranges/contains.html)`ranges::contains_subrange()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_contains))*[P2302R4](https://wg21.link/P2302R4)19

[Ranges fold algorithms](https://en.cppreference.com/algorithm/ranges.html#Constrained_fold_operations)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_fold))*[P2322R6](https://wg21.link/P2322R6)[(](https://en.cppreference.com/ranges/cartesian_product_view.html)`views::cartesian_product`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_cartesian_product))*[P2374R4](https://wg21.link/P2374R4)[P2540R1](https://wg21.link/P2540R1)[,](https://en.cppreference.com/concepts/equality_comparable.html)`equality_comparable`

[,](https://en.cppreference.com/concepts/totally_ordered.html)`totally_ordered`

[) (](https://en.cppreference.com/utility/compare/three_way_comparable.html)`three_way_comparable`

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_concepts))*[P2404R3](https://wg21.link/P2404R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_algorithm_iterator_requirements))*[P2408R5](https://wg21.link/P2408R5)[std::bitset](https://en.cppreference.com/utility/bitset.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_bitset))*[P2417R2](https://wg21.link/P2417R2)`basic_string::substr()``&&`

[P2438R2](https://wg21.link/P2438R2)[(](https://en.cppreference.com/ranges/as_rvalue_view.html)`views::as_rvalue`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_as_rvalue))*[P2446R2](https://wg21.link/P2446R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_modules))*[P2465R3](https://wg21.link/P2465R3)(partial)*

19.36*

[(](https://en.cppreference.com/utility/forward_like.html)`std::forward_like()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_forward_like))*[P2445R1](https://wg21.link/P2445R1)[std::fstream](https://en.cppreference.com/io/basic_fstream.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ios_noreplace))*[P2467R1](https://wg21.link/P2467R1)[(](https://en.cppreference.com/ranges/repeat_view.html)`views::repeat`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_repeat))*[P2474R2](https://wg21.link/P2474R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges))*[P2494R2](https://wg21.link/P2494R2)[std::basic_string_view](https://en.cppreference.com/string/basic_string_view.html)range[constructor](https://en.cppreference.com/string/basic_string_view/basic_string_view.html)should be explicit[P2499R0](https://wg21.link/P2499R0)[: synchronous coroutine generator for ranges (](https://en.cppreference.com/coroutine/generator.html)`std::generator`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_generator))*[P2502R2](https://wg21.link/P2502R2)[P2787R0](https://wg21.link/P2787R0)[std::apply](https://en.cppreference.com/utility/apply.html)[P2517R1](https://wg21.link/P2517R1)[) (](https://en.cppreference.com/memory/start_lifetime_as.html)`std::start_lifetime_as`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_start_lifetime_as))*[P2590R2](https://wg21.link/P2590R2)[P2679R2](https://wg21.link/P2679R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format))*[P2419R2](https://wg21.link/P2419R2)[std::move_iterator](https://en.cppreference.com/iterator/move_iterator.html)should not always be[(](https://en.cppreference.com/iterator/input_iterator.html)`input_iterator`

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_move_iterator_concept))*[P2520R0](https://wg21.link/P2520R0)[explicit object parameter](https://en.cppreference.com/language/member_functions.html#Explicit_object_parameter)call operators[LWG3617](https://wg21.link/LWG3617)[P1169R4](https://wg21.link/P1169R4)[extended floating-point types](https://en.cppreference.com/header/stdfloat.html)[P1467R9](https://wg21.link/P1467R9)[(](https://en.cppreference.com/utility/expected.html)`std::expected`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_expected))*[P2505R5](https://wg21.link/P2505R5)[(](https://en.cppreference.com/ranges/enumerate_view.html)`views::enumerate`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_enumerate))*[P2164R9](https://wg21.link/P2164R9)[(](https://en.cppreference.com/types/is_implicit_lifetime.html)`std::is_implicit_lifetime`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_implicit_lifetime))*[P2674R1](https://wg21.link/P2674R1)[std::reference_wrapper](https://en.cppreference.com/utility/functional/reference_wrapper.html)should be a reference type ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_common_reference))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_common_reference_wrapper))*[P2655R3](https://wg21.link/P2655R3)[std::allocator_traits](https://en.cppreference.com/memory/allocator_traits.html)[P2652R2](https://wg21.link/P2652R2)[std::numeric_limits::has_denorm](https://en.cppreference.com/types/numeric_limits/has_denorm.html)[P2614R2](https://wg21.link/P2614R2)`view`s`explicit`[P2711R1](https://wg21.link/P2711R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges))*[P2609R3](https://wg21.link/P2609R3)[P2770R0](https://wg21.link/P2770R0)[std::visit()](https://en.cppreference.com/utility/variant/visit.html)for classes derived from[std::variant](https://en.cppreference.com/utility/variant.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_variant))*[P2162R2](https://wg21.link/P2162R2)19.30*

[P2017R1](https://wg21.link/P2017R1)[input range adaptors](https://en.cppreference.com/ranges.html#Views)and[std::counted_iterator](https://en.cppreference.com/iterator/counted_iterator.html)[P2259R1](https://wg21.link/P2259R1)19.31*

[should join all views of ranges](https://en.cppreference.com/ranges/join_view.html)`views::join`[P2328R1](https://wg21.link/P2328R1)[does not require](https://en.cppreference.com/ranges/view.html)`view`

[(](https://en.cppreference.com/concepts/default_initializable.html)`default_initializable`

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges))*[P2325R3](https://wg21.link/P2325R3)[P2281R1](https://wg21.link/P2281R1)(partial)*

19.31*

[for](https://en.cppreference.com/language/constexpr.html)`constexpr`[std::optional](https://en.cppreference.com/utility/optional.html)and[std::variant](https://en.cppreference.com/utility/variant.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_optional))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_variant))*[P2231R1](https://wg21.link/P2231R1)12

19

[and redesigned](https://en.cppreference.com/ranges/lazy_split_view.html)`views::lazy_split``views::split`[P2210R2](https://wg21.link/P2210R2)[ranges::istream_view](https://en.cppreference.com/ranges/basic_istream_view.html)[P2432R1](https://wg21.link/P2432R1)[with ownership (](https://en.cppreference.com/ranges/view.html)`view`

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges))*[P2415R2](https://wg21.link/P2415R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format))*[P2372R3](https://wg21.link/P2372R3)[P2418R2](https://wg21.link/P2418R2)[P2393R1](https://wg21.link/P2393R1)[family (](https://en.cppreference.com/utility/format/format.html)`std::format()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format))*[P2216R3](https://wg21.link/P2216R3)15

[std::format](https://en.cppreference.com/utility/format/format.html)[P2418R2](https://wg21.link/P2418R2)`std::basic_format_string`[P2508R1](https://wg21.link/P2508R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges))*[P2602R2](https://wg21.link/P2602R2)[std::format](https://en.cppreference.com/utility/format/format.html)fill character allowances[P2572R1](https://wg21.link/P2572R1)[std::format](https://en.cppreference.com/utility/format/format.html)'s width estimation[P2675R1](https://wg21.link/P2675R1)[std::barrier](https://en.cppreference.com/thread/barrier.html)'s phase completion guarantees ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_barrier))*[P2588R3](https://wg21.link/P2588R3)19.36*

C++23 feature

Paper(s)

GCC libstdc++

Clang libc++

MSVC STL

Apple Clang*

DR*nn* - the number *nn* after "DR" denotes target C++ revision the Defect Report is applied to, e.g., DR20 → C++20.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/23&action=edit§ion=21)] External links

| 1. |
|
