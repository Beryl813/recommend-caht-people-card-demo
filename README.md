# HelloTalk 语伴推荐高保真交互 Demo

这是一个基于单个 HTML 文件实现的 HelloTalk 语伴推荐与聊天交互原型，适合用于产品演示、交互评审、视觉走查和 GitHub Pages 在线预览。

## 快速预览

无需安装依赖，也无需构建。

### 本地打开

直接双击 `index.html`，或在浏览器中打开该文件即可。

### 使用本地 HTTP 服务

```bash
python3 -m http.server 8080
```

然后访问 <http://localhost:8080>。

## 主要功能

- iPhone 风格设备外壳和动态岛展示
- 「为你推荐」横向卡片流
- 卡片横滑、鼠标拖拽和滚动吸附
- 未触达语伴的「打招呼」流程
- 已触达语伴的「继续聊天」流程
- 历史会话和纯净新建会话两种聊天状态
- 发送文本、贴纸、礼物等交互
- 聊天页返回推荐流后自动更新触达状态
- 点击头像或昵称进入语伴个人主页
- 个人主页的语言信息、动态、荣誉和关注状态展示
- 推荐策略切换：正常推荐卡片 / 卡片为空
- 推荐流下拉刷新交互
- 语言筛选和分类筛选交互
- 右侧 Demo 控制台，可快速跳转到关键状态

## Demo 控制台

桌面端页面右侧提供演示控制台，可以快速查看以下状态：

- 历史会话：Nemo
- 个人主页：Karl
- 纯净新建会话：Andrew
- 正常推荐卡片
- 卡片消失后的信息流状态

## 项目结构

```text
.
├── index.html   # 完整 Demo，包含 HTML、CSS、JavaScript 和内嵌图片资源
├── README.md    # 项目说明文档
├── LICENSE      # MIT License
└── .gitignore   # Git 忽略规则
```

## 技术说明

- 原生 HTML、CSS 和 JavaScript
- 零 npm 依赖
- 无需打包工具
- 贴纸、礼物图标和部分演示素材以内嵌 Base64 形式存放在 `index.html`
- 部分头像使用 Unsplash 远程图片地址，因此首次加载头像时需要网络连接
- Demo 没有后端服务，发送消息、筛选和状态变化仅保存在当前页面会话中

## 上传到 GitHub

在本目录执行：

```bash
git init
git add .
git commit -m "Add HelloTalk recommendation demo"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repository>.git
git push -u origin main
```

把 `<your-username>` 和 `<your-repository>` 替换成你的 GitHub 用户名和仓库名。

## 部署到 GitHub Pages

1. 打开 GitHub 仓库的 **Settings**。
2. 进入 **Pages**。
3. 在 **Build and deployment** 中选择 **Deploy from a branch**。
4. 分支选择 `main`，目录选择 `/ (root)`。
5. 点击 **Save**。

等待 GitHub 完成部署后，即可通过 Pages 地址访问 Demo。

## 兼容性

建议使用最新版 Chrome、Safari、Edge 或 Firefox。桌面端适合查看完整的设备外壳和 Demo 控制台，移动端适合体验页面内的滑动和触摸交互。

## 免责声明

本项目是用于产品原型和交互演示的前端 Demo，不包含真实账号、聊天服务、推荐算法或后端数据。项目中使用的品牌名称和视觉元素仅用于原型展示。

## License

本项目采用 MIT License，详见 [LICENSE](LICENSE)。
