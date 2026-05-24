# ARCH — design-apparel-street Spec

**Status:** Approved  
**Author:** torifo  
**Created:** 2026-05-18  
**Updated:** 2026-05-18

---

## 1. Overview

### Problem Statement
ストリートウェア好きの若者（19–24歳）が好むブランドサイトは「重い・遅い・情報過多」か、反対に「地味すぎてカルチャーを感じない」かに二極化しており、エディトリアル誌のような没入感とストリートの生々しさを両立するデザインは希少。

### Goal
Highsnobiety的エディトリアル感と渋谷ストリートの緊張感を体現した架空ブランド「ARCH」のランディングページを実装し、デザイン研究として公開する。カスタムカーソル・フィルムグレイン・グリッドブレイクなどのUIテクニックを検証する。

### Non-Goals
- 実際のカート・決済機能
- CMS・データベース連携
- ユーザー認証

### Background
- 既存の `/Users/akito-shoji/dev/design/apparel/index.html` を元に精緻化
- ARCHは本デザイン研究のために作成した架空ブランドであり、実在のブランド・店舗・商品ではない
- `design-apparel-street` リポジトリ、`design.apparel-street.riumu.net` 独自ドメイン予定
- 同シリーズ4作のうちの1作

---

## 2. User Stories

| ID | Persona | Want to | So that |
|----|---------|---------|---------|
| US-01 | street（19–24歳・男性中心） | ページを開いた瞬間にブランドのクールさを感じたい | 「自分のためのブランド」と即座に判断できる |
| US-02 | street | 商品を雑誌を見るように流し見したい | 気になったものをピックできる |
| US-03 | street | ブランドのスタンスを短い言葉で確認したい | 哲学が合うかを判断できる |
| US-04 | street | スマートフォンでも同じ体験を得たい | 外出先でも余韻を持てる |

### Acceptance Criteria (EARS notation)

**US-01: ファーストビューでのブランド体験**
- WHEN ページが読み込まれた THEN ローダー（ロゴ+バー）が1.4秒以内に消え、ヒーローが現れる
- WHEN ヒーローが表示された THEN 超大型タイポグラフィ「WEAR WHAT YOU MEAN.」がサイバーライムのアクセントとともに視認できる
- WHEN ユーザーがスクロールし始めた THEN ヒーローのタイポグラフィがパララックスで浮き上がる

**US-02: 商品グリッドブラウズ**
- WHEN ユーザーが商品グリッドに到達した THEN 4枚の商品が非対称オフセット配置で表示される
- WHEN 商品カードにホバーした THEN 画像がズーム（scale 1.07）+ グレースケール解除される
- WHEN スクロールで商品が視野に入った THEN staggeredフェードインが実行される

**US-03: ブランドスタンス確認**
- WHEN ストーリーセクションに到達した THEN 白背景反転セクションでブランドステートメントが読める
- WHEN ユーザーが読んだ THEN 「服は言語だ」のコンセプトと2段組テキストが確認できる

**US-04: モバイル対応**
- WHEN 375px幅で閲覧した THEN 全セクションが横スクロールなしで表示される
- WHEN モバイルで閲覧した THEN カスタムカーソルは非表示になり、デフォルトカーソルになる

---

## 3. Functional Requirements

| ID | Requirement | Priority | Notes |
|----|-------------|----------|-------|
| FR-01 | ページロードアニメーション（ARCH ロゴ+バー） | P0 | 1.4秒 |
| FR-02 | フィルムグレイン固定オーバーレイ | P0 | SVG noise, opacity 0.04 |
| FR-03 | カスタムカーソル（ドット+遅延追従リング） | P0 | モバイルは非表示 |
| FR-04 | フルスクリーンヒーロー（写真+超大型タイポ+CTA） | P0 | パララックス付き |
| FR-05 | 12カラムグリッドブレイク商品配置（4商品） | P0 | 非対称オフセット |
| FR-06 | マーキーテキスト（無限ループ） | P1 | ホバーで一時停止 |
| FR-07 | ブランドストーリー（ライト背景反転） | P1 | アウトラインテキスト |
| FR-08 | カテゴリセクション（2カラム大判） | P1 | |
| FR-09 | フィーチャーストリップ（3カラム） | P2 | 送料・返品・サステナ |
| FR-10 | スクロールリビールアニメーション | P1 | IntersectionObserver |
| FR-11 | ナビ（スクロールでブラー+ボーダー） | P0 | |
| FR-12 | モバイルファースト対応（375px基準） | P0 | |

---

## 4. Architecture

### Page Structure

```
index.html
├── <div class="loader">           # ARCH ロゴ + プログレスバー
├── <div class="grain">            # fixed, pointer-events:none
├── <div class="cursor-dot">       # カスタムカーソル（ドット）
├── <div class="cursor-ring">      # カスタムカーソル（リング）
├── <nav>                          # ロゴ左、リンク右
├── <section class="hero">         # フルスクリーン + パララックス
├── <section class="arrivals">     # 12カラムグリッドブレイク
├── <div class="marquee">          # 無限スクロール
├── <section class="story">        # 白背景反転
├── <section class="categories">   # 2カラム
├── <div class="features">         # 3カラムストリップ
└── <footer>                       # ミニマル
```

### Component Responsibilities

