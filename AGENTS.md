# LASSO 实验室 - 课题长文 (content.md) AI 生成指令 (AGENTS.md)

本指令专供 **AI 编程助手（Cursor / Windsurf / Copilot）** 或 **通用大语言模型（DeepSeek / ChatGPT / Claude / Kimi）** 使用。仅当任务是撰写、更新或打包 **LASSO 官网课题／工作介绍页** 时应用；仓库中的其他任务不受本文件的文章格式要求约束。

在此类任务中，将用户提供的科研论文（PDF、全文文本、摘要引言或草稿）转换为符合 LASSO 官网排版标准的学术长文 `content.md`，并在要求交付材料包时核对封面、插图及可选视频。

---

## 核心排版铁律 (Rules)

1. **绝对四大二级标题（严禁任何增删或修改，严禁在标题中使用 `&` 符号）**：
   - `## Overview`：研究背景、传统方案缺陷/核心痛点、本课题的攻坚目标（100~200 词）。若有演示短视频，紧随其后放置 `<video>`。
   - `## Target Scenarios`：典型应用场景、物理环境约束与部署拓扑图说明。
   - `## System Architecture`：软硬件系统框图说明、核心信号处理流程与硬核算法推导。
   - `## Experimental Evaluation`：试验台硬件参数表 + 性能对比/误差曲线 + 核心量化要点。

2. **零一级大标题**：
   第一行严禁写 `# 课题名称`（官网网页模板会自动根据表单信息生成顶部标题、作者名录与技术标签）。

3. **首屏视频先导片（Teaser Video，可选）**：
   若本课题有现场实测或系统 Demo 演示短视频（放置于 `./assets/demo.mp4`），请将其紧跟在 `## Overview` 文本段落之后：
   ```markdown
   <video controls src="./assets/demo.mp4"></video>
   *Video 1: Real-time passive trajectory tracking demonstration on the NI USRP testbed.*
   ```
   若没有视频，直接省略该标签，严禁自创独立章节。

4. **图片与图注规范**：
   所有插图一律使用相对路径 `./assets/文件名.png`，且紧随其后必须带一行单行斜体英文图注：
   ```markdown
   ![Target Application Scenario](./assets/scenario.png)
   *Figure 1: Indoor non-line-of-sight tracking scenario.*
   ```

5. **数学公式规范**：
   - 行内公式使用单个美元符号：`$f_D = \frac{2v}{\lambda}$`
   - 独立居中大公式使用双美元符号：
     $$\min_{\mathbf{v}} \|\mathbf{A}\mathbf{v} - \mathbf{f}_D\|_2^2$$

6. **文末核心量化结论**：
   在 `## Experimental Evaluation` 末尾，必须使用无序列表输出 2~3 条以**加粗关键词**开头的量化突破（如定位精度、处理时延、信噪比鲁棒性）：
   ```markdown
   * **Millimeter-Level Precision**: Achieves a median tracking error of **3.2 mm** in LoS environments and **7.8 mm** under NLoS conditions.
   * **Low Pipeline Latency**: Full signal extraction and trajectory stitching executes within $18\,\mathrm{ms}$.
   ```

7. **文风要求**：
   100% 纯正学术英文（Pure Academic English）。语言严谨、客观、克制，杜绝浮夸营销词汇（严禁使用 revolutionary, groundbreaking, unprecedented 等）。

8. **事实依据**：
   硬件型号、实验条件、误差统计和性能提升必须能从用户提供的论文或数据中找到依据。上面的数字和图注只示范格式，不得当作真实课题结果使用；缺少数据时不要编造量化结论。

---

## 材料包结构与交付（整合 README.txt）

交付完整课题介绍页材料包时，采用以下目录结构；`assets/` 中的文件名应与 `content.md` 的实际引用一致，示例文件名可按课题替换：

```text
my-project/
├── AGENTS.md          AI 撰写与交付规则，可随材料包附上
├── content.md         必填：课题正文
├── cover.png          必填：课题封面，推荐 16:9 横版、分辨率不低于 1920×1080
└── assets/            必填：正文引用的图片和多媒体资源
    ├── scenario.png
    ├── architecture.png
    ├── results-1.png
    ├── results-2.png
    └── demo.mp4        可选：确有演示视频时才提供
```

- 正文图片统一使用 `![说明](./assets/文件名.png)`，下一行紧跟单行斜体英文图注 `*Figure X: ...*`。交付前确认每个引用路径都有对应文件；不能用不存在的占位图片冒充已完成素材。
- 行内公式使用 `$...$`，独立居中公式使用 `$$...$$`。页面顶部标题、作者和标签由官网生成，因此 `content.md` 直接从 `## Overview` 开始。
- 确有现场实测或系统 Demo 视频时，将 MP4 放入 `assets/demo.mp4`，建议控制在 30 MB 内；在 Overview 文本段落后插入视频标签和英文图注。没有视频则省略。
- 完成后检查四个二级标题、Overview 的 100–200 词、文末 2–3 条有来源的量化结论、全部图片路径和封面文件。需要提交材料包时，将外层文件夹压缩为 ZIP，再由用户上传至腾讯文档收集表。

---

## 开箱即用提示词（直接复制给 DeepSeek / ChatGPT / Claude）

如果你使用的是网页版 AI，可直接复制下方内容发送：

```text
你是一名顶尖的工科学术助理。请严格遵守以下规则，根据我提供的科研论文信息，为我们实验室官网撰写一份标准的课题成果长文（content.md）：

1. 全文只能包含以下 4 个标准二级标题，严禁自创或增加其他大标题，严禁在标题中使用 & 符号：
   ## Overview
   ## Target Scenarios
   ## System Architecture
   ## Experimental Evaluation
2. 第一行绝对不要写 # 一级大标题（网页会自动生成标题和作者栏）。
3. 全文统一使用纯正、克制的学术英文。
4. 插图请预留标准相对路径占位符：
   ![图片说明](./assets/xxx.png)
   *Figure X: 英文详细图注。*
5. 数学公式使用标准 LaTeX（行内 $x$，居中大公式 $$...$$）。
6. 第 4 节末尾必须包含 2~3 个以加粗关键词开头的核心量化结论（如精度提升 xx%、时延降低至 xx ms）。
7. 仅使用论文或用户提供的真实实验数字、硬件规格与插图；缺少依据时不要编造。图片路径必须对应实际交付的 assets 文件，另备 16:9 横版 cover.png；有真实演示视频才加入 demo.mp4。

【我的论文信息如下】：
（在此粘贴你的论文英文摘要、引言、核心方法或实验数据）
```
