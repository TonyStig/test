# API Server 说明文档 #


用于介绍API服务是如何设计和工作的。

> **使用框架:**
> - geth用于提供以太坊RPC服务
> - node.js (具体组件参阅package.json)
> - MySQL
> - forever组件或其他node管理组件
> - nginx或其他http服务器

## 初始化 ##

* 安装好MySQL后，使用config/panda.sql进行process_id的配置和表的建立。
* 使用npm install安装所需的node.js模块。

## 重要文件说明 ##

| 文件              | 功能         | 描述         |
|------------------|-------------|--------------|
| ApiServer.js     | 入口         | 用node或forever启动，然后将请求分发到各Processer |
| EthProcesser.js  | 处理器       | 将请求分发组具体处理业务的类或Util |
| DataProcesser.js | 处理器       | 专门用于数据库的相关操作，其他的类不应直接与数据库交互 |
| DatabaseUtil.js  | 数据库具体调用 | 数据库的相关操作的具体实现 |
| Web3Wallet.js    | 以太专具体调用 | 与以太坊相关操作的具体实现，通过geth的RPC服务实现 |
| ApiError.js      | 错误代码      | 错误处理应该标准化，新错误类型尽量添加到此文件 |

## 架构图 ##

> ApiServer (入口）
>> EthProcesser （以太处理器）
>>> Web3Wallet
>>>> geth RPC服务

>> DataProcesser （数据库处理器）
>>> DatabaseUtil
>>>> MySQL服务
