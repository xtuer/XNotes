```cpp
// The program is used to demostrate function template and
// overrided function template

#include <iostream>

template<typename T>
void display(T t) {
    std::cout << "T: " << t << std::endl;
}

template<typename T, typename S>
void display(T t, S s) {
    std::cout << "T: " << t << ", S: " << s << std::endl;
}

// SIZE is a const variable
template<typename T, int SIZE>
void display(T t) {
    for (int i = 0; i < SIZE; ++i) {
        std::cout << "For: " << i << " ==> " << t << std::endl;
    }
}

int main() {
    display<int>(3);
    display<int, double>(3, 4.5);
    display<char, 5>('B');

    return 0;
}

```



