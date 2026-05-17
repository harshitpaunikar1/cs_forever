Title: C++20 - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/20.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:06:48+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# C++20

From cppreference.com

<

[cpp](https://en.cppreference.com/cpp.html)C++20 is a major version after C++17, featuring major features (concepts, modules, coroutines, and ranges) and other language and library features. The standard was published in December 2020.

| This section is incomplete |

## Contents |

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/20&action=edit§ion=1)] New language features

-
[Feature test macros](https://en.cppreference.com/experimental/feature_test.html) -
[Three-way comparison](https://en.cppreference.com/language/operator_comparison.html#Three-way_comparison)operator <=> and[operator==() = default](https://en.cppreference.com/language/default_comparisons.html) -
[Designated initializers](https://en.cppreference.com/language/aggregate_initialization.html#Designated_initializers) - Init-statements and initializers in
[range-](https://en.cppreference.com/language/range-for.html)`for`

-
`char8_t` - New
[attributes](https://en.cppreference.com/language/attributes.html):`[[`

,[no_unique_address](https://en.cppreference.com/language/attributes/no_unique_address.html)]]`[[`

,[likely](https://en.cppreference.com/language/attributes/likely.html)]]`[[`

[unlikely](https://en.cppreference.com/language/attributes/likely.html)]] -
in`Pack-expansions`[lambda init-captures](https://en.cppreference.com/language/lambda.html#Lambda_capture) - Removed the requirement to use
`typename`

to disambiguate types in many contexts -
,`consteval``constinit` - Further relaxed constexpr
- Signed integers are 2's complement
-
[Bitwise shift operators](https://en.cppreference.com/language/operator_arithmetic.html)unified behavior -
[aggregate initialization](https://en.cppreference.com/language/aggregate_initialization.html)using parentheses -
[coroutines](https://en.cppreference.com/language/coroutines.html) -
[modules](https://en.cppreference.com/language/modules.html) -
[Constraints and concepts](https://en.cppreference.com/language/constraints.html) -
[Abbreviated function template](https://en.cppreference.com/language/function_template.html#Abbreviated_function_template) - DR11:
[array new](https://en.cppreference.com/language/new.html#Defect_reports)can deduce array size

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/20&action=edit§ion=2)] New library features

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/20&action=edit§ion=3)] New headers

-
`<bit>` -
`<compare>` -
`<concepts>` -
`<coroutine>` -
`<format>` -
`<numbers>` -
`<ranges>` -
`<source_location>` -
`<span>` -
`<syncstream>` -
`<version>`

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/20&action=edit§ion=4)] Library features

-
[Library feature-test macros](https://en.cppreference.com/utility/feature_test.html) -
[Formatting library](https://en.cppreference.com/utility/format.html) -
[Concepts library](https://en.cppreference.com/concepts.html) -
[Calendar](https://en.cppreference.com/chrono.html#Calendar)and[Time zone](https://en.cppreference.com/chrono.html#Time_zone)library in`<chrono>` -
[std::source_location](https://en.cppreference.com/utility/source_location.html) -
`std::span` -
:`std::endian``big`

/`little`

/`native`

- Integral power-of-2 operations and
in`std::bit_cast``<bit>` - Array support for
[std::make_shared](https://en.cppreference.com/memory/shared_ptr/make_shared.html) -
`std::remove_cvref` -
`std::to_address` -
[Floating-point atomics](https://en.cppreference.com/atomic/atomic.html#Specializations_for_floating-point_types),atomics`std::shared_ptr` - Thread-coordination classes:
,`std::barrier`, and`std::latch``std::counting_semaphore` -
and`std::jthread`[thread cancellation](https://en.cppreference.com/atomic.html#Thread_cancellation)classes:,`std::stop_token`, and`std::stop_source``std::stop_callback` -
`std::basic_osyncstream` -
and other`std::basic_string`uses`char8_t` - constexpr for
,`<algorithm>`,`<utility>``<complex>` -
/`string::starts_with`and`ends_with`/`string_view::starts_with``ends_with` -
`std::assume_aligned` -
`std::bind_front` -
/`std::c8rtomb``std::mbrtoc8` -
etc`std::make_obj_using_allocator` -
/`std::make_shared_for_overwrite``std::make_unique_for_overwrite` - Heterogeneous lookup in unordered associative containers
-
with additional member functions and`std::pmr::polymorphic_allocator`as its default template argument`std::byte` -
`execution::unseq` -
and`std::midpoint``std::lerp` -
`std::ssize` -
,`std::is_bounded_array``std::is_unbounded_array` -
[Ranges](https://en.cppreference.com/ranges.html) - Uniform container erasure:
[std::erase](https://en.cppreference.com/container/vector/erase2.html)/[std::erase_if](https://en.cppreference.com/container/vector/erase2.html), e.g.or`std::erase(std::list)`etc`erase_if(std::map)` -
[Mathematical constants](https://en.cppreference.com/numeric/constants.html)in`<numbers>`

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/20&action=edit§ion=5)] Defect reports

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/20&action=edit§ion=6)] Compiler support

Main Article: [C++20 compiler support](https://en.cppreference.com/compiler_support.html#C.2B.2B20_features)

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

GCC

Clang

MSVC

Apple Clang

EDG eccp

Intel C++

Nvidia HPC C++ (ex PGI)*

Nvidia nvcc

Cray

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

GCC libstdc++

Clang libc++

MSVC STL

Apple Clang*

DR*nn* - the number *nn* after "DR" denotes target C++ revision the Defect Report is applied to, e.g., DR20 → C++20.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/20&action=edit§ion=7)] External links

| 1. |
|
