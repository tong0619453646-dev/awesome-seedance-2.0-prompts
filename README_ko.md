<div align="center">

<a href="https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-seedance-2.0-prompts"><img src="assets/banner.jpg" alt="Awesome Seedance 2.0 프롬프트" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-175_cases-111111)](README_ko.md#menu)
[![Try Seedance 2.0 on APIKO](https://img.shields.io/badge/Try_Seedance_2.0-on_APIKO-4F46E5)](https://apiko.app/ko/models/seedance-2.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seedance-2.0-prompts&utm_content=model_try)
[![Seedance 2.0 API docs](https://img.shields.io/badge/Seedance_2.0-API_docs-111111)](https://apiko.app/docs/api-manual/video-series/seedance/seedance-2.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-seedance-2.0-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-Current-111111)](README_ko.md)

</div>

# Awesome Seedance 2.0 프롬프트

<a id="introduction"></a>
## 🌟 소개

**Seedance 2.0 프롬프트: 결과 클립이 붙은 복사 가능한 영상 프롬프트 175개. 애니메이션과 클레이부터 액션, 뷰티 광고, 브이로그, DIY 타임랩스까지.**

프롬프트마다 그 프롬프트로 만든 클립이 붙어 있습니다. 복사하거나, 길이와 화면 비율이 맞춰진 채로 모델 페이지에서 여세요. 결과 영상은 모두 GitHub에서 바로 재생됩니다.

검색과 필터는 [apiko.app/seedance-2-0-prompts](https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-seedance-2.0-prompts&utm_content=intro).

> [!NOTE]
> 프롬프트는 작성자가 올린 원문 그대로라 대부분 영어입니다. 제목과 설명은 저희가 썼습니다. 모든 예시에 작성자와 원본 게시물 링크를 달았습니다.

<a id="quick-start"></a>
## 🚀 빠른 시작

**브라우저에서:** 모든 예시에 **APIKO에서 실행** 링크가 있습니다. [apiko.app](https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seedance-2.0-prompts&utm_content=browser)에서 해당 예시가 열리며, **사용**을 누르면 프롬프트가 Seedance 2.0 플레이그라운드에 채워집니다.

**API로:** [APIKO API 키](https://apiko.app/ko/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seedance-2.0-prompts&utm_content=api_key)를 만든 뒤 작업을 생성하고, 영상이 완성될 때까지 상태를 조회합니다.

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

엔드포인트: `POST https://api.apiko.app/v1/videos` (작업 생성) · `GET https://api.apiko.app/v1/videos/{id}` (상태와 결과 조회)

<a id="how-to-write"></a>
## ✍️ Seedance 2.0 프롬프트 작성법

이 페이지의 프롬프트에 반복해서 나오는 네 가지 구조.

- **초 단위 구간** · `0–3초: … 3–7초: … 7–15초: …` — 많은 프롬프트가 클립을 초 단위로 나누고 구간마다 동작 하나만 적어 15초 안의 순서를 지킵니다.
- **무엇으로 찍는지 쓰기** · `카메라 기종이나 포맷 + 움직임 + 누가 들고 있는지` — DV, 16mm, 팔을 뻗어 든 휴대폰, 고정 삼각대: 무엇으로 찍는지 쓰면 질감과 흔들림이 함께 정해집니다.
- **참고 자료에 번호 붙이기** · `@Image1 = 캐릭터. @Image2 = 제품. 유지: … 변경: …` — 참고 프롬프트는 업로드 순서로 파일을 부르고 각 파일에서 무엇을 바꿔도 되는지 적어 얼굴과 제품을 유지합니다.
- **변화 과정을 쓰기** · `시작 상태 → 계기 → 결과` — DIY, 메이크오버, 괴물 프롬프트는 변화 전, 변하는 순간, 결과를 적고 Seedance 2.0은 그대로 따라갑니다.

**예시에서 보이는 것**

- **긴 대본은 여러 클립으로 나눕니다.** Seedance 2.0은 요청당 4~15초를 만듭니다. 그보다 긴 카드는 여러 번 생성해 편집한 것입니다.
- **애니메이션 스타일이 잘 유지됩니다.** 스타일을 맨 앞에 쓰면 클레이, 수묵화, 애니, 손그림 스톱모션이 클립 내내 유지됩니다.
- **소리도 적으세요.** 소리는 영상과 함께 생성됩니다. ASMR 질감, 음악, 대사를 적으면 들립니다.
- **사실감을 깨는 요소를 금지하세요.** 브이로그와 DIY 프롬프트는 CGI, 배경음악, 자막을 빼서 실제 영상처럼 보이게 합니다.
- **정확한 구도는 첫 프레임으로.** 제품과 평면도 카드는 업로드한 이미지에서 시작해 움직이기 전에 구도를 고정합니다.

<a id="menu"></a>
## 📑 목차

- [⭐ 추천](#featured) (6)
- [🎬 시네마틱](prompts/cinematic_ko.md) (20) — 카메라 아이디어 하나로 만든 장면: 사람처럼 구는 동물, 매크로, 초현실적인 순간.
- [🥊 액션](prompts/action_ko.md) (25) — 무협 결투부터 오토바이 탈출까지, 격투·추격·스턴트.
- [• 드라마와 로맨스](prompts/drama_ko.md) (7) — 사람 이야기: 이별, 첫눈에 반한 순간, 지친 하루.
- [🐉 판타지와 SF](prompts/fantasy-scifi_ko.md) (24) — 드래곤, 메카, 괴물, 마법이 등장하는 큰 장면.
- [🧸 애니메이션](prompts/animation_ko.md) (34) — 애니, 3D 카툰, 클레이, 수묵화, 손그림 스톱모션.
- [• 브이로그와 일상](prompts/vlog-lifestyle_ko.md) (31) — 휴대폰·DV 감성 영상, 여행 산책, 느린 일상.
- [👟 제품·뷰티·패션](prompts/product_ko.md) (21) — 스킨케어, 주얼리, 음식, 패션 광고. 상당수가 UGC 스타일입니다.
- [• DIY와 타임랩스](prompts/craft-timelapse_ko.md) (13) — 에폭시 바닥, 리모델링, 핸드메이드, 요리를 처음부터 끝까지.
- [❓ 자주 묻는 질문](#faq)
- [🔗 관련 링크](#related)

<a id="featured"></a>
## ⭐ 추천

<a id="cinematic-01"></a>
### 1. 차 안에서 찍은 빨간 스쿠터 탄 고양이 두 마리

작성자 [@Just_sharon7](https://x.com/Just_sharon7) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-01#cinematic-01)** · [원본 게시물](https://x.com/Just_sharon7/status/2084901309988425731)

https://github.com/user-attachments/assets/a73e7827-858a-4f85-862a-f39b6bd24fd8

**프롬프트:**

```text
A highly realistic cinematic shot filmed from inside a moving car looking out the side window, capturing two cats riding a small red mini motorcycle on a suburban road. An orange tabby cat is driving, gripping the handlebars with both front paws, mouth open in a surprised or determined expression, ears slightly back from the wind. Behind it, a fluffy pure white cat is perched as a passenger, holding up a shiny empty metal food bowl with one paw while the other rests for balance, mouth wide open as if meowing or yelling. The motorcycle is a compact red mini bike with a visible headlight, black tires, and a small license plate area. Background shows a typical American suburban street with houses, trees, power lines, a concrete barrier, other cars passing, and a partly cloudy sky. Dynamic motion blur on the background to convey speed, natural daylight, humorous and absurd vibe.
```

<a id="fantasy-scifi-04"></a>
### 56. 용암 구체를 부수는 전사와 백룡

작성자 [@Zyrellix](https://x.com/Zyrellix) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=fantasy-scifi-04#fantasy-scifi-04)** · [원본 게시물](https://x.com/Zyrellix/status/2092121112746287527)

https://github.com/user-attachments/assets/0b3b595f-e1d6-4881-bbbc-52cc4c1b6977

**프롬프트:**

```text
A cinematic dark fantasy epic video in 8K resolution. Extreme macro close-up of a female warrior's eye, iris reflecting a burning molten celestial orb swirling inside dark storm clouds. Low-angle tracking shot as an East Asian female warrior clad in sleek black leather-and-steel armor walks through shallow water carrying an ornate key. She steps onto a circular stone platform engraved with glowing golden runes, surrounded by mist, cascading waterfalls, and ancient temple ruins. Above, a colossal magma-veined celestial sphere looms within a vortex of swirling clouds. She inserts the key into a moss-covered stone altar, triggering a massive circular runic array that launches vertical high-pressure water geysers into the sky. A giant, majestic white serpentine dragon with fiery orange eyes emerges from the mist. The warrior extends her hand as her eyes glow bright golden, establishing a powerful magical bond. The dragon turns upwards, soaring into the sky and unleashing a beam of pure radiant white energy directly into the celestial orb, causing it to shatter into shockwaves of blinding light. Epic cinematic scale, volumetric fog, photorealistic visual effects, Unreal Engine 5 render style, dark gray and golden color grading, hyper-detailed.
```

<a id="animation-19"></a>
### 95. 클레이로 만든 오디세우스와 키클롭스

작성자 [@miilesus](https://x.com/miilesus) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=animation-19#animation-19)** · [원본 게시물](https://x.com/miilesus/status/2080744222571848176)

https://github.com/user-attachments/assets/1b395962-dc6f-45db-a475-1c178df27617

**프롬프트:**

```text
Create a 3D claymation style animation of a cute caricature of Odysseus, wearing weathered bronze armor, a deep red cape, leather sandals, and windswept hair, sailing alone across a miniature stormy sea in a tiny wooden ship. A gigantic Cyclops suddenly rises from the water and reaches toward him. Odysseus calmly pulls out an enormous olive, launches it into the Cyclops’s mouth with a tiny catapult, and watches as the confused giant begins chewing happily. The storm instantly clears, the Cyclops gives him a thumbs up, and Odysseus takes a triumphant selfie with the giant in the background. Smooth expressive clay animation, epic orchestral music mixed with playful sound effects, handcrafted textures, cinematic lighting, mythological scale, absurd humor, viral energy.
```

<a id="craft-timelapse-11"></a>
### 173. 폐타이어로 만든 인피니티 미러 테이블

작성자 [@Ruslanchain](https://x.com/Ruslanchain) · 24초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=craft-timelapse-11#craft-timelapse-11)** · [원본 게시물](https://x.com/Ruslanchain/status/2118023608815571361)

https://github.com/user-attachments/assets/a2352d5b-f26d-4725-962e-97309a2d59db

**프롬프트:**

```text
Vertical DIY video, photorealistic style. A man in a black baseball cap, gray t-shirt and black cargo pants kneels on a concrete patio beside a red brick wall with potted plants. He sprays foaming cleaner onto a filthy mud-caked car tire, scrubs it with a brush until white foam drips down, then wipes the tire spotless black with a cloth. He fits a round plywood disc inside the tire, drives screws with a yellow cordless drill, attaches three angled wooden legs, flips the tire upright into a sturdy table base and sets a round glass top on it. He coils a warm white LED strip around the inner rim, places the glass back on top, and plugs in a power cord from the side of the tire so the LEDs glow through the glass. The scene transitions to a cozy living room at night with a beige sectional sofa, a floor lamp and a round jute rug, where the glowing tire coffee table now sits as the centerpiece. The camera slowly pushes in on the tabletop, revealing a hypnotic infinite mirror tunnel of repeating golden LED rings receding into darkness. Warm ambient lighting, smooth camera movements, satisfying transformation montage, high detail, realistic textures and reflections.
```

<a id="action-02"></a>
### 22. 보석 매장 안의 무술 액션

작성자 [@mimu_ai1](https://x.com/mimu_ai1) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=action-02#action-02)** · [원본 게시물](https://x.com/mimu_ai1/status/2091215411341930633)

https://github.com/user-attachments/assets/42027033-7a36-4323-8ee4-32092c469add

**프롬프트:**

```text
A dynamic, cinematic action sequence inside a luxury jewelry boutique at night. A confident young woman with long dark hair, olive skin, and sharp green eyes is the hero. She wears an elegant emerald silk evening gown and gold earrings. Three masked thieves in black tactical gear attempt a robbery, and she single-handedly defeats them with fast, precise martial arts choreography. She vaults over glass display cases, shattering them in dramatic slow motion as diamonds, pearls, and glass shards scatter and sparkle through the air like rain, catching warm spotlight beams. She slides across a marble counter, throws one attacker into a shelf of watches, and disarms the last with a spinning kick. At the end, she stands calm amid the glittering wreckage, picks up a single diamond ring, examines it in the light, and looks directly into the camera with a faint smile. Dynamic handheld camera, whip pans, slow-motion inserts, moody warm lighting with deep shadows, realistic physics, high production value, cinematic style, 4K.
```

<a id="cinematic-15"></a>
### 15. 끝없는 협곡 위에서 사라지는 흔들다리

작성자 [@zyvaoz](https://x.com/zyvaoz) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-seedance-2.0-prompts&utm_content=cinematic-15#cinematic-15)** · [원본 게시물](https://x.com/zyvaoz/status/2081398750996746385)

https://github.com/user-attachments/assets/f87e11b6-1311-4689-a53f-ce51683d2b29

**프롬프트:**

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

- **[🎬 시네마틱 전체 20개 보기](prompts/cinematic_ko.md)**
- **[🥊 액션 전체 25개 보기](prompts/action_ko.md)**
- **[• 드라마와 로맨스 전체 7개 보기](prompts/drama_ko.md)**
- **[🐉 판타지와 SF 전체 24개 보기](prompts/fantasy-scifi_ko.md)**
- **[🧸 애니메이션 전체 34개 보기](prompts/animation_ko.md)**
- **[• 브이로그와 일상 전체 31개 보기](prompts/vlog-lifestyle_ko.md)**
- **[👟 제품·뷰티·패션 전체 21개 보기](prompts/product_ko.md)**
- **[• DIY와 타임랩스 전체 13개 보기](prompts/craft-timelapse_ko.md)**

<a id="faq"></a>
## ❓ 자주 묻는 질문

<details>
<summary><b>이 Seedance 2.0 프롬프트는 무료로 써도 되나요?</b></summary>

복사, 수정, 실행 모두 가능합니다. 프롬프트와 영상은 카드에 표시된 크리에이터의 것이니 클립을 상업적으로 쓰기 전에 원문을 확인하세요.

</details>

<details>
<summary><b>Seedance 2.0 영상은 얼마나 길게 만들 수 있나요?</b></summary>

요청당 4~15초, 480p·720p·1080p입니다. 이 페이지의 더 긴 카드는 여러 클립을 이은 것입니다.

</details>

<details>
<summary><b>어떤 화면 비율을 지원하나요?</b></summary>

16:9, 9:16, 1:1, 4:3, 3:4, 21:9입니다.

</details>

<details>
<summary><b>참고 이미지, 영상, 오디오를 쓸 수 있나요?</b></summary>

네. 참고 이미지 최대 9장, 참고 영상 3개(합계 15초), 참고 오디오 3개를 업로드 순서대로 @Image1, @Video1, @Audio1로 부릅니다. 첫 프레임(마지막 프레임 포함)은 참고 자료와 함께 쓸 수 없습니다.

</details>

<details>
<summary><b>프롬프트는 얼마나 길게 쓸 수 있나요?</b></summary>

최대 20,000자입니다. 대사, 소리, 카메라 지시는 모두 프롬프트에 씁니다.

</details>

<details>
<summary><b>Seedance 2.0과 2.5 중 무엇을 써야 하나요?</b></summary>

Seedance 2.5는 최대 30초에 참고 자료를 더 많이 받습니다(이미지 30장, 영상 10개, 오디오 10개). 15초 안에 들어가는 아이디어는 대부분 Seedance 2.0으로 충분합니다. 초당 가격은 각 모델 페이지에 있습니다.

</details>

<details>
<summary><b>결과가 예시와 다른 이유는?</b></summary>

실행할 때마다 결과가 다르고, 작성자가 참고 자료, 다른 해상도, Seedance 2.0 Fast를 썼을 수 있습니다. 한 번에 하나씩 바꿔 비교하세요.

</details>

<details>
<summary><b>API로는 어떻게 실행하나요?</b></summary>

model을 seedance-2.0으로, prompt에 프롬프트를 넣어 /v1/videos로 POST하고, 작업을 조회한 뒤 영상을 내려받습니다. 모든 필드는 API 문서에 있습니다.

</details>


<a id="related"></a>
## 🔗 관련 링크

- [Seedance 2.0 프롬프트 · apiko.app](https://apiko.app/ko/seedance-2-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Seedance 2.0 실행](https://apiko.app/ko/models/seedance-2.0?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Seedance 2.0 API 문서](https://apiko.app/docs/api-manual/video-series/seedance/seedance-2.0?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Seedance 2.5 프롬프트](https://apiko.app/ko/seedance-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [Kling 4.0 프롬프트](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [전체 프롬프트 라이브러리](https://apiko.app/ko/prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-seedance-2.0-prompts)
- [APIKO API 코드 예시](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**다른 프롬프트 모음**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_ko.md)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_ko.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_ko.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_ko.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_ko.md)

<a id="license"></a>
## 📄 라이선스와 출처

프롬프트와 결과 영상은 각 카드에 표시된 크리에이터의 것이며, 카드는 X 원문으로 연결됩니다. 제목, 설명, 번역, 빌드 스크립트는 [CC BY 4.0](LICENSE)으로 배포합니다.

이 목록이 도움이 됐다면 ⭐ 를 눌러 다른 사람도 찾을 수 있게 해 주세요.
