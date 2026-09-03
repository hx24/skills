---
name: editorial-poster
description: Use when user uploads photo(s) and asks for high-end editorial poster, art publication cover, top-photo bottom-illustration poster, minimalist hand-drawn paper illustration poster, or watercolor memory poster. Two styles in one skill: flat (default, universal) and watercolor (human dynamic moments). Triggers on keywords like editorial poster, art book cover, independent publication cover, photo to illustration poster, watercolor poster, 平涂版, 水彩版, 人物水墨画.
---

# Editorial Poster

One skill, two styles. Create one independent high-end editorial poster for each uploaded photo. Do not combine multiple photos into a collage. Each photo must be processed and output as a separate poster.

## Styles

- `flat` (平涂版, DEFAULT): bottom half = minimalist hand-drawn paper illustration with acrylic-style flat color shapes, 10–20% of bottom half. Universal: people, pets, objects, still scenes, architecture.
- `watercolor` (人物水墨画 / 水彩版): bottom half = poetic translucent watercolor memory with motion blur following the real movement direction, 15–30% of bottom half. Best for fleeting human moments: running, jumping, turning, waving, looking back, interaction, sports, kids, street, travel. Concept: top says "This is what happened", bottom says "This is how the moment felt".

## When to use

- User uploads 1 or more photos and requests a poster / editorial / art-book / publication-cover transformation.
- If multiple photos are provided, loop over them: one input photo → one output poster. Never merge them.
- User may specify style upfront (style=flat/watercolor, 平涂版/人物水墨画/水彩版). If not specified, default to `flat`.

## Workflow

1. Take one original uploaded photo as input.
2. Parse style: explicit `style=flat/watercolor` (平涂版/人物水墨画/水彩版) wins. Otherwise default to `flat`, but analyze whether the subject looks like a fleeting human moment (human expression, gesture, movement, interaction: running, jumping, turning, swinging, walking, laughing, waving, looking back). Remember this flag for the post-generation notice.
3. Parse optional custom text from the user request (see Custom text).
4. Generate a strict 3:4 vertical poster using the matching spec below (Style A for flat, Style B for watercolor), applying custom text if provided.
5. Repeat for each additional photo independently.
6. Output each poster as a separate image.
7. AFTER generation, always tell the user in text (never baked into the image): which style was just generated, plus the other available style. If default `flat` was used but the photo was flagged as watercolor-suitable, explicitly recommend trying watercolor and ask whether to generate a watercolor version. Example: "刚才生成的是平涂版（flat）。检测到照片是人物动态瞬间，也很适合人物水墨画版（watercolor），要再生成一版看看吗？"

## Custom text (user-overridable)

Optional parameters the user may specify at call time:
- `title`: main text, e.g. "标题：夏日海边" / `title="Summer by the Sea"`. Keep short (1–8 words / 1–10 Chinese characters recommended).
- `sub`: secondary text, e.g. "副标题：2026" / `sub="2026"`. Optional, even shorter than title.

Parsing rules:
- Accept Chinese or English forms: 标题/题目/title, 副标题/小字/sub/subtitle, 文字/text.
- If the user gives explicit text, it takes highest priority and MUST appear verbatim in the bottom half (exact characters, language, spelling, punctuation).
- If the user says no text / 无字 / 不要文字, render the bottom half with illustration only, no typography.
- If the user says nothing about text, fall back to the default TYPOGRAPHY behavior of the active style spec.
- Style difference: `flat` supports title + sub; `watercolor` supports ONLY one line of text (use `title` as that line, recommend English 1–4 words; `sub` is ignored with a notice to the user).

## 使用说明（中文）

适用场景：用户上传 1 张或多张照片，希望转成高端编辑风海报 / 艺术出版物封面 / 上照片下插画的极简海报时使用。一个 skill 两种风格。

风格：
- 平涂版（flat，默认）：下半为丙烯风平涂小插画，通用，人物/宠物/物件/静物/建筑都行。
- 人物水墨画版（watercolor，水彩版）：下半为轻透水彩动态记忆，最适合人物动态情绪瞬间（跑跳转身挥手回头互动、运动亲子街头旅行）。

输入要求：
- 至少 1 张原始照片，无照片时先请用户上传。
- 支持人物、宠物、物品、场景等各类照片。

使用方法：
1. 一次取一张原图作为输入，不要拼贴、多图合成。
2. 先解析风格：用户明确指定（人物水墨画/水彩版/平涂版/style=watercolor/flat）则听用户的；没指定默认平涂版，同时判断是否为人物动态瞬间并记住。
3. 再解析自定义文字，有指定则必须原文呈现（人物水墨画版只用一行，`sub` 会被忽略并告知）。
4. 按对应风格 Spec 生成严格 3:4 竖版海报。
5. 有多张图时逐张独立生成，每张图输出一张独立海报。
6. 出图后必须用文字说明（不要画进图里）：刚才生成的是哪个版本 + 还支持哪个版本；若默认出了平涂版但检测到适合人物水墨画，主动推荐并询问是否再出一版。

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
- “用这张照片生成 editorial-poster 海报”（默认平涂版）
- “这几张各出一张编辑风海报，不要拼在一起”
- “直接出人物水墨画版”
- “用人物水墨画版 watercolor 出这张”
- “标题用《海边假日》，副标题 2026，出 editorial-poster 海报”（默认平涂版）
- “title=My Dog, sub=2026，不要其他文字”
- “人物水墨画版，文字用 RUNNING FREE”

## Poster Spec Style A (flat) — pass verbatim when style=flat

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

## Poster Spec Style B (watercolor / 人物水墨画) — pass verbatim when style=watercolor

