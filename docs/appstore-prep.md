# App Store 上架准备（付费售卖）

## 一、开源协议结论

上游项目 [xatuke/openauthenticator](https://github.com/xatuke/openauthenticator) 采用 **MIT License**
（Copyright (c) 2026 Aayushman Choudhary，已通过 GitHub API 核实）。

**二次开发并在 App Store 收费售卖不违反 MIT 协议。** MIT 明确授予
use / copy / modify / merge / publish / distribute / sublicense / **sell** 的权利，且无 copyleft
（不要求开源你的修改）。唯一义务：

1. **在分发物中保留原版权声明和许可文本** —— 已放入仓库根目录 `ACKNOWLEDGMENTS.md`；
   上架版本建议在 App 内（如设置面板底部或"关于"里）加一个 Acknowledgments 入口展示它。
2. MIT **不授予商标/名称权**：`OpenAuthenticator` 这个名字不受协议保护，上架必须改名
   （商店要求名称唯一）。

## 一.5、品牌决定：AuthPop

已选定商用名称 **AuthPop**（备选：PopAuth、OtpPop —— 提交前在 App Store Connect /
微软 Partner Center 保留名称时如被占用则顺延备选）。Windows 版工程已直接以 AuthPop 命名。

macOS 端**已同步改名**（2026-07-04）：bundle id → `com.authpop.mac`，产物 →
`dist/AuthPop.app`，Keychain service → `com.authpop.accounts`，Raycast/构建/发布脚本
均已更新。改名副作用（需要用户手动处理一次）：

1. 辅助功能授权失效 → 系统设置里给 AuthPop 重新授权（首次 Enter 粘贴会自动弹引导）。
2. Keychain service 变更，旧账号不随迁 → 重新导入一次。
3. Raycast 命令 → 重跑 `./install-raycast-command.sh`。
4. 图标品牌可后续重做（现图标为本仓库自制 assets/，不属上游，可继续用）。

## 二、账号准备（你后面办）

- Apple Developer Program：99 USD/年，个人或公司主体均可收费售卖。
  公司主体需要 D-U-N-S 编号（免费申请，约 1-2 周）。
- 收款需在 App Store Connect 填税务与银行信息（大陆银行卡可收美元结算）。

## 三、技术改造清单（上架前必须做）

| # | 事项 | 说明 |
|---|------|------|
| 1 | **开启 App Sandbox** | App Store 硬性要求。entitlements 增加：`com.apple.security.app-sandbox`、`com.apple.security.files.user-selected.read-only`（文件导入）、`com.apple.security.device.camera`（扫码导入） |
| 2 | **1PUX 解压去掉 /usr/bin/unzip** | 沙盒内 spawn 外部进程不可靠，换成内置解压（如 ZIPFoundation 或 Compression framework） |
| 3 | **Enter 粘贴功能评估** | 合成 Cmd+V 依赖辅助功能授权，沙盒内技术上可行（Paste 等上架应用先例），但有审核风险；保留现有"未授权自动降级为复制"逻辑即可 |
| 4 | **签名切换** | 目前用本地自签/ad-hoc（build-oa.sh）。上架需回到 Xcode 工程（`xcodegen generate`），Team 换成你的开发者账号，Archive 后走 App Store Connect 分发 |
| 5 | **隐私材料** | `PrivacyInfo.xcprivacy`（声明不收集数据）、隐私政策 URL（必填，一页静态页即可）、相机用途描述（已在 Info.plist） |
| 6 | **版本与图标** | 1024px 商店图标已有（assets/AppIcon-1024.png）；CFBundleShortVersionString 规范化 |
| 7 | **⚠️ 清理仓库敏感文件** | `Sources/OpenAuthenticator/2026-06-30-145820-google-authenticator.txt` 疑似真实导出数据，务必移出仓库并确认未提交过 git 历史 |

## 四、上架流程（拿到账号后）

1. App Store Connect 新建 App（名称、Bundle ID、SKU、类目：工具/效率）。
2. 定价：直接选付费档位（如 ¥18 / $2.99），无需内购。
3. Xcode Archive → Distribute → App Store Connect 上传。
4. 填写截图（菜单栏 + 弹窗两组）、描述、关键词、隐私政策 URL、隐私问卷（"不收集数据"）。
5. 提交审核；备注里说明辅助功能权限用途（Enter 粘贴验证码），降低被拒概率。

## 五、Windows / 微软商店版

Windows 版是全新代码（Swift → C#/.NET，无法复用一行），属于**完全自研**，与上游 MIT
协议无任何牵连，收费上架微软商店无许可问题。TOTP 算法本身是公开标准（RFC 6238 / RFC 4226），
不构成对任何项目的派生。详见 `windows/` 目录及其 README。
