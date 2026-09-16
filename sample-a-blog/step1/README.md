# Sample A / Step 1 — Modern CSS へのリファクタリング

## このステップのゴール

基礎編で完成させたブログページを、**見た目を変えずに**最新の CSS 構文で書き直す。
「動くコードを、より読みやすく・保守しやすく作り直す」リファクタリングを体験する。

## 出発点

基礎編の完成形（`sec-html-css-basic/step6 - 完成`）と同じ HTML・CSS。
HTML はこのサンプルの Step 2 まで一切変更しない。

## やること

1. **[CSS ネスト](https://developer.mozilla.org/ja/docs/Web/CSS/Guides/Nesting)**: コンポーネント（`.post` や `.nav-list`）ごとに関連ルールを 1 つのブロックにまとめる
   - `&:hover` `&:active` のように擬似クラスを親ルールの中に書く
   - `@media` もコンポーネントの中にネストできる（末尾の「レスポンシブ対応」セクションが不要になる）
2. **[`clamp()`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Values/clamp)**: `.page-title` の文字サイズと余白を `clamp(最小, 推奨, 最大)` の流体指定に変え、
   メディアクエリによる上書きを削除する
3. **[`color-mix()`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Values/color_value/color-mix)**: ボタンのホバー色 2 つを固定値でなく基本色から自動生成する
   （`color-mix(in srgb, var(--button-primary-default), white 30%)`）
4. **[`:has()`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Selectors/:has)**: フッターの列内のリンクにホバーしたら、**親側の**列見出しの色が変わるようにする
   （子の状態から親を選択できるのは `:has()` だけ）

## ポイント

- **リファクタリングの原則**: 見た目のスクリーンショットを before / after で比べて同じであること
- **ネストの単位**: 何でもネストせず「1 コンポーネント = 1 ブロック」を目安にする（深いネストは逆に読みにくい）
- **流体タイポグラフィ**: `clamp()` の推奨値に `rem + vw` を混ぜると画面幅に比例して伸縮する
- **デザイントークンの削減**: `color-mix()` により「基本色を変えるだけでホバー色も追従する」

## 表示の確認

見た目は基礎編の完成形と**完全に同じ**であること（唯一の変化はフッター列のホバーで見出しの色が変わること）。
CSS の行数と `@media` ブロックの数が減っていることを確認する。
