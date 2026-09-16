# Sample A / Step 2 — 高度なレイアウト

## このステップのゴール

Step 1 のコードに、モダンなレイアウト技法 4 つを導入する。
HTML は引き続き一切変更しない（CSS だけでここまでできることを体感する）。

## やること

1. **スティッキーヘッダー**: `.site-header` に [`position`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Properties/position)`: sticky` + `top: 0` + `z-index`
   - スクロールしてもヘッダーが画面上部に張り付く
2. **RAM パターン**: `.post-list` の列指定を
   [`grid-template-columns`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Properties/grid-template-columns)`: repeat(auto-fit, minmax(280px, 1fr))` に置き換える
   - **R**epeat + **A**uto-fit + **M**inmax。「280px 以上を確保できるだけ列を作り、無理なら折り返す」
   - Step 1 まで残っていた `.post-list` のメディアクエリ 2 つがこの 1 行で不要になる
3. **[サブグリッド](https://developer.mozilla.org/ja/docs/Web/CSS/Guides/Grid_layout/Subgrid)**: カードの内部（画像・タイトル・著者情報・要約・ボタン）を
   親グリッドの行定義に参加させ、**横に並んだカード同士で各行の高さを揃える**
   - `.post` を `grid-row: span 5` + `grid-template-rows: subgrid` に
   - `.post-body` も `span 4` + `subgrid` に（入れ子のサブグリッド）
   - タイトルが 2 行になるカードがあっても、隣のカードの著者情報・要約・ボタンの位置がそろう
4. **[コンテナクエリ](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/At-rules/@container)**: `.post` に [`container-type`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Properties/container-type)`: inline-size` を宣言し、
   **ビューポートではなくカード自身の幅**が 420px 以上のときだけタイトルと要約を大きくする
   - `@container` はネストして「その要素自身のルールの中」に書ける

## ポイント

- **メディアクエリからの卒業**: RAM パターンとコンテナクエリを使うと「画面幅ではなく、
  部品が置かれた場所の広さ」に応じてレイアウトが決まる。部品の再利用性が上がる
- **サブグリッドの考え方**: 子グリッドが自分で行を定義する代わりに、親の行トラックを「借りる」
- **フッターのメディアクエリは残す**: ページ全体の大枠は画面幅で決めてよい。
  すべてをコンテナクエリにする必要はなく、使い分けが大事

## 表示の確認

- スクロールするとヘッダーが上部に固定される
- ブラウザ幅を変えると、メディアクエリなしで記事一覧が 1 → 2 → 3 列に変化する
- 2 列表示のとき（カードが広いとき）だけカードのタイトルが大きくなる
- 「A beginner-friendly guide...」のタイトルが 2 行になる幅でも、
  隣のカードと著者情報・要約・ボタンの高さがそろっている（サブグリッドの効果）
