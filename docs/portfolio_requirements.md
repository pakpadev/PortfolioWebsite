# エンジニアポートフォリオサイト 要件定義書

**作成日**: 2026-04-21  
**バージョン**: 1.0  
**プロジェクト名**: Pakpa Portfolio — *Cyberspace Edition*

---

## 1. プロジェクト概要

AIおよびブロックチェーン技術を専門とするエンジニアのポートフォリオサイト。  
「電子空間（Cyberspace）」をビジュアルテーマに、技術的な深みと洗練されたデザインで訪問者に強い印象を与える一枚構成のLP（ランディングページ）。

---

## 2. 技術スタック

| カテゴリ | 採用技術 |
|---|---|
| フロントエンド | React + TypeScript (Vite) |
| スタイリング | Tailwind CSS + CSS Variables |
| アニメーション | Framer Motion |
| アイコン | Lucide React / React Icons |
| ルーティング | なし（SPA / スクロールナビ） |
| デプロイ | GitHub Pages |
| ビルドツール | Vite |
| CI/CD | GitHub Actions（自動デプロイ） |

---

## 3. デプロイ要件

### 3-1. GitHub Pages 設定

- リポジトリ: `{username}.github.io` または `{username}/portfolio`
- ブランチ戦略: `main` ブランチへのpushで `gh-pages` ブランチへ自動デプロイ
- ビルド出力先: `dist/`
- `vite.config.ts` にて `base` を適切に設定（サブディレクトリデプロイの場合 `/portfolio/`）

### 3-2. GitHub Actions ワークフロー例

```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm run build
      - uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

---

## 4. デザイン要件

### 4-1. テーマコンセプト

**「Cyberspace」— 電子空間**

- デジタルの奥行きと光を表現する暗背景 × ネオン発光カラー
- グリッドライン / ワイヤーフレーム的なUI要素
- スキャンライン・グリッチエフェクト・パーティクルなど電子空間の質感
- テキストは「ターミナル風」+「スリムなサンセリフ」の混在

### 4-2. カラーパレット

| 用途 | 変数名 | カラーコード |
|---|---|---|
| 背景（ベース） | `--bg-base` | `#030712` |
| 背景（サブ） | `--bg-sub` | `#0d1117` |
| グリッドライン | `--grid-line` | `#0f2a3f` |
| アクセント1（シアン） | `--accent-cyan` | `#00f5ff` |
| アクセント2（紫） | `--accent-purple` | `#7b2fff` |
| アクセント3（グリーン） | `--accent-green` | `#00ff9f` |
| テキスト（メイン） | `--text-primary` | `#e2e8f0` |
| テキスト（サブ） | `--text-muted` | `#64748b` |
| ボーダー | `--border` | `#1e3a4a` |
| グロウ（発光） | `--glow-cyan` | `0 0 20px rgba(0,245,255,0.4)` |

### 4-3. タイポグラフィ

| 用途 | フォント | 特徴 |
|---|---|---|
| 見出し（英語） | `Share Tech Mono` | ターミナル/モノスペース感 |
| 見出し（日本語） | `Noto Sans JP` | 細め（weight 300-400） |
| ボディ | `JetBrains Mono` | コードっぽいテキスト |
| アクセント文字 | `Orbitron` | SF/テック感のあるディスプレイ体 |

### 4-4. ビジュアルエフェクト

- **パーティクル背景**: 浮遊する点と繋がる線（Canvas または CSS）
- **グリッドオーバーレイ**: パースペクティブグリッドを遠景に配置
- **グリッチアニメ**: ヒーローセクションのテキストに断続的なグリッチ
- **スキャンライン**: 半透明の横線オーバーレイ（全体）
- **ネオングロウ**: カード・ボタン・バッジにbox-shadow発光効果
- **スクロールフェードイン**: Framer Motion の `whileInView` でセクションごとに出現

---

## 5. ページ構成（セクション）

一枚のLPとして以下のセクションをスクロール形式で構成。

### 5-1. セクション一覧

