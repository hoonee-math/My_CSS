# Tailwind Grid 시스템 완벽 가이드

## 🎯 핵심 개념

### 1. 모바일 우선 (Mobile First)

Tailwind은 **모바일 우선** 방식을 사용합니다.

```html
<!-- ❌ 잘못된 이해 -->
md:grid-cols-3  ← 모바일용? NO!

<!-- ✅ 올바른 이해 -->
grid-cols-1     ← 모바일용 (기본값, 0px~)
md:grid-cols-3  ← 데스크톱용 (768px 이상)
```

#### 반응형 Breakpoint

| Prefix | 화면 크기 | 적용 시점 |
|--------|----------|----------|
| (없음) | 모든 화면 | 항상 (기본값) |
| `sm:` | 640px 이상 | 큰 모바일, 태블릿 |
| `md:` | 768px 이상 | 태블릿, 작은 노트북 |
| `lg:` | 1024px 이상 | 노트북 |
| `xl:` | 1280px 이상 | 데스크톱 |
| `2xl:` | 1536px 이상 | 큰 데스크톱 |

```html
<!-- 모바일: 1칸, 태블릿: 2칸, 데스크톱: 3칸 -->
<div class="grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
```

---

## 📐 Grid 기본 속성

### Grid Container (부모)

#### 1. `grid` - Grid 컨테이너 생성

```html
<div class="grid">
  <!-- Grid 아이템들 -->
</div>
```

**CSS 변환:**
```css
display: grid;
```

---

#### 2. `grid-cols-{n}` - 컬럼(세로 분할)

```html
<div class="grid grid-cols-3">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

**CSS 변환:**
```css
grid-template-columns: repeat(3, 1fr);
```

**시각화:**
```
┌────────┬────────┬────────┐
│   1    │   2    │   3    │
└────────┴────────┴────────┘
   1fr      1fr      1fr
```

**사용 가능한 값:**
- `grid-cols-1` ~ `grid-cols-12`
- `grid-cols-none`

---

#### 3. `grid-rows-{n}` - 로우(가로 분할)

```html
<div class="grid grid-rows-3">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

**CSS 변환:**
```css
grid-template-rows: repeat(3, 1fr);
```

**시각화:**
```
┌──────────┐
│    1     │  1fr
├──────────┤
│    2     │  1fr
├──────────┤
│    3     │  1fr
└──────────┘
```

**사용 가능한 값:**
- `grid-rows-1` ~ `grid-rows-6`
- `grid-rows-none`

---

#### 4. `gap-{size}` - 간격

```html
<div class="grid grid-cols-3 gap-4">
```

**CSS 변환:**
```css
gap: 1rem; /* 16px */
```

**종류:**
- `gap-0` ~ `gap-96`
- `gap-px` (1px)
- `gap-[10px]` (커스텀)

**세부 제어:**
```html
<!-- 가로/세로 간격 따로 -->
<div class="gap-x-4 gap-y-2">
```

---

### 커스텀 Grid Template

#### `grid-cols-[값]` - 커스텀 컬럼

```html
<div class="grid grid-cols-[200px_1fr_2fr]">
```

**CSS 변환:**
```css
grid-template-columns: 200px 1fr 2fr;
```

**시각화:**
```
┌────┬─────────┬──────────────────┐
│200px│   1fr   │       2fr        │
└────┴─────────┴──────────────────┘
```

**사용 예시:**
```html
<!-- 고정폭 + 유동폭 조합 -->
<div class="grid-cols-[250px_1fr]">  <!-- 사이드바 + 메인 -->

<!-- 비율 설정 -->
<div class="grid-cols-[1fr_2fr_1fr]">  <!-- 1:2:1 비율 -->

<!-- auto: 내용물 크기 -->
<div class="grid-cols-[auto_1fr_auto]">  <!-- 양쪽 auto, 가운데 채움 -->
```

---

#### `grid-rows-[값]` - 커스텀 로우

```html
<div class="grid grid-rows-[1fr_2fr_2fr_1fr]">
```

**CSS 변환:**
```css
grid-template-rows: 1fr 2fr 2fr 1fr;
```

