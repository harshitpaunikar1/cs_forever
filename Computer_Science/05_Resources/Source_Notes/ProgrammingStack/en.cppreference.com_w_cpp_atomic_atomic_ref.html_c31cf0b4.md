Title: std::atomic_ref - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/atomic/atomic_ref.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:07:03+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# std::atomic_ref

| Defined in header
|
||
| template< class T > struct atomic_ref; |
(since C++20) | |

The `std::atomic_ref`

class template applies atomic operations to the object it references.

For the lifetime of the `std::atomic_ref`

object, the object it references is considered an atomic object. If one thread writes to an atomic object while another thread reads from it, the behavior is well-defined (see [memory model](https://en.cppreference.com/language/memory_model.html) for details on data races). In addition, accesses to atomic objects may establish inter-thread synchronization and order non-atomic memory accesses as specified by [std::memory_order](https://en.cppreference.com/memory_order.html).

The lifetime of an object must exceed the lifetime of all `std::atomic_ref`

s that references the object. While any `std::atomic_ref`

instance referencing an object exists, the object must be exclusively accessed through these `std::atomic_ref`

instances. No subobject of an object referenced by an `std::atomic_ref`

object may be concurrently referenced by any other `std::atomic_ref`

object.

Atomic operations applied to an object through an `std::atomic_ref`

are atomic with respect to atomic operations applied through any other `std::atomic_ref`

referencing the same object.

Like [references](https://en.cppreference.com/language/reference.html) in the core language, constness is shallow for `std::atomic_ref`

- it is possible to modify the referenced value through a const `std::atomic_ref`

object.

If any of the following conditions are satisfied, the program is ill-formed:

-
[std::is_trivially_copyable_v](https://en.cppreference.com/types/is_trivially_copyable.html)<T> is false. -
is false and`is_always_lock_free`

[std::is_volatile_v](https://en.cppreference.com/types/is_volatile.html)<T> is true.

`std::atomic_ref`

is [CopyConstructible](https://en.cppreference.com/named_req/CopyConstructible.html).

## Contents |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_ref&action=edit§ion=1)] Nested types

| Type | Definition |
`value_type`
|
|

`difference_type`

-
`value_type`

, if`T`

is an arithmetic type other than*cv*bool. - Otherwise,
[std::ptrdiff_t](https://en.cppreference.com/types/ptrdiff_t.html), if`T`

is a pointer-to-object type. - Otherwise, not defined.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_ref&action=edit§ion=2)] Data members

| Member | Description |
T*
|
the pointer to the referenced object (exposition-only member object*) |
| [static] |
indicates that the type is always lock-free (public static member constant) |
| [static] |
indicates the required alignment of an object to be referenced by `atomic_ref` (public static member constant) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_ref&action=edit§ion=3)] Member functions

constructs an `atomic_ref` object (public member function) | |
stores a value into the object referenced by an `atomic_ref` object (public member function) | |
checks if the `atomic_ref` object is lock-free (public member function) | |
| atomically replaces the value of the referenced object with a non-atomic argument (public member function) | |
| atomically obtains the value of the referenced object (public member function) | |
| loads a value from the referenced object (public member function) | |
| atomically replaces the value of the referenced object and obtains the value held previously (public member function) | |
| atomically compares the value of the referenced object with non-atomic argument and performs atomic exchange if equal or atomic load if not (public member function) | |
| blocks the thread until notified and the atomic value changes (public member function) | |
| notifies at least one thread waiting on the atomic object (public member function) | |
| notifies all threads blocked waiting on the atomic object (public member function) | |
| (C++26) |
returns the object's address (public member function) |
## Provided only when
| |
| atomically adds the argument to the value stored in the referenced object and obtains the value held previously (public member function) | |
| atomically subtracts the argument from the value stored in the referenced object and obtains the value held previously (public member function) | |
| atomically adds to or subtracts from the referenced value (public member function) | |
## Provided only when
| |
| (C++26) |
atomically performs
(public member function) |

[std::min](https://en.cppreference.com/algorithm/min.html)between the argument and the value of the referenced object and obtains the value held previously(public member function)

(public member function)

##### Provided only when `T`

is an integral type other than *cv* bool

(public member function)

(public member function)

(public member function)

(public member function)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_ref&action=edit§ion=4)] Specializations

The standard specifies that `std::atomic_ref`

has following specializations:

| template<> struct atomic_ref</*integral-type*/>; |
(1) | (since C++20) |
| template<> struct atomic_ref</*floating-point-type*/>; |
(2) | (since C++20) |
| template< class /*pointer-type*/ > requires /* see below */ |
(3) | (since C++20) |

*cv*bool.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_ref&action=edit§ion=5)] Notes

Implementations may merge the specified specializations. E.g. MSVC STL merges all of them into the primary template.

When `T`

is *cv* void or a function type, std::atomic_ref<T*> (i.e. std::atomic_ref<void*>, std::atomic_ref<int(*)()> etc.) does not have `difference_type`

or any operation requiring pointer arithmetic or relational comparison(since C++26).

|
|---|

`__cpp_lib_atomic_ref`

`201806L`

`std::atomic_ref`

`__cpp_lib_constexpr_atomic`

`202411L`

[std::atomic](https://en.cppreference.com/atomic.html)and`std::atomic_ref`

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_ref&action=edit§ion=6)] Defect reports

| DR | Applied to | Behavior as published | Correct behavior |
|---|---|---|---|
(
|

if

`T`

is a const type or pointer-to-non-object type
or not provided for unsuitable

`T`

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_ref&action=edit§ion=7)] See also

| (C++11) |
atomic class template and specializations for bool, integral, floating-point,(since C++20) and pointer types (class template) |
