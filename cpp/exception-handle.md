```cpp
#include <iostream>

class MyError {
public:
    MyError() {
        std::cout << "MyError()" << std::endl;
    }

    ~MyError() {
        std::cout << "~MyError()" << std::endl;
    }
};

void test() {
    try {
        throw MyError();
        throw "The cat ate my homework!";
    } catch (const char *err) {
        std::cout << err << std::endl;
    } catch (const MyError &myErr) {
        std::cout << "caught my error" << std::endl;
    } catch (...) {
        std::cout << "Unknown error" << std::endl;
    }
}

int main() {
    test();

    return 0;
}
```



