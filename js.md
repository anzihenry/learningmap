# Javascript

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
- Boolean()
    - 0 --> false
    - null, undefine, NaN --> false
    - "" --> false
    - 其他值均为true

