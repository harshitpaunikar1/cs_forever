Title: Concurrency support library (since C++11) - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/atomic.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:06:58+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# Concurrency support library (since C++11)

[cpp](https://en.cppreference.com/cpp.html)

C++ includes built-in support for threads, atomic operations, mutual exclusion, condition variables, and futures.

## Contents |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=1)] Threads

Threads enable programs to execute across several processor cores.

| Defined in header
| |
| (C++11) |
manages a separate thread (class) |
| (C++20) |
(class) |

##### Functions managing the current thread

`this_thread`

(function)

(function)

(function)

(function)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=2)] Cooperative cancellation (since C++20)

The components *stop source*, *stop token*, and *stop callback* can be used to asynchronously request that an operation stops execution in a timely manner, typically because the result is no longer required. Such a request is called a *stop request*.

These components specify the semantics of shared access to a *stop state*. Any object modeling any of these components that refer to the same stop state is an associated stop source, stop token, or stop callback, respectively.

|
The concepts stoppable-source
`stoppable_token` |
(since C++26) |

They are designed:

- to cooperatively cancel the execution such as for
[std::jthread](https://en.cppreference.com/thread/jthread.html), - to interrupt
[std::condition_variable_any](https://en.cppreference.com/thread/condition_variable_any.html)waiting functions,

- to perform stopped completion of an asynchronous operation created by execution::connect,
|
(since C++26) |

- or for a custom execution management implementation.

In fact, they do not even need to be used to "stop" anything, but can instead be used for a thread-safe one-time function(s) invocation trigger, for example.

| Defined in header
| |
## Stop token types | |
| (C++20) |
an interface for querying if a
(class) |

(class)

`std::inplace_stop_source`

object (class)

##### Stop source types

[std::jthread](https://en.cppreference.com/thread/jthread.html)s(class)

*stoppable-source*

that is the sole owner of the stop state (class)

##### Stop callback types

[std::jthread](https://en.cppreference.com/thread/jthread.html)cancellation(class template)

`std::inplace_stop_token`

(class template)

(alias template)

##### Concepts (since C++20)

(concept)

(concept)

(exposition-only concept*)

(exposition-only concept*)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=3)] Cache size access (since C++17)

| Defined in header
| |
| min offset to avoid false sharing max offset to promote true sharing (constant) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=4)] Atomic operations

These components are provided for fine-grained atomic operations allowing for lockless concurrent programming. Each atomic operation is indivisible with regards to any other atomic operation that involves the same object. Atomic objects are [free of data races](https://en.cppreference.com/language/memory_model.html#Threads_and_data_races).

| Defined in header
| |
## Atomic types | |
| (C++11) |
atomic class template and specializations for bool, integral, floating-point,(since C++20) and pointer types (class template) |
| (C++20) |
provides atomic operations on non-atomic objects (class template) |
## Operations on atomic types | |
| (C++11) |
checks if the atomic type's operations are lock-free (function template) |
| (C++11)(C++11) |
atomically replaces the value of the atomic object with a non-atomic argument (function template) |
| (C++11)(C++11) |
atomically obtains the value stored in an atomic object (function template) |
| (C++11)(C++11) |
atomically replaces the value of the atomic object with non-atomic argument and returns the old value of the atomic (function template) |
| atomically compares the value of the atomic object with non-atomic argument and performs atomic exchange if equal or atomic load if not (function template) | |
| (C++11)(C++11) |
adds a non-atomic value to an atomic object and obtains the previous value of the atomic (function template) |
| (C++11)(C++11) |
subtracts a non-atomic value from an atomic object and obtains the previous value of the atomic (function template) |
| (C++11)(C++11) |
replaces the atomic object with the result of bitwise AND with a non-atomic argument and obtains the previous value of the atomic (function template) |
| (C++11)(C++11) |
replaces the atomic object with the result of bitwise OR with a non-atomic argument and obtains the previous value of the atomic (function template) |
| (C++11)(C++11) |
replaces the atomic object with the result of bitwise XOR with a non-atomic argument and obtains the previous value of the atomic (function template) |
| (C++26)(C++26) |
replaces the atomic object with the result of
(function template) |

[std::min](https://en.cppreference.com/algorithm/min.html)with a non-atomic argument and obtains the previous value of the atomic(function template)

(function template)

(function template)

(function template)

##### Flag type and operations

(class)

(function)

(function)

(function)

(function)

(function)

(function)

##### Initialization

(function template)

(function macro)

[std::atomic_flag](https://en.cppreference.com/atomic/atomic_flag.html)to false(macro constant)

##### Memory synchronization ordering

(enum)

[std::memory_order_consume](https://en.cppreference.com/atomic/memory_order.html)dependency tree(function template)

(function)

(function)

[<stdatomic.h>](https://en.cppreference.com/header/stdatomic.h.html)

##### C compatibility macros (since C++23)

[std::atomic](https://en.cppreference.com/atomic/atomic.html)<T>(function macro)

Neither the `_Atomic`

macro, nor any of the non-macro global namespace declarations are provided by any C++ standard library header other than [ <stdatomic.h>](https://en.cppreference.com/header/stdatomic.h.html).

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=5)] Mutual exclusion

Mutual exclusion algorithms prevent multiple threads from simultaneously accessing shared resources. This prevents data races and provides support for synchronization between threads.

| Defined in header
| |
| (C++11) |
provides basic mutual exclusion facility (class) |
| (C++11) |
provides mutual exclusion facility which implements locking with a timeout (class) |
| (C++11) |
provides mutual exclusion facility which can be locked recursively by the same thread (class) |
| (C++11) |
provides mutual exclusion facility which can be locked recursively by the same thread and implements locking with a timeout (class) |
| Defined in header
| |
| (C++17) |
provides shared mutual exclusion facility (class) |
| (C++14) |
provides shared mutual exclusion facility and implements locking with a timeout (class) |
## Generic mutex management | |
| Defined in header
| |
| (C++11) |
implements a strictly scope-based mutex ownership wrapper (class template) |
| (C++17) |
deadlock-avoiding RAII wrapper for multiple mutexes (class template) |
| (C++11) |
implements movable mutex ownership wrapper (class template) |
| (C++14) |
implements movable shared mutex ownership wrapper (class template) |
| tags used to specify locking strategy (tag) | |
## Generic locking algorithms | |
| (C++11) |
attempts to obtain ownership of mutexes via repeated calls to `try_lock` (function template) |
| (C++11) |
locks specified mutexes, blocks if any are unavailable (function template) |
## Call once | |
| (C++11) |
helper object to ensure that
call_once |

(class)

(function template)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=6)] Condition variables

A condition variable is a synchronization primitive that allows multiple threads to communicate with each other. It allows some number of threads to wait (possibly with a timeout) for notification from another thread that they may proceed. A condition variable is always associated with a mutex.

| Defined in header
| |
| (C++11) |
provides a condition variable associated with a
(class) |

(class)

`notify_all`

to be invoked when this thread is completely finished (function)

(enum)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=7)] Semaphores (since C++20)

A semaphore is a lightweight synchronization primitive used to constrain concurrent access to a shared resource. When either would suffice, a semaphore can be more efficient than a condition variable.

| Defined in header
| |
| (C++20) |
semaphore that models a non-negative resource count (class template) |
| (C++20) |
semaphore that has only two states (typedef) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=8)] Latches and Barriers (since C++20)

