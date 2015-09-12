+++
title = "GnuPG Tips"
slug = "tips"
+++

## ＰＧＰで復号化しようとすると失敗する

**【本項目は最近のバージョンでは当てはまらない可能性があります。参考としてご参照ください。】**

Windows版ではGnuPGの場所を指定するレジストりキー（¥¥HKEY\_CURRENT\_USER¥Software¥GNU¥GnuPG¥HomeDir）に指定されているディレクトリ（指定が無い場合はc:¥gnupgになります）にoptionsというファイル（拡張子無し）を作成しforce-v3-sigsと表記します。UNIX版ではホームディレクトリ内に.gnupgというフォルダが作成されているので同様にその中のoptionsを変更します。こうするとＰＧＰ５，ＰＧＰ６系に対応するようになります。（ＰＧＰ２系はＲＳＡ／ＩＤＥＡを使用しているため非対応）。注意しなければならないのが最初に鍵を生成する際にこれをしておく必要があることです。尚、相手がGnuPGを使用しているのが分かっている場合は `--openpgp` オプションを実行時に追加することで対応できます。（GnuPGはどちらの場合も正常に復号化できます。）

## 受信者秘匿メッセージとは？

GnuPG同士の場合は受信者を秘匿することができます。（Anonymous Receipient機能）通常暗号化をすると相手の鍵ＩＤが鍵に含まれます。これにより復号化の際にどの鍵に向けて発信されているかを判断します。受信者を秘匿することにより、この情報を外してしまいます。これにより誰に向けて発信されているかという情報をメッセージが持たなくなります。これをするのには次のようにします。

    gpg -ea --throw-keyid filename.asc

このオプションを使うと復号化の際に全ての鍵に対して復号化を試みる為、処理が多少遅くなります。（複数の秘密鍵がある場合、全ての鍵に対して復号化できるまでパスワードを入力する必要があります。複数の受信者にお互いの情報を明かすことなく暗号化するなどの使い方がありますがＰＧＰ５，６との互換性がなくなるので注意してください。

詳しくは[受信者秘匿機能の利用](/documents/anonymous-recipients)もご覧ください。

### 1.4.x以上

-rの代わりに-Rを指定することにより-Rを指定したユーザーを選択的に設定することが可能になりました。

    gpg -ea -r 0xffffff -R 0xeeeeee

この場合、0xffffffに対しては普通に暗号化されますが、0xeeeeeeへの暗号化は秘匿されます。
throw-idを使用した場合は受信者全員が秘匿化されます。

### 注意

これを使用することにより、宛先のKey IDは秘匿されますが誰かにメッセージが宛てられているという事実を隠すことはできません。そのため、トラフィック分析などで宛先が判明してしまう場合はありますのであくまでも予備的な方法であることに注意してください。

## Windows版で復号化したファイルが読めない

UNIX版では問題ないものでWindows版では問題があるものとしてリダイレクタの使用があります。次のように復号していないでしょうか？

    gpg -d filename.asc > file

ファイルがバイナリファイルの場合はこれを使うと問題が起きます。次のように復号化するようにしてください。

    gpg -o file -d filename.asc

これで問題ないはずです。

## GnuPGの商業利用は問題なく可能か？

**【本項は参考情報として提供されています。法的な疑問等が有る場合は弁護士等に相談してください。】**

GnuPGは特許でカバーされているアルゴリズムを使用していないため商業利用は問題なく可能です。ちなみにGnuPGのライセンスであるGNU Public Licenseではソフトウェアの利用に関する項目はありませんので明示的に表明していないGnuPGの場合は自由に使用できます。

### 〜1.4.8 参考：GNU General Public License Section 0より抜粋


    Activities other than copying, distribution and modification are
    not covered by this License; they are outside its scope. The act of
    running the Program is not restricted, and the output from the Program
    is covered only if its contents constitute a work based on the Program
    (independent of having been made by running the Program). Whether that
    is true depends on what the Program
    does.

