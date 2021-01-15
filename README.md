# ChainCall

## Usage

```cpp

    #include "chaincall.hpp"

    ...
    
    //chain
    auto v1 = chaincall::chain() >> [] { return 42; } >> add_1 >> power_2 >> div_2;
    auto v2 = chaincall::chain(2) >> add_1 >> power_2 >> div_2;
    auto v3 = chaincall::chain(1, 2) >> [](int a, int b) { return a + b; } >> power_2 >> div_2;
    auto v4 = chaincall::chain() >> [] { return make_tuple(3, 7); } >> [](int a, int b) { return a * b; } >> power_2 >> div_2;

    cout << v1.value << endl; //(42+1)**2/2 = 924
    cout << v2.value << endl; //(2+1)**2/2 = 4
    cout << v3.value << endl; //(1+2)**2/2 = 4
    cout << v4.value << endl; //(3*7)**2/2 = 220

    //pipe
    auto composed_func1 = chaincall::pipe([](int a, int b) { return a * b; }, power_2, div_2);
    auto composed_func2 = chaincall::pipe() << add << power_2 << div_2;

    cout << composed_func1(2, 7).value << endl; //(2*7)**2/2 = 98
    cout << composed_func2(2, 7).value << endl; //(2+7)**2/2 = 40
    
    ...
    
```
## Output

```

924
4
4
220
98
40

```