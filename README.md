<div align="center">

<a href="https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-seedance-2.0-prompts"><img src="assets/banner.jpg" alt="Awesome Seedance 2.0 Prompts" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-175_cases-111111)](README.md#menu)
[![Try Seedance 2.0 on APIKO](https://img.shields.io/badge/Try_Seedance_2.0-on_APIKO-4F46E5)](https://apiko.app/models/seedance-2.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seedance-2.0-prompts&utm_content=model_try)
[![Seedance 2.0 API docs](https://img.shields.io/badge/Seedance_2.0-API_docs-111111)](https://apiko.app/docs/api-manual/video-series/seedance/seedance-2.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seedance-2.0-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Current-111111)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome Seedance 2.0 Prompts

<a id="introduction"></a>
## 🌟 Introduction

**Seedance 2.0 prompts: 175 copyable video prompts with the clips they made, from anime and claymation to action, beauty ads, vlogs and DIY time-lapses.**

Each prompt is shown with the clip it produced. Copy it, or open it on the model page with the duration and aspect already set. Every result video plays right here on GitHub.

Search and filter them on [apiko.app/seedance-2-0-prompts](https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-seedance-2.0-prompts&utm_content=intro).

> [!NOTE]
> Each prompt is kept exactly as its author posted it, so most are in English; titles and descriptions are ours. Every case credits the author and links to the original post.

<a id="quick-start"></a>
## 🚀 Quick start

**In the browser:** every case has a **Run on APIKO** link. It opens the example on [apiko.app](https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seedance-2.0-prompts&utm_content=browser); press **Use** there to load the prompt into the Seedance 2.0 playground.

**With the API:** create an [APIKO API key](https://apiko.app/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seedance-2.0-prompts&utm_content=api_key), then create a task and poll it until the video is ready.

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

Endpoints: `POST https://api.apiko.app/v1/videos` (create a task) · `GET https://api.apiko.app/v1/videos/{id}` (read the status and result)

<a id="how-to-write"></a>
## ✍️ How to write a Seedance 2.0 prompt

Four structures that recur in the prompts on this page.

- **Timed beats** · `0–3 s: … 3–7 s: … 7–15 s: …` — Many prompts split the clip into second ranges with one action each, which keeps a 15-second clip in order.
- **Name the camera** · `Camera body or format + how it moves + who holds it` — MiniDV, 16mm, a phone at arm's length or a locked tripod: saying what filmed the scene sets both the look and the shake.
- **Number the references** · `@Image1 = character. @Image2 = product. Keep: … Change: …` — Reference prompts call files by their order and say what each one may change, so faces and products stay the same.
- **Describe the transformation** · `Start state → trigger → end state` — DIY, makeover and creature prompts describe the before, the moment of change and the result, which Seedance 2.0 follows step by step.

**What the examples show**

- **Long scripts are split into clips.** Seedance 2.0 makes 4 to 15 seconds per request. Cards longer than that were made in several runs and edited together.
- **Animation styles hold well.** Claymation, ink wash, anime and hand-painted stop motion keep their look across the whole clip when the style is stated first.
- **Write the sound.** Sound is generated with the video; prompts that name ASMR textures, music or spoken lines get them.
- **Ban what breaks realism.** Vlog and DIY prompts exclude CGI, music and text overlays so the clip passes as real footage.
- **Use a first frame for exact layouts.** Product and blueprint cards start from an uploaded image, which fixes the composition before anything moves.

<a id="menu"></a>
## 📑 Menu

- [⭐ Featured](#featured) (6)
- [🎬 Cinematic](prompts/cinematic.md) (20) — Single scenes with a strong camera idea: animals behaving like people, macro shots, surreal moments.
- [🥊 Action](prompts/action.md) (25) — Fights, chases and stunts, from wuxia duels to motorcycle escapes.
- [• Drama and romance](prompts/drama.md) (7) — Short scenes about people: goodbyes, first glances, a long day at work.
- [🐉 Fantasy and sci-fi](prompts/fantasy-scifi.md) (24) — Dragons, mechs, monsters and magic at full scale.
- [🧸 Animation](prompts/animation.md) (34) — Anime, 3D cartoon, claymation, ink wash and hand-painted stop motion.
- [• Vlogs and lifestyle](prompts/vlog-lifestyle.md) (31) — Phone and MiniDV footage, travel walks and slow everyday moments.
- [👟 Products, beauty and fashion](prompts/product.md) (21) — Skincare, jewelry, food and fashion spots, many in a UGC style.
- [• DIY and time-lapse](prompts/craft-timelapse.md) (13) — Epoxy floors, renovations, handmade objects and cooking from start to finish.
- [❓ FAQ](#faq)
- [🔗 Related](#related)

<a id="featured"></a>
## ⭐ Featured

<a id="cinematic-01"></a>
### 1. Two cats ride a red scooter, filmed from a car

by [@Just_sharon7](https://x.com/Just_sharon7) · 15s · 16:9 · **[▶ Run on APIKO](https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-01#cinematic-01)** · [Original post](https://x.com/Just_sharon7/status/2084901309988425731)

https://github.com/user-attachments/assets/a73e7827-858a-4f85-862a-f39b6bd24fd8

**Prompt:**

```text
A highly realistic cinematic shot filmed from inside a moving car looking out the side window, capturing two cats riding a small red mini motorcycle on a suburban road. An orange tabby cat is driving, gripping the handlebars with both front paws, mouth open in a surprised or determined expression, ears slightly back from the wind. Behind it, a fluffy pure white cat is perched as a passenger, holding up a shiny empty metal food bowl with one paw while the other rests for balance, mouth wide open as if meowing or yelling. The motorcycle is a compact red mini bike with a visible headlight, black tires, and a small license plate area. Background shows a typical American suburban street with houses, trees, power lines, a concrete barrier, other cars passing, and a partly cloudy sky. Dynamic motion blur on the background to convey speed, natural daylight, humorous and absurd vibe.
```

<a id="fantasy-scifi-04"></a>
### 56. A warrior and a white dragon shatter a molten orb

by [@Zyrellix](https://x.com/Zyrellix) · 30s · 16:9 · **[▶ Run on APIKO](https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=fantasy-scifi-04#fantasy-scifi-04)** · [Original post](https://x.com/Zyrellix/status/2092121112746287527)

https://github.com/user-attachments/assets/0b3b595f-e1d6-4881-bbbc-52cc4c1b6977

**Prompt:**

```text
A cinematic dark fantasy epic video in 8K resolution. Extreme macro close-up of a female warrior's eye, iris reflecting a burning molten celestial orb swirling inside dark storm clouds. Low-angle tracking shot as an East Asian female warrior clad in sleek black leather-and-steel armor walks through shallow water carrying an ornate key. She steps onto a circular stone platform engraved with glowing golden runes, surrounded by mist, cascading waterfalls, and ancient temple ruins. Above, a colossal magma-veined celestial sphere looms within a vortex of swirling clouds. She inserts the key into a moss-covered stone altar, triggering a massive circular runic array that launches vertical high-pressure water geysers into the sky. A giant, majestic white serpentine dragon with fiery orange eyes emerges from the mist. The warrior extends her hand as her eyes glow bright golden, establishing a powerful magical bond. The dragon turns upwards, soaring into the sky and unleashing a beam of pure radiant white energy directly into the celestial orb, causing it to shatter into shockwaves of blinding light. Epic cinematic scale, volumetric fog, photorealistic visual effects, Unreal Engine 5 render style, dark gray and golden color grading, hyper-detailed.
```

<a id="animation-19"></a>
### 95. Claymation Odysseus meets the Cyclops

by [@miilesus](https://x.com/miilesus) · 15s · 16:9 · **[▶ Run on APIKO](https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=animation-19#animation-19)** · [Original post](https://x.com/miilesus/status/2080744222571848176)

https://github.com/user-attachments/assets/1b395962-dc6f-45db-a475-1c178df27617

**Prompt:**

```text
Create a 3D claymation style animation of a cute caricature of Odysseus, wearing weathered bronze armor, a deep red cape, leather sandals, and windswept hair, sailing alone across a miniature stormy sea in a tiny wooden ship. A gigantic Cyclops suddenly rises from the water and reaches toward him. Odysseus calmly pulls out an enormous olive, launches it into the Cyclops’s mouth with a tiny catapult, and watches as the confused giant begins chewing happily. The storm instantly clears, the Cyclops gives him a thumbs up, and Odysseus takes a triumphant selfie with the giant in the background. Smooth expressive clay animation, epic orchestral music mixed with playful sound effects, handcrafted textures, cinematic lighting, mythological scale, absurd humor, viral energy.
```

<a id="craft-timelapse-11"></a>
### 173. An old tire becomes an infinity-mirror table

by [@Ruslanchain](https://x.com/Ruslanchain) · 24s · 9:16 · **[▶ Run on APIKO](https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=craft-timelapse-11#craft-timelapse-11)** · [Original post](https://x.com/Ruslanchain/status/2118023608815571361)

https://github.com/user-attachments/assets/a2352d5b-f26d-4725-962e-97309a2d59db

**Prompt:**

```text
Vertical DIY video, photorealistic style. A man in a black baseball cap, gray t-shirt and black cargo pants kneels on a concrete patio beside a red brick wall with potted plants. He sprays foaming cleaner onto a filthy mud-caked car tire, scrubs it with a brush until white foam drips down, then wipes the tire spotless black with a cloth. He fits a round plywood disc inside the tire, drives screws with a yellow cordless drill, attaches three angled wooden legs, flips the tire upright into a sturdy table base and sets a round glass top on it. He coils a warm white LED strip around the inner rim, places the glass back on top, and plugs in a power cord from the side of the tire so the LEDs glow through the glass. The scene transitions to a cozy living room at night with a beige sectional sofa, a floor lamp and a round jute rug, where the glowing tire coffee table now sits as the centerpiece. The camera slowly pushes in on the tabletop, revealing a hypnotic infinite mirror tunnel of repeating golden LED rings receding into darkness. Warm ambient lighting, smooth camera movements, satisfying transformation montage, high detail, realistic textures and reflections.
```

<a id="action-02"></a>
### 22. A martial arts fight inside a jewelry boutique

by [@mimu_ai1](https://x.com/mimu_ai1) · 10s · 16:9 · **[▶ Run on APIKO](https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=action-02#action-02)** · [Original post](https://x.com/mimu_ai1/status/2091215411341930633)

https://github.com/user-attachments/assets/42027033-7a36-4323-8ee4-32092c469add

**Prompt:**

```text
A dynamic, cinematic action sequence inside a luxury jewelry boutique at night. A confident young woman with long dark hair, olive skin, and sharp green eyes is the hero. She wears an elegant emerald silk evening gown and gold earrings. Three masked thieves in black tactical gear attempt a robbery, and she single-handedly defeats them with fast, precise martial arts choreography. She vaults over glass display cases, shattering them in dramatic slow motion as diamonds, pearls, and glass shards scatter and sparkle through the air like rain, catching warm spotlight beams. She slides across a marble counter, throws one attacker into a shelf of watches, and disarms the last with a spinning kick. At the end, she stands calm amid the glittering wreckage, picks up a single diamond ring, examines it in the light, and looks directly into the camera with a faint smile. Dynamic handheld camera, whip pans, slow-motion inserts, moody warm lighting with deep shadows, realistic physics, high production value, cinematic style, 4K.
```

<a id="cinematic-15"></a>
### 15. A rope bridge dissolves over a bottomless canyon

by [@zyvaoz](https://x.com/zyvaoz) · 15s · 16:9 · **[▶ Run on APIKO](https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-15#cinematic-15)** · [Original post](https://x.com/zyvaoz/status/2081398750996746385)

https://github.com/user-attachments/assets/f87e11b6-1311-4689-a53f-ce51683d2b29

**Prompt:**

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

- **[🎬 All 20 Cinematic cases](prompts/cinematic.md)**
- **[🥊 All 25 Action cases](prompts/action.md)**
- **[• All 7 Drama and romance cases](prompts/drama.md)**
- **[🐉 All 24 Fantasy and sci-fi cases](prompts/fantasy-scifi.md)**
- **[🧸 All 34 Animation cases](prompts/animation.md)**
- **[• All 31 Vlogs and lifestyle cases](prompts/vlog-lifestyle.md)**
- **[👟 All 21 Products, beauty and fashion cases](prompts/product.md)**
- **[• All 13 DIY and time-lapse cases](prompts/craft-timelapse.md)**

<a id="faq"></a>
## ❓ FAQ

<details>
<summary><b>Are these Seedance 2.0 prompts free to use?</b></summary>

Copy, edit and run any of them. The prompts and videos belong to the creators credited on each card, so check the original post before reusing a clip commercially.

</details>

<details>
<summary><b>How long can a Seedance 2.0 video be?</b></summary>

4 to 15 seconds per request, at 480p, 720p or 1080p. Longer cards on this page were made from several clips.

</details>

<details>
<summary><b>Which aspect ratios are supported?</b></summary>

16:9, 9:16, 1:1, 4:3, 3:4 and 21:9.

</details>

<details>
<summary><b>Can I use reference images, videos and audio?</b></summary>

Yes: up to 9 reference images, 3 reference videos (15 seconds in total) and 3 reference audio clips, called @Image1, @Video1 and @Audio1 in list order. A first frame, optionally with a last frame, cannot be combined with reference media.

</details>

<details>
<summary><b>How long can a prompt be?</b></summary>

Up to 20,000 characters. Dialogue, sound and camera directions all go in the prompt.

</details>

<details>
<summary><b>Seedance 2.0 or Seedance 2.5?</b></summary>

Seedance 2.5 makes clips up to 30 seconds and takes more references (30 images, 10 videos, 10 audio clips); Seedance 2.0 covers most ideas that fit in 15 seconds. The model pages list the price per second of each.

</details>

<details>
<summary><b>Why does my clip differ from the example?</b></summary>

Each run gives a different result, and authors may have used references, another resolution or Seedance 2.0 Fast. Change one detail at a time to compare.

</details>

<details>
<summary><b>How do I run a prompt through the API?</b></summary>

POST it as prompt to /v1/videos with model seedance-2.0, poll the task, then download the video. The API docs list every field.

</details>


<a id="related"></a>
## 🔗 Related

- [Seedance 2.0 Prompts · apiko.app](https://apiko.app/seedance-2-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Run Seedance 2.0](https://apiko.app/models/seedance-2.0?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Seedance 2.0 API docs](https://apiko.app/docs/api-manual/video-series/seedance/seedance-2.0?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Seedance 2.5 prompts](https://apiko.app/seedance-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Kling 4.0 prompts](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [All prompt libraries](https://apiko.app/prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Code examples for the APIKO API](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**More prompt collections**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts)
- [Awesome Claude Fable 5.2 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-fable-5.2-video-prompts)
- [Awesome Seedream 5.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedream-5.5-prompts)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts)

<a id="license"></a>
## 📄 License and credits

Prompts and result videos belong to the creators credited on each card, which links to the original post on X. Titles, descriptions, translations and the build scripts are released under [CC BY 4.0](LICENSE).

If this list saves you time, a ⭐ helps others find it.