複製、頒布、変更以外の行為は本使用許諾の対象としません。それらは本使用許諾の範囲外です。「プログラム」を実行させる行為に関して制約はありません。「プログラム」の出力は、(「プログラム」を実行させて作成させたかどうかとは無関係に)
その内容が「プログラム生成物」である場合に限り本使用許諾の対象となります。これが当てはまるかどうかは、「プログラム」が何をするものかに依ります。
1.4.8〜 1.4.8からはGPLv3が適応されるため、以下の部分が適応されます。

### GNU General Public License v3, 2. Basic Permissionsより抜粋


    All rights granted under this License are granted for the term of copyright on
    the Program, and are irrevocable provided the stated conditions are
    met. This License explicitly affirms your unlimited permission to run
    the unmodified Program. The output from running a covered work is
    covered by this License only if the output, given its content,
    constitutes a covered work. This License acknowledges your rights of
    fair use or other equivalent, as provided by copyright
    law.

本許諾書の下で認められるすべての権利は、『プログラム』に主張される『コピーライト』の条項に基づき授与されるものであり、ここで述べられた条件が満たされている限り覆すことはできない。本許諾書は、改変されていない『プログラム』をあなたが無制限に実行することを許可し、明示的に確約する。『保護された作品』を実行することから得られた出力結果は、その出力内容が『保護された作品』を構成する場合のみ本許諾書で保護される。本許諾書は、あなたが有するフェアユースまたはその同等物の権利を、『コピーライト』法規によって提供される通りに承認する。

## 対称暗号化したファイルがＰＧＰで復号化できない（またはその逆）

**【本項目は最近のバージョンでは当てはまらない可能性があります。参考としてご参照ください。】**

ＰＧＰで複合化できるように対称暗号化（つまり-cオプションの暗号化）するのには–cipher-algo
CAST5の指定が必要です。つまり次のようにします。

    gpg --cipher-algo CAST5 -c filename.asc

上記の方法でもうまくいかない場合があるようです。現在検証中です。しばらくお待ち下さい。

ＰＧＰとＧＰＧが生成するパケットの違いを検証してみたところ、圧縮方式が違うことで起こる問題のようです。→技術情報

上の暗号化時のコマンドラインの代わりに次のように入力してください。

    gpg --cipher-algo CAST5 --compress-algo 1 -c filename.asc

これでも問題があるようでしたらご一報下さい。９月２０日にリリースされた１．０．３ではこれがデフォルトのオプションになっているようです。

## ＰＧＰで復号化したときにSecure Viewerで表示されるようにしたい

PGPには電磁波により文字を読み取るTEMPEST攻撃を避けるためのビュワーが入っていますが、GnuPGにはこの機能は入っていないため、一見、不可能なようですが実はこれをする方法があります。暗号化をするときに次のようにするとできます。

    gpg --cipher-algo CAST5 --compress-algo 1 --set-filename _CONSOLE -c filename.asc

実はSecure Viewerはファイル名が_CONSOLEという名前で設定されているだけなのでこれをset-filenameオプションで設定するとこれが簡単に実現できてしまいます。Secure Viewerでは日本語は化けてしまうので注意してください。

### 1.4.x以上

for-your-eyesオプションを使用してください。

    gpg --for-your-eyes-only -c filename.asc

## PGPから乗り換えたい

PGPから乗り換える場合は次のようにします。まず、PGPで秘密鍵と公開鍵をファイルに保存します。仮にkeys.ascという名前で保存したと仮定します。次にそのファイルをGnuPGで次のようにします。

    gpg --import keys.asc

これでGnuPGに秘密鍵と公開鍵が取り込まれます。これで乗り換えは完了です。尚、通常のバージョンのGnuPGではこの方法が使えるのはPGPがバージョン５以降の場合のみです。（IDEA/RSA形式のものは使用できません）

## Windows版でタイムゾーンがかみ合わない

**【本項目は最近のバージョンでは当てはまらない可能性があります。参考としてご参照ください。】**

