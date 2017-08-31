# cxxpool

Version: 2.0.0

cxxpool is a header-only thread pool for C++. It enables you to schedule independent
tasks with or without specifying task priorities. Pushing a task into the thread
pool returns a future associated to the underlying execution. 

cxxpool is designed for ease of use, portability, and scalability. It is written in 
C++11 and only depends on the standard library. Just copy `src/cxxpool.h` 
to your project and off you go! Tested with GCC, Clang, and Visual Studio.

## Example

This example creates a thread pool with 4 threads and pushes
three simple tasks into the pool.

```cpp
#include <iostream>
#include "cxxpool.h"

int sum(int x, int y) {
    return x + y;
}

int main() {
    cxxpool::thread_pool pool{4};

    // pushing tasks and retrieving futures
    auto future1 = pool.push([]{ return 42; });
    auto future2 = pool.push([](double x){ return x; }, 13.);
    auto future3 = pool.push(sum, 6, 7);

    // output: results = 42, 13, 13
    std::cout << "results = " << future1.get() << ", ";
    std::cout << future2.get() << ", " << future3.get() << std::endl;
}
```

## Running the tests

You'll need:
* [libunittest](http://libunittest.sourceforge.net/)
* [cppcheck](http://cppcheck.sourceforge.net/) 
* [valgrind](http://valgrind.org/) 

If you're on Mac or Linux, just do:
```
./make_check.sh [compiler]
```
where compiler defaults to `g++` and can also be `clang++`.

If you're using Visual Studio you will have to set up a project
manually to run all tests.


## Feedback

Contact me if you have any questions or suggestions to make this a better library!
Email me at `chr.blume@gmail.com` or create a GitHub issue.
