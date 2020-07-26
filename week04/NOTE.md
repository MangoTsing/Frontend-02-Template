## 计算机网络

学习笔记

## 浏览器

- URL HTTP
- HTML parse
- DOM  css computing
- CSS layout
- position render
- BItmap 浏览器的网页就是得到一个bitmap图片

基础渲染流程



## 有限状态机

重点在于**机**，而不是状态。

每一个状态是一个机器，互相解耦。编写状态机的代码，可以忽略其他状态机的代码。

应用于：游戏中敌人的AI，静止状态和战斗状态简化逻辑。

每个状态机都接受相同的状态，状态机内都是纯函数，不应该受外部控制，不读取外部状态。同时需要知道自己的下一个状态。

Moore状态机有确定的下一个状态，Mealy状态机根据输入决定下一个状态。（摩尔和米粒）

iSO七层网络模型



HTTP 由一个Req Res组成，全双工（可以你发给我，也可以我发给你），一个Req 回来一个 Res，如果多个重复，那肯定http出错了

TCP 流，包，端口，IP地址，re quire('net')，libnet/libpcap的c++基础库，可以把流经网卡本不属于的包给抓出来，用于其他途径场景，处理特殊的ip。

INTERNET

4G/5G/WIFI



## toy-browser



- http协议 文本类型协议，与二进制相对，所有的都是字符串，unicode等传输

Request:

Request line 

- POST / GET /PUT 等
- path: HOST，路径
- 协议版本 HTTP /1.1

HEADER

-  ip
- Content-type 类型等

Body

字符串内容



### HTTP请求总结

- Content type 必要字段
- body 是 key value格式
- 不同的content type 影响 body 格式

Response：

Response line:

- 协议，状态码，固定文本 
- Header 部分
- Body部分

>  Body Node 返回的 chunked body格式

### send请求总结

- 设计connection链接，通过net模块可以创建
- 收到数据，并且实现parser函数，解析数据
- 根据praser状态，resolve整个Promise



### ResponseParse总结

- Response必须分段构造，可以使用状态机构造，要创造一个ResponsePrase来负责构造
- 分段处理ResponseText时，用状态机来分析结构

### ResponseBody总结

- Response的body可以根据Content-Type不同，有不同结构，因此会采用子Parser的结构来解决问题
- 以TrunkedBodyParser为例，同样用状态机来处理问题，虽然不一定完全的是Mealy状态机



## parserHTML 文件



### 总结

- 把parser单独拆倒文件中
- parser接受HTML 文本作文参数，返回一颗dom树

第二步总结

- 使用FSM（状态机）来实现HTML的分析
- 因为HTML标准中，已经规定了HTML的状态，80种
- 使用部分HTML状态，来实现



### 解析标签

开始标签

结束标签

自封闭标签

流程：

-  寻找<符号，寻找TagName，然后再寻找endTagName状态，寻找tagName的过程，可以match\t，换行\n，\f，空格符号

- 如果match到空格，可以确定是 tag的属性状态 ，如果是属性state，可以判断=号，然后死等>

- 如果match到/符号，可以确定是自封闭标签，那后面只能是`>`符号

- 如果是>可以确定是开始标签

状态机还需要计算

### 创建元素

- 加入计算逻辑

把我们想要的元素token拿到



### 小总结

- 在状态机中，加入业务逻辑，计算type，以及tagName或者content值
- 在标签结束状态，创建emit函数，提交整体token，暂时还未创建dom结构

### 处理属性

流程：

- 进入处理属性的判断，value遇到 = 进入属性判断，然后判断双引号，单引号，以及没有引号，还要判断afterQuoted，属性后需要有空格或者直接>符号
- 遇到 / 以及>执行结束判断
- 遇到EOF进行结束判断
- 结束后写入token内

小总结：

- 属性分单双无引号三种，因此需要较多状态处理
- 处理属性方式和标签类似
- 属性结束，把属性加到标签的token上，形成一个完整的标签Token

### 使用token构建DOM树

上面几个都是词法分析，下面就是语法分析了。

如果想要友好，可以实现如果标签没有封闭等特殊情况等额外处理，方便使用，但我们没必要那么麻烦。



接下来需要使用`emit(token)`去push stack

需要把element push 进入数组里

```javascript
let element = {
	children: [],
	type: 'element',
	attributes: []
}
this.stack = [{type: 'document' , ...}]
```

最终生成的DOM树类似

```javascript
let dom = {
      children: [
        {
          attributes: [...],
          children: [obj,obj],
          parent: {type: "element", children: [], ...},
          tagName: "head",
          type: "element"
        }
      ]
}
```



#### 小总结构建树

- 使用栈去构建DOM树
- 遇到开始标签，创建元素入，遇到结束标签出
- 自封闭节点可视为入栈后立即出栈
- 任何元素的福元素是他入栈前的栈顶

最终构建了一个DOM树的数据结构，类似上面的 dom



### 最终步骤，将文本节点加入DOM树

给element追加content值，type: text

进行文本节点合并入element里

- 文本节点与自定义标签处理类似，不会入栈
- 但多个文本节点需要合并

完成整个HTMl的解析

 