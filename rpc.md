# 进程间通讯 RPC
## 插件
请直接参照 [egg-rpc4js](https://github.com/iamljw/egg-rpc4js)
## 约定
- 暴露的接口实现，全部放在 `${baseDir}/app/rpc` 文件夹下，命名为 `handler.js`，如下目录结构：
```js
egg-example
├── app
│   ├── controller // 普通接口实现目录
│   │   └── home.js
|   ├── rpc // RPC接口实现目录
|   |   └── handler.js
│   └── router.js
├── config
│   └── config.default.js
└── package.json
```
- 实现类写法
```js
// ${baseDir}/app/rpc/handler.js
'use strict';

class Handler {
    constructor(app) {
        this.app = app;
    }

    async getUser() {
        // ...
    }
    // ...
}

module.exports = Handler;
```
- 接口名  
统一采用：反转域名.模块名.模块名(首字母大写)Service，例：`cn.com.tichain.account.AccountService`
## 关于服务注册中心
目前在rpc实现中，支持 zookeeper 作为注册、发现服务器，供rpc内部实现代码使用。同时在每个服务启动时，应该在 consul 服务器上注册服务信息，供开发和维护人员查看。