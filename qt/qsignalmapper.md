QSignalMapper 主要使用的场景是多个 widget 触发同一个 slot，每个 widget 都对应一个数据\(mapper-&gt;setMapping\(\) 中设置\)，在 slot 中只关心数据，并不关心 widget 是谁，例如计算器。

> 当然 widget 对应的数据也可以用 property 设置，QSignalMapper 只是一种方式而已。

```cpp
Widget::Widget(QWidget *parent) : QWidget(parent), ui(new Ui::Widget) {
    ui->setupUi(this);

    QSignalMapper *mapper = new QSignalMapper(this);
    mapper->setMapping(ui->startButton, "B1");
    mapper->setMapping(ui->stopButton,  "B2");

    connect(ui->startButton, &QPushButton::clicked, mapper, QOverload<>::of(&QSignalMapper::map));
    connect(ui->stopButton,  &QPushButton::clicked, mapper, QOverload<>::of(&QSignalMapper::map));

    connect(mapper, QOverload<const QString &>::of(&QSignalMapper::mapped), [this](const QString &text) {
        qDebug() << sender(); // sender() 为 NULL
        qDebug() << text;
    });
}
```



