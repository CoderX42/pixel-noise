# PixelNoise · 像素白噪音

> 像素风环境音 / 白噪音网页应用，**我的世界式方块 UI**，纯 **Web Audio API** 合成 + **Canvas** 粒子场景，无需任何外部音频文件。

[English summary](#english-summary) · [快速开始](#快速开始) · [功能](#功能) · [技术说明](#技术说明)

---

## 快速开始

1. 克隆或下载本仓库。
2. 用浏览器直接打开主页面（推荐）：
   - **[`index.html`](index.html)**（仓库根目录）— **正式单页应用**（混音、日夜主题、定时器、移动端优化等）。本地双击或用静态服务器打开即可。
   - 旧路径 [`ui/PixelNoise.html`](ui/PixelNoise.html) 仅作 **301 式跳转** 到根路径，便于书签迁移；**开发请以根目录 `index.html` 为准**。
3. 也可对比其他实验版本：`ui/Antigravity/ui-v5.html`、`ui-v6.html`、`ui/kimi/` 等。

> 若使用本地 `file://` 打开，部分浏览器对 `AudioContext` 策略较严，**首次播放需用户点击**；如遇异常，可用任意静态服务器托管目录后通过 `http://localhost` 访问。

---

## 功能

| 能力 | 说明 |
|------|------|
| **六种场景** | 雨声、森林、海浪、篝火、风雪、纯噪；声画对应，多层合成增强听感。 |
| **MIX 混音** | 可同时叠加最多 5 路场景（需开启 MIX 模式）。 |
| **日 / 夜主题** | 切换界面与画布氛围（含夜间星空等）。 |
| **定时停止** | 多档分钟定时，结束后自动暂停。 |
| **状态记忆** | `localStorage`（如 `pxn5_v3`）保存音量、场景、主题、混音等。 |
| **快捷键** | 空格播放/暂停；`1`–`6` 切换场景；`↑` `↓` 调节音量。 |
| **沉浸细节** | 像素溶解切换场景、点击画布涟漪、播放中中央大按钮延时淡出等。 |

---

## 技术说明

- **音频**：白噪 / 粉噪 / 棕噪、滤波器、LFO、短时 burst、啁啾振荡器等，全部在浏览器内实时生成。  
- **画面**：逻辑像素网格 + 约 30fps 绘制，场景装饰与粒子（雨、浪、火、雪、林、噪点等）。  
- **UI**：Silkscreen + VT323、方块描边与按压反馈、安全区与横竖屏布局。  

更完整的设计规范见 [`ui/Antigravity/design-spec-v2.md`](ui/Antigravity/design-spec-v2.md)。

**给 AI / 协作者的提示词（Markdown）：**

- [实现规格（页面与工程）](docs/prompts/implementation.md)
- [UI/UX 设计约束与动效](docs/prompts/ui-ux-design.md)

---

## 仓库结构（摘要）

```
PixelNoise/
├── docs/
│   └── prompts/              # 实现与 UI/UX 提示词
├── index.html                # 正式应用（GitHub Pages 根路径无 .html 后缀）
├── README.md                 # 本说明
├── CLAUDE.md                 # 面向 AI/协作的开发说明
├── frontend-design/          # 前端设计相关技能文档（含 LICENSE）
└── ui/
    ├── PixelNoise.html       # 跳转至根路径（旧链接兼容）
    ├── Antigravity/          # 设计稿与多版 UI 迭代
    └── kimi/                 # 其他实验分支
```

---

## GitHub 部署（GitHub Pages）

本仓库为**纯静态文件**，适合用 [GitHub Pages](https://pages.github.com/) 免费托管。

**线上地址（启用 Pages 后）：**  
[https://coderx42.github.io/pixel-noise/](https://coderx42.github.io/pixel-noise/)  
（用户名 `CoderX42`、仓库名 `pixel-noise` 时请与此一致；若不同请替换 URL。）

**在 GitHub 网页上开启步骤：**

1. 打开仓库 **[CoderX42/pixel-noise](https://github.com/CoderX42/pixel-noise)**。  
2. 进入 **Settings → Pages**（左侧菜单）。  
3. **Build and deployment** 里 **Source** 选 **Deploy from a branch**。  
4. **Branch** 选 **`main`**，文件夹选 **`/ (root)`**，点 **Save**。  
5. 等待约 1～2 分钟，页面顶部会出现绿色提示。

**访问地址（地址栏不会出现 `.html`）：**  
- 主页：`https://coderx42.github.io/pixel-noise/`  
  GitHub Pages 会把仓库根目录的 **`index.html`** 作为默认文档，因此 **无需** 写 `/index.html`。  
- 若仍打开旧链接 `.../ui/PixelNoise.html`，会自动跳转到上述根路径。

> **原理**：静态托管没有「隐藏后缀」的服务器重写；要实现无 `.html`，应使用 **`/` + `index.html`** 或 **`/某个目录/` + 该目录下的 `index.html`**（例如 `https://example.com/app/`）。

**首次把代码推送到该仓库（在本机项目目录执行）：**

```bash
git init
git add .
git commit -m "Initial commit: PixelNoise"
git branch -M main
git remote add origin https://github.com/CoderX42/pixel-noise.git
git push -u origin main
```

若远程已有提交，可先 `git pull origin main --rebase` 再 `git push`。推送需登录 GitHub（HTTPS 用 **Personal Access Token** 代替密码，或配置 **SSH**）。

---

## 浏览器与策略

- 推荐 **Chrome / Safari / Firefox** 等现代浏览器（支持 Web Audio 与 ES6+）。  
- 受浏览器**自动播放策略**限制，音频必须在**用户手势**（如点击播放）后启动，属正常行为。

---

## English summary

**PixelNoise** is a browser-based **pixel-art ambient / white-noise generator** with a **Minecraft-inspired block UI**. All sounds are **synthesized in real time** via the **Web Audio API** (no audio assets); the visuals use **Canvas** particles and retro-style animations. Open the repository root **`index.html`** (or the deployed site root URL) in a modern browser to run it.

---

## 致谢与许可

- 界面与动效参考方块建造类游戏的美学；字体来自 Google Fonts。  
- `frontend-design/` 目录内文件遵循其自带的 [LICENSE](frontend-design/LICENSE.txt)。  
- 主项目若未单独声明许可证，以仓库所有者后续添加的 `LICENSE` 为准。
