
## 介绍

​	D1 是g740团队为企业级的基础数据快速生成form table查询页面的Web应用。它支持MySQL、PostgreSQL、SQL Server、Oracle数据库，提供数据表快速查询、导出等功能。

## 问题
![preview](https://raw.githubusercontent.com/g740/D1/master/images/preview.png)

传统方式开发以上页面，需要解决以下问题：

- 需要展示的表是什么
- 表格展示的字段有哪些
- 表格展示的字段别名是什么
- 表格字段的列宽度是多少
- 表格字段的展示顺序
- 支持查询字段有哪些
- 支持查询字段类型是什么
- 表单字段是否可以精确或模糊查找
- 表单下拉框的以及默认值、选项值
- 表单类型的排版以及配置
- 导出的数据文件格式是什么
- 哪些字段支持导出
- 导出的数据字段宽度是多少
- 导出数据字段的别名是什么

如果有一款工具能快速解决上述问题，那将会大大提升工作的效率和用户体验。这时，D1应运而生。

## 目标
- 提供数据库快速动态查询
  在表或视图基础上建立Data Facet生成form 和 table 的默认配置，通过 form table配置信息进行动态查询

- 提供数据库动态查询结果可视化
  通过 form table配置（可显示的字段、字段别名、字段的位置、字段的列宽度）显示表格内容

- 提供数据库动态查询结果导出
  通过 form table配置（导出的字段、字段别名、字段导出长度、字段的位置）执行导出

- 提供多数据库类型支持
  支持MySQL、PostgreSQL、SQL Server、Oracle的可视化，目前仅支持MySQL

- 提供数据库查询、导出动态配置
  提供 form table setting配置页面由用户自定义查询、导出配置

- 支持多种页面Form元素（文本框，下拉框，日历，数值）

- 下拉框内容支持动态配置

- 支持自动收集下拉框内容

- 支持Form元素默认值配置

- 支持自动收集Form默认值

  ​


## 功能

1、构造基本Form + List/Table + Export页面。Admin Page通过D1 Core Functionality访问Biz Database，可以根据配置好的Data Facet Key对表或视图进行Preview。

2、对请求/返回进行再加工以满足高级要求，并将Hosting service的访问压力分摊到各Biz service。对于业务Page来说，API由各业务服务提供，各业务服务的实现依赖D1 Core Functionality将数据访问需求转换成可执行SQL，再由各业务服务自己发起DB查询，各业务服务有机会对执行查询前的内容和执行查询后的内容进行加工以满足特殊需求。

![jiagou](https://raw.githubusercontent.com/g740/D1/master/images/jiagou.png)



## 组织结构

```
d1
├── d1-core —— d1核心模块
├── d1-client —— 访问d1-core的客户端
├── d1-admin-page —— d1的管理页面
├── d1-vue-component —— 快速构建form table页面组件
├── d1-demo -- d1的使用演示
```



## 技术选型

### 前端








### 后台

| 技术            | 版本     | 说明        |
| ------------- | ------ | --------- |
| Spring Boot   | 2.0.3  | MVC核心框架   |
| Fastjson      | 1.2.30 | JSON处理    |
| Swagger       | 2.7.0  | Api文档框架   |
| Apache Poi    | 3.9    | excel框架   |
| Tomcat jdbc   | 8.5.23 | 数据库连接池    |
| Jsch          | 0.1.54 | ssh连接框架   |
| eureka-client | 2.0.3  | eureka客户端 |




## 部署

### 前端

#### 开发环境

| 工具   | 版本   |
| ---- | ---- |
| vue  | 2.3  |



####启动







### 后台
#### 开发环境

| 工具              | 版本          |
| --------------- | ----------- |
| jdk             | 1.8+        |
| mysql           | 5.7         |
| oracle 11g      | 11.2.0.1.0  |
| sql server 2017 | 14.0.3048.4 |
| postgresql      | 9.4.23      |

#### 启动

- 克隆代码到本地

  ```
  https://github.com/g740/d1.git
  ```

- 推荐使用idea，使用idea导入d1 maven项目

- 展开d1-core module，打开`bootstrap.properties`修改以下配置

  应用名、端口

  ```
  spring.application.name=d1-core
  server.port= 7400
  ```

  ​

  临时文件的路径

  ```
  file.temp.path=D:/dirTmp
  ```

  d1-core基础数据库支持（目前仅支持MySQL），不配置默认使用sqlite，docker实例重启会丢失，最好配置远程数据库

  ```
  ############  MYSQL   #########
  #数据库类型
  d1.basic.datasource.type=mysql
  #具体连接url，带schema或database
  d1.basic.datasource.url=jdbc:mysql://192.168.199.231:3306/d1_core?useSSL=false
  #数据库用户名
  d1.basic.datasource.user=root
  #数据库密码
  d1.basic.datasource.password=123456
  #是否使用ssl
  d1.basic.datasource.useSsl=false
  #是否使用ssh
  d1.basic.datasource.useSshTunnel=false
  d1.basic.datasource.sslCaFile=
  d1.basic.datasource.sslClientCertificateFile=
  d1.basic.datasource.sslClientKeyFile=
  #ssh主机地址
  d1.basic.datasource.sshProxyHost=192.168.199.231
  #ssh主机端口
  d1.basic.datasource.sshProxyPort=22
  #ssh用户名
  d1.basic.datasource.sshProxyUser=ubuntu
  #ssh监听的本地端口
  d1.basic.datasource.sshLocalPort=3307
  #ssh认证方式：key_pair(秘钥认证)、password（密码认证）
  d1.basic.datasource.sshAuthType=key_pair
  #ssh密码
  d1.basic.datasource.sshProxyPassword=1
  #ssh秘钥文件
  d1.basic.datasource.sshKeyFile=src/main/bin/ssh-key-file/id_rsa
  #ssh口令
  d1.basic.datasource.sshPassPhrase=123456
  ```
  运行`D1CoreApplication.java`  启动d1-core开始建表

  ![coreStart](https://raw.githubusercontent.com/g740/D1/master/images/coreStart.png)


  浏览器输入：http://localhost:7400/swagger-ui.html#访问swagger页面

  ![d1CoreSwagger](https://raw.githubusercontent.com/g740/D1/master/images/d1CoreSwagger.png)



 - 展开demo，在`pom.xml` 文件中添加d1-client依赖包

   ```
   <dependency>
       <groupId>ai.sparklabinc</groupId>
       <artifactId>d1-client</artifactId>
       <version>0.0.1-</version>
   </dependency>
   ```


   在yml或properties配置文件中加入配置

   ```
   #####临时文件路径#####
   file.temp.path=D:/dirTmp

   ```

   提供两个方式调用d1-core

   方式一：在配置文件中添加配置

   ```
   #d1-core url
   d1-core-service.url=http://localhost:8080
   ```

   方式二：调用的时候传d1-core的serviceId

   ```
   generalQuery(dataSourceKey,true,"d1-core", restructureParameter);
   ```

## 演示

###演示地址










###相关截图

![demo1](https://raw.githubusercontent.com/g740/D1/master/images/demo1.png)

![demo2](https://raw.githubusercontent.com/g740/D1/master/images/demo2.png)

![demo3](https://raw.githubusercontent.com/g740/D1/master/images/demo3.png)

![demo4](https://raw.githubusercontent.com/g740/D1/master/images/demo4.png)

![demo5](https://raw.githubusercontent.com/g740/D1/master/images/demo5.png)












## TODO

1、支持更多的数据库（Oracle、Postgresql、SQL Server、DB2），目前仅支持MySQL。

2、支持SSL连接、字典的收集与配置功能。





