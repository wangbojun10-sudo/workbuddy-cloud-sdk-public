# WorkBuddy Cloud SDK（公共库登记）

本仓库是 npm 包 [`@tencent-ai/workbuddy-cloud-sdk`](https://www.npmjs.com/package/@tencent-ai/workbuddy-cloud-sdk) 的公共镜像，仅用于微信小游戏审核时登记「第三方公共库」用途。

- **来源**：npm 官方包 `@tencent-ai/workbuddy-cloud-sdk@0.1.4`（MIT 许可证）
- **原始 tarball**：<https://registry.npmjs.org/@tencent-ai/workbuddy-cloud-sdk/-/workbuddy-cloud-sdk-0.1.4.tgz>
- **许可证**：MIT（见 `LICENSE`，版权归原作者所有）
- **本仓库未做任何加密、混淆或修改**，所有文件原样来自 npm 发布包与该包的官方构建产物

## 用途说明

该 SDK 由腾讯 WorkBuddy 平台提供，用于在生成的应用中访问 WorkBuddy 云服务
（Auth / Database / Storage / LLM），属于通用基础库，**不含任何业务逻辑**。

小游戏《好友猜猜乐》（AppID: wxdbf41e467117bf9e）仅将其作为云数据库访问的
基础依赖使用，游戏全部玩法、界面与逻辑代码均为开发者原创。

## 目录结构

| 路径 | 说明 |
|---|---|
| `lib/` | npm 包原样源码（esbuild 产物，含模块注释，可读、非混淆） |
| `miniprogram_dist/miniprogram.js` | npm 包原样提供的微信小程序专用构建产物（压缩版） |
| `miniprogram_npm/@tencent-ai/workbuddy-cloud-sdk/miniprogram.js` | 小游戏包内实际引用的构建产物（未压缩 esbuild bundle，与上传包逐字节一致，含 421 行模块来源注释） |
| `docs/api-reference.md` | 审核提到的 6 个接口（downloadAdvertisingFundsOrder 等）的位置与作用对照说明 |
| `package.json` / `LICENSE` | npm 包 0.1.4 原样文件 |

## 验证方式

```bash
# 下载 npm 官方包并比对，可确认本仓库文件未被篡改
curl -O https://registry.npmjs.org/@tencent-ai/workbuddy-cloud-sdk/-/workbuddy-cloud-sdk-0.1.4.tgz
tar -xzf workbuddy-cloud-sdk-0.1.4.tgz
diff -r package/lib lib
```
