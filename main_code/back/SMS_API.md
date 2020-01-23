# SMS_API


*Schedule Manage System*


- [约定](#约定)
- [前置条件](#前置条件)
- [注册登陆](#注册登陆)
- [总事务获取](#总事务获取)
- [操作事务](#操作事务)
- [操作每日任务](#操作每日任务)
- [错误码对照表](#错误码对照表)


## 约定:


事务->长期事务和短期事务

baseURL:`localhost:12210`


## 前置条件


除了登陆和注册,所有请求需要在`Header`中带上`token`



## 注册登陆


#### POST `/auth/register` 注册用户

Payload:
```json
{
    "password":"123456",
    "username":"test",
    "code":"hlkjlhaslid" //邀请码
}
```

Success(200):
```json
{
    "data": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InRlc3RlciIsImV4cCI6MTU4MDIxMTc0NywiaXNzIjoiU2NoX21hbiJ9.nloucu6Cx4W0Xg5r54Uf-G0gixrrpaUoWZAAAAAAAA"
    },
    "error": 0,
    "msg": "success"
}
```

#### Post `/auth/login` 用户登陆
Payload:
```json
{
	"password":"123456",
	"username":"test"
}
```

success(200):
```json
{
    "data": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InRlc3RlciIsImV4cCI6MTU4MDIxMTc0NywiaXNzIjoiU2NoX21hbiJ9.nloucu6Cx4W0Xg5r54Uf-G0gixrrpaUoWZGAAAAAAAA"
    },
    "error": 0,
    "msg": "success"
}
```


## 总事务获取 


#### GET `/all/affairs` 获取所有事务

Success(200)
```json
{
    "data": [
        {
            "id": 7,
            "title": "PHP留言板",
            "deadline": "1111-11-11 11:11:11",
            "extra": "",
            "created_at": "2019-10-20 13:26:50"
        },
        {
            "id": 8,
            "title": "英语课介绍用PPT",
            "deadline": "1111-11-11 11:11:11",
            "extra": "",
            "created_at": "2019-10-20 13:27:48"
        },
    ],
    "error": 0,
    "msg": "success"
}
```

#### GET `/all/dailyAffairs` 获取所有每日任务

Success(200)
```json
{
    "data": [
        {
            "ID": 9,
            "CreatedAt": "0001-01-01T00:00:00Z",
            "UpdatedAt": "0001-01-01T00:00:00Z",
            "DeletedAt": null,
            "Title": "英语单词打卡",
            "Extra": ""
        },
    ],
    "error": 0,
    "msg": "success"
}
```


## 操作事务


#### POST `/opera/add` 增

Payload:
```json
{
	"title":"test", //required
	"deadline":"2000-01-01T00:00:00Z",
	"extra":"extra"
}
```

Success(200):
```json
{
    "data": "",
    "error": 0,
    "msg": "success"
}
```

#### DELETE `/opera` 删

Query:

* `id` 事务编号

Success(200)
```json
{
    "data": "",
    "error": 0,
    "msg": "success"
}
```

#### PUT `/opera` 改

Query:

* `id` 事务编号

Payload:
```json
{
	"title":"test111", //required
	"deadline":"3000-01-01T00:00:00Z",
	"extra":"extra!!!"
}
```

Success(200)
```json
{
    "data": "",
    "error": 0,
    "msg": "success"
}
```


## 操作每日任务


#### POST `/operaDaily/add` 增

Payload:
```json
{
	"title":"test", //required
	"extra":"extra"
}
```

Success(200)
```json
{
    "data": "",
    "error": 0,
    "msg": "success"
}
```

#### DELETE `/operaDaily` 删

Query:

* `id` 每日任务编号

Success(200):
```json
{
    "data": "",
    "error": 0,
    "msg": "success"
}
```

#### PUT `/operaDaily` 改

Query:

* `id` 每日任务编号

```json
{
	"title":"test111", //required
	"extra":"extra!!!"
}
```

Success(200):
```json
{
    "data": 20000,
    "error": 0,
    "msg": "success"
}
```


## 获取随机背景图片

#### GET `/backgroundImage` 

```json
{
    "data": {
        "URL": "http://schmanimage.sweetbeecr.com/test3",
        "created_at": "2020-01-21T19:24:55+08:00"
    },
    "error": 0,
    "msg": "success"
}
```


## 错误码对照表


注:出现`500`错误,则一般是后端出错

|错误码对照表|含义|msg|
---|---|---|
|30200|token过期,需要重新登陆|`Token Expired`|
|30210|token格式更改,请重新登陆|`Token Format Changed`|
|40000|json格式错误|`Wrong Format Of JSON`|
|40010|Header错误|`Wrong Format Of Header`|
|40020|无效Token|`Wrong Format of Token`|
|40030|用户名重复|`Duplicate username`|
|40400|传入的参数无法解析|`Unable To Parse Parameters`|
|40410|用户名或者密码错误|`Username or Password Wrong`|
|40420|邀请码错误|`Invitation Code Wrong`|
|40430|要操作的事务不存在|`Not Found`|
|50000|合法数据无法插入数据库|`Can't Insert Into Database`|
|50010|生成token失败|`Can't Generate Token`|
|50020|中间件出错|`Middleware Wrong`|