現在のWindowsバージョンではローカル時間がGMTとして認識されてしまう問題が存在します。開発者によるとこの問題をWindows版では専用のコードを使用して回避する方向のようですのでしばらくお待ち下さい。

この問題はPGP側の「問題」のようです。PGP側でタイムゾーンの補正を二重にかけているようです。この問題はPGP同士では露見しないため今まで判明しなかったおそれがあります。現段階ではGnuPG開発メーリングリストとPGPメーリングリストにこの情報を投稿しました。（尚、この問題は「仕様バグ」に近く、「バグ」と呼称するのには語弊があるためここでは「問題」と呼称しました。OpenPGPを定義するRFC2440では二重に補正をかける定義はありません。）
尚、この問題はGnuPG News Japanにて作田氏の検証により判明しました。 この問題はＰＧＰ７．０より修正されているようです。

## openpgpオプションとは？

GnuPGはOpenPGPに記述されている仕様に則り実装されているわけですがオプションの中にはこれに従わないようにするものがあります。この一般的な例がforce-v3-sigsなどのＰＧＰ対応を考慮しているものです。このオプションはそれを全て無視し、OpenPGPに従うように設定するものです。これは特にoptionsファイルなどにそれを指定している場合にそれを変更せずにOpenPGPモード（つまり相手が対応する暗号ソフトを持っていることが判明している場合）などに使います。

### 1.4.x以前

RFC2440の内容に準じます。

### 1.4.x以降

RFC4880の内容に準じます。

新たにrfc2440及びrfc4880オプションが追加されています。従来の意味でのopenpgpを使用したい場合においてはrfc2440を使用します。rfc4880とopenpgpは同じ挙動となります。

## show-session-keyとoverride-session-keyとは？

1.0.3より新たにサポートされた機能が上記の二つのオプションです。この二つは英国のＲＩＰ法対策に付加されているものです。どういう場合に使うかというと警察機関などが復号鍵の提出を求める場合、秘密鍵を渡してしまうとなりすましなどのリスクがあります。そこでこれはSession keyと呼ばれる暗号化時にそのメッセージのみで使われるキーを表示し、またそれで復号化するオプションです。次のようにするとSession keyが表示されます。

    gpg --show-session-key file.gpg

上記のコマンドラインを入力するとパスフレーズを訊かれるのでパスフレーズを入力するとSession keyが表示されます。尚、これを用いて復号化するには

    gpg --override-session-key ［先に抽出したSession key］ file.gpg

とします。尚、このSession keyが知られてしまうとそのメッセージは誰でも復号化できてしまいます。このオプションは特に必要とされる以外は使用しない方がいいでしょう。（公開鍵暗号の意味がなくなってしまいます。）

## Windows用のフロントエンド

