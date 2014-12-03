# SUIT CSSデザイン原則

SUIT CSSは、コンポーネントベース開発におけるCSSオーサリングの体験を改善することにフォーカスした方法論である。

コンポーネントベースのシステムは、独立したユニットをゆるい繋がりによって組み合わせ、うまく定義された合成オブジェクトに仕上げることを可能とする。
コンポーネントはカプセル化されるが、インターフェースやイベントによって相互運用することはできる。

1. [モジュラリティ](#modularity)
2. [凝集性](#cohesion)
3. [合成と設定](#composition)
4. [疎結合](#coupling)
5. [ソフトなカプセル化](#encapsulation)
6. [ドキュメンテーション](#documentation)

<a name="modularity"></a>
## モジュラリティ

それぞれのコンポーネントは、1つの目的とそのためのUIに必要なすべてのものを含んでいなければならない。
コンポーネントは、HTML、CSS、JavaScriptおよびその外側のコンテキストを意識することのないアセットを含むことができる。

<a name="cohesion"></a>
## 凝集性

コンポーネントが定義する機能と見た目は意味的に関連していなければならない。
コンポーネントは互いに直接影響し合ってはならない。

<a name="composition"></a>
## 合成と設定

合成のしやすさ（Composability）とは、コンポーネントの相互関係に関わることである。
合成可能なシステムとは、必要に応じて様々に組み合わせできるコンポーネントから成る。

設定（(Configuration）は、コンポーネントが提供するインターフェースを通じて行われる。

<a name="coupling"></a>
## 疎結合

コンポーネントは、自身が依存するものの見た目や振る舞いを直接変更してはならない。
コンポーネント間のやり取りの結果を疎結合にするために、インターフェースとイベントを用いること。

コンポーネントを跨ぐコードの再利用をやり過ぎると、その結合を強めてしまう。
表面的に似たコードの繰り返しを無くすことよりも、分離することのほうがより重要である。

<a name="encapsulation"></a>
## ソフトなカプセル化

コンポーネントの実装が他のコンポーネントに開示されてはならない。
例えば、コンポーネントが他のコンポーネントのHTMLツリー内にスタイルを影響させてはならないし、コンポーネントのHTMLが他のコンポーネントのHTML内に直接含まれたりしてもならない。

巨大かつ適用可能な（Adaptive）なアプリケーションにとって、複雑性は重要な問題である。
コンポーネントの絡み合いを減らしていくほど、システムについて理解することが容易になる。

<a name="documentation"></a>
## ドキュメンテーション

コンポーネントがどのように使われるべきか、実装において個々のCSSプロパティがなぜ必要なのかといったことがちゃんと解説された、小さく独立したコンポーネントを書くこと。
CSS自身がドキュメントになるとは考えないこと。

## 関連情報

* [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
* [Cohesion](http://en.wikipedia.org/wiki/Cohesion_(computer_science))
* [Component-based software engineering](http://en.wikipedia.org/wiki/Component-based_software_engineering)
* [Encapsulation](http://en.wikipedia.org/wiki/Encapsulation_(object-oriented_programming))
* [Functional programming](http://en.wikipedia.org/wiki/Functional_programming)
* [Single responsibility principle](http://en.wikipedia.org/wiki/Single_responsibility_principle)
* [SOLID CSS](http://blog.millermedeiros.com/solid-css/)
