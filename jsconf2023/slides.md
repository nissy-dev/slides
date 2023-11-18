---
layout: section
fonts:
  # basically the text
  sans: 'M PLUS'
  # for code blocks, inline code, etc.
  mono: 'Monaco'
title: Deep dive into Biome
canvasWidth: 800
highlighter: 'shiki'
lineNumber: true
transition: 'view-transition'
---

# Deep dive into Biome

---
transition: 'view-transition'
---

# Who am I？

<Transform :scale="1.4">

- Daiki Nishikawa (GitHub: @nissy-dev X: @nissy_dev)
- Frontend engineer at Cybozu, Inc.
  - Replace frontend using Next.js App Router
- I like coding rust 🦀 (also like eating 🦀)
- Core contributor of Biome

</Transform>

<!--

実は同じチームの麦島が、午後に Next.js の App Router に関する発表をするので、
もし気になる人はみてもらえたらと思います。

フロントエンドエンジニアのかたわら、TyeScript から型に興味を持ち、
最近は Rust を書くことが好きです。そして、今日取り上げる Biome のコアコントリビュータをしています。

-->

---
transition: 'view-transition'
---

# Today's talk is ...

<Transform :scale="1.4">

- Know what is Biome
- Understand the difference between Biome and other tools
- Feel close to Rust code showing linter code

</Transform>

---
layout: center
title: Biome logo
transition: 'view-transition'
---

<img src="/biome_logo_slogan.png" />

<!--

とういうことで最近の Biome の紹介からまずは始めてこうと思います！
ちなみに、これ今後 biome で使っていくことにした、新しいロゴになります。

まだ、そのうち公式な発表を出す予定なのですが、
せっかくの JSConf ということでちょっと先出ししてみました。

-->

---

# What is Biome?

<Transform :scale="1.4">

- Provide toolchains for web development
  - Currently, focus on linter and formatter
  - Language support: JS, TS, JSON and JSONC
- Biome is the fork of Rome by community
  - The members of Rome are laid off
  - Rome isn't maintained anymore

</Transform>

---
transition: 'view-transition'
---

# Latest update 

<Transform :scale="1.4">