[GPG4WIN](http://www.gpg4win.org) ではWindows用のツールがセットになって配布されています。

## PGPとGnuPG破棄証明書の作成の違いは？

PGPとGnuPGの破棄証明書の作成方法は大きく異なります。PGPでは破棄証明書を作成した時点で対象の鍵に自動的にマージされます。つまりPGPで鍵の破棄をする場合、「破棄証明書」の発行はされずそのまま鍵を破棄ということになります。GnuPGでは破棄証明書を発行すると破棄証明書ファイルが作成されます。この時点で鍵の破棄は行われず、これをインポートするまで破棄したことにはなりません。ちなみにGnuPGの破棄証明書の発行は次のように行います。

    gpg --gen-revoke [keyid]sec 1024D/82957B66


    2000-07-08 Hideki Saito Create a revocation certificate for
    this key? y

    Please select the reason for the revocation: 1 = Key has been
    compromised 2 = Key is superseded 3 = Key is no longer used 0 =
    Cancel (Probably you want to select 1 here) Your decision? 1

    Enter an optional description; end it with an empty line:

    >【任意のコメント（入力しないで改行すると終了）】

    Reason for revocation: Key has been compromised (No description
    given) ←上でコメントを入力した場合はそれがここに表示されます。

    Is this okay? y

    You need a passphrase to unlock the secret key for user:
    “Hideki Saito ” 1024-bit DSA key, ID 82957B66, created 2000-07-08
    Enter passphrase: 【パスフレーズを入力】

    ASCII armored output forced. Revocation certificate created.
    Please move it to a medium which you can hide away; if Mallory gets
    access to this certificate he can use it to make your key unusable.
    It is smart to print this certificate and store it away, just in case
    your media become unreadable. But have some caution: The print system
    of your machine might store the data and make it available to others!

    -----BEGIN PGP PUBLIC KEY BLOCK-----
    Version: GnuPG v1.0.4-1
    (MingW32)
    Comment: A revocation certificate should follow

    【省略】

    -----END PGP PUBLIC KEY BLOCK-----

破棄証明書を作成するGnuPGのアプローチは面倒なように思えますが実はこれは理にかなっているといえます。破棄証明書は一般的に短く、紙に印刷しても打ち込める程度のものです。（３行程度）使用しているＰＣのクラッシュなどで秘密鍵を紛失してしまうことなども決して珍しくありません。破棄証明書を印刷して保存しておくと後に何らかの原因で鍵を破棄する必要が出てきた場合に置いても秘密鍵を持っている必要はないわけです。

## PGP、GnuPG各バージョンの標準アルゴリズムは？

**【本項目の情報は古くなっています。近く更新される予定です。】**

PGPとGnuPGの各バージョンの標準暗号アルゴリズムは次のようになっています。

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="left" />

<col  class="left" />
</colgroup>
<tbody>
<tr>
<td class="left">PGP 2.x</td>
<td class="left">IDEA</td>
</tr>


<tr>
<td class="left">PGP 5.x, 6.x</td>
<td class="left">(DH) CAST, (RSA) IDEA</td>
</tr>


<tr>
<td class="left">PGP 7</td>
<td class="left">(DH) CAST (RSA) CAST (RSA-Legacy) IDEA</td>
</tr>


<tr>
<td class="left">GnuPG 1.0.1 - 1.0.3</td>
<td class="left">Twofish</td>
</tr>


<tr>
<td class="left">GnuPG 1.0.4</td>
<td class="left">AES (Rijndael)</td>
</tr>
</tbody>
</table>

これらの標準設定に基づき鍵に「好まれる」標準が書き込まれます。そのため、例えばGnuPG 1.0.3で作った鍵ペアを1.0.4にインポートしてもそれが引き継がれます。これを変更するためにはそのバージョンで–editオプションを用い、期限切れ（expire）を再度設定することによりその変更が鍵に書き込まれます。

尚、GnuPGの鍵の場合、PGPがアルゴリズムを理解しないためIDEAと表示されますがCASTを使用しますので特に問題はありません。

## GnuPGとPGP 7.0の相性について

**【本項目は最近のバージョンでは当てはまらない可能性があります。参考としてご参照ください。】**

PGP 7.0の場合は次の設定においてGnuPGとの互換性が保たれます。 Diffie-Hellman/DSS鍵で任意の鍵長
RSA鍵で任意の鍵長 鍵がRSA Legacyの場合はIDEAを使用するため、通常GnuPGでは互換性がありません。GnuPGでCAST,
Rijndael, 3DES, Twofishを明示的に指定した場合PGP 7.0との互換性が保たれますが通常は明示的な指定は必要ありません。（公開鍵に設定されているアルゴリズムを使用するため）

GnuPGはforce-v3-sigsを指定しない場合version 4署名を生成しますがこれはPGP
7.0.xにおいても検証することが可能です。尚、以前のバージョンではこれは検証できないためご使用にはご注意下さい。（GnuPGNewsJapanにて作田さんより情報を戴きました、ありがとうございました。）

## GnuPGでIDEAを使うには

バージョン1.4.13よりIDEAアルゴリズムは正式にサポートされました。

### Windowsバージョンの場合

1. バージョンが1.0.5以降なのを確認の上、このページからidea.dllをダウンロードします。
2. このファイルを任意の場所（c:¥lib¥gnupg¥が望ましいです）にコピーします。
3. GnuPGをインストールしている場所に存在するoptionsをテキストエディタなどで開きます。
4. c:¥lib¥gnupgにコピーした場合 load-extension idea.dll と追記します。

その他の場所にコピーした場合

    load-extension c:/gnupg/idea.dll

というような書式で追記します。ディレクトリのセパレーターが¥ではなく/であることに注意してください。

### UNIXバージョンの場合

1. idea.cをダウンロードします。
2. 以下のようにコンパイルします。

    gcc -Wall -O2 -shared -fPIC -o idea idea.c

でこのidea.cをコンパイルします。

任意の場所にコピーして.gnupg/optionsに次のように追記します。

    load-extension /home/user/.gnupg/options

これが成功した場合、
次のような表示があるはずです。

    gpg --version

    gpg (GnuPG) 1.0.5
    Copyright (C) 2001 Free Software Foundation, Inc. This program comes
    with ABSOLUTELY NO WARRANTY. This is free software, and you are
    welcome to redistribute it under certain conditions. See the file
    COPYING for details.
    Home: c:/gnupg
    Supported algorithms:
    Cipher: IDEA, 3DES, CAST5, BLOWFISH, RIJNDAEL, RIJNDAEL192, RIJNDAEL256, TWOFISH
    Pubkey: RSA, RSA-E, RSA-S, ELG-E, DSA, ELG
    Hash: MD5, SHA1, RIPEMD160

万が一IDEAが表示されない場合はideaモジュールの場所やoptionsの設定を確認してください。

## GnuPGの安全性について

GnuPGの安全性について説明する前に理解しておく必要があるのがどんな暗号も解けない暗号はないということです。
つまり時間はかかるにしろいつかは暗号を解くことが可能なわけです。暗号の安全性を高めているのはその時間が非常に長く
現在の技術水準で数百年から数千年という時間となります。 また、未発見の解読方法が発見されると暗号の強度はかなり下がります。
例えばRSAでは大きな数の素因数分解が非常に困難であるという前提のもとにその暗号の強度が保たれています。
将来、素因数分解が容易に行える方法が見つかることがあればRSAの信頼性が損なわれるわけです。
また、コンピューターのスピードの向上による暗号解読の短縮なども懸念されますがこれは鍵長をある程度に保っていくと
それなりに安全に保てます。この計算はO(X^2)の性質を持ちます。つまり鍵長が一ビット増えるとその計算時間はそのべき乗した長さとなります。
RSAの詳しい説明ははやわかりRSAをご覧下さい。

GnuPGで使われる暗号は現段階でその信頼性が検証されているものです。暗号の強度の点で言えば問題はありません。ただし上記したように鍵長がある程度長いものを使用してください。

なお、ソフトウェア自体の安全性ですがこれもソースコードが公開されているということでバックドアなどを仕掛けることは事実上困難です（バイナリで公開されているものは配布者によってそのようなことがなされている可能性は否めません。その場合、ソースをコンパイルするか信頼できるサイト、つまり公式のサイトなどからダウンロードすることをお勧めします。どちらにせよ配布物とその署名を確認するなどの確認をするといいでしょう。）

## GnuPGでの日本語使用について

ターミナル、またはコマンドプロンプトなどでサポートされる場合、GnuPGで日本語を使用することは可能です。
しかしいくつかの点で気を付ける必要があります。

### ＯＳが使用する文字コードの違い

Windows上では日本語はShift-JISを標準にしています。しかしほとんどのUNIXはEUC-JPという文字コードを使用しています。最近ではこれらを変換できるエディタも多く、一見問題が無いように思えるのですが署名などを使用する場合これが大きな問題となります。そのままで署名検証すると問題は起こらないのですが変換ツールなどを使用して他の文字コードに変換した場合に署名が検証できないという問題が発生します。この問題は特に相手が違うＯＳを使用しているのが既知な場合などコメント欄に使用している文字コードを表記するなどの工夫が必要です。

### メールでの文字コード扱いの問題

インターネットでメールを送信するとメールはISO-2022-JP(JIS)に変換されて送信されます。この場合前述の文字コードの違いに加え、JISから環境のネイティブなフォーマット（例えばWindows上ではShift-JISへの変換）が自動的に行われることを認識している必要があります。インターネットでのメールはJISを使うという前提が成り立っているため、通常、この場合は送信する際、JISに変換したものを署名・暗号化するべきであると言えます。これはメーラーなどのプラグインを使用する方法が一番簡単です。トップにいくつか関連サイトへのリンクがありますのでぜひご覧下さい。

## MacOS XでのGnuPG使用について

【本項は更新中です。】

## GnuPGにおける指定失効者

GnuPGで指定失効者（Designated Revoker）を指定、または鍵の失効を行う方法です。指定失効者とは秘密鍵を持っていなくとも鍵を失効できるユーザーのことを指します。

### 指定失効者の設定

注意：指定失効者は設定すると解除（破棄）することができません。 edit-keyオプションを使用して鍵編集モードに入ります。

    gpg --edit-key 公開鍵ID

addrevokerコマンドを入力し、指定失効者のIDを入力します。

    pub 1024D/xxxxxxxx 2006-06-26 xxxxxxxx
    Primary key
    fingerprint: xxxx xxxx xxxx xxxx xxxx xxxx xxxx xxxx xxxx xxxx<
    WARNING:
    appointing a key as a designated revoker cannot be undone! Are you
    sure you want to appoint this key as a designated revoker? (y/N)

ここでyとすることにより指定失効者が追加されます。 鍵をsaveコマンドで保存し、もう一度鍵編集モードに入ると以下のような表示がされます。

    This key may be revoked by DSA key xxxxxxxx
    xxxxxx xxxxxx <xxxxxxx @xxxx.xxx>

これにより、指定失効者の設定がされました。

### 指定失効者による鍵の破棄

指定失効者による鍵の破棄は本人による破棄にとほぼ同様です。
異なる点は、破棄証明書の生成をgen-revokeの代わりにdesig-revokeで行う点です。

    gpg --desig-revoke xxxxxxxx

ここで、指定失効者のパスフレーズを入力すると破棄証明書が生成されます。これを–importで取り込むことにより鍵の破棄が行われます。

### 制限事項

公開鍵サーバによっては指定失効者により破棄された鍵を認識しない場合があります。

## 有効期限（Expire）の設定の方法いろいろ

edit-keyの鍵インターフェースなどでの設定で使用できる有効期限の設定にはいくつかの方法があります。

尚、あまり使用されませんが、ファイルやメッセージなどへの署名にも有効期限を設定することができます。ask-sig-expireを設定すると署名の度にこれが確認されるようになります。

### 無期限

0を指定します。

### 残りの期限で指定する

数字のみの指定で残り期限は日の単位になります。つまり10の入力で10日の有効期限となります。同様にwを追加すると週単位の指定、mを指定すると月単位の指定、yを使用すると年単位の指定となります。尚、この場合、有効期限の時間は現在時間と同様になります。

### 有効期限の日付を指定する

YYYY-MM-DDのフォーマットで入力することにより、有効期限を日付で指定できます。例えば2015-03-19と入力すると2015年3月19日0時0分に失効するものとなります。

YYYYMMDDTHHmmSSのフォーマットで入力すると時刻を含む有効期限を設定できます。例えば20150319T103020と指定するとシステム指定のタイムゾーンで2015年3月19日10時30分20秒に失効します。

### 残りの秒数で指定する

seconds=xの形で指定することにより秒数の指定ができます。例えば、120秒で失効する署名を作成する場合はseconds=120と指定します。特殊な場合を除き、あまり役に立たないかと思います。