| Component | Responsibility |
|-----------|---------------|
| Loader | ブランドロゴのファーストインプレッション演出 |
| Grain | フィルム質感。全体に固定オーバーレイ |
| Cursor | インタラクション強化。ホバー時にリングが拡大 |
| Hero | 超大型タイポで世界観を一撃で伝える |
| Arrivals | 非対称グリッドで「雑誌を見ている」感 |
| Marquee | ブランドキーワードとエネルギーの供給 |
| Story | 白地反転でセクション間のメリハリ |

### Key Design Decisions

| Decision | Chosen | Rationale | Rejected alternatives |
|----------|--------|-----------|----------------------|
| テーマ | ダークモード（オフブラック） | ストリートウェアの重力感・シリアスさ | ライト（trendと被る） |
| Display font | Clash Display（Fontshare） | 幾何学コンデンスでハイプカルチャー感 | Anton（汎用すぎ）、Impact（古い） |
| アクセントカラー | サイバーライム #C8FF00 | 黒背景との最大コントラスト、Y2K感 | 赤（ありきたり）、白（地味） |
| グリッド | 12カラムブレイク（非対称） | 雑誌的発見感。整列は単調 | 等幅4カラム（FORMっぽい） |
| カーソル | ドット+遅延追従リング | インタラクション品質の差別化 | なし（体験が弱い） |
| Grain強度 | opacity 0.04 | 主張しすぎず質感を出す | 0.08（うるさい）、0（質感なし） |

---

## 5. Design System

### Color Palette
```css
--bg:           #090907;   /* オフブラック */
--bg-sub:       #111110;
--bg-card:      #131310;
--fg:           #F4EFE6;   /* クリームホワイト */
--fg-muted:     #6B6560;
--border:       #1D1D1A;
--accent:       #C8FF00;   /* サイバーライム */
--accent-warm:  #E8C84A;   /* ゴールド */
```

### Typography
```css
--font-display: 'Clash Display', 'Noto Sans JP', sans-serif;
--font-body:    'DM Sans', 'Noto Sans JP', sans-serif;
```
- Fontshare CDN: Clash Display
- Google Fonts CDN: DM Sans, Noto Sans JP

### Spacing & Motion
```css
--ease: cubic-bezier(0.16, 1, 0.3, 1);  /* 速い立ち上がり・スローアウト */
/* hero title: slideUp 1.1s, stagger 0.12s */
/* cursor ring: lag factor 0.12 (RAF loop) */
/* parallax: scrollY * 0.12px */
```

---

## 9. Testing Strategy (Visual QA)

| Layer | Scenarios |
|-------|-----------|
| Desktop (1280px) | グリッドブレイク確認、カーソル動作、パララックス |
| Mobile (375px) | カーソル非表示、グリッド2カラム化、マーキー速度 |
| アニメーション | ローダー1.4秒、stagger reveal、マーキーシームレス |
| ホバー | 商品ズーム+グレースケール解除、カーソルリング拡大 |
| フォント | Clash Display・DM Sans 正常適用確認 |

---

## 10. Implementation Notes

- **ベースファイル**: `/Users/akito-shoji/dev/design/apparel/index.html` から移行・整理
- **Grain**: `position:fixed; inset:-100%; width:300%; height:300%` で画面全体をカバー、`animation: grainShift 0.4s steps(1) infinite` でチラつき演出
- **カーソルリング遅延**: `requestAnimationFrame` ループで `rx += (target - rx) * 0.12` の慣性追従
- **パララックス**: `scroll` イベントで `heroTitle.style.transform = translateY(scrollY * 0.12px)` — `will-change: transform` 付与
- **グリッドオフセット（意図的な非対称）**: 2枚目は `margin-top: 5rem`、4枚目は `grid-column: 3/7; margin-top: 2.5rem`
  - **設計意図**: 上部 Arrivals グリッドは「雑誌的非対称オフセット」（FR-05 / US-02 AC / Key Design Decisions）で、4 枚の**上端**を意図的にズラす。これは「整列＝単調」を避け、エディトリアル誌（Highsnobiety等）のグリッドブレイク感を再現するため
  - **下部 Categories との対比**: 下部 `.cat-grid` は 2 カラム整列（cat-card は全て同一 aspect-ratio・margin なし）で、上のグリッドブレイクとの**意図的なリズム差**を作っている。「上はカオス＝発見感、下は整然＝選びやすさ」というセクション役割の使い分け
  - **FB-017 受領（2026-05-25）**: 「上の写真の高さが揃ってないのは敢えて？」というレビュー指摘あり。**意図的**であり、整列させると本来のコンセプトが崩れるため修正しない判断。将来の同種レビューを抑止するため、index.html の `.arrivals-grid` 周辺に意図を示すコメントを追加
- **マーキー**: 8アイテム（4×2セット）で `translateX(-50%)` アニメ

---

## 11. Open Questions

| # | Question | Owner | Due | Status |
|---|----------|-------|-----|--------|
| 1 | 既存 index.html を完全置換するか、このspec.mdから新規実装するか | torifo | 実装開始時 | Open |
| 2 | `design.apparel-street.riumu.net` のDNS設定タイミング | torifo | 後日 | Open |

---

## References

- [spec.md（ナビゲーター）](../spec.md)
- [既存実装](../index.html)
- Font: [Clash Display](https://www.fontshare.com/fonts/clash-display), [DM Sans](https://fonts.google.com/specimen/DM+Sans)
- Inspiration: [Highsnobiety](https://www.highsnobiety.com), [UNDERCOVER](https://undercoverism.com)
