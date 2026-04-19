# Claude Code 1時間ハンズオン研修

Claude Code を初めて使う**コーダー（HTML/CSS 中心）向け**の、60分ハンズオンワークショップ教材。

3つの基礎機能（**Slash Commands** / **CLAUDE.md** / **Skills**）を、サンプルプロジェクトを触りながら習得します。

---

## 事前準備（受講者向け）

### 1. Claude Code のインストール

公式手順: https://docs.claude.com/en/docs/claude-code/quickstart

```bash
# 例（npm 経由）
npm install -g @anthropic-ai/claude-code

# 動作確認
claude --version
```

### 2. このリポジトリの取得とブラウザ確認

```bash
git clone <このリポジトリの URL> claude-code-training
cd claude-code-training/sample-project
open index.html        # macOS の場合
```

ブラウザで「UI コンポーネント集」のページが開き、Button と Card が表示されれば準備完了。

> ビルドツールも npm install も不要です。HTML/CSS のみで動きます。
>
> **git に詳しくなくて OK**: 当日は `git clone` 以外の git コマンドは使いません。clone でつまずいたら講師にお声がけください。

---

## 当日の流れ（60分）

| 時間 | セクション | 資料 |
|------|------------|------|
| 0:00 – 0:05 | 環境確認 | この README |
| 0:05 – 0:10 | 全体像説明 | [slides/intro.md](slides/intro.md) |
| 0:10 – 0:25 | 演習1: Slash Commands | [exercises/01-slash-commands.md](exercises/01-slash-commands.md) |
| 0:25 – 0:42 | 演習2: CLAUDE.md | [exercises/02-claude-md.md](exercises/02-claude-md.md) |
| 0:42 – 0:57 | 演習3: Skills | [exercises/03-skills.md](exercises/03-skills.md) |
| 0:57 – 1:00 | まとめ・Q&A | — |

---

## ディレクトリ構成

```
claude-code-training/
├── README.md                 # このファイル
├── slides/intro.md           # オープニング用スライド (Marp)
├── exercises/
│   ├── 01-slash-commands.md
│   ├── 02-claude-md.md
│   └── 03-skills.md
└── sample-project/           # 演習で触る最小 HTML/CSS プロジェクト
    ├── index.html
    └── css/
        ├── reset.css
        ├── tokens.css        # デザイントークン
        └── components.css    # BEM コンポーネント
```

---

## ゴール

研修終了後、受講者は以下ができる状態になります:

- [ ] 自分の定型作業を Slash Command として定義できる
- [ ] CLAUDE.md にプロジェクトの前提を書いて、Claude の振る舞いを揃えられる
- [ ] Skill を作って、自然文の依頼から自動発動させられる
- [ ] 3機能を**目的別に使い分け**られる
