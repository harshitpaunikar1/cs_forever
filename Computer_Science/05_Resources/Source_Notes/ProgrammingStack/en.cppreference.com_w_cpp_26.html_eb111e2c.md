Title: C++26 - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/26.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:06:51+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# C++26

From cppreference.com

<

[cpp](https://en.cppreference.com/cpp.html)The next generation of the C++ standard.

The current IS schedule for C++26: [P1000R6](https://wg21.link/P1000R6) (2024-05-14).

| This section is incomplete |

## Contents |

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=1)] New language features

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=2)] New library features

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=3)] New modules

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=4)] New headers

-
`<contracts>` -
`<debugging>` -
`<hazard_pointer>` -
`<hive>` -
`<inplace_vector>` -
`<linalg>` -
`<rcu>` -
`<simd>` -
`<text_encoding>`

C compatibility headers:

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=5)] Obsolete features

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=6)] Removed features

| This section is incomplete |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=7)] Deprecated features

| This section is incomplete |

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=8)] Defect reports

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=9)] Compiler support

Main Article: [C++26 compiler support](https://en.cppreference.com/compiler_support.html#C.2B.2B26_features)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/26&action=edit§ion=T-1)] C++26 core language features

| C++26 feature |
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
| DR98: Removing undefined behavior from lexing |
|

[P1854R4](https://wg21.link/P1854R4)[Unevaluated strings](https://en.cppreference.com/language/string_literal.html#Unevaluated_strings)[P2361R6](https://wg21.link/P2361R6)18

**@**

, **$**

, and **`**

to the [basic character set](https://en.cppreference.com/language/charset.html#Basic_character_set)[P2558R2](https://wg21.link/P2558R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))*[P2738R1](https://wg21.link/P2738R1)[P2552R3](https://wg21.link/P2552R3)[P2752R3](https://wg21.link/P2752R3)[messages (](https://en.cppreference.com/language/static_assert.html)`static_assert`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_static_assert))*[P2741R3](https://wg21.link/P2741R3)[Placeholder variables with no name](https://en.cppreference.com/language/conflicting_declarations.html#Potentially-conflict_declarations)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_placeholder_variables))*[P2169R4](https://wg21.link/P2169R4)[Pack indexing](https://en.cppreference.com/language/pack_indexing.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_pack_indexing))*[P2662R3](https://wg21.link/P2662R3)[P2864R2](https://wg21.link/P2864R2)[P2308R1](https://wg21.link/P2308R1)[temporary](https://en.cppreference.com/language/reference_initialization.html#Lifetime_of_a_temporary)[P2748R5](https://wg21.link/P2748R5)[structured bindings](https://en.cppreference.com/language/structured_binding.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_structured_bindings))*[P0609R3](https://wg21.link/P0609R3)[uninitialized reads](https://en.cppreference.com/language/default_initialization.html#Read_from_an_indeterminate_byte),`[[`[indeterminate](https://en.cppreference.com/language/attributes/indeterminate.html)]]

attribute
[P2795R5](https://wg21.link/P2795R5)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_deleted_function))*[P2573R2](https://wg21.link/P2573R2)[Variadic](https://en.cppreference.com/language/parameter_pack.html)[friends](https://en.cppreference.com/language/friend.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_variadic_friend))*[P2893R3](https://wg21.link/P2893R3)[aggregate initialization](https://en.cppreference.com/language/aggregate_initialization.html)[P3106R1](https://wg21.link/P3106R1)[P3034R1](https://wg21.link/P3034R1)[P2809R3](https://wg21.link/P2809R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_new))*[P2747R2](https://wg21.link/P2747R2)[Structured binding](https://en.cppreference.com/language/structured_binding.html)declaration as a condition ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_structured_bindings))*[P0963R3](https://wg21.link/P0963R3)21

[constraints](https://en.cppreference.com/language/constraints.html)involving[fold expressions](https://en.cppreference.com/language/fold.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_fold_expressions))*[P2963R3](https://wg21.link/P2963R3)[Deleting](https://en.cppreference.com/language/delete.html)a pointer to an incomplete type should be ill-formed[P3144R2](https://wg21.link/P3144R2)[Structured bindings](https://en.cppreference.com/language/structured_binding.html)can introduce a[pack](https://en.cppreference.com/language/parameter_pack.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_structured_bindings))*[P1061R10](https://wg21.link/P1061R10)[structured bindings](https://en.cppreference.com/language/structured_binding.html)and references to constexpr variables[P2686R5](https://wg21.link/P2686R5)[exceptions](https://en.cppreference.com/language/exceptions.html):[[1]](https://en.cppreference.com/language/constant_expression.html#P3068_1),[[2]](https://en.cppreference.com/language/constant_expression.html#P3068_2)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr_exceptions))*[P3068R6](https://wg21.link/P3068R6)[P3176R1](https://wg21.link/P3176R1)[P2865R6](https://wg21.link/P2865R6)[(](https://en.cppreference.com/preprocessor/embed.html)`#embed`

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_pp_embed))*[P1967R14](https://wg21.link/P1967R14)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_template_parameters))*[P2841R7](https://wg21.link/P2841R7)[Trivial relocatability](https://en.cppreference.com/language/class_property_specifiers.html#Trivial_relocatability)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_trivial_relocatability))*[P2786R13](https://wg21.link/P2786R13)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_trivial_union))*[P3074R7](https://wg21.link/P3074R7)[P1494R5](https://wg21.link/P1494R5)[Contracts](https://en.cppreference.com/language/contracts.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_contracts))*[P2900R14](https://wg21.link/P2900R14)C++26 feature

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

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/26&action=edit§ion=T-2)] C++26 library features

| C++26 feature |
Paper(s) |
GCC libstdc++ |
Clang libc++ |
MSVC STL |
Apple Clang* |
|
|---|---|---|---|---|---|---|
| Testing for success or failure of
<charconv> |

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_to_chars))*

