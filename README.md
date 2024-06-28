Here is a short sample of how to use the library:

```C++
#include <iostream>
#include <json-ser/json-ser.hpp>
#include <ser/macro.hpp>
#include <sstream>

struct Test
{
  SER_PROPS(one, two);
  int one;
  std::string two;
};

auto main() -> int
{
  {
    auto ss = std::istringstream{R"({"one":314, "two":"hello world"})"};
    Test test;
    jsonDeser(ss, test);
    std::cout << "One: " << test.one << std::endl;
    std::cout << "Two: " << test.two << std::endl;
  }
  {
    auto ss = std::ostringstream{};
    Test test;
    test.one = 420;
    test.two = "hello again";
    jsonSer(ss, test);
    std::cout << ss.str() << std::endl;
  }
}
```


Output:
```
One: 314
Two: hello world
{
  "one": 420,
  "two": "hello again"
}
```
