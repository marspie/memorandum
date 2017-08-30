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

* 加减乘除

```
int result1 = parser.parseExpression("1+2-3*4/2").getValue(Integer.class);//-3
int result11 = parser.parseExpression("4 div 3").getValue(Integer.class);//1  div等同 / 不区分大小写
```

* 求余

```
int result2 = parser.parseExpression("4%3").getValue(Integer.class);//1
int result22 = parser.parseExpression("4 MOD 3").getValue(Integer.class);//1 mod等同 % 不区分大小写
```

* 幂运算

```
int result3 = parser.parseExpression("2^3").getValue(Integer.class);//8
```

3.关系表达式

等于（==）、不等于\(!=\)、大于\(&gt;\)、大于等于\(&gt;=\)、小于\(&lt;\)、小于等于\(&lt;=\)，区间\(between\)运算

between 运算符右边操作数必须是列表类型,且只能包含2个元素。第一个元素为开始，第二个元素为结束，区间运算是包含边界值的,

同样提供了等价的“EQ” 、“NE”、 “GT”、“GE”、 “LT” 、“LE”来表示等于、不等于、大于、大于等于、小于、小于等于，不区分大小写.

```
boolean result = parser.parseExpression("1>2").getValue(boolean.class);//false
boolean result2 = parser.parseExpression("10 between {1, 20}").getValue(boolean.class);//true
boolean result3 = parser.parseExpression("10 eq 0").getValue(boolean.class);//false
```

4.逻辑表达式    【且（and）、或\(or\)、非\(!或NOT\)】

```
boolean result1 = parser.parseExpression("2>1 and (!true or !false)").getValue(boolean.class); //true
boolean result1 = parser.parseExpression("2>1 && (!true || !false)").getValue(boolean.class);//true
```

注：同样支持Java中的 && 和 \|\| 。

5.字符串连接及截取表达式

使用"+"进行字符串连接，使用"'String'\[index\]"来截取一个字符,"'world\[1\]'" 返回 o

```
String result1 = parser.parseExpression("'Hello ' + 'world'").getValue(String.class);
String result2 = parser.parseExpression("'Hello ' + 'world'[1]").getValue(String.class); //Hello o
```

6.三目运算及Elivis运算表达式

三目运算符 "表达式1?表达式2:表达式3"

```
boolean result1 = parser.parseExpression("2>1?true:false").getValue(boolean.class); //true
```

7.正则表达式

使用"string matches regex"

```
boolean result1 = parser.parseExpression("'123' matches '\\d{3}'").getValue(boolean.class); //true
```

8.括号优先级表达式

 使用"\(表达式\)"构造，括号里的具有高优先级。

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



