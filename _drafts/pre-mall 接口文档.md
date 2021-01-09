# 1 项目简介

这是一个商城项目，包含前台和后台两部分。

前台主要通过微信小程序和 Spring Boot 来实现，后台通过 Vue 和 Spring Boot 来实现。通过前后端分离，实现长城的功能。

```markdown
| 参数名 | 参数类型 | 是否必须 | 说明 |
| :----: | :------: | :------: | :--: |
|        |          |          |      |
```

接口说明

请求方式

url

请求参数

返回参数

## 1.1 后台业务模块

### 1.1.1 登录

#### 1.1.1.1 接口说明

Login：根据admin表中的数据查询admin信息
Logout：看完shiro部分之后再做

### 1.1.1.2 请求方式

POST

#### 1.1.1.3 url

/admin/auth/login

/admin/auth/logout

#### 1.1.1.4 请求参数

|  参数名  | 参数类型 | 是否必须 |  说明  |
| :------: | :------: | :------: | :----: |
| username |   str    |   yes    | 用户名 |
| password |   str    |   yes    |  密码  |

#### 1.1.1.5 返回参数

| 参数名 | 参数类型 | 是否必须 |         说明          |
| :----: | :------: | :------: | :-------------------: |
|  data  |  object  |   yes    |      返回的数据       |
| errmsg |   str    |   yes    |                       |
| errno  |   int    |   yes    | 返回错误码，0表示正常 |

```json
{
    "errno": 0,
    "data": "458a9a92-bfa8-40c6-ba7f-ba68ab1cba84",
    "errmsg": "成功"
}
```



### 1.1.2  首页

#### 1.1.2.1 接口说明

首页

/admin/dashboard

用户数量、商品数量、货品数量、订单数量的统计

### 1.1.3 用户管理

主要做的是条件查询

#### 1.1.3.1 会员管理

##### 1.1.3.1.1 请求方式

GET

##### 1.1.3.1.2 url

/admin/user/list

##### 1.1.3.1.3 请求参数

|     参数名      | 参数类型 | 是否必须 |      说明      |
| :-------------: | :------: | :------: | :------------: |
|      page       |   int    |   yes    |   分页的起点   |
|      limit      |   int    |   yes    |  每页显示数量  |
| sort（add_tim） |   str    |   yes    | 按添加时间顺序 |
|  order（desc）  |   str    |   yes    |      排序      |

##### 1.1.3.1.4 返回参数

```json
{
    "errno": 0,
    "data": {
        "total": 3,
        "items": [{
            "id": 1,
            "username": "test1",
            "password": "$2a$10$3joHPif3l/wsyKqxZA8aieZGQCWFcibfEtSJhAFLGovRPdtruDOuO",
            "gender": 0,
            "birthday": "2020-04-29",
            "lastLoginTime": "2020-04-27 20:15:47",
            "lastLoginIp": "",
            "userLevel": 0,
            "nickname": "测试用户",
            "mobile": "13554556544",
            "avatar": "https://wpimg.wallstcn.com/f778738c-e4f8-4870-b634-56703b4acafe.gif?imageView2/1/w/80/h/80",
            "weixinOpenid": "",
            "status": 0,
            "deleted": false
        }]
    },
    "errmsg": "成功"
}
```

#### 1.1.3.2 收货地址

##### 1.1.3.2.1 请求方式

GET

##### 1.1.3.2.2 url

/admin/address/list

##### 1.1.3.2.3 请求参数

|     参数名      | 参数类型 | 是否必须 |      说明      |
| :-------------: | :------: | :------: | :------------: |
|      page       |   int    |   yes    |   分页的起点   |
|      limit      |   int    |   yes    |  每页显示数量  |
| sort（add_tim） |   str    |   yes    | 按添加时间顺序 |
|  order（desc）  |   str    |   yes    |      排序      |

##### 1.1.3.2.3 返回参数

```json
{
    "errno": 0,
    "data": {
        "total": 10,
        "items": [{
            "area": "洪山区",
            "isDefault": false,
            "areaId": 1881,
            "address": "花山街道软件新城2期",
            "province": "湖北省",
            "city": "武汉市",
            "name": "刘师傅",
            "mobile": "18675730010",
            "id": 2,
            "cityId": 201,
            "userId": 3,
            "provinceId": 17
        }]
    },
    "errmsg": "成功"
}
```

#### 1.1.3.3 会员收藏

##### 1.1.3.3.1 请求方式

GET

##### 1.1.3.3.2 url