| # | セクションID | 名称 | 概要 |
|---|---|---|---|
| 1 | `#hero` | ヒーロー | フルスクリーン。名前・肩書き・一言キャッチ |
| 2 | `#about` | About | 自己紹介・バックグラウンド |
| 3 | `#skills` | Skills | 技術スキルのビジュアル表示 |
| 4 | `#projects` | Projects | 制作物・プロジェクト一覧 |
| 5 | `#experience` | Experience | 職歴・経験タイムライン |
| 6 | `#contact` | Contact | SNSリンク・連絡先 |

### 5-2. セクション詳細

#### Hero セクション
- フルスクリーン（`100vh`）
- パーティクル or グリッドアニメーション背景
- `<h1>`: 名前（グリッチエフェクト付き）
- `<h2>`: 肩書き（例: `AI Engineer / Blockchain Developer`）タイピングアニメーション
- CTAボタン: 「View Projects」「Contact」
- スクロールダウンインジケーター

#### About セクション
- アバター/プロフィール画像（任意）
- テキスト2〜3段落（自己紹介）
- キーワードバッジ（例: `#AI`, `#Blockchain`, `#Node.js`, `#AWS`）

#### Skills セクション
- カテゴリ別グリッドカード（AI / Blockchain / Infrastructure / Tools）
- 各スキルにアイコン + 名称
- ホバーで発光アニメーション

**想定スキルカテゴリ例**:
```
AI/ML: LLM, Ollama, RAG, Fine-tuning, Claude API, OpenAI API
Blockchain: Solidity, Ethereum, Web3.js, NFT, DeFi
Backend: Node.js, TypeScript, REST API, GraphQL
Cloud/Infra: AWS (EC2, Lambda, S3), Docker
Tools: Git, Vite, GitHub Actions
```

#### Projects セクション
- カードグリッドレイアウト（2〜3列、モバイルは1列）
- 各カード: プロジェクト名 / 説明 / 使用技術バッジ / リンク（GitHub / Demo）
- ホバーで詳細オーバーレイ or スケールアップ

#### Experience セクション
- 縦タイムライン形式
- 各エントリ: 期間 / 会社名・プロジェクト名 / 役割 / 概要

#### Contact セクション
- GitHub / X (Twitter) / LinkedIn / メール等のSNSリンク
- ネオン発光のアイコンボタン
- コピーライト表記

---

## 6. ナビゲーション

- **固定ヘッダー** (`position: fixed`): スクロール時に背景ブラー + 透過
- ロゴ（名前 or イニシャル）+ セクションリンク
- モバイル時: ハンバーガーメニュー → ドロワー
- アクティブセクションのリンクをハイライト（Intersection Observer）
- スムーズスクロール（CSS: `scroll-behavior: smooth`）

---

## 7. レスポンシブ対応

| ブレークポイント | 幅 | 対応端末 |
|---|---|---|
| `sm` | 640px〜 | スマートフォン（横） |
| `md` | 768px〜 | タブレット |
| `lg` | 1024px〜 | ノートPC |
| `xl` | 1280px〜 | デスクトップ |
| `2xl` | 1536px〜 | 大型ディスプレイ |

### レスポンシブ方針

- **モバイルファースト**で設計
- グリッドは `grid-cols-1 → md:grid-cols-2 → lg:grid-cols-3` の段階的展開
- ヒーローのパーティクルエフェクトはモバイルで軽量化（描画数削減）
- フォントサイズは `clamp()` を活用してスケール
- ナビはモバイルでハンバーガーメニューに切り替え

---

## 8. パフォーマンス要件

| 指標 | 目標値 |
|---|---|
| Lighthouse Performance | 85点以上 |
| First Contentful Paint | 2秒以内 |
| Total Bundle Size | 500KB以下（gzip後） |
| 画像最適化 | WebP形式 + `loading="lazy"` |

- Viteの標準コード分割を活用
- フォントは `font-display: swap`
- パーティクルはrequestAnimationFrameで効率化
- アニメーションは `prefers-reduced-motion` に対応

