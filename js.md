# Javascript

## 'use strict';
## variables
- let
- var
- const 
    - 假如是直接字面值，变量命名就用全大写，单词间用下划线分割
    - 假如是需要计算，就跟骆驼方式

## data types

### primitive
- string
- number
- bigint
- boolean
- symbol
- null
- undefined
### types
- Number
    - Integer取值范围：-(2^53-1) ~ 2^53-1
    - Float
    - Infinity, -Infinity, NaN
        - NaN 与任何值都不相等，包括它自己
- BigInt
    - 数字后面加个n
- String
    - UTF-16编码的字符串
    - '' 、"" 、`` (可以使用变量名作占位, 类似其他语言的formatted string)
    - 获取string的某个字符
        - str.charAt(index), 超出范围的时候返回''
        - str[index], 超出范围的时候返回undefined
        - 可以用 for (let char of str)来遍历字符串的每个字符
    - 获取子串
        - substr   有可能在某些地方不支持
        - substring   假如传入的index为负数，会当0处理
        - slice  就用这个就好！！！

- Boolean
- Symbol
    - 创建一个symbol
        - let id = Symbol(key)，普通symbol
        - let id = Symbol.for(key), 全局symbol，有点类似单例的感觉，symbol还没有被创建的话，就创建，后面只返回这个实例， 可以了解下：Symbol.keyFor(symbol)
        - [System Symbol](https://tc39.es/ecma262/#sec-well-known-symbols)
    - 不会自动转换成String，都有description，就是key的字符串表达。
    - 可以用于与其他库区别定义property，就类似于namespace？
    - Object.keys()和for...in 枚举, 不会把symbol算进去，但是Object.assign(),却会把symbol和property一起复制，详见：“hiding symbolic properties” principle
- Object
    - properties
        - 增加property，直接声明就算添加了
        - 删除property，使用形如：delete object.property
        - 访问property，
            - .访问（要求property是一个有效的名字）
            - []访问（property名称在这里是string类型）
        - computed property， 跟[]有莫大关系，能动态生成property名称
        - property名称可以使用保留字，没任何限制，但类型只能是string或者symbol，假如不是这两种类型就类型转换成string
        - property顺序，key是纯数字，怎会按照数字顺序，不然就按照声明顺序
        - Optional chaining '?.'
            - object?.property/object?.["property"] (假如object为null/undefined，返回undefined，否则相当于object.property/object["property"])
            - object.method?.() (假如object.method为null/undefined，返回undefined，否则相当于object.method())
    
    - methods
        - this指针
            - arrow function用的上下文的this指针，它本身没有this指针
        - 定义方式
            - methodName: function(){}
            - methodName() {}
        - 构造函数、new操作符
            - 构造函数一般是首字母大写命名
            - 构造函数只能通过new运算符使用 eg: new User(name)
        
    
    - object copy
        - 浅拷贝 Object.assign()
        - 深拷贝

    - 垃圾回收机制
        - 引用计数算法，无法处理循环引用的情况。
        - 标记-清除算法，2012年之后所有浏览器都用了这个算法
            - 分代回收
            - 增量标记
            - 惰性清理
        - 记住这个：因为“有零引用的对象”总是不可获得的，但是相反却不一定，参考“循环引用”
    - Collection
        - Array
            - array本身实现了的函数基本可以让它成为 stack，queue，deque 这几种常用数据结构
            - 枚举元素时别用for...in，因为这样会把array的所有property都枚举，不单单会枚举元素，而且本身效率也很低
            - length=元素index最大值 + 1，而且可以直接被赋值，因此可以通过改变length，直接清理数组元素，array.length = 0
            - Don’t compare arrays with ==, 枚举元素来一一对比
            - methods   array的方法，基本都有thisArg,有些时候非常有用
                - splice
                - slice
                - find(fn)/findIndex(fn)
                - forEach(fn)
                - sort(fn)

        - Map、WeakMap
        - Set、WeakSet

- null
- undefined

### typeof operator
- 注意typeof null

### type conversion
- String()
- Number()
    - undefined --> NaN
    - null --> 0
    - true/false --> 1/0
    - string（转换前先去掉前后的空格）
        - length == 0 --> 0
        - length != 0
            - can not convert --> NaN
            - 对应的数字值
- Boolean()、!!(Double Not)
    - 0 --> false
    - null, undefine, NaN --> false
    - "" --> false
    - 其他值均为true
- 

### comparison
- 不同类型值比较 ，
所有值都先类型转换成number，再进行比较
    - 体会一下 "0" == 0 值为true
    - 严格相等（===）、严格不不相等（!==）, 比较时不做类型转换
    - null、undefined比较
        - null == undefined  (true)
        - null == otherValue (false)
        - undefined == otherValue (false)
        - 体会一下example: 
            alert( null > 0 );  // (1) false
            alert( null == 0 ); // (2) false
            alert( null >= 0 ); // (3) true
            alert( undefined > 0 ); // false (1)
            alert( undefined < 0 ); // false (2)
            alert( undefined == 0 ); // false (3)
        - 建议：比较值之前最好确定下是不是为null或者undefined，能避免一些陷阱

- Object.is()
    - Object.is(NaN, Nan) => true
    - Object.is(0, -0) => false
    - 除了上面这两个特例，其实Object.is(a, b)等价于a === b

## flow control
### 逻辑运算符
- || (返回第一个真运算的原始值，否则返回最后一个运算的原始值）
- && (返回第一个假运算的原始值，否则返回最后一个运算的原始值)
- !
- ?? (相当于(a !== null && a !== undefined) ? a : b)
    - 运算优先级相当低
    - 建议：都加上括号，以明确优先级，避免踩坑

### 条件执行
- if-else (对比下这个运算：a ? b : c)
- switch-case （使用的是 === ）

### 循环执行
- for，for...in
- while
- do...while

## function
- 函数表达式，需要在最后有个;
- arrow function

