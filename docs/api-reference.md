# 审核涉及接口对照说明

本文针对微信小游戏审核提到的 6 个标识符逐一说明：它们**全部来自官方 npm 包
`@tencent-ai/workbuddy-cloud-sdk@0.1.4`**（MIT 许可），是 SDK 内置的
「微信虚拟支付 / 广告结算 / 商户财务 / 账号回调」通用接口。

小游戏《好友猜猜乐》**未调用**其中任何虚拟支付、结算相关接口（游戏为纯免费玩法，
无内购、无广告变现），这些符号仅因打包了该 SDK 而存在于代码中。

下表给出每个标识符在源码中的位置与作用：

| 标识符 | 源码位置 | 所属模块 | 作用 |
|---|---|---|---|
| `downloadAdvertisingFundsOrder` | `lib/miniprogram.js` L441 | `WechatVirtualAdvertisingFundsAPI` 路由表 | 广告金结订单下载接口的云端路径常量 `/.cloud/wechat-virtual-advertising-funds/v1/orders/download` |
| `wechatVirtualAdvertisingFunds` | `lib/miniprogram.js` L494 | `WechatVirtualAdvertisingFundsAPI` | 微信虚拟支付·广告金结算 API 类的参数校验逻辑（如 `createFundsBill` 的 `transferAmount` 校验） |
| `resolveWechatVirtualPermission` | `lib/miniprogram.js` L164 | 虚拟支付权限工具函数 | 将 `permission-denied` 错误解析为结构化的权限缺失信息（分类 / 原因码 / 缺失 scope） |
| `handleWorkBuddyCallback` | `lib/chunk-VB3AB5XH.js` 等 | 账号模块 | WorkBuddy 账号 OAuth 登录回调处理（README「WorkBuddy 账号登录」章节有完整示例） |
| `isWechatVirtualReauthorizationRequired` | `lib/miniprogram.js` L176 | 虚拟支付权限工具函数 | 判断错误是否属于「需要重新授权」类别 |
| `downloadIOSSettlementBill` | `lib/miniprogram.js` L1132 | `WechatVirtualMerchantFinanceAPI` 路由表 | iOS 结算账单下载接口的云端路径常量 `/.cloud/wechat-virtual-merchant-finance/v1/ios-settlement-bills/download` |

## 与小游戏代码的关系说明

- 小游戏业务代码（`game/`、`utils/` 目录）仅调用 SDK 的：
  - `createMiniProgramWorkBuddyCloud` —— 创建云客户端；
  - `cloud.database.from(...).select/update/insert` —— 云数据库读写（房间、战绩、好友榜）；
  - `cloud.auth.signInWithWechat` —— 微信登录。
- 上述 6 个符号只存在于 SDK 打包产物
  `miniprogram_npm/@tencent-ai/workbuddy-cloud-sdk/miniprogram.js` 中，
  为 SDK 自带能力，游戏运行时不会触达。
- 可用 npm 官方 tarball 比对验证本仓库文件未被修改：
  <https://registry.npmjs.org/@tencent-ai/workbuddy-cloud-sdk/-/workbuddy-cloud-sdk-0.1.4.tgz>
