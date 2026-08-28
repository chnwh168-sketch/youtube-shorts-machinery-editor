---
name: youtube-shorts-machinery-editor
description: Edit local construction machinery and industrial equipment footage into YouTube Shorts and create matching publishing copy. Use when the user asks to 剪视频, 继续剪, 批量剪, 生成一条/10条 Short, 禁用口播素材, 做封面标题/英文字幕/配乐/调色, 出标题文案/Tag, 生成 YouTube/Instagram/LinkedIn 发布文案, reuse local Synology or /Volumes/video materials, or update the saved machinery Short editing rules.
---

# YouTube Shorts Machinery Editor

Final approved default as of 2026-08-24: use this skill's TK Shorts Editor cover preset, no background music, clean English cover titles/captions, and silent AAC unless the user explicitly requests usable machine sound. Choose clear source footage at 720p or higher, prefer 1080p or higher, avoid reusing recorded source time ranges, keep all-vertical edits vertical, keep all-horizontal edits horizontal, and make mixed-orientation material into vertical Shorts by default. For machinery outputs, prepend a visible 1-second cover section by default so players and upload previews do not skip the cover; use a one-frame cover only if the user explicitly asks for exactly one frame. Treat the publishing-copy Word document and used-material CSV as required companion outputs for every delivered batch.

## Core Workflow

Use this skill for local machinery/product demo footage, especially under `/Volumes/video`.

1. Before choosing clips, read `/Volumes/video/剪辑输出/素材使用记录/剪辑避重规则.md` and every readable `/Volumes/video/剪辑输出/素材使用记录/已用素材片段*.csv`.
2. Do not reuse source material time ranges already recorded. If using the same source file again, choose a non-overlapping time range.
3. Search all accessible local and mounted material folders under `/Volumes/video`, including organized folders and Synology-mounted sources.
- Preserve the latest explicit product scope and exclusions across continuation requests. If the user says “only sweepers and floor scrubbers” or “no talking-head material,” later requests such as “continue,” “make 10 more,” or “make 20” keep that scope until the user changes it.
- When the user says `不要口播` or equivalent, hard-exclude every source path containing `口播` and every clip that visually shows a presenter speaking or addressing the camera, regardless of its folder name. Reject talking-head clips with speech subtitles even if the machine is visible. Normal operators may appear only while driving, testing, loading, maintaining, or demonstrating the machine without addressing the camera. Prefer machine-only action, factory, detail, and result shots.
4. Prefer the user's main products: 钢筋切断机、钢筋弯曲机/弯箍机、抹光机、冲击夯、平板夯、压路机、地坪研磨机、马路切割机、扫地机、洗地机、升降平台.
   - For the recurring Monday batch, produce 20 new videos and prioritize 扫地车/扫地机 and 洗地机. If their verified clear, stable, unused material is insufficient, fill the remaining quota with 升降平台. Never reuse an already-recorded time range merely to reach 20.
5. Keep one Short focused on one product subtype. Do not mix different subtypes in the same video, such as 弯曲中心、台式弯曲机、手提弯曲机、弯箍机、弯弧机.
6. Use only clear, stable, high-quality clips. Source footage must be at least 720p by displayed resolution, such as `1280x720`, `720x1280`, or higher. Prefer `1080p` or higher when alternatives exist. Reject below-720p, blurry, shaky, dark, low-resolution, hard-subtitled, watermarked, UI-contaminated, or heavily compressed footage. If unsure, inspect with `ffprobe`, generate a contact sheet, and visually check sharpness before rendering.
7. Include close-up shots when the product benefits from detail, such as cutting heads, blades, bending heads, compacting plates, rollers, brushes, control panels, or lifting mechanisms.
8. If every selected usable source clip for a Short is truly vertical, such as `1080x1920` or `720x1280`, render the final edit vertical at `1080x1920`. Preserve the vertical composition; do not convert an all-vertical edit into horizontal.
9. If every selected usable source clip for a Short is truly horizontal, such as `1920x1080`, and no suitable vertical clip is being used for that product/story, render the final edit horizontal at `1920x1080`. Preserve the full horizontal product frame; do not force a whole all-horizontal edit into vertical just because the platform is Shorts.
10. When usable vertical and horizontal clips both exist for one product, prioritize a vertical `1080x1920` Short. Use clear vertical clips as the main structure, and convert selected horizontal clips into vertical inserts instead of defaulting the whole edit to landscape.
11. When converting a horizontal clip into vertical, keep the horizontal source image complete and centered in the middle band. Fill the top and bottom with the same source enlarged and blurred, then add a subtle semi-transparent dark overlay to the top/bottom background so the product remains readable. Do not hard-crop away the product unless the user explicitly asks for a tight crop.

## Output Rules

