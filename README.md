# notes
个人笔记本 行动上的矮子，思想上的巨人

# 文章列表
  - [ ] 游览器原理
     - [ ] 输入地址到页面呈现发生了什么？

# 问题列表
## 问题8: react-keep 组件的实现思路
   ```
     此种实现方案会阻断数据流的传播，因此停止进行，如果后续有更好的方法，eg：官方的offScreen 可以再次进行开发
     
   ```
   ```
      将需要缓存的组件 在卸载的时候将其存放到外部的“display:none”的容器内部，保存其状态，当页面切换回来的时候，再将页面的恢复到对应的位置
      
      
   ```
   ```javascript
      if (!presentParentNode || !originalParentNode) {
       return;
     }
     const elementNodes = findElementsBetweenComments(originalParentNode, identification);
     const commentNode = findComment(presentParentNode, identification);
     if (!elementNodes.length || !commentNode) {
       return;
     }
     elementNodes.push(elementNodes[elementNodes.length - 1].nextSibling as Node);
     elementNodes.unshift(elementNodes[0].previousSibling as Node);
     // Deleting comment elements when using commet components will result in component uninstallation errors
     for (let i = elementNodes.length - 1; i >= 0; i--) {
       presentParentNode.insertBefore(elementNodes[i], commentNode);
     }
     originalParentNode.appendChild(commentNode);
   ```

## 问题7: 游览器的跳转问题-- react-router 是这么实现的？
   ```
      待思考
   ```

## 问题6: antd-pro 框架的自定义菜单如何配置？
   
   https://procomponents.ant.design/components/layout/#%E8%87%AA%E5%AE%9A%E4%B9%89-menu-%E7%9A%84%E5%86%85%E5%AE%B9

## <font color="red">问题5: electron 打包后的dmg文件运行会比编译器卡顿很多？</font>
    M1芯片的电脑 打包需要和正常的打包不同

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
   解决办法: 通过useRef变量缓存某些值或者方法；
   
   问题原因: 当前方法仅首次进行生成，生成的时候形成的了一个闭包，后续props的更没法使当前函数的刷新，所以导致函数的作用域还是旧的作用域；

## 问题3: monaco 编辑器如何获取当前行的的文本的内容？
    解决办法: XXX.getModel().setValueInRange(); 方法

## 问题2: table的header进行sorter设置的时候，点击会导致表格滚到最左侧？
    解决办法: 缓存onScroll方法、滚动距离 在table=》下的onchange之后调用一下滚动方法

## 问题1: 当table渲染数据过多时 导致页面卡顿 如何解决这个问题？
    1、使用react-virtualized 做虚拟滚动
    2、使用轻量级的react-window 进行优化
