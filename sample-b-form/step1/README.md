# Sample B / Step 1 — Web フォームのマークアップとスタイリング

## このステップのゴール

基礎編と同じデザイントークンを使った「お問い合わせページ」を新規に作り、
フォーム部品の正しいマークアップと基本のスタイリングを学ぶ。

## やること

### HTML（フォームのマークアップ）

1. [`<form>`](https://developer.mozilla.org/ja/docs/Web/HTML/Reference/Elements/form) の中に、次の部品を並べる
   - お名前: [`<input type="text">`](https://developer.mozilla.org/ja/docs/Web/HTML/Reference/Elements/input) + `required`
   - メールアドレス: `<input type="email">`（形式チェックが自動で働く）+ `placeholder`
   - お問い合わせの種類: [`<select>`](https://developer.mozilla.org/ja/docs/Web/HTML/Reference/Elements/select) + `<option>`（先頭は `value=""` の「選択してください」）
   - 返信の希望: ラジオボタン 2 つを [`<fieldset>`](https://developer.mozilla.org/ja/docs/Web/HTML/Reference/Elements/fieldset) + `<legend>` でグループ化
   - ニュースレター購読: チェックボックス（任意項目）
   - メッセージ: [`<textarea>`](https://developer.mozilla.org/ja/docs/Web/HTML/Reference/Elements/textarea) + `required` + `minlength="10"`
   - 送信: [`<button type="submit">`](https://developer.mozilla.org/ja/docs/Web/HTML/Reference/Elements/button)
2. すべての入力欄に [`<label>`](https://developer.mozilla.org/ja/docs/Web/HTML/Reference/Elements/label) を付ける
   - テキスト系は `for` 属性と `id` で関連付け
   - ラジオ・チェックボックスは `<label>` で丸ごと包む書き方
3. 各欄の下に補足メッセージ `<p class="hint">` を置く（Step 2 でエラー表示に変える）
4. `autocomplete` 属性（`name` / `email`）でブラウザの自動入力を助ける

### CSS

1. デザイントークン・ヘッダー・パンくずは基礎編/ Sample A から流用
2. `.contact-form` を `display: grid` + `gap` で縦に整列（`max-width: 640px` で読みやすい幅に）
3. **入力欄の枠線・余白を自分でデザインする**
   - destyle.css はフォーム部品の見た目も完全にリセットしているため、
     枠線がない状態からのスタートになる
4. `textarea` は `resize: vertical` で縦方向のみリサイズ可能に

## ポイント

- **`<label>` は必須**: クリック範囲が広がり、スクリーンリーダーが項目名を読み上げられる。
  「見た目がラベルっぽいテキスト」ではだめ
- **`type` を正しく選ぶ**: `email` にするだけで形式チェックとスマホのキーボード切り替えが手に入る
- **制約は HTML 属性で宣言する**: `required` / `minlength` / `type` が Step 2 の CSS バリデーション表示の土台になる

## 表示の確認

- フォームが中央の 1 カラムで整列している
- 何も入力せず「送信する」を押すと、**ブラウザ標準のエラーメッセージ**が表示される
  （JavaScript を書いていないのに検証が動く＝制約検証は HTML の標準機能）
