# HTML/CSSコードスタイル

## 目次

1. [原則](#general-principles)
2. [ホワイトスペース](#whitespace)
3. [HTML](#html)
  * [フォーマット](#html-format)
  * [属性の順序](#html-attrs)
  * [命名](#html-naming)
  * [実例](#html-example)
4. [CSS](#css)
  * [コメント](#css-comments)
  * [フォーマット](#css-format)
  * [実例](#css-example)


<a name="general-principles"></a>
## 1. 原則

> "Part of being a good steward to a successful project is realizing that
> writing code for yourself is a Bad Idea™. If thousands of people are using
> your code, then write your code for maximum clarity, not your personal
> preference of how to get clever within the spec." - Idan Gazit

* 早すぎるコードの最適化をしようとはせず、読みやすく理解しやすいように維持すること。
* CSSは、プロジェクト内の他のCSSと変わらないように見えるようにすること


<a name="whitespace"></a>
## 2. ホワイトスペース

* 読みやすさのためホワイトスペースを使う。
* インデントには2つのスペースを使う。
* セパレーターとして1行よりも多い空行を使わない。
* 行末およびファイル末尾のホワイトスペースはすべて除去する。


<a name="html"></a>
## 3. HTML

<a name="html-format"></a>
### 3.1. フォーマット

* タグと属性名には常に小文字を使う。
* 1つの行には1つのブロックレベル要素を書く。
* ネストした各ブロックレベル要素には1段階のインデントを行う。
* 値を持たない真偽値属性を使う（例: `checked="checked"`ではなく`checked`）。
* 属性値のクオートには常にダブルクオートを使う。
* スタイルシートの`link`および`syle`と`script`要素からは`type`属性を取り除く。
* 常に閉じタグを含める。

（1行の長さは常識的な上限を保つ。例: 80文字。）

例:

```html
<div class="Tweet">
  <a href="{{url}}">
    <img src="{{avatar}}" alt="">
  </a>
  <p>{{text}}</p>
  <button disabled>Reply</button>
</div>
```

#### 例外

復数の属性を持つ要素は、読みやすさの向上と差分の利便性のため属性を複数行に並べることができる。

例:

```html
<a class="{{class}}"
 data-action="{{action}}"
 data-id="{{id}}"
 href="{{url}}">
  <span>{{text}}</span>
</a>
```


<a name="html-attrs"></a>
### 3.2. HTML 属性の順序

HTML属性はアルファベット順に記述すべきである。

例:

```html
<a class="{{class}}" data-name="{{name}}" href="{{url}}" id="{{id}}">{{text}}</a>
```


<a name="html-naming"></a>
### 3.3. 命名

命名は難しいがとても重要である。
コードベースをメンテナンスしやすく保つにあたって重大な部分である。
コンポーネントをリネームすることを恐れないこと。

* HTMLクラス名は、明解でよく考えられた適切な名前にする。HTMLとCSSファイルのどちらでも通用する名前にすべきである。
* 省略形のクラス名を_機械的_に使うのは避ける。理解しづらくならないように。

「悪い」名前の例:

```html
<div class="cb s-scr"></div>
```

```css
.cb {
  background: #000;
}

.cb.s-scr {
  overflow: auto;
}
```

より良い名前の例:

```html
<div class="ColumnBody is-scrollable"></div>
```

```css
.ColumnBody {
    background: #000;
}

.ColumnBody.is-scrollable {
    overflow: auto;
}
```


<a name="html-example"></a>
### 3.4. HTML 実例

ルールに沿った例。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Document</title>
    <link rel="stylesheet" href="main.css">
    <script src="main.js"></script>
  </head>
  <body>
    <article class="Post" id="1234">
      <time class="Post-timestamp">{{date}}</time>
      <a data-analytics-action="{{action}}"
       data-analytics-category="{{category}}"
       data-id="1234"
       href="{{url}}">{{text}}</a>
      <ul>
        <li>
          <a href="{{url}}">{{text}}</a>
          <img src="{{src}}" alt="">
        </li>
        <li>
          <a href="{{url}}">{{text}}</a>
        </li>
      </ul>

      <a class="u-linkComplex" href="{{url}}">
        <span class="u-linkComplex-target">{{text}}</span>
        {{text}}
      </a>

      <input value="text" readonly>
    </article>
  </body>
</html>
```


<a name="css"></a>
## 4. CSS

<a name="css-comments"></a>
### 4.1. コメント

ちゃんとコメントされているコードはとても重要だ。
コンポーネントの詳細や働き、その制限、利用方法の説明に時間をかけること。
チームの人たちに、奇妙なコードや自明ではないコードの意図を推測させたりしてはならない。

コメントの書式は、シンプルかつ1つのコードベース内で一貫していること。

* コメントは対象となるものの前に新しい行を用意して記述する。
* 行の長さは常識的な上限を保つ。例: 80文字。
* CSSコードをセクションに分けるためにコメントを気前よく使う。
* "sentence case"コメントを使い、一貫したインデントを行う。
* 個別の宣言についての説明を参照させるには、数値を行末にコメントとして書く。

Tip: configure your editor to provide you with shortcuts to output agreed-upon
comment patterns.

例:

```css
/**
 * Short description using Doxygen-style comment format
 *
 * The first sentence of the long description starts here and continues on this
 * line for a while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 *
 * TODO: This is a todo statement that describes an atomic task to be completed
 *   at a later date. It wraps after 80 characters and following lines are
 *   indented by 2 spaces.
 *
 * @tag This is a tag named 'tag'
 *
 * 1. A helpful description of a declaration's purpose.
 * 2. Another declaration or collection of declarations can reference this
 *    comment with an inline comment corresponding to the lists number.
 */

/* Thematic section comment block
   ========================================================================== */

/* Basic comment */
```

<a name="css-format"></a>
### 4.2. フォーマット

The chosen code format ensures that code is: easy to read; easy to clearly
comment; minimizes the chance of accidentally introducing errors; and results
in useful diffs and blames.

* Use one discrete selector per line in multi-selector rulesets.
* Include a single space before the opening brace of a ruleset.
* Include one declaration per line in a declaration block.
* Use one level of indentation for each declaration.
* Include a single space after the colon of a declaration.
* Use lowercase and shorthand hex values, e.g., `#aaa`.
* Use single or double quotes consistently. Preference is for double quotes,
  e.g., `content: ""`.
* Quote attribute values in selectors, e.g., `input[type="checkbox"]`.
* _Where allowed_, avoid specifying units for zero-values, e.g., `margin: 0`.
* Include a space after each comma in comma-separated property or function
  values.
* Include a semi-colon at the end of the last declaration in a declaration
  block.
* Place the closing brace of a ruleset in the same column as the first
  character of the ruleset.
* Separate each ruleset by a blank line.

```css
.selector-1,
.selector-2,
.selector-3[type="text"] {
  background: #fff;
  background: linear-gradient(#fff, rgba(0, 0, 0, 0.8));
  box-sizing: border-box;
  color: #333;
  display: block;
  font-family: helvetica, arial, sans-serif;
}

.selector-a,
.selector-b {
  padding: 10px;
}
```

#### 宣言の順序

Use alphabetical ordering of declarations unless the cascade absolutely
requires otherwise.

```css
.selector {
  background: #000;
  border: 10px solid #333;
  box-sizing: border-box;
  color: #fff;
  display: inline-block;
  font-family: sans-serif;
  font-size: 16px;
  text-align: right;
  width: 100%;
}
```

#### 例外

Large blocks of single declarations can use a slightly different, single-line
format. In this case, a space should be included after the opening brace and
before the closing brace.

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

Long, comma-separated property values - such as collections of gradients or
shadows - can be arranged across multiple lines in an effort to improve
readability and produce more useful diffs.

```css
.selector {
  background-image:
    linear-gradient(#fff, #ccc),
    linear-gradient(#f3c, #4ec);
  box-shadow:
    1px 1px 1px #000,
    2px 2px 1px 1px #ccc inset;
}
```

<a name="example"></a>
### 4.3. 実例

ルールに沿った例。

```css
/** @define Grid; use strict */

/**
 * Column layout with horizontal scroll.
 *
 * This creates a single row of full-height, non-wrapping columns that can
 * be browsed horizontally within their parent.
 *
 * Example HTML:
 *
 * <div class="Grid">
 *   <div class="Grid-cell Grid-cell--3"></div>
 *   <div class="Grid-cell Grid-cell--3"></div>
 *   <div class="Grid-cell Grid-cell--3"></div>
 * </div>
 */

/**
 * Grid container
 *
 * Must only contain `.Grid-cell` children.
 *
 * 1. Remove inter-cell whitespace
 * 2. Prevent inline-block cells wrapping
 */

.Grid {
  font-size: 0; /* 1 */
  height: 100%;
  white-space: nowrap; /* 2 */
}

/**
 * Grid cells
 *
 * No explicit width by default. Extend with `.Grid-cell--n` classes.
 *
 * 1. Reset font-size inherited from `.Grid`
 * 2. Set the inter-cell spacing
 * 3. Reset white-space inherited from `.Grid`
 */

.Grid-cell {
  border: 2px solid #333;
  box-sizing: border-box;
  display: inline-block;
  font-size: 1rem; /* 1 */
  height: 100%;
  overflow: hidden;
  padding: 0 10px; /* 2 */
  position: relative;
  vertical-align: top;
  white-space: normal; /* 3 */
}

/* Cell states */

.Grid-cell.is-animating {
  background-color: #fffdec;
}

/* Cell dimension modifiers
   ========================================================================== */

.Grid-cell--1 { width: 10%; }
.Grid-cell--2 { width: 20%; }
.Grid-cell--3 { width: 30%; }
.Grid-cell--4 { width: 40%; }
.Grid-cell--5 { width: 50%; }

/* Cell modifiers
   ========================================================================== */

.Grid-cell--detail,
.Grid-cell--important {
  border-width: 4px;
}
```


[github.com/necolas/idiomatic-html](https://github.com/necolas/idiomatic-html)
と
[github.com/necolas/idiomatic-css](https://github.com/necolas/idiomatic-css).
を元に作成。

