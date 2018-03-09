```cpp
Widget::Widget(QWidget *parent) : QWidget(parent), ui(new Ui::Widget) {
    ui->setupUi(this);
//    ui->widget->setAttribute(Qt::WA_TransparentForMouseEvents,true);
    band = new QRubberBand(QRubberBand::Rectangle); // parent 为 null 显示为独立窗口
}

Widget::~Widget() {
    delete ui;
}

void Widget::resizeEvent(QResizeEvent *event) {
       band->setGeometry(10, 10, width() - 20, height() - 20);
       band->show();
}

```



