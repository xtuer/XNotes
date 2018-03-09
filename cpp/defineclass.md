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



