## **SQL获取分组后取某字段最大的一条记录**

    DROP TABLE IF EXISTS `test`;
    CREATE TABLE `test` (
      `id` INT(11) NOT NULL AUTO_INCREMENT,
      `name` VARCHAR(32) DEFAULT NULL,
      `course` VARCHAR(32) NOT NULL,
      `score` DECIMAL(10,0) NOT NULL,
      PRIMARY KEY (`id`)
    ) DEFAULT CHARSET=utf8;
    INSERT  INTO `test`(`id`,`name`,`course`,`score`) VALUES (1,'张三','语文',78),
    (2,'张三','数学',80),
    (3,'李四','语文',90),
    (4,'李四','数学',78),
    (5,'王五','语文',80),
    (6,'王五','数学',100);

* 获取各科成绩最高的记录：

方法一：\(效率最高\)

```
SELECT * FROM test AS a
WHERE score = (SELECT MAX(b.score)
FROM test AS b
WHERE a.course = b.course );
```

方法二：\(效率次之\)

```
SELECT
a.* FROM test a,
(SELECT course,MAX(score) score FROM test GROUP BY course) b
WHERE a.course = b.course AND a.score = b.score ORDER BY a.course;
```



