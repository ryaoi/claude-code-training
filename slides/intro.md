---
marp: true
theme: default
paginate: true
header: "Claude Code 1時間ハンズオン"
---

# Claude Code 1時間ハンズオン

3つの基礎機能を手を動かして覚える

<!-- 自己紹介と「今日は60分で3機能を完走します」を一言 -->

---

## 今日のゴール

「3つの基礎機能」を、実際に動かして理解する:

1. **Slash Commands** — 自分の作業をコマンド化
2. **CLAUDE.md** — プロジェクトの記憶を持たせる
3. **Skills** — 自然文から自動発動する能力

> 浅く広くではなく、**3つを深く触る**のが目的です。

---

## タイムテーブル

| 時間 | 内容 |
|------|------|
| 0:00 – 0:05 | 環境確認 |
| 0:05 – 0:10 | 全体像（このスライド） |
| 0:10 – 0:25 | 演習1: Slash Commands |
| 0:25 – 0:42 | 演習2: CLAUDE.md |
| 0:42 – 0:57 | 演習3: Skills |
| 0:57 – 1:00 | まとめ・Q&A |

---

## 環境確認（5分）

- [ ] `claude` コマンドが動く（`claude --version`）
- [ ] このリポジトリを `git clone` 済み
- [ ] ブラウザで `sample-project/index.html` が開ける
  - 「UI コンポーネント集」のページに Button と Card が見える
- [ ] エディタでプロジェクトが開けている

> 詰まったら手を上げてください。
> **git に詳しくなくて OK**: `git clone` 以外の git は使いません。

---

## Claude Code とは

- ターミナルで動く AI コーディングアシスタント
- ファイル読み書き・コマンド実行などをエージェント的に行う
- **設定ファイル（`.md`）でカスタマイズできる** ← 今日の主題

> 「賢いだけ」じゃなく「**自分仕様にできる**」のが Claude Code の価値。

<!-- 参考: https://code.claude.com/docs/en/quickstart -->
> 公式入門: https://code.claude.com/docs/en/quickstart

---

## プロンプトの基本

Claude Code はチャットボットではなく、**指示を受けて自律的に動くエージェント**。
依頼の書き方で結果が変わる。

### 3つの心得

1. **具体的に書く**
   - NG:「バグ直して」 / OK:「ログイン後にトークンが切れる症状を `src/auth/` あたりで直して」
2. **文脈を渡す**
   - 関係ファイル（`@<path>`）、スクリーンショット、期待する結果を一緒に渡す
3. **対話で詰める**
   - 一発で当てに行かない。違うと思ったら止めて方針修正

> `Esc` で中断、`Esc Esc` で巻き戻し、`/clear` で履歴リセット。**やり直せる**ので大胆に試そう。

> 公式: https://code.claude.com/docs/en/best-practices

---

## 入力の基本: 3つのプレフィックス

| 先頭文字 | 動作 | 例 |
|----------|------|-----|
| `/` | コマンド・Skill を呼び出す（補完あり） | `/clear` |
| `@` | **ファイル参照**（パス補完が出る、超便利） | `@css/tokens.css の役割は？` |
| `!` | シェルコマンドを直接実行 | `!ls css` |

> 「`@` を打つ → ファイルパスが補完される → Enter」で、Claude にファイルを正確に指せる。

> 公式: https://code.claude.com/docs/en/interactive-mode#quick-commands

---

## 覚えておきたいショートカット

| キー | 動作 |
|------|------|
| `Ctrl+C` | 入力 / 生成を中断 |
| `Esc Esc`（2回） | 直前の状態に巻き戻し |
| `Shift+Enter` | 改行（効かない端末では `\` + `Enter`） |
| `↑` / `↓` | コマンド履歴を辿る |
| `Ctrl+D` | セッション終了 |

> 詰まったら `Ctrl+C`、やり直したくなったら `Esc Esc`。この2つだけ覚えておけば安心。

> 公式（全ショートカット）: https://code.claude.com/docs/en/interactive-mode#keyboard-shortcuts

---

## まず覚えておきたい組み込みコマンド

| コマンド | 用途 |
|----------|------|
| `/help` | ヘルプ画面（ドキュメントリンク等） |
| `/clear` | 会話履歴をリセット（**今日たくさん使う**） |
| `/init` | プロジェクトを分析して `CLAUDE.md` の雛形を生成 |
| `/model` | 使うモデルを切り替え |

> 使えるコマンド一覧は **`/` だけ打つ** と補完候補で出る。試してみよう。

> 公式（全コマンド）: https://code.claude.com/docs/en/commands

---

## 今日の3機能（プレビュー）

| | Slash Command | CLAUDE.md | Skill |
|---|---|---|---|
| いつ動く | **手動**（`/name`） | **起動時に常時** | **自然文マッチで自動** |
| 配置 | `.claude/commands/<name>.md` | `<root>/CLAUDE.md` | `.claude/skills/<name>/SKILL.md` |
| 実体 | `.md` ファイル | `.md` ファイル | **ディレクトリ** |
| 用途 | 自分の定型作業 | プロジェクトの前提 | Claude にいつでも使ってほしい能力 |

> 詳細は各演習の冒頭で解説します。今は「3つあるんだ」だけで OK。

---

## 3機能の関係（1枚図）

```
                  あなたの依頼
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
  Slash Command   CLAUDE.md        Skill
  /explain        起動時に          description が
  と自分で打つ    自動ロード        マッチで自動発動
        │              │              │
        └──────── Claude が動く ──────┘
```

- **Slash Command**: 手動トリガー（自分が呼ぶ）
- **CLAUDE.md**: 常時ロード（前提知識）
- **Skill**: 自動トリガー（Claude が判断）

> 公式: Skills (Slash Commands も含む) https://code.claude.com/docs/en/skills / Memory https://code.claude.com/docs/en/memory

---

## 各演習の進め方

各演習は **「解説 5分 → ハンズオン 10分前後」** の構成:

1. **解説** — 機能の仕組み・書き方・コツを学ぶ
2. **ハンズオン** — 実際に `.md` ファイルを書いて動かす
3. **観察ポイント** — 何が起きたか確認する

> 詰まった時のチェックリストも各演習に付いています。

---

## 今日扱わないもの（名前だけ）

| 機能 | ざっくり何？ | 公式ドキュメント |
|------|-------------|-----------------|
| **Subagents** | 別コンテキストで動く専門エージェント | https://code.claude.com/docs/en/sub-agents |
| **MCP** | 外部ツール接続のプロトコル | https://code.claude.com/docs/en/mcp |
| **Hooks** | イベント駆動の自動化 | https://code.claude.com/docs/en/hooks |
| **Plugins** | 機能セットの配布単位 | https://code.claude.com/docs/en/plugins |

→ 全体目次: https://code.claude.com/docs

---

## では演習1へ

`exercises/01-slash-commands.md` を開いてください

> まず**解説セクション（5分）** を読んでから、ハンズオンに進みます。
