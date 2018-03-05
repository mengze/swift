# README
## 用户认证
### 参数类型
* 请求参数类型：`JSON`
* 响应数据类型：`JSON`

### 基础路径
根据部署环境决定

### 请求路径
```
/oauth/token
```

### 认证参数
```
// 密码认证方法如下：
{
    ”authType”:”phone”, 
    ”memberName”:”#登录用户名”,
    ”password”:”BASE64压缩登录密码”
}

// 手机认证方法如下：
{
    ”authType”:”phone”,
    ”memberName”:”#手机号”,
    ”password”:”#压缩动态码”
}
```


### 认证响应
**认证成功**

```
{
    "access_token":"#加密TOKEN信息",
    "token_type":"#认证方式",
    "refresh_token":"#刷新TOKEN",
    "expires_in":”#TOKEN有效期”
}
```

**认证失败**

```
{
    "error":"#异常关键字",
    "error_description":"#异常描述"
}

```

## 授权业务

### 请求路径
```
/business/{appModule}/{businessType}/{businessAction}
```
参数描述如下：

* `appModule`: 应用模块:
* `businessType`：业务接口
* `businessAction`：业务动作

### 请求头

```
Authorization: bearer {access_token}
```

### 请求参数
```
{
    "businessName":"#业务ID",
    "businessJsonParam":"#业务参数"
}
```

### 数据响应

**执行成功**

```
{
    "status":"#执行状态 true",
    "code":"#响应码 200"，
    "data":"#业务响应数据，json或null"
}
```

**执行异常**

```
// 用户token失效异常：
{
    "status":"#执行状态 false",
    "code":"#响应码 401"，
    "data":"#token异常信息"
}
// 业务接口执行异常：
{
    "status":"#执行状态 false",
    "code":"#响应码 200"，
    "data":"#业务异常信息"
}
```

## 开放业务
### 请求路径
```
/obs/{appModule}/{businessType}/{businessAction}
```

### 请求参数
```
{
    "businessName":"#业务ID",
    "businessJsonParam":"#业务参数"
}
```

### 数据响应
**执行成功**

```
{
    "status":"#执行状态 true",
    "code":"#响应码 200"，
    "data":"#业务响应数据，json或null"
}
```
**执行异常**

```
{
    "status":"#执行状态 false",
    "code":"#响应码 200"，
    "data":"#业务异常信息"
}
```


## 用户注销
### 请求路径

```
/oauth/revoke-token
```
### 请求头

```
Authorization: bearer {access_token}
```
### 请求参数
无

### 响应参数
无
