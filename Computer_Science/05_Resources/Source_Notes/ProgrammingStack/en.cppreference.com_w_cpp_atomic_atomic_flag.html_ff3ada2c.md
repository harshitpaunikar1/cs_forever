Title: std::atomic_flag - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/atomic/atomic_flag.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:07:01+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# std::atomic_flag

From cppreference.com

| Defined in header
|
||
| class atomic_flag; |
(since C++11) | |

`std::atomic_flag`

is an atomic boolean type. Unlike all specializations of [std::atomic](https://en.cppreference.com/atomic.html), it is guaranteed to be lock-free. Unlike [std::atomic](https://en.cppreference.com/atomic.html)<bool>, `std::atomic_flag`

does not provide load or store operations.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_flag&action=edit§ion=1)] Member functions

| constructs an atomic_flag (public member function) | |
| [deleted] |
the assignment operator (deleted) (public member function) |
| atomically sets flag to false (public member function) | |
| atomically sets the flag to true and obtains its previous value (public member function) | |
| (C++20) |
atomically returns the value of the flag (public member function) |
| (C++20) |
blocks the thread until notified and the atomic value changes (public member function) |
| (C++20) |
notifies at least one thread waiting on the atomic object (public member function) |
| (C++20) |
notifies all threads blocked waiting on the atomic object (public member function) |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_flag&action=edit§ion=2)] Example

A [spinlock](https://en.wikipedia.org/wiki/Spinlock) mutex demo can be implemented in userspace using an atomic_flag. Do note that spinlock mutexes are [extremely dubious](https://www.realworldtech.com/forum/?threadid=189711&curpostid=189723) in practice.

Run this code

#include <atomic> #include <iostream> #include <mutex> #include <thread> #include <vector> class mutex { std::atomic_flag m_{}; public: void lock() noexcept { while (m_.test_and_set([std::memory_order_acquire])) #if defined(__cpp_lib_atomic_wait) && __cpp_lib_atomic_wait >= 201907L // Since C++20, locks can be acquired only after notification in the unlock, // avoiding any unnecessary spinning. // Note that even though wait guarantees it returns only after the value has // changed, the lock is acquired after the next condition check. m_.wait(true,[std::memory_order_relaxed]) #endif ; } bool try_lock() noexcept { return !m_.test_and_set([std::memory_order_acquire]); } void unlock() noexcept { m_.clear([std::memory_order_release]); #if defined(__cpp_lib_atomic_wait) && __cpp_lib_atomic_wait >= 201907L m_.notify_one(); #endif } }; static mutex m; static int out{}; void f([std::size_t]n) { for ([std::size_t]cnt{}; cnt < 40; ++cnt) {[std::lock_guard]lock{m};[std::cout]<< n << ((++out % 40) == 0 ? '\n' : ' '); } } int main() {[std::vector]<[std::thread]> v; for ([std::size_t]n{}; n < 10; ++n) v.emplace_back(f, n); for (auto &t : v) t.join(); }

Possible output:

0 1 1 2 0 1 3 2 3 2 0 1 2 3 2 3 0 1 3 2 0 1 2 3 2 3 0 3 2 3 2 3 2 3 1 2 3 0 1 3 2 3 2 0 1 2 3 0 1 2 3 2 0 1 2 3 0 1 2 3 2 3 2 3 2 0 1 2 3 2 3 0 1 3 2 3 0 2 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 0 3 2 0 2 3 2 3 2 3 2 3 2 3 0 3 2 3 0 3 0 3 2 3 0 3 2 3 2 3 0 2 3 0 3 2 0 2 2 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 6 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 7 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/atomic/atomic_flag&action=edit§ion=3)] See also

| atomically sets the flag to true and returns its previous value (function) | |
| (C++11)(C++11) |
atomically sets the value of the flag to false (function) |
| (C++20)(C++20) |
blocks the thread until notified and the flag changes (function) |
| (C++20) |
notifies a thread blocked in atomic_flag_wait (function) |
| (C++20) |
notifies all threads blocked in atomic_flag_wait (function) |
| (C++11) |
initializes an std::atomic_flag to false (macro constant) |
|
|
