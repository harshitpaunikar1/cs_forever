Title: C++ compiler support - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/compiler_support.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:07:09+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# C++ compiler support

[cpp](https://en.cppreference.com/cpp.html)

| This page is maintained as best-effort and may lag behind most recent compiler releases. If you see something is out-of-date, please help us by updating it! |

The following tables present compiler support for new C++ features. These include accepted revisions to the standard, as well as various technical specifications:

## Contents |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/compiler_support&action=edit§ion=1)] Notes

DR*nn* - the number *nn* after "DR" denotes target C++ revision the Defect Report is applied to, e.g., DR20 → C++20.

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/compiler_support&action=edit§ion=2)] C++26 features

Note that this list may change, as the draft C++26/2c standard evolves.

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

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/compiler_support&action=edit§ion=3)] C++23 features

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

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/compiler_support&action=edit§ion=4)] C++20 features

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/20&action=edit§ion=T-1)] C++20 core language features

| C++20 feature |
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
| Allow
|

[P0409R2](https://wg21.link/P0409R2)`__VA_OPT__`

[P0306R4](https://wg21.link/P0306R4)[P1042R1](https://wg21.link/P1042R1)10 (partial)*

12

[Designated initializers](https://en.cppreference.com/language/aggregate_initialization.html#Designated_initializers)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_designated_initializers))*[P0329R4](https://wg21.link/P0329R4)8

10

[template-parameter-list for generic lambdas](https://en.cppreference.com/language/lambda.html#Syntax)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_generic_lambdas))*[P0428R2](https://wg21.link/P0428R2)[Default member initializers for bit-fields](https://en.cppreference.com/language/bit_field.html#Cpp20_Default_member_initializers_for_bit_fields)[P0683R1](https://wg21.link/P0683R1)[P0702R1](https://wg21.link/P0702R1)[P0704R1](https://wg21.link/P0704R1)[Concepts](https://en.cppreference.com/language/constraints.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_concepts))*[P0734R0](https://wg21.link/P0734R0)10

19.30*

[Lambdas in unevaluated contexts](https://en.cppreference.com/language/lambda.html#Lambdas_in_unevaluated_contexts)[P0315R4](https://wg21.link/P0315R4)14 (partial)*

17

2024.0

[Three-way comparison](https://en.cppreference.com/language/operator_comparison.html#Three-way_comparison)operator ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_impl_three_way_comparison))*[P0515R3](https://wg21.link/P0515R3)10

[P0588R1](https://wg21.link/P0588R1)[init-statements for range-based for](https://en.cppreference.com/language/range-for.html#Syntax)[P0614R1](https://wg21.link/P0614R1)[lambdas](https://en.cppreference.com/language/lambda.html)[P0624R2](https://wg21.link/P0624R2)[P0641R2](https://wg21.link/P0641R2)[P0692R1](https://wg21.link/P0692R1)14

[P0846R0](https://wg21.link/P0846R0)[needed for constant evaluation](https://en.cppreference.com/language/constant_expression.html#Functions_and_variables_needed_for_constant_evaluation)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr_in_decltype))*[P0859R0](https://wg21.link/P0859R0)9

19.31**

`[[`[likely](https://en.cppreference.com/language/attributes/likely.html)]]

and `[[`[unlikely](https://en.cppreference.com/language/attributes/likely.html)]]

[P0479R5](https://wg21.link/P0479R5)[more optional](https://en.cppreference.com/keywords/typename.html)`typename`[P0634R3](https://wg21.link/P0634R3)[in](https://en.cppreference.com/language/parameter_pack.html)`Pack-expansions`[lambda init-captures](https://en.cppreference.com/language/lambda.html#Lambda_capture)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_init_captures))*[P0780R2](https://wg21.link/P0780R2)`[[`[no_unique_address](https://en.cppreference.com/language/attributes/no_unique_address.html)]]

[P0840R2](https://wg21.link/P0840R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_concepts))*[P0848R3](https://wg21.link/P0848R3)[structured bindings](https://en.cppreference.com/language/structured_binding.html)customization point finding rules[P0961R1](https://wg21.link/P0961R1)[range-for](https://en.cppreference.com/language/range-for.html)loop customization point finding rules[P0962R1](https://wg21.link/P0962R1)[P0969R0](https://wg21.link/P0969R0)[Destroying](https://en.cppreference.com/memory/new/operator_delete.html)(`operator delete`

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_impl_destroying_delete))*[P0722R3](https://wg21.link/P0722R3)[Constant template parameters](https://en.cppreference.com/language/template_parameters.html#Constant_template_parameter)[P0732R2](https://wg21.link/P0732R2)19.28 (16.9)*

[capture](https://en.cppreference.com/language/lambda.html#Lambda_capture)of this via`[=]`

[P0806R2](https://wg21.link/P0806R2)[(](https://en.cppreference.com/language/explicit.html)`explicit(bool)`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_conditional_explicit))*[P0892R2](https://wg21.link/P0892R2)[feature-test macros](https://en.cppreference.com/experimental/feature_test.html)[P0941R2](https://wg21.link/P0941R2)19.20*

[P1008R1](https://wg21.link/P1008R1)[virtual function](https://en.cppreference.com/language/virtual.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))*[P1064R0](https://wg21.link/P1064R0)[P1120R0](https://wg21.link/P1120R0)10

[char8_t](https://en.cppreference.com/language/types.html#char8_t)

([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_char8_t))*[P0482R6](https://wg21.link/P0482R6)[(](https://en.cppreference.com/types/is_constant_evaluated.html)`std::is_constant_evaluated()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_constant_evaluated))*[P0595R2](https://wg21.link/P0595R2)[P1002R1](https://wg21.link/P1002R1)[Immediate functions](https://en.cppreference.com/language/consteval.html)(consteval) ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_consteval))*[P1073R3](https://wg21.link/P1073R3)11

14 (partial)*

17

(partial)*

19.29 (16.10)*

15.0.0*

[Nested inline namespaces](https://en.cppreference.com/language/namespace.html)[P1094R2](https://wg21.link/P1094R2)[constrained](https://en.cppreference.com/language/template_parameters.html#Type_template_parameter)[declarations](https://en.cppreference.com/language/auto.html)[P1141R2](https://wg21.link/P1141R2)19.28 (16.9)*

[P1236R1](https://wg21.link/P1236R1)[and polymorphic](https://en.cppreference.com/language/dynamic_cast.html)`dynamic_cast`[in](https://en.cppreference.com/language/typeid.html)`typeid`[constant expressions](https://en.cppreference.com/language/constant_expression.html)[P1327R1](https://wg21.link/P1327R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))*[P1330R0](https://wg21.link/P1330R0)[Coroutines](https://en.cppreference.com/language/coroutines.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_impl_coroutine))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_coroutine))*[P0912R5](https://wg21.link/P0912R5)[LWG3393](https://wg21.link/LWG3393)17 (partial)*

19.10**

19.28 (16.8)*

[initialization of aggregates](https://en.cppreference.com/language/aggregate_initialization.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_aggregate_paren_init))*[P0960R3](https://wg21.link/P0960R3)`new`

-expressions[P1009R2](https://wg21.link/P1009R2)[Modules](https://en.cppreference.com/language/modules.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_modules))*[P1103R3](https://wg21.link/P1103R3)19.10**

19.28 (16.8)*

[P1041R4](https://wg21.link/P1041R4)[P1139R2](https://wg21.link/P1139R2)19.26**

`<=> != ==`

[P1185R2](https://wg21.link/P1185R2)[P1286R2](https://wg21.link/P1286R2)[P1091R3](https://wg21.link/P1091R3)[P1381R1](https://wg21.link/P1381R1)16

19.24**

[P0388R4](https://wg21.link/P0388R4)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr_dynamic_alloc))*[P0784R7](https://wg21.link/P0784R7)`volatile`

[P1152R4](https://wg21.link/P1152R4)[(](https://en.cppreference.com/language/constinit.html)`constinit`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constinit))*[P1143R2](https://wg21.link/P1143R2)[Deprecate comma operator in subscripts](https://en.cppreference.com/language/operator_other.html#Built-in_comma_operator)[P1161R3](https://wg21.link/P1161R3)`[[`[nodiscard](https://en.cppreference.com/language/attributes/nodiscard.html)]]

with message
[P1301R4](https://wg21.link/P1301R4)[P1331R2](https://wg21.link/P1331R2)[P1668R1](https://wg21.link/P1668R1)[(](https://en.cppreference.com/language/enum.html#Using-enum-declaration)`using enum`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_using_enum))*[P1099R5](https://wg21.link/P1099R5)[Three-way comparison](https://en.cppreference.com/language/operator_comparison.html#Three-way_comparison)for specified comparison category[P1186R3](https://wg21.link/P1186R3)`[[`[nodiscard](https://en.cppreference.com/language/attributes/nodiscard.html)]]

for constructors
[P1771R1](https://wg21.link/P1771R1)[class template argument deduction](https://en.cppreference.com/language/ctad.html)for alias templates ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_deduction_guides))*[P1814R0](https://wg21.link/P1814R0)[class template argument deduction](https://en.cppreference.com/language/ctad.html)for aggregates ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_deduction_guides))*[P1816R0](https://wg21.link/P1816R0)[P2082R1](https://wg21.link/P2082R1)11*

2024.1

[Implicit move](https://en.cppreference.com/language/return.html)for more local objects and rvalue references[P1825R0](https://wg21.link/P1825R0)[P1946R0](https://wg21.link/P1946R0)`std::weak_equality`

and `std::strong_equality`

[P1959R0](https://wg21.link/P1959R0)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_nontype_template_args))*[P1907R1](https://wg21.link/P1907R1)11

[P0593R6](https://wg21.link/P0593R6)[P1957R2](https://wg21.link/P1957R2)11*

C++20 feature

Paper(s)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/20&action=edit§ion=T-2)] C++20 library features

| C++20 feature |
Paper(s) |
GCC libstdc++ |
Clang libc++ |
MSVC STL |
Apple Clang* |
|
|---|---|---|---|---|---|---|
std::endian |

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_endian))*

[P0463R1](https://wg21.link/P0463R1)[std::make_shared()](https://en.cppreference.com/memory/shared_ptr/make_shared.html)to support arrays ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_shared_ptr_arrays))*[P0674R1](https://wg21.link/P0674R1)[Floating-point atomic](https://en.cppreference.com/atomic/atomic.html#Specializations_for_floating-point_types)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_float))*[P0020R6](https://wg21.link/P0020R6)[Synchronized buffered](https://en.cppreference.com/io/basic_syncbuf.html)([) (](https://en.cppreference.com/io/basic_osyncstream.html)`std::basic_osyncstream`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_syncbuf))*[P0053R7](https://wg21.link/P0053R7)[and](https://en.cppreference.com/header/algorithm.html)`<algorithm>`[(](https://en.cppreference.com/header/utility.html)`<utility>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_algorithms))*[P0202R3](https://wg21.link/P0202R3)12

13.0.0*

[(](https://en.cppreference.com/header/complex.html)`<complex>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_complex))*[P0415R1](https://wg21.link/P0415R1)16

15.0.0*

[std::memory_order](https://en.cppreference.com/atomic/memory_order.html)a scoped enumeration[P0439R0](https://wg21.link/P0439R0)[String](https://en.cppreference.com/string/basic_string.html)[prefix](https://en.cppreference.com/string/basic_string/starts_with.html)and[suffix](https://en.cppreference.com/string/basic_string/ends_with.html)checking:`string``(_view)`[/](https://en.cppreference.com/string/basic_string/starts_with.html)`::starts_with`[(](https://en.cppreference.com/string/basic_string_view/ends_with.html)`ends_with`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_starts_ends_with))*[P0457R2](https://wg21.link/P0457R2)`operator<=>`

[(](https://en.cppreference.com/header/compare.html)`<compare>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_three_way_comparison))*[P0768R1](https://wg21.link/P0768R1)12 (partial)*

17

19.28 (16.9)*

[(](https://en.cppreference.com/types/remove_cvref.html)`std::remove_cvref`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_remove_cvref))*[P0550R2](https://wg21.link/P0550R2)`[[`[nodiscard](https://en.cppreference.com/language/attributes/nodiscard.html)]]

in the [standard library](https://en.cppreference.com/language/attributes/nodiscard.html#Standard_library)[P0600R1](https://wg21.link/P0600R1)16

19.22*

15.0.0*

[in](https://en.cppreference.com/utility/move.html)`std::move`[numeric algorithms](https://en.cppreference.com/algorithm.html#Numeric_operations)[P0616R0](https://wg21.link/P0616R0)[Utility](https://en.cppreference.com/memory/to_address.html)to convert a pointer to a raw pointer ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_to_address))*[P0653R2](https://wg21.link/P0653R2)[and](https://en.cppreference.com/memory/shared_ptr/atomic2.html)`std::shared_ptr`[(](https://en.cppreference.com/memory/weak_ptr/atomic2.html)`std::weak_ptr`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_shared_ptr))*[P0718R2](https://wg21.link/P0718R2)[(](https://en.cppreference.com/container/span.html)`std::span`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_span))*[P0122R7](https://wg21.link/P0122R7)[Calendar](https://en.cppreference.com/chrono.html#Calendar)and[Time zone](https://en.cppreference.com/chrono.html#Time_zone)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_chrono))*[P0355R7](https://wg21.link/P0355R7)13 (partial)*

14

19 (

[partial](https://libcxx.llvm.org/Status/Cxx20.html#note-p0355))*`<version>`[P0754R2](https://wg21.link/P0754R2)[P0809R0](https://wg21.link/P0809R0)[ConstexprIterator](https://en.cppreference.com/named_req/ConstexprIterator.html)requirements ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_string_view))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_array_constexpr))*[P0858R0](https://wg21.link/P0858R0)[std::basic_string::reserve()](https://en.cppreference.com/string/basic_string/reserve.html)should not shrink[P0966R1](https://wg21.link/P0966R1)[Atomic Compare-And-Exchange](https://en.cppreference.com/atomic/atomic/compare_exchange.html)with padding bits[P0528R3](https://wg21.link/P0528R3)[(](https://en.cppreference.com/atomic/atomic_ref.html)`std::atomic_ref`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_ref))*[P0019R8](https://wg21.link/P0019R8)`std::map::contains()`[P0458R2](https://wg21.link/P0458R2)[piecewise construction](https://en.cppreference.com/memory/scoped_allocator_adaptor/construct.html)[P0475R1](https://wg21.link/P0475R1)[(](https://en.cppreference.com/numeric/bit_cast.html)`std::bit_cast()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_bit_cast))*[P0476R2](https://wg21.link/P0476R2)[Integral power-of-2 operations](https://en.cppreference.com/utility/bit.html):[ std::bit_ceil()](https://en.cppreference.com/numeric/bit_ceil.html),

[,](https://en.cppreference.com/numeric/bit_floor.html)

`std::bit_floor()`[,](https://en.cppreference.com/numeric/bit_width.html)

`std::bit_width()`[(](https://en.cppreference.com/numeric/has_single_bit.html)

`std::has_single_bit()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_int_pow2))*

[P0556R3](https://wg21.link/P0556R3)[P1956R1](https://wg21.link/P1956R1)10*

12*

19.27**

19.28 (16.8)*

13.0.0**

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_list_remove_return_type))*[P0646R1](https://wg21.link/P0646R1)[(](https://en.cppreference.com/memory/new/destroying_delete_t.html)`std::destroying_delete_t`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_destroying_delete))*[P0722R3](https://wg21.link/P0722R3)[(](https://en.cppreference.com/types/is_convertible.html)`std::is_convertible`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_nothrow_convertible))*[P0758R1](https://wg21.link/P0758R1)[to](https://en.cppreference.com/algorithm/shift.html)`std::shift_left/right`[(](https://en.cppreference.com/header/algorithm.html)`<algorithm>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_shift))*[P0769R2](https://wg21.link/P0769R2)[std::swap()](https://en.cppreference.com/utility/swap.html)and`swap`

related functions
[P0879R0](https://wg21.link/P0879R0)[(](https://en.cppreference.com/types/type_identity.html)`std::type_identity`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_type_identity))*[P0887R1](https://wg21.link/P0887R1)[Concepts library](https://en.cppreference.com/concepts.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_concepts))*[P0898R3](https://wg21.link/P0898R3)`constexpr`

[comparison operators](https://en.cppreference.com/container/array/operator_cmp.html)for[std::array](https://en.cppreference.com/container/array.html)[P1023R0](https://wg21.link/P1023R0)[(](https://en.cppreference.com/utility/functional/unwrap_reference.html)`std::unwrap_ref_decay`

and `std::unwrap_reference`

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_unwrap_ref))*[P0318R1](https://wg21.link/P0318R1)[(](https://en.cppreference.com/utility/functional/bind_front.html)`std::bind_front()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_bind_front))*[P0356R5](https://wg21.link/P0356R5)[std::reference_wrapper](https://en.cppreference.com/utility/functional/reference_wrapper.html)for incomplete types[P0357R3](https://wg21.link/P0357R3)`operator>>(basic_istream&, CharT*)`[P0487R1](https://wg21.link/P0487R1)[char8_t](https://en.cppreference.com/language/types.html#char8_t)

([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_char8_t))*[P0482R6](https://wg21.link/P0482R6)16

15.0.0*

[Utility functions](https://en.cppreference.com/memory/uses_allocator_construction_args.html)to implement[uses-allocator](https://en.cppreference.com/memory/make_obj_using_allocator.html)[construction](https://en.cppreference.com/memory/uninitialized_construct_using_allocator.html)[P0591R4](https://wg21.link/P0591R4)[std::variant](https://en.cppreference.com/utility/variant.html)and[std::optional](https://en.cppreference.com/utility/optional.html)should propagate copy/move triviality[P0602R4](https://wg21.link/P0602R4)[std::variant](https://en.cppreference.com/utility/variant.html)converting constructor[P0608R3](https://wg21.link/P0608R3)19.42**

[std::function](https://en.cppreference.com/utility/functional/function.html)'s move constructor should be`noexcept`[P0771R1](https://wg21.link/P0771R1)[One](https://en.cppreference.com/iterator.html)[Ranges](https://en.cppreference.com/ranges.html)[Proposal](https://en.cppreference.com/algorithm/ranges.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ranges))*[P0896R4](https://wg21.link/P0896R4)15*

[unordered associative containers](https://en.cppreference.com/container.html#Unordered_associative_containers)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_generic_unordered_lookup))*[P0919R3](https://wg21.link/P0919R3)[P1690R1](https://wg21.link/P1690R1)19.25* (P1690R1)

`<chrono>``zero()`

, `min()`

, and `max()`

should be `noexcept`[P0972R0](https://wg21.link/P0972R0)[std::pointer_traits](https://en.cppreference.com/memory/pointer_traits.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_memory))*[P1006R1](https://wg21.link/P1006R1)[(](https://en.cppreference.com/memory/assume_aligned.html)`std::assume_aligned()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_assume_aligned))*[P1007R3](https://wg21.link/P1007R3)11

[) (](https://en.cppreference.com/memory/unique_ptr/make_unique.html)`make_unique_for_overwrite`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_smart_ptr_for_overwrite))*[P1020R1](https://wg21.link/P1020R1)[P1973R1](https://wg21.link/P1973R1)12*

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_array_constexpr))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_functional))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_iterator))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_tuple))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_utility))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_string_view))*[P1032R1](https://wg21.link/P1032R1)`std::span`[P1085R2](https://wg21.link/P1085R2)`operator+(basic_string)`[P1165R1](https://wg21.link/P1165R1)[, or](https://en.cppreference.com/container/vector/erase2.html)`std::erase(std::vector)`[(](https://en.cppreference.com/container/map/erase_if.html)`std::erase_if(std::map)`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_erase_if))*[P1209R0](https://wg21.link/P1209R0)[P1115R3](https://wg21.link/P1115R3)10*

11*

19.27**

12.0.5**

[P1502R1](https://wg21.link/P1502R1)[as a vocabulary type (](https://en.cppreference.com/memory/polymorphic_allocator.html)`polymorphic_allocator<>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_polymorphic_allocator))*[P0339R6](https://wg21.link/P0339R6)[(](https://en.cppreference.com/algorithm/execution_policy_tag.html)`std::execution::unseq`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_execution))*[P1001R2](https://wg21.link/P1001R2)[and](https://en.cppreference.com/numeric/lerp.html)`std::lerp()`[(](https://en.cppreference.com/numeric/midpoint.html)`std::midpoint()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_interpolate))*[P0811R3](https://wg21.link/P0811R3)19.28 (16.8)*

`std::span`[P1024R3](https://wg21.link/P1024R3)14

[intuitive](https://en.cppreference.com/filesystem/create_directory.html)`std::create_directory()`[P1164R1](https://wg21.link/P1164R1)[and unsigned extent for](https://en.cppreference.com/iterator/size.html)`std::ssize()`[(](https://en.cppreference.com/container/span.html)`std::span`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_ssize))*[P1227R2](https://wg21.link/P1227R2)[un](https://en.cppreference.com/types/is_unbounded_array.html))[bounded](https://en.cppreference.com/types/is_bounded_array.html)arrays ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_bounded_array_traits))*[P1357R1](https://wg21.link/P1357R1)[(](https://en.cppreference.com/container/array/to_array.html)`std::to_array()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_to_array))*[P0325R4](https://wg21.link/P0325R4)[std::basic_stringbuf](https://en.cppreference.com/io/basic_stringbuf.html)âs buffer[P0408R7](https://wg21.link/P0408R7)[Layout](https://en.cppreference.com/types/is_layout_compatible.html)-[compatibility](https://en.cppreference.com/types/is_corresponding_member.html)and[pointer](https://en.cppreference.com/types/is_pointer_interconvertible_base_of.html)-[interconvertibility](https://en.cppreference.com/types/is_pointer_interconvertible_with_class.html)traits ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_layout_compatible))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_pointer_interconvertible))*[P0466R5](https://wg21.link/P0466R5)[Bit operations](https://en.cppreference.com/utility/bit.html): std::[ rotl()](https://en.cppreference.com/numeric/rotl.html),

[,](https://en.cppreference.com/numeric/rotr.html)

`rotr()`[,](https://en.cppreference.com/numeric/countl_zero.html)

`countl_zero()`[,](https://en.cppreference.com/numeric/countl_one.html)

`countl_one()`[,](https://en.cppreference.com/numeric/countr_zero.html)

`countr_zero()`[,](https://en.cppreference.com/numeric/countr_one.html)

`countr_one()`[(](https://en.cppreference.com/numeric/popcount.html)

`popcount()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_bitops))*

[P0553R4](https://wg21.link/P0553R4)19.28 (16.8)*

[Mathematical constants](https://en.cppreference.com/numeric/constants.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_math_constants))*[P0631R8](https://wg21.link/P0631R8)[Text formatting](https://en.cppreference.com/utility/format.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_format))*[P0645R10](https://wg21.link/P0645R10)17

[and](https://en.cppreference.com/thread/stop_token.html)`std::stop_token`[(](https://en.cppreference.com/thread/jthread.html)`std::jthread`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_jthread))*[P0660R10](https://wg21.link/P0660R10)(partial)*

20*

[std::allocator](https://en.cppreference.com/memory/allocator.html)and related utilities ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_dynamic_alloc))*[P0784R7](https://wg21.link/P0784R7)[std::string](https://en.cppreference.com/string/basic_string.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_string))*[P0426R1](https://wg21.link/P0426R1)[P1032R1](https://wg21.link/P1032R1)[P0980R1](https://wg21.link/P0980R1)19.30**

[std::vector](https://en.cppreference.com/container/vector.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_vector))*[P1004R2](https://wg21.link/P1004R2)19.30**

[range adaptors](https://en.cppreference.com/ranges.html)[P1035R7](https://wg21.link/P1035R7)[std::invoke()](https://en.cppreference.com/utility/functional/invoke.html)and related utilities[P1065R2](https://wg21.link/P1065R2)[,](https://en.cppreference.com/thread/counting_semaphore.html)`std::counting_semaphore`[and](https://en.cppreference.com/thread/latch.html)`std::latch`[(](https://en.cppreference.com/thread/barrier.html)`std::barrier`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_flag_test))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_lock_free_type_aliases))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_wait))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_barrier))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_latch))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_semaphore))*[P1135R6](https://wg21.link/P1135R6)[(](https://en.cppreference.com/utility/source_location.html)`std::source_location`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_source_location))*[P1208R6](https://wg21.link/P1208R6)(partial)

16

[to the standard library](https://en.cppreference.com/language/operator_comparison.html#Three-way_comparison)`<=>`[P1614R2](https://wg21.link/P1614R2)(partial)

17*

(partial)

19

[std::atomic](https://en.cppreference.com/atomic/atomic.html)and[std::atomic_flag](https://en.cppreference.com/atomic/atomic_flag.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_value_initialization))*[P0883R2](https://wg21.link/P0883R2)[numeric algorithms](https://en.cppreference.com/numeric.html#Numeric_operations)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_numeric))*[P1645R1](https://wg21.link/P1645R1)[Safe integral comparisons](https://en.cppreference.com/utility.html#Integer_comparison_functions)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_integer_comparison_functions))*[P0586R2](https://wg21.link/P0586R2)C++20 feature

Paper(s)

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/compiler_support&action=edit§ion=5)] Older standards

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/compiler_support&action=edit§ion=6)] See also

|
Feature testing |

[C documentation](https://en.cppreference.com/c/compiler_support.html)for compiler support
