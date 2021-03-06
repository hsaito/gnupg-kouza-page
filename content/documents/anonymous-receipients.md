+++
title = "受信者秘匿機能の利用"
slug = "anonymous-recipients"
categories = [
  "機能解説",
]
+++

## 受信者秘匿とは？

受信者秘匿機能は暗号化処理を行なう際に暗号化対象者の情報を匿名化し、暗号の宛先を読みとれないようにする処理です。

例えば他人に対する暗号を復号しようとすると以下のような表示になります。

    gpg: encrypted with 1024-bit RSA key, ID D69E7A73, created 2013-07-26
        "Test Key (Not for deployment) <test@example.com>"
    gpg: decryption failed: No secret key

上記はその暗号の対象者の公開鍵を持っていて、秘密鍵を持っていない場合の表示ですが、このように複合ができなくとも、そのメッセージが誰に向けて送られたのか、という情報が含まれることになります。

公開鍵がない場合は上記のように名前こそは表示されませんが、それでもメッセージの頻度などからある程度推測が可能な場合もあります。

受信者秘匿を行なうと、上記の代りに以下のような表示になります。

    gpg: anonymous recipient; trying secret key xxxxxxxx ...
    gpg: anonymous recipient; trying secret key xxxxxxxx ...

    gpg: encrypted with RSA key, ID 00000000
    gpg: decryption failed: No secret key

これは受信者に関する情報が暗号に含まれていないため、手持ちの鍵で試行するという形になります。

普通の暗号が名前の書いてある鍵付きのロッカーだとすると、受信者秘匿暗号は無記名のロッカーであると言えます。誰のロッカーか分からないので、手持ちの鍵で開くか試すまで自分が開けるのに必要な鍵を持っているかすら分かりません。

## なぜ秘匿するのか？

昨今のNSAなどのスキャンダルから、諜報機関は主にメタデータを取得していることが明らかになってきました。メタデータは通信の内容ではなく、その通信が誰に向けて宛てられているのかなどの情報を含みます。

特に機密を要する情報などに関しては暗号の中身はもちろん、そのメタデータも保護するのが必要になってきます。

# GnuPGでの使用法

GnuPGでは、受信者指定の際に「r」オプションを使用する変わりに「R」を使用することにより実現できます。つまり、以下の違いです。

通常の場合は

    gpg -r D69E7A73 -e hoge.txt

受信者秘匿の場合は

    gpg -R D69E7A73 -e hoge.txt

このオプションは組み合わせて使うことも可能です。

    gpg -r D69E7A73 -R E23E7A34 -e hoge.txt

throw-keyidオプションを使用することで、これを強制することも可能です。

    gpg --throw-keyid -r D69E7A73 -e hoge.txt

上記の場合は、通常の「r」オプションが使用されていますが、「throw-keyid」が指定されているので、秘匿されます。

## セキュリティ面での注意点

### 配布方法による分析

この方法で秘匿することにより、暗号自体の宛先の秘匿はできますが、それをメールなどで送信することにより、その送信事実はメタデータとして記録されます。[^1]対策としては以下のようなものが考えられます。

#### 同報の利用

暗号を使用する通信はメーリングリストなど、同報を通じて行ない、暗号を受けとる可能性のある人物を加入しておきます。受信者は自分宛、もしくはそのグループの他人宛のメッセージの両方を受けとり、それぞれ、受信時に各々の環境で復号を試行します。
通信量は増えますが、外部から誰に向けて宛てられたのかの分析が飛躍的に難しくなります。

### ダミー受信者の使用

予め、鍵を生成した上で、秘密鍵のみを破棄した鍵をいくつか作成しておき、暗号時に、それらの鍵に対しても秘匿暗号化を行います。こうすることによる狙いは暗号が宛てられている人数を秘匿することです。また、これを応用することにより、宛先が誰でもないメッセージを流すことにより、どのようなタイミングで通信が行なわれているかなどの把握を外部から行われるのを防止する効果があります。

## 制限事項など

### PGPとの非互換

GnuPGでは長らく対応されていたこの機能ですが、PGPでは対応していません。[^2]

### MUIとの非互換

Enigmailなどではサポートされません。

# 最後に

このように秘匿暗号化を使用することにより、通信内容面以外に、そのメタデータも秘匿することが可能になります。通信傍受の仕組みなどの情報が明らかになるにつれ、メタデータの秘匿はこれから大きなテーマになってくるかと思います。

現在は制限事項などのため、日常でメールなどに使用することは難しいかもしれませんが、工夫して利用することにより、強力な通信手法になるかと思います。

[^1]: これをトラフィック分析といいます
[^2]: 尚、Mac版においてはPGPでも動作するのを確認しています。但し復号のみ
