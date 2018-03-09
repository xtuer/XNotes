## Qt 下载

[http://download.qt.io/archive/qt](http://download.qt.io/archive/qt)

## 设置 QWidget 为 Dialog

设置为 Dialog，是希望在任务栏不显示图标

```cpp
widget.setWindowFlags(Qt::Dialog | Qt::Popup | Qt::FramelessWindowHint);
```

> Qt::Popup 不能少

## 快捷键

```cpp
QShortcut *shortcut = new QShortcut(QKeySequence(Qt::CTRL + Qt::Key_L), this);

connect(shortcut, &QShortcut::activated, [] {
    qDebug() << "shortcut";
});
```

```cpp
void Widget::loadQss() {
    QAction *action = new QAction();
    action->setShortcut(QKeySequence(Qt::CTRL + Qt::Key_L));
    this->addAction(action);

    connect(action, &QAction::triggered, [] {
        UiUtil::loadQss();
    });
}
```

## INCLUDEPATH and DEPENDPATH

INCLUDEPATH is used during compilation to find included header files. DEPENDPATH is used to resolve dependencies between header and source files, eg. which source files need to be recompiled when certain header file changes. If you modify a header file in folder foo/ and foo/ is not listed in DEPENDPATH, nothing gets recompiled. If foo/ is listed in DEPENDPATH, source files depending on that header will get recompiled. Paths can be relative to the .pro file or absolute paths.

## Post event

```cpp
void Widget::click1() {
    QKeyEvent *pressKey = new QKeyEvent(QEvent::KeyPress, Qt::Key_Comma, Qt::NoModifier, ",");
    QKeyEvent *releaseKey = new QKeyEvent(QEvent::KeyRelease, Qt::Key_Comma, Qt::NoModifier, ",");
    QApplication::postEvent(ui->lineEdit, pressKey);
    QApplication::postEvent(ui->lineEdit, releaseKey);
}
```

## 使自定义 Widget 的 QSS 生效

我们继承 QWidget 的类默认 QSS 不起作用，需要调用`setAttribute(Qt::WA_StyledBackground, true)` 后才行。

## QLineEdit password echo

QLineEdit: The password character can be styled using the lineedit-password-character property.

```css
QLineEdit {
    lineedit-password-character: 9679;
}
```

## 格式化数字

```cpp
qDebug() << QString("%1, %2")
    .arg(14, 4, 10, QChar('0'))          // 0014
    .arg(15.775, 0, 'f', 5, QChar('0')); // 15.77500
```

## 绘制 Check Box

```cpp
void Widget::paintEvent(QPaintEvent *) {
    QStyleOption opt;
    opt.init(this);
    opt.rect = QRect(100, 100, 20, 20);
    opt.state |= QStyle::State_On;

    QPainter p(this);
    p.drawRect(opt.rect);
    style()->drawPrimitive(QStyle::PE_IndicatorCheckBox, &opt, &p, this);
}
```

## readData readRawData

Qt difference between read readData readRawData

## XML

生成一个 XML 文件用的是以前的方法 QDom 那一套方法，但是在生成元素的属性的时候发现每次生成属性的属性顺序都是随机的，查了很久终于发现有人说在构建环境里面设置 `QT_HASH_SEED=1` 就可以，我也试了确实顺序不在随机了每次都是固定的。

## 计算 MD5

```cpp
#include <QCryptographicHash>
#include <QDebug>

int main(int argc, char *argv[]) {
    QByteArray hex = QCryptographicHash::hash("Biao", QCryptographicHash::Md5).toHex();
    QString md5(hex.constData());

    qDebug() << md5;

    return 0;
}
```

## Subdirs Project 中设置当前项目

所谓当前项目，是指点击运行按钮\(CMD+R\)时启动的项目

设置: Projects &gt; Run &gt; Run configuration

![](/assets/qt/subdirs-projects.png)

## 启用 Retina 高分辨率

```cpp
// 启用 Retina 高分辨率
QApplication::setAttribute(Qt::AA_UseHighDpiPixmaps);
QApplication::setAttribute(Qt::AA_EnableHighDpiScaling);
QApplication app(argc, argv);
```

## Modal 窗口局部事件循环

```cpp
TopWindow window(centralWidget, {4, 4, 4, 4}, {8, 8, 8, 8}, ":/image/colorful-border.png");
window.setWindowFlags(Qt::Dialog | Qt::Popup | Qt::FramelessWindowHint);
window.setWindowModality(Qt::ApplicationModal);
window.show();

// 进入局部事件循环，阻塞代码继续往下走，窗口关闭时结束此局部事件循环，控制权交还给 QApplication
// The event loop returns from the call to quit().
QEventLoop loop;
connect(&window, &TopWindow::aboutClose, &loop, &QEventLoop::quit);
loop.exec();

qDebug() << "Final";
```

## 窗口居中显示

```cpp
void UiUtil::centerWindow(QWidget *window) {
    // This doesn't show the widget on the screen since you don't relinquish control back to the queue
    // until the hide() happens. In between, the invalidate() computes the correct positions.
    window->show();
    window->layout()->invalidate();
    window->hide();

    QSize size = qApp->desktop()->availableGeometry().size() - window->size();
    int x = qMax(0, size.width() / 2);
    int y = qMax(0, size.height() / 2);
    window->move(x, y);
}
```

## 从 Layout 中删除 Widget

```cpp
1. widget->deleteLater();  // 删除 widget，会自动把它从 layout 中删除，也会删除它相关的 QLayoutItem
2. layout->removeWidget(); // 会把 widget 和它相关的 QLayoutItem 从 layout 中删除，需要自己 delete widget
```

> After looking in the source code: `removeWidget()` method also remowes according QLayoutItem. It's a pity that it is not well documented.

```cpp
// 清空 layout
void UiUtils::clearLayout(QLayout *layout) {
    if (layout) {
        QLayoutItem *item;

        // The key point here is that the layout items are stored inside the layout in a stack
        while((item = layout->takeAt(0)) != 0) {	
            if (item->widget()) {
                layout->removeWidget(item->widget());
                delete item->widget();
            }	

            delete item;
        }
    }
}
```



