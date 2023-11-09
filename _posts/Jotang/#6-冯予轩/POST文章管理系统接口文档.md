# POST文章管理系统接口文档

## 1. 用户管理

### 1.1 登录

#### 1.1.1 基本信息

> 请求路径：/users/login
>
> 请求方式：POST
>
> 接口描述：用户登录，成功后返回token加入其他请求的请求头



#### 1.1.2 请求参数

参数格式：application/json

参数说明：

|  参数名  |  类型  | 是否必须 |  备注  |
| :------: | :----: | :------: | :----: |
| username | String |    是    | 用户名 |
| password | String |    是    |  密码  |

请求参数样例：

```json
{
    "username":"ajuan",
    "password":"ajuan123"
}
```



#### 1.1.3 响应数据

参数格式：application/json

参数说明：

| 参数名 |  类型  | 是否必须 |             备注             |
| :----: | :----: | :------: | :--------------------------: |
|  code  | number |    是    | 响应码，1表示成功，0表示失败 |
|  msg   | String |    否    |           提示信息           |
|  data  | String |    是    |   相应的数据，即下发的jwt    |

响应数据样例：

```json
{
    "code": 1,
    "msg": "success",
    "data": "eyJhbGciOiJIUzI1NiJ9.eyJwYXNzd29yZCI6ImFiYWkxMjMiLCJsZXZlbCI6MSwidXNlcm5hbWUiOiJhYmFpIiwiZXhwIjoxNjk2NzA0ODg5fQ.TrlNq4fVfjIhgpNq6d2m3MQrS-UlTP3xrhalzsGJN1Y"
}
```

若用户名或密码错误：

```json
{
    "code": 0,
    "msg": "用户名或密码错误！",
    "data": null
}
```

#### 1.1.4 备注说明

用户登录成功后，系统会自动下发JWT令牌，然后在后续的每次请求中，都需要 在请求头header中携带到服务端，请求头的名称为 token，值为 登录时下发的 JWT令牌。 如果检测到用户未登录，则会返回如下固定错误信息：

```json
{
    "code": 0,
    "msg": "NOT_LOGIN",
    "data": null
}
```



### 1.2 注册（额外功能）

#### 1.2.1 基本信息

> 请求路径：/users/register
>
> 请求方式：POST
>
> 接口描述：用户注册



#### 1.2.2 请求参数

参数格式：application/json

参数说明：

|  参数名  |  类型  | 是否必须 |  备注  |
| :------: | :----: | :------: | :----: |
| username | String |    是    | 用户名 |
| password | String |    是    |  密码  |

请求参数样例：

```json
{
    "username":"test",
    "password":"test123"
}
```



#### 1.1.3 响应数据

参数格式：application/json

参数说明：

| 参数名 |  类型  | 是否必须 |             备注             |
| :----: | :----: | :------: | :--------------------------: |
|  code  | number |    是    | 响应码，1表示成功，0表示失败 |
|  msg   | String |    否    |           提示信息           |
|  data  | String |    是    |   相应的数据，即下发的jwt    |

响应数据样例：

```json
{
    "code": 1,
    "msg": "success",
    "data": null
}
```



### 1.3 查询所有用户(额外功能)

#### 1.3.1 基本信息

> 请求路径：/users
>
> 请求方式：GET
>
> 接口描述：用于查询所有用户的用户名和密码，仅管理员有权限



#### 1.3.2 请求参数

参数格式：queryString

请求参数样例：`/users`



#### 1.3.3 响应数据

参数格式：application/json

参数说明：

|  参数名  |   类型   | 是否必须 |                  备注                  |
| :------: | :------: | :------: | :------------------------------------: |
|   code   |  number  |    是    |      响应码，1表示成功，0表示失败      |
|   msg    |  String  |    否    |                提示信息                |
|   data   | Object[] |    是    |               相应的数据               |
|    id    |  number  |    是    |                   id                   |
|  level   |  number  |    是    | 用户权限，0表示管理，level越低权限越高 |
| username |  String  |    是    |                 用户名                 |
| password |  String  |    是    |                  密码                  |

响应数据样例：

以管理员账号登录：

```json
{
    "code": 1,
    "msg": "success",
    "data": [
        {
            "id": 1,
            "username": "admin",
            "password": "123456",
            "level": 0
        },
        {
            "id": 2,
            "username": "abai",
            "password": "abai123",
            "level": 1
        },
        {
            "id": 3,
            "username": "ajuan",
            "password": "ajuan123",
            "level": 2
        },
        {
            "id": 7,
            "username": "test",
            "password": "test123",
            "level": 2
        }
    ]
}
```

其他账号登录：

```json
{
    "code": 0,
    "msg": "权限不足！",
    "data": null
}
```



### 1.4 注销（额外功能）

#### 1.4.1 基本信息

> 请求路径：/users/{id}
>
> 请求方式：DELETE
>
> 接口描述：用户注销。管理员可随意注销账号，其他用户在正确登录的情况下可注销自己的账号



#### 1.4.2 请求参数

参数格式：路径参数

参数说明：

