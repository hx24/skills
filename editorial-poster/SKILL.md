---
name: editorial-poster
description: Use when user uploads photo(s) and asks for high-end editorial poster, art publication cover, top-photo bottom-illustration poster, or minimalist hand-drawn paper illustration poster. Triggers on keywords like editorial poster, art book cover, independent publication cover, photo to illustration poster.
---

# Editorial Poster

Create one independent high-end editorial poster for each uploaded photo. Do not combine multiple photos into a collage. Each photo must be processed and output as a separate poster.

## When to use

- User uploads 1 or more photos and requests a poster / editorial / art-book / publication-cover transformation.
- If multiple photos are provided, loop over them: one input photo → one output poster. Never merge them.

## Workflow

1. Take one original uploaded photo as input.
2. Parse optional custom text from the user request (see Custom text).
3. Generate a strict 3:4 vertical poster following the spec below, applying custom text if provided.
4. Repeat for each additional photo independently.
5. Output each poster as a separate image.

## Custom text (user-overridable)

Optional parameters the user may specify at call time:
- `title`: main text, e.g. "标题：夏日海边" / `title="Summer by the Sea"`. Keep short (1–8 words / 1–10 Chinese characters recommended).
- `sub`: secondary text, e.g. "副标题：2026" / `sub="2026"`. Optional, even shorter than title.

