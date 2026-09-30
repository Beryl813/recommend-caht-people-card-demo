# HelloTalk 语伴推荐高保真交互原型 (HelloTalk Recommendation Demo)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](#)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)](#)
[![JavaScript](https://img.shields.io/badge/ES6+-F7DF1E?logo=javascript&logoColor=black)](#)
[![Zero Dependency](https://img.shields.io/badge/Dependencies-0-brightgreen.svg)](#)

这是一个面向 **HelloTalk 语伴发现与推荐流（Partner Recommendation Flow）** 的像素级、高保真前端交互原型。项目严格对齐产品需求文档（PRD）与真实 App 交互规范，完整复刻了 iPhone 15 Pro 外壳、推荐卡片状态机、多轮历史聊天承接、纯净新建会话、语伴个人主页等核心功能。

---

## 🌟 核心特性与设计规范

### 1. 推荐卡片触达状态机 (Reachability State Machine)
* **未触达态（初始状态，如 Andrew、Yuki）**：
  * 卡片按钮文案为 **「打招呼」**；
  * 按钮采用 HelloTalk 经典主按钮样式：品牌紫底白字；
  * **初次进入承接纯净空白**：点击「打招呼」进入后，承接**完全空白**的新建会话（不预置假数据、不预置贴纸、隐藏时间戳），符合真实 IM 的主动开场逻辑。
* **已触达态（成功发送消息后，如 Nemo、Karl）**：
  * 在会话页中成功打字发送第一条消息或互动后，系统自动记录该语伴为已触达；
  * 返回推荐流后，卡片按钮即刻更新为 **「继续聊天」**；
  * 按钮唯一定色锁定为 **薰衣草柔紫**（背景 `#f1edfe`、深紫文字 `#6c38f8`、微柔描边 `#dfd5fd`），低调优雅且具备高识别度。

### 2. 「为你推荐」横滑卡片流与像素级吸附 (Carousel Track)
* **16px 恒定留白几何对齐**：
  * 容器采用 `padding: 0 16px`、`scroll-padding: 0 16px` 与 `gap: 16px`；
  * 经过严格几何数学断言：卡片宽度 154px + 间距 16px = 170px 步长。当滑到任意一张卡片时，前序卡片恰好以 `0px` 移出视口，**左侧恒定保留 16px 纯净背景距离**，绝无卡片露边贴边瑕疵，与上下方信息流完美对齐；
* **强力逐张吸附 (`scroll-snap-stop: always`)**：
  * 横滑无论快慢均精准卡位，卡片居首吸附；
* **PC 端鼠标拖拽支持**：
  * 支持鼠标按住平滑拖拽横滑与松手惯性吸附，体验媲美真机触控。

### 3. 原生多轮会话流承接 (Native Chat Stream)
* **真实 IM 视觉对齐**：
  * 顶部导航栏展示语伴昵称、VIP 标示与返回操作；
  * 顶部规范加入居中浅灰时间戳（`今天 10:45`），避免消息突兀贴顶；
  * 对方文本气泡左侧配齐**圆形头像与国旗标识**，气泡保留原生微尖角（左上 4px，其余 18px）；
  * 点击对方头像支持无缝联动跳转至其个人主页；
* **智能悬浮下箭头**：
  * 默认隐藏，仅当用户向上翻看历史记录超过 120px 时智能淡出；点击可平滑回滚至最新消息并自动隐藏。

### 4. 极致纯净原则 (0 Toast Rule)
* 项目全局严格践行 **0 Toast 体验**，彻底清除了所有生硬突兀的黑色浮窗提示；
* 无论是点赞、送礼、关注、筛选还是切换语伴，全流程依靠界面状态本身的动效反馈，还原大厂应用自然高级的沉浸感。

### 5. 语伴个人主页 (Profile View)
* 真实高清头像与多语种背景信息墙；
* 动态点阵世界地图覆盖层；
* 语言能力双向评估仪表盘（母语流利度进度条 + 学习语言点阵量规）；
* 个人动态（Momentos）、荣誉勋章（Honra）与个人信息折叠卡片。

---

## 📐 状态流转一览表

| 场景 / 语伴状态 | 卡片按钮文案 | 按钮视觉样式 | 点击卡片按钮承接页面 | 会话中发送消息后表现 |
| :--- | :--- | :--- | :--- | :--- |
| **未曾互动过（如 Andrew）** | **打招呼** | 紫色高亮主按钮 | **纯净空白新建会话**<br>（0 贴纸/卡片，等待用户主动输入） | 卡片实时变更为「继续聊天」（薰衣草柔紫） |
| **原本已有互动（如 Nemo）** | **继续聊天** | continue-chat 态 / 薰衣草柔紫 | **多轮趣味历史会话流**<br>（含时间戳、萌牛表情包、四叶草礼物记录） | 消息实时追加至会话底部 |
| **兜底策略测试（无历史兜底）** | - | - | **推荐卡片直接消失**<br>（信息流无缝顶格，无多余留白） | - |

---

## 🛠️ 技术架构与设计考量

* **单文件即服务 (Single-file Zero-dependency)**：
  * 全部 HTML、CSS 与 JavaScript 均整合成单个独立文件 `index.html`；
  * 所有图标均采用内联矢量 SVG，所有头像与配图均转码为 Base64 格式内嵌，无需配置任何本地静态服务器或 CDN，离线即可 100% 运行。
* **高拟真 iPhone 15 Pro 仿真外壳**：
  * 精准实现 395px 宽度机身、50px 圆角、灵动岛（Dynamic Island）、状态栏时间与网络信号；
  * 提供自适应缩放机制，在不同分辨率屏幕下均能居中展示。
* **全功能调试控制台 (Demo Controls)**：
  * 界面右侧配备演示控制抽屉，支持一键直达「继续聊天」、「个人主页」、「打招呼」以及一键模拟策略切换。

---

## 🚀 快速上手与运行

### 方式一：本地直接运行
1. 克隆或下载本仓库代码：
   ```bash
   git clone https://github.com/your-username/hellotalk-recommendation-demo.git
   cd hellotalk-recommendation-demo
   ```
2. 双击打开 `index.html`，即可在 Chrome、Safari、Edge 等任意主流浏览器中直接交互体验。

### 方式二：本地简易 HTTP 服务（可选）
```bash
# 使用 Python 3
python3 -m http.server 8080

# 或使用 Node.js serve
npx serve .
```
然后在浏览器中访问 `http://localhost:8080` 即可。

### 方式三：免费部署至 GitHub Pages
1. 将代码推送至 GitHub 仓库；
2. 打开仓库页面，进入 **Settings** -> **Pages**；
3. 在 **Branch** 下选择 `main`（或 `master`），目录选择 `/ (root)`，点击 **Save**；
4. 稍等数秒即可通过生成的专属网址在线体验原型 Demo！

---

## 📁 目录结构

```text
.
├── README.md              # 项目详尽说明文档（即本文档）
├── index.html             # 高保真交互原型主程序（内嵌全部样式、脚本与媒体资源）
└── screenshots/           # 原型演示截图（可选展示用）
```

---

## 📄 开源许可证

本项目基于 [MIT 许可证](LICENSE) 开源。仅供学习交流与交互原型演示使用。
