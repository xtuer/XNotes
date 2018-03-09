```cpp
#include <iostream>
using namespace std;

int main(int argc, char *argv[]) {
    int matrix[10][10];
    int number = 0;

    for (auto row = begin(matrix); row != end(matrix); ++row) {
        for (auto data = begin(*row); data != end(*row); ++data) {
            *data = number++;
        }
    }

    for (auto row = begin(matrix); row != end(matrix); ++row) {
        for (auto data = begin(*row); data != end(*row); ++data) {
            std::cout << *data << ", ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```



