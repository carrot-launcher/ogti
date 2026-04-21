# 4軸16タイプ診断フレームワーク

MBTI風の **4軸 × 16タイプ** 構造を持つジョーク診断を作るためのフレームワーク。ブラウザだけで動く静的サイト。

## カスタマイズ

フォーク後に編集するファイルは **`data/` 配下の3つ** だけ:

| ファイル | 内容 |
|---|---|
| `data/config.js` | テーマ/配色 / ブランド / 4軸 / グループ / 結果セクション / 利用規約情報 |
| `data/questions.js` | 設問と回答 |
| `data/types.js` | 16タイプそれぞれの名前・タグライン・強み/癖/相方 |

軸の数 (4)、タイプ数 (16)、採点ロジック、画面デザインはフレームワーク側で固定。

### テーマ / 配色

見た目は **テーマ (構造) × パレット (UI配色) × グループ色 (結果の意味色・固定) の3レイヤー** で構成。

```js
// data/config.js
theme:   'neon',       // 構造レイヤー: フォント・角丸など (色なし)
palette: 'random',     // UI配色: 'red-blue' 等固定 / 'random' / ['matrix','sunset']
```

`palette: 'random'` にするとロードごとに `app.js` の `KNOWN_PALETTES` からランダムに選ばれます。

**グループ色 (結果の意味色)** は UI パレットとは独立に `styles.css` の `:root` 直下に固定で置かれています。「熱血派 / 狂騒派 / 幽玄派 / 正統派」の4色はロードごとに変わらないので、診断結果の意味が保たれます。

プリセットの実体は `styles.css` 冒頭の `:root[data-theme="..."]` / `:root[data-palette="..."]` ブロック。パレット追加時は `app.js` の `KNOWN_PALETTES` にも名前を足してください。

同梱プリセット:

| kind | name | 内容 |
|---|---|---|
| theme | `neon` | Rampart One / RocknRoll One / Zen Maru Gothic の3書体、角丸16/24px |
| palette | `red-blue` | 赤×シアン×金 (デフォルト) |
| palette | `lime-magenta` | 黄緑×マゼンタ |
| palette | `matrix` | 映画 The Matrix 風、全面緑 |
| palette | `sunset` | 夕焼けのオレンジ×マゼンタ×金 |
| palette | `ice` | 氷の洞窟、白×青×シアン |
| palette | `blood-moon` | 血月、深赤×オレンジ×琥珀 |
| palette | `vaporwave` | 80年代ポップ、ピンク×シアン×紫 |
| palette | `hacker` | 旧式CRTターミナルの琥珀 |
| palette | `miami` | Miami Vice 80s、ホットピンク×ターコイズ |
| palette | `aurora` | オーロラ、紫×緑×青 |
| palette | `arcade` | アーケードゲーム、マゼンタ×シアン×イエロー |
| palette | `lava` | 溶岩、赤×オレンジ×黄 |
| palette | `deep-sea` | 深海、ターコイズ×深青 |
| palette | `halloween` | ハロウィン、オレンジ×紫×妖緑 |

組み合わせは自由ですが、全組み合わせが映えるとは限りません (例: 低彩度パレットはneonの発光と相性が悪い)。

### 設問数のルール

- 各軸の設問数は **奇数** にしてください (例: 3 / 5 / 7 問)
- 採点値 ±3/±5/±7 (奇数) との組合せで、引き分けが数学的に発生しません
- 軸ごとに数が違っても OK (軸1=7問、軸2=5問... など)
- 偶数の軸があると起動時にコンソール警告が出ます

## ローカル実行

ES modules を使うため `file://` では動きません。HTTPサーバを立ててブラウザで開いてください。

```bash
python -m http.server 8000   # Python 3
npx serve                    # Node.js
```

VS Code の **Live Server** 拡張でも可。

## デプロイ

GitHub Pages にそのまま push して配信可能。ビルドステップなし。

## ライセンス

[CC BY-NC-ND 4.0](./LICENSE) / [利用規約](./terms.html)

非商用・改変なしでの共有は歓迎。商用利用・改変しての再配布は禁止。
