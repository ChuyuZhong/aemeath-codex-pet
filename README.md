# 爱弥斯 Codex Pet

<div align="center">
  <img src="preview/idle.gif" alt="爱弥斯待机动画" width="150" />
  <img src="preview/waving-touch.gif" alt="爱弥斯挥手动画" width="150" />
  <img src="preview/jumping.gif" alt="爱弥斯跳跃动画" width="150" />
</div>

<p align="center">让展开羽翼的爱弥斯，在 Codex 里陪你一起写代码 ✨</p>

这是一个面向 Codex 桌面端的自定义动态宠物包。R2 以原始爱弥斯表情包素材为基础，尽量保留原画的像素风格、动作节奏和角色形象，并将不同素材映射到 Codex Pet 的标准动画状态中。

> 当前稳定版：**R2**  
> R3 的逐帧清晰化仍处于实验阶段，因此本仓库发布包暂时回退并固定使用 R2。

## 动画预览

| 待机 | 向右移动 | 向左移动 | 工作 |
| --- | --- | --- | --- |
| ![待机](preview/idle.gif) | ![向右移动](preview/running-right.gif) | ![向左移动](preview/running-left.gif) | ![工作](preview/running.gif) |

| 挥手 / 触碰候选 | 跳跃 | 等待 / 检查 | 失败 / 特殊反应 |
| --- | --- | --- | --- |
| ![挥手](preview/waving-touch.gif) | ![跳跃](preview/jumping.gif) | ![等待](preview/waiting.gif) | ![失败](preview/failed-special.gif) |

完整图集预览：[`preview/aemeath-v2-atlas-preview.png`](preview/aemeath-v2-atlas-preview.png)

## 安装与部署

### 方法一：手动安装

1. 从 GitHub Releases 下载 `aemeath-codex-pet-r2.zip` 并解压。
2. 打开当前 Windows 用户目录下的 `.codex\pets` 文件夹。
3. 新建 `aemeath-v2` 文件夹。
4. 将发布包根目录中的以下两个文件复制进去：
   - `pet.json`
   - `spritesheet-v2-r2.webp`
5. 完全退出 Codex（包括系统托盘中的进程），然后重新启动。
6. 在 Codex 的宠物选择界面中选择“爱弥斯 V2 · 羽翼”。

最终目录应如下：

```text
%USERPROFILE%\.codex\pets\aemeath-v2\
├─ pet.json
└─ spritesheet-v2-r2.webp
```

### 方法二：使用 PowerShell 安装

在解压后的发布包根目录打开 PowerShell，执行：

```powershell
$petDir = Join-Path $env:USERPROFILE ".codex\pets\aemeath-v2"
New-Item -ItemType Directory -Force -Path $petDir | Out-Null
Copy-Item .\pet.json, .\spritesheet-v2-r2.webp -Destination $petDir -Force
```

随后完全退出并重新启动 Codex。如果更新后仍显示旧动画，请再次确认 Codex 已彻底退出；自定义宠物素材可能会被当前进程缓存。

## 动作映射

| Codex 状态 | 使用素材 / 动作 |
| --- | --- |
| 待机 `idle` | 素材 4 |
| 向右移动 `running-right` | 素材 1 |
| 向左移动 `running-left` | 素材 1 水平翻转 |
| 挥手 `waving` | 素材 3 |
| 跳跃 `jumping` | 素材 2 |
| 失败 `failed` | 素材 5 |
| 等待 `waiting` | 素材 5 |
| 工作 `running` | 素材 7 |
| 检查 `review` | 素材 5 |

这些状态主要由 Codex 根据当前工作状态自动切换；部分动作是否能通过点击或触碰直接触发，会受到 Codex 当前版本和界面行为的影响。

## 版本说明

### R2（当前稳定版）

- 使用 Codex Pet V2 图集格式：`1536 × 2288`。
- 图集为 `8 × 11` 个单元格，每格 `192 × 208`。
- `pet.json` 使用 `spriteVersionNumber: 2`。
- 按原始表情包重新整理九种标准动作。
- 左移行动画由右移动画逐帧水平翻转，保持动作节奏一致。
- 保留原始素材风格，未采用 R3 的大范围逐帧重绘。
- 已通过结构校验，图集透明通道与已使用单元格均有效。

### R3（实验版，暂未发布）

- 尝试使用生成式图像工具逐帧修复毛刺和边缘。
- 部分帧出现了细节漂移或清晰化风格不一致，因此正式版暂时回退至 R2。

## 未来可能的优化

- 在不改变五官和原始画风的前提下，继续进行更保守的边缘去毛刺。
- 改善部分动作首尾帧的衔接，让循环更加自然。
- 为等待、检查和失败状态制作区分度更高的专属动作。
- 补充更自然的 16 方向注视动画，而不是复用静态帧。
- 根据 Codex 后续开放的触发能力，增加点击、拖动或随机互动动作。
- 增加自动打包与图集校验流程，降低后续版本更新成本。

## 文件说明

```text
.
├─ pet.json                       # Codex Pet 配置
├─ spritesheet-v2-r2.webp         # R2 动画图集
├─ preview/                       # README 动图与图集预览
└─ docs/
   ├─ source-mapping.json         # 动作与原始素材的映射记录
   └─ validation.json             # 图集结构校验结果
```

实际安装时只需要 `pet.json` 和 `spritesheet-v2-r2.webp`。

## 版权与使用说明

本项目是非官方、非商业的同人 Codex Pet 适配项目。角色形象、原始表情包及相关美术素材的权利归原作者与相应权利方所有；本仓库不对这些素材授予额外的商业使用许可。

原始素材参考页面：[哔哩哔哩动态](https://www.bilibili.com/opus/1167003396733927448)

如果你计划二次分发、用于商业项目或将素材用于其他用途，请先取得相应权利方授权。若权利方认为本项目存在不妥，请通过 Issue 联系维护者处理。

---

如果这个小家伙让你的 Codex 工作时间更开心，欢迎点一个 Star ⭐

## 友情链接

主包同学制作的菲比 codex pet也可以了解一下：
[菲比啾比](https://github.com/sherlidian01-web/phoebe-codex-pet)

最后，放一只菲比在这里，你们不许欺负她。

<p align="left">
<img src="./phoebe.png" width="300">
</p>

