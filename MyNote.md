# nginx

urlwrite 进行URL的编辑，实现真实URL的映射

动静分离

负载均衡

反向代理

以上 --> 网关服务器

防盗链--

nginx HTTPS原理及其配合NGINX实现

# Mybatis

1. 单个参数作为mybatis的入参时，不用考虑入参类型描述是什么并且单参，直接使用对象的字段即可，Map类型直接使用对应的Key值即可

2. 记得提交事务。

```java
SqlSessionFactoryBuilder->SqlSessionFactory->session->getMapper()->Method->session.commit()
```

3. XML文件编写的时候，可以在sql里面先测试一下 

4. 配置文件

   ![image-20220409163400646](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409163400646.png)

   1. settings
      1. 例如数据库字段名同Java实体类属性字段格式自动映射功能在\<settings>中配置![image-20220409163829296](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409163829296.png)
      2. 类型别名的实现方法\<typeAliases>![image-20220409164330101](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409164330101.png) 
      3. 不同环境下数据库设置![image-20220409171316028](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409171316028.png)
      4. 日志输出1.加依赖，2.配置参数![image-20220409172018922](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409172018922.png)
   2. Mappers标签的xml映射，建议将接口及其xml放在同一个包下：![image-20220409171610023](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409171610023.png)
   3. 获取参数的俩种方式#{} ${}。\$是一种拼接的过程，字符串需要控制单引号

5. 注解开发其实可用性不高

6. 动态SQL

   1. if \<if test="">  \</if> 这个test属性不需要加#{}  

   2. trim 包裹着sql语句段 prefixOverrides suffixOverrides  标签体内有内容，会动态添加指定内容。prefix suffix \<trim prefixOverrides>

   3. \<where>标签等效于如下\<trim>标签

      ```xml
      <trim prefix="where" prefixOverrides="and|or">
      </trim>
      ```

   4. \<set> 标签等效于如下\<trim>标签

      ```xml
      <trim prefix="set" suffixOverrides=",">
      </trim>
      ```

   5. \<foreach> 标签，动态遍历数组类型,数组默认是array，list集合默认是list，当然也可以使用@param标签指定参数名

      ```xml
      <foreach collection="" open="" close="" item="item" separator="">
      #{item}
      </foreach>
      ```

   6. \<choose> 选择进入类似于Java的switch case

      ```xml
      <choose>
      	<when test="">
        </when>
        <when test="">
        </when>
        <when test="">
        </when>
        
        <otherwise>
        </otherwise>
      </choose>
      ```

7. sql片段抽取，提高复用性，可维护性

   ```xml
   <sql id="" >
   重复sql片段
   </sql>
   
   <select> 
   <include refid=""/>
   </select>
   ```

8. resultMap结果集映射，使用的时候指定返回类型必须使用resultMap，

   1. 可以自动映射，在resultMapping开启自动映射 true，当然也可以指定为false

      ```xml
      <resultMap id="" type="" autoMapping="true">
      	<id column="" property=""></id> <!--主键 -->
        <result column="" property=""></result> <!--非主键 -->
      </resultMap>
      ```

   2. resultMap中存在继承功能

      ```xml
      <resultMap id="baseMap" type="" autoMapping="true">
      	<id column="" property=""></id> <!--主键 -->
        <result column="" property=""></result> <!--非主键 -->
      </resultMap>
      
      <resultMap id="myMap" type="" autoMapping="false">
      <!-- 写明自己特别或者额外的映射方式-->
        <result column="" property=""></result>
      </resultMap>
      ```

      ![image-20220409192413973](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409192413973.png)

9. 多表查询，解决结果集映射的问题。重难点

   1. 一对一查询

      1. 利用resultMap: ![image-20220409192413973](/Users/lushixiang/CodingSpace/Git/Github.com/xiaoluxiang.github.io/MyNote.assets/image-20220409192413973.png)

          ![image-20220409192059051](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409192059051.png)

      2. 利用\<association>标签![image-20220409193007220](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409193007220.png)

   2. 一对多查询

      1. 对于同一个主键，mybatis会自动识别
      2. 使用collection标签自动封装查询结果集![image-20220409194122231](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409194122231.png)

   3. 分步查询，将各步的接口及其xml语句实现，然后在xml配置俩者关联起来。column="{}"

      1. ![image-20220409200029445](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409200029445.png)
      2. ![image-20220409200054363](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409200054363.png)

   4. 按需查询

      ![image-20220409200443202](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409200443202.png)

10. 分页查询，引入依赖，在mybatis的配置文件中引入该依赖的插件，分页查询返回前端除查询结果其他的分页信息，包括总记录数。其他他就是在后面加了limit

    1. ![image-20220409201757500](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220409201757500.png)

    2. 配置分页信息，在他的返回值传入PageInfo中即可获得对于的分页信息

       ```java
       PageHelper.startPage(1,1);
       // 查询获得结果
       // 传入pageInfo获得相关信息
       PageInfo pageInfo = new PageInfo<>();
       sout(pageInfo.getTotal());
       sout(pageInfo.getPages());
       sout(pageInfo.getPageNum());
       sout(pageInfo.getPageSize());
       ```

    3. 分页查询存在的问题，一对多的过程中，mybatis无法处理，故采用分布查询。

