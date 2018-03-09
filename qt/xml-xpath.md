```cpp
#include <QDebug>
#include <QApplication>
#include <QXmlQuery>

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    QString html = "<html><body><span>Alice</span></body></html>";

    QXmlQuery query;
    query.setFocus(html);
    query.setQuery("/html/body/span/text()"); // text() 表示取文本

    QString r;
    query.evaluateTo(&r);
    qDebug() << r;

    return app.exec();
}

输出 

Alice
```



