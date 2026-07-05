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

ブラウザ向け SDK が動き出した 2026 年

</div>

<!--
こんにちは。今日は OpenTelemetry の話をします。
ただしサーバーサイドではなく、ブラウザ・フロントエンド側に絞ります。

OpenTelemetry はすでにバックエンドではよく使われていますが、最近はブラウザ向け SDK の開発も動き出しています。
今日はその背景と、いまどこまで進んでいるのかを10分で紹介します。
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
簡単に自己紹介します。
Daiki Nishikawa といいます。GitHub と X は nissy-dev / nissy_dev です。

Cybozu でソフトウェアエンジニアをしていて、フロントエンドの横断的な技術支援や、AI を使った脆弱性検出基盤の整備をしています。
普段からフロントエンドの監視や品質改善に関わることが多く、その流れで OpenTelemetry Browser の動きを追っています。
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
先に、この発表で一番伝えたいことを置いておきます。

OpenTelemetry は、もうサーバーサイドだけの話ではありません。
フロントエンド向けの仕様や SDK の実装も進んでいます。

まだ課題はありますが、将来的にはフロントエンドでもベンダー非依存で監視を実装できる選択肢が現実味を帯びてきています。
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
まず OpenTelemetry について、簡単に前提を揃えます。

OpenTelemetry は、トレース・メトリクス・ログといったテレメトリを扱うための共通仕様です。
特定の監視ベンダーの SDK や形式に強く依存しすぎないようにする、というのが大きな価値です。

今年5月には CNCF の Graduated Projects にもなっていて、クラウドネイティブの世界ではかなり重要な位置づけになっています。
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
ここで少し会場に聞いてみます。

まず、サーバーサイドで OpenTelemetry を使っている、または触ったことがある人はいますか？
次に、フロントエンドで使っている人はいますか？

おそらくサーバーサイドの方が多くて、フロントエンドはまだ少ないと思います。
この差が、今日話したいポイントです。
-->

---
transition: 'view-transition'
---

# フロントエンドでの現状

<div class="text-2xl mt-4">

- <logos-sentry /> や <logos-datadog /> などの SaaS の SDK の利用が主流
- フロントエンドの監視まで手が回ってないチームも多そう
- OpenTelemetry で "安定して" できるのはトレースの送信だけ
  - `@opentelemetry/sdk-trace-web` を利用して実装できる


</div>

<!--
フロントエンドの監視は、現状だと Sentry や Datadog のような SaaS の SDK を入れるケースが多いと思います。
これらは便利で、エラー監視や Session Replay なども含めて一通り揃っています。

一方で、OpenTelemetry で安定してできることはまだ限定的です。
たとえばトレースの送信は `@opentelemetry/sdk-trace-web` でできますが、フロントエンド監視全体を任せられる状態ではありません。
-->

---
transition: 'view-transition'
---

# OpenTelemetry での動き

<div class="flex flex-1 flex-col text-2xl mt-4">

- Client SDK and Instrumentation SIG として議論はされていた
  - SIG: Special Interest Group
  - 議事録[^2]を見る限り 2021年ごろから
- ブラウザだけではなくモバイル (Android/iOS) も含む議論
  - 議論の対象範囲が広く、共通設計に2年以上の時間がかかっていた

</div>

[^2]: https://docs.google.com/document/d/16Vsdh-DM72AfMg_FIt9yT9ExEWF4A_vRbQ3jRNBe09w/edit?tab=t.0#heading=h.n5vcc992gs6y

<!--
では OpenTelemetry 側でフロントエンドの話が最近急に出てきたのかというと、そうではありません。

Client SDK and Instrumentation SIG、つまりクライアント向け SDK と計測まわりのグループとして、2021年ごろから議論はありました。

ただし対象はブラウザだけではなく、Android や iOS も含んでいました。
そのため共通設計の対象が広く、ブラウザ固有の話を進めるには時間がかかっていたようです。
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
ここが今回の発表で一番大事な変化です。

