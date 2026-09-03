# shunchobi.github.io

`https://shunchobi.github.io/` のルートで配信するページ。中身は **app-ads.txt** 1 本と、
ルートを 404 にしないための最小の index.html だけ。

公開先: <https://shunchobi.github.io/>

> このフォルダは Unity プロジェクトのリポジトリの中にあるが、**別のリポジトリ**である。
> 親リポジトリ側では `.gitignore` で `/shunchobi.github.io/` を除外しているため、
> Unity 側のコミットには入らない。`site/` と同じ作り。

## なぜこのリポジトリが要るのか

AdMob は広告枠の販売者を確認するために、App Store / Google Play の掲載情報にある
デベロッパーの Web サイトの **ドメインのルート** に `app-ads.txt` を探しに行く。

App Store に登録しているデベロッパーの Web サイトは
`https://shunchobi.github.io/solitaire-world-tour-site/index.html` なので、
AdMob が見に行くのは `https://shunchobi.github.io/app-ads.txt` になる。

ところが公開サイトのリポジトリ `shunchobi/solitaire-world-tour-site` は GitHub Pages の
**プロジェクトサイト**で、`/solitaire-world-tour-site/` というサブパスで配信される。
あちらに `app-ads.txt` を置いても
`https://shunchobi.github.io/solitaire-world-tour-site/app-ads.txt` にしかならず、
AdMob はそこを見ない。実際 AdMob の管理画面では「アプリを確認できませんでした」になった。

GitHub Pages がルートで配信するのは、リポジトリ名が `<ユーザー名>.github.io` の
**ユーザーサイト**だけ。そのためにこのリポジトリを作った。
プロジェクトサイトとユーザーサイトは共存するので、`solitaire-world-tour-site` は
これまでどおり動く。

なお `app-ads.txt` は必須ではない。無くても広告は配信されるが、認可した販売経路からしか
買わない広告主の需要が届かなくなるぶん収益が下がる。

## 中身

```
app-ads.txt   AdMob のパブリッシャー ID 1 行。iOS / Android の両方をこれ 1 本で兼ねる
index.html    ルートを 404 にしないための案内。公開サイトへのリンクだけ
.nojekyll     Jekyll のビルドを走らせない
```

`app-ads.txt` は IAB Tech Lab の仕様に沿った書式で、1 行が
`<広告システムのドメイン>, <パブリッシャー ID>, <関係の種別>, <認証局 ID>` を表す。
パブリッシャー ID `pub-8709392240032722` は AdMob アカウントに紐づく値なので、
**AdMob のアカウントを変えない限り書き換えない**。値は AdMob の
「アプリの設定」→ app-ads.txt の設定手順に表示されるものを正とする。

## 公開

GitHub Pages の設定は Settings → Pages → Source: **Deploy from a branch** /
Branch: `main` / フォルダ: `/ (root)`。ユーザーサイトのリポジトリは既定のブランチから
自動で公開されるが、Pages の画面に出ていなければここで指定する。

```bash
git add -A && git commit -m "..." && git push
```

反映まで 1〜3 分。Actions タブの `pages build and deployment` の成功が本当の合図。

## 変更したあとにやること

1. <https://shunchobi.github.io/app-ads.txt> をブラウザで開き、HTML ではなく
   テキストが 1 行返ることを確認する
2. AdMob →「アプリ」→ 対象アプリ →「アプリの設定」→ app-ads.txt の欄で
   **「アップデートを確認」** を押す
3. AdMob のクロールは数分で終わることが多いが、24 時間かかる場合もある

## 参考

- [app-ads.txt ファイルについて](https://support.google.com/admob/answer/9787936?hl=ja)
- [app-ads.txt に関するよくある質問](https://support.google.com/admob/answer/9675354?hl=ja)
- [app-ads.txt に関する問題を解決する](https://support.google.com/admob/answer/9776740?hl=ja)
