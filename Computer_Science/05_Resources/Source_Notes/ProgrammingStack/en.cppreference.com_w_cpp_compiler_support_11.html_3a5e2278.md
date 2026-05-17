Title: Compiler support for C++11 - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/compiler_support/11.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:07:11+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# Compiler support for C++11

From cppreference.com

<

[cpp](https://en.cppreference.com/cpp.html) |[compiler support](https://en.cppreference.com/compiler_support.html)

DR*nn* - the number *nn* after "DR" denotes target C++ revision the Defect Report is applied to, e.g., DR20 → C++20.

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

HP aCC

Digital Mars C++

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

GCC libstdc++

Clang libc++

MSVC STL

Apple Clang*

IBM Open XL C/C++ for AIX*

Sun/Oracle C++*

Embarcadero C++ Builder*
