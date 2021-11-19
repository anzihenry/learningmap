# Javascript

## 'use strict';
## variables
- let
- var
- const 
    - 假如是直接字面值，变量命名就用全大写，单词间用下划线分割
    - 假如是需要计算，就跟骆驼方式

## data types
### types
- Number
(Integer取值范围：-(2^53-1) ~ 2^53-1)
    - BigInt(数字后面加个n)
    - Infinity, -Infinity, NaN
- String
    - ''
    - ""
    - `` (可以使用变量名作占位, 类似其他语言的formatted string)
- Boolean
- Object
    - properties
    - ordered
- Symbol
- 特殊值
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
- for
- while
- do...while

## function
- 函数表达式，需要在最后有个;
- arrow function

