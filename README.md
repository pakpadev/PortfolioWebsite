# PortfolioWebsite

Pakpa のポートフォリオサイトです。`docs/` 内の要件定義・画面設計・参考 HTML をもとに、GitHub Pages へそのまま配置しやすい静的サイトとして実装しています。

## 構成

- `index.html`: サイト本体
- `assets/styles.css`: デザイン、レスポンシブ、アニメーション
- `assets/app.js`: ナビゲーション、タイプライター、パーティクル、スクロール演出
- `assets/og-image.svg`: OGP 用画像
- `docs/`: 要件定義と参考資料

## ローカル確認

小規模な静的サイトのため、Docker やビルドは不要です。`index.html` をブラウザで開くと確認できます。

PowerShell から開く場合:

```powershell
Start-Process .\index.html
```

## カスタマイズ箇所

- 連絡先リンク: `index.html` の `#contact` 内の `href="#"` と `mailto:your@email.com`
- プロジェクトリンク: `#projects` 内の `GitHub` / `Demo` リンク
- プロフィール文・経歴: `#about` と `#experience`