[P2497R0](https://wg21.link/P2497R0)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_text_encoding))*[P1885R12](https://wg21.link/P1885R12)[P2862R1](https://wg21.link/P2862R1)[and](https://en.cppreference.com/string/basic_string/to_string.html)`std::to_string`[use](https://en.cppreference.com/string/basic_string/to_wstring.html)`std::to_wstring`[(](https://en.cppreference.com/utility/format/format.html)`std::format`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_to_string))*[P2587R3](https://wg21.link/P2587R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format))*[P2757R3](https://wg21.link/P2757R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format))*[P2510R3](https://wg21.link/P2510R3)[Hashing](https://en.cppreference.com/utility/hash.html)support for[value classes (](https://en.cppreference.com/chrono.html)`std::chrono`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_chrono))*[P2592R3](https://wg21.link/P2592R3)[:](https://en.cppreference.com/header/rcu.html)`<rcu>`[Read-Copy Update](https://en.cppreference.com/atomic.html#Read-Copy-Update_mechanism)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_rcu))*[P2545R4](https://wg21.link/P2545R4)[:](https://en.cppreference.com/header/hazard_pointer.html)`<hazard_pointer>`[Hazard pointers](https://en.cppreference.com/atomic.html#Hazard_pointers)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hazard_pointer))*[P2530R3](https://wg21.link/P2530R3)`std::projected`[P2538R1](https://wg21.link/P2538R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_algorithms))*[P2562R1](https://wg21.link/P2562R1)[(](https://en.cppreference.com/utility/format/basic_format_arg.html#visit)`std::basic_format_arg::visit()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format))*[P2637R3](https://wg21.link/P2637R3)[(](https://en.cppreference.com/utility/variant/visit.html)`std::variant::visit()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_variant))*[P2637R3](https://wg21.link/P2637R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_within_lifetime))*[P2641R4](https://wg21.link/P2641R4)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_associative_heterogeneous_insertion))*[P2363R5](https://wg21.link/P2363R5)[as keys in unordered associative containers (](https://en.cppreference.com/memory/weak_ptr.html)`std::weak_ptr`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_smart_ptr_owner_equality))*[P1901R2](https://wg21.link/P1901R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_fstream_native_handle))*[P1759R6](https://wg21.link/P1759R6)[(](https://en.cppreference.com/string/basic_string_view.html)`std::string_view`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_sstream_from_string_view))*[P2495R3](https://wg21.link/P2495R3)[with](https://en.cppreference.com/utility/bitset.html)`std::bitset`[(](https://en.cppreference.com/string/basic_string_view.html)`std::string_view`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_bitset))*[P2697R1](https://wg21.link/P2697R1)[and](https://en.cppreference.com/header/cmath.html)`<cmath>`[(](https://en.cppreference.com/header/complex.html)`<complex>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_cmath))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_complex))*[P1383R2](https://wg21.link/P1383R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ratio))*[P2734R0](https://wg21.link/P2734R0)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_function_ref))*[P0792R14](https://wg21.link/P0792R14)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_copyable_function))*[P2548R6](https://wg21.link/P2548R6)[,](https://en.cppreference.com/utility/functional/bind_front.html)`std::bind_front`[, and](https://en.cppreference.com/utility/functional/bind_front.html)`std::bind_back`[to NTTP callables (](https://en.cppreference.com/utility/functional/not_fn.html)`std::not_fn`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_bind_front))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_bind_back))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_not_fn))*[P2714R1](https://wg21.link/P2714R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_submdspan))*[P2630R4](https://wg21.link/P2630R4)[P3355R1](https://wg21.link/P3355R1)`::operator new`[P2013R5](https://wg21.link/P2013R5)[std::char_traits](https://en.cppreference.com/string/char_traits.html),[std::errc](https://en.cppreference.com/error/errc.html)and facilities in:[,](https://en.cppreference.com/header/charconv.html)`<charconv>`[,](https://en.cppreference.com/header/cstdlib.html)`<cstdlib>`[,](https://en.cppreference.com/header/cstring.html)`<cstring>`[(](https://en.cppreference.com/header/cwchar.html)`<cwchar>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_char_traits))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_charconv))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_cstdlib))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_cstring))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_cwchar))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_errc))*[P2338R4](https://wg21.link/P2338R4)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_feature_test_macros))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_functional))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_iterator))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_memory))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_ranges))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_ratio))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_tuple))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_utility))*[P2198R7](https://wg21.link/P2198R7)[Saturation arithmetic](https://en.cppreference.com/numeric.html#Saturation_arithmetic)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_saturation_arithmetic))*[P0543R3](https://wg21.link/P0543R3)[:](https://en.cppreference.com/header/debugging.html)`<debugging>`[Debugging support](https://en.cppreference.com/utility.html#Debugging_support)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_debugging))*[P2546R5](https://wg21.link/P2546R5)[P2810R4](https://wg21.link/P2810R4)[: A free function linear algebra interface based on the BLAS (](https://en.cppreference.com/header/linalg.html)`<linalg>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_linalg))*[P1673R13](https://wg21.link/P1673R13)[P3050R2](https://wg21.link/P3050R2)[P3222R0](https://wg21.link/P3222R0)[assert()](https://en.cppreference.com/error/assert.html)macro user friendly[P2264R7](https://wg21.link/P2264R7)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format))*[P2918R2](https://wg21.link/P2918R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_span_initializer_list))*[P2447R6](https://wg21.link/P2447R6)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_span))*[P2821R5](https://wg21.link/P2821R5)[std::complex](https://en.cppreference.com/numeric/complex.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_tuple_like))*[P2819R2](https://wg21.link/P2819R2)[std::generate_canonical](https://en.cppreference.com/numeric/random/generate_canonical.html)[P0952R2](https://wg21.link/P0952R2)[P2868R3](https://wg21.link/P2868R3)[std::basic_string::reserve()](https://en.cppreference.com/string/basic_string/reserve.html)that takes no argument[P2870R3](https://wg21.link/P2870R3)[)](https://en.cppreference.com/header/codecvt.html)`<codecvt>`[P2871R3](https://wg21.link/P2871R3)[std::strtok](https://en.cppreference.com/string/byte/strtok.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_cstring))*[P2937R0](https://wg21.link/P2937R0)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_algorithm))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_array))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_optional))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_string_view))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_variant))*[P2407R5](https://wg21.link/P2407R5)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_expected))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_mdspan))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_out_ptr))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_span))*[P2833R2](https://wg21.link/P2833R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_as_const))*[P2836R1](https://wg21.link/P2836R1)[P2950R0](https://wg21.link/P2950R0)[std::make_format_args](https://en.cppreference.com/utility/format/make_format_args.html)now accepts only lvalue references instead of forwarding references[P2905R2](https://wg21.link/P2905R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format_uchar))*[P2909R4](https://wg21.link/P2909R4)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_concat))*[P2542R8](https://wg21.link/P2542R8)[strings](https://en.cppreference.com/string/basic_string.html)and[string views](https://en.cppreference.com/string/basic_string_view.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_string_view))*[P2591R5](https://wg21.link/P2591R5)[algorithms](https://en.cppreference.com/algorithm.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_algorithm_default_value_type))*[P2248R8](https://wg21.link/P2248R8)[P3217R0](https://wg21.link/P3217R0)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_generate_random))*[P1068R11](https://wg21.link/P1068R11)[Comparisons](https://en.cppreference.com/utility/functional/reference_wrapper/operator_cmp.html)for[std::reference_wrapper](https://en.cppreference.com/utility/functional/reference_wrapper.html), and constraints for comparisons of[,](https://en.cppreference.com/utility/pair/operator_cmp.html)`std::pair`[,](https://en.cppreference.com/utility/tuple/operator_cmp.html)`std::tuple`[, and](https://en.cppreference.com/utility/optional/operator_cmp.html)`std::optional`[(](https://en.cppreference.com/utility/variant/operator_cmp.html)`std::variant`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constrained_equality))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_reference_wrapper))*[P2944R3](https://wg21.link/P2944R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_submdspan))*[P2642R6](https://wg21.link/P2642R6)[P3029R1](https://wg21.link/P3029R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_min_max))*[P0493R5](https://wg21.link/P0493R5)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format_path))*[P2845R8](https://wg21.link/P2845R8)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_print))*[P3142R0](https://wg21.link/P3142R0)[P2875R4](https://wg21.link/P2875R4)[P2867R2](https://wg21.link/P2867R2)[std::shared_ptr](https://en.cppreference.com/memory/shared_ptr.html)Atomic Access APIs[P2869R4](https://wg21.link/P2869R4)[std::wstring_convert](https://en.cppreference.com/locale/wstring_convert.html)[P2872R3](https://wg21.link/P2872R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_print))*[P3107R5](https://wg21.link/P3107R5)[P3235R3](https://wg21.link/P3235R3)[Execution control library](https://en.cppreference.com/experimental/execution.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_senders))*[P2300R10](https://wg21.link/P2300R10)[P3396R0](https://wg21.link/P3396R0)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_inplace_vector))*[P0843R14](https://wg21.link/P0843R14)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_philox_engine))*[P2075R6](https://wg21.link/P2075R6)[std::optional](https://en.cppreference.com/utility/optional.html)range support ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_optional_range_support))*[P3168R2](https://wg21.link/P3168R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_virtual_base_of))*[P2985R0](https://wg21.link/P2985R0)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_mdspan))*[P2389R2](https://wg21.link/P2389R2)[std::ignore](https://en.cppreference.com/utility/tuple/ignore.html)[P2968R2](https://wg21.link/P2968R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges))*[P2997R1](https://wg21.link/P2997R1)[std::is_trivial](https://en.cppreference.com/types/is_trivial.html)and[std::is_trivial_v](https://en.cppreference.com/types/is_trivial.html)[P3247R2](https://wg21.link/P3247R2)[P3136R1](https://wg21.link/P3136R1)[(](https://en.cppreference.com/ranges/cache_latest_view.html)`std::ranges::cache_latest_view`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_cache_latest))*[P3138R5](https://wg21.link/P3138R5)[equality operators](https://en.cppreference.com/utility/expected/operator_cmp.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constrained_equality))*[P3379R0](https://wg21.link/P3379R0)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_aligned_accessor))*[P2897R7](https://wg21.link/P2897R7)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_sufficiently_aligned))*[P2897R7](https://wg21.link/P2897R7)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_ref))*[P2835R7](https://wg21.link/P2835R7)[std::atomic](https://en.cppreference.com/atomic/atomic.html)and std::atomic_ref[P3323R1](https://wg21.link/P3323R1)[std::atomic](https://en.cppreference.com/atomic/atomic.html)and std::atomic_ref ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_atomic))*[P3309R3](https://wg21.link/P3309R3)[specialized memory algorithms](https://en.cppreference.com/memory.html#Uninitialized_memory_algorithms)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_raw_memory_algorithms))*[P3508R0](https://wg21.link/P3508R0)[P3369R0](https://wg21.link/P3369R0)[and](https://en.cppreference.com/header/stdbit.h.html)`<stdbit.h>``<stdckdint.h>`[P3370R1](https://wg21.link/P3370R1)[:](https://en.cppreference.com/header/simd.html)`<simd>`[data-parallel types](https://en.cppreference.com/numeric/simd.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_simd))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_simd_complex))*[P1928R15](https://wg21.link/P1928R15)[P3430R3](https://wg21.link/P3430R3)[P3441R2](https://wg21.link/P3441R2)[P3287R3](https://wg21.link/P3287R3)[P2663R7](https://wg21.link/P2663R7)[P2933R4](https://wg21.link/P2933R4)[execution environments](https://en.cppreference.com/experimental/execution.html#Environments)[P3325R5](https://wg21.link/P3325R5)[std::bad_alloc](https://en.cppreference.com/memory/new/bad_alloc.html),[std::bad_cast](https://en.cppreference.com/types/bad_cast.html)etc. ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_exceptions))*[P3068R6](https://wg21.link/P3068R6)[P3378R2](https://wg21.link/P3378R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_trivially_relocatable))*[P2786R13](https://wg21.link/P2786R13)`std::memory_order::consume`

[P3475R1](https://wg21.link/P3475R1)[std::monostate](https://en.cppreference.com/utility/variant/monostate.html)in`<utility>`[P0472R3](https://wg21.link/P0472R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_indirect))*[P3019R14](https://wg21.link/P3019R14)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_polymorphic))*[P3019R14](https://wg21.link/P3019R14)[std::deque](https://en.cppreference.com/container/deque.html),
std::flat_map, std::flat_multimap,
std::flat_set, std::flat_multiset,
[std::forward_list](https://en.cppreference.com/container/forward_list.html),
[std::list](https://en.cppreference.com/container/list.html),
[std::map](https://en.cppreference.com/container/map.html), [std::multimap](https://en.cppreference.com/container/multimap.html),
[std::queue](https://en.cppreference.com/container/queue.html), [std::priority_queue](https://en.cppreference.com/container/priority_queue.html),
[std::set](https://en.cppreference.com/container/set.html), [std::multiset](https://en.cppreference.com/container/multiset.html),
[std::stack](https://en.cppreference.com/container/stack.html),
[std::unordered_map](https://en.cppreference.com/container/unordered_map.html), [std::unordered_multimap](https://en.cppreference.com/container/unordered_multimap.html),
[std::unordered_set](https://en.cppreference.com/container/unordered_set.html), and [std::unordered_multiset](https://en.cppreference.com/container/unordered_multiset.html)

([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_deque))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_flat_map))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_flat_set))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_forward_list))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_list))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_map))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_queue))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_set))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_stack))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_unordered_map))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_unordered_set))*

