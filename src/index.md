# Hello, Netlify!

Netlify 存在は知っていたがこれまで試してもみていなかった。少し興味が出てきたので試してみる。

いろいろな機能があるみたいで頭がパーンしそうだが、静的サイトのホスティングのさわりをやってみる。CLI ツール入れてデプロイコマンドを叩くだけで OK みたいなかんじでできるっぽいので、それをやりたい。


以下を参考に進める。

- https://docs.netlify.com/cli/get-started/
- https://docs.netlify.com/cli/get-started/#manual-deploys

チュートリアルないかと数分探してみたけど CLI でどーんとやるみたいなのが見つからなかった。

Netlify のブログにいろいろチュートリアルはあるっぽい。

https://www.netlify.com/tags/tutorial/

## サインアップ

GitHub のアカウントでやった。

## CLI ツールのインストール

```
$ yarn add netlify-cli -D
```

https://docs.netlify.com/cli/get-started/#installation ではグローバルにインストールするようになっているが、今回はローカルにインストールした。

こういう CLI ツールって Heroku とか Firebase にもあって、たいていドキュメントにはグローバルにインストールするかんじになっているけれど、どうすればよいのか迷う。時と場合によるんだろうが。

Homebrew にもありそうだと思って brew search netlify してみたら netlify-cli があって、これでもインストールできそうだった。

## デプロイ

```
-> yarn netlify deploy -d dist --prod
yarn run v1.22.4
$ /Users/tfrkd/tmp/netlify/hello_netlify/node_modules/.bin/netlify deploy -d dist --prod
Logging into your Netlify account...
Opening https://app.netlify.com/authorize?response_type=ticket&ticket=0115cbde8b5a3c871a3866d748a70055

You are now logged into your Netlify account!

Run netlify status for account details

To see all available commands run: netlify help

This folder isn't linked to a site yet
? What would you like to do? +  Create & configure a new site
? Team: furu's team
Choose a unique site name (e.g. super-cool-site-by-furu.netlify.app) or leave it blank for a random name. You can update the site name later.
? Site name (optional): undefined

Site Created

Admin URL: https://app.netlify.com/sites/festive-dubinsky-8216ec
URL:       https://festive-dubinsky-8216ec.netlify.app
Site ID:   09b5fa26-87c9-410b-b48b-49ed4fd52fe5
Deploy path: /Users/tfrkd/tmp/netlify/hello_netlify/dist
Deploying to main site URL...
✔ Finished hashing 1 files
✔ CDN requesting 0 files
✔ Finished uploading 0 assets
✔ Deploy is live!

Logs:              https://app.netlify.com/sites/festive-dubinsky-8216ec/deploys/5ece4c2402a1c65c3661cb8b
Unique Deploy URL: https://5ece4c2402a1c65c3661cb8b--festive-dubinsky-8216ec.netlify.app
Website URL:       https://festive-dubinsky-8216ec.netlify.app
✨  Done in 153.92s.
```

デプロイする前に `netlify login` が必要かと思ったが `netlify deploy` だけでうまいことやってくれる。

## サイトをブラウザで開く

```
$ yarn netlify open:site
```

## サイトの削除

```
-> yarn netlify sites:delete 09b5fa26-87c9-410b-b48b-49ed4fd52fe5
yarn run v1.22.4
$ /Users/tfrkd/tmp/netlify/hello_netlify/node_modules/.bin/netlify sites:delete 09b5fa26-87c9-410b-b48b-49ed4fd52fe5
Warning: You are about to permanently delete "festive-dubinsky-8216ec"
         Verify this siteID "09b5fa26-87c9-410b-b48b-49ed4fd52fe5" supplied is correct and proceed.
         To skip this prompt, pass a --force flag to the delete command

Be careful here. There is no undo!

? WARNING: Are you sure you want to delete the "festive-dubinsky-8216ec" site? Yes

Deleting site "09b5fa26-87c9-410b-b48b-49ed4fd52fe5"...
Site "09b5fa26-87c9-410b-b48b-49ed4fd52fe5" successfully deleted!
✨  Done in 17.41s.
```

削除したサイトにアクセスしてみると 404 Not Found になった。すぐ反映された。

```
-> http https://festive-dubinsky-8216ec.netlify.app/
HTTP/1.1 404 Not Found
Age: 1
Cache-Control: no-cache
Connection: keep-alive
Content-Length: 9
Content-Type: text/plain; charset=utf-8
Date: Wed, 27 May 2020 12:03:33 GMT
Server: Netlify
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: ALLOWALL
X-NF-Request-ID: f40fdf92-acdc-42db-805a-bcd47b36802d-11773196
X-Request-Id: 38f7e71b-24ec-4b67-8d8f-e9a61a48b06c
X-Runtime: 0.003125

Not Found
```

## 感想

サインアップして CLI ツールインストールしてデプロイコマンド叩くだけで静的サイトホスティングできてお手軽っぽい。まあ、他の似たようなサービスもそうなのかもしれんが。

https://tfrkd.org/ はさくらの VPS で動かしているのだけれど、Let's Encrypt の証明書がうまく更新されておらず、それが長年放置されており最悪になっている。そして VPS 自体、使っていなさすぎるのでこういう何にもしなくても動き続けてくれるところに引越したい気持ちがある。

Basic 認証するには Pro プラン以上が必要で月45ドル必要か。
