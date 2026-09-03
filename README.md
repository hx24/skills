# My Skills

[中文](./README.zh-CN.md)

This repo stores personal reusable skills. Each skill lives in its own folder with a `SKILL.md`.

## Skills List

| Skill | Folder | Description |
|-------|--------|-------------|
| editorial-poster | `editorial-poster/` | One skill, two styles. Strict 3:4 vertical, top 50% original photo, bottom 50% illustration. `flat` (default, universal: people/pets/objects/scenes) and `watercolor` (人物水墨画, human dynamic moments). Never collage multiple photos. |

## Usage

1. Upload 1 or more photos.
2. Ask the agent to use `editorial-poster`, e.g.:
   - "Generate an editorial-poster from this photo" (defaults to flat)
   - "Use watercolor style for this one"
   - "title=My Dog, sub=2026, style=flat"
3. One input photo → one output poster. Multiple photos are processed independently.
4. After generation the agent always tells you which style was made and offers the other one; if flat was made but the photo looks like a human dynamic moment, it will recommend trying watercolor.

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
