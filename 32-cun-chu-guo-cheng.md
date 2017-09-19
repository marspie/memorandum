# Mysql存储过程创建使用

**什么是存储过程**

就是一组SQL语句集，功能强大，可以实现一些比较复杂的逻辑功能，类似于JAVA语言中的方法；

存储过程跟触发器有点类似，都是一组SQL集，但是存储过程是主动调用的，且功能比触发器更加强大，触发器是某件事触发后自动调用；

**特性**

有输入输出参数，可以声明变量，有if/else, case,while等控制语句，通过编写存储过程，可以实现复杂的逻辑功能；

函数的普遍特性：模块化，封装，代码复用；

速度快，只有首次执行需经过编译和优化步骤，后续被调用可以直接执行，省去以上步骤；

**创建存储过程**

存储过程proc\_add功能很简单，两个整型输入参数a和b，一个整型输出参数sum，功能就是计算输入参数a和b的结果，赋值给输出参数sum；

    DROP PROCEDURE IF EXISTS `proc_add`;
    DELIMITER ;;
    CREATE DEFINER=`root`@`localhost` PROCEDURE `proc_add`(IN a INT, IN b INT, OUT SUM INT)
    BEGIN
        #Routine body goes here...

        DECLARE c INT;
        IF a IS NULL THEN SET a = 0; 
        END IF;

        IF b IS NULL THEN SET b = 0;
        END IF;

        SET SUM  = a + b;
    END
    ;;
    DELIMITER ;

_调用_

```
SET @b=5;
CALL proc_add(2,@b,@s);
SELECT @s AS SUM;
```

_不带参存储过程_

    DROP PROCEDURE IF EXISTS `pro_query`;
    DELIMITER ;;
    CREATE DEFINER=`root`@`%` PROCEDURE `pro_query`()
    BEGIN
    	#Routine body goes here...
    	SELECT 1;

    END;;

    DELIMITER ;     

调用

```
CALL pro_query()
```



