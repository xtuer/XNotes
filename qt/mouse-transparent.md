在Qt中，QWidget 默认是非鼠标穿透的，如果将 QWidget 覆盖在其他控件上面，即使这个 QWidget 是透明的，鼠标也是无法点击下面的控件的。我们可以通过设置它的属性来实现鼠标穿透，也即点击它的时候它接收不到鼠标事件，它的 children 也接收不到鼠标事件，鼠标事件会发送给它后面的 QWidget:

```cpp
QWidget::setAttribute(Qt::WA_TransparentForMouseEvents,true);
```



