# 注释&文档
## 注释
- 文档注释，对某一文件作说明时使用
    ```js
    'use strict';

    /**
    * 文件描述xxx
    * @author: 刘建文
    * @email: lovedreamer7@163.com
    * @date: 2019-09-02 09:55:14
    */

    const os = require('os');

    class AccountService extends BaseService {
        // ...
    }

    module.exports = AccountService;
    ```
- 方法注释，对某一方法作说明时使用  
    Controller层：
    ```js
    /**
     * 用户的冻结资产
     */
    async frozenAsset() {
        // ...
    }
    ```
    Service层：
    ```js
    /**
     * 用户的冻结资产
     * @return {string} 冻结的资产
     * @param {int} uid 用户id
     * @param {int} chain 链
     * @param {string} symbol 币种
     */
    async frozenAsset(uid, chain, symbol) {
        // ...
    }
    ```
- 段落注释，对某一段代码作说明时使用
    ```js
    // ------------ 购买基金，同时调用积分模块扣除积分 ------------
    await service.fund.invest(uid, productId, amount);
    await service.integral.assetChange(uid, chain, symbol, amount, 'investFund');
    ```
- 行注释，对某一行作说明时使用
    ```js
    const countBonus = bigAdd(oldBonus, newBonus); // 计算奖金
    ```
## 文档
这里主要针对 *表设计* 和 *接口文档* 作统一的要求  
1. 表设计，写在 README.md 中（删除 README.zh-CN.md）
    ```md
    # 基金模块
    ## 表设计
    - aistatistics     AI量化产品统计
    - statistics       活期产品统计
    - daily_interest   每日计息
    - order            订单
    - ord_investment   投资订单
    - ord_ransom       赎回订单
    - ord_premium      保费订单
    - product          基金产品
    ```
2. 接口文档，在接口定义处备注说明
    ```js
    'use strict';

    /**
     * @param {Egg.Application} app - egg application
     */
    module.exports = app => {
        const { router, controller } = app;
        const apiV1 = router.namespace('/api/v1');
        router.get('/', controller.home.index);
        // ------------ 用户的冻结资产 ------------
        apiV1.get('/frozenAsset', controller.handler.frozenAsset);
        // ------------ 上传说明书 ------------
        apiV1.post('/upload/instructions', controller.handler.uploadInstructions);
        // ------------ 最新认购播报 ------------
        apiV1.get('/broadcast/:productId', controller.handler.broadcast);
        // ...
    };
    ```