- Put final MP4 files directly in `/Volumes/video/剪辑输出`.
- Put a matching publishing-copy Word document (`.docx`) directly in `/Volumes/video/剪辑输出` for every delivered video batch, even when the continuation request does not repeat the copy requirement. Do not use Markdown as the final publishing-copy format. Use clear names such as `发布文案_样片85_YYYYMMDD.docx` or `发布文案_批量86-95_YYYYMMDD.docx`.
- Do not create product subfolders in `/Volumes/video/剪辑输出`; the only regular subfolder should be `/Volumes/video/剪辑输出/素材使用记录`.
- Use clear Chinese filenames that describe the product/content. Do not include `YouTubeShort`, `Youtube Short`, or `YouTube Short` in filenames.
- Target 15-45 seconds. Prefer 18-25 seconds when making samples or batches unless the user asks otherwise.
- Render by the selected source orientation: all-vertical edits output `1080x1920`; all-horizontal edits output `1920x1080`; mixed vertical/horizontal edits output `1080x1920` unless the user explicitly asks for horizontal. Keep `30fps`, H.264, AAC audio.
- Final MP4s must open directly on the cover. After muxing, confirm the video stream `start_time` and first video packet PTS/DTS are `0.000000`; if audio starts before video or the first video packet is delayed, re-encode/remux with no edit list (for example `-use_editlist 0`) and no leading audio gap before delivery.
- Do not add background music. Use silent AAC by default for batch work so speech cannot leak into the result. Keep original machine audio only when the user explicitly requests it and it has been checked to contain no speech; add BGM only when the user explicitly asks for music.
- Apply a consistent light color pass across clips, such as mild contrast/saturation lift and sharpening. Avoid a mismatched look between segments.

## Approved Text Style

Use English cover titles and English intermittent captions unless the user asks for another language.

### Cover Title

- Follow the approved cover preset from `/Users/jiaxiaochong/Documents/视频剪辑专家/skills/tk-shorts-editor/SKILL.md`.
- Always prepend an in-video cover section unless the user explicitly says no cover. For machinery videos, the normal cover duration is `1.0s` at 30fps so the cover is visible in common players and upload previews. Use a one-frame cover only if the user explicitly asks for exactly one frame.
- Use a clear, sharp, stable product frame that matches the title. Prefer a close, readable machine/action frame over a random wide shot.
- Choose a clean cover frame that highlights the product: product should be complete or clearly recognizable, centered or strongly framed, with minimal clutter, no watermark, no hard subtitles, no awkward operator blockage, and enough open space for the title panel.
- Cover style: clean editorial lower panel, high contrast, large English title, readable two-line spacing, no clutter.
- Draw one semi-transparent black lower panel, usually starting around `y=1040-1120` and ending near `y=1600-1660` for 1080x1920 vertical output. Add a narrow left accent bar in the same pale yellow.
- Place the cover title panel and title text horizontally centered in the video whenever possible. For horizontal `1920x1080` outputs, center the panel left-to-right and put it low enough to avoid covering the product body; for vertical outputs, keep the panel in the safe lower-middle area and visually centered.
- Cover title color must be the approved soft pale yellow `#FFF7C7`, with a thin black outline. Do not use white cover titles by default.
- Use `Roboto Black Italic` from `/Users/jiaxiaochong/Documents/视频剪辑专家/skills/tk-shorts-editor/assets/fonts/Roboto-BlackItalic.ttf` for English cover titles when available. Use `AlimamaShuHeiTi-Bold.ttf` only as fallback or for Chinese text.
- Use two or three short title lines when needed. Keep the user's exact title text if supplied; otherwise write a concise English product hook.
- Use cover title font size `80`. If text does not fit safely, shorten it or split it into two lines; do not reduce the font size. Do not add badge text unless the user asks.
- Do not make decorative cards, border frames, complex layouts, extra icons, divider lines, or center-box poster designs.

### Captions

- Captions must also stay inside the safe area. Do not place them too low where YouTube Shorts UI can cover them.
- Captions should appear only at key moments, not throughout the whole video.
- Use two lines when needed; keep phrases short.
- Do not reduce the approved caption font sizes just to fit. Shorten the wording or split into two lines instead.
- Approved caption font size: `80` on every line. Shorten the wording or split it into two lines instead of reducing the size.
- First line: white. Second line: light yellow `#fff4b0`.
- No background boxes or panels behind captions.
- Suggested placement for 1080x1920: first line around `y=1040`, second line around `y=1140`, centered with `x=(w-text_w)/2`.

## Publishing Copy and Tags

After every delivered video or batch, produce a matching Word document (`.docx`) in `/Volumes/video/剪辑输出`; do not wait for the user to remind you. For batches, include one clearly separated entry per video and keep each entry on one page when practical. Do not include the literal label `Hashtags:` before platform hashtags; put the hashtag line directly after the related title, description, caption, or post so it can be copied without deleting a label. Add a clickable local link to each final MP4; use an ASCII display label if the document renderer cannot display Chinese paths. Render the DOCX to page images and visually inspect every page before delivery.

For each video, include:

- Final video path.
- Product/content summary in English.
- YouTube title, description, hashtags, and YouTube Studio tags.
- Instagram Reel caption and hashtags.
- LinkedIn post and hashtags.

Write platform copy in English by default, directly related to the exact product and action shown. Do not use generic claims that the footage does not support. Keep text practical and B2B-oriented for machinery buyers, dealers, contractors, facility teams, municipal users, or rental companies as appropriate.

