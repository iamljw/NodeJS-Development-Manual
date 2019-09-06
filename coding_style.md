# 代码风格
## eslint（强制）
统一规则
```json
{
    "extends": "eslint-config-egg",
    "rules": {
        "indent": ["error", 4, { "SwitchCase": 1 }],
        "comma-dangle": ["error", "never"],
        "array-bracket-spacing":["error", "never"],
    }
}
```
## 严格模式（强制）
在js文件开头必须声明使用严格模式 `'use strict';`
## 处理失败请求（强制）
采用异常抛出的方式，配合 [egg-error-handler](https://github.com/iamljw/egg-error-handler) 使用

```js
// app/service/demo.js
'use strict';

const { ParameterError } = require('tic-lib').clientError;
const { BaseService } = require('tic-lib').context;

class DemoService extends BaseService {
    // ...
    async show(id) {
        if (!id) {
            throw new ParameterError();
        }
    }
}

// 客户端响应数据如下
{
    code: 1001,
    success: false,
    message: '参数错误'
}
```
## 对象|数组 换行（推荐）
对象属性字段字符数超过 20 需换行，示例：
```js
const { ctx, service } = this;
const {
    ctx,
    service,
    app,
    bigAdd,
    bigMinus
} = this;
```
数组元素字符数超过 20 需换行，示例：
```js
const [ age, weight, height ] = user.body;
const data = [
    name,
    age,
    weight,
    height,
    birthday
];
```
## 应用生命周期管理（强制）
弃用暴露函数的方式，采用类方法来管理应用的生命周期：
```js
// app.js
'use strict';

// 弃用
module.exports = (app) => {
    app.beforeStart(async () => {
        // ...
    });
}

// 采用以下方式管理生命周期
class AppBootHook {
    constructor(app) {
        this.app = app;
    }

    // 插件启动完毕
    async willReady() {
        // ...
    }
}

module.exports = AppBootHook;
```
## 继承类（强制）
不允许直接使用 egg 提供的 Controller、Service 类
```js
// 错误写法✖
const { Controller } = require('egg');

class HomeController extends Controller {
    // ...
}
// 正确写法✔
const { BaseController } = require('../base_context_class');

class HomeController extends BaseController {
    // ...
}
```
该内容已经集成到 [泰链 NodeJS 开发者库](https://github.com/iamljw/tic-lib) 中。
## 任务调度(强制)
文件名固定格式写法：
- second.js: 每秒钟执行
- minute.js: 每分钟执行
- hour.js: 每小时执行
- daily.js: 每天0时0分0秒执行
- monthly.js: 每月1号0时0分0秒执行
- year.js: 每年1月1号0时0分0秒执行

*符合以上规则的任务，统一写在一个文件里。如果是单 work 进程的任务，在标准写法后面加 _work，例：daily_work.js*

时区设置(中国)
```js
cronOptions: {
    tz: 'Asia/Shanghai'
}
```
## 常量字典(强制)
所有常量均放在目录 `${baseDir}/app/constant` 下，并且采用二级属性对象写法进行分类，并标注说明：
```js
module.exports = {
    // 链类型
    chain: {
        ETH: 0,
        EOS: 1,
        BTC: 2,
        USDT: 3
    },
    // 积分操作类型
    integralOperateType: {
        RECHARGE: 'recharge', // 充币
        // ...
    }
};
```