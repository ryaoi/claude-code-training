# training-sample

Claude Code 研修用の最小 HTML/CSS サンプル。
ビルド不要、ブラウザで `index.html` を開くだけで動きます。

## 構成

```
sample-project/
├── index.html              # コンポーネント集デモページ
└── css/
    ├── reset.css           # 最小リセット
    ├── tokens.css          # デザイントークン (色・余白・角丸など)
    └── components.css      # コンポーネントの実装 (BEM)
```

## 起動方法

```bash
# macOS
open index.html

# または任意の簡易サーバ
python3 -m http.server 8000
# → http://localhost:8000
```

## 既存コンポーネント

- **Button** (`.btn`, `.btn--primary`, `.btn--secondary`)
- **Card** (`.card`, `.card__title`, `.card__body`)

## 研修中の使い方

- **演習1**: `tokens.css` の色を変えて `/commit` でコミット
- **演習2**: CLAUDE.md を作って、未実装の **Tag** コンポーネントを Claude に追加させる
- **演習3**: 変更内容から PR 説明文を Skill で生成