---

## 9. アクセシビリティ

- セマンティックHTML（`<header>`, `<main>`, `<section>`, `<footer>`等）
- `alt` テキスト設定
- フォーカス可視化（キーボードナビ）
- カラーコントラスト比 WCAG AA 準拠（テキスト系）
- `aria-label` の適切な付与

---

## 10. ディレクトリ構成

```
portfolio/
├── public/
│   ├── favicon.ico
│   └── og-image.png          # OGP画像
├── src/
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Header.tsx
│   │   │   └── Footer.tsx
│   │   ├── sections/
│   │   │   ├── Hero.tsx
│   │   │   ├── About.tsx
│   │   │   ├── Skills.tsx
│   │   │   ├── Projects.tsx
│   │   │   ├── Experience.tsx
│   │   │   └── Contact.tsx
│   │   ├── ui/
│   │   │   ├── ParticleBackground.tsx
│   │   │   ├── GlitchText.tsx
│   │   │   ├── NeonCard.tsx
│   │   │   ├── SkillBadge.tsx
│   │   │   └── TypewriterText.tsx
│   │   └── common/
│   │       ├── SectionTitle.tsx
│   │       └── ScrollIndicator.tsx
│   ├── data/
│   │   ├── skills.ts          # スキルデータ
│   │   ├── projects.ts        # プロジェクトデータ
│   │   └── experience.ts      # 経歴データ
│   ├── hooks/
│   │   ├── useActiveSection.ts
│   │   └── useScrollAnimation.ts
│   ├── styles/
│   │   ├── globals.css        # CSS変数・リセット
│   │   └── animations.css     # グリッチ・スキャンライン等
│   ├── types/
│   │   └── index.ts
│   ├── App.tsx
│   └── main.tsx
├── .github/
│   └── workflows/
│       └── deploy.yml
├── vite.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## 11. データ定義

### プロジェクトデータ型

```typescript
interface Project {
  id: string;
  title: string;
  description: string;
  techStack: string[];
  githubUrl?: string;
  demoUrl?: string;
  category: 'AI' | 'Blockchain' | 'Web' | 'Other';
  featured: boolean;
}
```

### スキルデータ型

```typescript
interface Skill {
  name: string;
  icon: string;        // アイコン名 or SVGパス
  category: SkillCategory;
  level?: 'expert' | 'proficient' | 'familiar';
}

type SkillCategory = 'AI' | 'Blockchain' | 'Backend' | 'Cloud' | 'Tools';
```

### 経歴データ型

```typescript
interface Experience {
  id: string;
  period: string;       // 例: "2022.04 — present"
  company: string;
  role: string;
  description: string;
  tags: string[];
}
```

---

## 12. SEO / OGP

- `<title>`: `{名前} | AI & Blockchain Engineer`
- `<meta description>`: 概要文（120文字以内）
- OGP タグ（`og:title`, `og:description`, `og:image`, `og:url`）
- Twitter Card 設定
- `robots.txt` + `sitemap.xml`（任意）

---

## 13. 開発フロー

1. リポジトリ作成 & Vite + React + TS 初期化
2. Tailwind CSS / Framer Motion セットアップ
3. グローバルCSS変数・テーマ定義
4. レイアウトコンポーネント（Header / Footer）
5. 各セクション実装（Hero → About → Skills → Projects → Experience → Contact）
6. エフェクト実装（パーティクル / グリッチ / スキャンライン）
7. レスポンシブ調整
8. パフォーマンス・アクセシビリティ最適化
9. GitHub Pages デプロイ設定
10. 動作確認 & 公開

---

## 14. 今後の拡張候補（スコープ外）

- ブログ / 記事セクション（MDX対応）
- 多言語対応（日本語 / 英語）
- ダークモード / ライトモード切替
- お問い合わせフォーム（Formspree 等）
- アナリティクス（Google Analytics / Cloudflare）

---

*本要件定義書は制作開始前の合意文書として使用することを想定しています。実装フェーズで詳細が変更になる場合は本書を更新してください。*
