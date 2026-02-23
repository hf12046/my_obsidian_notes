---
source: https://qiita.com/ntaka329/items/a2b936b3796ed1ba7373
published: 2026-02-20
created: 2026-02-23
tags:
  - clippings
  - 生成AI
---
## はじめに

GMOコネクトの永田です。

**数十行の箇条書き → 49ページの提案スライド。**

大げさに聞こえるかもしれませんが、Claude Code と Slidev を組み合わせたワークフローで実現しました。

RFPへの提案書作成は、課題分析・ストーリー設計・図表作成・デザイン調整とやることが多く、正直しんどい作業です（ぶっちゃけ、やりたくない😇）。そのたたき台作成の **工数を激減させる** 、というのが本記事のテーマです。

「全自動で完成」とはいきません。人手レビューは引き続き必要です。ただ、「ゼロから書き始める」という最大の壁がなくなるだけで、体感は全然違います。

前回記事（Slidevテンプレート編）の続きとして、ワークフロー全体を解説します。

## （最初に）まとめ

|  | 内容 |
| --- | --- |
| **Input** | 提案コンセプト箇条書き（約20行） |
| **Output** | 49ページの Slidev 形式スライド |
| **方法** | 3フェーズ（計7プロンプト） |
| **ツール** | Claude Code / Slidev / context7 / Playwright MCP |
| **成功の鍵** | Phase 1（テンプレート整備）を先に固める |

