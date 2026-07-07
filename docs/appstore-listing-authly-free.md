# App Store 文案 — Authly (免费版 / Authly Authenticator)

商店记录：**Authly Authenticator** · bundle `com.authly.free` · macOS · 英语(美国) · 免费。
下面是可直接粘贴进 App Store Connect「1.0 准备提交」页的英文素材。

---

## 副标题 / Promotional Text（170 字符内）
> Fast, private 2FA codes right from your menu bar. Everything stays on your Mac — no account, no cloud, no tracking.

## 描述 / Description（4000 字符内）
```
Authly is a fast, private authenticator that lives in your menu bar. Click the icon, copy your code, done — no window to hunt for, no account to create, nothing sent to the cloud.

WHY AUTHLY
• Menu bar first — your 2FA codes are one click away, anytime.
• Private by design — secrets are stored only on your Mac, in the system Keychain. No account, no sync servers, no analytics, no tracking.
• Works offline — TOTP codes are generated entirely on-device (RFC 6238). No network required, ever.
• Passwords too — keep your logins alongside your codes and copy them just as quickly.

EASY IMPORT
• Scan a QR code with your camera.
• Import QR-code screenshots.
• Import a CSV exported from Apple Passwords, Chrome, or 1Password.
• Export your codes back out as standard otpauth QR images anytime — your data is never locked in.

SIMPLE & SECURE
• Standard TOTP (6/8-digit, 30s) compatible with Google, GitHub, Microsoft, and thousands of other services.
• Optional Touch ID / password lock before your codes are shown.
• Countdown ring so you always know how long a code is valid.

Authly does one thing well: get you your code, fast, without giving anything away.

Looking for a global hotkey popup, autofill, and paste-back? Those live in Authly Pop.
```

## 关键词 / Keywords（100 字符内，逗号分隔，不留空格更省字符）
```
2fa,authenticator,otp,totp,mfa,two factor,verification code,menu bar,password,security,login,offline
```
（当前 88 字符，OK）

## 技术支持网址 / Support URL
`https://<你的用户名>.github.io/<仓库>/`  （用下面的隐私政策同一个站点即可，或建一个简单 support 页）

## 营销网址 / Marketing URL（可不填）
留空即可，或填项目主页。

## 版权 / Copyright
`2026 He Liwei`

---

## 隐私政策 URL（必填）
把 `docs/privacy-policy.html` 发布到 GitHub Pages，得到形如：
`https://<用户名>.github.io/<仓库>/privacy-policy.html`

发布方法（最简单）：
1. 把本仓库 push 到 GitHub（public 或 private 皆可，Pages 对 private 需付费；用 public 最省事，但注意先删掉那个 google-authenticator.txt 敏感文件再 push）。
2. 仓库 Settings → Pages → Source 选 `main` 分支 `/docs` 目录 → Save。
3. 等 1–2 分钟，访问 `https://<用户名>.github.io/<仓库>/privacy-policy.html` 确认能打开。

---

## App 隐私问卷（App 隐私 面板）答案
- Data collection：**No, we do not collect data from this app.**（不收集任何数据）
- 因此不需要填任何数据类型。

## App 审核信息
- 需要登录：**取消勾选**（App 无需登录账号）。
- 备注给审核员（可选，降低被拒概率）：
  > Authly is a local, offline TOTP authenticator. All secrets are stored on-device in the Keychain; the app makes no network requests and collects no data. To test: click the menu bar icon, use the “+” / camera / import to add an account (or paste an otpauth:// URI), then click a row to copy the code.

## 出口合规（加密问卷）
App 使用的是标准 TOTP/HMAC（仅本机、标准算法）：
- “你的 App 是否使用加密？” → Yes（用了 HMAC-SHA1 等标准加密）。
- “是否符合豁免？” → 通常可选 **Yes, exempt**（仅用于认证、标准算法，符合 App Store 常见豁免；Info.plist 可加 `ITSAppUsesNonExemptEncryption=false` 一劳永逸）。
