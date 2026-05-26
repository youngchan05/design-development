# GEARS Design System — Component Style Guide

> GHG Emission, Authentic Reporting System  
> UI Prototype 기반 React 이식용 디자인 스펙  
> 작성 기준: `docs/gears-components.html` + 실제 페이지(fleet-list, notice-list, mrv-detail 등)

---

## 1. Design Tokens

### Color

```ts
// theme.ts 교체 값
colors: {
  // Background
  bg:        '#f5f7f5',
  surface:   '#ffffff',
  surface2:  '#f0f4f0',

  // Border
  border:    'rgba(0, 0, 0, 0.08)',
  borderMd:  'rgba(0, 0, 0, 0.13)',

  // Brand — Teal
  teal:      '#3d8b6e',
  tealDim:   'rgba(61, 139, 110, 0.09)',
  tealMid:   'rgba(61, 139, 110, 0.22)',

  // Text
  text1:     '#1a2420',   // 주 텍스트
  text2:     '#5a6e68',   // 보조 텍스트
  text3:     '#9eb0aa',   // 힌트/라벨/비활성

  // Semantic
  danger:    '#e05252',
  warning:   '#c2a60e',
  success:   '#2e7d57',
  info:      '#5a7bcc',
}
```

### Dark Mode

`document.documentElement.dataset.theme = 'dark'` 방식으로 토글

```ts
darkColors: {
  bg:        '#111214',
  surface:   '#1c1d21',
  surface2:  '#25272c',
  border:    'rgba(255, 255, 255, 0.07)',
  borderMd:  'rgba(255, 255, 255, 0.13)',
  teal:      '#4fa882',
  tealDim:   'rgba(79, 168, 130, 0.12)',
  tealMid:   'rgba(79, 168, 130, 0.25)',
  text1:     '#e4e6ea',
  text2:     '#8a9299',
  text3:     '#464c52',
}
```

### Radius

```ts
radius: {
  sm: '6px',   // input, button, badge
  md: '10px',  // card, modal, dropdown
}
```

### Sizing

```ts
sizing: {
  navH:     '52px',   // top navigation height
  sidebarW: '200px',  // sidebar width (collapsed: 56px)
  ctrlH:    '38px',   // input/button default height
  ctrlFs:   '13.5px', // input/button font size
}
```

### Typography

- **Font**: `'Geist', system-ui, sans-serif`
- **Mono Font**: `'Geist Mono', monospace` (숫자, 코드, IMO 번호)

| 용도 | size | weight |
|------|------|--------|
| Page Title | 32px | 700, letter-spacing: -0.8px |
| Section Heading | 22px | 700, letter-spacing: -0.5px |
| Card Title | 16px | 600 |
| Body | 14px | 400 |
| UI Label / Table row | 13px | 500 |
| Form Label | 12px | 600 |
| Table Header | 11px | 600, uppercase, letter-spacing: 0.4px |
| Mono (IMO, number) | 12.5px | 400, Geist Mono |

---

## 2. Atoms

### Button

5가지 variant, 3가지 size.

```
base:    height 38px, padding 0 16px, radius 6px, font-size 13.5px, font-weight 500
sm:      height 30px, padding 0 12px, font-size 12px
lg:      height 44px, padding 0 22px, font-size 14px
```

| Variant | Background | Color | Border |
|---------|-----------|-------|--------|
| `default` | `surface` | `text2` | `borderMd` |
| `primary` | `teal` | `#fff` | `teal` |
| `outline` | transparent | `teal` | `tealMid` |
| `ghost` | transparent | `text2` | transparent |
| `danger` | `#e05252` | `#fff` | `#e05252` |
| `disabled` | — | — | opacity 0.45 |

**Hover:**
- default → bg: `tealDim`, color: `teal`, border: `tealMid`
- primary → bg: `#34775e`
- danger → bg: `#c94343`
- ghost → bg: `surface2`, border: `border`

---

### Input

```
height: 38px (--ctrl-h)
padding: 0 12px
border: 1px solid borderMd
border-radius: 6px
font-size: 13.5px
color: text1
background: surface
```

| State | 변화 |
|-------|------|
| focus | border: `tealMid`, box-shadow: `0 0 0 3px rgba(61,139,110,.07)` |
| disabled | bg: `surface2`, color: `text3`, cursor: not-allowed |
| error | border: `#e05252`, focus shadow: `rgba(224,82,82,.07)` |

**Select**: 동일 height/padding + 우측 chevron SVG 아이콘 (appearance: none)  
**Textarea**: 동일 border 스타일, min-height: 80px, resize: vertical

