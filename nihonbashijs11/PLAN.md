# Plan: nihonbashijs11 — OpenTelemetry Browser スライド

10分の発表。「伝わる発信のつくりかた」の設計思想（誰に・何を・どの順で）に沿って構成する。
発信指針の詳細はリポジトリルートの [AGENTS.md](../AGENTS.md) を参照。

## 発表の目的（確定：A 動向共有中心）

最新の技術動向をフラットに共有し、「OpenTelemetry はもうサーバーだけじゃない」と気づいてもらう。
採用の後押しやコミュニティ参加の呼びかけは、締めで軽く添える程度に留める。

## コアメッセージ（一文・先出し＆締めで再提示）

> OpenTelemetry はもうサーバーだけのものじゃない

## ターゲット（一人に具体化）

Web アプリのフロントを書くエンジニア。Sentry / Datadog RUM 等の SaaS は業務で使用。
バックエンドで OTel を軽く触った程度で「OTel＝サーバーの計装」という認識。

→ 説明の粒度: トレーシング／オブザーバビリティの基礎は深掘りしない。
OSS 標準でフロントを計装できる意義・SIG 体制・instrumentation の現状にフォーカスする。

## 構成テンプレート＝課題解決型

前提 → 疑問(=課題) → なぜ起きた → 転機(解決) → 現在地 → 残課題 → まとめ

## アウトライン（見出しだけで伝わる／同粒度・全13枚）

### 第1幕 前提と疑問

1. **OpenTelemetry はもうサーバーだけのものじゃない**（タイトル・サブタイトルで内容を示す）
2. **なぜ自分がこれを話すか**（自己紹介・短く・信頼をつくる）
3. **今日持ち帰ってほしい一言**（コアメッセージ先出し）
4. **OpenTelemetry とは**（挙手① → 一枚で前提を揃える・比喩）
5. **使われ方のギャップ**（挙手②サーバー / 挙手③フロント → 差を体感）

### 第2幕 なぜ？と転機（ストーリー）

6. **なぜフロントでは使われないのか**（Sentry / Datadog / NewRelic のロゴ）
7. **実は議論は2021年から始まっていた**
8. **Client と一口に言っても複数ある**（ブラウザ / モバイル(iOS/Android)・固有事情で難航）
9. **転機：去年ブラウザが SIG 独立**（＝ OpenTelemetry Browser）
10. **追い風：今年 Graduated Project に**（説得材料）

### 第3幕 現在地と展望

11. **どこまで動くのか：instrumentation の現在地**（表・repo リンク・図）
12. **まだ解けていない課題**（sourcemap symbolication: collector 未対応 / honeycomb processor、session replay）
13. **持ち帰ってほしいのは一つ**（コアメッセージ再提示 ＋ 一言アクションは軽め）

## セクション時間配分（10分・リハで調整）

| セクション | スライド | 目安 |
| --- | --- | --- |
| 導入 | 1-3 | 1.5分 |
| 前提と疑問 | 4-5 | 1.5分 |
| なぜ・転機 | 6-10 | 4分 |
| 現在地・課題 | 11-12 | 2.5分 |
| まとめ | 13 | 0.5分 |

## スライド制作ルール

- 各スライドに意味を持つ見出しを付ける（「Example」だけの見出しは禁止）
- 重要情報（結論・図）は上半分、ページ番号・注釈は下
- 大きい文字を使い、コントラストを十分に確保（shiki テーマ・背景色に注意）
- 本文は最小限にし、補足・エピソードは `<!-- スピーカーノート -->` へ（読ませない）
- コードは4行程度 ＋ shiki ハイライト ＋ 抜粋
- 文章は最後に自分の言葉でリライトする
- 締めは「準備は真剣・本番は気楽」のトーンで

## 制作プロセス

- 発散 → 収束: キーワード出し → 並べ替えは上記アウトラインで完了
- リハーサル: 通しで「技術の話が出るまで長くないか」「時間配分」を確認し、必要なら（話し方でなく）構成そのものを入れ替える

## Phase 1: プロジェクトセットアップ（jsconf2023 踏襲）

- `nihonbashijs11/` に `package.json` / `setup/shiki.ts` / `vercel.json` / `public/` / `README.md`
- 依存: `@slidev/cli`, theme, `@iconify-json/logos`
- scripts: `dev` / `build` / `export`

参考実装:

- `jsconf2023/slides.md`: frontmatter(layout/fonts/transition)、`layout: section/center/image-right`、`<Transform :scale>`、`<!-- スピーカーノート -->`
- `jsconf2023/setup/shiki.ts`, `jsconf2023/vercel.json`, `jsconf2023/public/`

## 素材

- Sentry / Datadog / NewRelic / OpenTelemetry のロゴ
- opentelemetry-browser repo の instrumentation 状況スクリーンショット

## 未確定

- ロゴ素材を logos iconset で賄うか、`public/` に画像配置するか

## 参考リンク

- OpenTelemetry Browser: <https://github.com/open-telemetry/opentelemetry-browser>
- honeycomb collector symbolicator: <https://github.com/honeycombio/opentelemetry-collector-symbolicator>
- 過去の議論: <https://docs.google.com/document/d/16Vsdh-DM72AfMg_FIt9yT9ExEWF4A_vRbQ3jRNBe09w/edit>
