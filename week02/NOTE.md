本周学习总结：



## 什么是语言

### 语言的分类

#### 非形式语言

#### 形式语言

#### 乔姆斯基谱系

## 产生式

### 什么是产生式？

### 巴特斯诺尔范式（BNF）

### BNF定义可以递归，尝试写一个BNF

```
BNF

<LeftKuohaoExpression>::=<LeftKuohaoExpression>"("<MultiplicativeExpression>|<AddtiveExpression>|<Number>
<RightKuohaoExpression>::=<LeftKuohaoExpression>+<RightKuohaoExpression>")"+
<MultiplicativeExpression>::=<Number>|<MultiplicativeExpression>"*"<Number>|<MultiplicativeExpression>"/"<Number>
<AddtiveExpression>::=<MultiplicativeExpression>|<AddtiveExpression>"+"<MultiplicativeExpression>|<AddtiveExpresstion>"-"<MultiplicativeExpression>
```

### 通过产生式理解乔姆斯基谱系

#### 上下文相关，无关文法

JS总体属于无关文法，但也有相关文法。

### 其他产生式

EBNF，ABNF

产生式大体意思相同，但写法不同，看明白一个可以大概看懂其他的。

## 现代语言分类

### 通过用途分类

数据描述语言 DDL（Data Description Language）： JSON,HTML,XAML,SQL,CSS,XML,SGML

图灵完备的编程语言： C，C++，C#，Java，Python，Ruby，Rust，Perl，Lisp，T-SQL，Clojure，Haskell，JavaScript，Go，PHP，Object-C，Swift，Dart，v，Scheme，OCaml，Standard ML，Unlambda



### 通过表达方式分类

声明式语言： JSON,HTML,XAML,SQL,CSS,XML,SGML，Lisp，Clojure，Haskell，Scheme，OCaml，Standard ML，Unlambda

命令式语言： C，C++，C#，Java，Python，Ruby，Rust，Perl，T-SQL，JavaScript，Go，PHP，Object-C，Swift，Dart，v



### 编程语言的静态与动态

源码运行在客户端的，为动态语言，运行在程序员端的叫静态语言。



### 一般命令式编程

Atom -> Expression -> StateMents -> Structure -> Program

有语句的语言，基本已经可以称作为图灵完备了。

语法作为线索，通过语义和运行时产生的效果。连接语法与运行时的就是语义



## JS基本类型

### Number

IEEE 754 双精度浮点 [https://baike.baidu.com/item/IEEE%20754/3869922?fr=aladdin](https://baike.baidu.com/item/IEEE 754/3869922?fr=aladdin)

64位，第一位表示正负，2~12位表示指数位，其他位作为精度位，精度位乘以指数位，乘以 2 的指数次方的表示。

### String

字节码，编码等知识

### Null Undefined

Null为空，Undefined为未定义，void 0;也可以得到undefined，目前在函数内部依然可以修改`undefined`的值，注意风险。

### Object

继承，原型等知识

### Symbol

基本用作 Object 的属性，例子：可以通过`typeof JSON` 语句查看效果

### Boolean

基本作为 `true false`存在



