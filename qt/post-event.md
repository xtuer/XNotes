```cpp
void Widget::click1() {
    QKeyEvent *pressKey = new QKeyEvent(QEvent::KeyPress, Qt::Key_Comma, Qt::NoModifier, ",");
    QKeyEvent *releaseKey = new QKeyEvent(QEvent::KeyRelease, Qt::Key_Comma, Qt::NoModifier, ",");
    QApplication::postEvent(ui->lineEdit, pressKey);
    QApplication::postEvent(ui->lineEdit, releaseKey);
}
```



