# 命名规则

## 编码方面
1. 代码中的命名均不能以下划线或美元符号开头和结尾。
2. 私有属性一致使用 `Symbol` 符号来作为属性名，描述格式：类名 属性名。
3. 严禁使用英文和拼音混合。
4. 类名使用 UpperCamelCase 风格，方法名、参数名、变量使用 LowerCamelCase 风格。
5. 常量名全部大写，单词用下划线隔开，要求语义清晰。
6. 基类命名以 *Base* 开头，例：BaseController。
7. 对象的布尔类型属性命名统一格式 *isXXX*，值为 **0** 或 **1**。
8. JS文件名命名，字母小写，单词间以逗号分割。
9. 文件夹命名，字母小写，单词以 `-` 分割。
10. 模块命名
    - 普通模块：api-模块名，字母小写，单词以 `-` 分割。
    - 业务模块：项目名-模块名，字母小写，单词以 `-` 分割。
11. 在常量和变量的命名时，表示类型的名称放在词尾，以提升辨识度。
12. Controller/Service层方法命名规约
    - 获取单个对象的方法用 *get* 做前缀。
    - 获取多个对象的方法用 *list* 做前缀，复数形式结尾。
    - 获取统计值的方法用 *count* 做前缀。
    - 插入的方法用 *save*或*insert* 做前缀。
    - 删除的方法用 *remove*或*delete* 做前缀。
    - 更新的方法用 *update* 做前缀。
13. 领域模型命名规约
    - 数据对象：xxxDO，xxx为表名。例：`productDO`
    - 数据传输对象：xxxDTO，xxx为业务领域相关名称。例：`productListDTO`
    - 展示对象：xxxVO，xxx为界面/网页名称。例：`indexVO`
14. Controller、Service、Schedule 类命名，以文件名开头，UpperCamelCase风格：
    ```js
    // ${baseDir}app/controller/demo.js
    class DemoController extends BaseController {
        // ...
    }

    // ${baseDir}app/service/demo.js
    class DemoService extends BaseService {
        // ...
    }

    // ${baseDir}app/schedule/daily.js
    class DailySub extends Subscription {
        // ...
    }
    ```
## 数据库
1. 数据库名与模块名一致。
2. 表名字母小写，单词以下划线分割。
3. 当表较多时推荐使用分类，在表名前面加上分类名，例如充值订单表：ord_recharge。
4. 表字段使用 LowerCamelCase 风格，和Model对象属性保持一致。
5. 主键名统一使用 id。
6. 表示时间的字段，除了有明确时间语义的(如：birthday)，否则一律用 `At` 做后缀。例：*transferAt*。