Latches and barriers are thread coordination mechanisms that allow any number of threads to block until an expected number of threads arrive. A latch cannot be reused, while a barrier can be used repeatedly.

| Defined in header
| |
| (C++20) |
single-use thread barrier (class) |
| Defined in header
| |
| (C++20) |
reusable thread barrier (class template) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=9)] Futures

The standard library provides facilities to obtain values that are returned and to catch exceptions that are thrown by asynchronous tasks (i.e. functions launched in separate threads). These values are communicated in a *shared state*, in which the asynchronous task may write its return value or store an exception, and which may be examined, waited for, and otherwise manipulated by other threads that hold instances of [std::future](https://en.cppreference.com/thread/future.html) or [std::shared_future](https://en.cppreference.com/thread/shared_future.html) that reference that shared state.

| Defined in header
| |
| (C++11) |
stores a value for asynchronous retrieval (class template) |
| (C++11) |
packages a function to store its return value for asynchronous retrieval (class template) |
| (C++11) |
waits for a value that is set asynchronously (class template) |
| (C++11) |
waits for a value (possibly referenced by other futures) that is set asynchronously (class template) |
| (C++11) |
runs a function asynchronously (potentially in a new thread) and returns a
(function template) |

[std::async](https://en.cppreference.com/thread/async.html)(enum)

[std::future](https://en.cppreference.com/thread/future.html)and[std::shared_future](https://en.cppreference.com/thread/shared_future.html)(enum)

##### Future errors

(class)

(function)

(enum)

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=10)] Safe reclamation (since C++26)

Safe-reclamation techniques are most frequently used to straightforwardly resolve access-deletion races.

## Read-Copy-Update mechanism | |
| Defined in header
| |
| (C++26) |
allows an object to be protected by RCU (class template) |
| (C++26) |
provides regions of RCU protection (class) |
| (C++26) |
returns a reference to a static-duration object of type `std::rcu_domain` (function) |
| (C++26) |
blocks until a protection region unlocks on a RCU domain (function) |
| (C++26) |
may evaluate scheduled operations on a RCU domain and blocks until all preceding evaluations are complete (function) |
| (C++26) |
schedules the evaluation of a specified function on a RCU domain, potentially allocating memory, and invoking scheduled evaluations (function template) |
## Hazard pointers | |
| Defined in header
| |
| (C++26) |
allows an object to be hazard-protectable (class template) |
| (C++26) |
single-writer multi-reader pointer that can be owned by at most one thread at any point of time (class) |
| (C++26) |
constructs a hazard pointer (function) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/thread&action=edit§ion=11)] See also

|
|
