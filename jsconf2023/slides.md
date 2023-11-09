---
layout: section
fonts:
  # basically the text
  sans: 'M PLUS'
  # for code blocks, inline code, etc.
  mono: 'Fira Code'
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

- Daiki Nishikawa (nissy)
- Frontend engineer at Cybozu Inc.
- I like coding rust 🦀 (also like eating 🦀)
- Core contributor of Biome

</Transform>

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

<img src="/biome_logo.png" />

---

# What is Biome?

<Transform :scale="1.4">

- Biome is the fork of Rome by community
  - The members of Rome are laid off
  - Rome isn't maintained anymore
- Provide toolchains for web development
  - Currently, focus on linter and formatter
  - Language support: JS, TS, JSON and JSONC

</Transform>

---
transition: 'view-transition'
---

# Latest update 

<Transform :scale="1.4">

- <logos-intellij-idea /> Release Intellij plugin
- 🆕 Add new 15 lint rules
- 🏛 Establish project governance
- 🚀 Start working CSS parser

</Transform>

<!--

Web Storm 使っている人がどれくらいいるのか聞いても良さそう

-->

---
layout: image-right
image: ./public/governance.png
transition: 'view-transition'
---

# Governance

- Welcome to more contributors
  - Join three new maintainers
- Collect funds from community
  - Open Collective
  - GitHub Sponsor
- Start thinking about roadmap

---
layout: image-right
image: ./public/css_support.png
transition: 'view-transition'
---

# CSS Support

- Working CSS parser
- Formatter and linter will come next year

---
layout: section
transition: 'view-transition'
---

# Who use Biome...?

---
layout: center
title: npm trends
transition: 'view-transition'
---

<img src="/npm_trend.png" />

<!--

画像は差し替える

-->

---
layout: image-left
image: ./public/vercel.png
transition: 'view-transition'
---

# A. Vercel

- Ant Design
- Unleash
- Tamagui
- ... and you?

<!--

この会場でも使っている人を聞いてみる

-->

---
layout: section
transition: 'view-transition'
---

# Why use Biome?

---

# Advantages

<Transform :scale="1.4">

- 🚀 Fast: Built with Rust
- ✅ Simple: Zero configuration to get started
- 🔋 Batteries Included: First class support for TS and JSX
- ... is this all?

</Transform>

---
transition: 'view-transition'
---

# Error resilience!

<div class="flex flex-col justify-center">
  <video controls>
    <source src="/public/eslint-rome-comparison.mp4" type="video/mp4" />
  </video>
</div>

Cited by [https://rome.tools/blog/2021/09/21/rome-will-be-rewritten-in-rust/](https://web.archive.org/web/20230328125908/https://rome.tools/blog/2022/11/08/rome-10/)

---
layout: section
title: Let's look into the internals of parser!
transition: 'view-transition'
---

<div class="flex flex-col gap-2xl font-bold">
  <div class="text-gray text-xl">From the viewpoint of error resilience</div>
  <div class="text-4xl">Let's look into the internals of parser!</div>
</div>

---
transition: 'view-transition'
---

# General parser

<div class="flex mt-4xl justify-center">
  <img src="/public/general_parser.png" class="h-70" />
</div>

---
transition: 'view-transition'
---

# Biome parser

- Don't convert code to AST directly
- Return AST even if the syntax is invalid

<div class="flex mt-xl justify-center">
  <img src="/public/biome_parser.png" class="h-70" />
</div>

---
layout: two-cols
transition: 'view-transition'
---

## Green Tree・Red Tree

<div class="mt-2xl">

- Green Tree
  - Immutable tree
  - Include all information about code
- Red Tree
  - Mutable tree
  - Computed from Green Tree
  - Expose APIs to manipulate trees

</div>

::right::

Example of Green Tree (`const = 1;`)

```text
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
```

---
layout: two-cols
transition: 'view-transition'
---

## Cast Red Tree to AST

<div class="mt-2xl">

- Traverse Red Tree and cast to AST
- AST is defined by DSL
  - incompatible with estree
- Bognus node
  - A custom node for broken syntax

</div>

::right::

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
    ],
  },
},
JsBogusStatement {
  items: [
    QUESTION@10..11 "?" [] [],
  ],
},
```

---
transition: 'view-transition'
---

# Red-Green Tree (lossless syntax tree)

<Transform :scale="1.4">

- Great error resilience
- Fully recoverable
- Created by C# compiler team
  - rust-analyzer and swift also use
- Biome use the forked Rowan
  - Rowan: A library for red-green tree used in rust-analyzer

</Transform>

---
layout: section
title: Let's look into the internals of parser!
transition: 'view-transition'
---

<div class="flex flex-col gap-2xl font-bold">
  <div class="text-4xl">Our parser is based on Red-Green Tree!</div>
  <div class="text-xl text-gray">This is why everything is from scratch</div>
  <div class="text-xl text-gray">Existing AST-based parser tools can't be used</div>
</div>

---
layout: section
transition: 'view-transition'
---

# How about linter?

## Let's look into our liner code!

---
layout: section
transition: 'view-transition'
---

# TODO


---
transition: 'view-transition'
---

# References
