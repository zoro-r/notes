
# Buffer

Buffer的用处是什么？

在Node中,应用需要处理网络协议、操作数据库、处理图片、接收上传文件等，在网络流和文件的操作中，还要处理大量二进制数据，JavaScript自有的字符串远远不能满足这些需求，于是Buffer对象应运而生====Buffer：string字符串的延伸？

## 结构

类似于数组，它的元素为16进制的2位数，即0到255的数值。

```node
  var str = "Joker 最棒";
  var bug = new Buffer(str, 'utf-8');
  => <Buffer e6 xx xx xx>
```

### 存取值
```node
  var buf = new Buffer(100);
  buf[10] ===> 0~255的一个随机整数
  // 赋值
  buf[10] = 100;
  // buf[10] ===> 100
  // 如果赋值为非0～255之间的数字呢？
  buf[20] = -100; // 156 = (-100 + 256)
  buf[21] = 300; // 44 = (300 - 256)
  buf[20] = 3.14; // 3 舍去小数部分

```

### 内存分配

buffer的内存分配事在node的C++层面实现内存申请的，Node 使用slab分配机制，slab是一块申请好的固定大小的内存区域，slab有三种状态

1、full：完全分配状态

2、partial：部分分配状态。

3、empty：没有被分配状态

Node以8KB来界限来区分Buffer是大对象还是小对象

```
 Buffer.poolSize = 8 * 1024;
```

## 转换

Buffer对象可以与字符串之间相互转换，目前之前的类型如下

- ASCII
- UTF-8
- UTF-16LE/UCS-2
- Base64
- Binary
- Hex

### 字符串转Buffer
 ```
  new Buffer(str, [encoding]);
  
  buf.write(string, [offset],[length],[encoding])
 ```
### Buffer 转字符串

```node
 bug.toString([encoding = 'UTF-8'], [start], [end])
 
 // 判断 是否支持编码
 
 Buffer.isEncoding(encoding)
 
 对于不支持的类型，可以借助Node生态圈中的模块完成 iconv、iconv-lite
 
 var iconv = require('iconv-lite');
 var str = iconv.decode(buf,'win1251');
 var bug = iconv.encode('Sample input string','win1251');
```

### 乱码问题
```
 造成原因，加入我们界定了Buffer对象的长度为11，而中文一个占3个字节,有些中文会被截断，所以会出现这种乱麻
 
 解决方法
 
 1、增加Buffer的长度
 2、
 
 setEncoding
 
```


## Buffer与性能
通过预先转换静态内容为Buffer对象，可以有效地减少CPU的重复使用，节省服务器资源，在NODE构建的WEB应用中，可以选择将页面中的动态内容和静态内容分离，静态内容部分为Buffer，







