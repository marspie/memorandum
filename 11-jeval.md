# **Java数学表达式解析工具-Jeval**

下载[https://sourceforge.net/projects/jeval/files ](https://sourceforge.net/projects/jeval/files) 或Maven引入

```
<dependency>
    <groupId>net.sourceforge.jeval</groupId>
    <artifactId>jeval</artifactId>
    <version>0.9.4</version>
</dependency>
```

* #### 使用示例

```
package com.marspie.jeval;

import org.junit.Test;

import net.sourceforge.jeval.Evaluator;

public class JevalTest {

    @Test
    public void test1() {
        Evaluator evaluator = new Evaluator();
        //计算公式
        String exp = "#{a}-(#{b}-#{v})*(6*#{e}/100)+32";  
        try {
            /** * 添加变量到 Evaluator 类实例.  */  
            evaluator.putVariable("a", "33");  
            evaluator.putVariable("b", "10");  
            evaluator.putVariable("v", "10");  
            evaluator.putVariable("e", "5"); 
            //公式计算
            System.out.println(evaluator.evaluate(exp));  
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    @Test
    public void test2() {
        Evaluator evaluator = new Evaluator();
        try {
            System.out.println("1.-->" + evaluator.evaluate("1+2*3-2/1")); // 直接计算字符串型的数学表达式
            System.out.println("2.-->" + evaluator.evaluate("toUpperCase(trim( trim(' a b c ') ))")); // 执行java中的方法
            evaluator.putVariable("a", "'Hello'");// 定义字符串变量
            evaluator.putVariable("b", "'World'");
            evaluator.putVariable("c", "1"); // 定义数字变量
            evaluator.putVariable("d", "2");
            System.out.println("3.-->" + evaluator.evaluate("#{a}")); // 输出字符串
            System.out.println("4.-->" + evaluator.evaluate("#{b}"));
            System.out.println("5.-->" + evaluator.evaluate("#{PI}"));
            System.out.println("6.-->" + evaluator.evaluate("#{a} + ' ' + #{b} + '!'")); // 拼接后输出
            System.out.println("7.-->" + evaluator.evaluate("(#{c} + #{d}) - #{c}")); // 拼接后输出计算结果
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

# Spring 表达式语言之 SpEL

spring ExpressionParser 同样可以用于数学表达式的计算，Maven引入

```
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>4.3.0.RELEASE</version>
</dependency>
```

* #### 使用示例

```
import org.junit.Test;
import org.springframework.expression.Expression;
import org.springframework.expression.ExpressionParser;
import org.springframework.expression.spel.standard.SpelExpressionParser;
import org.springframework.expression.spel.support.StandardEvaluationContext;

public class ExpressionParserTest {

	@Test
	public void test1() {
		ExpressionParser parser = new SpelExpressionParser();
		// 解析表达式'Hello '+' World!'
		Expression exp = parser.parseExpression("'Hello '+' World!'");
		// 取出解析结果
		String result = exp.getValue().toString();
		// 输出结果
		System.out.println(result);
	}
	
	@Test
	public void test2() {
		ExpressionParser parser = new SpelExpressionParser();
		Double five = parser.parseExpression("1+2*3-2/1").getValue(Double.class); //直接计算字符串
		System.out.println(five);
		
		//定义数字变量
		StandardEvaluationContext context = new StandardEvaluationContext();
		context.setVariable("a", 1);
		context.setVariable("b", 2);
	 
		int result = (int) parser.parseExpression("#a+#b*3-2/2").getValue(context); 
		System.out.println(result);
	}
}
```