成果物・プロンプト全文 → [https://github.com/gmoconnect/proposal-slide-sample](https://github.com/gmoconnect/proposal-slide-sample)

最終的に出来上がったスライド（PDF）→ [https://github.com/gmoconnect/proposal-slide-sample/blob/main/design/slidev/slides.pdf](https://github.com/gmoconnect/proposal-slide-sample/blob/main/design/slidev/slides.pdf)

---

## Before / After 比較

まず最初に、どんなInputをいれたら、最終的にどんなアウトプットになったか、を見てみます。

## Before — アーキテクトが用意したInput

`prompts/2_story/prompt-story.md` の「提案コンセプト」部分のみ（約20行）が実質的なInputです。

```markdown
### 提案コンセプト

AWSのサーバーレス構成＆マネージドサービスで、
NoOpsでコスト・可用性・性能・セキュリティのバランスをとる。

- 認証: Cognito
- CloudFront
  --> ALB(Cognito JWT verify)
  --> ECS on Fargate
  --> Aurora Serverless v2
- ダッシュボード: S3 --> Athena --> QuickSight
- CI/CD: codecommit --> CodeBuild --> ECR image
  - codepipeline(必要に応じ手動承認) --> CodeDeploy ECS Blue/Green(TestTrafficあり)
- バイナリデータはS3 pre-signed URLを利用して、クライアントから直接読み書きすることで、通信・処理負荷をオフロード
- Fargate Imageは、golang予定
  - 単一バイナリでImageSize最小
  - Multi-Stage build+distrolessなど軽量OSベースで、ImageSize最小化。不要なpackage無しによるCVE検知の減少
  - rootFileSystem readonlyによりセキュア化
- WAFはAWS ManagedRuleの利用を想定
  - WAFのSOCが必要な場合、WafCharmなどのSOCサービスの導入を検討
- Security
  - GuardDuty, CloudTrailなど
```

## After — 生成されたスライド例（3枚）

代表的な3枚を紹介します。全体は49ページのスライドが生成されました。

**① 定量効果サマリー（KPIカード）**

6つの評価観点すべてを定量値で一覧。 `KPICard` コンポーネントで数値のインパクトを強調しています。

[![定量効果サマリー（KPIカード）](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4174180/e787d903-c1c4-4179-8c59-1f8eb2fa0dcd.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4174180%2Fe787d903-c1c4-4179-8c59-1f8eb2fa0dcd.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7418fbaad6b8f565b41f9b754e9248d8)

---

**② Before/After 比較（CloudFront + Fargate 自動スケーリング）**

現行の固定構成と提案構成を左右対比。 `BeforeAfter` コンポーネントと `Callout` で、課題→解決をコンパクトにまとめています。

[![BeforeAfter比較スライド](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4174180/829fb859-4a8d-45ed-8c3c-297478efe049.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4174180%2F829fb859-4a8d-45ed-8c3c-297478efe049.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=80f1e3f3f1dfdee52ef8f7444a43eb02)

---

**③ プロセスフロー（S3 ライフサイクルポリシー）**

段階的なデータ移行フローとコスト比較表を組み合わせ。 `ProcessFlow` コンポーネントで時系列の流れを視覚化しています。

[![S3ライフサイクルプロセスフロー](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4174180/329b08d3-c9f5-4b1a-b155-161fd2608ab8.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4174180%2F329b08d3-c9f5-4b1a-b155-161fd2608ab8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=347d10c4ffba431ead99c0fc4c03ee2e)

---

## 具体的な実施手順

全体は **3フェーズ・7ステップ** で構成されています。以下の手順と各プロンプトを参考に、プロジェクトに応じてカスタマイズしてください。

このうち、Phase 1はテンプレートとノウハウ集の整備、Phase 2はストーリー作成、Phase 3はSlidev化に分かれています。

特にPhase 1の準備が成功の鍵となります。非常に手間と時間がかかる工程ですが、ここをしっかりやることで、Phase 2・3がスムーズに進むのと、今後も提案書作成のたびに再利用できる資産ができますので、がんばりましょう😊

## 事前準備

- Claude Code（VSCode拡張: `Claude Code for VS Code` ）をインストール
- モデル: Opus 4.6（+ Thinking推奨）
- MCPプラグイン追加: `context7` 、 `playwright`

## Phase 1: 提案書スライドテンプレートの作成

まず、提案書作成のためのテンプレートとノウハウ集を整備します。

### Step 1: 提案書ストーリーのノウハウ作成

**Chat Session**: 新規、Plan mode で方針確認後に実施

提案書のストーリー構成（Why→What→How、アンサーファーストなど）のノウハウ集を Markdown で作成します。自社に既存のテンプレートや過去の提案書があれば、そちらを活用する方が効果的です（pptx/pdf/画像でも可）。

以下、prompt例です。

```text
官公庁の入札などで、評価者に伝わりやすい（＝高得点を得やすい）提案書のノウハウをMarkdownで整理したい。
国内外問わず、世の中の評価が高い提案書のノウハウやテンプレートを検索し、整理できないか？

### ノウハウ例

- ストーリー構成
  - 顧客理解(why)-->what-->how
  - アンサーファースト、評価項目にストレートに回答
  - サマリー --> 詳細
  - スライド間の繋がり
  - 顧客の用語の利用
- スライドノウハウ
  - リード文
  - 情報密度のコントロール
  - 1スライド1メッセージ
  - 図表の多用、カード型などの視覚効果
- 説得力を強化
  - Before/After、定量効果（数値）
- 色、フォント、太字など
  - 白・青など信頼感、誠実さなどの感覚
  - アクセントカラー
  - Boldでの協調

### 参考資料の例

- https://research.njss.info/bid-guide/993729/
- https://research.njss.info/bid-guide/992690/
- https://www.alleyoop.co.jp/blog/302/
- https://sairu.co.jp/method/3543/
- https://sairu.co.jp/method/2601/
```

作成例: [`design/proposal-knowhow.md`](https://github.com/gmoconnect/proposal-slide-sample/blob/main/design/proposal-knowhow.md)

---

### Step 2: スライド作成ノウハウの収集

**Chat Session**: 新規、 `Ask before edits`

次に、Slidevコンポーネント設計に活用できるよう、外資系コンサル等のスライド例を調査し、スライド構成やビジュアル表現のノウハウをMarkdownでまとめます。提案書ノウハウ集にないが有用な内容があれば、提案書ノウハウ集にも反映させましょう。

ここも自社の過去提案書からスライド例を抽出してまとめるのも効果的です。

```text
「スライド構成の調査」を実施

### スライド構成の調査

- 「外資系コンサル スライド作成」などで検索し、実際のスライド例を調査
  - 例: https://logmi.jp/main/skillup/331325
- 提案書ノウハウ集( design/proposal-knowhow.md )にないが有用なノウハウがあれば、提案書ノウハウ集( design/proposal-knowhow.md )にも反映
- 将来的にslidevテンプレート化を見据え、どのようなコンポーネントがスライドで使われているかを調査
```

作成例: [`design/slide-component-survey.md`](https://github.com/gmoconnect/proposal-slide-sample/blob/main/design/slide-component-survey.md)

---

### Step 3: Slidev テンプレートの作成

**Chat Session**: Step 2 から継続、Plan mode で方針確認後に実施

最後に、上記の調査結果を元に、Slidev のレイアウト・コンポーネント・デザイントークンを作成します。context7 MCP で Slidev の最新仕様を確認しながら進めます。

```text
調査結果（ design/slide-component-survey.md ）と、
提案ノウハウ集（ design/proposal-knowhow.md ）を元に、slidevのテンプレートを作成。
提案書ノウハウ集に対しslidevでどのComponentを使うと良いかのslidevテンプレート利用ガイドを、
新規Markdownで作成。

### 作成内容

- slidevの仕様はcontext7で確認
- キッチンシンク的な説明ページ＋ノウハウに沿ったサンプルページ構成
- 16:9横表示
- <div>は直接使わず、できる限りComponentとして、再利用が可能でデザイン変更時の一括適用ができるようにすること。
```

作成例:

- [`design/slidev-usage-guide.md`](https://github.com/gmoconnect/proposal-slide-sample/blob/main/design/slidev-usage-guide.md) （13レイアウト・19コンポーネントのガイド）
- [`design/slidev/`](https://github.com/gmoconnect/proposal-slide-sample/tree/main/design/slidev) （テンプレートファイル群）

ここまでで、提案書作成のためのテンプレートとノウハウ集が整いました。次のフェーズでは、実際に提案ストーリーを作成していきます。

## Phase 2: 提案ストーリーを作成

### Step 4: ストーリー案の作成

**Chat Session**: 新規、Plan mode で方針確認後に実施

ここが本記事の核心です。 **`### 提案コンセプト` の箇条書きを自分で書くだけ** で、あとはClaudeが提案ノウハウに従ってストーリーを組み立てます。

```text
requirements/requirements_sample.md の提案依頼に対し、ストーリーをまずは作成したい。

- ストーリーは提案ノウハウに従う
  - design/proposal-knowhow.md
- まだslidevにはせず、普通のMarkdownで記載する。（ストーリーなど内容レビューの後、slidev化）
- 複雑な図は、別途デザイナーにて作成するので、絵に含めたい内容をテキストでまとめる。

### 提案コンセプト

AWSのサーバーレス構成＆マネージドサービスで、NoOpeでコスト・可用性・性能・セキュリティのバランスをとる。

- 認証: Cognito
- CloudFront
  --> ALB(Cognito JWT verify)
  --> ECS on Fargate
  --> Aurora Serverless v2
- ダッシュボード: S3 --> Athena --> QuickSight
- CI/CD: codecommit --> CodeBuild --> ECR image
  - codepipeline(必要に応じ手動承認) --> CodeDeploy ECS Blue/Green(TestTrafficあり)
- バイナリデータはS3 pre-signed URLを利用して、クライアントから直接読み書きすることで、通信・処理負荷をオフロード
- Fargate Imageは、golang予定
  - 単一バイナリでImageSize最小
  - Multi-Stage build+distrolessなど軽量OSベースで、ImageSize最小化。不要なpackage無しによるCVE検知の減少
  - rootFileSystem readonlyによりセキュア化
- WAFはAWS ManagedRuleの利用を想定
  - WAFのSOCが必要な場合、WafCharmなどのSOCサービスの導入を検討
- Security
  - GuardDuty, CloudTrailなど
```

内容は、よくあるオンプレからAWSサーバーレス構成への提案を想定したものですが、実際のプロジェクトに合わせて適宜変更してください。

ClaudeがPhase1のノウハウに沿って、ストーリー構成を作ってくれているのが分かりますね。

[![スクリーンショット 2026-02-19 23.10.36.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4174180/563e6a8e-af85-4a6c-a15e-c0dc00032fe9.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4174180%2F563e6a8e-af85-4a6c-a15e-c0dc00032fe9.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=9a7d966719bb12ba4a71cb32877bbf32)

作成例: [`proposal/story-before-review.md`](https://github.com/gmoconnect/proposal-slide-sample/blob/main/proposal/story-before-review.md)

---

### Step 5: ストーリー案のレビュー＆修正

**Chat Session**: 新規、 `Ask before edits`

作成したストーリーを「分かりやすい提案書か？」という観点でレビューし、スライド分量も調整します。コンテキストが混ざらないよう、複数の新規セッションで繰り返すと品質が上がります。

```text
作成したストーリー( proposal/story.md ) を、slidev形式（16:9横）のMarkdownにする予定。
slidev形式にする前に、提案ストーリーや構成を、勝てる提案書（＝評価者から高得点を得られるスライド）か？レビューして欲しい。
また、（16:9横）だと溢れそう・余白が多そうなスライドは、適切に分割・統廃合して欲しい。

- 提案書のガイドライン
  - design/proposal-knowhow.md
```

作成例: [`proposal/story.md`](https://github.com/gmoconnect/proposal-slide-sample/blob/main/proposal/story.md)

非常に手間と時間がかかりますが、実務では人手によるレビューを必ず併用してください。

なお、今回の例だとストーリーについては、レビューをほぼ入れていないため、ツッコミどころが多々残っていますので、ご承知おきください。

## Phase 3: Slidev 形式の Markdown に変換

### Step 6: Slidev 形式への変換

**Chat Session**: 新規、Plan mode で方針確認後に実施

ストーリーを Slidev Markdown に変換します。内容的には前回の記事と同じです。  
Playwright MCP を使ってClaudeが表示確認しながら修正を進めます。Slidevは自分で起動して、ポート番号をClaudeに伝えましょう。  
（Claudeがslidevを起動すると不安定なことがあったので）

```text
作成したストーリー( proposal/story.md )を、slidev（16:9横）に変換。
変換にあたり確認、要決定事項があれば提示し、合わせて推奨案も含めて提示。

slidevの起動はこちらで行うので、起動が必要になったらコマンドを例示して起動を依頼してください。
また、スライドの表示確認は、playwright mcpを使ってください。

### 参照するドキュメント

- 提案書のガイドライン
  - design/proposal-knowhow.md
- slidev化のガイドライン
  - design/slidev-usage-guide.md

### slidevの起動例

npx slidev story.md --port 3030
```

作成例: [`design/slidev/slides.md`](https://github.com/gmoconnect/proposal-slide-sample/blob/main/design/slidev/slides.md)

---

### Step 7: Slidev 形式のレビュー＆修正

**Chat Session**: 新規、 `Ask before edits`

Playwright MCP でスライドを確認しながら、ガイドラインの観点で品質を上げます。納得できるまで複数セッションで繰り返します。

```text
スライド( design/slidev/slides.md )をガイドラインの観点で再レビューし、
ガイドラインに沿った評価者が理解しやすい（＝高得点を得やすい）スライドかを確認。

slidevはport3030で起動中。

- 提案書のガイドライン
  - design/proposal-knowhow.md
- slidev化のガイドライン
  - design/slidev-usage-guide.md

評価者が理解しやすいスライドだと確信したら、ユーザーにPDF変換のコマンド例を例示してください。

### pdf変換コマンド例

npx slidev export slides_008.md --output slides_008.pdf
```

Claudeレビューで色々と指摘はしてくれています。

[![スクリーンショット 2026-02-20 14.41.31.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4174180/a3f87dfe-27cd-4178-b2cd-7cc8cb613a84.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4174180%2Fa3f87dfe-27cd-4178-b2cd-7cc8cb613a84.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=95bead54299b1d84c17d43e21e872d54)

[![スクリーンショット 2026-02-20 14.52.46.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4174180/1c7779cd-973c-419b-bf85-0bca5bdbf3f1.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4174180%2F1c7779cd-973c-419b-bf85-0bca5bdbf3f1.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=4446734384272bbfff585bc2e45f56e4)

ぱっと見、色々と指摘をしてくれてはいますが、後で目視でも見たところ、結構気になるところはありました。  
チェックリストにある観点でも漏れていることが多々あったので、注意が必要です。

非常に手間と時間がかかりますが、実務では人手によるレビューを必ず併用してください。（2回目）

## まとめ＋所感

## できたこと

- 約20行の箇条書きから **49ページの提案スライド** を生成
- KPIカード・BeforeAfter・プロセスフローなど **提案書らしいビジュアル** を自動生成
- Claude が Playwright MCP でスライドを **自律的に確認・修正**

## まだ改善の余地あり

- アーキテクチャ図は別途作成が必要（次回、Google AI Studio連携にチャレンジ予定）
- 人手レビューは引き続き必須（ガイドラインのチューニングで徐々に改善可能）
- テンプレートは自社既存のものを流用する方がより効果的

## 所感

「たたき台をゼロから作る」という最大の壁がなくなっただけで、体感はかなり違います。  
特にPhase 1のテンプレート整備を一度やってしまえば、次回以降はさらにスムーズです。

提案書作成に苦労されている方、ぜひ試してみてください。