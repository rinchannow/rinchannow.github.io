# 1 引言

之前的权限管理：filter interceptor

对每一个用户和每一个请求进行权限管理

# 2 权限管理的基础知识

系统 控制 用户 可以获得授权的 资源

两部分：用户认证、用户授权

## 2.1 用户认证

### 2.1.1 用户认证 authen

用户是否合法：是谁？身份是什么？

用户身份验证的常用方法：用户名密码方式、指纹、声纹

### 2.1.2 用户认证的流程

```flow
   st=>start: 访问系统的资源（某个菜单、链接、按钮、方法等）
   cond1=>condition: 是否允许匿名访问？
   cond2=>condition: 用户是否认证通过过？
   cond3=>condition: 是否认证通过？
   op1=>operation: 继续访问
   op2=>operation: 输入用户名和密码进行用户身份认证
   e=>end
   st->cond1
   cond1(no)->cond2
   cond1(yes)->op1->st
   cond2(no)->op2->e
   cond2(yes)->op1->st
   cond3(no)->op2
   cond3(yes)->op1
   


```

 