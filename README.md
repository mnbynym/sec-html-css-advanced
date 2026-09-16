# HTML5 と CSS で学ぶモダン・ウェブページの作成 ― 応用編

基礎編（`sec-html-css-basic`）で作った MDN Blog 風ページを題材に、
モダン CSS・高度なレイアウト・アニメーション・Web フォームを学ぶ 3 時間の研修教材。
**JavaScript は使わない**（CSS と HTML の標準機能だけでどこまでできるかを体験する）。

## 前提

- 基礎編を修了していること（デザイントークン・Flexbox・Grid・メディアクエリを使えること）
- プレビューには VS Code の Live Server など `http://localhost` を使うこと
  （Sample A Step 3 の View Transitions は `file://` では動かない）
- ブラウザは最新の Chrome / Edge を推奨
  （スクロール連動アニメーションなど一部機能は Chromium 系のみ対応）

## 構成（2 サンプル / 全 5 ステップ）

テーマが並列な応用編は、積み上げ型の 1 サンプルにせず 2 つに分ける。

### Sample A — ブログページの発展（約 2 時間）

基礎編の完成形を出発点に、CSS だけを進化させていく。

| ステップ | テーマ | 主な内容 |
| --- | --- | --- |
| step1 | Modern CSS へのリファクタ | CSS ネスト・`clamp()`・`color-mix()`・`:has()` |
| step2 | 高度なレイアウト | `position: sticky`・RAM パターン・サブグリッド・コンテナクエリ |
| step3 - 完成 | アニメーションとインタラクション | `transition`・`@keyframes`・スクロール連動・View Transitions・`prefers-reduced-motion` |

### Sample B — Web フォーム（約 1 時間）

同じデザイントークンを使った「お問い合わせページ」を新規に作る。

| ステップ | テーマ | 主な内容 |
| --- | --- | --- |
| step1 | フォームのマークアップ | `<form>` `<label>` `<input>` `<select>` `<textarea>` `<fieldset>`・制約属性 |
| step2 - 完成 | CSS だけのバリデーション UX | `:user-invalid`・`:focus-visible`・`accent-color`・エラーの出し分け |

## 進め方

各ステップのフォルダには**そのステップを終えた状態**のファイルが入っている。
受講生は前のステップのフォルダをコピーし、README の「やること」に沿って編集してから、
ステップのフォルダと見比べて答え合わせをする（基礎編と同じ方式）。

## このシリーズで扱わないもの（次回以降）

- JavaScript 全般（DOM 操作・イベント・fetch による Web API の利用）
- フォーム送信先の実装（バックエンド）
- ダークモード対応（`prefers-color-scheme`）・`<picture>` によるレスポンシブ画像