昨年中頃から、ブラウザに関しては独立した SDK として開発を進める流れになりました。
ブラウザ固有の意思決定を早くし、開発を進めやすくするためです。

Grafana Labs や Elastic などのメンバーも参加していて、今年に入ってから実装もかなり活発になっています。
興味がある人は `open-telemetry/opentelemetry-browser` を見るのが早いです。
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
現在地としては、基本的なテレメトリ収集ツールはすでに実装されています。

ユーザー操作、Core Web Vitals、エラーなどを集めるためのものが、`@opentelemetry/browser-instrumentation` として使えるようになっています。

また、これまで opentelemetry-js や opentelemetry-js-contrib 側にあったブラウザ向けのツールも、今後はこちらのリポジトリに集約される予定です。
fetch、xml-http-request、document-load などがその対象です。
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
  - OpenTelemetry Collector では標準対応されていない
  - Loki などバックエンド側の対応にもばらつきがある

</div>

<!--
ここからは、実用に向けて自分が気になっている点を2つ紹介します。

1つ目は、minify されたエラーのスタックトレースを誰が復元するのか、という点です。
フロントエンドでは本番コードが minify されるので、そのままではスタックトレースが読みづらくなります。

SaaS ではソースマップをアップロードして、元のコードに対応づけるところまでやってくれることが多いです。
一方で OpenTelemetry の世界では、Collector が標準でやってくれるわけではなく、Loki などバックエンド側の対応にもばらつきがあります。

この責務をどこで持つのかは、まだ整理が必要そうです。
-->

---
transition: 'view-transition'
---

# 実用に向けて気になる点: Session Replay

<div class="flex justify-center mt-4">

<video class="w-full rounded-lg shadow-lg" src="https://docs.dd-static.net/images//getting_started/session_replay/preview.mp4" autoplay loop muted playsinline controls></video>

</div>

<!--
2つ目は Session Replay です。

Session Replay を知らない人もいると思うので、まず実物を見せます。
ユーザーがどこをクリックしたか、どんな画面遷移をしたかを、録画のように再現できる機能です。

エラーが起きた瞬間の前後の操作を見られるので、フロントエンドの調査ではかなり強力です。
ただし、これを OpenTelemetry の共通仕様としてどう扱うかはまだ難しい論点です。
-->

---
transition: 'view-transition'
---

# 実用に向けて気になる点: Session Replay

<div class="flex flex-1 flex-col text-2xl mt-4">

- Session Replay はどう共通仕様としてまとめるのか？
  - rrweb [^3]をベースに各ベンダーは作っていると思うが、それぞれの要件に合わせてカスタマイズはされていそう
  - issue は作成されているが、特にレスポンスはない[^4]

</div>

[^3]: https://github.com/rrweb-io/rrweb

[^4]: https://github.com/open-telemetry/opentelemetry-browser/issues/32

<!--
前のスライドで見せたような Session Replay を、OpenTelemetry としてどう共通仕様にするのかはまだ不明瞭です。

実装としては rrweb をベースにしているベンダーが多いと思います。
ただ、各社の UI やデータの見せ方に合わせて、かなりカスタマイズされているはずです。

OpenTelemetry Browser のリポジトリにも issue はありますが、今のところ大きな議論は進んでいないようです。
ここは今後の見どころだと思っています。
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
まとめです。

OpenTelemetry は、サーバーサイドだけではなくフロントエンドにも広がりつつあります。
ブラウザ向け SDK が独立して動き始め、実装も進んでいます。

一方で、エラーの復元や Session Replay のように、実用に向けてまだ整理が必要な領域もあります。

フロントエンドの監視をベンダー非依存で考える選択肢として、OpenTelemetry Browser はこれから面白くなっていくと思います。
気になったらぜひリポジトリを覗いてみてください。
-->
