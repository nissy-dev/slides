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

- OpenTelemetry は、もう "サーバーサイド" だけの話ではありません！
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

- より高速化な意思決定や開発を目指して、ブラウザに関しては昨年の中頃から独立して SDK 開発を進めることに
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

- ユーザー操作、Core Web Vitals、エラーなどを回収するためのツールはすでに実装されている
  - `@opentelemetry/browser-instrumentation`
- opentelemetry-js や opentelemetry-js-contrib に実装されていたブラウザ関連のツールも、こちらのリポジトリに移行して集中管理する予定のよう
  - fetch / xml-http-request / document-load など

</div>

<!--
現在地を共有。各 instrumentation の実装状況は repo を見るのが早い。
スクショを public/ に置いて差し替えると、より伝わる。
-->

---
transition: 'view-transition'
layout: two-cols-header
---

# 実用に向けて気になっている点

::left::

<div class="text-xl mt-4 pr-4">

- Session replay のようなデータの見せ方とも非常に関係のある機能をどう実現するのか
  - issue は作成されているが、特にレスポンスはない[^3]

</div>

[^3]: https://github.com/open-telemetry/opentelemetry-browser/issues/32

::right::

<div class="h-full flex items-center">

<iframe
  class="w-full aspect-video rounded-lg shadow-lg"
  src="https://player.vimeo.com/video/888869651"
  frameborder="0"
  allow="autoplay; fullscreen; picture-in-picture"
  allowfullscreen
></iframe>

</div>

<!--
正直に、まだ unknown な部分も共有する。
symbolication: collector 標準では未対応。honeycomb の collector-symbolicator が参考。
session replay: どう実現するかは不明瞭。ここは今後の見どころ。
-->

---
layout: center
transition: 'view-transition'
---


<div class="flex flex-col text-2xl text-center">

<div class="mb-4">OpenTelemetry は</div>

<div>フロントエンドに広がりつつあります</div>

</div>

<div class="text-lg opacity-70 mt-8">

気になったら [opentelemetry-browser](https://github.com/open-telemetry/opentelemetry-browser) を覗いてみてください

</div>

<!--
最後にコアメッセージを再提示。
締めは気楽に。「フロントの動向、面白くなってきたので追ってみてください」で終える。
-->
