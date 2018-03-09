设置 QListView, QTableView 的 item 的 padding:

```css
/* Works for both QListView and QListWidget */
QListView::item {
    /* Won't work without borders set */
    border: 0px;
    padding-left: 10px;
}

/* For icon only */
QListView::icon {
    left: 10px;
}

/* For text only */
QListView::text {
    left: 10px;
}
```

Unfortunately I don't have an answer to the question \_why doesn't it work without borders set, \_but ... it works when you do set them.

## 去掉虚线框

```css
QWidget:focus{
    outline: none; /* Remove all  QWidget's focus border */
} 
```