# Mysql优化

1. 索引是

2. Hash索引为什么使用的越来越少 

3. 为什么建议INNODB必须建主键，并且推荐使用整形的自增主键
4. 推荐使用联合索引
5. 最左前缀原则及其底层设计原理
6. 学会使用EXPLANIN
7. MVCC 
8. B+树和B树区别
9. BufferPool

## 尚硅谷

1. 存储过程于存储函数
   1. 

# Linux

1. 文件系统

# 函数式编程

1. 

# MYSQL 高级篇-尚硅谷

## 索引

1. B+树，树的深度决定了按照索引查找的IO加载次数，三层就是亿级。四层就是千亿级
2. 聚集索引，索引即数据，数据即索引。InnoDB，MyISAM







# Gateway

1. API网关
2. 请求参数（query，body，header）
3. 配置文件过滤器
   - 过滤器使用，-filter， 然后-name指定过滤器，-args指定对于参数  
   - 请求路径过滤
   - 路径过滤
   - key value 过滤
   - 所有过滤器，得调用继续向下过滤的方法
4. 限流
   1. 计数，单位时间内设定阈值
   2. 漏桶算法，设定存储清楚容器（栈，队列，堆），不超出容量即可正常有序取出处理
   3. 令牌桶算法，针对客户端进行限制，限 制最大同时可访问次数。搭配redis 
5. 自定义代码过滤器



# Spring

1. stopWatch 
2. unsafe 
3. 如何getSpringFactoriesInstances
4. PropertySource

# IO多路复用

![image-20220424105904103](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/image-20220424105904103.png)



Spring Boot自动配置的原理

Spring Boot启动会通过扫描注解，其中EnableAutoConfigruation会自动去Maven中的各个start下的spring.factories文件。这些文件中写明了各start所需注入的bean

@SpringBootApplication注解包含@SpringBootConfiguration，@EnableConfiguration，@ComponentScan

@ComponentScan注解是有点意思的，value（basePackages）分析注解即为接口，默认实现与默认返回，以便深入理解注解工作原理



Java的spi服务发现机制：resources/META_INFO.services/FullInterfaceName。文件里存放所有的实现类的全限定名称

SpringBoot的自动加载机制：通过启动类上@EnableAutoConfiguration注解配置，自动加载Maven中所有starter下的spring.factories文件内容



spring 配置文件种类&配置文件优先级

> [参考文章](https://juejin.cn/post/7113920258016018439)

```txt
命令行参数
JVM系统参数
系统环境参数
jar包外部application-{profile}.properties/yml
jar包内部的application-{profile}.properties/yml
jar包外部的application.properties/yml

项目根目录下的/config目录下的配置文件。
项目根目录下的配置文件。
项目类路径（resources）下的/config目录下的配置文件。
项目类路径（resources）下的配置文件。

项目根目录下的配置文件或者/config目录下的配置文件在打包的时候不会被打入jar包中，因此一般很少用到

bootstrap配置文件由spring父上下文加载，并且比application配置文件优先加载（父上下文不会使用application配置文件），而application配置文件由子上下文加载。bootstrap加载的配置信息不能被application的相同配置覆盖。

但是注意，如果要使用配置文件中的变量，那么同名变量将使用application文件中的配置，因为在Environment中，application配置文件的propertySource排在bootstrap配置文件的propertySource之前，Spring 在进行属性注入、获取时，将会顺序遍历所有的propertySource查找属性，如果找到了就直接返回。.peoperties文件比.yaml文件的属性查找优先级更高的原理一样。
```



# 术语

日切，通俗的来说就是进行日期切换，更换系统记账的时间。日切过程中如果交易可以照常提交并正确处理返回，就说系统支持7*24小时不间断服务



# 话术

谈谈对XX的看法：先描述XX的定义，XX的功能/特点。描述业务场景，场景下的瓶颈，XX的解决方案。

# Batch

集群任务：数据划分，数据处理，任务调度。数据划分可以不同维度，key+start+offset，多次划分。数据处理可对应着read（可通过标志位循环read），process，write三大逻辑。本机调度：自定义完成处理流程，一次打满全场。也可以跨机调用（自定义rpc远程调用）











# remember

网络：架构->协议->认证->安全

设计原则&设计模式：7+24。生产（单例）->结构->行为

数据结构：数组->链表->栈->队列->树->图

算法：分治二分->贪心->动态->回溯



盈通的大地之神功耗高

迅景残血版黑狼版功耗比较高（散热差）



蓝宝石全系列都可以买，看供电口认识版本

迪兰：恶魔>战神（散热差）>战将

讯景：水很深，组装卡很多

华硕：散热差

微星：无显存散热

华擎：全系可购买

铭瑄：型号多，值得购买，需要和官网做下对比

盈通：全系可购买

| 店铺 | 型号 | 价格 | 质保 |
| ---- | ---- | ---- | ---- |
|      |      |      |      |

