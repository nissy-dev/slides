---
layout: section
fonts:
  sans: 'M PLUS'
  mono: 'Monaco'
title: タイトル
canvasWidth: 800
transition: 'view-transition'
---

<div class="flex flex-col text-5xl leading-relaxed">

<div>フロントエンドにも広がる</div>
<div>OpenTelemetry</div>

</div>

<div class="opacity-70 mt-4">

ブラウザでの計装が動き出した 2026 年

</div>

<!--
挨拶。今日は10分で「OpenTelemetry のいま」を、特にフロントエンドの動きにしぼって話します。
準備は真剣に、本番は気楽に。
-->

---
transition: 'view-transition'
---

# 自己紹介

<div class="flex items-center mt-4">

<div class="flex-1 text-2xl leading-relaxed">

- Daiki Nishikawa
  - GitHub: @nissy-dev
  - X: @nissy_dev
- Cybozu のソフトウェアエンジニア
  - フロントエンドの横断技術支援
  - AIを用いた脆弱性検出基盤（ハーネス）の整備

</div>

<img
  src="https://avatars.githubusercontent.com/u/17228098"
  class="w-40 h-40 rounded-full shadow-lg ring-4 ring-white/70 shrink-0"
/>

</div>

<!--
自己紹介は短く。なぜ自分がこの話をするのか＝この分野を追ってきた、という信頼づけだけしておく。
-->

---
transition: 'view-transition'
---

# 今回の発表で伝えたいこと

<div class="text-2xl mt-4">

- OpenTelemetry は、もう "サーバーサイド" だけの話ではありません
- フロントエンドでの仕様の策定、SDK の実装が進んでいます
- フロントエンドでもベンダー非依存の監視の実装が可能になる日が来るかも

</div>

<!--
まず、今日の発表で覚えてほしいことを先にまとめさせてもらうと、次のようになるかなと思います。

では、発表の本題を初めていきますね。
-->

---
transition: 'view-transition'
---

# OpenTelemetry とは？

<div class="flex flex-1 flex-col text-2xl mt-4">

- テレメトリ (トレース / メトリクス / ログ) を扱う共通仕様
  - 監視ツールを提供するベンダーに実装がロックインするのを防ぐ
- 5月には CNCF の Graduated Projects として認定された[^1] 🎉
  - CNCF: Cloud Native Computing Foundation
  - 他には Kubernetes、Prometheus、Fluentd など

</div>

[^1]: https://opentelemetry.io/ja/blog/2026/otel-graduates/

<!--
まず OpneTelemetry を聞いたことない人もいるかもしれないので、OpneTelemetry とはなんぞやというところを説明します。
-->

---
transition: 'view-transition'
---

# どこで使われている？

<div class="text-2xl mt-4">

- 🙋 サーバーサイドで使っている人？
- 🙋 フロントエンドで使っている人？

</div>

<div v-click class="text-2xl opacity-70 mt-4">

サーバーサイドでの利用はよく見る気がする<br/>
あれ、フロントエンドは...?

</div>

<!--
2つ続けて挙手してもらう。会場でこの「差」を体感させるのが狙い。
この差が、次の「なぜ？」につながる。
-->

---
transition: 'view-transition'
---

# フロントエンドでの現状

<div class="text-2xl mt-4">

- <logos-sentry /> や <logos-datadog /> などの SaaS の SDK の利用が主流
- フロントエンドの監視まで手に回ってないチームも多そう
- OpenTelemetry で "安定して" できるのはトレースの送信だけ
  - `@opentelemetry/sdk-trace-web` を利用して実装できる


</div>

<!--
ロゴを出しつつ、「すでに便利な選択肢がある」ことが普及していない理由、と説明する。
ロゴ素材は public/ に差し替え可能。
-->

---
transition: 'view-transition'
---

# OpenTelemetry での動き

<div class="flex flex-1 flex-col text-2xl mt-4">

- Client SDK and Instrumentation として議論はされていた
  - 議事録[^2]を見る限り 2021年ごろから
- ブラウザだけではなくモバイル (Android/iOS) も含む議論
  - 議論の対象範囲が広く、共通設計に2年以上の時間がかかっていた

</div>

