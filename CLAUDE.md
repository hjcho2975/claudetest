# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 목적

Android 앱 **톨리스트** (`com.tallest.app`, Google Play) 를 홍보하는 1페이지 랜딩 사이트. 결과물은 브라우저에서 바로 여는 `index.html` 하나 — 빌드 도구, 번들러, 서버 프레임워크 없음.

톨리스트는 **어린이 키 성장 예측 및 관리 앱** 입니다 (투두리스트 앱이 아닙니다 — 이름 때문에 헷갈리기 쉬움). 질병관리청 공식 성장 데이터와 한국 어린이 230만 명의 데이터를 기반으로 최종 키 예측, 사춘기 시기 분석, 성장 급증/정체 알림, 또래 비교, 맞춤 영양·운동·수면 가이드를 제공합니다.

## 카피라이팅 톤

부모의 심리 자극이 핵심 — 아래 훅을 일관되게 사용:

- **골든타임의 일회성**: "성장기는 단 한 번", "키는 자라는 시기에만 자랍니다"
- **놓치면 후회**: "10년 뒤 '그때 알았더라면'이라는 말을 하지 않으려면"
- **데이터 기반 안심**: "230만 명", "질병관리청", "전문의 검증" 같은 신뢰 시그널을 반복
- **무료**: 진입 장벽 제거 강조

문구 변경 시 위 톤을 유지할 것.

## 현재 상태

`index.html`은 HTML/CSS/JS가 모두 인라인된 자체 완결 파일. 섹션 순서:

1. **Nav** (sticky, blur backdrop) — 브랜드 + 다운로드 CTA
2. **Hero** — eyebrow / 거대 헤드라인(브레이크 분리, accent 그라디언트) / sub / CTA 2개 / 폰 mockup
3. **Hook (#why)** — 2열 그리드, "성장기는 단 한 번" 메시지
4. **Features** — 3×2 그리드, SVG 아이콘 + 제목 + 설명
5. **Stats** — 230만 / KDCA / 100% (count-up 애니메이션)
6. **How it works** — 3단계, `counter-increment`로 번호 자동 매김
7. **Final CTA** — 후회 방지 카피 + Play Store 버튼
8. **Footer** — 저작권 + 링크

모든 외부 링크는 `https://play.google.com/store/apps/details?id=com.tallest.app` 로 통일 (Play Store 페이지 하나만 존재).

`mycareer.md`, `test.text`는 이전 작업 잔여물로 현재 프로젝트와 무관.

## 편집 시 보존해야 할 기능

- **`.reveal` 스크롤 인 애니메이션**: `IntersectionObserver`가 `.reveal` 요소에 `.visible` 클래스 부여. 새 섹션은 `class="reveal"` 만 추가하면 자동 적용. 단계적 등장은 `.reveal-delay-1/2/3` 으로 조절.
- **`.stat-num[data-target]` 카운트업**: 화면 진입 시 0→target까지 ease-out 큐빅. 새 통계 카드 추가 시 `data-target="N"` `data-suffix="%"` 패턴 유지.
- **앵커 부드러운 스크롤**: `a[href^="#"]` 클릭 시 `scrollIntoView({behavior:'smooth'})`.
- **고정 nav blur**: `backdrop-filter: saturate(180%) blur(20px)` — Apple 무드의 핵심.

## 디자인 컨벤션 (Apple 스타일)

- **컬러**: 검은 배경(`#000`) + 보조 다크 그레이(`#0a0a0a`/`#111113`), 주 텍스트 `#f5f5f7`, 보조 `#a1a1a6`, 액센트 `#0a84ff` / `#5ac8fa`. CSS 변수로 `:root` 에 정의되어 있으니 커스텀 헥스 코드를 직접 박지 말 것.
- **타이포그래피**: SF Pro Display → Pretendard → Noto Sans KR 폴백. 헤드라인은 `clamp()` + 음수 `letter-spacing` (-0.03~-0.04em) + `line-height: 1.05~1.15` — Apple Dribbble 무드.
- **그라디언트 액센트**: 주요 단어/숫자에만 `linear-gradient(135deg, var(--accent-soft), #fff)` + `background-clip: text` 적용. 남발하지 말 것.
- **카드**: 둥근 모서리 `24px`, 1px 보더, hover 시 `translateY(-4px)` + 보더 강조.
- **버튼**: pill (`border-radius: 999px`), primary는 흰 배경 + 검정 글씨, ghost는 보더만.
- **모션**: cubic-bezier(0.16, 1, 0.3, 1) — 길고 부드러운 ease-out.

새 UI 요소는 위 톤을 유지하고 컬러풀한 그라디언트 / 둥글둥글한 material 스타일은 피할 것.

## 기타

- 사이트 자체가 결과물. 미리보기는 브라우저에서 `index.html` 직접 열기 (Windows에서 `start index.html`).
- UI 텍스트 언어: 한국어.
- WebFetch가 Play Store URL에서 404를 자주 반환함 — 앱 정보 추가 조사 필요 시 WebSearch로 우회.