```
Create one independent high-end editorial art poster from the uploaded photograph. Strict 3:4 vertical composition. Divide the canvas horizontally into two exactly equal sections: TOP HALF exactly 50%, BOTTOM HALF exactly 50%. Reality above. Memory below. Central concept: "A fleeting human moment remembered through watercolor." The final result should feel like a refined independent art publication, contemporary photography book, or poetic travel journal. Never commercial advertisement or generic poster template.

TOP HALF — ORIGINAL PHOTOGRAPH
- Preserve the uploaded photograph as faithfully as possible. Do not redesign or reinterpret.
- Preserve: subject identity, facial features, expression, hairstyle, body proportions, clothing, accessories, objects, pose, gesture, movement, spatial relationship between people, camera perspective, lighting, atmosphere, original narrative.
- Especially preserve spontaneous human expressions and body language. If two or more people are essential to the emotional moment, preserve all of them. Do not automatically isolate one person. Background people irrelevant to the central moment should not become important subjects.
- Apply only subtle premium editorial color grading. Maintain realistic photographic texture. Never beautify excessively, change identity, alter gesture, or reposition the body.
- If necessary for 3:4 layout, naturally extend only environmental areas (sky, ground, walls, road, architecture, vegetation). Never stretch main subjects.

BOTTOM HALF — POETIC WATERCOLOR MEMORY
- NOT a complete watercolor copy. A visual memory extracted from the photograph. Identify the most emotionally recognizable moment first.
- Preserve only: main character(s), essential silhouettes, facial mood, body gesture, movement direction, interaction between people, one or two important objects, a few environmental clues. Remove everything unnecessary.
- SUBJECT SCALE: the complete illustrated scene occupies approximately 15-30% of the bottom half. Do not enlarge to fill the page. Surround with a very large amount of untouched paper. Feeling: "a small human moment floating inside a large quiet page."
- WATERCOLOR MOVEMENT: delicate traditional watercolor, light, translucent, airy, imperfect, restrained. No heavy saturated wash, no fully painted surfaces. Allow white paper to show through. Amplify the movement already in the photo with controlled motion blur following the actual physical direction (directional brush dragging, broken pigment edges, translucent overlapping washes, partially dissolved contours, dry-brush streaks, soft trailing pigment, disappearing edges). Keep face, body center, essential gesture, important object relatively clear; let secondary moving areas dissolve. Never random blur.
- EMOTION: laughing retains joyful openness; running retains energy; waving preserves raised hand; looking back preserves gaze-body relationship; interaction preserves emotional connection. Must immediately remind viewer of the exact photographed moment.
- ENVIRONMENT: reduce to a few poetic clues dissolving into paper (crosswalk = pale horizontal strokes, field = soft green wash, road = gray directional strokes, railing = thin broken line, buildings = faint silhouettes, trees = soft pigment shapes, lights = tiny diffused dots). No rectangular painted background, no complete scenery, no hard frame, no vignette. Watercolor suspended on paper.
- PAPER: warm white or pale ivory watercolor paper, subtle grain. Transparent pigment, soft pooling, dry-brush texture, irregular edges, granulation, occasional unfinished marks. Avoid excessive splashes.
- COLOR: extract from photo, compress to approximately 3-5 dominant colors, restrained saturation, generally lighter and quieter than photo. Preserve recognizable clothing colors muted (denim blue = muted denim, red jersey = restrained warm red, green field = pale sage, black = charcoal gray). Fade into paper. Never dense colorful painting.
- COMPOSITION: do not mechanically center. Give more negative space in front of / around movement. For multiple people preserve relative scale, distance, direction, emotional relationship. Effortless, quiet, poetic.

TYPOGRAPHY
- CUSTOM TEXT OVERRIDE: if user gave explicit title/text, render THAT single line verbatim (exact characters, no translation, no extra words). `sub` is ignored in watercolor style.
- If user requested no text, no typography.
- Otherwise: use ONLY ONE line of text, a short English phrase 1-4 words chosen for the emotion/movement (e.g. IN THE MOMENT, ON THE MOVE, IN MOTION, RUNNING FREE, TOGETHER, HERE & NOW). No year, no subtitle, no description, no second line. Small, quiet, widely spaced, refined, editorial, placed in negative space near lower area, never competing with illustration.

VISUAL LANGUAGE: Quiet, Poetic, Airy, Human, Spontaneous, Refined, Minimal, Emotional, Editorial, Handmade, Imperfect, Light, Dynamic, Nostalgic, Premium. Contrast: TOP = real vivid spontaneous moment; BOTTOM = same moment lighter, quieter, softer, fleeting.

AVOID: heavy/saturated watercolor, dense backgrounds, full-scene reproduction, large characters, commercial illustration, anime, cute cartoon, digital painting, vector, colored pencil, crayon, oil, 3D, excessive splashes, random blur, speed lines, overly detailed faces, rigid outlines, busy compositions, frames, multiple text blocks, years, subtitles, captions, logos.

FINAL ART DIRECTION: top says "This is what happened." Bottom says "This is how the moment felt." Extract the emotional center, preserve essential people, gesture, expression, interaction, movement direction, let everything else disappear into watercolor, motion, paper and empty space. A memory that is still moving.
```

## Notes

- Always keep input photo identity unchanged in the top half.
- Bottom illustration must be recognizably derived from the same photo, not a generic drawing.
- Custom user text (title / sub) has highest priority: render verbatim, never translate or embellish. In watercolor style only one text line is allowed.
- Post-generation notice is mandatory: always state which style (flat/watercolor) was generated and that the other style is available; recommend watercolor when the photo is a human dynamic moment but flat was generated, and ask if the user wants the other version.
- If no photo is uploaded, ask the user to upload one before generating.