[^2]: https://docs.google.com/document/d/16Vsdh-DM72AfMg_FIt9yT9ExEWF4A_vRbQ3jRNBe09w/edit?tab=t.0#heading=h.n5vcc992gs6y

<!--
自分も気になって調べたら、2021年ごろから Client side の実装が議論されていた、という発見を共有する。
過去の議論ドキュメントが残っている（PLAN.md のリンク参照）。
-->

---
transition: 'view-transition'
---

# Browser SDK としての独立

<div class="flex flex-1 flex-col text-2xl mt-4">

- 昨年中頃から、ブラウザだけ独立して SDK 開発を進めることに
  - より迅速な意思決定・開発を目指して
  - Grafana Labs、Elastic などに所属するメンバーが参画
- github: open-telemetry/opentelemetry-browser
  - 今年に入ってから実装もかなり活発になっている

</div>

<!--
ここが今日の山場。
モチベーションの高いブラウザが独立したことで、開発が一気に前に進み始めた。
-->
---
transition: 'view-transition'
---

# SDK の実装の現在地

<div class="flex flex-1 flex-col text-2xl mt-4">

- 基本的なテレメトリ収集ツールはすでに実装済み
  - ユーザー操作 / Core Web Vitals / エラーなど
  - `@opentelemetry/browser-instrumentation` として利用可能
- 既存のブラウザ向けツールもこのリポジトリに集約予定
  - opentelemetry-js や opentelemetry-js-contrib にあるもの
  - fetch / xml-http-request / document-load など

</div>

<!--
現在地を共有。各 instrumentation の実装状況は repo を見るのが早い。
既存ツールは opentelemetry-js / opentelemetry-js-contrib に散在していたが、こちらに移して集中管理する方針、と口頭で補足。
スクショを public/ に置いて差し替えると、より伝わる。
-->
---
transition: 'view-transition'
---

# 実用に向けて気になる点: エラーの復元

<div class="flex flex-1 flex-col text-2xl mt-4">

- minify されたエラーのスタックトレースの復元は誰の責務？
  - source map で元コードに対応づける処理 = symbolication
- 復元をどこで担うかが定まっていない
  - SaaS はソースマップの保持と復元まで行なっている
  - 一方 OpenTelemetry Collector では未対応
  - Loki などバックエンド側の対応にもばらつきがある

</div>

<!--
エラーのスタックトレースの復元（symbolication）も unknown な論点として共有する。
Collector も送信先も現状は担わないため、どこで解決するかが未定。
この後、もう一つの論点 Session Replay に入る。まず実物を見せる。
-->

---
transition: 'view-transition'
---

# 実用に向けて気になる点: Session Replay

<div class="flex justify-center mt-4">

<video class="w-full rounded-lg shadow-lg" src="https://docs.dd-static.net/images//getting_started/session_replay/preview.mp4" autoplay loop muted playsinline controls></video>

</div>

<!--
Session Replay を知らない人向けに、まず実物を見せる。
ユーザー操作を録画のように再現できる機能。次のスライドで、これをベンダー非依存でどう共通化するかが論点、と繋げる。
-->

---
transition: 'view-transition'
---

# 実用に向けて気になる点: Session Replay

<div class="flex flex-1 flex-col text-2xl mt-4">

- Session Replay はどう共通仕様としてまとめるのか？
  - rrweb [^3]をベースに各社作っていると思うが、それぞれのデータの見せ方に合わせてカスタマイズはされていそう
  - issue は作成されているが、特にレスポンスはない[^4]

</div>

[^3]: https://github.com/rrweb-io/rrweb

[^4]: https://github.com/open-telemetry/opentelemetry-browser/issues/32

<!--
正直に、まだ unknown な部分も共有する。
Session Replay: どう実現するかは不明瞭。ここは今後の見どころ。
次のスライドで Session Replay の実例（Datadog）を見せる。
-->

---
layout: center
transition: 'view-transition'
---

<div class="flex flex-col text-4xl text-center">

<div class="mb-4">OpenTelemetry は</div>

<div>フロントエンドに広がりつつあります</div>

<div class="text-lg opacity-70 mt-8">

気になったら opentelemetry-browser を覗いてみてください

</div>

</div>


<!--
最後にコアメッセージを再提示。
締めは気楽に。「フロントの動向、面白くなってきたので追ってみてください」で終える。
-->
