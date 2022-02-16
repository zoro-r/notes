# notes
记录一直以来的一些问题以及解决方案

## 问题4: react hooks组件 当遇到antv的 xxx.on('plot:click', (args: any) 方法的回调的时候，内部的变量会与外部的不一致；代码如下
   ```javascript
   
       const [data, setData] = useState('1');
       // 1 
       console.log(data);
       chart.chart.on('tooltip:change', (ev: any) => {
         hoverData = ev.data;
       });
       chart.chart.on('plot:click', (args: any) => {
          // 2
          console.log(data);
       });
       
       当setData改变了data的值后 1和2的打印的值不一致 1依旧为更新之前的值
   ```
   解决办法: 将data的作用域提升到最外面，且不使用useState进行保存

## 问题3: monaco 编辑器如何获取当前行的的文本的内容？
    解决办法: XXX.getModel().setValueInRange(); 方法

## 问题2: table的header进行sorter设置的时候，点击会导致表格滚到最左侧？
    解决办法: 缓存onScroll方法、滚动距离 在table=》下的onchange之后调用一下滚动方法

## 问题1: 当table渲染数据过多时 导致页面卡顿 如何解决这个问题？
    1、使用react-virtualized 做虚拟滚动
    2、使用轻量级的react-window 进行优化
