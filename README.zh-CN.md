# 我的 Skills

[English](./README.md)

本仓库用于存放个人可复用的 skills。每个 skill 独立一个文件夹，内含 `SKILL.md`。

## Skill 列表

| Skill | 目录 | 说明 |
|-------|------|------|
| editorial-poster | `editorial-poster/` | 一个 skill 两种风格。严格 3:4 竖版，上半 50% 原图照片，下半 50% 插画。`flat` 平涂版（默认，通用：人物/宠物/物件/场景）与 `watercolor` 人物水墨画版（人物动态瞬间）。多图不拼贴，逐张独立出图。 |

## 使用说明

1. 上传 1 张或多张照片。
2. 让 Agent 使用 `editorial-poster`，例如：
   - “用这张照片生成 editorial-poster 海报”（默认平涂版）
   - “这张直接出人物水墨画版”
   - “标题用《海边假日》，style=flat”
3. 一张输入图 → 一张输出海报，多张图逐张独立处理。
4. 出图后 Agent 会告知当前是哪个版本、还支持哪个版本；若默认出了平涂版但照片是人物动态瞬间，会主动推荐人物水墨画版并询问是否再出一版。

详细规范见 `editorial-poster/SKILL.md`。

## 如何新增 Skill

1. 在本目录下新建文件夹：`<skill-name>/`，名称小写短横线分隔，如 `my-new-skill`。
2. 在其中添加 `SKILL.md`，开头包含 frontmatter：
   ```markdown
   ---
   name: my-new-skill
   description: 这个 skill 做什么、什么时候触发。
   ---
   ```
3. 编写工作流 + 规范 + 使用说明（建议英文 + 中文都写）。
4. 同步更新 `README.md` 和 `README.zh-CN.md` 的 Skill 列表。

## 目录结构

```
.
├── README.md
├── README.zh-CN.md
└── editorial-poster/
    └── SKILL.md
```
