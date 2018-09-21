## 点击 legend 隐藏显示曲线

Legend 对应一组 QLegendMarker，点击它的时候发射 clicked 信号:

```cpp
const auto markers = chart->legend()->markers();
for (QLegendMarker *marker : markers) {
    connect(marker, &QLegendMarker::clicked, [=] {
        marker->series()->setVisible(!marker->series()->isVisible());
        marker->setVisible(true);
    });
}
```

## 缩放

```cpp
chart->roomIn(); // 放大: factor 为 2
chart->roomOut(); // 缩小: factor 为 2
chart->roomReset(); // 恢复最初大小
```

