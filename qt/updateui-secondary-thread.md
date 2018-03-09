Because of limitations inherited from the low-level libraries on which Qt's GUI support is built, _QWidget and its subclasses are not reentrant_. One consequence of this is that we cannot directly call functions on a widget from a secondary thread. If we want to, say, change the text of a QLabel from a secondary thread, we can emit a signal connected to QLabel::setText\(\) or call **QMetaObject::invokeMethod\(\)** from that thread. For example:

```cpp
void MyThread::run() {
    ...
    QMetaObject::invokeMethod(label, "setText", Q_ARG(QString, "Hello"));
    ...
}
```



