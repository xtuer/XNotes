```cpp
Widget::Widget(QWidget *parent) : QWidget(parent), ui(new Ui::Widget) {
    ui->setupUi(this);

    QStandardItemModel *model = new QStandardItemModel();

    for (int i = 0; i < 150; ++i) {
        QString iconPath = QString("/Users/Biao/Desktop/%1.png").arg(i%2==0? "x":"y");
        QString text = i%2==0? "东邪西毒\n南帝北丐":"中神通"; // 可以多行显示
        QStandardItem *item = new QStandardItem(QIcon(iconPath), text);
        item->setToolTip("天地不仁, 以万物为刍狗<br>圣人不仁, 以百姓为刍狗<br>"
                         "<font color=\"red\">结刍为狗, 用之祭祀, 既毕事则弃而践之</font><br>"
                         "<img src=\"/Users/Biao/Desktop/Estas-Tonne.jpg\">");
        model->appendRow(item);
    }

    ui->listView->setModel(model);
    ui->listView->setWrapping(true); // 空间不够显示后自动折叠
    ui->listView->setFlow(QListView::LeftToRight); // 从左向右排列
    ui->listView->setViewMode(QListView::IconMode); // 文字在图标下面
    ui->listView->setResizeMode(QListView::Adjust); // 大小变化后重新布局 items
    ui->listView->setEditTriggers(QAbstractItemView::NoEditTriggers); // 不允许编辑
    ui->listView->setIconSize(QSize(64, 64)); // 图标大小
    // ui->listView->setGridSize(QSize(100, 120)); // item 的大小
    // ui->listView->setUniformItemSizes(true); // 所有的 item 一样大
}
```



