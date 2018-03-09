```cpp
int main(int argc, char *argv[]) {
    QApplication a(argc, argv);
    Widget w;
    w.show();

    QSettings settings("xxxx.ini",QSettings::IniFormat);
    settings.setIniCodec(QTextCodec::codecForName("UTF8"));
    //settings.setValue("username", "呼呼"); // key 不要用中文，否则会被 encoded
    //settings.setValue("password", "秘密");
    //settings.sync();

    qDebug() << settings.value("username").toString();
    qDebug() << settings.value("password").toString();

    return a.exec();
}
```