[P3372R3](https://wg21.link/P3372R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_inplace_vector))*[P3074R7](https://wg21.link/P3074R7)[(](https://en.cppreference.com/ranges/to_input_view.html)`std::ranges::to_input_view`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_to_input))*[P3137R3](https://wg21.link/P3137R3)[and](https://en.cppreference.com/ranges/approximately_sized_range.html)`std::ranges::approximately_sized_range`[(](https://en.cppreference.com/ranges/reserve_hint.html)`std::ranges::reserve_hint`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges_reserve_hint))*[P2846R6](https://wg21.link/P2846R6)[: A bucket-based container that re-uses memory locations from erased elements (](https://en.cppreference.com/header/hive.html)`<hive>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hive))*[P0447R28](https://wg21.link/P0447R28)[: Contract-violation handling support (](https://en.cppreference.com/header/contracts.html)`<contracts>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_contracts))*[P2900R14](https://wg21.link/P2900R14)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_array))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_basic_string))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_basic_string_view))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_bitset))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_deque))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_expected))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_forward_list))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_inplace_vector))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_list))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_mdspan))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_optional))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_span))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_valarray))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardened_vector))*[P3471R4](https://wg21.link/P3471R4)[,](https://en.cppreference.com/header/algorithm.html)`<algorithm>`[,](https://en.cppreference.com/header/numeric.html)`<numeric>`[, (](https://en.cppreference.com/header/random.html)`<random>`[,](https://en.cppreference.com/header/execution.html)`<execution>`[)](https://en.cppreference.com/header/memory.html)`<memory>`(

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_algorithm))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_execution))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_memory))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_numeric))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_freestanding_random))*[P2976R1](https://wg21.link/P2976R1)[P3349R0](https://wg21.link/P3349R0)C++26 feature

Paper(s)

GCC libstdc++

Clang libc++

MSVC STL

Apple Clang*

DR*nn* - the number *nn* after "DR" denotes target C++ revision the Defect Report is applied to, e.g., DR20 → C++20.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/26&action=edit§ion=10)] External links

| 1. |
|
