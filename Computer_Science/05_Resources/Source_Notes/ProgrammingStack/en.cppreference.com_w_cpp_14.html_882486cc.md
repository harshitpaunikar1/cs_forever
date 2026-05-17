Title: C++14 - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/14.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:06:44+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# C++14

From cppreference.com

<

[cpp](https://en.cppreference.com/cpp.html)C++14 is a minor version after the major version C++11, featuring mainly minor improvements and defect fixes. Its approval was announced on August 18, 2014. It was released on December 15, 2014.

Before its approval, C++1y is sometimes used to indicate its release in 2010s.

| This section is incomplete |

## Contents |

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/14&action=edit§ion=1)] New language features

-
[variable templates](https://en.cppreference.com/language/variable_template.html) -
[generic lambdas](https://en.cppreference.com/language/lambda.html) - lambda init-capture
- new/delete elision
-
[relaxed restrictions on constexpr functions](https://en.cppreference.com/language/constexpr.html) -
[binary literals](https://en.cppreference.com/language/integer_literal.html) -
[digit separators](https://en.cppreference.com/language/integer_literal.html#Single_quote) -
[return type deduction for functions](https://en.cppreference.com/language/function.html#Return_type_deduction_.28since_C.2B.2B14.29) -
[aggregate classes](https://en.cppreference.com/language/aggregate_initialization.html)with default non-static member initializers.

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/14&action=edit§ion=2)] New library features

-
[std::make_unique](https://en.cppreference.com/memory/unique_ptr/make_unique.html) -
[std::shared_timed_mutex](https://en.cppreference.com/thread/shared_timed_mutex.html)and[std::shared_lock](https://en.cppreference.com/thread/shared_lock.html) -
[std::integer_sequence](https://en.cppreference.com/utility/integer_sequence.html) -
[std::exchange](https://en.cppreference.com/utility/exchange.html) -
[std::quoted](https://en.cppreference.com/io/manip/quoted.html) - and many small improvements to existing library facilities, such as
- two-range overloads for some algorithms
- type alias versions of type traits
- user-defined literals for
,`basic_string`and`duration``complex` - etc.

| This section is incomplete |

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/14&action=edit§ion=3)] Defect reports

## [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/14&action=edit§ion=4)] Compiler support

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/14&action=edit§ion=T-1)] C++14 core language features

| C++14 feature |
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
|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Tweaked wording for
|

[N3323](https://wg21.link/N3323)[Binary literals](https://en.cppreference.com/language/integer_literal.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_binary_literals))*[N3472](https://wg21.link/N3472)4.9

[, Return type deduction for normal functions (](https://en.cppreference.com/language/auto.html)`decltype(auto)`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_decltype_auto))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_return_type_deduction))*[N3638](https://wg21.link/N3638)4.9

3.4

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_init_captures))*[N3648](https://wg21.link/N3648)4.9

[Generic lambda expressions](https://en.cppreference.com/language/lambda.html#Explanation)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_generic_lambdas))*[N3649](https://wg21.link/N3649)[Variable templates](https://en.cppreference.com/language/variable_template.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_variable_templates))*[N3651](https://wg21.link/N3651)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_constexpr))*[N3652](https://wg21.link/N3652)[default member initializers](https://en.cppreference.com/language/data_members.html#Member_initialization)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_aggregate_nsdmi))*[N3653](https://wg21.link/N3653)[memory allocations](https://en.cppreference.com/language/new.html#Allocation)[N3664](https://wg21.link/N3664)`[[`[deprecated](https://en.cppreference.com/language/attributes/deprecated.html)]]

attribute
[N3760](https://wg21.link/N3760)16.0

[Sized deallocation](https://en.cppreference.com/language/delete.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_sized_deallocation))*[N3778](https://wg21.link/N3778)[Single quote](https://en.cppreference.com/language/integer_literal.html#Single_quote)as digit separator[N3781](https://wg21.link/N3781)C++14 feature

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

IBM Open XL C++ for z/OS

IBM XL C++

Sun/Oracle C++

### [[edit](https://en.cppreference.com/mwiki/index.php?title=Template:cpp/compiler_support/14&action=edit§ion=T-2)] C++14 library features

| C++14 feature |
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
| constexpr for
<complex> |

[N3302](https://wg21.link/N3302)[operator function objects](https://en.cppreference.com/functional.html#Operator_function_objects)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_transparent_operators))*[N3421](https://wg21.link/N3421)[std::result_of](https://en.cppreference.com/types/result_of.html)and[SFINAE](https://en.cppreference.com/language/sfinae.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_result_of_sfinae))*[N3462](https://wg21.link/N3462)`<chrono>`[N3469](https://wg21.link/N3469)`<array>`[N3470](https://wg21.link/N3470)[,](https://en.cppreference.com/header/initializer_list.html)`<initializer_list>`[and](https://en.cppreference.com/header/utility.html)`<utility>``<tuple>`[N3471](https://wg21.link/N3471)[std::integral_constant](https://en.cppreference.com/types/integral_constant.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_integral_constant_callable))*[N3545](https://wg21.link/N3545)[User-defined literals](https://en.cppreference.com/language/user_literal.html#Standard_library)for[and](https://en.cppreference.com/header/chrono.html)`<chrono>`[(](https://en.cppreference.com/header/string.html)`<string>`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_chrono_udls))* ([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_string_udls))*[N3642](https://wg21.link/N3642)[Null forward iterators](https://en.cppreference.com/named_req/ForwardIterator.html#Singular_iterators)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_null_iterators))*[N3644](https://wg21.link/N3644)10

[std::quoted](https://en.cppreference.com/io/manip/quoted.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_quoted_string_io))*[N3654](https://wg21.link/N3654)[std::make_unique](https://en.cppreference.com/memory/unique_ptr/make_unique.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_make_unique))*[N3656](https://wg21.link/N3656)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_generic_associative_lookup))*[N3657](https://wg21.link/N3657)[std::integer_sequence](https://en.cppreference.com/utility/integer_sequence.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_integer_sequence))*[N3658](https://wg21.link/N3658)[std::shared_timed_mutex](https://en.cppreference.com/thread/shared_timed_mutex.html)[N3659](https://wg21.link/N3659)[std::exchange](https://en.cppreference.com/utility/exchange.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_exchange_function))*[N3668](https://wg21.link/N3668)[N3669](https://wg21.link/N3669)[(](https://en.cppreference.com/utility/pair/get.html)`std::get<T>()`[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_tuples_by_type))*[N3670](https://wg21.link/N3670)[std::equal](https://en.cppreference.com/algorithm/equal.html),[std::is_permutation](https://en.cppreference.com/algorithm/is_permutation.html),[std::mismatch](https://en.cppreference.com/algorithm/mismatch.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_robust_nonmodifying_seq_ops))*[N3671](https://wg21.link/N3671)[transformation traits](https://en.cppreference.com/meta.html#Type_transformations)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_transformation_trait_aliases))*[N3655](https://wg21.link/N3655)[User-defined Literals for](https://en.cppreference.com/numeric/complex/operator%2522%2522i.html)(`std::complex`

[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_complex_udls))*[N3779](https://wg21.link/N3779)[std::is_null_pointer](https://en.cppreference.com/types/is_null_pointer.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_null_pointer))*[LWG2247](https://wg21.link/LWG2247)[std::is_final](https://en.cppreference.com/types/is_final.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_is_final))*[LWG2112](https://wg21.link/LWG2112)[std::make_reverse_iterator](https://en.cppreference.com/iterator/make_reverse_iterator.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_make_reverse_iterator))*[LWG2285](https://wg21.link/LWG2285)[std::shared_timed_mutex](https://en.cppreference.com/thread/shared_timed_mutex.html)([FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_shared_timed_mutex))*[N3891](https://wg21.link/N3891)[FTM](https://en.cppreference.com/experimental/feature_test.html#cpp_lib_tuple_element_t))*[N3887](https://wg21.link/N3887)C++14 feature

Paper(s)

GCC libstdc++

Clang libc++

MSVC STL

Apple Clang*

IBM Open XL C/C++ for AIX*

Sun/Oracle C++*

Embarcadero C++ Builder*

* - hover over a cell marked with the star * to see additional pop-up notes.

DR*nn* - the number *nn* after "DR" denotes target C++ revision the Defect Report is applied to, e.g., DR20 → C++20.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/14&action=edit§ion=5)] External links

| 1. |
|
