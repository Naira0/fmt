# fmt

### Usage

```c++
std::map<std::string, int> map{ {"key1", 10}, {"key2", 20}};

std::string str = fmt::format("string {} number {} bool {} null {} map {}", "hello", 10, true, nullptr, map);

std::cout << str;

// output: string hello number 10 bool true null null map [ key1: 10, key2: 20 ]
```

you can also use fmt::print to print stuff directly.

you can overload the fmt::to_string function to make the format function work with your own custom type.

it should already work fine with most builtin types and containers.

### overload example
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

the header must be included after the overload so the string_of function can have access to the overload.
