Title: std::atomic - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/atomic/atomic.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:07:00+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# std::atomic

| Defined in header
|
||
| template< class T > struct atomic; |
(1) | (since C++11) |
| template< class U > struct atomic<U*>; |
(2) | (since C++11) |
| Defined in header
|
||
| template< class U > struct atomic<
|
(3) | (since C++20) |
| template< class U > struct atomic<
|
(4) | (since C++20) |
| Defined in header
|
||
| #define _Atomic(T) /* see below */ |
(5) | (since C++23) |

Each instantiation and full specialization of the `std::atomic`

template defines an atomic type. If one thread writes to an atomic object while another thread reads from it, the behavior is well-defined (see [memory model](https://en.cppreference.com/language/memory_model.html) for details on data races).

In addition, accesses to atomic objects may establish inter-thread synchronization and order non-atomic memory accesses as specified by [std::memory_order](https://en.cppreference.com/memory_order.html).

`std::atomic`

is neither copyable nor movable.

|
The compatibility macro `_Atomic(T)` is identical to `std::atomic<T>` while both are well-formed.
It is unspecified whether any declaration in namespace |
(since C++23) |

## Contents |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=1)] Specializations

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=2)] Primary template

The primary `std::atomic`

template may be instantiated with any [TriviallyCopyable](https://en.cppreference.com/named_req/TriviallyCopyable.html) type `T`

satisfying both [CopyConstructible](https://en.cppreference.com/named_req/CopyConstructible.html) and [CopyAssignable](https://en.cppreference.com/named_req/CopyAssignable.html). The program is ill-formed if any of following values is false:

-
[std::is_trivially_copyable](https://en.cppreference.com/types/is_trivially_copyable.html)<T>::value -
[std::is_copy_constructible](https://en.cppreference.com/types/is_copy_constructible.html)<T>::value -
[std::is_move_constructible](https://en.cppreference.com/types/is_move_constructible.html)<T>::value -
[std::is_copy_assignable](https://en.cppreference.com/types/is_copy_assignable.html)<T>::value -
[std::is_move_assignable](https://en.cppreference.com/types/is_move_assignable.html)<T>::value -
[std::is_same](https://en.cppreference.com/types/is_same.html)<T, typename[std::remove_cv](https://en.cppreference.com/types/remove_cv.html)<T>::type>::value

struct Counters { int a; int b; }; // user-defined trivially-copyable type std::atomic<Counters> cnt; // specialization for the user-defined type

std::atomic<bool> uses the primary template. It is guaranteed to be a [standard layout struct](https://en.cppreference.com/language/classes.html#Standard-layout_class) and has a [trivial destructor](https://en.cppreference.com/language/destructor.html#Trivial_destructor).

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=3)] Partial specializations

The standard library provides partial specializations of the `std::atomic`

template for the following types with additional properties that the primary template does not have:

`std::atomic<U*>`

for all pointer types. These specializations have standard layout, trivial default constructors,(until C++20) and trivial destructors. Besides the operations provided for all atomic types, these specializations additionally support atomic arithmetic operations appropriate to pointer types, such as [,](https://en.cppreference.com/atomic/fetch_add.html)

`fetch_add`

[.](https://en.cppreference.com/atomic/fetch_sub.html)

`fetch_sub`

|
3,4) Partial specializations std::atomic<
See
std::atomic<std::weak_ptr> |
(since C++20) |

#### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=4)] Specializations for integral types

When instantiated with one of the following integral types, `std::atomic`

provides additional atomic operations appropriate to integral types such as [ fetch_add](https://en.cppreference.com/atomic/fetch_add.html),

[,](https://en.cppreference.com/atomic/fetch_sub.html)

`fetch_sub`

[,](https://en.cppreference.com/atomic/fetch_and.html)

`fetch_and`

[,](https://en.cppreference.com/atomic/fetch_or.html)

`fetch_or`

[:](https://en.cppreference.com/atomic/fetch_xor.html)

`fetch_xor`

- The character types char, char8_t(since C++20), char16_t, char32_t, and wchar_t;
- The standard signed integer types: signed char, short, int, long, and long long;
- The standard unsigned integer types: unsigned char, unsigned short, unsigned int, unsigned long, and unsigned long long;
- Any additional integral types needed by the typedefs in the header
.`<cstdint>`

Additionally, the resulting `std::atomic<`

specialization has standard layout, a trivial default constructor,(until C++20) and a trivial destructor. Signed integer arithmetic is defined to use two's complement; there are no undefined results.
*Integral*>

## Specializations for floating-point typesWhen instantiated with one of the cv-unqualified floating-point types (float, double, long double and cv-unqualified
`fetch_sub` |
(since C++20) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=6)] Member types

| Type | Definition | ||||
`value_type`
|
`T` (regardless of whether specialized or not)
| ||||
`difference_type`
|
|

[â](https://en.cppreference.com/atomic.html#cite_ref-1)`difference_type`

is not defined in the primary`std::atomic`

template or in the partial specializations for[std::shared_ptr](https://en.cppreference.com/memory/shared_ptr.html)and[std::weak_ptr](https://en.cppreference.com/memory/weak_ptr.html).

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=7)] Member functions

| constructs an atomic object (public member function) | |
| stores a value into an atomic object (public member function) | |
| checks if the atomic object is lock-free (public member function) | |
| atomically replaces the value of the atomic object with a non-atomic argument (public member function) | |
| atomically obtains the value of the atomic object (public member function) | |
| loads a value from an atomic object (public member function) | |
| atomically replaces the value of the atomic object and obtains the value held previously (public member function) | |
| atomically compares the value of the atomic object with non-atomic argument and performs atomic exchange if equal or atomic load if not (public member function) | |
| (C++20) |
blocks the thread until notified and the atomic value changes (public member function) |
| (C++20) |
notifies at least one thread waiting on the atomic object (public member function) |
| (C++20) |
notifies all threads blocked waiting on the atomic object (public member function) |
## Constants | |
| [static] (C++17) |
indicates that the type is always lock-free (public static member constant) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=8)] Specialized member functions

## Specialized for integral, floating-point(since C++20) and pointer types | |
| atomically adds the argument to the value stored in the atomic object and obtains the value held previously (public member function) | |
| atomically subtracts the argument from the value stored in the atomic object and obtains the value held previously (public member function) | |
| adds to or subtracts from the atomic value (public member function) | |
## Specialized for integral and pointer types only | |
| (C++26) |
atomically performs
(public member function) |

[std::min](https://en.cppreference.com/algorithm/min.html)between the argument and the value of the atomic object and obtains the value held previously(public member function)

(public member function)

##### Specialized for integral types only

(public member function)

(public member function)

(public member function)

(public member function)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=9)] Type aliases

Type aliases are provided for bool and all integral types listed above, as follows:

## Aliases for all
| |
atomic_bool(C++11) |
std::atomic<bool> (typedef) |
atomic_char(C++11) |
std::atomic<char> (typedef) |
atomic_schar(C++11) |
std::atomic<signed char> (typedef) |
atomic_uchar(C++11) |
std::atomic<unsigned char> (typedef) |
atomic_short(C++11) |
std::atomic<short> (typedef) |
atomic_ushort(C++11) |
std::atomic<unsigned short> (typedef) |
atomic_int(C++11) |
std::atomic<int> (typedef) |
atomic_uint(C++11) |
std::atomic<unsigned int> (typedef) |
atomic_long(C++11) |
std::atomic<long> (typedef) |
atomic_ulong(C++11) |
std::atomic<unsigned long> (typedef) |
atomic_llong(C++11) |
std::atomic<long long> (typedef) |
atomic_ullong(C++11) |
std::atomic<unsigned long long> (typedef) |
atomic_char8_t(C++20) |
std::atomic<char8_t> (typedef) |
atomic_char16_t(C++11) |
std::atomic<char16_t> (typedef) |
atomic_char32_t(C++11) |
std::atomic<char32_t> (typedef) |
atomic_wchar_t(C++11) |
std::atomic<wchar_t> (typedef) |
atomic_int8_t(C++11)(optional) |
std::atomic<
(typedef) |

**atomic_uint8_t**

[std::uint8_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int16_t**

[std::int16_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint16_t**

[std::uint16_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int32_t**

[std::int32_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint32_t**

[std::uint32_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int64_t**

[std::int64_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint64_t**

[std::uint64_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int_least8_t**

[std::int_least8_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint_least8_t**

[std::uint_least8_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int_least16_t**

[std::int_least16_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint_least16_t**

[std::uint_least16_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int_least32_t**

[std::int_least32_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint_least32_t**

[std::uint_least32_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int_least64_t**

[std::int_least64_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint_least64_t**

[std::uint_least64_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int_fast8_t**

[std::int_fast8_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint_fast8_t**

[std::uint_fast8_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int_fast16_t**

[std::int_fast16_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint_fast16_t**

[std::uint_fast16_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int_fast32_t**

[std::int_fast32_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint_fast32_t**

[std::uint_fast32_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_int_fast64_t**

[std::int_fast64_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uint_fast64_t**

[std::uint_fast64_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_intptr_t**

[std::intptr_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uintptr_t**

[std::uintptr_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_size_t**

[std::size_t](https://en.cppreference.com/types/size_t.html)>(typedef)

**atomic_ptrdiff_t**

[std::ptrdiff_t](https://en.cppreference.com/types/ptrdiff_t.html)>(typedef)

**atomic_intmax_t**

[std::intmax_t](https://en.cppreference.com/types/integer.html)>(typedef)

**atomic_uintmax_t**

[std::uintmax_t](https://en.cppreference.com/types/integer.html)>(typedef)

##### Aliases for special-purpose types

**atomic_signed_lock_free**

(typedef)

**atomic_unsigned_lock_free**

(typedef)

`std::atomic_int`*N*_t

, `std::atomic_uint`*N*_t

, `std::atomic_intptr_t`

, and `std::atomic_uintptr_t`

are defined if and only if `std::int`*N*_t

, `std::uint`*N*_t

, [std::intptr_t](https://en.cppreference.com/types/integer.html), and

[std::uintptr_t](https://en.cppreference.com/types/integer.html)are defined, respectively.

|
|
(since C++20) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=10)] Notes

There are non-member function template equivalents for all member functions of `std::atomic`

. Those non-member functions may be additionally overloaded for types that are not specializations of `std::atomic`

, but are able to guarantee atomicity. The only such type in the standard library is [std::shared_ptr](https://en.cppreference.com/memory/shared_ptr.html)<U>.

`_Atomic`

is a [keyword](https://en.cppreference.com/c/keyword/_Atomic.html) and used to provide [atomic types](https://en.cppreference.com/c/language/atomic.html) in C.

Implementations are recommended to ensure that the representation of `_Atomic(T)`

in C is same as that of `std::atomic<T>`

in C++ for every possible type `T`

. The mechanisms used to ensure atomicity and memory ordering should be compatible.

On GCC and Clang, some of the functionality described here requires linking against `-latomic`

.

|
|---|

`__cpp_lib_atomic_ref`

`201806L`

`std::atomic_ref`

`__cpp_lib_constexpr_atomic`

`202411L`

`std::atomic`

and std::atomic_ref
### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=11)] Example

#include <atomic> #include <iostream> #include <thread> #include <vector> std::atomic_int acnt; int cnt; void f() { for (auto n{10000}; n; --n) { ++acnt; ++cnt; // Note: for this example, relaxed memory order is sufficient, // e.g. acnt.fetch_add(1, std::memory_order_relaxed); } } int main() { {[std::vector]<[std::jthread]> pool; for (int n = 0; n < 10; ++n) pool.emplace_back(f); }[std::cout]<< "The atomic counter is " << acnt << '\n' << "The non-atomic counter is " << cnt << '\n'; }

Possible output:

The atomic counter is 100000 The non-atomic counter is 69696

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=12)] Defect reports

The following behavior-changing defect reports were applied retroactively to previously published C++ standards.

| DR | Applied to | Behavior as published | Correct behavior |
|---|---|---|---|
|

[fixed width integer types](https://en.cppreference.com/types/integer.html)were missing[LWG 3012](https://cplusplus.github.io/LWG/issue3012)`std::atomic<T>`

was permitted for any `T`

that is trivially copyable but not copyable

[LWG 3949](https://cplusplus.github.io/LWG/issue3949)trivial destructor was accidently dropped in C++17

[LWG 4069](https://cplusplus.github.io/LWG/issue4069)(

[P3323R1](https://wg21.link/P3323R1))`T`

was questionable
`T`

being cv-qualified
[P0558R1](https://wg21.link/P0558R1)functions for atomic types might accidently

fail; invalid pointer operations were provided

member typedefs

`value_type`

and

`difference_type`

are added
### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic&action=edit§ion=13)] See also

| (C++11) |
the lock-free boolean atomic type (class) |
| (C++20) |
atomic shared pointer (class template specialization) |
| (C++20) |
atomic weak pointer (class template specialization) |
|
|
