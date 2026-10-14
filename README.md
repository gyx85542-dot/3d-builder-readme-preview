<p align="center">
  <img src="logo.png" alt="Topview 3D Builder" width="120" />
</p>

<h1 align="center">Topview 3D Builder</h1>

<p align="center"><b>先搭好场景，再让 AI 来拍。</b><br/>Block it in 3D. Let AI shoot it.</p>

<p align="center">
  让 AI 视频里的人物站位、镜头角度、空间关系，从"抽卡"变成"导演说了算"。<br/>
  从一个想法，到 3D 场景，再到真实的动画视频，全流程一站打通。免费、本地运行、无需注册。
</p>

---

https://github.com/user-attachments/assets/5b07a0d4-d3cc-48c0-aebf-31e2232d90de

<p align="center"><sub>↑ 在 Studio 里搭场景、摆机位、拉运镜，再到成片，一气呵成</sub></p>

## 🚀 快速上手

### 第 1 步：安装插件

选择你正在用的 AI 工具。需要 Python 3.11+、Node.js 20.6+，以及 [uv](https://docs.astral.sh/uv/) 或 pipx（任选其一）。

ChatGPT / Codex · Cursor · Claude Code

#### ChatGPT / Codex

ChatGPT 桌面端与 Codex 共用同一份配置，装一次即可，安装后重启应用。

```bash
codex plugin marketplace add https://github.com/topviewai/topview-3d-builder.git --ref main
codex plugin add topview-3d-builder@topview-3d-builder
```

#### Cursor

```bash
git clone https://github.com/topviewai/topview-3d-builder.git ~/.cursor/plugins/local/topview-3d-builder
```

重启 Cursor 生效。

#### Claude Code

```bash
claude plugin marketplace add https://github.com/topviewai/topview-3d-builder.git
claude plugin install topview-3d-builder@topview-3d-builder
```

安装后重启 Claude Code。

<details>
<summary>其他支持 Skills 的工具</summary>

```bash
npx skills add https://github.com/topviewai/topview-3d-builder.git
```

然后选择 `topview-3d-cli`。

</details>

> 首次渲染会自动下载一次渲染所需的浏览器组件（约几百 MB），之后无需重复下载。
> 更新、卸载、手动安装 CLI 等进阶操作，请见 [开发者与进阶文档](DEVELOPER.md)。

### 第 2 步：开一个新会话，直接说你想要的场景

> "搭一个场景：一个角色坐在盒子旁边，渲染一张正面视角。"

### 第 3 步：查看场景，继续调整

需要调整就继续说，或者打开 Studio 手动微调。满意之后，以这个 3D 场景为依据，输出真实质感的动画视频。

## 你是不是也遇到过这些问题？

用 AI 生成视频，最让创作者崩溃的往往不是画质，而是**"它根本不听我的"**：

| 创作者的痛点 | 具体表现 |
| --- | --- |
| 😵 **站位全靠猜** | 想要"两人面对面坐在桌子两侧"，生成出来却是并排、穿模、或者桌子消失了 |
| 🎰 **镜头像抽卡** | 反打、过肩、俯拍……提示词写了一大段，AI 只给你一个随机角度 |
| 🔁 **改一点，全盘重来** | 只想让角色往左挪半步，重新生成后，人物、场景、构图全变了 |
| 💸 **试错成本高** | 每次生成都在烧积分和时间，一个镜头抽十几次才勉强能用 |
| 🧩 **多镜头对不上** | 同一场戏的几个镜头里，人物位置和空间关系前后矛盾，剪不到一起 |
| 📐 **不会画分镜** | 没有美术功底，没法用画面把脑子里的调度表达清楚 |

**根源在于：只用文字，很难把"空间"说清楚。**

## Topview 3D Builder 做什么

> **把"说不清的空间"，变成"看得见的 3D 场景"，再变成"真实的视频"。**

它打通了**从一个想法，到 3D 场景，再到真实视频**的完整创作流程：

1. **想法 → 3D 场景：** 你只需要说出脑海里的画面，AI 自动帮你搭好场景：谁站哪、朝哪看、拿什么、镜头从哪个角度拍。
2. **3D 场景 → 调度图：** 3D 场景是**导演的调度图**，把"站位、比例、镜头"这些最容易被 AI 搞错的东西提前定死。
3. **调度图 → 真实视频：** 以 3D 场景为依据，渲染成**真实质感的动画视频**。画面质感、光影、表演由视频模型发挥，调度完全按你的设计走。

```
一个想法  →  AI 搭好 3D 场景  →  自动检查并微调  →  多机位渲染  →  输出真实的动画视频
```

## 你会得到什么

### 🎬 导演式掌控，而不是抽卡
人物站位、朝向、坐姿、道具摆放、镜头角度，都由你决定。同一个场景可以输出多个机位，**人物和空间在所有镜头里保持一致**。

### 🎥 运镜也能提前设计
在时间轴上规划镜头的推、拉、升、环绕和切镜，拉长或缩短时长，后面的片段会自动顺延。**镜头怎么走，成片就怎么拍。**

### 💬 说人话就能搭
不用学 3D 软件。在 ChatGPT、Cursor、Claude Code 里直接说：

> "帮我搭一个场景：两个人隔着桌子对坐，一个女人正在说话，给我正面、过肩和俯视三个镜头。"

### ✅ 生成视频之前先自动"质检"
系统会自动检查人物有没有悬空或穿模、彼此距离是否合理、人物是否在镜头里、构图是否合适。**问题在生成视频之前就被发现**，省下反复重试的积分。

### ✏️ 随时可改，改一处不动其他
场景以项目形式保存，下次打开接着改。想让人物挪半步、换个坐姿、加一台机位，**只改你要改的那一处**，不用整个推倒重来。你也可以在内置可视化编辑器（Studio）里亲手拖拽调整。

### 🔒 本地运行，素材不上传
搭建和渲染都在你自己的电脑上完成，**无需账号，不上传任何内容**。

## 看看能做出什么

左边是你搭的 3D 调度，右边是据此生成的视频镜头：**3D 里怎么摆，成片就怎么拍。**

<table>
  <tr>
    <th width="50%" align="center">3D 调度</th>
    <th width="50%" align="center">生成的视频</th>
  </tr>
  <tr>
    <td align="center"><video src="https://github.com/user-attachments/assets/f304c401-a009-470c-ba7b-1fba10ea3a14" width="100%" controls muted playsinline></video></td>
    <td align="center"><video src="https://github.com/user-attachments/assets/3365923a-a8b4-4c78-aeaa-2d32b6c22320" width="100%" controls muted playsinline></video></td>
  </tr>
  <tr>
    <td colspan="2"><b>🐉 空镜 · 跟随飞行：</b>骑士驾驭巨龙飞越城堡。镜头从骑士身后偏上的位置出发，越过龙翼望向塔楼，8 秒内跟随飞行，随巨龙掠过城堡、飞向远方山丘。</td>
  </tr>
  <tr>
    <td align="center"><video src="https://github.com/user-attachments/assets/5a12c45a-a5d0-4fe8-a5d9-40689fd62988" width="100%" controls muted playsinline></video></td>
    <td align="center"><video src="https://github.com/user-attachments/assets/d20f2c9a-8fc2-45c7-b7cc-249a4a6b1e8c" width="100%" controls muted playsinline></video></td>
  </tr>
  <tr>
    <td colspan="2"><b>☕ 产品 · 推近升镜：</b>咖啡店吧台，一个人把壶里的饮品倒进杯中。镜头从吧台对面的全景开始，8 秒内推近并升高，最终切到俯拍倒水的特写。</td>
  </tr>
  <tr>
    <td align="center"><video src="https://github.com/user-attachments/assets/a49d606b-b480-4846-a60c-59044c93c1f7" width="100%" controls muted playsinline></video></td>
    <td align="center"><video src="https://github.com/user-attachments/assets/6a3afbde-32f2-4274-8f25-c7f8b93bcca5" width="100%" controls muted playsinline></video></td>
  </tr>
  <tr>
    <td colspan="2"><b>🏀 运动 · 起跳投篮：</b>球员起跳投篮。镜头从球员身旁的低位出发，8 秒内升高并推向篮筐，最后停在篮筐上方俯视。</td>
  </tr>
  <tr>
    <td align="center"><video src="https://github.com/user-attachments/assets/3616a492-1961-4760-ab3e-259c603b292c" width="100%" controls muted playsinline></video></td>
    <td align="center"><video src="https://github.com/user-attachments/assets/8db00ea9-9b6b-414e-a76b-9b92761504f6" width="100%" controls muted playsinline></video></td>
  </tr>
  <tr>
    <td colspan="2"><b>🚴 街景 · 跟拍拉升：</b>一个人沿城市街道骑行。镜头从平视角度并行跟拍，8 秒内升高并后拉，最终以高角度俯瞰整条街道。</td>
  </tr>
</table>

### 更多可以直接试的提示词

> 搭一个小咖啡馆：两个人隔着桌子对坐。镜头放在窗外，用 4 秒缓缓推近。渲染首帧、中间帧和末帧。

> 一位女士站在白色影棚里，摆出"行走"姿势。给我三个机位：正面、四分之三侧面、低角度，三个都渲染出来。

> 在空旷的街道中央放一辆车，镜头用 5 秒绕车环绕 90 度。

> 基于我现在的场景，在主角身后再加一个机位，播放到一半时切过去。

## 内置素材，开箱即用

| 素材 | 数量 | 说明 |
| --- | --- | --- |
| 👤 角色 | 4 个 | 儿童、青年、女性、男性 |
| 🧍 姿势 | 121 种 | 坐、站、行走、对打、爬行、伸手…… |
| 📦 道具 | 基础几何体 | 用方块、柱体等快速搭出桌椅、墙体、物件 |
| 🎥 镜头 | 自由添加 | 叙事镜头 + 全景俯视机位，方便一眼看清全场调度 |

> 素材由 Topview 制作，采用 CC BY 4.0 协议，可自由使用。

## 适合谁

- **AI 短剧 / 短视频创作者**：让多镜头之间人物位置不"穿帮"，提高成片率
- **广告 / 品牌内容团队**：先在内部对齐调度和镜头，再投入生成成本
- **独立导演 / 分镜师**：不会画画，也能快速出分镜参考
- **电商 / 营销运营**：批量产出人物与产品关系稳定的场景素材
- **教育、动画、游戏预演**：快速验证一场戏该怎么拍


## 目前能做什么，不能做什么

我们希望你对产品有清晰的预期：

| ✅ 擅长 | ⚠️ 暂不支持 |
| --- | --- |
| 人物站位、朝向、坐立等**静态姿势** | 行走、跑步等**连续身体动画**（可用"行走姿势"静帧 + 位移关键帧表达走位） |
| 抽象、比例正确的场景调度 | 精细的场景与道具细节、写实质感 |
| 多机位、全景俯视、构图检查 | 自定义角色形象（目前使用 4 个内置人偶角色） |

> 3D 场景是"画面骨架"，用来约束视频模型的调度，最终的真实质感由视频生成阶段完成。


## 常见问题

**需要 3D 建模基础吗？**
不需要。用自然语言描述即可，系统会自动完成搭建、检查和渲染。

**需要付费或注册吗？**
搭建、编辑、渲染全部免费，且无需账号。

**我的内容会被上传吗？**
不会。所有项目都保存在你本机的 `.topview-3d/` 文件夹中。

**它能直接生成视频吗？**
能。它覆盖从想法到 3D 场景，再到真实动画视频的完整流程：先把调度搭好，再以 3D 场景为依据输出视频。

## 了解更多

- 🌐 产品主页：[topview.ai/3d-builder](https://www.topview.ai/3d-builder)
- 🛠 开发者与进阶文档（CLI、项目格式、版本发布、贡献指南）：[DEVELOPER.md](DEVELOPER.md)
- 🐞 问题反馈：[GitHub Issues](https://github.com/topviewai/topview-3d-builder/issues)

## 许可

- 代码、Schema 与文档：[Apache License 2.0](LICENSE)
- 内置素材（角色、姿势等）：[CC BY 4.0](builtin-assets/LICENSE)，署名："Scene3D built-in assets © Topview, CC BY 4.0"
