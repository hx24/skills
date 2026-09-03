# 我的 Skills

[English](./README.md)

本仓库用于存放个人可复用的 skills。每个 skill 独立一个文件夹，内含 `SKILL.md`。

## Skill 列表

| Skill | 目录 | 说明 |
|-------|------|------|
| editorial-poster | `editorial-poster/` | 为每张上传照片生成一张独立的高端编辑风海报。严格 3:4 竖版，上半 50% 为原图照片，下半 50% 为极简手绘纸感插画。多图不拼贴，逐张独立出图。 |

## 使用说明

1. 上传 1 张或多张照片。
2. 让 Agent 使用 `editorial-poster`，例如：
   - “用这张照片生成 editorial-poster 海报”
   - “这几张各出一张编辑风海报，不要拼在一起”
3. 一张输入图 → 一张输出海报，多张图逐张独立处理。

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
