---
source: https://note.com/anpanpoteto/n/nbca0934b8f44
published: 2026-02-16
created: 2026-02-23
tags:
  - clippings
  - 生成AI
---
![見出し画像](https://assets.st-note.com/production/uploads/images/252082798/rectangle_large_type_2_203d0f8b7f6f0b79f6140691e1d2e1a7.png?width=1280)

## スライド作成を自動化するClaude「skills」の作り方

[Taro Segawa](https://note.com/anpanpoteto)

＊以下をClaudeにコピペして、テンプレートを添付するのみで、プレゼン資料を自社テンプレートに合わせて自動生成する「skills」を作成することが可能です。  

  
会社や組織の既存テンプレートPPTXを活用し、Claudeが用途や対象に応じてスライドを選択・構成・テキスト編集してPPTXを出力する「スライドジェネレータースキル」の作り方。

---

## このスキルでできること

テンプレートPPTX（数十ページの「全部入り」資料）を登録しておくと、Claudeに「○○向けの資料を作って」と依頼するだけで、必要なスライドだけを抜き出し、テキストを差し替えたPPTXを自動生成できる。

**活用シーンの例：**

- 営業先ごとにカスタマイズしたピッチデック
- 社内向けの部門紹介・プロジェクト報告
- 採用説明会向けの会社紹介資料
- 投資家向けの事業計画プレゼン
- 研修・セミナー用のスライドセット
- パートナー企業への協業提案

共通するのは「ベースとなるスライド群が既にあり、対象や目的によって構成を変えたい」という点。

---

## 全体像

```cpp
必要なもの                  作るもの                       使い方
─────────                  ─────────                     ─────────
テンプレートPPTX     →     スキル一式                →   「○○向けの資料を作って」
（全部入りの資料）          ├── SKILL.md                   と言うだけで
                           ├── slide-catalog.json         テンプレートからスライドを選び
                           ├── scripts/generate.py        テキストを差し替えた
                           └── template/○○.pptx          PPTXを自動生成
```

所要時間の目安：テンプレート解析〜スキル完成まで **約1〜2時間** （Claudeとの対話込み）

---

## Phase 1: テンプレートPPTXの準備

### 必要な素材

テンプレートとなるPPTXファイルを1つ用意する。以下の条件を満たすものが理想的。

- **PPTX形式** であること（PDFやGoogleスライドではなく、.pptx）
- **20〜60ページ** 程度（少なすぎると選択の幅がなく、多すぎるとカタログ作成が大変）
- **完成形のデザイン** が含まれていること（ロゴ、配色、フォント、イラスト等）
- 対象や用途によって「使う/使わない」を切り替えたいスライドが混在していること

### テンプレートが手元にない場合

- 過去に作った資料から、最も完成度の高いものを選ぶ
- 「全部入り」のマスターデッキがあればベスト
- なければ複数の資料から良いスライドを1つのPPTXにまとめて作成してもよい

---

## Phase 2: テンプレートの解析

ClaudeにPPTXファイルをアップロードし、以下のプロンプトで解析を依頼する。

### プロンプト例

```cpp
このPPTXファイルは弊社のテンプレートです。
これを使って、対象や用途に応じてスライドを選択・構成するスキルを作りたいです。

まず、テンプレートの中身を解析してください：
1. 全スライドのサムネイルを生成して確認
2. 各スライドの内容・レイアウトパターンを分類
3. カテゴリ分け（会社紹介/課題提起/ソリューション/等）
```

### Claudeが実行する解析コマンド

```php
# サムネイル一覧を生成（レイアウト確認用）
python /mnt/skills/public/pptx/scripts/thumbnail.py template.pptx

# テキスト内容を抽出
python -m markitdown template.pptx
```

### 解析で把握すべきこと

各スライドについて以下を整理する：

項目 内容 例 **ページ番号** PPTXの何ページ目か 6 **スライドファイル名** XML上のファイル名 slide6.xml **名前** スライドの内容を表す名前 会社概要 **カテゴリ** 大まかな分類 company **レイアウトタイプ** デザインパターン table, columns, diagram 等 **編集可能な要素** 差し替え可能なテキスト タイトル、本文、数値 **使うべき場面** どんな時に選ぶか 会社の基本情報を紹介する場合

---

## Phase 3: slide-catalog.json の作成

解析結果をもとに、全スライドの情報をJSON形式でカタログ化する。これがスキルの心臓部。

### フォーマット

```javascript
{
  "version": "1.0",
  "template_file": "template.pptx",
  "total_slides": 30,
  "categories": {
    "structural": "構造スライド（表紙、目次、セクション区切り、クロージング）",
    "company": "会社紹介",
    "problem": "課題提起",
    "solution": "ソリューション",
    "product": "プロダクト紹介",
    "strategy": "事業戦略（ビジネスモデル、市場規模等）"
  },
  "slides": [
    {
      "id": "cover",
      "name": "表紙",
      "category": "structural",
      "template_page": 1,
      "slide_file": "slide1.xml",
      "description": "会社ロゴとタイトルを表示",
      "editable_fields": [
        {
          "field": "title",
          "description": "プレゼンタイトル",
          "default": "会社紹介資料"
        },
        {
          "field": "date",
          "description": "日付",
          "default": ""
        }
      ],
      "use_when": "すべてのプレゼンの冒頭に使用",
      "layout_type": "title",
      "required": true
    }
  ],
  "preset_compositions": {
    "full-intro": {
      "name": "フル紹介",
      "duration": "30分",
      "description": "全セクションを網羅したフルプレゼン",
      "slides": ["cover", "toc", "company-overview", "...", "closing"]
    },
    "short-pitch": {
      "name": "ショートピッチ",
      "duration": "10分",
      "description": "要点を絞った短めのプレゼン",
      "slides": ["cover", "problem", "solution", "closing"]
    }
  }
}
```

### カタログ作成のコツ

**idの命名規則：**

- 英語のケバブケース（company-overview, market-size）
- 内容を端的に表す名前にする
- セクション区切りは section-divider-xxx で統一

**カテゴリの決め方：**

- structural は必須（表紙・目次・セクション区切り・クロージング）
- それ以外は資料の構造に合わせて自由に定義（4〜8カテゴリが目安）
- 例：company, problem, solution, product, feature, strategy, team, case-study

**editable\_fields のポイント：**

- 画像中心のスライド（スクリーンショット等）は空にしてよい
- テキスト中心のスライドは差し替え可能なフィールドをすべて列挙する
- default には現在テンプレートに入っているテキストを記載する（Claudeが差分を理解しやすくなる）

**preset\_compositions の設計：**

- 最低2〜3パターンは用意する
- 想定される主要ユースケースごとに1パターン
- 典型的なパターン例：

パターン 対象 時間目安 特徴 フル紹介 初対面の相手 30分 全セクション網羅 ショートピッチ 既存の関係者 10〜15分 課題→解決策に絞る 経営層向け 意思決定者 15分 ROI・事業計画中心 技術者向け 実務担当者 20分 デモ・機能中心 社内向け 自社メンバー 10分 概要・進捗中心

---

## Phase 4: SKILL.md の作成

以下のテンプレートをベースに、自社固有の情報を埋める。{...} の箇所を置き換える。

```ruby
---
name: {スキル名}-slide-generator
description: |
  {組織名}のスライドを、テンプレートPPTXから必要なページを選択・複製・編集して生成するスキル。
  ユーザーの要望（対象、目的、強調ポイントなど）に基づき、適切なスライド構成を提案し、
  対話的にカスタマイズしながらPPTXファイルを出力する。

  トリガー条件:
  - 「資料を作って」「スライドを作成」「プレゼン資料」「ピッチデック」
  - 「○○向けの資料」「○○用のスライド」
  - テンプレートからスライドを選んで構成したい場合
---

# {組織名} スライドジェネレーター

## ⚠️ 最重要ルール

**このスキルは必ずテンプレートPPTXファイルを使用してスライドを生成する。**
**テンプレートが見つからない場合でも、絶対にpptxgenjsでゼロから作成してはならない。**
**テンプレートが見つからなければ、ユーザーにアップロードを依頼して待機すること。**

テンプレート探索順序：
1. \`/mnt/skills/user/{スキル名}-slide-generator/template/{テンプレートファイル名}.pptx\`
2. \`/mnt/user-data/uploads/\` 内の \`.pptx\` ファイル
3. どちらにもなければ → ユーザーにアップロードを依頼（pptxgenjsは使わない）

## ワークフロー

\`\`\`
1. 要件ヒアリング → 2. スライド構成提案 → 3. ユーザー確認 → 4. PPTX生成 → 5. QA → 6. 納品
\`\`\`

### Step 1: 要件ヒアリング

ユーザーから以下の情報を収集する（不明な場合は確認する）：

| 項目 | 説明 |
|------|------|
| **対象** | 誰に向けたプレゼンか |
| **目的** | プレゼンのゴール |
| **時間** | 想定時間 |
| **強調ポイント** | 特に訴求したい内容 |
| **カスタマイズ** | テキスト変更の要望 |

### Step 2: スライド構成提案

\`slide-catalog.json\` のカタログを参照し、以下のルールで構成を提案する：

- 必ず「表紙」で始まり「クロージング」で終わる
- セクション区切りスライドを適宜挿入する
- 10分 → 8〜12枚、15分 → 10〜15枚、30分 → 20〜30枚が目安
- 対象の関心に合わせてスライドの優先度を調整

プリセット構成：
{ここにpreset_compositionsの内容を転記}

### Step 3: ユーザー確認/調整

提案した構成をユーザーに提示し、追加/削除/順序変更/テキスト変更を確認する。

### Step 4: PPTX生成

**重要: PPTXスキル（/mnt/skills/public/pptx/editing.md）のワークフローに従う**
**絶対にpptxgenjsでゼロから作成してはならない。必ずテンプレートPPTXから生成すること。**

#### Step 4a: テンプレート発見（最重要）

以下の順序でテンプレートPPTXを探す。
**見つからない場合はpptxgenjsに切り替えず、ユーザーにアップロードを依頼すること。**

\`\`\`bash
TEMPLATE=""

# 1. スキルディレクトリ内
if [ -f "/mnt/skills/user/{スキル名}-slide-generator/template/{ファイル名}.pptx" ]; then
  TEMPLATE="/mnt/skills/user/{スキル名}-slide-generator/template/{ファイル名}.pptx"
# 2. ユーザーアップロード
elif ls /mnt/user-data/uploads/*.pptx 2>/dev/null | head -1; then
  TEMPLATE=$(ls /mnt/user-data/uploads/*.pptx 2>/dev/null | head -1)
# 3. 見つからない
else
  echo "ERROR: テンプレートPPTXが見つかりません。アップロードを依頼してください。"
  exit 1
fi

cp "$TEMPLATE" /home/claude/template.pptx
\`\`\`

**⚠️ テンプレートが見つからない場合の対応：**
- **絶対にpptxgenjsでゼロから作成しない**
- ユーザーにテンプレートPPTXのアップロードを依頼する
- アップロードされるまで処理を中断する

#### Step 4b: アンパック〜スライド選択〜パック

\`\`\`bash
# 1. アンパック
python /mnt/skills/public/pptx/scripts/office/unpack.py /home/claude/template.pptx /home/claude/unpacked/

# 2. スライド選択（generate.pyを使用）
python /mnt/skills/user/{スキル名}-slide-generator/scripts/generate.py /home/claude/unpacked/ "cover,..."

#    generate.pyが見つからない場合の手動手順：
#    (a) ppt/_rels/presentation.xml.rels からrId→slideファイルの対応を確認
#    (b) slide-catalog.json の slide_file を参照し、残すスライドのrIdを特定
#    (c) ppt/presentation.xml の <p:sldIdLst> 内で残す <p:sldId> だけ記述
#    (d) 不要な <p:sldId> 行を削除

# 3. テキスト編集（str_replaceツールで各slideのXMLを編集）

# 4. クリーンアップ
python /mnt/skills/public/pptx/scripts/clean.py /home/claude/unpacked/

# 5. パック
python /mnt/skills/public/pptx/scripts/office/pack.py /home/claude/unpacked/ /home/claude/output.pptx --original /home/claude/template.pptx
\`\`\`

### Step 5: QA

\`\`\`bash
python -m markitdown /home/claude/output.pptx
python /mnt/skills/public/pptx/scripts/office/soffice.py --headless --convert-to pdf /home/claude/output.pptx
pdftoppm -jpeg -r 150 /home/claude/output.pdf slide
\`\`\`

### Step 6: 納品

\`\`\`bash
cp /home/claude/output.pptx /mnt/user-data/outputs/プレゼン資料.pptx
\`\`\`

## テンプレートファイルの探索（重要）

**テンプレートPPTXファイルの探索は以下の優先順位で行う：**

### 優先度1: スキルディレクトリ
\`\`\`
/mnt/skills/user/{スキル名}-slide-generator/template/{ファイル名}.pptx
\`\`\`

### 優先度2: ユーザーアップロード
\`\`\`bash
ls /mnt/user-data/uploads/*.pptx 2>/dev/null
\`\`\`

### テンプレートが見つからない場合
**絶対にpptxgenjsでゼロから作成してはならない。**
ユーザーにアップロードを依頼して待機する。

**なぜゼロから作成してはならないか：**
- テンプレートにはブランドデザイン（ロゴ、配色、レイアウト、イラスト）が含まれている
- 高品質なスライドデザインが既に用意されている
- pptxgenjsで再現しようとすると品質が大幅に劣化する
- テンプレートからの選択・編集が本スキルの根幹である

## テキスト編集のガイドライン

- **フォーマット保持**: XML編集時、既存の \`<a:rPr>\`（フォント、サイズ、色）をそのまま維持する
- **日本語テキスト**: \`lang="ja-JP"\` を適切に設定する
- **改行**: 元のスライドの改行位置を尊重し、テキストが溢れないようにする
- **Bold指定**: ヘッダーや強調テキストは \`b="1"\` を維持する

## トラブルシューティング

| 問題 | 対処法 |
|------|--------|
| テンプレートPPTXが見つからない | ユーザーにPPTXファイルのアップロードを依頼 |
| スライドのデザインが崩れる | テキスト量を元のスライドと同程度に調整 |
| 文字化けが発生 | \`lang="ja-JP"\` の設定を確認 |
| スライド番号がずれる | \`<p:sldIdLst>\` の順序を再確認 |
```

---

## Phase 5: generate.py の作成

スライド選択・フィルタリング用のヘルパースクリプト。以下をそのまま使い、パスだけ変更する。

変更すべき箇所は CATALOG\_CANDIDATES 内のパス（2箇所）のみ。

```python
#!/usr/bin/env python3
"""
スライドジェネレーター ヘルパー
テンプレートPPTXから必要なスライドを選択・並び替え・不要スライドを削除する。

使い方:
  python generate.py <unpacked_dir> <slide_ids_comma_separated>
  python generate.py <unpacked_dir> "preset:<プリセット名>"
"""

import json, os, re, sys
from pathlib import Path

SKILL_DIR = Path(__file__).parent.parent
CATALOG_CANDIDATES = [
    SKILL_DIR / "slide-catalog.json",
    # ↓ 自社のスキルパスに変更する
    Path("/mnt/skills/user/{スキル名}-slide-generator/slide-catalog.json"),
    Path("/home/claude/{スキル名}-slide-generator/slide-catalog.json"),
]

def load_catalog():
    for path in CATALOG_CANDIDATES:
        if path.exists():
            with open(path, "r", encoding="utf-8") as f:
                return json.load(f)
    raise FileNotFoundError(
        f"slide-catalog.json が見つかりません。探索パス: "
        f"{[str(p) for p in CATALOG_CANDIDATES]}"
    )

def get_slide_mapping(catalog, selected_ids):
    slides_by_id = {s["id"]: s for s in catalog["slides"]}
    mapping = []
    for sid in selected_ids:
        if sid not in slides_by_id:
            print(f"WARNING: Unknown slide id '{sid}', skipping",
                  file=sys.stderr)
            continue
        slide = slides_by_id[sid]
        mapping.append({
            "id": sid,
            "name": slide["name"],
            "slide_file": slide["slide_file"],
            "template_page": slide["template_page"],
            "editable_fields": slide.get("editable_fields", []),
            "layout_type": slide.get("layout_type", "unknown"),
        })
    return mapping

def read_presentation_xml(d):
    with open(os.path.join(d, "ppt", "presentation.xml"),
              "r", encoding="utf-8") as f:
        return f.read()

def write_presentation_xml(d, content):
    with open(os.path.join(d, "ppt", "presentation.xml"),
              "w", encoding="utf-8") as f:
        f.write(content)

def get_rid_to_slide_mapping(d):
    with open(os.path.join(d, "ppt", "_rels", "presentation.xml.rels"),
              "r", encoding="utf-8") as f:
        content = f.read()
    return {
        m.group(1): m.group(2)
        for m in re.finditer(
            r'Id="(rId\d+)"\s+[^>]*Target="slides/(slide\d+\.xml)"',
            content,
        )
    }

def filter_slides(unpacked_dir, keep_slide_files):
    pres_xml = read_presentation_xml(unpacked_dir)
    match = re.search(
        r'<p:sldIdLst>(.*?)</p:sldIdLst>', pres_xml, re.DOTALL
    )
    if not match:
        print("ERROR: Cannot find <p:sldIdLst>", file=sys.stderr)
        return

    entries = {}
    for m in re.finditer(r'(<p:sldId\s+[^/]*/>)', match.group(1)):
        tag = m.group(1)
        rid = re.search(r'r:id="(rId\d+)"', tag)
        if rid:
            entries[rid.group(1)] = tag

    rid_to_slide = get_rid_to_slide_mapping(unpacked_dir)
    slide_to_rid = {v: k for k, v in rid_to_slide.items()}

    new_tags = []
    for sf in keep_slide_files:
        rid = slide_to_rid.get(sf)
        if rid and rid in entries:
            new_tags.append(entries[rid])
        else:
            print(f"WARNING: Cannot find slide '{sf}'",
                  file=sys.stderr)

    new_block = (
        "<p:sldIdLst>\n    "
        + "\n    ".join(new_tags)
        + "\n  </p:sldIdLst>"
    )
    pres_xml = re.sub(
        r'<p:sldIdLst>.*?</p:sldIdLst>',
        new_block,
        pres_xml,
        flags=re.DOTALL,
    )
    write_presentation_xml(unpacked_dir, pres_xml)
    print(f"Updated: keeping {len(new_tags)} slides")

def main():
    if len(sys.argv) < 3:
        print(
            "Usage: python generate.py <unpacked_dir> "
            "<slide_ids|preset:name>"
        )
        sys.exit(1)

    unpacked_dir, slide_ids_str = sys.argv[1], sys.argv[2]
    catalog = load_catalog()

    if slide_ids_str.startswith("preset:"):
        preset_name = slide_ids_str.split(":", 1)[1]
        preset = catalog["preset_compositions"][preset_name]
        selected_ids = preset["slides"]
        print(f"Using preset: {preset['name']} ({preset['duration']})")
    else:
        selected_ids = [s.strip() for s in slide_ids_str.split(",")]

    mapping = get_slide_mapping(catalog, selected_ids)
    if not mapping:
        print("ERROR: No valid slides", file=sys.stderr)
        sys.exit(1)

    print(f"\n=== スライド構成（{len(mapping)}枚）===")
    for i, s in enumerate(mapping, 1):
        mark = "✏️" if s["editable_fields"] else "📋"
        print(
            f"  {i:2d}. {s['name']} [{s['layout_type']}] "
            f"{mark}  → {s['slide_file']}"
        )

    if os.path.isdir(unpacked_dir):
        filter_slides(
            unpacked_dir, [m["slide_file"] for m in mapping]
        )

if __name__ == "__main__":
    main()
```

---

## Phase 6: フォルダ構成とデプロイ

### 最終フォルダ構成

```cpp
{スキル名}-slide-generator/
├── SKILL.md                        ← スキル定義
├── slide-catalog.json              ← 全スライドカタログ＋プリセット
├── scripts/
│   └── generate.py                 ← スライド選択ヘルパー
└── template/
    └── {テンプレート名}.pptx        ← テンプレート本体
```

### デプロイ方法

1. 上記フォルダをZIPにまとめる
2. Claudeプロジェクトの「カスタムスキル」としてアップロード
3. /mnt/skills/user/{スキル名}-slide-generator/ に配置される

---

## Phase 7: 動作テスト

デプロイ後、以下の4パターンで動作確認する。

**テスト1: プリセット生成** → テンプレートからスライドが正しく抜き出され、PPTXが生成されること

**テスト2: カスタム構成** → 「○○向けに10分の資料を作って」でヒアリング→構成提案→生成が動くこと

**テスト3: テキスト編集** → タイトルや本文の差し替えが正しく反映され、デザインが崩れないこと

**テスト4: テンプレート未配置（異常系）** → テンプレートがない状態で「アップロードしてください」のメッセージが出ること。pptxgenjsで生成しようとしないこと。

---

## よくある落とし穴と対策

### 1\. Claudeがテンプレートを見つけられずゼロから作ってしまう

最も頻出する問題。テンプレートファイルのパスが合っていない場合に発生する。

**対策：**

- SKILL.mdの **冒頭・Step 4・テンプレート探索セクション** の計3箇所以上で「pptxgenjs禁止」を明記する
- /mnt/user-data/uploads/ へのフォールバックを入れる（ユーザーがチャットにPPTXを添付した場合に対応）
- 「なぜゼロから作成してはならないか」の理由も書く（Claudeが判断を迷わないように）

### 2\. slide\_fileが実際のXMLファイル名と不一致

**対策：** テンプレートをアンパックして実際のファイル名を確認する

```cpp
python /mnt/skills/public/pptx/scripts/office/unpack.py template.pptx unpacked/
ls unpacked/ppt/slides/
```

### 3\. テキスト編集でデザインが崩れる

**対策：**

- str\_replaceツールでテキスト部分だけを差し替える（XMLタグは変更しない）
- テキスト量は元のスライドと同程度に調整する
- QAで必ずPDF変換して見た目を確認する

### 4\. 日本語テキストが文字化けする

**対策：** XMLの <a:rPr> に lang="ja-JP" が設定されていることを確認

### 5\. カタログが大きすぎてClaudeが混乱する

**対策：**

- 50ページ以上の場合、カテゴリを細かく分ける
- use\_when の説明を具体的に書く（曖昧だとClaudeが誤選択する）
- プリセットを充実させる（カスタム選択の判断をClaudeに任せすぎない）

---

## 作成を依頼するプロンプト（コピペ用）

以下のプロンプトをClaudeに送り、PPTXファイルを添付すれば、スキル一式を作ってもらえる。

```cpp
添付のPPTXファイルは弊社のテンプレートです。
これをもとに、スライドジェネレータースキルを作成してください。

スキルの要件：
- テンプレートPPTXからスライドを選択・構成してPPTXを生成する
- ユーザーの要望（対象・目的・時間）に応じてスライド構成を提案する
- テキストの差し替えに対応する
- テンプレートが見つからない場合はpptxgenjsでゼロから作成せず、
  アップロードを依頼するようにする

以下のファイルを作成してください：
1. SKILL.md（スキル定義・ワークフロー）
2. slide-catalog.json（全スライドのカタログ＋プリセット構成）
3. scripts/generate.py（スライド選択ヘルパー）
4. template/ にテンプレートPPTXを配置

プリセット構成として以下のパターンを想定しています：
- フル紹介（30分）: {説明}
- ショートピッチ（15分）: {説明}
- {パターン名}: {説明}

最後にテスト生成を実行して、PPTXが正しく出力されることを確認してください。
```

---

## チェックリスト

スキル完成時に確認すべき項目：

- \[ \] テンプレートPPTXが template/ に配置されている
- \[ \] slide-catalog.json に全スライドが登録されている
- \[ \] 各スライドの slide\_file が実際のXMLファイル名と一致している
- \[ \] プリセット構成が2つ以上定義されている
- \[ \] SKILL.md に「pptxgenjs禁止」が3箇所以上明記されている
- \[ \] SKILL.md にテンプレート探索の優先順位が記載されている
- \[ \] SKILL.md に uploads/ フォールバックが記載されている
- \[ \] generate.py のカタログ探索パスが正しい
- \[ \] テスト生成でPPTXが正常に出力される
- \[ \] テスト生成でデザインが崩れていない
- \[ \] テキスト差し替えが正しく動作する
- \[ \] テンプレート未配置時に適切なエラーメッセージが出る

成果物はzipファイルで出力しなさい。

  

スライド作成を自動化するClaude「skills」の作り方｜Taro Segawa