**시각화:**
```
┌─────────────┐
│    1fr      │  ← 작음
├─────────────┤
│             │
│    2fr      │  ← 2배
│             │
├─────────────┤
│             │
│    2fr      │  ← 2배
│             │
├─────────────┤
│    1fr      │  ← 작음
└─────────────┘
```

**fr (fraction) 이해:**
```
1fr + 2fr + 2fr + 1fr = 총 6fr

1fr = 전체 높이의 1/6
2fr = 전체 높이의 2/6 (= 1/3)
```

---

#### `auto` vs `fr` vs `px`

```html
<div class="grid-rows-[auto_1fr_auto]">
```

| 값 | 의미 | 사용 예 |
|----|------|---------|
| `auto` | 내용물 크기에 맞춤 | 헤더, 푸터 |
| `1fr` | 남은 공간을 비율로 분배 | 메인 콘텐츠 |
| `100px` | 고정 크기 | 고정 높이 영역 |

**예시:**
```
┌─────────────┐
│   Header    │  auto (내용만큼)
├─────────────┤
│             │
│    Main     │  1fr (남은 공간 전부)
│             │
├─────────────┤
│   Footer    │  auto (내용만큼)
└─────────────┘
```

---

## 🎨 Grid Item (자식) 속성

### 1. `col-span-{n}` - 컬럼 차지

```html
<div class="grid grid-cols-4">
  <div class="col-span-2">2칸 차지</div>
  <div>1칸</div>
  <div>1칸</div>
</div>
```

**CSS 변환:**
```css
grid-column: span 2 / span 2;
```

**시각화:**
```
┌──────────────────┬────────┬────────┐
│    col-span-2    │   1    │   2    │
└──────────────────┴────────┴────────┘
```

**값:**
- `col-span-1` ~ `col-span-12`
- `col-span-full` (모든 칸 차지)

---

### 2. `col-start-{n}` / `col-end-{n}` - 컬럼 시작/종료 위치

```html
<div class="grid grid-cols-4">
  <div class="col-start-2 col-end-4">2번 칸부터 4번 칸 전까지</div>
</div>
```

**CSS 변환:**
```css
grid-column-start: 2;
grid-column-end: 4;
```

**시각화:**
```
칸 번호:  1      2      3      4
       ┌──────┬──────┬──────┬──────┐
       │      │  시작 │      │ 끝   │
       └──────┴──────┴──────┴──────┘
                └──────────┘
              col-start-2 col-end-4
```

**값:**
- `col-start-1` ~ `col-start-13`
- `col-end-1` ~ `col-end-13`
- `col-start-auto` / `col-end-auto`

---

### 3. `row-span-{n}` - 로우 차지

```html
<div class="grid grid-rows-3">
  <div class="row-span-2">2줄 차지</div>
  <div>1줄</div>
</div>
```

**CSS 변환:**
```css
grid-row: span 2 / span 2;
```

**시각화:**
```
┌──────────────┐
│              │
│  row-span-2  │
│              │
├──────────────┤
│      1       │
└──────────────┘
```

**값:**
- `row-span-1` ~ `row-span-6`
- `row-span-full`

---

### 4. `row-start-{n}` / `row-end-{n}` - 로우 시작/종료 위치

```html
<div class="row-start-2 row-end-4">
```

**CSS 변환:**
```css
grid-row-start: 2;
grid-row-end: 4;
```

**값:**
- `row-start-1` ~ `row-start-7`
- `row-end-1` ~ `row-end-7`
- `row-start-auto` / `row-end-auto`

---

## 💡 실전 예제

### 예제 1: 기본 3칼럼 레이아웃

```html
<div class="grid grid-cols-3 gap-4">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>
```

**결과:**
```
┌────┬────┬────┐
│ 1  │ 2  │ 3  │
├────┼────┼────┤
│ 4  │ 5  │ 6  │
└────┴────┴────┘
```

---

### 예제 2: 반응형 그리드

```html
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
</div>
```

