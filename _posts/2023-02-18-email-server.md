---
title: メールサーバのアップデート
---

### docker-mailserver と Postfix

自分のドメインのメールサーバには、以前から [docker-mailserver](https://github.com/docker-mailserver/docker-mailserver) を使っている。
これはメールのいろんな設定を全部自動でやってくれる神のような Docker コンテナだ。
ぼくは昔は qmail を使っていたので、`toru-xxx@torus.jp` というふうにメールアドレスのデリミタにダッシュを使っていた。
Gmail だとこれがプラス記号（`+`）しか使えないので、仕方なく自分のサーバで Postfix を使い続けていた。

Postfix だけなら大したことはないけど、最近の e メールは経路暗号化やドメイン署名とかの仕組みが導入されて昔よりも遥かに複雑になった。
これらをすべて理解して設定するのは大変だけど、docker-mailserver を使うとかなり簡単にできるようになる。

### Gmail へ転送するときの問題

ぼくのアドレスにメールが届くと、それらはすべて Gmail に転送するように設定している。
これは Postfix の仮想アドレスの仕組みを使うだけで実現できる。
しかしスパムや詐欺メールも多く届くので、Gmail のサーバがぼくのメールサーバをスパムの送信元としてみなすようになってしまった。
しかも、本物のスパム（？）の多くは正常に Gmail に転送される一方、スパムでない正常なメール（多くの場合は個人宛の重要なメール）が Gmail のサーバに弾かれてしまう。

Gmail は転送を拒否するときに下のようなメッセージを残す：

> 550-5.7.1 [139.162.180.121      12] Our system has detected that this message is 550-5.7.1 likely unsolicited mail
> To reduce the amount of spam sent to Gmail, 550-5.7.1 this message has been blocked.
> Please visit 550-5.7.1  https://support.google.com/mail/?p=UnsolicitedMessageError 550 5.7.1  for more information.

じつは以前からこのメッセージはたびたび受け取っていたけど、これまで放置していた。
でもさすがに、放置し続けるとぼくのドメインの信用も落ちてしまうので、対策することにした。

### 対策

[Best practices for forwarding email to Gmail - Gmail Help](https://support.google.com/mail/answer/175365)
の内容を参考に次のような対策を施した：

- envelope sender の設定
- SPF の設定
- DKIM の設定

### envelope sender

envelope sender の設定は Postfix で簡単にできる。
方法は次の Stack Exchange の回答に従った：
[linux - How do I change the Envelope From in Postfix? - Server Fault](https://serverfault.com/questions/533912/how-do-i-change-the-envelope-from-in-postfix/584649#584649)
ただ、設定を Postfix の main.cf に書き込むためには、docker-mailserver が決めた方法でテキストファイルを配置する必要がある。

まず docker-data/dms/config/postfix-canonical というファイルを作成して次の 1 行を書き込む。

```
/./ envelope-sender@torus.jp
```

このファイルは Docker コンテナの中では /tmp/docker-mailserver/ に配置されるので、このパスを参照するように docker-data/dms/config/postfix-main.cf に次のような項目を追加する：

```
canonical_maps = regexp:/tmp/docker-mailserver/postfix-canonical
canonical_classes = envelope_sender
```

これでメールを転送するときに Postfix が envelope sender を設定するようになる。

### バーチャルアドレスの設定

メールの転送の際に Gmail から弾かれてバウンスすると、エラーメールが作られてさらに Gmail に転送しようとしてバウンスするというループに陥ることがあるようだった。
そこで、管理者アドレス宛のメールは別のアドレスに転送することにした。
この設定は docker-data/dms/config/postfix-virtual.cf に記述する。

```
envelope-sender@torus.jp xxxxx@me.com
postmaster@torus.jp xxxxx@me.com
toru@torus.jp xxxxx@gmail.com
```

このように管理者アドレス宛のメールは iCloud へ、個人アドレス宛のメールは Gmail へ転送するようにした。


### docker-mailserver のアップデート

次に DKIM を設定しようとしたけど、いいかげんいまのバージョンは古すぎるかと思ったので最新版に更新することにした。
`git fetch` したあと、どきどきしながら `git rebase v11.3.1` を実行してみると、何事もなかったようにアップデートできた。
さらにおそるおそる docker-compose を再起動してみたけど、全く問題なく動作していた。
すばらしい。

### DKIM

DKIM の設定は docker-mailserver に含まれる setup.sh を使うだけだった。（cf. [Best Practices \| DKIM - Docker Mailserver](https://docker-mailserver.github.io/docker-mailserver/v11.3/config/best-practices/dkim/)）

```
$ ./setup.sh config dkim
```

この後にコンテナを再起動すると DNS レコードに書き込むためのテキストが所定のテキストファイルに出力される。

ぼくは Google Domains を使っているので、その DNS の設定で `mail._domainkey` というホスト名の TXT レコードを作成し、
`"v=DKIM1; h=sha256; k=rsa; "` で始まるテキストを設定した。
設定は即座に反映されるのでオンラインのチェッカーですぐに確認できた。
ぼくはこのサイトのチェッカーを使った：[DKIM Check- DomainKeys Identified Mail (DKIM) Record Lookup - MxToolBox](https://mxtoolbox.com/dkim.aspx)

### 最終確認

すでに Gmail から独自ドメインを送信元とする設定はしていたので、試しにぼくが使っている他のアドレスにメールを送ってみたところ、無事に下のように SPF と DKIM が確認できた。

![image](https://user-images.githubusercontent.com/65044/219829237-9c5bd6b7-9b78-4cff-b723-332d1688a7db.png)

これでぼくのメールシステムも現代的になったと思う。
