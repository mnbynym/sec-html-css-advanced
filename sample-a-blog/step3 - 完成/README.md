# Sample A / Step 3 — アニメーションとインタラクション（完成）

## このステップのゴール

JavaScript を 1 行も書かずに、CSS だけで「動き」を付ける。
仕上げに記事詳細ページ（`article.html`）を追加し、ページ間の遷移もアニメーションさせる。

## やること

### 1. マイクロインタラクション

- カードのホバー演出: `.post` に [`translate`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Properties/translate) と [`box-shadow`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Properties/box-shadow) + `transition`
  - `translate` / `scale` / `rotate` は `transform` の**個別プロパティ**（モダンな書き方）
- ナビのホバーにも `transition` を追加してなめらかに

### 2. キーフレームアニメーション

- [`@keyframes`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/At-rules/@keyframes) で `fade-up`（下からふわっと）を定義し、ページ見出しの表示時に適用

### 3. スクロール連動アニメーション

- [`animation-timeline`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/Properties/animation-timeline)`: view()` で、カードが**画面に入るのに合わせて**フェードイン
- 時間ではなくスクロール位置がアニメーションの進行度になる
- 未対応ブラウザがあるため `@supports (animation-timeline: view())` で囲む（プログレッシブ・エンハンスメント）

### 4. View Transitions（ページ間の遷移）

- 記事詳細ページ `article.html` を追加し、1 件目のカードの Read more からリンクする
- [`@view-transition`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/At-rules/@view-transition)` { navigation: auto; }` を両ページの CSS に書くだけで、ページ移動がクロスフェードになる
- 一覧のカード画像と記事ページの画像に同じ `view-transition-name`（クラス `.vt-featured`）を
  付けると、**画像が拡大しながら移動する**演出になる

### 5. 動きを減らす配慮

- [`prefers-reduced-motion`](https://developer.mozilla.org/ja/docs/Web/CSS/Reference/At-rules/@media/prefers-reduced-motion) メディアクエリで、OS で「視差効果を減らす」を
  設定しているユーザーにはアニメーションと遷移を無効にする

### 補足：CSS の整理

- 著者情報の行（`.post-meta`）はカードと記事ページの両方で使うため、
  `.post` のネストから**外に**移動した（スコープの見直しもリファクタリングの一部）

## ポイント

- **動きは「意味」のために**: 浮き上がり＝クリックできる、フェードイン＝視線誘導。飾りのための動きは足さない
- **プログレッシブ・エンハンスメント**: `@supports` で囲めば、未対応ブラウザでは単に動きがないだけでページは壊れない
- **アクセシビリティ**: `prefers-reduced-motion` への対応は動きを付けた人の責任

## 表示の確認

⚠️ View Transitions は `file://`（ファイルを直接開く）では動作しない。
VS Code の **Live Server** など、`http://localhost` でプレビューすること。

- カードにホバーすると浮き上がり、影がつく
- ページを再読み込みすると「Blog it better」が下からふわっと現れる
- スクロールすると、画面に入ってきたカードがフェードインする（Chrome / Edge）
- 1 件目のカードの Read more で記事ページに移動する際、カード画像が拡大しながら遷移する
- OS の設定で「動きを減らす」を有効にすると、上記の動きがすべて止まる
  （開発者ツール → レンダリングタブ → prefers-reduced-motion をエミュレートでも確認可能）