**모바일 (0~767px):**
```
┌────┐
│ 1  │
├────┤
│ 2  │
├────┤
│ 3  │
├────┤
│ 4  │
└────┘
```

**태블릿 (768px~1023px):**
```
┌────┬────┐
│ 1  │ 2  │
├────┼────┤
│ 3  │ 4  │
└────┴────┘
```

**데스크톱 (1024px~):**
```
┌────┬────┬────┬────┐
│ 1  │ 2  │ 3  │ 4  │
└────┴────┴────┴────┘
```

---

### 예제 3: 헤더-사이드바-메인-푸터

```html
<div class="grid grid-cols-3 grid-rows-[auto_1fr_auto] gap-4 h-screen">
  <!-- Header: 3칸 전체 -->
  <header class="col-span-3 bg-blue-500">Header</header>

  <!-- Sidebar: 1칸 -->
  <aside class="bg-gray-200">Sidebar</aside>

  <!-- Main: 2칸 -->
  <main class="col-span-2 bg-white">Main Content</main>

  <!-- Footer: 3칸 전체 -->
  <footer class="col-span-3 bg-gray-800">Footer</footer>
</div>
```

**결과:**
```
┌───────────────────────────────┐
│          Header (3칸)          │  auto
├─────────┬─────────────────────┤
│         │                     │
│ Sidebar │   Main Content (2칸) │  1fr
│  (1칸)   │                     │
├─────────┴─────────────────────┤
│          Footer (3칸)          │  auto
└───────────────────────────────┘
```

---

### 예제 4: 복잡한 레이아웃 (grid-responsive-tailwind.html)

```html
<div class="grid gap-4
            grid-cols-1
            md:grid-cols-3 md:grid-rows-[1fr_2fr_2fr_1fr]">

  <!-- Header: 모바일 1칸, 데스크톱 3칸 -->
  <div class="col-span-1 md:col-span-3">Header</div>

  <!-- Sidebar: 데스크톱에서 2줄 차지 -->
  <div class="md:row-start-2 md:row-span-2">Sidebar</div>

  <!-- Main: 데스크톱에서 2칸 차지 -->
  <div class="md:col-start-2 md:col-span-2">Main</div>

  <!-- Section & Content -->
  <div class="md:col-start-2">Section</div>
  <div class="md:col-start-3">Content</div>

  <!-- Footer: 3칸 전체 -->
  <div class="col-span-1 md:col-span-3">Footer</div>
</div>
```

**모바일:**
```
┌──────────┐
│  Header  │
├──────────┤
│ Sidebar  │
├──────────┤
│   Main   │
├──────────┤
│ Section  │
├──────────┤
│ Content  │
├──────────┤
│  Footer  │
└──────────┘
```

**데스크톱:**
```
┌─────────────────────────────┐  1fr
│          Header             │
├─────────┬──────────┬────────┤
│         │          │        │
│ Sidebar │   Main   │        │  2fr
│         │          │        │
├─────────┼──────────┼────────┤
│         │          │        │
│         │ Section  │Content │  2fr
│         │          │        │
├─────────┴──────────┴────────┤
│          Footer             │  1fr
└─────────────────────────────┘
```

---

## 🔧 자주 쓰는 패턴

### 1. 카드 그리드 (반응형)

```html
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
  <div class="card">Card 1</div>
  <div class="card">Card 2</div>
  <div class="card">Card 3</div>
  <div class="card">Card 4</div>
</div>
```

---

### 2. 사이드바 레이아웃

```html
<div class="grid grid-cols-1 lg:grid-cols-[250px_1fr] gap-4">
  <aside>고정 폭 사이드바 (250px)</aside>
  <main>남은 공간 채우기</main>
</div>
```

---

### 3. 대시보드 레이아웃

```html
<div class="grid grid-cols-12 gap-4">
  <div class="col-span-12 lg:col-span-8">메인 차트</div>
  <div class="col-span-12 lg:col-span-4">사이드 위젯</div>
  <div class="col-span-12 md:col-span-6 lg:col-span-3">위젯 1</div>
  <div class="col-span-12 md:col-span-6 lg:col-span-3">위젯 2</div>
  <div class="col-span-12 md:col-span-6 lg:col-span-3">위젯 3</div>
  <div class="col-span-12 md:col-span-6 lg:col-span-3">위젯 4</div>
</div>
```

