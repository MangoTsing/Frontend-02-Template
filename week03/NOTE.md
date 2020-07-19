学习笔记 week03

## 运算符和表达式

语法树：优先级关系

中缀树，抽象语法树

利用产生式描述优先级

### 表达式优先级：

1.最高优先级Member 表达式

```
a.b

a[b]

newFoo()
```

2.其次 new优先级 低一级

new Foo小于new Foo()

3.call（函数回调） 表达式

优先级更低

```
foo()['b']
foo().b
super()
```

4.左手右手运算 优先级

为什么 a.b = c成立 a + b = c 不成立

只有满足 左手表达式 才可以放在 = 号左边

那什么是 左手表达式呢， 就是能放在等号左边的表达式。

例子a:

​	Update 表达式

```
a ++ 
a --
++ a
-- a
```

几乎一定属于右手表达式。在JS里没有例外，大部分没有例外

l例子b:

​	Unary单目运算符

```
delete 引用类型才可以生效
void foo() 返回值稳定undefined，改变语法结构
typeof a
+ a
~ a 整数按位取反
await a 会对后续语法造成影响
```

例子c:

Exponental 右结合运算符 乘方

```
 **
```

3 ** 2 ** 3

5.优先级更低

乘除运算，加减，shift位移>><<，关系符

加号会出现连接字符串和数字加法，类型转换比较复杂

关系比较表达式 大小于号， instanceof 和 In 等。

6.优先级更低

比较号

```
== 转换规则比较多，如果确定两边相同类型可以尝试使用

!=
```

按位与按位或 更低

​	 & |

7.逻辑运算

 && ||

8.三目运算符

? :

### 表达式的类型转换

- a+b
- “false" == false 复杂的，建议用===或者提前做完类型转换
- a[o] = 1

拆箱转换 Unboxing

- ToPremitive

- toString vs valueOf

- Symbol.toPrimitive

  ```
  var o = {
  	toString(){ return "2"},
  	valueOf(){return 1},
  	[Symbol.toPrimitive](){return 3}
  }
  
  ```

  定义了toPrimitive就会忽略toString和valueOf

  

加法先调用valueOf，当作为属性名优先调用toString()方法，比如定义一个x[o] = 1，打印出来x得到的key是2，value是1

装箱转换 Boxing

​	Object 提供了转换的包装类

- Number new Number() 返回值的不同
- String 同上
- Boolean 同上
- Symbol new Object(Symbol("a")) 加了new Symbol会报错

Number语法，在2018标准里分成4个部分

10进制表示

小数点可以存在前后都合法，同时支持科学计数法 `1e3`

2进制表示

0b开头，只有0或者1

8进制表示

0o开头，只能0~7

16进制表示

Hex，以0x开头，还可以从0~F来表示0~15

## 语句

### 语法

> 用语句完成控制流程

- 简单语句
- 组合语句
- 声明

### 运行时

执行记录，作用域相关

啥是执行记录？

每一个语句执行后产生的

```
[[type]]: normal, break, continue, return, or thorw

[[value]]: 基本类型

[[target]]：label 其实就是语句前的标识符和冒号 例如 case:
```

## 简单语句复合语句

## 声明

## 宏任务和微任务

## 函数调用

### Realm

所有的内置对象会放在一个Realm里

比如 var x = {} // 它继承自哪一个obj?

因此，创建数组和对象直接量都会创建对象。

使用隐式转换也会创建对象，比如 xxx.toString()

这些的原型来自于Realm，如果没有它，就不知道它们的原型是什么。同时Realm在ES2018之前没有得到很好的标准化。

> 可以互相传递原型

找到所有的Realm对象，做一个可视化

[http://www.ecma-international.org/ecma-262/11.0/index.html#sec-code-realms](http://www.ecma-international.org/ecma-262/11.0/index.html#sec-code-realms)