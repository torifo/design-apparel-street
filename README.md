[English](#english) | [日本語](#japanese)

---

<a id="english"></a>

# ARCH — design-apparel-street

> **"Wear What You Mean"**

A design study exploring a fictional youth apparel brand tailored to the **street persona** — hype-culture-driven, streetwear-focused, editorial dark aesthetic, targeting Japanese men and women aged 19–24.

ARCH is a fictional brand created for this design study. It is not a real brand, store, or product.

## Overview

| | |
|---|---|
| **Brand** | ARCH |
| **Persona** | street |
| **Live Site** | [design.apparel-street.riumu.net](https://design.apparel-street.riumu.net/) |
| **Custom Domain** | `design.apparel-street.riumu.net` |

## Design Concept

- **Color**: Off-black `#090907` × cyber lime `#C8FF00` × cream `#F4EFE6`
- **Typography**: Clash Display (display) × DM Sans (body)
- **Aesthetic**: Highsnobiety editorial × Shibuya streetwear
- **UX**: Custom cursor, film grain overlay, parallax hero typography, asymmetric grid break, infinite marquee

## Tech Stack

- Pure HTML + CSS Custom Properties + Vanilla JS
- Fontshare (Clash Display) + Google Fonts CDN
- No framework, no build step — GitHub Pages ready

## Install as a skill / スキルとして導入

This repo ships a cross-agent **`SKILL.md`** (open standard) usable by both Claude Code and Codex CLI as a design-reference skill. Link the repo into the agent's skills directory:

このリポジトリは Claude Code / Codex CLI 共通の **`SKILL.md`**（オープン標準）を同梱し、デザイン参照スキルとして使えます。

```bash
# Claude Code
ln -s "$(pwd)" ~/.claude/skills/design-apparel-street
# Codex CLI
ln -s "$(pwd)" ~/.codex/skills/design-apparel-street
```

Restart the agent; it is matched automatically by the skill's `description` (skill name: `design-apparel-street`). / エージェント再起動後、`description` に基づき自動マッチします。

## Part of

This repository is one of four design studies under the **apparel persona series**:

| Persona | Brand | Repo |
|---------|-------|------|
| trend | LUEUR | [design-apparel-trend](https://github.com/torifo/design-apparel-trend) |
| street | ARCH | [design-apparel-street](https://github.com/torifo/design-apparel-street) |
| vintage | FRAY | [design-apparel-vintage](https://github.com/torifo/design-apparel-vintage) |
| minimal | FORM | [design-apparel-minimal](https://github.com/torifo/design-apparel-minimal) |

---

<a id="japanese"></a>

# ARCH — design-apparel-street（日本語）

> **「自分の言葉で語れる服を」**

若者向けアパレルショップのデザイン研究。**streetペルソナ**（ハイプカルチャー・ストリートウェア・エディトリアル・19〜24歳）に特化した架空ブランドのサイトです。

ARCHは、このデザイン研究のために作成した架空ブランドです。実在のブランド、店舗、商品ではありません。

## 概要

| | |
|---|---|
| **ブランド** | ARCH |
| **ペルソナ** | street |
| **公開URL** | [design.apparel-street.riumu.net](https://design.apparel-street.riumu.net/) |
| **独自ドメイン** | `design.apparel-street.riumu.net` |

## デザインコンセプト

- **カラー**: オフブラック × サイバーライム × クリーム
- **フォント**: Clash Display（見出し）× DM Sans（本文）
- **世界観**: Highsnobiety × 渋谷エディトリアル
- **UX**: カスタムカーソル、フィルムグレイン、超大型パララックスタイポグラフィ、グリッドブレイク

## 技術

- 純粋なHTML + CSS Custom Properties + Vanilla JS
- Fontshare + Google Fonts CDN、ビルド不要でGitHub Pages対応

## シリーズ

このリポジトリはアパレル・ペルソナシリーズ4作のうちの1つです。  
ナビゲーターページ: [apparel-design](https://github.com/torifo/apparel-design)