---

## 📋 치트시트

### Grid Container

| 클래스 | CSS |
|--------|-----|
| `grid` | `display: grid;` |
| `grid-cols-3` | `grid-template-columns: repeat(3, 1fr);` |
| `grid-rows-4` | `grid-template-rows: repeat(4, 1fr);` |
| `grid-cols-[200px_1fr]` | `grid-template-columns: 200px 1fr;` |
| `gap-4` | `gap: 1rem;` (16px) |
| `gap-x-4` | `column-gap: 1rem;` |
| `gap-y-2` | `row-gap: 0.5rem;` |

### Grid Item

| 클래스 | CSS |
|--------|-----|
| `col-span-2` | `grid-column: span 2 / span 2;` |
| `col-start-2` | `grid-column-start: 2;` |
| `col-end-4` | `grid-column-end: 4;` |
| `row-span-3` | `grid-row: span 3 / span 3;` |
| `row-start-1` | `grid-row-start: 1;` |
| `row-end-3` | `grid-row-end: 3;` |

### 반응형 Prefix

| Prefix | 화면 크기 |
|--------|----------|
| (없음) | 0px ~ (모바일) |
| `sm:` | 640px ~ |
| `md:` | 768px ~ |
| `lg:` | 1024px ~ |
| `xl:` | 1280px ~ |
| `2xl:` | 1536px ~ |

---

## ❓ FAQ

### Q1: `grid-cols-3`와 `grid-template-columns: repeat(3, 1fr)` 차이는?

**같습니다!** Tailwind의 `grid-cols-3`는 CSS의 `repeat(3, 1fr)`로 변환됩니다.

---

### Q2: `grid-rows-[1fr_2fr_2fr_1fr]`에서 `[]`는 왜 쓰나요?

Tailwind에 **미리 정의되지 않은 커스텀 값**을 사용할 때 `[]`를 씁니다.

```html
<!-- 미리 정의됨 -->
<div class="grid-cols-3">  ← OK

<!-- 커스텀 값 -->
<div class="grid-cols-[200px_1fr_300px]">  ← [] 필요
```

---

### Q3: `auto` vs `fr`의 차이는?

- **`auto`**: 내용물 크기에 맞춤 (최소한의 공간)
- **`fr`**: 남은 공간을 비율로 분배 (확장됨)

```html
<!-- auto: 내용만큼 -->
<div class="grid-rows-[auto_1fr_auto]">
  <header>텍스트 한 줄 (auto)</header>
  <main>남은 공간 전부 차지 (1fr)</main>
  <footer>텍스트 한 줄 (auto)</footer>
</div>
```

---

### Q4: 모바일에서는 `md:` 클래스가 적용 안 되나요?

**네, 안 됩니다!**

`md:` prefix는 **768px 이상**에서만 적용됩니다.

```html
<div class="grid-cols-1 md:grid-cols-3">
  <!-- 모바일(~767px): grid-cols-1 -->
  <!-- 데스크톱(768px~): grid-cols-3 -->
</div>
```

---

### Q5: `col-span-full`은 뭔가요?

모든 컬럼을 차지합니다 (= `col-span-전체칸수`)

```html
<div class="grid grid-cols-4">
  <div class="col-span-full">4칸 전부 차지</div>
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
</div>
```

---

## 🎓 학습 순서 추천

1. ✅ 기본 `grid`, `grid-cols`, `gap` 이해
2. ✅ `col-span`, `row-span`으로 영역 차지하기
3. ✅ 반응형 (`md:`, `lg:`) 적용해보기
4. ✅ 커스텀 값 `[]` 사용해보기
5. ✅ `col-start`, `row-start`로 정밀 배치

---

## 🔗 참고

- [Tailwind CSS Grid 공식 문서](https://tailwindcss.com/docs/grid-template-columns)
- 실습 파일: `layouts/grid-responsive-tailwind.html`
