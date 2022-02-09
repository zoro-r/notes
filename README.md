# notes
记录一直以来的一些问题以及解决方案

## 问题1: 当table渲染数据过多时 导致页面卡顿 如何解决这个问题？
    1、使用react-virtualized 做虚拟滚动
    2、使用轻量级的react-window 进行优化

## 问题2: table的header进行sorter设置的时候，点击会导致表格滚到最左侧？
    1、解决办法: 缓存onScroll方法、滚动距离 在table=》下的onchange之后调用一下滚动方法
