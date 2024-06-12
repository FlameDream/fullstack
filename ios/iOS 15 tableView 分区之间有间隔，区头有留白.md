## iOS 15 tableView 分区之间有间隔，区头有留白

在iOS15以上的系统版本下，tableView 设置Section过程中，Section直接的Header留有空白区域。

#### 解决方案

```object-oc

if (@available(iOS 15.0, *)) {
    self.tableView.sectionHeaderTopPadding = 0;
}

```