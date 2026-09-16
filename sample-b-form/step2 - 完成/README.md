# Sample B / Step 2 — CSS だけのバリデーション UX（完成）

## このステップのゴール

JavaScript を使わず、HTML の制約検証（`required` / `type` / `minlength`）と
CSS の擬似クラスだけで「入力エラーがその場で分かる」フォームに仕上げる。

## やること

1. **[`accent-color`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Properties/accent-color)**: チェックボックスとラジオボタンをブランドカラーに（1 行で完了）
2. **[`:focus-visible`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Selectors/:focus-visible)**: キーボード操作時だけ青いフォーカスリングを表示する
3. **必須マークの自動表示**: [`:has()`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Selectors/:has) で「必須の欄を持つ `.field`」を選び、
   ラベルの後ろに `::after` で `*` を付ける（HTML に `*` を手書きしない）
4. **[`:user-invalid`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Selectors/:user-invalid) / `:user-valid`**: ユーザーが**一度さわった後**の欄だけ、
   不正なら赤い枠、正しければ緑の枠にする
5. **エラーメッセージの出し分け**: `.hint` をふだんは `display: none` にし、
   兄弟セレクタ `:user-invalid ~ .hint` のときだけ赤字で表示する
6. **送信ボタンの状態表示**: `form:invalid .submit-button { opacity: 0.5 }` で
   「まだ送信できない」ことを見た目で伝える

## ポイント

- **`:invalid` と `:user-invalid` の違い**が最重要。`:invalid` はページを開いた瞬間から
  必須欄がすべて「不正」扱いになり真っ赤になる。`:user-invalid` は
  「ユーザーが操作した後」だけ反応するので UX がよい
- **制約は HTML、見せ方は CSS** という役割分担。検証ロジックを 1 行も書いていない
- **CSS の限界も知る**: 送信ボタンの `opacity` は見た目の合図であって無効化ではない。
  本当に送信を止めているのはブラウザの制約検証。より高度な制御
  （エラー文言のカスタマイズ、送信の非同期化）は JavaScript の領域になる

## 表示の確認

- ラジオボタン・チェックボックスが青（ブランドカラー）になっている
- 必須項目のラベルに赤い `*` が付いている（HTML には書いていない）
- ページを開いた直後は**どの欄も赤くない**
- 名前欄をクリックして何も入力せず次の欄に移ると、名前欄が赤くなりエラーメッセージが出る
- メール欄に `abc` とだけ入力して離れると赤、正しい形式にすると緑になる
- すべて正しく入力すると送信ボタンの薄さが解除される
- Tab キーで移動すると、いま居る欄に青いフォーカスリングが表示される
