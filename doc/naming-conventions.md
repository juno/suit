# SUIT CSS命名規則

SUIT CSSは_構造化されたクラス名_と_意味のあるハイフン_（単にハイフンを単語区切りとして使うのではないということ）に依っている。
CSSをDOMに適用する際に存在する制限（スタイルのカプセル化の欠如）への対処およびクラス間の関係を扱いやすくすることを支援する。

構造に関する主要なことは**[ユーティリティ](utilities.md)**と**[コンポーネント](components.md)**を参照。

**目次**

* [u-utilityName](#u-utilityName)
* [ComponentName](#ComponentName)
* [ComponentName--modifierName](#ComponentName--modifierName)
* [ComponentName-descendantName](#ComponentName-descendantName)
* [ComponentName.is-stateOfComponent](#is-stateOfComponent)

## [ユーティリティ](utilities.md)

低レベル（下位）の構造およびポジションに関するもの。ユーティリティはコンポーネント内のどんな要素に対しても直接適用することができる。

構文: `u-[sm|md|lg-]<utilityName>`

<a name="u-utilityName"></a>
### u-utilityName

ユーティリティにはキャメルケースの名前を使わなくてはならない。以下の例は、コンポーネント内に簡単な構造を作るのにユーティリティをどのように使えるかを示したもの。

```html
<div class="u-cf">
  <a class="u-floatLeft" href="{{url}}">
    <img class="u-block" src="{{src}}" alt="">
  </a>
  <p class="u-sizeFill u-textBreak">
    …
  </p>
</div>
```

### レスポンシブユーティリティ

レスポンシブな派生系がある一部のユーティリティは、スモール、ミディアム、ラージの各メディアクエリブレークポイントに対応する `u-sm-<name>`、`u-md-<name>`、`u-lg-<name>` というパターンを持っている。


## [コンポーネント](components.md)

コンポーネント固有のスタイリングのためのCSS。

構文: `[<namespace>-]<ComponentName>[--modifierName|-descendentName]`

この構文には、HTMLとCSSを読み書きする上でいくつかの利点がある:

* コンポーネントのルート(root)、子孫となる要素、修飾に対するクラスを判別しやすくなる
* セレクタの詳細度を低く保つことができる
* 装飾のためのセマンティクスを文書のセマンティクスから分離できる

### namespace - 名前空間 (オプション)

必要に応じてコンポーネントには名前空間のプレフィックスを付けることができる。
例えば、すべての自分のコンポーネントに名前空間のプレフィックスを付けておくことで、カスタムコンポーネントとライブラリが衝突する可能性を排除することができる。

```css
.twt-Button { /* … */ }
.twt-Tabs { /* … */ }
```

これによって、HTMLを読んだ時にどのコンポーネントが自分のライブラリのものかが明確になる。

<a name="ComponentName"></a>
### ComponentName - コンポーネント名

コンポーネントの名前はパスカルケースで記述しなくてはならない。
HTML/CSSにおいてパスカルケースを使うのはコンポーネントのみとする。

```css
.MyComponent { /* … */ }
```

```html
<article class="MyComponent">
  …
</article>
```

<a name="ComponentName--modifierName"></a>
### ComponentName--modifierName - コンポーネント名--モディファイア名

コンポーネントモディファイアとは、基本となるコンポーネントの装飾を何らかの形で変更するクラスである（例：コンポーネントの特定の形態を表すため）。
モディファイア名はキャメルケースで、かつコンポーネント名とは2つのハイフンで分けられていなくてはならない。
このクラスは、基本となるコンポーネントのクラスに_加えて_HTMLに記述しなければならない。

```css
/* Core button */
.Button { /* … */ }
/* Default button style */
.Button--default { /* … */ }
```

```html
<button class="Button Button--default" type="button">…</button>
```

<a name="ComponentName-descendentName"></a>
### ComponentName-descendentName - コンポーネント名-子孫名

コンポーネントの子孫とはコンポーネントの子孫ノードに付けられるクラスであり、個々のコンポーネントの代わりに子孫に対して直接装飾を行うためのものである。
子孫名はキャメルケースで記述しなければならない。

```html
<article class="Tweet">
  <header class="Tweet-header">
    <img class="Tweet-avatar" src="{{src}}" alt="{{alt}}">
    …
  </header>
  <div class="Tweet-bodyText">
    …
  </div>
</article>
```

<a name="is-stateOfComponent"></a>
### ComponentName.is-stateOfComponent - コンポーネント名.is-状態

コンポーネントの状態に対する変更をあらわすには`is-stateName`を使う。
状態名はキャメルケースでなければならない。
**これらのクラスには直接スタイリングは行わない。常に他のクラスと連接させて共に使うこと。**

同じ状態名を復数のコンテキストで使うことができる。ただし、その状態を持つすべてのコンポーネントでは状態毎の自身のスタイルを（そのコンポーネント内に閉じた形で）定義していなければならない。

```css
.Tweet { /* … */ }
.Tweet.is-expanded { /* … */ }
```

```html
<article class="Tweet is-expanded">
  …
</article>
```