---

### Checkbox / Radio

```
width/height: 16px
accent-color: teal
```

`.check-item` wrapper: `display:flex, align-items:center, gap:8px, font-size:13.5px`

---

### Badge

#### Status Badge (dot 포함)

```
height: 22px, padding: 0 9px, border-radius: 11px
font-size: 11px, font-weight: 600
.badge__dot: width 6px, height 6px, border-radius 50%
```

| variant | background | color | border |
|---------|-----------|-------|--------|
| `submitted` | `tealDim` | `teal` | `1px solid tealMid` |
| `approved` | `rgba(61,139,110,.12)` | `#2d7355` | `rgba(61,139,110,.25)` |
| `draft` | `rgba(154,113,58,.1)` | `#9a713a` | — |
| `pending` | `rgba(99,130,220,.1)` | `#5a7bcc` | — |
| `rejected` | `rgba(224,82,82,.1)` | `#c94343` | — |

#### Label Badge

| variant | style |
|---------|-------|
| `new` | bg: `teal`, color: #fff, font-size: 10px, radius: 3px |
| `notice` | bg: `surface2`, color: `text3`, border: `borderMd`, radius: 3px |

#### CII Rating Badge

```
width/height: 24px, border-radius: 5px, font-size: 12px, font-weight: 700
```

| 등급 | background | color |
|------|-----------|-------|
| A | `rgba(61,139,110,.15)` | `#2d7355` |
| B | `rgba(86,160,100,.15)` | `#3a8044` |
| C | `rgba(204,166,54,.15)` | `#8a6e1a` |
| D | `rgba(220,130,60,.15)` | `#9a5010` |
| E | `rgba(224,82,82,.15)` | `#b83030` |

#### Reg Badge (Compliance status, fleet-list 전용)

```
padding: 2px 8px, border-radius: 20px, font-size: 10.5px, font-weight: 500
border: 1px solid transparent
```

| variant | background | color |
|---------|-----------|-------|
| `approved` | `rgba(61,139,110,.1)` | `teal` |
| `submitted` | `rgba(37,99,235,.1)` | `#2563eb` |
| `revision` | `rgba(245,158,11,.12)` | `#b45309` |
| `saved` | `surface2` | `text3`, border: `border` |

---

### Avatar

```
border-radius: 8px (sm), 10px (md), 12px (lg)
font-weight: 700
```

| size | width/height | font-size |
|------|-------------|-----------|
| sm (default) | 32px | 11px |
| md | 40px | 13px |
| lg | 52px | 16px |

| color | background | color |
|-------|-----------|-------|
| green | `rgba(61,139,110,.15)` | `teal` |
| blue | `rgba(99,130,220,.15)` | `#5a7bcc` |
| orange | `rgba(220,130,60,.15)` | `#9a5010` |

---

## 3. Molecules

### Form Field

```
label → font-size: 12px, font-weight: 600, color: text2
  .req (필수 *) → color: #e05252
hint → font-size: 11.5px, color: text3
error → font-size: 11.5px, color: #e05252, flex + gap 4px + icon
```

---

### Search Input

```
height: 38px, padding: 0 12px 0 34px (좌측 아이콘 공간)
search icon: position absolute, left: 10px, color: text3
```

Filter 버튼과 조합:
```
<SearchInput /> + <Button> Filter <CountBadge>{n}</CountBadge> </Button>
```

---

### Breadcrumb

```
font-size: 12px, color: text3
separator: › (chevron)
current page: color: text2, font-weight: 500
links: hover → color: teal
```

---

### Info Banner

3가지 semantic state. 아이콘 + 텍스트 구성.

```
padding: 12px 16px, border-radius: 6px, font-size: 12.5px, line-height: 1.55
```

| variant | background | border | icon color |
|---------|-----------|--------|------------|
| `info` (default) | `tealDim` | `tealMid` | `teal` |
| `warning` | `rgba(204,166,54,.08)` | `rgba(204,166,54,.25)` | `#8a6e1a` |
| `error` | `rgba(224,82,82,.07)` | `rgba(224,82,82,.2)` | `#c94343` |

---

### Alert

Info Banner보다 강조도 높음. 닫기(×) 버튼 포함. 4가지 semantic state.

```
padding: 12px 14px, border-radius: 6px, font-size: 12.5px
구조: icon + body(title + desc) + close button
title: font-size 13px, font-weight 600
```

