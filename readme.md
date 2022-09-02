# fmt
A very small, simple, and fast formatting library for C++.

## Usage

```c++
std::map<std::string, int> map{ {"key1", 10}, {"key2", 20}};

std::string str = fmt::format("string {} number {} bool {} null {} map {}", "hello", 10, true, nullptr, map);

std::cout << str;

// or print it directly

fmt::println("string {} number {} bool {} null {} map {}", "hello", 10, true, nullptr, map)

// output: string hello number 10 bool true null null map [ key1: 10, key2: 20 ]
```

## Functions
#### all functions are under the fmt namespace
* `print` prints to stdout using printf
* `println` as expected does the same but prints with a new line. uses puts. 
* `fatal` prints and exits with status code -1
* `to_string` converts the given type to a string
* `string_of` determines the best way to get the string of a types and returns its string value
* `format` the base function for doing formatting

## Overload example
you can overload the fmt::to_string function to make it work with other types.
```c++
struct User
{
    int id;
    std::string name;
};

namespace fmt
{
    std::string to_string(const User& user)
    {
        return std::to_string(user.id) + ": " + user.name;
    }
}

#include "fmt.hpp"

int main()
{

    User user{10, "john"};
    std::string str = fmt::format("user -> {}", user);

    std::cout << str;
}
```

the header must be included after the overload so the string_of function can have access to the overload. alternatively you can just put it directly in the fmt.hpp file

## Motivation
I created this library because I didn't want to depend on a large library to do basic formatting, I just wanted the most simple formatting in a tiny hpp file.
In terms of performance it's much faster than sprintf. on my machine with an average input sprintf would take anywhere from 6k ns to 10k ns, but fmt::format would take 400 to 500 ns.