Parsing rules:
- Accept Chinese or English forms: 标题/题目/title, 副标题/小字/sub/subtitle, 文字/text.
- If the user gives explicit text, it takes highest priority and MUST appear verbatim in the bottom half (exact characters, language, spelling, punctuation).
- If the user says no text / 无字 / 不要文字, render the bottom half with illustration only, no typography.
- If the user says nothing about text, fall back to the default TYPOGRAPHY behavior in the Poster Spec (optional minimal auto text, or no text if it doesn't fit).

## 使用说明（中文）

适用场景：用户上传 1 张或多张照片，希望转成高端编辑风海报 / 艺术出版物封面 / 上照片下插画的极简海报时使用。

输入要求：
- 至少 1 张原始照片，无照片时先请用户上传。
- 支持人物、宠物、物品、场景等各类照片。

使用方法：
1. 一次取一张原图作为输入，不要拼贴、多图合成。
2. 先解析用户是否指定了自定义文字（见下方自定义文字）。
3. 按下方 Poster Spec 生成严格 3:4 竖版海报，有自定义文字则必须原文呈现。
4. 有多张图时逐张独立生成，每张图输出一张独立海报。
5. 直接输出成图，无需额外解释。

自定义文字（可选）：
- `title` 主标题：如“标题：夏日海边” / `title="Summer by the Sea"`，建议 1–10 个汉字 / 1–8 个英文词。
- `sub` 副标题：如“副标题：2026” / `sub="2026"`，可选，比主标题更短。
- 支持中文或英文写法：标题/题目/title，副标题/小字/sub/subtitle，文字/text。
- 指定了就必须一字不差地画在下半部分（不翻译、不改写、不加字）。
- 说“无字 / 不要文字”则下半部分只保留插画，不加任何字。
- 不提文字时，走默认行为：可加极简自动文字，也可不加。

输出要求：
- 上半部分必须忠实还原原图人物身份、构图、姿态、服装、物件关系，仅做高级编辑级调色。
- 下半部分必须是从同一张照片提炼出的极简手绘纸感插画，主体小而居中，留白大，4 色以内。
- 整体感觉：安静、诗意、克制、高级，像独立艺术出版物封面，而非商业广告。

示例说法：
- “用这张照片生成 editorial-poster 海报”
- “这几张各出一张编辑风海报，不要拼在一起”
- “标题用《海边假日》，副标题 2026，出 editorial-poster 海报”
- “title=My Dog, sub=2026，不要其他文字”

## Poster Spec — pass verbatim to the image generation model

```
Strict 3:4 vertical composition.

Divide the canvas horizontally into two exactly equal sections, with a precise 1:1 height ratio.
The top half occupies exactly 50% of the canvas.
The bottom half occupies exactly 50% of the canvas.
The two sections should feel visually connected as one refined art publication cover.

TOP HALF — ORIGINAL PHOTOGRAPH
- Preserve the original photograph as faithfully as possible.
- Keep the main composition, subjects, identity, facial features, body proportions, poses, expressions, clothing, objects, and spatial relationships unchanged.
- Preserve the realistic photographic texture, natural lighting, shadows, atmosphere, and original color mood.
- Apply only subtle, sophisticated editorial color grading, creating the feeling of a premium magazine photograph, contemporary art book, or high-end independent publication.
- The image should remain photorealistic and authentic, never overly retouched or artificially stylized.
- If necessary to fit the 3:4 composition naturally, extend the sky, ground, walls, or surrounding environmental background.
- Background extension must feel seamless and photographic.
- Never stretch, distort, reshape, replace, or alter the main subject.

BOTTOM HALF — MINIMAL HAND-DRAWN PAPER ILLUSTRATION
- Extract the most recognizable visual elements from the original photograph and reinterpret them as a minimalist hand-drawn paper-cover illustration.
- Preserve:
  - The most recognizable subject
  - Essential silhouette and proportions
  - Key pose or gesture
  - Important objects
  - The core narrative relationship between people and objects
- Highly simplify the image. Remove unnecessary details and retain only the visual information needed for immediate recognition.
- Use:
  - Delicate, slightly imperfect hand-drawn lines
  - A small number of bold, clearly defined acrylic-style flat color shapes
  - Rough paper texture
  - Visible handmade brush marks
  - Slightly irregular, organic edges
  - Subtle imperfections that make it feel genuinely handmade
- The main illustrated subject should be small, centered, and carefully composed, occupying approximately 10-20% of the bottom half.
- Leave a large amount of negative space around the illustration.
- The background should primarily resemble:
  - Rough white paper
  - Warm off-white paper
  - Pale natural paper
  - Minimal editorial book-cover stock
- Use only a few lines or small color shapes to suggest the surrounding environment.

COLOR PALETTE
- Extract the dominant colors directly from the original photograph.
- Compress the palette into no more than 4 main colors.
- Keep the colors restrained, sophisticated, and harmonious.
- Use bold but controlled flat color blocks.
- Avoid excessive color variation.
- Preserve subtle paper grain and handmade brush texture.
- The illustration should visually feel like a simplified color interpretation of the photograph.

TYPOGRAPHY
- CUSTOM TEXT OVERRIDE: if the user request includes explicit title / sub / text, render THAT text verbatim in the bottom half. Preserve exact characters, language, spelling, and punctuation. Never translate, rephrase, or add extra words. Style it minimal, understated, editorial, interacting with the negative space.
- If the user explicitly requests no text (no text / 无字 / 不要文字), output illustration only with no typography.
- Otherwise (no user text specified): a small amount of simple typography may be included when appropriate.
- Possible auto elements: a short title, keyword, object name, location, year, number, short phrase.
- Text should be minimal, understated, and editorial.
- Typography should naturally interact with the large areas of negative space and the small illustration, evoking art book covers, independent publishing, contemporary editorial design, thoughtful children's picture books.
- Do not force text into the composition if it does not naturally fit the photograph.

VISUAL LANGUAGE
- The final poster should feel: Quiet · Poetic · Refined · Minimal · Innocent · Relaxed · Artistic · Thoughtful · High-recognition · Premium
- The visual concept should be: "A small subject surrounded by a large amount of empty space."
- The result should resemble a carefully designed independent art publication cover, rather than a commercial advertisement.

AVOID
- Do not use: colored-pencil aesthetics, crayon textures, bleeding watercolor, pure line-art illustration, complex realistic illustration, heavy oil-painting effects, smooth polished digital illustration, 3D rendering, glossy 3D textures, commercial cartoon aesthetics, cute commercial character design, e-commerce advertising aesthetics, generic poster templates, excessive decorative elements, busy compositions, excessive typography.

FINAL ART DIRECTION
- The top half should feel like a beautiful, authentic editorial photograph.
- The bottom half should feel like a small, handmade visual poem derived from that photograph.
- The two halves should clearly belong to the same visual story, while maintaining a strong contrast between photographic realism above and minimal handmade illustration below.
- Prioritize recognition, restraint, negative space, material texture, subtle imperfection, editorial sophistication, and artistic storytelling over decorative complexity.
```

## Notes

- Always keep input photo identity unchanged in the top half.
- Bottom illustration must be recognizably derived from the same photo, not a generic drawing.
- Custom user text (title / sub) has highest priority: render verbatim, never translate or embellish.
- If no photo is uploaded, ask the user to upload one before generating.
