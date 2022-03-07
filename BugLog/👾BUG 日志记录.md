# 👾BUG 日志记录



<br>



## 🤯系统找不到指定的路径(properties)

<br>

<font size="5rem" color="#23a8f2">具体信息：</font>

java.io.FileNotFoundException: jdbc-demo\src\druid.properties (系统找不到指定的路径。)

<br>

<font size="5rem" color="#3ed1b5">解决方法：</font>

1. 首先通过 `System.getProperty("user.dir")` 获取当前所在项目的路径

   <img src="C:\Users\sarex\AppData\Roaming\Typora\typora-user-images\image-20220305225517379.png" alt="image-20220305225517379" style="zoom:80%;" /> 

2. 检查项目的路径有没有模块名，如果打印的路径有模块名，那么代码中就不需要模块名

   <img src="C:\Users\sarex\AppData\Roaming\Typora\typora-user-images\image-20220305225849110.png" alt="image-20220305225849110" style="zoom:80%;" />



成功排除bug

<img src="C:\Users\sarex\AppData\Roaming\Typora\typora-user-images\image-20220305230001153.png" alt="image-20220305230001153" style="zoom:80%;" />



<br>



## 🫤@Test报错

<br>

<font size="5rem" color="#23a8f2">具体信息：</font>

Annotations are not allowed here 且只有Remove选项

<img src="👾BUG 日志记录.assets/image-20220305230529145.png" alt="image-20220305230529145" style="zoom:80%;" /> 

<br>

<font size="5rem" color="#3ed1b5">解决方法：</font>

只要你写完代码就行了😓（无语。。。。找了半天错误，结果就这🙃



<br>



## 🐻pom.xml 没有 properties





<br>



## 😳serverTimezone未设置

<br>

<font color="skybule" size="5rem">具体信息：</font>

java.sql.SQLException: The server time zone value '�й���׼ʱ��' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.

![image-20220307172048526](👾BUG 日志记录.assets/image-20220307172048526.png)

<br>

<font size="5rem" color="#3ed1b5">解决方法：</font>

从控制台的报错信息可以得知，错误在没有设置 `serverTimezone`

在MySQL 8.X版本中需要传入时区信息，故需要在 `mybatis-config.xml` 配置文件中添加 `serverTimezone=Asia/Shanghai`

<img src="👾BUG 日志记录.assets/image-20220307172754136.png" alt="image-20220307172754136" style="zoom:80%;" /> 

>在XML中，直接使用一些符号会出差错，所以我们就会一些实体名称来代替

![image-20220307190054446](👾BUG 日志记录.assets/image-20220307190054446.png)



参考文章：

[serverTimezone错误](https://blog.csdn.net/weixin_44096353/article/details/118715116)

[对实体 "serverTimezone" 的引用必须以 ';' 分隔符结尾](https://www.bbsmax.com/A/VGzl4gg8zb/)