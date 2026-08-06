---
name: lotus-meme-github
description: Generate original square Chinese 土味/长辈图 floral meme stickers from a bundled background gallery. Use when a user wants a kitschy lotus, rose, rainbow, or glitter greeting-card meme and supplies text using plus signs to mark the red emphasized phrase, such as “我们什么时候+开组会+呢”.
---

# 莲花土味表情包生成器

Create a square meme sticker in two user-facing steps: choose one bundled background, then provide marked text. Keep the process conversational and visual.

## Step 1: Background single-choice question

Before asking for any text, show all four image files from `assets/` inline in the current conversation. Use the local absolute paths after resolving this skill directory. Present exactly one choice question:

“请选择一个背景：1 荷花蓝天、2 绿叶玫瑰、3 彩虹茶壶、4 荷花玫瑰晚霞。”

Accept only one selection unless the user explicitly asks to change it later. Map the answer as follows:

| Choice | Background asset | Visual character |
| --- | --- | --- |
| 1 | `assets/01-lotus-sky.png` | 蓝天荷花、清爽 |
| 2 | `assets/02-rose-green.png` | 深绿玫瑰、浓郁 |
| 3 | `assets/03-rainbow-teapot.png` | 彩虹茶壶、最土味 |
| 4 | `assets/04-lotus-rose-sunset.png` | 紫红晚霞、闪耀 |

Do not use external images. These bundled images are the selection previews; use the selected one as the image-generation reference only, not as a fixed canvas, so the final image remains original and leaves room for the text.

## Step 2: Parse marked text

Ask the user for one phrase in this exact pattern: `前文+重点文字+后文`.

For example, `我们什么时候+开组会+呢` means:

- Full text: `我们什么时候开组会呢`
- Emphasized text: `开组会`
- Prefix: `我们什么时候`
- Suffix: `呢`

Require exactly two `+` signs. If malformed, ask the user to send it again in that pattern. Preserve every character inside and outside the signs exactly.

## Generate the sticker

Use the built-in image-generation tool with the selected background shown as a style/composition reference. Generate one original 1:1 square image.

Use this layout:

- Put the emphasized phrase in the center as the largest text: vivid red, thick luminous yellow outline, deep dark shadow.
- Put prefix and suffix in royal blue with thick yellow outlines. Use a balanced top line and bottom line; combine short fragments when it improves legibility.
- Preserve the selected background’s key colors and flower motif, but retain clear contrast behind all text.
- Render only the user’s exact Chinese text. Include no other words, numbers, logos, watermarks, or people.

Inspect the result for exact Chinese text and emphasis. If text is incorrect or the highlighted phrase is not visually dominant, regenerate once with that single correction.

Save a selected final to `output/` in the user’s active workspace with a descriptive filename such as `我们什么时候开组会呢-荷花表情包.png`. Show it inline and provide a local file link.
