# **Springboot 使用问题**

1. **不连接数据库报错**

```
***************************
APPLICATION FAILED TO START
***************************

Description:

Cannot determine embedded database driver class for database type NONE
```

原因是：springboot启动时会自动注入数据源和配置jpa

解决：在@SpringBootApplication中排除其注入

```
@SpringBootApplication(exclude={DataSourceAutoConfiguration.class,HibernateJpaAutoConfiguration.class})
```



