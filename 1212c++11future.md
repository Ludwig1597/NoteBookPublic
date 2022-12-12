> 2022.12.9

  

# C++11 std::future

  

## 什么是std::future

  

In C++,`std::future` is a type that represents a value that may be available in the future.

It is typically used in concurrent programming,where one thread of execution can ask for the value of a `std::future` object,

and another thread of execution can set the value of the `std::future` object.

This allows the two threads to communicate with each other and coordinate their work.

  

`std::future` is a C++ standard library class that represents the result of an asynchronous operation.

It provides a mehanism to access the result of a petentially long-running operation,

such as a function call,without blocking the execution of the calling thread.

`std::future` allows the calling thread to retrieve the result of the asynchronous operation once it becomes available.

  

## code

  

```c++

#include <chrono>

#include <future>

#include <iostream>

#include <thread>

using namespace std;

  

int calculateResult() {

// This function perform a long and complex calculation & return the result

return 42;

}

  

int main() {

// Create a std::future object to hold the result of the calculation

std::future<int> result = std::async(calculateResult);

  

// Do some other work here,while the calculation is happening in the

// background

cout << "here" << endl;

std::this_thread::sleep_for(std::chrono::milliseconds(1000));

cout << "after main thread sleep 1s" << endl;

  

// When we are ready to get the result,we can call the get()method on the

// std::future object

cout << "the result is" << result.get() << endl;

  

cout << "end" << endl;

return 0;

}

```

  

## compile & execute

  

```shell

sjx@Samsung:~$ g++ future.cpp -lpthread -o future

sjx@Samsung:~$ ./future

here

after main thread sleep 1s

the result is42

end

sjx@Samsung:~$

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQzNDc4MjgyXX0=
-->