| 参数名 |  类型  | 是否必须 |    备注    |
| :----: | :----: | :------: | :--------: |
|   id   | number |    是    | 用户对应id |

请求参数样例：`/users/8`



#### 1.4.3 响应数据

参数格式：application/json

参数说明：

| 参数名 |  类型  | 是否必须 |             备注             |
| :----: | :----: | :------: | :--------------------------: |
|  code  | number |    是    | 响应码，1表示成功，0表示失败 |
|  msg   | String |    否    |           提示信息           |
|  data  | String |    否    |          返回的数据          |

响应数据样例：

正常注销：

```json
{
    "code": 1,
    "msg": "success",
    "data": null
}
```

请求的用户不存在：

```json
{
    "code": 0,
    "msg": "用户不存在！",
    "data": null
}
```

请求注销其他用户：

```json
{
    "code": 0,
    "msg": "权限不足！",
    "data": null
}
```



### 1.5 修改密码（额外功能）

#### 1.5.1 基本信息

> 请求路径：/users
>
> 请求方式：PUT
>
> 接口描述：用于修改用户的密码。管理员可直接修改密码，其他用户在正确登录的情况下可修改自己的密码



#### 1.5.2 请求参数

参数格式：application/json

参数说明：

|  参数名  |  类型  | 是否必须 |    备注    |
| :------: | :----: | :------: | :--------: |
| password | String |    是    | 修改的密码 |

请求参数样例：

```json
{
    "id":2,
    "password":"test111"
}
```



#### 1.5.3 响应数据

参数格式：application/json

参数说明：

| 参数名 |   类型   | 是否必须 |             备注             |
| :----: | :------: | :------: | :--------------------------: |
|  code  |  number  |    是    | 响应码，1表示成功，0表示失败 |
|  msg   |  String  |    否    |           提示信息           |
|  data  | Object[] |    否    |          相应的数据          |

响应数据样例：

```json
{
    "code": 1,
    "msg": "success",
    "data": null
}
```



## 2. 文章管理

### 2.1 查询文章

#### 2.1.1 基本信息

> 请求路径：/posts
>
> 请求方式：GET
>
> 接口描述：用于查询所有文章



#### 2.1.2 请求参数

参数格式：queryString

请求参数样例：`/posts`



#### 2.2.3 响应数据

参数格式：application/json

参数说明：

|  参数名  |   类型   | 是否必须 |                  备注                  |
| :------: | :------: | :------: | :------------------------------------: |
|   code   |  number  |    是    |      响应码，1表示成功，0表示失败      |
|   msg    |  String  |    否    |                提示信息                |
|   data   | Object[] |    是    |               相应的数据               |
|    id    |  number  |    是    |                   id                   |
|  level   |  number  |    是    | 用户权限，0表示管理，level越低权限越高 |
| username |  String  |    是    |                 用户名                 |
| password |  String  |    是    |                  密码                  |

响应数据样例：

以管理员账号登录：

```json
{
    "code": 1,
    "msg": "success",
    "data": [
        {
            "id": 6,
            "level": 2,
            "title": "test4",
            "author": "admin",
            "postContent": "this is test 4",
            "createTime": "2023-10-06T16:53:57",
            "updateTime": "2023-10-06T16:53:57"
        },
        {
            "id": 5,
            "level": 2,
            "title": "test3",
            "author": "admin",
            "postContent": "this is test 3",
            "createTime": "2023-10-06T16:53:50",
            "updateTime": "2023-10-06T16:53:50"
        },
        {
            "id": 4,
            "level": 2,
            "title": "test2",
            "author": "admin",
            "postContent": "this is test 2",
            "createTime": "2023-10-06T16:53:42",
            "updateTime": "2023-10-06T16:53:42"
        },
        {
            "id": 2,
            "level": 1,
            "title": "test1",
            "author": "admin",
            "postContent": "this is test 1",
            "createTime": "2023-10-06T16:53:06",
            "updateTime": "2023-10-06T16:53:06"
        },
        {
            "id": 1,
            "level": 1,
            "title": "test",
            "author": "admin",
            "postContent": "testtesttesttest",
            "createTime": "2023-10-02T16:55:05",
            "updateTime": "2023-10-02T16:55:08"
        }
    ]
}
```

阿摆账号（level为1）登录：

```json
{
    "code": 1,
    "msg": "success",
    "data": [
        {
            "id": 6,
            "level": 2,
            "title": "test4",
            "author": "admin",
            "postContent": "this is test 4",
            "createTime": "2023-10-06T16:53:57",
            "updateTime": "2023-10-06T16:53:57"
        },
        {
            "id": 5,
            "level": 2,
            "title": "test3",
            "author": "admin",
            "postContent": "this is test 3",
            "createTime": "2023-10-06T16:53:50",
            "updateTime": "2023-10-06T16:53:50"
        },
        {
            "id": 4,
            "level": 2,
            "title": "test2",
            "author": "admin",
            "postContent": "this is test 2",
            "createTime": "2023-10-06T16:53:42",
            "updateTime": "2023-10-06T16:53:42"
        },
        {
            "id": 2,
            "level": 1,
            "title": "test1",
            "author": "admin",
            "postContent": "this is test 1",
            "createTime": "2023-10-06T16:53:06",
            "updateTime": "2023-10-06T16:53:06"
        },
        {
            "id": 1,
            "level": 1,
            "title": "test",
            "author": "admin",
            "postContent": "testtesttesttest",
            "createTime": "2023-10-02T16:55:05",
            "updateTime": "2023-10-02T16:55:08"
        }
    ]
}
```