/admin/collect/list

##### 1.1.3.3.3 请求参数

|     参数名      | 参数类型 | 是否必须 |      说明      |
| :-------------: | :------: | :------: | :------------: |
|      page       |   int    |   yes    |   分页的起点   |
|      limit      |   int    |   yes    |  每页显示数量  |
| sort（add_tim） |   str    |   yes    | 按添加时间顺序 |
|  order（desc）  |   str    |   yes    |      排序      |

##### 1.1.3.3.4 请求参数

```json
{
    "errno": 0,
    "data": {
        "total": 11,
        "items": [{
            "id": 4,
            "userId": 3,
            "valueId": 1127047,
            "type": 0,
            "addTime": "2020-12-08 14:51:11",
            "updateTime": "2020-12-08 14:51:11",
            "deleted": false
        }]
    },
    "errmsg": "成功"
}
```

#### 1.1.3.4 会员足迹

##### 1.1.3.4.1 请求方式

GET

##### 1.1.3.4.2 url

/admin/footprint/list

##### 1.1.3.4.3 请求参数

|     参数名      | 参数类型 | 是否必须 |      说明      |
| :-------------: | :------: | :------: | :------------: |
|      page       |   int    |   yes    |   分页的起点   |
|      limit      |   int    |   yes    |  每页显示数量  |
| sort（add_tim） |   str    |   yes    | 按添加时间顺序 |
|  order（desc）  |   str    |   yes    |      排序      |

##### 1.1.3.4.4 请求参数

```json
{
    "errno": 0,
    "data": {
        "total": 970,
        "items": [{
            "id": 964,
            "userId": 1,
            "goodsId": 1181036,
            "addTime": "2020-12-11 18:25:04",
            "updateTime": "2020-12-11 18:25:04",
            "deleted": false
        }]
    },
    "errmsg": "成功"
}
```

#### 1.1.3.5 会员足迹

##### 1.1.3.5.1 请求方式

GET

##### 1.1.3.5.2 url

/admin/history/list

##### 1.1.3.5.3 请求参数

|     参数名      | 参数类型 | 是否必须 |      说明      |
| :-------------: | :------: | :------: | :------------: |
|      page       |   int    |   yes    |   分页的起点   |
|      limit      |   int    |   yes    |  每页显示数量  |
| sort（add_tim） |   str    |   yes    | 按添加时间顺序 |
|  order（desc）  |   str    |   yes    |      排序      |

##### 1.1.3.5.4 请求参数

```json
{
    "errno": 0,
    "data": {
        "total": 6,
        "items": [{
            "id": 2,
            "userId": 3,
            "keyword": "新品上市",
            "from": "wx",
            "addTime": "2020-12-08 11:33:02",
            "updateTime": "2020-12-08 11:33:02",
            "deleted": false
        }]
    },
    "errmsg": "成功"
}
```

#### 1.1.3.6 意见反馈

##### 1.1.3.6.1 请求方式

GET

##### 1.1.3.6.2 url

/admin/feedback/list

##### 1.1.3.6.3 请求参数

|     参数名      | 参数类型 | 是否必须 |      说明      |
| :-------------: | :------: | :------: | :------------: |
|      page       |   int    |   yes    |   分页的起点   |
|      limit      |   int    |   yes    |  每页显示数量  |
| sort（add_tim） |   str    |   yes    | 按添加时间顺序 |
|  order（desc）  |   str    |   yes    |      排序      |

##### 1.1.3.6.4 请求参数

```json
{
    "errno": 0,
    "data": {
        "total": 28,
        "items": [{
            "id": 9,
            "userId": 1,
            "username": "test1",
            "mobile": "13511111111",
            "feedType": "功能异常",
            "content": "13123",
            "status": 1,
            "hasPicture": false,
            "picUrls": [],
            "addTime": "2020-12-08 20:36:24",
            "updateTime": "2020-12-08 20:36:24",
            "deleted": false
        }]
    },
    "errmsg": "成功"
}
```

### 1.1.4 商场管理

#### 1.1.4.1 行政区域

/admin/region/list

GET

#### 1.1.4.2 品牌制造商

#### 1.1.4.3 商品类目

#### 1.1.4.4 订单管理

#### 1.1.4.5 通用问题

#### 1.1.4.6 关键词

### 1.1.5 商品管理

### 1.1.6 推广管理

### 1.1.7 系统管理（必做）

### 1.1.8 配置管理（必做）

### 1.1.9 统计报表