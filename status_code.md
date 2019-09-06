# 状态码

对应响应体的 `code` 字段，特别的 1000、2000、3000 直接继承至 Error 类，并且作为其下的子类的继承类，
如其下子类不能满足业务需求，可直接使用父类根据业务需求进行扩展。

错误类已经全部集成到 tic-lib 中，[查看错误类源码](https://github.com/iamljw/tic-modules/tree/master/lib/errors)。

## 0 代表成功的请求
## 1xxx 客户端错误
- 1000: `ClientError` 客户端错误
- 1001: `ParameterError` 参数错误
- 1002: `UserNotFoundError` 用户不存在
- 1003: `InvalidPasswordError` 密码校验不通过 ()
- 1004: `LogonExpirationError` 登录过期
- 1005: `InsufficientBalanceError` 余额不足
- 1006: `InvalidRequestError` 无效的请求
## 2xxx 请求资源错误
- 2000: `ResourceError` 请求资源错误
- 2001: `NotFoundError` 找不到资源
- 2002: `PermissionDeniedError` 权限不足
- 2003: `LoginRequiredError` 需登录后访问
- 2004: `AccessDeniedError` 访问拒绝
- 2005: `RedirectError` 重定向
- 2006: `RequestTimeoutError` 请求超时
- 2007: `BanLoginError` 禁止登录
- 2008: `DataLoadingFailureError` 数据加载失败
## 3xxx 服务器错误
- 3000: `ServerError` 服务器错误
- 3001: `InternalError` 内部错误
- 3002: `ThirdPartyServicesError` 第三方服务异常
- 3003: `InternalServicesError` 内部服务异常
- 3004: `ServerMaintenanceError` 服务器更新、维护