阿卷账号（level为2）登录：

```json
{
    "code": 1,
    "msg": "success",
    "data": [
        {
            "id": 6,
            "level": 2,
            "title": "test4",
            "author": "admin",
            "postContent": "this is test 4",
            "createTime": "2023-10-06T16:53:57",
            "updateTime": "2023-10-06T16:53:57"
        },
        {
            "id": 5,
            "level": 2,
            "title": "test3",
            "author": "admin",
            "postContent": "this is test 3",
            "createTime": "2023-10-06T16:53:50",
            "updateTime": "2023-10-06T16:53:50"
        },
        {
            "id": 4,
            "level": 2,
            "title": "test2",
            "author": "admin",
            "postContent": "this is test 2",
            "createTime": "2023-10-06T16:53:42",
            "updateTime": "2023-10-06T16:53:42"
        }
    ]
}
```



### 2.2 删除文章

#### 2.2.1 基本信息

> 请求路径：/posts/{ids}
>
> 请求方式：DELETE
>
> 接口描述：用于（批量）删除文章



#### 2.2.2 请求参数

参数格式：路径参数

参数说明：

| 参数名 |   类型    | 是否必须 |       备注       |
| :----: | :-------: | :------: | :--------------: |
|  ids   | 数组array |    是    | 要删除的文章的id |

请求参数样例：`/posts/1,2`



#### 2.2.3 响应数据

参数格式：application/json

参数说明：

| 参数名 |   类型   | 是否必须 |             备注             |
| :----: | :------: | :------: | :--------------------------: |
|  code  |  number  |    是    | 响应码，1表示成功，0表示失败 |
|  msg   |  String  |    否    |           提示信息           |
|  data  | Object[] |    是    |          相应的数据          |

响应数据样例：

```json
{
    "code": 1,
    "msg": "success",
    "data": null
}
```

#### 2.2.4 备注说明

在设计中，删除操作是基于查询所有文章的返回数据之上的，即用户无法看到权限高的文章，故未判断权限是否足够删除



### 2.3 添加文章

#### 2.3.1 基本信息

> 请求路径：/posts
>
> 请求方式：POST
>
> 接口描述：用于添加文章



#### 2.3.2 请求参数

参数格式：application/json

参数说明：

|   参数名    |  类型  | 是否必须 |   备注   |
| :---------: | :----: | :------: | :------: |
|    title    | String |    否    |   标题   |
|   author    | String |    否    |   作者   |
| postContent | String |    否    | 文章内容 |

请求参数样例：

```json
{
    "title":"test",
    "author":"admin",
    "postContent":"this is a test!"
}
```





#### 2.3.3 响应数据

参数格式：application/json

参数说明：

| 参数名 |   类型   | 是否必须 |             备注             |
| :----: | :------: | :------: | :--------------------------: |
|  code  |  number  |    是    | 响应码，1表示成功，0表示失败 |
|  msg   |  String  |    否    |           提示信息           |
|  data  | Object[] |    否    |          相应的数据          |

响应数据样例：

```json
{
    "code": 1,
    "msg": "success",
    "data": null
}
```

#### 

### 2.4 修改文章

#### 2.4.1 基本信息

> 请求路径：/posts
>
> 请求方式：PUT
>
> 接口描述：用于修改文章



#### 2.4.2 请求参数

参数格式：application/json

参数说明：

|   参数名    |  类型  | 是否必须 |   备注   |
| :---------: | :----: | :------: | :------: |
|     id      | number |    是    |    id    |
|    title    | String |    否    |   标题   |
|   author    | String |    否    |   作者   |
| postContent | String |    否    | 文章内容 |

请求参数样例：

```json
{
    "id":1,
    "title":"test",
    "author":"admin",
    "postContent":"this is a test!"
}
```





#### 2.3.3 响应数据

参数格式：application/json

参数说明：

| 参数名 |   类型   | 是否必须 |             备注             |
| :----: | :------: | :------: | :--------------------------: |
|  code  |  number  |    是    | 响应码，1表示成功，0表示失败 |
|  msg   |  String  |    否    |           提示信息           |
|  data  | Object[] |    否    |          相应的数据          |

响应数据样例：

```json
{
    "code": 1,
    "msg": "success",
    "data": null
}
```

#### 

#### 2.4.4 备注说明

基于文章查询的结果，选择修改某文章时，先调用根据id查询文章功能将文章作者、标题、内容返回给前端回显，前端作出修改后返回Post类型数据给后端处理，故请求数据中包含id项，只是该项不对用户显示。

同时，和删除功能一致，由于操作是基于查询所有文章的返回数据之上的，即用户无法看到权限高的文章，故未判断权限是否足够修改