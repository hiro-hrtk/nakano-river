# 中野区 大雨・洪水ウォッチ

今夜〜明日の大雨に備えるための、非公式の1ページ防災サイト。

- **上部：全国の大雨・洪水掲示板** — 気象庁の集約データ（`bosai/warning/data/r8/map.json`）を
  ブラウザから直接取得し、各地域の最新発表を「電光掲示板（横スクロール）＋自動スクロールの一覧」で表示。
  大雨（特別警報・警報・注意報）と洪水（警報・注意報）のみ対象。約5分ごとに自動更新。
- **下部：中野区の河川ライブ映像** — 東京都建設局「東京都水防チャンネル」（YouTube）の
  河川監視カメラを、神田川・妙正寺川・江古田川ごとにまとめて埋め込み（タップで再生）。
- スマホ表示に対応。

すべてクライアントサイド（静的HTML＋JS）で動くので、**GitHub Pages にそのまま置けます**。

---

## GitHub Pages で公開する手順

### 1. リポジトリを用意してプッシュ

```bash
cd /Users/daniel/Documents/ClaudePJT/nakano-river

git init
git add .
git commit -m "中野区 大雨・洪水ウォッチ 初版"

# GitHub 上で空のリポジトリ（例: nakano-river）を作成してから：
git branch -M main
git remote add origin https://github.com/<あなたのユーザー名>/nakano-river.git
git push -u origin main
```

> `gh` CLI があれば `gh repo create nakano-river --public --source=. --push` の1行でOK。

### 2. Pages を有効化

GitHub のリポジトリページで **Settings → Pages** を開く：

- **Source**: `Deploy from a branch`
- **Branch**: `main` / `/ (root)` → **Save**

1〜2分ほどで次のURLに公開されます：

```
https://<あなたのユーザー名>.github.io/nakano-river/
```

### 3. 更新のしかた

`index.html` を編集して `git commit` → `git push` するだけ。数十秒で反映されます。

---

## 動作メモ / 注意

- **公式サイトではありません。** 避難の判断は、気象庁「キキクル」や中野区の避難情報など
  **公式発表と自治体の指示に必ず従ってください。**
- 気象データは気象庁の公開JSON（`www.jma.go.jp/bosai/`、CORS許可済み）を利用。
  仕様は予告なく変わることがあり、その場合は掲示板の表示が止まります（映像は影響を受けません）。
- 河川カメラ映像の著作権・利用条件は東京都建設局「東京都水防チャンネル」に従います。
- ローカル確認は `index.html` をブラウザで直接開くだけでOK（サーバー不要）。
  ※一部ブラウザは `file://` だと外部取得を制限することがあります。その場合は
  `python3 -m http.server` などで簡易サーバーを立ててください。

## カスタマイズ

- **カメラ地点の増減**: `index.html` 内の `var CAMS = [...]` を編集。
  地点のYouTube動画IDは「東京都水防チャンネル」<https://www.youtube.com/@TokyoSuibou/streams> から取得できます。
- **掲示板で拾う警報の種類**: `var KIND = {...}` にコードを追加（例：高潮などを足す場合）。
- **更新間隔**: 末尾の `5 * 60 * 1000`（ミリ秒）を変更。

## データ出典

- 気象庁 防災情報（気象警報・注意報） <https://www.jma.go.jp/bosai/warning/>
- 東京都 水防災総合情報システム <https://www.kasen-suibo.metro.tokyo.lg.jp/>
- 東京都水防チャンネル（YouTube） <https://www.youtube.com/@TokyoSuibou>
- NHKニュース RSS（主要 cat0 / 社会 cat1） <https://www.nhk.or.jp/toppage/rss/index.html>
- 中野区 河川カメラ・気象情報 <https://www.city.tokyo-nakano.lg.jp/bosai/suigai-sonae/uryo/nakanokukasen.html>