Use these platform constraints unless the user gives newer instructions:

- YouTube title: keep under 100 characters.
- YouTube description: keep under 5,000 characters.
- YouTube hashtags: use a small set of directly related hashtags, normally 3, and avoid hashtag stuffing.
- YouTube Studio tags: use concise keyword phrases for product names, applications, and likely search variants; do not paste large tag blocks into the description.
- Instagram: keep the Reel caption short with the product/action hook first; use 3-5 highly relevant hashtags.
- LinkedIn: keep the post professional and under 3,000 characters; use practical application context and a small number of industry hashtags.

## Rendering Pattern

Use FFmpeg or the local video-editing workflow. A typical video filter shape:

```text
scale=1080:1920:force_original_aspect_ratio=increase,
crop=1080:1920,
setsar=1,
fps=30,
eq=contrast=1.06:saturation=1.08:brightness=0.01,
unsharp=5:5:0.75:3:3:0.35,
format=yuv420p
```

For horizontal-to-vertical inserts, use a centered full-width horizontal foreground over a blurred/enlarged source background with subtle top/bottom darkening. A typical filter shape:

```text
[src]scale=1080:-1[fg];
[src]scale=1080:1920:force_original_aspect_ratio=increase,
crop=1080:1920,
boxblur=24:2,
drawbox=x=0:y=0:w=1080:h=1920:color=black@0.18:t=fill[bg];
[bg][fg]overlay=(W-w)/2:(H-h)/2
```

Use `drawtext` with centered text and a thin black outline. Cover title text should use the TK Shorts Editor cover preset: lower translucent black editorial panel, narrow pale-yellow left accent bar, `#FFF7C7` title, and a visible 1-second intro by default. Captions should stay without background boxes unless the user explicitly changes that rule. Keep the font sizes above unless the user explicitly changes them.

Do not add BGM by default. Prefer low, clean original machine audio when it helps the product feel real; otherwise use silence. Never add synthetic music beds or royalty-safe tracks unless the user explicitly requests music.

### Final MP4 First-Frame Rule

The delivered MP4 must open directly on the designed cover, not a black frame. The first decoded video frame must be the cover, the cover must remain visible at `0.5s`, and the first video packet must start at `0.000000`.

When finalizing with FFmpeg, avoid MP4 edit-list or audio-leading gaps that make some players show black before video starts. If needed, finish with options such as `-use_editlist 0`, `-avoid_negative_ts disabled`, `-muxpreload 0`, `-muxdelay 0`, and `-movflags +faststart`. If using silence instead of machine audio, add silent AAC only after the video timeline is normalized, then recheck both streams start at `0.000000`.

If `ffprobe` shows the video stream or first video packet starting later than `0.000000`, such as `0.023000`, do not deliver that file. Re-encode/remux it until the video stream, audio stream, and first video packet all start at `0.000000`, then extract and visually inspect the first frame.

## Used Material Record

After rendering, write a CSV in `/Volumes/video/剪辑输出/素材使用记录`, for example:

```text
已用素材片段_批量42-51_YYYYMMDD.csv
```

Include columns:

```text
日期,成片路径,产品,素材路径,开始秒,结束秒,备注
```

Record every source segment actually used, with exact source path and start/end seconds. Mark every row with `已剪过下次避开` so later batches can reliably exclude it.

## Quality Check

Before final response:

1. Run `ffprobe` or equivalent to confirm each final MP4 is the intended orientation (`1080x1920` for all-vertical or mixed-orientation edits, or `1920x1080` for all-horizontal/intentionally horizontal edits), `30fps`, H.264 video, AAC audio, and 15-45 seconds. Also confirm the video stream and first video packet start at `0.000000` so the file opens directly on the cover instead of a black frame.
2. Generate and inspect sample frames for the cover at `0.0s` and `0.5s`, plus at least one caption moment. Confirm the first frame and 0.5s frame are still the cover, title/captions are not clipped, the cover uses the TK Shorts Editor lower-panel preset with pale yellow `#FFF7C7`, captions have no background box, the title panel is horizontally centered, and the chosen cover frame is clean and product-focused.
3. Scan the body for unintended black or near-black transition frames and embedded logo/title cards, using `blackframe`/`blackdetect` or a dense timeline contact sheet when needed. Remove those intervals and re-render before delivery.
4. For any horizontal clip converted into vertical, inspect sample frames to confirm the product is not cropped off, the foreground remains sharp, and the top/bottom background uses the semi-transparent blurred/softened fill rather than plain black bars.
5. Confirm the output folder contains final videos directly, with no unwanted product subfolders.
6. Confirm filenames do not contain `YouTubeShort`.
7. If non-talking footage was requested, confirm no selected source path contains `口播`, no presenter addresses the camera, no speech subtitles remain, and the final audio contains no speech. Use silent AAC when any source audio may contain dialogue.
8. Confirm the matching publishing-copy DOCX exists, contains one entry for every final video, omits the literal `Hashtags:` label, and passed rendered-page visual QA.
9. Report final video paths, the publishing-copy DOCX path, and the material-use CSV path to the user.