| variant | background | border | color |
|---------|-----------|--------|-------|
| `info` | `tealDim` | `tealMid` | `#1e4a38` |
| `success` | `rgba(46,125,87,.08)` | `rgba(46,125,87,.25)` | `#1e4a2a` |
| `warning` | `rgba(194,124,14,.08)` | `rgba(194,124,14,.25)` | `#5a3a00` |
| `error` | `rgba(224,82,82,.08)` | `rgba(224,82,82,.22)` | `#7a1c1c` |

Dark mode: info→`#7dcfac`, success→`#6ec98a`, warning→`#e8c060`, error→`#e88080`

---

### Accordion

```
border: 1px solid border, border-radius: 6px, overflow: hidden
header: padding 12px 16px, font-size 13px, font-weight 500
  open state: color: teal, background: tealDim
  chevron: rotate 90deg when open (transition: 0.2s)
body: max-height 0 → open (transition: max-height 0.25s cubic-bezier(.4,0,.2,1))
body inner: padding 14px 16px, font-size 12.5px, border-top: 1px solid border
```

---

### Filter Popover

```
trigger: Button (Filter + count badge)
popover: position absolute, top: calc(100% + 8px), width: 260px
  background: surface, border: 1px solid border, border-radius: 10px
  box-shadow: 0 12px 32px rgba(0,0,0,.1)
head: padding 12px 14px, title + Reset button
body: padding 14px, flex-column, gap 12px (FormField들)
foot: padding 10px 14px, background: surface2, Cancel + Apply buttons
```

---

### Notification Button

```
width/height: 34px, border-radius: 6px, border: 1px solid border
hover: background tealDim, color teal, border tealMid
badge: position absolute, top -4px, right -4px
  background: #e05252, color #fff, font-size 9px, min-width 16px, height 16px, border-radius 8px
```

---

## 4. Organisms

### Top Navigation

```
position: fixed, top: 0, height: 52px (--nav-h)
background: surface, border-bottom: 1px solid border
z-index: 100
left: logo + subtitle
right: badge + theme toggle + notification + user avatar
```

Logo mark: 28px, border-radius 7px, bg: teal

---

### Sidebar

```
position: fixed, top: nav-h, width: 200px (--sidebar-w)
height: calc(100vh - nav-h)
background: surface, border-right: 1px solid border
transition: width 0.25s cubic-bezier(.4,0,.2,1)
collapsed width: 56px (아이콘만 표시)
```

**Section label**: font-size 9.5px, font-weight 700, uppercase, color: text3  
**Nav item**: padding 7px 10px, border-radius 6px, font-size 12.5px, font-weight 500  
- hover: color text1, bg tealDim  
- active: color teal, bg tealDim  

**Accordion sub-item**: indent 28px, font-size 12px, dot prefix  
**Collapse toggle button**: position absolute, right edge, width 18px, height 36px, border-radius 0 6px 6px 0

---

### Section Card

```
background: surface, border: 1px solid border, border-radius: 10px
header: padding 14px 20px, border-bottom: 1px solid border
  title: font-size 13px, font-weight 600
  title-dot: width 3px, height 14px, bg teal, border-radius 2px (좌측 accent)
body: padding 20px
```

---

### Tabs

```
tab-bar: display flex, border-bottom: 1px solid border
tab-item: padding 10px 16px 9px, font-size 13px, font-weight 500, color text3
  border-bottom: 2px solid transparent, margin-bottom: -1px
  active: color teal, border-bottom-color teal, font-weight 600
  hover: color text2
tab-pane: display none → active: display block, padding 20px
```

---

### Table

**공통 스타일:**

```
font-size: 12.5px
table-layout: fixed
border-collapse: collapse

th: padding 10px 12px, background surface2, font-size 11px, font-weight 600,
    color text3, uppercase, letter-spacing 0.3px, border-bottom 1px solid border

td: padding 11px 12px, border-bottom 1px solid border, color text2,
    overflow hidden, text-overflow ellipsis, white-space nowrap

tbody tr: cursor pointer
tbody tr:hover td: background tealDim
tbody tr:last-child td: border-bottom none
```

**Fleet style** (sticky thead + checkbox):
```
.tbl-wrap: overflow auto, max-height 280px
thead tr: position sticky, top 0, z-index 5
→ colgroup으로 각 컬럼 width 고정
```

**Notice style** (pinned row + row click):
```
tr.pinned td: background rgba(61,139,110,.04)
tr.pinned td:first-child: border-left 2px solid teal
```

**Selected row:**
```
tr.selected td: background rgba(61,139,110,.06)
```

**Mono number cells:**
```
.num: font-family Geist Mono, color text3
```

---

### Side Drawer

Fleet list 행 클릭 시 우측 슬라이드인 패널.  
`createPortal`로 `document.body`에 마운트 권장.

