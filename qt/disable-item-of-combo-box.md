```cpp
class MyModel : public QStandardItemModel {
public:
    Qt::ItemFlags flags(const QModelIndex & index) const {
        Qt::ItemFlags flags = QAbstractItemModel::flags(index);

        if (index.row() == 1) {
            flags &= ~Qt::ItemIsEnabled;
        }

        return flags;
    }
};

MainWidget::MainWidget(QWidget *parent) : QWidget(parent), ui(new Ui::MainWidget) {
    ui->setupUi(this);
    MyModel *model = new MyModel();
    model->insertRow(0, new QStandardItem("one"));
    model->insertRow(0, new QStandardItem("two"));
    model->insertRow(0, new QStandardItem("three"));
    model->insertRow(0, new QStandardItem("four"));
    ui->comboBox->setModel(model);
}
```



