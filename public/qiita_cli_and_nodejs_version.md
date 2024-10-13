---
title: "Node.jsのバージョンが低すぎてQiita CLIでエラー出した件"
tags:
  - 'Qiita CLI'
private: false
updated_at: '2024/10/13'
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
# Qiita CLI を使う前に Node.js のバージョンを確認しよう

PM試験の記事を書こーと思ってQiita見たら[Qiita CLI](https://qiita.com/Qiita/items/32c79014509987541130)というのがあるじゃないの、これは便利、ということで諸々設定して使おうとしたら、

```bash
npx qiita login
(中略)
Qiita APIへのリクエストでネットワークエラーが発生しました
  インターネットに接続されているかご確認ください
```

えええ？？トークンが払い出せてるというかQiitaが見られているってことはインターネットは接続できてるってはずだけど？と思いながらChatGPT 4oにエラーメッセージぺたーで相談。

「node-fetchインストールしましたか？」と訊かれたのでとりあえずインストール。エラーメッセージ変わらず。

IssueやDiscussionを見ても特にこのエラーメッセージが生えた人は居ないということはおそらくパッケージではなくおま環問題と判断。

Node.jsとか知らんしこれはもう物理 (普通にプラットフォーム上で) で書くしか無いか... と思い、ふと[README](https://github.com/increments/qiita-cli?tab=readme-ov-file#1-%E4%BA%8B%E5%89%8D%E6%BA%96%E5%82%99)を見て気づきました。

**Qiita CLI を使うには Node.js 18.18.0 以上が必要です。**

たーぶんこれじゃないか？そもそもいつの間にか`npm`とか使えるようになってるけど最後にインストールした経緯覚えてないくらいだしこれはアプデもしてませんわ、と思ってChatGPTにNode.jsのバージョン確認方法を訊いて実行。

```bash
node --version
v17.9.0
```

全然足りてなかった！！ということでバージョンアップの方法もChatGPTにご相談。

```bash
nvm install --lts
```

```bash
Installing latest LTS version.
Downloading and installing node v20.18.0...
Downloading https://nodejs.org/dist/v20.18.0/node-v20.18.0-darwin-arm64.tar.xz...
############################################################################## 100.0%
Computing checksum with shasum -a 256
Checksums matched!
Now using node v20.18.0 (npm v10.8.2)
```

もう一度！

```bash
npx qiita login
(中略)
Hi Daku-on!

ログインが完了しました 🎉
以下のコマンドを使って執筆を始めましょう！
```

よっしゃぁ！

ということでこの記事のpublishに至るわけです。ちゃんちゃん。
