# Spring 表达式语言SpEl

## 基本表达式

1.字面量表达式    【 SpEL支持的字面量包括：字符串、数字类型（int、long、float、double）、布尔类型、null类型】

* 字符串 

```
ExpressionParser parser = new SpelExpressionParser();
String str1 = parser.parseExpression("'Hello World!'").getValue(String.class);
String str2 = parser.parseExpression("\"Hello World!\"").getValue(String.class);
```

* 数字

```
int int1 = parser.parseExpression("1").getValue(Integer.class);
long long1 = parser.parseExpression("-1L").getValue(long.class);
float float1 = parser.parseExpression("1.1").getValue(Float.class);
double double1 = parser.parseExpression("1.1E+2").getValue(double.class);
int hex1 = parser.parseExpression("0xa").getValue(Integer.class);
long hex2 = parser.parseExpression("0xaL").getValue(long.class);
```

* 布尔

```
boolean true1 = parser.parseExpression("true").getValue(boolean.class);
boolean false1 = parser.parseExpression("false").getValue(boolean.class);
```

* null

```
Object null1 = parser.parseExpression("null").getValue(Object.class);
```

2.算数运算表达式    【支持加\(+\)、减\(-\)、乘\(\*\)、除\(/\)、求余（%）、幂（^）运算】

3.关系表达式

4.逻辑表达式

5.字符串连接及截取表达式

6.三目运算及Elivis运算表达式

7.正则表达式

8.括号优先级表达式

## 类相关表达式

1. 类类型表达式
2. 类实例化

3. instanceof表达式

4. 变量定义及引用

5. 自定义函数

6. 赋值表达式

7. 对象属性存取及安全导航表达式

8. 对象方法调用

9. Bean引用

## 集合相关表达式

1. 内联List
2. 内联数组

3. 集合，字典元素访问

4. 列表，字典，数组元素修改

5. 集合投影

6. 集合选择

## 表达式模板



