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







## 🫤@Test报错

<br>

<font size="5rem" color="#23a8f2">具体信息：</font>

Annotations are not allowed here 且只有Remove选项

<img src="👾BUG 日志记录.assets/image-20220305230529145.png" alt="image-20220305230529145" style="zoom:80%;" /> 

<br>

<font size="5rem" color="#3ed1b5">解决方法：</font>

只要你写完代码就行了😓（无语。。。。找了半天错误，结果就这🙃