[TOC]



## 流程梳理

1. 有请求参数和响应的返回值，把返回参数封装成一个 bean ，同时加 @RequestBody

2. Controller 里面，写一个 Handler 方法，返回值是 BaseRespVo ，前面加上 @RequestMapping ，方法传入的参数就是请求参数

   ```java
   	@RequestMapping("list")
       public BaseRespVo list(Integer page, Integer limit, String sort, String order) {
   ```

3. 写具体的业务逻辑，也就是返回值要得到具体的值，通过一个 Service 方法来获得一个具体的行为方法，里面传入的就是请求参数

   ```java
       ListData<User> listData = userService.queryList(page, limit, sort, order);
   ```

4. 那么，我们现在需要在这个 Controller 类的最上方连接一个 Service 方法的实例

   ```java
       @Autowired
       UserService userService;
   ```

5. 这时便可以创建一个 Service 接口及其实现，接着在里面创建上面的“具体的行为方法的接口”，在实现类里写具体逻辑。同时在 Service 接口的上方要加 @Service

   ```java
   public interface UserService {
       ListData<User> queryList(Integer page, Integer limit, String sort, String order);
   }
   ```

   ```java
       @Override
       public ListData<User> queryList(Integer page, Integer limit, String sort, String order) {
   
           return null;
       }
   ```

6. 由于 Service 相当于 数据层 到 控制层的一个中转，所以在这里也要 @Autowired 数据持久层的指挥官—— UserMapper 接口的一个实例，放在实现类下面（Mapper 接口之前已经用 Generator 生成好了）

   ```java
       @Autowired
       UserMapper userMapper;
   ```

7. 既然要使用 Mapper ，那么就要配置 MyBatis 了。配置方法是在这个项目的应用类（也就是上面加了 @SpringBootApplication 的那个类）下面加一个 @MapperScan 注解，表示我要扫描这个地方所有的 Mapper 了！之后改一下 pom.xml 里面的配置，MySQL 版本要用 5.1.47

   ```java
   @SpringBootApplication
   @MapperScan(basePackages = "com.rinchan.mapper")
   public class PremallApplication {
   ```

8. 之前对数据库进行操作，方法都是用 userMapper 来获得 UserMapper 接口的方法（这个方法具体的 sql 语句在对应的 UserMapper.xml 里面），但是现在，userMapper 指挥官有了新的工具人！那就是、当当当，userExample。现在的 UserMapper 接口里面放满了方法，这些方法传入的参数当然就是 userExample。
   所以，先 new 一个 userExample 出来，用它带的工具（方法），来处理一下传进来的请求参数。现在它是个成熟的 userExample 了，于是 userMapper 指挥官就可以把成熟的 userExample 传进自己的某一个方法里面了，这样就得到了响应给前端的返回值。

   ```java
           // page 页码
           // limit 当前页的大小
           PageHelper.startPage(page, limit);
   
           UserExample userExample = new UserExample();
           userExample.setOrderByClause(sort + " " + order);
   		// 因为下面这条是个查询语句，所以如果要使用分页插件，必须在它上面
           List<User> users = userMapper.selectByExample(userExample);
           ListData<User> listData = new ListData<>();
           listData.setItems(users);
           PageInfo<User> userPageInfo = new PageInfo<>(users);
           long total = userPageInfo.getTotal();
           listData.setTotal((int) total);
        return listData;
   ```
   
   

## 注意事项

1. 日期格式在 bean 类里设置，在需要格式化的那个成员变量头上加注解

   ```java
       @JsonFormat(pattern = "yyyy-mm-dd", timezone = "GMT+8")
       private Date birthday;
   ```

   

## 实用工具

### 1 分页插件 pageHelper

#### 1.1 引入依赖

pom.xml
pagehelper-spring-boot-starter

#### 1.2 配置语言（对应什么样的 sql 方言）

application.yml

```yml 
pagehelper:
  helper-dialect: mysql
```

#### 1.3 使用

service 层使用，在执行查询语句之前使用

## 大困惑（待解决）

#### json 解析 嵌套（系统管理-管理员）

## 小困惑（解决的）

### bo 和 vo

bo 就是返回参数里面，json 数据分组的组名

vo 就是页面上给展示出来的数据的列名

### map  和 list 怎么写

![image-20210109092342271](D:\myblog\rinchannow.github.io\_drafts\noteInProject2.assets\image-20210109092342271.png)

## 快捷键

shift + f6 改变所有成员变量名

ctrl + alt + shift + j

## Tricks

#### 一种不建议的测试方法

![image-20210109143746061](D:\myblog\rinchannow.github.io\_drafts\noteInProject2.assets\image-20210109143746061.png)

也可以给这个 json 字符串 封装成一个 TestBean , 主要是先让项目跑起来