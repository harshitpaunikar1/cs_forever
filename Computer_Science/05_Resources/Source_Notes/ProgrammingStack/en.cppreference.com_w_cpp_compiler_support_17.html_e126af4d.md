Title: Compiler support for C++17 - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/compiler_support/17.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:07:13+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# Compiler support for C++17

From cppreference.com

<

[cpp](https://en.cppreference.com/cpp.html) |[compiler support](https://en.cppreference.com/compiler_support.html)

DR*nn* - the number *nn* after "DR" denotes target C++ revision the Defect Report is applied to, e.g., DR20 → C++20.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/17&action=edit§ion=T-1)] C++17 core language features

| C++17 feature |
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
|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| DR11: New
auto |

[N3922](https://wg21.link/N3922)[N4051](https://wg21.link/N4051)[trigraphs](https://en.cppreference.com/language/operator_alternative.html#Trigraphs)[N4086](https://wg21.link/N4086)[Nested namespace](https://en.cppreference.com/language/namespace.html#Syntax)definition[N4230](https://wg21.link/N4230)[with no message (](https://en.cppreference.com/language/static_assert.html)`static_assert`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_static_assert))*[N3928](https://wg21.link/N3928)[Attributes](https://en.cppreference.com/language/attributes.html)for namespaces and enumerators ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_enumerator_attributes))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_namespace_attributes))*[N4266](https://wg21.link/N4266)6

`u8`

character literals[N4267](https://wg21.link/N4267)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_nontype_template_args))*[N4268](https://wg21.link/N4268)[Unary fold expressions](https://en.cppreference.com/language/fold.html#Explanation)and empty parameter packs[P0036R0](https://wg21.link/P0036R0)[keyword](https://en.cppreference.com/keyword/register.html)`register`[P0001R1](https://wg21.link/P0001R1)[P0002R1](https://wg21.link/P0002R1)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_noexcept_function_type))*[P0012R1](https://wg21.link/P0012R1)[in preprocessor conditionals](https://en.cppreference.com/preprocessor/include.html)`__has_include`[P0061R1](https://wg21.link/P0061R1)[inheriting constructors](https://en.cppreference.com/language/using_declaration.html#Inheriting_constructors)([DR1941](https://wg21.link/DR1941)et al) ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_inheriting_constructors))*[P0136R1](https://wg21.link/P0136R1)[Aggregate classes](https://en.cppreference.com/language/aggregate_initialization.html)with base classes ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_aggregate_bases))*[P0017R1](https://wg21.link/P0017R1)[Fold Expressions](https://en.cppreference.com/language/fold.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_fold_expressions))*[N4295](https://wg21.link/N4295)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_capture_star_this))*[P0018R3](https://wg21.link/P0018R3)[P0138R2](https://wg21.link/P0138R2)[(](https://en.cppreference.com/language/lambda.html)`constexpr`

lambda expressions[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))*[P0170R1](https://wg21.link/P0170R1)[range-based for](https://en.cppreference.com/language/range-for.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_range_based_for))*[P0184R0](https://wg21.link/P0184R0)`[[`[fallthrough](https://en.cppreference.com/language/attributes/fallthrough.html)]]

[attribute](https://en.cppreference.com/language/attributes.html)[P0188R1](https://wg21.link/P0188R1)`[[`[nodiscard](https://en.cppreference.com/language/attributes/nodiscard.html)]]

[attribute](https://en.cppreference.com/language/attributes.html)[P0189R1](https://wg21.link/P0189R1)`[[`[maybe_unused](https://en.cppreference.com/language/attributes/maybe_unused.html)]]

[attribute](https://en.cppreference.com/language/attributes.html)[P0212R1](https://wg21.link/P0212R1)[floating-point literals](https://en.cppreference.com/language/floating_literal.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_hex_float))*[P0245R1](https://wg21.link/P0245R1)[P0028R4](https://wg21.link/P0028R4)[Dynamic memory allocation](https://en.cppreference.com/language/new.html)for over-aligned data ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_aligned_new))*[P0035R4](https://wg21.link/P0035R4)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_nontype_template_parameter_auto))*[P0127R2](https://wg21.link/P0127R2)[copy elision](https://en.cppreference.com/language/copy_elision.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_guaranteed_copy_elision))*[P0135R1](https://wg21.link/P0135R1)[P0137R1](https://wg21.link/P0137R1)[expression evaluation order](https://en.cppreference.com/language/eval_order.html)[P0145R3](https://wg21.link/P0145R3)[Structured Bindings](https://en.cppreference.com/language/structured_binding.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_structured_bindings))*[P0217R3](https://wg21.link/P0217R3)[attributes](https://en.cppreference.com/language/attributes.html)[P0283R2](https://wg21.link/P0283R2)[constexpr if](https://en.cppreference.com/language/if.html)statements ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_if_constexpr))*[P0292R2](https://wg21.link/P0292R2)[if](https://en.cppreference.com/language/if.html)and[switch](https://en.cppreference.com/language/switch.html)[P0305R1](https://wg21.link/P0305R1)[Inline variables](https://en.cppreference.com/language/inline.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_inline_variables))*[P0386R2](https://wg21.link/P0386R2)[dynamic exception specifications](https://en.cppreference.com/language/except_spec.html)[P0003R5](https://wg21.link/P0003R5)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_variadic_using))*[P0195R2](https://wg21.link/P0195R2)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_template_template_args))*[P0522R0](https://wg21.link/P0522R0)[Class template argument deduction](https://en.cppreference.com/language/ctad.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_deduction_guides))*[P0091R3](https://wg21.link/P0091R3)C++17 feature

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

Embarcadero C++ Builder

IBM Open XL C++ for AIX

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/17&action=edit§ion=T-2)] C++17 library features

| C++17 feature |
Paper(s) |
GCC libstdc++ |
Clang libc++ |
MSVC STL |
Apple Clang* |
IBM Open XL C/C++ for AIX* |
Intel Parallel STL |
Embarcadero C++ Builder* |
|
|---|---|---|---|---|---|---|---|---|---|
|

[N3911](https://wg21.link/N3911)[(](https://en.cppreference.com/error/exception/uncaught_exception.html)`std::uncaught_exceptions()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_uncaught_exceptions))*[N4259](https://wg21.link/N4259)[std::size()](https://en.cppreference.com/iterator/size.html),[std::empty()](https://en.cppreference.com/iterator/empty.html)and[std::data()](https://en.cppreference.com/iterator/data.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_nonmember_container_access))*[N4280](https://wg21.link/N4280)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_allocator_traits_is_always_equal))*[N4258](https://wg21.link/N4258)[std::invoke](https://en.cppreference.com/utility/functional/invoke.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_invoke))*[N4169](https://wg21.link/N4169)[std::map::try_emplace](https://en.cppreference.com/container/map/try_emplace.html),[std::map::insert_or_assign](https://en.cppreference.com/container/map/insert_or_assign.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_map_try_emplace))*[N4279](https://wg21.link/N4279)[std::unordered_map::try_emplace](https://en.cppreference.com/container/unordered_map/try_emplace.html),[std::unordered_map::insert_or_assign](https://en.cppreference.com/container/unordered_map/insert_or_assign.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_unordered_map_try_emplace))*[N4279](https://wg21.link/N4279)[std::pair](https://en.cppreference.com/utility/pair.html)and[std::tuple](https://en.cppreference.com/utility/tuple.html)[N4387](https://wg21.link/N4387)[std::bool_constant](https://en.cppreference.com/types/integral_constant.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_bool_constant))*[N4389](https://wg21.link/N4389)[std::shared_mutex](https://en.cppreference.com/thread/shared_mutex.html)(untimed) ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_shared_mutex))*[N4508](https://wg21.link/N4508)[std::forward_list](https://en.cppreference.com/container/forward_list.html),[std::list](https://en.cppreference.com/container/list.html), and[std::vector](https://en.cppreference.com/container/vector.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_incomplete_container_elements))*[N4510](https://wg21.link/N4510)[Type traits](https://en.cppreference.com/meta.html)variable templates ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_type_trait_variable_templates))*[P0006R0](https://wg21.link/P0006R0)[Logical operator type traits](https://en.cppreference.com/meta.html#Operations_on_traits)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_logical_traits))*[P0013R1](https://wg21.link/P0013R1)[std::as_const](https://en.cppreference.com/utility/as_const.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_as_const))*[P0007R1](https://wg21.link/P0007R1)[std::chrono::duration](https://en.cppreference.com/chrono/duration.html)and[std::chrono::time_point](https://en.cppreference.com/chrono/time_point.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_chrono))*[P0092R1](https://wg21.link/P0092R1)[std::owner_less](https://en.cppreference.com/memory/owner_less.html)(std::owner_less<void>) ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_transparent_operators))*[P0074R0](https://wg21.link/P0074R0)[std::not_fn](https://en.cppreference.com/utility/functional/not_fn.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_not_fn))*[P0005R4](https://wg21.link/P0005R4)[P0358R1](https://wg21.link/P0358R1)[execution policies](https://en.cppreference.com/algorithm.html#Execution_policies)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_execution))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_parallel_algorithm))*[P0024R2](https://wg21.link/P0024R2)(partial)*

[std::clamp()](https://en.cppreference.com/algorithm/clamp.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_clamp))*[P0025R1](https://wg21.link/P0025R1)[(nothrow-)swappable traits](https://en.cppreference.com/types/is_swappable.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_swappable))*[P0185R1](https://wg21.link/P0185R1)[Polymorphic memory resources](https://en.cppreference.com/header/memory_resource.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_memory_resource))*[P0220R1](https://wg21.link/P0220R1)[std::apply](https://en.cppreference.com/utility/apply.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_apply))*[P0220R1](https://wg21.link/P0220R1)[Searchers](https://en.cppreference.com/functional.html#Searchers)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_boyer_moore_searcher))*[P0220R1](https://wg21.link/P0220R1)[std::sample](https://en.cppreference.com/algorithm/sample.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_sample))*[P0220R1](https://wg21.link/P0220R1)[Mathematical special functions](https://en.cppreference.com/numeric/special_math.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_math_special_functions))*[P0226R1](https://wg21.link/P0226R1)[std::addressof](https://en.cppreference.com/memory/addressof.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_addressof_constexpr))*[LWG2296](https://wg21.link/LWG2296)[std::reverse_iterator](https://en.cppreference.com/iterator/reverse_iterator.html),[std::move_iterator](https://en.cppreference.com/iterator/move_iterator.html),[std::array](https://en.cppreference.com/container/array.html)and range access ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_array_constexpr))*[P0031R0](https://wg21.link/P0031R0)[std::atomic](https://en.cppreference.com/atomic/atomic.html)<T>::is_always_lock_free ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_atomic_is_always_lock_free))*[P0152R1](https://wg21.link/P0152R1)[std::enable_shared_from_this::weak_from_this](https://en.cppreference.com/memory/enable_shared_from_this/weak_from_this.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_enable_shared_from_this))*[P0033R1](https://wg21.link/P0033R1)[std::hypot](https://en.cppreference.com/numeric/math/hypot.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hypot))*[P0030R1](https://wg21.link/P0030R1)[(](https://en.cppreference.com/types/byte.html)`std::byte`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_byte))*[P0298R3](https://wg21.link/P0298R3)[std::string_view](https://en.cppreference.com/string/basic_string_view.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_string_view))*[N3921](https://wg21.link/N3921)[P0220R1](https://wg21.link/P0220R1)[P0254R2](https://wg21.link/P0254R2)[P0403R1](https://wg21.link/P0403R1)19.11**

[std::any](https://en.cppreference.com/utility/any.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_any))*[P0220R1](https://wg21.link/P0220R1)[P0032R3](https://wg21.link/P0032R3)[std::optional](https://en.cppreference.com/utility/optional.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_optional))*[P0220R1](https://wg21.link/P0220R1)[P0063R3](https://wg21.link/P0063R3)(partial)*

[and](https://en.cppreference.com/container/map/merge.html)`Maps`[(](https://en.cppreference.com/container/set/merge.html)`Sets`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_node_extract))*[P0083R3](https://wg21.link/P0083R3)[* functions of some](https://en.cppreference.com/container.html#Function_table)`emplace`[containers](https://en.cppreference.com/container.html)changed from void to reference[P0084R2](https://wg21.link/P0084R2)[std::variant](https://en.cppreference.com/utility/variant.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_variant))*[P0088R3](https://wg21.link/P0088R3)[std::make_from_tuple()](https://en.cppreference.com/utility/make_from_tuple.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_make_from_tuple))*[P0209R2](https://wg21.link/P0209R2)[std::has_unique_object_representations](https://en.cppreference.com/types/has_unique_object_representations.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_has_unique_object_representations))*[P0258R2](https://wg21.link/P0258R2)[std::gcd()](https://en.cppreference.com/numeric/gcd.html)and[std::lcm()](https://en.cppreference.com/numeric/lcm.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_gcd_lcm))*[P0295R0](https://wg21.link/P0295R0)[CWG issue 1776](https://cplusplus.github.io/CWG/issues/1776.html): Replacement of class objects containing reference members ([std::launder](https://en.cppreference.com/utility/launder.html)) ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_launder))*[P0137R1](https://wg21.link/P0137R1)[Extending memory management tools](https://en.cppreference.com/memory.html#Uninitialized_storage)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_raw_memory_algorithms))*[P0040R3](https://wg21.link/P0040R3)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_shared_ptr_weak_type))*[P0163R0](https://wg21.link/P0163R0)[Elementary string conversions](https://en.cppreference.com/utility.html#Elementary_string_conversions):[std::to_chars](https://en.cppreference.com/utility/to_chars.html)/[std::from_chars](https://en.cppreference.com/utility/from_chars.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_to_chars))*[P0067R5](https://wg21.link/P0067R5)11

14*

20*

19.24*

[std::shared_ptr](https://en.cppreference.com/memory/shared_ptr.html)and[std::weak_ptr](https://en.cppreference.com/memory/weak_ptr.html)with array support[P0414R2](https://wg21.link/P0414R2)[std::chrono::duration](https://en.cppreference.com/chrono/duration.html)and[std::chrono::time_point](https://en.cppreference.com/chrono/time_point.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_chrono))*[P0505R0](https://wg21.link/P0505R0)[std::shared_ptr](https://en.cppreference.com/memory/shared_ptr.html)<T[]> ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_shared_ptr_arrays))*[P0497R0](https://wg21.link/P0497R0)[std::char_traits](https://en.cppreference.com/string/char_traits.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_constexpr_string))*[P0426R1](https://wg21.link/P0426R1)[File system library](https://en.cppreference.com/filesystem.html)(std::filesystem) ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_filesystem))*[P0218R1](https://wg21.link/P0218R1)[P0219R1](https://wg21.link/P0219R1)[Hardware interference size](https://en.cppreference.com/thread/hardware_destructive_interference_size.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_hardware_interference_size))*[P0154R1](https://wg21.link/P0154R1)19

[(](https://en.cppreference.com/thread/scoped_lock.html)`std::scoped_lock`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_scoped_lock))*[P0156R2](https://wg21.link/P0156R2)[(](https://en.cppreference.com/types/is_aggregate.html)`std::is_aggregate`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_aggregate))*[LWG2911](https://wg21.link/LWG2911)[std::invoke_result](https://en.cppreference.com/types/result_of.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_invocable))*[P0604R0](https://wg21.link/P0604R0)`std::hash<std::filesystem::path>`[LWG3657](https://wg21.link/LWG3657)C++17 feature

Paper(s)

GCC libstdc++

Clang libc++

MSVC STL

Apple Clang*

IBM Open XL C/C++ for AIX*

Intel Parallel STL

Embarcadero C++ Builder*

##### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/17&action=edit§ion=T-3)] Notes

- As of 2020-11-20, the latest release of Oracle Developer Studio
[is 12.6](https://www.oracle.com/application-development/technologies/developerstudio-component-matrix.html). Its[documentation](https://docs.oracle.com/cd/E77782_01/html/E77789/bkaje.html)does not mention C++17. - Cray compiler may have support for some features earlier than 11.0. That version is when it became a derivative of Clang, gaining all of the attendant language feature support of the base compiler. See
[Cray/HPE document S-2179](https://support.hpe.com/hpesc/public/docDisplay?docLocale=en_US&docId=a00123566en_us).
