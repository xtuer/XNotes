![](/assets/qt/line-performance.png)

```cpp
#include <QApplication>
#include <QChartView>
#include <QLineSeries>
#include <QSplineSeries>
#include <QChart>

using namespace QtCharts;

int main(int argc, char *argv[]) {
    QApplication a(argc, argv);
    QChart *chart = new QChart();

    // 10 条线，每条有 10 万个点，使用 OpenGL 渲染
    for (int i = 0; i < 10; ++i) {
        QLineSeries *lineSeries = new QLineSeries();
        lineSeries->setName(QString("Line: %1").arg(i+1));
        lineSeries->setUseOpenGL(true);

        for (int x = 0; x < 100000; ++x) {
            lineSeries->append(x, qrand() % ((i+1) * 100));
        }

        chart->addSeries(lineSeries);
    }

    chart->setTitle("10 条线，每条有 10 万个点");
    chart->createDefaultAxes();
    chart->axisX()->setRange(100, 200);

    // 显示图标的 view
    QChartView *chartView = new QChartView(chart);
    chartView->setRenderHint(QPainter::Antialiasing);
    chartView->setWindowTitle("OpenGL 折线性能测试");
    chartView->resize(800, 300);
    chartView->show();

    return a.exec();
}
```

