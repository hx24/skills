# My Skills

[中文](./README.zh-CN.md)

This repo stores personal reusable skills. Each skill lives in its own folder with a `SKILL.md`.

## Skills List

| Skill | Folder | Description |
|-------|--------|-------------|
| editorial-poster | `editorial-poster/` | Create one independent high-end editorial poster per uploaded photo. Strict 3:4 vertical, top 50% original photo, bottom 50% minimal hand-drawn paper illustration. Never collage multiple photos. |

## Usage

1. Upload 1 or more photos.
2. Ask the agent to use `editorial-poster`, e.g.:
   - "Generate an editorial-poster from this photo"
   - "Generate one poster per photo, don't collage them"
3. One input photo → one output poster. Multiple photos are processed independently.

See details in `editorial-poster/SKILL.md`.

## How to Add a New Skill

1. Create a new folder under this directory: `<skill-name>/`
   - Name must be lowercase, hyphen-separated, e.g. `my-new-skill`.
2. Add `SKILL.md` inside it with frontmatter:
   ```markdown
   ---
   name: my-new-skill
   description: What it does and when to trigger it.
   ---
   ```
3. Write workflow + spec + usage (English + 中文 if needed).
4. Update both `README.md` and `README.zh-CN.md` Skills List.

## Directory Structure

```
.
├── README.md
├── README.zh-CN.md
└── editorial-poster/
    └── SKILL.md
```
