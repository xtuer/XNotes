```cpp
// QTimeLine 就是定时的发射信号，和自己用 QTimer 效果一样，但是可以设置缓存曲线

#include <QTimeLine>

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    QTimeLine *timeLine = new QTimeLine(1000);
    timeLine->setFrameRange(0, 100);
    timeLine->setLoopCount(0);
    QObject::connect(timeLine, &QTimeLine::frameChanged, [](int i) {
        qDebug() << i;
    });
    timeLine->start();

    return app.exec();
}
```



