我们继承 QWidget 的类默认 QSS 不起作用，需要调用 **setAttribute\(Qt::WA\_StyledBackground, true\)** 后才行。



典型的表述\(之一\)是，从 QWidget 派生一个窗口，使用 QSS 设置背景，在 Designer 中可以看到效果，编译运行后，没有背景。

该怎么办呢？对此Manual中专门有强调，摘录如下：



If you subclass from QWidget, you need to provide a paintEvent for your custom QWidget as below:

