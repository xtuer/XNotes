```cpp
class Person {
public:
    // 构造函数
    Person(int id = 11, const QString &name = "No Name") : id(id), name(name) {

    }

    // 析构函数: 如果有可能被继承，析构函数需要时 virtual 的
    virtual ~Person() {

    }

    // 拷贝构造函数
    Person(const Person &other) {
        id = other.id;
        name = other.name;
    }

    // 赋值运算符
    Person& operator=(const Person &other) {
        id = other.id;
        name = other.name;
        return *this;
    }

    int getId() {
        return id;
    }

    // 给 const Person 对象使用
    int getId() const {
        return id;
    }

    void setId(int id) {
        this->id = id;
    }

    QString getName() {
        return name;
    }

    QString getName() const {
        return name;
    }

    // 参数为类的对象时尽量使用 const Type &，否则参数就不能使用临时变量
    void setName(const QString &name) {
        this->name = name;
    }

private:
    int id;
    QString name;
    QString flag = "PERSON"; // 定义成员变量时 C++11 可以进行初始化
};

int main(int argc, char *argv[]) {
    Person p;
    qDebug() << p.getId();

    const Person &pref = p;
    qDebug() << pref.getId();
    qDebug() << pref.getName();


    return 0;
}

```

## 编译器优化

```cpp
#include <QDebug>

/**
 * 类的 4 个必要函数: 构造函数、拷贝构造函数、赋值运算符、析构函数
 */
class Box {
public:
    // 构造函数
    Box() {
        qDebug() << "Box()";
    }

    // 拷贝构造函数
    Box(const Box &other) {
        qDebug() << "Box(const Box &other)";
    }

    // 赋值运算符
    Box& operator=(const Box &other) {
        qDebug() << "Box operator=(const Box &other)";
        return *this;
    }

    // 析构函数
    ~Box() {
        qDebug() << "~Box()";
    }
};

Box foo() {
    return Box();
}

Box bar() {
    Box b;
    return b;
}

int main(int argc, char *argv[]) {
    Box b1;
    Box b2 = b1;
    Box b3 = Box();
    Box b4 = foo();
    Box b5 = bar();

    b3 = b2 = b1;

    return 0;
}
```

输出:

```
Box()
Box(const Box &other)
Box()
Box()
Box()
Box operator=(const Box &other)
Box operator=(const Box &other)
~Box()
~Box()
~Box()
~Box()
~Box()
```

