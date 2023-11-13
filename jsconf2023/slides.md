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

- Daiki Nishikawa (nissy)
- Frontend engineer at Cybozu, Inc.
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

<!--

新しいロゴに差し替えられそうなら差し替える

-->

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

- <logos-intellij-idea /> Release [Intellij plugin](https://plugins.jetbrains.com/plugin/22761-biome)
- 🆕 Add new 15 lint rules
- 🏛 Establish [project governance](https://github.com/biomejs/biome/blob/main/GOVERNANCE.md)
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
  - [Join three new maintainers](https://github.com/biomejs/biome/blob/main/CONTRIBUTING.md#current-members)
- Collect funds from community
  - [Open Collective](https://opencollective.com/biome)
  - [GitHub Sponsor](https://github.com/sponsors/biomejs)
- Start thinking about roadmap

---
layout: image-right
image: ./public/css_support.png
transition: 'view-transition'
---

# CSS Support

- [Working CSS parser](https://github.com/biomejs/biome/issues/268)
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

- [Ant Design](https://github.com/ant-design/ant-design)
- [Unleash](https://github.com/Unleash/unleash)
- [Tamagui](https://github.com/tamagui/tamagui)
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
  <div class="text-center">Biome can lint files with syntax errors</div>
</div>

---
layout: section
title: Let's look into the internals of parser!
transition: 'view-transition'
---

<div class="flex flex-col font-bold">
  <div class="text-4xl mb-2xl">Let's look into the internals of parser!</div>
  <div class="text-gray text-xl">From the viewpoint of error resilience</div>
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

---
layout: two-cols
transition: 'view-transition'
---

## Cast Red Tree to AST

<div class="mt-2xl">

- Traverse Red Tree and cast to AST
- [AST is defined by DSL](https://github.com/biomejs/biome/blob/main/xtask/codegen/js.ungram)
  - incompatible with estree
- Bogus node
  - A custom node for broken syntax

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
title: Our parser is based on Red-Green Tree!
transition: 'view-transition'
---

<div class="flex flex-col font-bold">
  <div class="text-4xl mb-2xl">Our parser is based on Red-Green Tree!</div>
  <div class="text-xl text-gray">This is why everything is from scratch</div>
  <div class="text-xl text-gray">Existing AST-based parser tools can't be used</div>
</div>

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

# Biome implementation
---

```rust
impl Rule for EnforceFooBar {
    // define 
    type Query = Ast<JsVariableDeclarator>;

    type State = ();
    type Signals = Option<Self::State>;
    type Options = ();

    fn run(ctx: &RuleContext<Self>) -> Self::Signals {
        let node = ctx.query();
        let parent = node
            .parent::<JsVariableDeclaratorList>()?
            .parent::<JsVariableDeclaration>()?;

        // check if a `const` variable declaration
        if parent.is_const() {
            // Check if value of variable is "bar"
            if node.id().ok()?.text() == "foo" {
                // Check if value of variable is "bar"
                let init_exp = node.initializer()?.expression().ok()?;
                let literal_exp = init_exp.as_any_js_literal_expression()?;
                if literal_exp.as_static_value()?.text() != "bar" {
                    // Report diagnostic to Biome
                    // The details of diagnostic is implemented by "diagnostic" method
                    return Some(());
                }
            }
        }
        None
    }
}
```

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
