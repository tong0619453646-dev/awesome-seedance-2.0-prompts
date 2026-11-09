<div align="center">

<a href="https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-seedance-2.0-prompts"><img src="assets/banner.jpg" alt="Awesome Seedance 2.0 提示詞" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-175_cases-111111)](README_zh-TW.md#menu)
[![Try Seedance 2.0 on APIKO](https://img.shields.io/badge/Try_Seedance_2.0-on_APIKO-4F46E5)](https://apiko.app/zh-tw/models/seedance-2.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seedance-2.0-prompts&utm_content=model_try)
[![Seedance 2.0 API docs](https://img.shields.io/badge/Seedance_2.0-API_docs-111111)](https://apiko.app/zh-tw/docs/api-manual/video-series/seedance/seedance-2.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seedance-2.0-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-Current-111111)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome Seedance 2.0 提示詞

<a id="introduction"></a>
## 🌟 簡介

**Seedance 2.0 提示詞：175 個可複製的影片提示詞，每個都附上生成的片段，涵蓋動漫、黏土動畫、動作、美妝廣告、Vlog 和 DIY 縮時。**

每個提示詞都附上它生成的影片：直接複製，或在模型頁開啟，長度和畫面比例已照範例設好。

線上搜尋與篩選： [apiko.app/seedance-2-0-prompts](https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-seedance-2.0-prompts&utm_content=intro).

> [!NOTE]
> 提示詞保持作者發布時的原文，所以大多是英文；標題與簡介由我們撰寫。每則都署名作者並連結原帖。

<a id="quick-start"></a>
## 🚀 快速開始

**網頁上用：** 每則都有「在 APIKO 執行」連結，會在 [apiko.app](https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seedance-2.0-prompts&utm_content=browser) 開啟這則範例；點「使用」，提示詞就會填進 Seedance 2.0 試用台。

**用 API：** 先建立 [APIKO API 金鑰](https://apiko.app/zh-tw/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seedance-2.0-prompts&utm_content=api_key)，再建立任務並輪詢，直到影片生成完成。

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

介面: `POST https://api.apiko.app/v1/videos` (建立任務) · `GET https://api.apiko.app/v1/videos/{id}` (查詢狀態與結果)

<a id="how-to-write"></a>
## ✍️ Seedance 2.0 提示詞怎麼寫

本頁提示詞裡反覆出現的四種結構。

- **按秒分段** · `0–3 秒：…… 3–7 秒：…… 7–15 秒：……` — 很多提示詞把片段按秒切開，每段只寫一個動作，15 秒以內的順序就不會亂。
- **寫明用什麼拍** · `機型或格式 + 怎麼動 + 誰拿著` — DV、16mm、伸直手臂拿的手機或固定三腳架：寫清是什麼在拍，畫面質感和晃動感就一起定了。
- **幫參考素材編號** · `@Image1 = 角色。@Image2 = 商品。保留：…… 改變：……` — 參考類提示詞照上傳順序稱呼檔案，並寫明每個檔案能改什麼，人臉和商品就能保持一致。
- **寫清變化過程** · `起始狀態 → 觸發 → 結果` — DIY、變裝和怪獸類提示詞寫出變化前、變化那一刻和結果，Seedance 2.0 會一步步照做。

**從範例裡看得出**

- **長劇本要拆成幾段。** Seedance 2.0 每次生成 4 到 15 秒，比這更長的卡片是分幾次生成再剪在一起的。
- **動畫風格很穩定。** 把風格寫在最前面，黏土、水墨、日式動畫和手繪定格能整段保持一致。
- **把聲音寫上。** 影片會一起生成聲音；寫明 ASMR 質感、音樂或台詞，就聽得到。
- **寫明不要什麼。** Vlog 和 DIY 提示詞排除 CGI、配樂和字幕，片段才像真實素材。
- **要精確構圖就用首幀。** 產品和格局圖類卡片從上傳的圖片開始，畫面動起來之前構圖就定了。

<a id="menu"></a>
## 📑 目錄

- [⭐ 精選](#featured) (6)
- [🎬 電影感](prompts/cinematic_zh-TW.md) (20) — 靠一個鏡頭創意撐起的單場景：像人一樣的動物、微距、超現實瞬間。
- [🥊 動作](prompts/action_zh-TW.md) (25) — 打鬥、追逐和特技，從武俠對決到機車逃亡。
- [• 劇情與愛情](prompts/drama_zh-TW.md) (7) — 關於人的小場景：告別、心動、疲憊的一天。
- [🐉 奇幻與科幻](prompts/fantasy-scifi_zh-TW.md) (24) — 巨龍、機甲、怪獸和魔法，場面都很大。
- [🧸 動畫](prompts/animation_zh-TW.md) (34) — 日式動畫、3D 卡通、黏土、水墨和手繪定格。
- [• Vlog 與生活](prompts/vlog-lifestyle_zh-TW.md) (31) — 手機和 DV 質感的素材、旅行漫步和日常慢鏡頭。
- [👟 產品、美妝與時尚](prompts/product_zh-TW.md) (21) — 保養、珠寶、食品和服裝廣告，很多是 UGC 風格。
- [• DIY 與縮時](prompts/craft-timelapse_zh-TW.md) (13) — 環氧地坪、翻修、手作和烹飪，從開始拍到完成。
- [❓ 常見問題](#faq)
- [🔗 相關連結](#related)

<a id="featured"></a>
## ⭐ 精選

<a id="cinematic-01"></a>
### 1. 從車裡拍到兩隻貓騎紅色小機車

作者 [@Just_sharon7](https://x.com/Just_sharon7) · 15 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-01#cinematic-01)** · [原帖](https://x.com/Just_sharon7/status/2084901309988425731)

<a href="https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-01#cinematic-01"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/cinematic-01.webp" width="560" alt="從車裡拍到兩隻貓騎紅色小機車 – Seedance 2.0"></a>

**提示詞:**

```text
A highly realistic cinematic shot filmed from inside a moving car looking out the side window, capturing two cats riding a small red mini motorcycle on a suburban road. An orange tabby cat is driving, gripping the handlebars with both front paws, mouth open in a surprised or determined expression, ears slightly back from the wind. Behind it, a fluffy pure white cat is perched as a passenger, holding up a shiny empty metal food bowl with one paw while the other rests for balance, mouth wide open as if meowing or yelling. The motorcycle is a compact red mini bike with a visible headlight, black tires, and a small license plate area. Background shows a typical American suburban street with houses, trees, power lines, a concrete barrier, other cars passing, and a partly cloudy sky. Dynamic motion blur on the background to convey speed, natural daylight, humorous and absurd vibe.
```

<a id="fantasy-scifi-04"></a>
### 56. 女武士與白龍擊碎熔岩星球

作者 [@Zyrellix](https://x.com/Zyrellix) · 30 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=fantasy-scifi-04#fantasy-scifi-04)** · [原帖](https://x.com/Zyrellix/status/2092121112746287527)

<a href="https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=fantasy-scifi-04#fantasy-scifi-04"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/fantasy-scifi-04.webp" width="560" alt="女武士與白龍擊碎熔岩星球 – Seedance 2.0"></a>

**提示詞:**

```text
A cinematic dark fantasy epic video in 8K resolution. Extreme macro close-up of a female warrior's eye, iris reflecting a burning molten celestial orb swirling inside dark storm clouds. Low-angle tracking shot as an East Asian female warrior clad in sleek black leather-and-steel armor walks through shallow water carrying an ornate key. She steps onto a circular stone platform engraved with glowing golden runes, surrounded by mist, cascading waterfalls, and ancient temple ruins. Above, a colossal magma-veined celestial sphere looms within a vortex of swirling clouds. She inserts the key into a moss-covered stone altar, triggering a massive circular runic array that launches vertical high-pressure water geysers into the sky. A giant, majestic white serpentine dragon with fiery orange eyes emerges from the mist. The warrior extends her hand as her eyes glow bright golden, establishing a powerful magical bond. The dragon turns upwards, soaring into the sky and unleashing a beam of pure radiant white energy directly into the celestial orb, causing it to shatter into shockwaves of blinding light. Epic cinematic scale, volumetric fog, photorealistic visual effects, Unreal Engine 5 render style, dark gray and golden color grading, hyper-detailed.
```

<a id="animation-19"></a>
### 95. 黏土版奧德修斯遇獨眼巨人

作者 [@miilesus](https://x.com/miilesus) · 15 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=animation-19#animation-19)** · [原帖](https://x.com/miilesus/status/2080744222571848176)

<a href="https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=animation-19#animation-19"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/animation-19.webp" width="560" alt="黏土版奧德修斯遇獨眼巨人 – Seedance 2.0"></a>

**提示詞:**

```text
Create a 3D claymation style animation of a cute caricature of Odysseus, wearing weathered bronze armor, a deep red cape, leather sandals, and windswept hair, sailing alone across a miniature stormy sea in a tiny wooden ship. A gigantic Cyclops suddenly rises from the water and reaches toward him. Odysseus calmly pulls out an enormous olive, launches it into the Cyclops’s mouth with a tiny catapult, and watches as the confused giant begins chewing happily. The storm instantly clears, the Cyclops gives him a thumbs up, and Odysseus takes a triumphant selfie with the giant in the background. Smooth expressive clay animation, epic orchestral music mixed with playful sound effects, handcrafted textures, cinematic lighting, mythological scale, absurd humor, viral energy.
```

<a id="craft-timelapse-11"></a>
### 173. 舊輪胎改成無限鏡茶几

作者 [@Ruslanchain](https://x.com/Ruslanchain) · 24 秒 · 9:16 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=craft-timelapse-11#craft-timelapse-11)** · [原帖](https://x.com/Ruslanchain/status/2118023608815571361)

<a href="https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=craft-timelapse-11#craft-timelapse-11"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/craft-timelapse-11.webp" width="320" alt="舊輪胎改成無限鏡茶几 – Seedance 2.0"></a>

**提示詞:**

```text
Vertical DIY video, photorealistic style. A man in a black baseball cap, gray t-shirt and black cargo pants kneels on a concrete patio beside a red brick wall with potted plants. He sprays foaming cleaner onto a filthy mud-caked car tire, scrubs it with a brush until white foam drips down, then wipes the tire spotless black with a cloth. He fits a round plywood disc inside the tire, drives screws with a yellow cordless drill, attaches three angled wooden legs, flips the tire upright into a sturdy table base and sets a round glass top on it. He coils a warm white LED strip around the inner rim, places the glass back on top, and plugs in a power cord from the side of the tire so the LEDs glow through the glass. The scene transitions to a cozy living room at night with a beige sectional sofa, a floor lamp and a round jute rug, where the glowing tire coffee table now sits as the centerpiece. The camera slowly pushes in on the tabletop, revealing a hypnotic infinite mirror tunnel of repeating golden LED rings receding into darkness. Warm ambient lighting, smooth camera movements, satisfying transformation montage, high detail, realistic textures and reflections.
```

<a id="action-02"></a>
### 22. 珠寶店裡的武打戲

作者 [@mimu_ai1](https://x.com/mimu_ai1) · 10 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=action-02#action-02)** · [原帖](https://x.com/mimu_ai1/status/2091215411341930633)

<a href="https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=action-02#action-02"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/action-02.webp" width="560" alt="珠寶店裡的武打戲 – Seedance 2.0"></a>

**提示詞:**

```text
A dynamic, cinematic action sequence inside a luxury jewelry boutique at night. A confident young woman with long dark hair, olive skin, and sharp green eyes is the hero. She wears an elegant emerald silk evening gown and gold earrings. Three masked thieves in black tactical gear attempt a robbery, and she single-handedly defeats them with fast, precise martial arts choreography. She vaults over glass display cases, shattering them in dramatic slow motion as diamonds, pearls, and glass shards scatter and sparkle through the air like rain, catching warm spotlight beams. She slides across a marble counter, throws one attacker into a shelf of watches, and disarms the last with a spinning kick. At the end, she stands calm amid the glittering wreckage, picks up a single diamond ring, examines it in the light, and looks directly into the camera with a faint smile. Dynamic handheld camera, whip pans, slow-motion inserts, moody warm lighting with deep shadows, realistic physics, high production value, cinematic style, 4K.
```

<a id="cinematic-15"></a>
### 15. 無底峽谷上逐漸消散的吊橋

作者 [@zyvaoz](https://x.com/zyvaoz) · 15 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-15#cinematic-15)** · [原帖](https://x.com/zyvaoz/status/2081398750996746385)

<a href="https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-15#cinematic-15"><img src="https://media.apiko.app/prompts/seedance-2-0-prompts/cinematic-15.webp" width="560" alt="無底峽谷上逐漸消散的吊橋 – Seedance 2.0"></a>

**提示詞:**

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

- **[🎬 查看「電影感」全部 20 則](prompts/cinematic_zh-TW.md)**
- **[🥊 查看「動作」全部 25 則](prompts/action_zh-TW.md)**
- **[• 查看「劇情與愛情」全部 7 則](prompts/drama_zh-TW.md)**
- **[🐉 查看「奇幻與科幻」全部 24 則](prompts/fantasy-scifi_zh-TW.md)**
- **[🧸 查看「動畫」全部 34 則](prompts/animation_zh-TW.md)**
- **[• 查看「Vlog 與生活」全部 31 則](prompts/vlog-lifestyle_zh-TW.md)**
- **[👟 查看「產品、美妝與時尚」全部 21 則](prompts/product_zh-TW.md)**
- **[• 查看「DIY 與縮時」全部 13 則](prompts/craft-timelapse_zh-TW.md)**

<a id="faq"></a>
## ❓ 常見問題

<details>
<summary><b>這些 Seedance 2.0 提示詞可以免費用嗎？</b></summary>

可以複製、修改和執行。提示詞和影片歸卡片標註的創作者所有，商用影片前請先看原文說明。

</details>

<details>
<summary><b>Seedance 2.0 影片最長多久？</b></summary>

每次 4 到 15 秒，480p、720p 或 1080p。本頁更長的卡片由多段組成。

</details>

<details>
<summary><b>支援哪些畫面比例？</b></summary>

16:9、9:16、1:1、4:3、3:4 和 21:9。

</details>

<details>
<summary><b>能用參考圖、參考影片和參考音訊嗎？</b></summary>

可以：最多 9 張參考圖、3 段參考影片（合計 15 秒）和 3 段參考音訊，照上傳順序稱為 @Image1、@Video1、@Audio1。首幀（可加尾幀）不能和參考素材同時使用。

</details>

<details>
<summary><b>提示詞最長多少字？</b></summary>

最多 20000 字元。台詞、聲音和運鏡都寫在提示詞裡。

</details>

<details>
<summary><b>選 Seedance 2.0 還是 2.5？</b></summary>

Seedance 2.5 最長 30 秒，參考素材更多（30 張圖、10 段影片、10 段音訊）；15 秒以內的創意用 Seedance 2.0 大多就夠。兩者每秒價格見各自的模型頁。

</details>

<details>
<summary><b>為什麼我生成的和範例不一樣？</b></summary>

每次生成結果都不同，作者也可能用了參考素材、其他解析度或 Seedance 2.0 Fast。一次只改一處細節來比較。

</details>

<details>
<summary><b>怎麼透過 API 執行提示詞？</b></summary>

向 /v1/videos 發 POST，model 填 seedance-2.0，prompt 填提示詞，輪詢任務後下載影片。API 文件列出了全部欄位。

</details>


<a id="related"></a>
## 🔗 相關連結

- [Seedance 2.0 提示詞 · apiko.app](https://apiko.app/zh-tw/seedance-2-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [試用 Seedance 2.0](https://apiko.app/zh-tw/models/seedance-2.0?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Seedance 2.0 API 文件](https://apiko.app/zh-tw/docs/api-manual/video-series/seedance/seedance-2.0?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Seedance 2.5 提示詞](https://apiko.app/zh-tw/seedance-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Kling 4.0 提示詞](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [全部提示詞庫](https://apiko.app/zh-tw/prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [APIKO API 程式碼範例](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**更多提示詞合集**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_zh-TW.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_zh-TW.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_zh-TW.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_zh-TW.md)

<a id="license"></a>
## 📄 授權與出處

提示詞和影片歸每張卡片標註的創作者所有，卡片可連到 X 上的原文。標題、簡介、譯文與生成腳本採用 [CC BY 4.0](LICENSE) 授權。

如果這份合集幫你省了時間，按個 ⭐ 能讓更多人看到。
