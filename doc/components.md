# SUIT CSSコンポーネント

SUIT CSSは、再利用可能で合成可能なコンポーネントのスタイリングのために設計されている。
コンポーネントをアプリケーションの構成要素とする試みの利点は明白だ。

コンポーネントとして、固有のセマンティクスとスタイリング、それに振るまいを持ったカスタムエレメントを考えてみよう。
例えば、このような`Photo`コンポーネントだ:

```html
<Photo src="photo.jpg" size="large" crop="circle">
  A photo of <a href="/barackobama">Barack Obama</a> in the Whitehouse.
</Photo>
```

これは以下のようなHTMLを生成するだろう:

```html
<article class="Photo Photo--sizeLarge">
  <a class="Photo-crop Photo-crop--circle" href="photo.jpg">
    <span class="Photo-icon">
      <span class="Icon Icon--zoom"></span>
    </span>
    <img class="Photo-img u-block" src="photo.jpg" alt="">
  </a>
  <div class="Photo-caption u-textBreak">
    A photo of <a href="/barackobama">Barack Obama</a> in the Whitehouse.
  </div>
</article>
```

SUIT CSSは、`Photo`コンポーネントの実装内で使われるCSSを部分的に分離することを支援する。
それによって、コンポーネント間でのスタイリングの絡み合いを減らしスタイリングを簡潔なものにし、コンポーネントの外にスタイルが漏れることも防ぐ。

(SUIT CSSの[命名規則](naming-conventions.md)も参照)

## コンポーネントのスコープ

コンポーネントのコアクラス名（例えば`ComponentName`）は、そのコンポーネントでのみ使われる名前空間を表す。
これは、ビルドプロセスで[suitcss-preprocessor](https://github.com/suitcss/preprocessor)や[rework-suit-conformance](https://github.com/suitcss/rework-suit-conformance)といったツールを使うことで強制することができる。

**コンポーネントファイル内のすべてのセレクタはコンポーネントの名前空間で始まらなければならない**。
例えば、`MyComponent`という名前のコンポーネントは、以下のようにすべてのセレクタが`MyComponent`という文字列で始まるCSSを持つことになる。

```css
/** @define MyComponent */

.MyComponent { /* ... */ }
.MyComponent--large { /* ... */ }
.MyComponent-title { /* ... */ }
.MyComponent-image { /* ... */ }
.MyComponent-text { /* ... */ }
.MyComponent-time { /* ... */ }
```

それぞれのクラスは、HTML内でそれぞれの要素にスタイルを適用するためのフックとなる。

```html
<article class="MyComponent u-cf">
  <h1 class="MyComponent-title">{{title}}</h1>
  <img class="MyComponent-image" src="{{src}}" alt="">
  <p class="MyComponent-text">
    <span class="MyComponent-time">{{time}}</span>
    {{text}}
  </p>
</div>
```

クラスと同様に、変数も変数名にコンポーネント名を含むことでスコープをそのコンポーネント内に限定しなければならない:

```css
/** @define MyComponent */

:root {
  --MyComponent-border-width: 5px;
}

.MyComponent {
  border-width: var(--MyComponent-border-width);
  /* ... */
}
```

これによって、デフォルトを上書きするテーマが可能となる。

コードがDRYでなくなるとしても、コンポーネントの結合や絡み合いのほうを防ぐこと。
分離することは回避可能な複雑さの予防になり、堅牢な再利用のためにも重要である。

## 1つのパターン、1つのコンポーネント

**各コンポーネントはUIの一部分だけを実装すべきである**。多くのことをやろうとしないこと。

**各コンポーネントは専用のCSSファイルを持つべきである**。コンポーネントに関するファイルはそのコンポーネント用のディレクトリに集められているのが理想である。

## 実装詳細のドキュメント化

コンポーネントは、その実装についてのドキュメントが無ければならない。コンポーネントのCSSコメントは以下の質問について回答するべきである:

* どのような表示（Presentation）が意図されているか？
* どんなモディファイアと状態があるか？
* 詳細だったり曖昧だったりするプロパティ値はどのような理由からか？
* どんな制限があるか？

## 祖先のコンテキストに対する順応

**ほとんどのコンポーネントは自身の幅やマージン、位置を指定すべきではない。**
コンポーネントをfull-widthまたはインラインであるように作成することで、祖先のコンテキストにうまく順応させることができるようになる。

## スタイリングの依存

**コンポーネントは自身が依存する実装について知るべきではない**。
何に依存するのかということは、それらのインターフェースを通じて設定するべきである。

コンポーネントの大きさやマージン、位置、継承可能なスタイルは_非直接的_に行うことができる。コンポーネントのルート要素にクラスを追加するか、それを他の要素でラップすること。

```css
/* 引用（Excerpt） */

.Excerpt {
  /* ... */
}

/* ネストしたコンポーネントに追加する */

.Excerpt-button {
  display: inline-block;
  margin-top: 20px;
}

/* ネストしたコンポーネントをラップする */

.Excerpt-wrapButton {
  display: inline-block;
  margin-top: 20px;
}
```

```html
<article class="Excerpt u-cf">
  {{! 実装に関するその他の詳細 }}

  <read-button class="Excerpt-button">続きを読む</read-button>

  <div class="Excerpt-wrapButton">
    <read-button>続きを読む</read-button>
  </div>
</article>
```
