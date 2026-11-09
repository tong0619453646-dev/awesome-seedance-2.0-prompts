<div align="center">

<a href="https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-seedance-2.0-prompts"><img src="assets/banner.jpg" alt="Awesome Seedance 2.0 提示词" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-175_cases-111111)](README_zh-CN.md#menu)
[![Try Seedance 2.0 on APIKO](https://img.shields.io/badge/Try_Seedance_2.0-on_APIKO-4F46E5)](https://apiko.app/zh/models/seedance-2.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seedance-2.0-prompts&utm_content=model_try)
[![Seedance 2.0 API docs](https://img.shields.io/badge/Seedance_2.0-API_docs-111111)](https://apiko.app/zh/docs/api-manual/video-series/seedance/seedance-2.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seedance-2.0-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-Current-111111)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome Seedance 2.0 提示词

<a id="introduction"></a>
## 🌟 简介

**Seedance 2.0 提示词：175 条可复制的视频提示词，每条附生成的片段，涵盖动漫、黏土动画、动作、美妆广告、Vlog 和 DIY 延时。**

每条提示词都附上它生成的视频：直接复制，或在模型页打开，时长和画幅已按示例设好。

在线搜索和筛选： [apiko.app/seedance-2-0-prompts](https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-seedance-2.0-prompts&utm_content=intro).

> [!NOTE]
> 提示词保持作者发布时的原文，所以大多是英文；标题和简介是我们写的。每条都署名作者并链接原帖。

<a id="quick-start"></a>
## 🚀 快速开始

**网页上用：** 每条都有「在 APIKO 运行」链接，会在 [apiko.app](https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seedance-2.0-prompts&utm_content=browser) 打开这条示例；点「使用」，提示词就会填进 Seedance 2.0 试用台。

**用 API：** 先创建 [APIKO API Key](https://apiko.app/zh/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seedance-2.0-prompts&utm_content=api_key)，再创建任务并轮询，直到视频生成完成。

```bash
export APIKO_API_KEY="your_key_here"

TASK_ID=$(curl -s https://api.apiko.app/v1/videos \
  -H "Authorization: Bearer $APIKO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "model": "seedance-2.0",
  "duration": 5,
  "resolution": "720p",
  "aspect_ratio": "16:9",
  "prompt": "A paper boat drifting across a calm lake at sunrise, slow dolly-in, soft wind and birdsong."
}' | python3 -c 'import json,sys; print(json.load(sys.stdin)["id"])')

while :; do
  TASK=$(curl -s https://api.apiko.app/v1/videos/$TASK_ID \
    -H "Authorization: Bearer $APIKO_API_KEY")
  printf '%s\n' "$TASK"
  printf '%s' "$TASK" | grep -qE '"status": *"(completed|failed)"|"error": *\{' && break
  sleep 10
done
```

接口: `POST https://api.apiko.app/v1/videos` (创建任务) · `GET https://api.apiko.app/v1/videos/{id}` (查询状态和结果)

<a id="how-to-write"></a>
## ✍️ Seedance 2.0 提示词怎么写

本页提示词里反复出现的四种结构。

- **按秒分段** · `0–3 秒：…… 3–7 秒：…… 7–15 秒：……` — 很多提示词把片段按秒切开，每段只写一个动作，15 秒以内的顺序就不会乱。
- **写明用什么拍** · `机型或格式 + 怎么动 + 谁拿着` — DV、16mm、伸直手臂拿的手机或固定三脚架：写清是什么在拍，画面质感和晃动感就一起定了。
- **给参考素材编号** · `@Image1 = 角色。@Image2 = 商品。保留：…… 改变：……` — 参考类提示词按上传顺序称呼文件，并写明每个文件能改什么，人脸和商品就能保持一致。
- **写清变化过程** · `起始状态 → 触发 → 结果` — DIY、变装和怪兽类提示词写出变化前、变化那一刻和结果，Seedance 2.0 会一步步照做。

**从示例里能看出**

- **长剧本要拆成几段。** Seedance 2.0 每次生成 4 到 15 秒，比这更长的卡片是分几次生成再剪到一起的。
- **动画风格很稳定。** 把风格写在最前面，黏土、水墨、日式动画和手绘定格能整段保持一致。
- **把声音写上。** 视频会一起生成声音；写明 ASMR 质感、音乐或台词，就能听到。
- **写明不要什么。** Vlog 和 DIY 提示词排除 CGI、配乐和字幕，片段才像真实素材。
- **要精确构图就用首帧。** 产品和户型图类卡片从上传的图片开始，画面动起来之前构图就定了。

<a id="menu"></a>
## 📑 目录

- [⭐ 精选](#featured) (6)
- [🎬 电影感](prompts/cinematic_zh-CN.md) (20) — 靠一个镜头创意撑起的单场景：像人一样的动物、微距、超现实瞬间。
- [🥊 动作](prompts/action_zh-CN.md) (25) — 打斗、追逐和特技，从武侠对决到摩托逃亡。
- [• 剧情与爱情](prompts/drama_zh-CN.md) (7) — 关于人的小场景：告别、心动、疲惫的一天。
- [🐉 奇幻与科幻](prompts/fantasy-scifi_zh-CN.md) (24) — 巨龙、机甲、怪兽和魔法，场面都很大。
- [🧸 动画](prompts/animation_zh-CN.md) (34) — 日式动画、3D 卡通、黏土、水墨和手绘定格。
- [• Vlog 与生活](prompts/vlog-lifestyle_zh-CN.md) (31) — 手机和 DV 质感的素材、旅行漫步和日常慢镜头。
- [👟 产品、美妆与时尚](prompts/product_zh-CN.md) (21) — 护肤、珠宝、食品和服装广告，很多是 UGC 风格。
- [• DIY 与延时](prompts/craft-timelapse_zh-CN.md) (13) — 环氧地坪、翻新、手作和烹饪，从开始拍到完成。
- [❓ 常见问题](#faq)
- [🔗 相关链接](#related)

<a id="featured"></a>
## ⭐ 精选

<a id="cinematic-01"></a>
### 1. 从车里拍到两只猫骑红色小摩托

作者 [@Just_sharon7](https://x.com/Just_sharon7) · 15 秒 · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-01#cinematic-01)** · [原帖](https://x.com/Just_sharon7/status/2084901309988425731)

<a href="https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-01#cinematic-01"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/cinematic-01.webp" width="560" alt="从车里拍到两只猫骑红色小摩托 – Seedance 2.0"></a>

**提示词:**

```text
A highly realistic cinematic shot filmed from inside a moving car looking out the side window, capturing two cats riding a small red mini motorcycle on a suburban road. An orange tabby cat is driving, gripping the handlebars with both front paws, mouth open in a surprised or determined expression, ears slightly back from the wind. Behind it, a fluffy pure white cat is perched as a passenger, holding up a shiny empty metal food bowl with one paw while the other rests for balance, mouth wide open as if meowing or yelling. The motorcycle is a compact red mini bike with a visible headlight, black tires, and a small license plate area. Background shows a typical American suburban street with houses, trees, power lines, a concrete barrier, other cars passing, and a partly cloudy sky. Dynamic motion blur on the background to convey speed, natural daylight, humorous and absurd vibe.
```

<a id="fantasy-scifi-04"></a>
### 56. 女武士与白龙击碎熔岩星球

作者 [@Zyrellix](https://x.com/Zyrellix) · 30 秒 · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=fantasy-scifi-04#fantasy-scifi-04)** · [原帖](https://x.com/Zyrellix/status/2092121112746287527)

<a href="https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=fantasy-scifi-04#fantasy-scifi-04"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/fantasy-scifi-04.webp" width="560" alt="女武士与白龙击碎熔岩星球 – Seedance 2.0"></a>

**提示词:**

```text
A cinematic dark fantasy epic video in 8K resolution. Extreme macro close-up of a female warrior's eye, iris reflecting a burning molten celestial orb swirling inside dark storm clouds. Low-angle tracking shot as an East Asian female warrior clad in sleek black leather-and-steel armor walks through shallow water carrying an ornate key. She steps onto a circular stone platform engraved with glowing golden runes, surrounded by mist, cascading waterfalls, and ancient temple ruins. Above, a colossal magma-veined celestial sphere looms within a vortex of swirling clouds. She inserts the key into a moss-covered stone altar, triggering a massive circular runic array that launches vertical high-pressure water geysers into the sky. A giant, majestic white serpentine dragon with fiery orange eyes emerges from the mist. The warrior extends her hand as her eyes glow bright golden, establishing a powerful magical bond. The dragon turns upwards, soaring into the sky and unleashing a beam of pure radiant white energy directly into the celestial orb, causing it to shatter into shockwaves of blinding light. Epic cinematic scale, volumetric fog, photorealistic visual effects, Unreal Engine 5 render style, dark gray and golden color grading, hyper-detailed.
```

<a id="animation-19"></a>
### 95. 黏土版奥德修斯遇独眼巨人

作者 [@miilesus](https://x.com/miilesus) · 15 秒 · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=animation-19#animation-19)** · [原帖](https://x.com/miilesus/status/2080744222571848176)

<a href="https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=animation-19#animation-19"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/animation-19.webp" width="560" alt="黏土版奥德修斯遇独眼巨人 – Seedance 2.0"></a>

**提示词:**

```text
Create a 3D claymation style animation of a cute caricature of Odysseus, wearing weathered bronze armor, a deep red cape, leather sandals, and windswept hair, sailing alone across a miniature stormy sea in a tiny wooden ship. A gigantic Cyclops suddenly rises from the water and reaches toward him. Odysseus calmly pulls out an enormous olive, launches it into the Cyclops’s mouth with a tiny catapult, and watches as the confused giant begins chewing happily. The storm instantly clears, the Cyclops gives him a thumbs up, and Odysseus takes a triumphant selfie with the giant in the background. Smooth expressive clay animation, epic orchestral music mixed with playful sound effects, handcrafted textures, cinematic lighting, mythological scale, absurd humor, viral energy.
```

<a id="craft-timelapse-11"></a>
### 173. 旧轮胎改成无限镜茶几

作者 [@Ruslanchain](https://x.com/Ruslanchain) · 24 秒 · 9:16 · **[▶ 在 APIKO 运行](https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=craft-timelapse-11#craft-timelapse-11)** · [原帖](https://x.com/Ruslanchain/status/2118023608815571361)

<a href="https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=craft-timelapse-11#craft-timelapse-11"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/craft-timelapse-11.webp" width="320" alt="旧轮胎改成无限镜茶几 – Seedance 2.0"></a>

**提示词:**

```text
Vertical DIY video, photorealistic style. A man in a black baseball cap, gray t-shirt and black cargo pants kneels on a concrete patio beside a red brick wall with potted plants. He sprays foaming cleaner onto a filthy mud-caked car tire, scrubs it with a brush until white foam drips down, then wipes the tire spotless black with a cloth. He fits a round plywood disc inside the tire, drives screws with a yellow cordless drill, attaches three angled wooden legs, flips the tire upright into a sturdy table base and sets a round glass top on it. He coils a warm white LED strip around the inner rim, places the glass back on top, and plugs in a power cord from the side of the tire so the LEDs glow through the glass. The scene transitions to a cozy living room at night with a beige sectional sofa, a floor lamp and a round jute rug, where the glowing tire coffee table now sits as the centerpiece. The camera slowly pushes in on the tabletop, revealing a hypnotic infinite mirror tunnel of repeating golden LED rings receding into darkness. Warm ambient lighting, smooth camera movements, satisfying transformation montage, high detail, realistic textures and reflections.
```

<a id="action-02"></a>
### 22. 珠宝店里的武打戏

作者 [@mimu_ai1](https://x.com/mimu_ai1) · 10 秒 · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=action-02#action-02)** · [原帖](https://x.com/mimu_ai1/status/2091215411341930633)

<a href="https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=action-02#action-02"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/action-02.webp" width="560" alt="珠宝店里的武打戏 – Seedance 2.0"></a>

**提示词:**

```text
A dynamic, cinematic action sequence inside a luxury jewelry boutique at night. A confident young woman with long dark hair, olive skin, and sharp green eyes is the hero. She wears an elegant emerald silk evening gown and gold earrings. Three masked thieves in black tactical gear attempt a robbery, and she single-handedly defeats them with fast, precise martial arts choreography. She vaults over glass display cases, shattering them in dramatic slow motion as diamonds, pearls, and glass shards scatter and sparkle through the air like rain, catching warm spotlight beams. She slides across a marble counter, throws one attacker into a shelf of watches, and disarms the last with a spinning kick. At the end, she stands calm amid the glittering wreckage, picks up a single diamond ring, examines it in the light, and looks directly into the camera with a faint smile. Dynamic handheld camera, whip pans, slow-motion inserts, moody warm lighting with deep shadows, realistic physics, high production value, cinematic style, 4K.
```

<a id="cinematic-15"></a>
### 15. 无底峡谷上逐渐消散的吊桥

作者 [@zyvaoz](https://x.com/zyvaoz) · 15 秒 · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-15#cinematic-15)** · [原帖](https://x.com/zyvaoz/status/2081398750996746385)

<a href="https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-15#cinematic-15"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/cinematic-15.webp" width="560" alt="无底峡谷上逐渐消散的吊桥 – Seedance 2.0"></a>

**提示词:**

```text
0-3 sec:
A vast canyon with no visible bottom. A rope bridge spans the gap, wooden planks suspended on frayed ropes. A lone traveler steps onto the first plank.

3-6 sec:
The traveler takes a step. Behind them, the plank they left dissolves into mist. The ropes unravel silently. The bridge shortens. No return possible.

6-9 sec:
More steps. Each plank crumbles after use. The traveler glances back. Nothing but empty air. They grip the rope rail tighter. The end grows closer.

9-12 sec:
The traveler runs now. Planks dissolve faster. The bridge disintegrates behind them in a cascading wave. The far edge approaches. One final leap.

12-15 sec:
The traveler lands on solid ground. They turn. The entire bridge is gone. Only the two rope stumps remain, swaying over the void. Fade to black.

Sound: Wood creak, plank snap, rope fray, running footsteps, landing thud, silence.
```

- **[🎬 查看「电影感」全部 20 条](prompts/cinematic_zh-CN.md)**
- **[🥊 查看「动作」全部 25 条](prompts/action_zh-CN.md)**
- **[• 查看「剧情与爱情」全部 7 条](prompts/drama_zh-CN.md)**
- **[🐉 查看「奇幻与科幻」全部 24 条](prompts/fantasy-scifi_zh-CN.md)**
- **[🧸 查看「动画」全部 34 条](prompts/animation_zh-CN.md)**
- **[• 查看「Vlog 与生活」全部 31 条](prompts/vlog-lifestyle_zh-CN.md)**
- **[👟 查看「产品、美妆与时尚」全部 21 条](prompts/product_zh-CN.md)**
- **[• 查看「DIY 与延时」全部 13 条](prompts/craft-timelapse_zh-CN.md)**

<a id="faq"></a>
## ❓ 常见问题

<details>
<summary><b>这些 Seedance 2.0 提示词可以免费用吗？</b></summary>

可以复制、修改和运行。提示词和视频归卡片标注的创作者所有，商用视频前请先看原帖说明。

</details>

<details>
<summary><b>Seedance 2.0 视频最长多久？</b></summary>

每次 4 到 15 秒，480p、720p 或 1080p。本页更长的卡片由多段拼成。

</details>

<details>
<summary><b>支持哪些画幅？</b></summary>

16:9、9:16、1:1、4:3、3:4 和 21:9。

</details>

<details>
<summary><b>能用参考图、参考视频和参考音频吗？</b></summary>

可以：最多 9 张参考图、3 段参考视频（合计 15 秒）和 3 段参考音频，按上传顺序称为 @Image1、@Video1、@Audio1。首帧（可加尾帧）不能和参考素材同时使用。

</details>

<details>
<summary><b>提示词最长多少字？</b></summary>

最多 20000 字符。台词、声音和运镜都写在提示词里。

</details>

<details>
<summary><b>选 Seedance 2.0 还是 2.5？</b></summary>

Seedance 2.5 最长 30 秒，参考素材更多（30 张图、10 段视频、10 段音频）；15 秒以内的创意用 Seedance 2.0 大多就够。两者每秒价格见各自的模型页。

</details>

<details>
<summary><b>为什么我生成的和示例不一样？</b></summary>

每次生成结果都不同，作者也可能用了参考素材、其他分辨率或 Seedance 2.0 Fast。一次只改一处细节来对比。

</details>

<details>
<summary><b>怎么通过 API 运行提示词？</b></summary>

向 /v1/videos 发 POST，model 填 seedance-2.0，prompt 填提示词，轮询任务后下载视频。API 文档列出了全部字段。

</details>


<a id="related"></a>
## 🔗 相关链接

- [Seedance 2.0 提示词 · apiko.app](https://apiko.app/zh/seedance-2-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [试用 Seedance 2.0](https://apiko.app/zh/models/seedance-2.0?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Seedance 2.0 API 文档](https://apiko.app/zh/docs/api-manual/video-series/seedance/seedance-2.0?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Seedance 2.5 提示词](https://apiko.app/zh/seedance-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Kling 4.0 提示词](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [全部提示词库](https://apiko.app/zh/prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [APIKO API 代码示例](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**更多提示词合集**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_zh-CN.md)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_zh-CN.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_zh-CN.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_zh-CN.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_zh-CN.md)

<a id="license"></a>
## 📄 许可与出处

提示词和视频归每张卡片标注的创作者所有，卡片可跳转到 X 上的原帖。标题、简介、译文和生成脚本采用 [CC BY 4.0](LICENSE) 许可。

如果这份合集帮你省了时间，点个 ⭐ 能让更多人看到。