```
position: fixed, top 0, right 0, bottom 0
width: 440px, max-width: 96vw
background: surface, border-left: 1px solid border
transform: translateX(100%) → open: translateX(0)
transition: 0.25s cubic-bezier(.4,0,.2,1)
box-shadow: -8px 0 32px rgba(0,0,0,.1)
z-index: 401

overlay: position fixed, inset 0, background rgba(0,0,0,.3)
  z-index: 400, opacity 0 → open: opacity 1
```

**구조:**
```
DrawerHead
  vessel name: font-size 15px, font-weight 700, letter-spacing -0.3px
  IMO: font-size 11.5px, color text3, Geist Mono
  close button: 28px, border-radius 6px

DrawerBody (overflow-y auto, flex-column, gap 22px)
  DrawerSection (Vessel Info / MRV Company Setting / Compliance Status)
    section title: font-size 10.5px, font-weight 600, uppercase, color text3
                   padding-bottom 8px, border-bottom 1px solid border
    DrawerGrid: grid 2-col, gap 12px
      DrawerField:
        label: font-size 11px, color text3
        value: font-size 13px, font-weight 500, color text1
    DrawerComplianceRow:
      padding 10px 14px, border-radius 8px, background surface2
      name: font-size 12.5px, font-weight 500, color text2
      + RegBadge (status)

DrawerFoot (border-top 1px solid border, padding 14px 22px)
  Edit MRV Setting (btn--primary, flex:1) + Close (btn--default)
```

---

### Selection Bar

테이블 행 선택 시 하단 액션 바.

```
background: rgba(61,139,110,.1), border: 1px solid tealMid, border-radius: 6px
padding: 10px 16px, display flex, justify-content space-between

info text: font-size 12.5px, color teal, font-weight 500
action buttons: height 30px, padding 0 12px, border-radius 6px, font-size 12px
  default: border tealMid, color teal, bg surface
  filled: bg teal, color #fff
  danger: color #e05252, border rgba(224,82,82,.3)
```

---

### Modal

`createPortal`로 `document.body`에 마운트 권장.

```
backdrop: position fixed, inset 0, background rgba(0,0,0,.45)
  opacity 0 → open: opacity 1, transition: 0.2s
modal box: background surface, border 1px solid borderMd, border-radius 10px
  box-shadow: 0 20px 60px rgba(0,0,0,.25)
  max-width: 400px (confirm/delete), 420px (form)
  transform: translateY(8px) scale(.98) → open: none

modal-head: padding 14px 18px, border-bottom 1px solid border
  title: font-size 13px, font-weight 600, color text1
  icon chip: width/height 28px, border-radius 8px (variant별 색상)
  close button: 26px, color text3

modal-body: padding 18px, font-size 13px, color text2, line-height 1.6

modal-foot: padding 12px 18px, border-top 1px solid border, background surface2
  justify-content flex-end, gap 8px
```

**3가지 variant:**

| type | icon bg | icon color | 주 버튼 |
|------|---------|------------|--------|
| Delete | `rgba(224,82,82,.1)` | `#e05252` | btn--danger |
| Confirm | `rgba(99,130,220,.1)` | `#5a7bcc` | btn--primary |
| Form | `tealDim` | `teal` | btn--primary |

---

### Toast

화면 우측 하단 fixed. 2.8초 후 자동 dismiss.  
`createPortal` + `position: fixed, bottom: 24px, right: 24px`

```
background: #1e2023 (dark, 라이트모드에서도 동일)
color: #f0f2f4
padding: 11px 14px 11px 12px, border-radius: 6px
font-size: 12.5px, font-weight: 500
box-shadow: 0 4px 20px rgba(0,0,0,.35)
opacity 0 + translateY(10px) → show: opacity 1 + translateY(0)

icon chip: width/height 18px, border-radius 50%
```

| variant | icon bg | icon color |
|---------|---------|------------|
| success | `rgba(61,139,110,.3)` | `#4fa882` |
| info | `rgba(99,130,220,.3)` | `#7a9bdd` |
| warning | `rgba(204,166,54,.3)` | `#cca836` |
| error | `rgba(224,82,82,.3)` | `#e05252` |

---

### Empty State

```
flex-column, align-items center, padding 40px 20px, color text3, text-align center
icon: opacity 0.35
title: font-size 13px, font-weight 600, color text2
desc: font-size 12px
+ optional action Button
```

---

## 5. Page Layout Pattern

### 전체 레이아웃

