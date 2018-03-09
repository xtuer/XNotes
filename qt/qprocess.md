```cpp
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    QTime time;
    time.start();
    QProcess process;
//    process.start("J:\\NBTSCAN\\nbtscan.exe", QStringList() << "172.17.78.0/24");
//    process.start("J:\\NBTSCAN\\nbtscan.exe -v -s : 172.17.78.0/24");
    process.start("J:\\NBTSCAN\\command\\nbtscan.exe", QStringList() << "-v" << "-s" << ":" << "172.17.78.0/24");

    qDebug() << process.arguments();

    process.waitForFinished();

    while (process.canReadLine()) {
        qDebug() << process.readLine().trimmed();
    }

    qDebug() << "Using " << time.elapsed();

    return app.exec();
}
```

```cpp
#include <QApplication>
#include <QProcess>
#include <QDebug>

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    QProcess *process = new QProcess();
    process->start("/bin/sh", QStringList() << "/Users/Biao/Desktop/x.sh");

    QObject::connect(process, &QProcess::readyReadStandardOutput, [=] {
        qDebug().noquote() << process->readAll().trimmed();
    });

    return app.exec();
}

------------------------ x.sh -------------------------
max=10
for (( i=2; i <= $max; ++i ))
do
    echo "$i"
    sleep 1
done
```



