```cpp
#include <iostream>

// The program is used to demostrate class template

// SIZE is a const variable
template<typename T, int SIZE>
class Xtuer {
public:
    void foo(T t) {
        std::cout << "foo() ==> T: " << t << ", SIZE: " << SIZE << std::endl;
    }

    void bar(T t);
};

template<typename T, int SIZE>
void Xtuer<T, SIZE>::bar(T t) {
    std::cout << "bar() ==> T: " << t << ", SIZE: " << SIZE << std::endl;
}

int main() {
    Xtuer<int, 5> xtuer;
    xtuer.foo(3);
    xtuer.bar(6);

    return 0;
}

```



