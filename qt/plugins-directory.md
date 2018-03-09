```cpp
int main(int argc, char *argv[]) {
    QApplication::addLibraryPath("./plugins");
    QApplication app(argc, argv);
}

把所有的插件放到 exe 所在目录的 plugins 目录中

----plugins
--------sqldrivers
--------imageformats
--------platforms
--------iconengines
```



