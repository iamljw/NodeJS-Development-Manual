# 接口风格

整体上采用 [RESTful API](http://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html) 接口设计原则

## 协议(Protocol)
API与用户的通信协议，采用HTTP/HTTPS协议。
## 版本(Version)
统一将API的版本号放入URL。形如 `v1` 和 `v2` 这样的标识。
## 路径(Path)
基本组成：
![path](https://github.com/chyingp/nodejs-learning-guide/raw/master/assets/url.png)

pathname部分组成：/module_name/api/version/p  
*示例*：`/account/api/v1/login`

## 过滤(Filtering)
列表数据获取接口，过滤信息统一附加在 **query string** 上  
接口默认提供支持：
- page：页码, 默认值为1
- size：数目， 默认值为10
- order：排序方式，可选值：`asc` | `desc`，默认升序

其他参数看实际需求而定

## 响应体(Response Body)
统一以json数据格式返回：
```js
// 成功请求
{
    "code": 200, // 状态码
    "success": true, // 请求成功/失败标识
    "data": {}, // 实际返回的数据
    "extra": {} // 附加数据，可选
}
// 错误请求
{
    "code": 1001,
    "success": false,
    "message": "invalid params" // 错误信息
}
```
[查看状态码大全](./status_code.md)