- <logos-intellij-idea /> Release [Intellij plugin](https://plugins.jetbrains.com/plugin/22761-biome)
- 🆕 Add new 15 lint rules
- 🏛 Establish [project governance](https://github.com/biomejs/biome/blob/main/GOVERNANCE.md)
- 🚀 Start working CSS parser

</Transform>

<!--

1つ目は intellij plugin のリリースです。
多くの要望が来ていてなかなかコアちーむが着手できていなかったのですが、
新しいコントリビューターがかなり実装してくれたことでリリースできました。


２つ目は lint ルールの追加です。
引き続き 15個の新しい lint ルールを実装して、linter の安定化に努めています。

３つ目と４つ目は次のスライドで説明していきます。

-->

---
layout: image-right
image: /governance.png
transition: 'view-transition'
---

# Governance

- Welcome to more contributors
  - [Join three new maintainers](https://github.com/biomejs/biome/blob/main/CONTRIBUTING.md#current-members)
- Collect funds from community
  - [Open Collective](https://opencollective.com/biome)
  - [GitHub Sponsor](https://github.com/sponsors/biomejs)
- Start thinking about roadmap

<!--

大きく２つの目的があった

- コントリビュータを増やす
- プロジェクトとして寄付を募集しやすくする

-->

---
layout: image-right
image: /css_support.png
transition: 'view-transition'
---

# CSS Support

- [Working CSS parser](https://github.com/biomejs/biome/issues/268)
- Formatter and linter will come next year

<!--

10月くらいから始めていて、今は at-rule 以外の基本的なパーサーの実装を進めている。
このまま進めていくと、年内は parser の実装をしていて、来年以降に formatter や linter の実装が始めると思います。

-->

---
layout: section
transition: 'view-transition'
---

# Who use Biome...?

---
layout: center
title: npm trends
transition: view-transition
---

<img src="/npm_trends.png" />

<!--
まずは、npm の weekly ダウンロードの数字を紹介します。

青色が biome 
緑色が rome
オレンジが astro 

weekly で 6万ダウンロードを超えたくらいとなっています。

もともと rome の頃は、Astro と同じくらい使われていました。
-->

---
layout: image-left
image: /vercel.png
transition: 'view-transition'
---

# A. Vercel

- [Ant Design](https://github.com/ant-design/ant-design)
- [Unleash](https://github.com/Unleash/unleash)
- [Tamagui](https://github.com/tamagui/tamagui)
- ... and you?

<!--

v0: ユーザーが入力したテキストに基づいてWebページのUIを自動生成してくれるサービスです

Ant design: Alibabaが開発したReact の UI ライブラリ

Unleash: フィーチャーフラグを管理するための機能を提供しているプロジェクト

Tamagui: React と React Native の両方に対応したUIライブラリ

スライドに書かれていないところだと、つい最近では

- Node.js に biome を formatter として利用する PR 
- つい一昨日、時雨堂さんも biome を使ってくれて、スポンサーにもなってくれました

会場にいるみなさんの中で、使っているよーという方いますか？

-->

---
layout: section
transition: 'view-transition'
---

# Why use Biome?

<!--

先ほどのアンケートの通り、多くの人は既存の prettier / eslint などを使っていて、
ある程度は満足しているのかなと思います。

じゃあ、なんで先ほど紹介したプロジェクトは Biome を使っているのかというところなのですが、
Biome の特徴についてみていきます。

-->

---

# Advantages

<Transform :scale="1.4">

- 🚀 Fast: Built with Rust
- ✅ Simple: Zero configuration to get started
- 🔋 Batteries Included: First class support for TS and JSX
- ... is this all?

</Transform>


<!--

速さ = TypeScript のようなリポジトリでも数百msでフォーマットできます。

２つ目と３つ目は、特に JS あんまり普段触らないなーという人にとっては嬉しいポイントなのかなと思います。

これらのポイントがよく biome については取り上げられると思うのですが、
今日もう１つ紹介したいポイントがあります。

-->

---
transition: 'view-transition'
---

# Error resilience!

<div class="flex flex-col justify-center">
  <video controls>
    <source src="/eslint-rome-comparison.mp4" type="video/mp4" preload="metadata" poster="/video_poster.png"/>
  </video>
  <div class="text-center">Biome can lint files with syntax errors</div>
</div>

<!--

error resilience は、構文エラーがあっても、パース処理をできる限り止めないで構文解析を続けられる特徴になります。

-->

---
layout: section
title: Let's look into the internals of parser!
transition: 'view-transition'
---

<div class="flex flex-col font-bold">
  <div class="text-4xl mb-2xl">Let's look into the internals of parser!</div>
  <div class="text-gray text-xl">From the viewpoint of error resilience</div>
</div>

<!--

とういうことで、今日のはこの違いに着目しながら、Biome のパーサーの処理についてみていこうと思います。

-->

---
transition: 'view-transition'
---

# General parser

<div class="flex mt-4xl justify-center">
  <img src="/general_parser.png" class="h-70" />
</div>


<!--

invalid な構文の場合、パーサーは途中で構文エラーを報告し、AST を構築しないことがある。
AST 構築されないと、先ほどの動画のように lint のエラーなどは報告できない。

-->


---
transition: view-transition
---

# Biome parser

- Don't convert code to AST directly
- Return AST even if the syntax is invalid

<div class="flex mt-xl justify-center">
  <img src="/biome_parser.png" class="h-70" />
</div>

<!--
２つの特徴がある

- 直接的に AST を構築せず、GreenTree/RedTree と呼ばれる構文木を生成する
- Red Tree をもとに AST は生成する
- このとき invalid な文法に対しても必ず AST を返すようにします

ということで、それぞれについて詳しくみていきます。
-->

---
layout: two-cols
transition: 'view-transition'
---

## Green Tree・Red Tree

<div class="mt-2xl">

- Green Tree
  - Immutable tree
  - Node has syntax kind and text length
  - Include all information about code
- Red Tree
  - Mutable tree
  - Computed from Green Tree
  - Node has APIs to manipulate trees

</div>

::right::

Example of Green Tree (`const a = 1;`)

```plaintext
1: JS_DIRECTIVE_LIST@0..0
2: JS_MODULE_ITEM_LIST@0..12
  0: JS_VARIABLE_STATEMENT@0..12
    0: JS_VARIABLE_DECLARATION@0..11
      0: (empty)
      1: CONST_KW@0..6 "const" [] [Whitespace(" ")]
      2: JS_VARIABLE_DECLARATOR_LIST@6..11
        0: JS_VARIABLE_DECLARATOR@6..11
          0: JS_IDENTIFIER_BINDING@6..8
            0: IDENT@6..8 "a" [] [Whitespace(" ")]
          1: (empty)
          2: JS_INITIALIZER_CLAUSE@8..11
            0: EQ@8..10 "=" [] [Whitespace(" ")]
            1: JS_NUMBER_LITERAL_EXPRESSION@10..11
              0: JS_NUMBER_LITERAL@10..11 "1" [] []
    1: SEMICOLON@11..12 ";" [] []
3: EOF@12..12 "" [] []
```


<!--

- Green Tree は初めに生成される構文木
- スペースやコメントなども含む具象構文木
- これを直接編集できない

-->

---
layout: two-cols
transition: 'view-transition'
---

## Cast Red Tree to AST

<div class="mt-2xl">

- Traverse Red Tree and cast to AST
- [AST is defined by DSL](https://github.com/biomejs/biome/blob/main/xtask/codegen/js.ungram)
  - incompatible with estree

</div>

::right::

Example of AST (`const a = 1;`)

```text
JsVariableStatement {
  declaration: JsVariableDeclaration {
    await_token: missing (optional),
    kind: CONST_KW@0..6 "const" [] [Whitespace(" ")],
    declarators: JsVariableDeclaratorList [
      JsVariableDeclarator {
        id: JsIdentifierBinding {
          name_token: IDENT@6..8 "a" [] [Whitespace(" ")],
        },
        variable_annotation: missing (optional),
        initializer: JsInitializerClause {
          eq_token: EQ@8..10 "=" [] [Whitespace(" ")],
          expression: JsNumberLiteralExpression {
            value_token: JS_NUMBER_LITERAL@10..11 "1" [] [],
          },
        },
      },
    ]
  }
}
```

<!--

- Red Tree を走査して、syntax kind の情報をもとに AST を作成しています。
- Biome の AST は DSL で定義しており、estree とは互換のないものになっています。

-->

---
layout: two-cols
transition: view-transition
---

## Handling invalid syntax

<div class="mt-2xl">

- Allow missing fields
- Use bogus node
  - A custom node for invalid syntax

</div>

::right::

Example of AST (`function}`)

```text {all|6-10|12-16}
items: JsModuleItemList [
  JsFunctionDeclaration {
    async_token: missing (optional),
    function_token: FUNCTION_KW@0..8 "function" [] [],
    star_token: missing (optional),
    id: missing (required),
    type_parameters: missing (optional),
    parameters: missing (required),
    return_type_annotation: missing (optional),
    body: missing (required),
  },
  JsBogusStatement {
    items: [
      R_CURLY@8..9 "}" [] [],
    ],
  },
],
```

<!--
Biome は ASTを生成する際に、 invalid な文法を考慮しているのが特徴です。どう考慮しているのかというと、、、
-->

---
transition: 'view-transition'
---

# Red-Green Tree (lossless syntax tree)

- Great error resilience
- Fully recoverable
- Created by C# compiler team
  - rust-analyzer and swift also use
- Biome use the forked Rowan
  - Rowan: A library for red-green tree used in rust-analyzer

<!--

Fully recoverable: 構文木からもとのソースコードを完全に復元できる特徴があります。

ASTベースだと、コメントやスペースなどの情報を省くため、一般的に元のコードを再現するのは難しいです。

-->


---
layout: section
title: Our parser is based on Red-Green Tree!
transition: view-transition
---

<div class="flex flex-col font-bold">
  <div class="text-4xl mb-2xl">Our parser is based on Red-Green Tree!</div>
  <div class="text-xl text-gray">This is why everything is from scratch</div>
  <div class="text-xl text-gray">Existing AST-based parser tools can't be used</div>
</div>

<!--
これが、Biomeがフルスクラッチでパーサーを実装している理由です。既存の例えば ligthing css や swcのようなパーサーを使いたくても使えないという状況です。
-->

---
layout: section
title: Next, let's look into our linter code!
transition: 'view-transition'
---

<div class="flex flex-col font-bold">
  <div class="text-4xl mb-2xl">Next, let's look into our linter code!</div>
  <div class="text-xl text-gray">According to the difference of our parser</div>
  <div class="text-l text-gray">our linter is also different...?</div>
</div>

---
transition: 'view-transition'
---

# Example: enforce-foo-bar

- All const variables named "foo" are assigned the string literal "bar"
- This is covered in [ESLint's custom rule tutorial](https://eslint.org/docs/latest/extend/custom-rule-tutorial)

<div class="mt-2xl">

```js
// show error!
const foo = "foo123";
↓ 
// expected
const foo = "bar";
```

</div>

---
transition: 'view-transition'
---

# ESLint implementation

```js
create(context) {
  return {
    // Performs action in the function on every variable declarator
    VariableDeclarator(node) {
      // Check if a `const` variable declaration
      if (node.parent.kind === "const") {
        // Check if variable name is `foo`
        if (node.id.type === "Identifier" && node.id.name === "foo") {
          // Check if value of variable is "bar"
          if (node.init && node.init.type === "Literal" && node.init.value !== "bar") {
            // report error
            context.report({ ... });
          }
        }
      }
    }
  }
}
```

---
transition: 'view-transition'
---

# Biome implementation

```rust {all|2-3|6-17|all}
impl Rule for EnforceFooBar {
    // define the AST node which visitor enter
    type Query = Ast<JsVariableDeclarator>;
    type State = ();

    // The main logic for linter
    // - return Some(()) when to report error
    // - return None **when not** to report error
    fn run(ctx: &RuleContext<Self>) -> Option<Self::State> {
      let node = ctx.query();
      let parent = node
          .parent::<JsVariableDeclaratorList>()?
          .parent::<JsVariableDeclaration>()?;

      ...
    }
}
```

---
transition: 'view-transition'
---

# Biome implementation

```rust {all|3-6|7-14|all}
fn run(ctx: &RuleContext<Self>) -> Option<Self::State> {
    ...
    // check if a `const` variable declaration
    if parent.is_const() {
        // Check if variable name is `foo`
        if node.id().ok()?.text() == "foo" {
            // Check if value of variable is "bar"
            let init_exp = node.initializer()?.expression().ok()?;
            let literal_exp = init_exp.as_any_js_literal_expression()?;
            if literal_exp.as_static_value()?.text() != "bar" {
                // Report error to Biome
                // The details of error message is implemented by "diagnostic" method
                return Some(());
            }
        }
    }
    None
}
```

---
transition: 'view-transition'
---

# Comparison

<Transform :scale="0.8">

```rust
impl Rule for EnforceFooBar {
    type Query = Ast<JsVariableDeclarator>;
    type State = ();
    
    fn run(ctx: &RuleContext<Self>) -> Option<Self::State> {
      let node = ctx.query();
      let parent = node
          .parent::<JsVariableDeclaratorList>()?
          .parent::<JsVariableDeclaration>()?;

      if parent.is_const() {
          if node.id().ok()?.text() == "foo" {
              let init_exp = node.initializer()?.expression().ok()?;
              let literal_exp = init_exp.as_any_js_literal_expression()?;
              if literal_exp.as_static_value()?.text() != "bar" {
                  return Some(());
              }
          }
      }
      None
    }
}
```

</Transform>

<img src="/eslint_impl.png" class="absolute top-3xl right-xl w-2/5" />

<logos-javascript class="absolute top-46 right-5 w-10 h-10" />

<logos-rust class="absolute bottom-8 right-50 w-10 h-10 fill-[#B7410E]" />

---
transition: 'view-transition'
layout: section
---

<div class="flex flex-col font-bold">
  <div class="text-4xl mb-2xl">The code is similar than I expected</div>
  <div class="text-xl text-gray">It is not necessary to know Rust and Biome in depth from the beginning</div>
</div>

---
transition: 'view-transition'
layout: section
---

<div class="flex flex-col font-bold">
  <div class="text-4xl mb-2xl">Did you feel more familiar with Biome?</div>
  <div class="text-xl text-gray">Welcome to your contribution!</div>
  <div class="text-xl text-gray">Learning new languages is fun!</div>
</div>

---
transition: 'view-transition'
---

# References

- [biomejs.dev](https://biomejs.dev/)
- [Announcing Biome](https://biomejs.dev/blog/annoucing-biome)
- [Announcing Rome v10](https://web.archive.org/web/20230328125908/https://rome.tools/blog/2022/11/08/rome-10/)
- [Rowan](https://github.com/rust-analyzer/rowan)
- [Syntax in rust-analyzer](https://github.com/rust-lang/rust-analyzer/blob/master/docs/dev/syntax.md)
- [Rome will be written in Rust 🦀](https://web.archive.org/web/20230401084626/https://rome.tools/blog/2021/09/21/rome-will-be-rewritten-in-rust/)
- [Rust Dublin October 2023 - Biome](https://www.youtube.com/watch?v=stxiUYmHn0s)