```
TopNav (fixed, height: 52px, z-index: 100)
  └── Sidebar (fixed, left: 0, top: 52px, width: 200px, z-index: 90)
  └── Main (margin-left: 200px, padding: 0 32px 80px)
        └── PageHeader (sticky, top: 52px, z-index: 80)
              ← breadcrumb + title + action buttons (Back / Save / Submit)
        └── Content (section cards, tables, tabs...)
```

### Sticky Page Header (detail pages)

```
position: sticky
top: var(--nav-h)   ← 52px
z-index: 80
background: bg (배경과 동일해야 스크롤 시 가려짐)
padding: 20px 0 16px
margin-top: -20px   ← 상단 여백 상쇄
border-bottom: 1px solid border
```

액션 버튼 배치: `Back to List (ghost) | Save (default) | Submit (primary)`

---

## 6. 다크모드 토글

```ts
// React에서
const toggleTheme = () => {
  const html = document.documentElement
  html.dataset.theme = html.dataset.theme === 'dark' ? '' : 'dark'
}
```

styled-components ThemeProvider와 함께 쓸 경우:
- `[data-theme="dark"]` CSS selector 또는
- ThemeProvider에 `darkTheme` 오브젝트를 전달하는 방식 둘 다 가능

---

## 7. 컴포넌트 클래스명 → Prop 매핑 참고

| HTML class | React prop 제안 |
|-----------|----------------|
| `.btn--primary` | `variant="primary"` |
| `.btn--sm` | `size="sm"` |
| `.badge--submitted` | `status="submitted"` |
| `.cii-a` ~ `.cii-e` | `rating="A"` ~ `rating="E"` |
| `.tbl-wrap--sticky` | `stickyHeader={true}` |
| `.tr.pinned` | `pinned={true}` |
| `.tr.selected` | `selected={true}` |
| `.alert--info` | `variant="info"` |
| `.modal (open)` | `open={true}` |
| `.drw (open)` | `open={true}` |

---

## 8. 라이브 데모에서 사용된 샘플 데이터

### Vessel data (fleet-list)

```ts
const vessels = [
  { name: 'KR OCEAN STAR',   imo: '9876543', type: 'Bulk Carrier', flag: 'Panama',       gt: '82,400',  cii: 'B', built: '2014', cls: 'KR',  mrv: 'POS SM(GEARS)', s2: 'Approved',  s3: 'Approved',  dv: 'Submitted', ciiSt: 'Approved'  },
  { name: 'HARMONY QUEEN',   imo: '9543210', type: 'Tanker',       flag: 'Marshall Is.', gt: '105,700', cii: 'A', built: '2017', cls: 'LR',  mrv: 'POS SM(GEARS)', s2: 'Approved',  s3: 'Approved',  dv: 'Approved',  ciiSt: 'Approved'  },
  { name: 'SEOUL PIONEER',   imo: '9112233', type: 'Container',    flag: 'Liberia',      gt: '64,200',  cii: 'C', built: '2011', cls: 'DNV', mrv: 'POS SM(GEARS)', s2: 'Revision',  s3: 'Submitted', dv: 'Saved',     ciiSt: 'Submitted' },
  { name: 'GREEN HORIZON',   imo: '9667788', type: 'Tanker',       flag: 'Bahamas',      gt: '118,500', cii: 'D', built: '2009', cls: 'BV',  mrv: 'TEST(Gears)',   s2: 'Submitted', s3: 'Saved',     dv: 'Saved',     ciiSt: 'Saved'     },
]
```

---

## 9. 참고 파일 위치 (HTML 프로토타입)

| 파일 | 내용 |
|------|------|
| `docs/gears-components.html` | 전체 컴포넌트 라이브러리 (토큰 + Atoms + Molecules + Organisms) |
| `docs/gears-fleet-list.html` | Fleet list 페이지 (table + side drawer + selection bar) |
| `docs/gears-notice-list.html` | Notice list 페이지 (pinned row table + filter popover + pagination) |
| `docs/gears-notice-detail.html` | Notice detail 페이지 |
| `docs/gears-notice-write.html` | Notice 작성 페이지 (rich text editor) |
| `docs/gears-mrv-detail.html` | MRV 신청서 detail (5-tab form + checklist + billing) |
| `docs/gears-login.html` | 로그인 페이지 (split-panel + SSO) |
| `docs/gears-dashboard-redesign.html` | 대시보드 (fleet overview + charts + EU ETS) |
| `docs/index.html` | 디자인 시스템 인덱스 |

---

*이 문서는 `docs/gears-components.html` 기준으로 작성되었습니다. 실제 구현 시 해당 HTML 파일의 CSS를 참조하여 styled-components로 포팅하세요.*
