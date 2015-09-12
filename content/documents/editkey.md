+++
title = "edit-keyオプションの使い方"
slug = "editkey"
categories = [
  "機能解説",
]
tag = "edit-key"
+++

GnuPGでは–edit-keyのオプションを使用して鍵（秘密鍵、または公開鍵）に対して変更を行ったり、情報を参照したりすることができます。 今回の特集ではそのオプション、特に鍵に変更を加えるものを見ていく事にします。 尚、このモードではコマンドラインから行う事ができる鍵への署名、破棄などをインタラクティブに行う事もできます。 （尚、これらは高度なオプションが含まれますので慎重に行う事をお勧めします。）

## edit-keyモードへの入り方


利用するのには以下のようにコマンドラインに入力します。

    gpg --edit-key 0x565A5E2A

この時、秘密鍵を使用できる場合は「Secret key is available.」と表示されます。（日本語化がなされている場合は「秘密鍵が使用できます。」となりますが今回の説明では英語で表示された場合のものを表示します。

    gpg --edit-key 0x565A5E2A

    gpg (GnuPG) 1.2.3; Copyright (C) 2003 Free Software Foundation, Inc.
    This program comes with ABSOLUTELY NO WARRANTY.
    This is free software, and you are welcome to redistribute it
    under certain conditions. See the file COPYING for details.
    Secret key is available.

    pub  1024D/565A5E2A  created: 2003-12-07 expires: never      trust: u/u
    sub  2048g/E8D70F9E  created: 2003-12-07 expires: never

    (1). FooBar (Not a production key) [email protected]>

    Command>

ここでhelpと入力すると以下のような表示が行われます。

    Command> help
    quit       quit this menu
    save       save and quit
    help       show this help
    fpr        show fingerprint
    list       list key and user IDs
    uid        select user ID N
    key        select secondary key N
    check      list signatures
    sign       sign the key
    lsign      sign the key locally
    nrsign     sign the key non-revocably
    nrlsign    sign the key locally and non-revocably
    adduid     add a user ID
    addphoto   add a photo ID
    deluid     delete user ID
    addkey     add a secondary key
    delkey     delete a secondary key
    addrevoker add a revocation key
    delsig     delete signatures
    expire     change the expire date
    primary    flag user ID as primary
    toggle     toggle between secret and public key listing
    pref       list preferences (expert)
    showpref   list preferences (verbose)
    setpref    set preference list
    updpref    updated preferences
    passwd     change the passphrase
    trust      change the ownertrust
    revsig     revoke signatures
    revuid     revoke a user ID
    revkey     revoke a secondary key
    disable    disable a key
    enable     enable a key
    showphoto  show photo ID

いろいろとオプションがありますが、これは日本語では以下のようになります。

    コマンド> help
    quit       このメニューを終了
    save       保存して終了
    help       このヘルプを表示
    fpr        指紋を表示
    list       鍵とユーザーIDの一覧
    uid        ユーザーID Nの選択
    key        副鍵Nの選択
    check      署名の一覧
    sign       鍵へ署名
    lsign      鍵へ内部的に署名
    nrsign     失効できないよう鍵へ署名
    nrlsign    失効できないよう鍵へ内部的に署名
    adduid     ユーザーIDの追加
    addphoto   フォトIDの追加
    deluid     ユーザーIDの削除
    addkey     副鍵の追加
    delkey     副鍵の削除
    addrevoker 失効鍵の追加
    delsig     署名の削除
    expire     有効期限の変更
    primary    ユーザーIDを主にする
    toggle     秘密鍵と公開鍵の一覧の切替え
    pref       選好の一覧 (エキスパート)
    showpref   選好の一覧 (冗長)
    setpref    選好の一覧を設定
    updpref    選好の一覧を更新
    passwd     パスフレーズの変更
    trust      所有者信用の変更
    revsig     署名の失効
    revuid     ユーザーIDの失効
    revkey     副鍵の失効
    disable    鍵の使用を禁止する
    enable     鍵の使用を許可する
    showphoto  フォトIDを表示

# showprefコマンド


showprefコマンドを使用する事により鍵の特性が表示されます。

    Command> showpref

    pub  1024D/565A5E2A  created: 2003-12-07 expires: never      trust: u/u
    (1). FooBar (Not a production key) [email protected]>
         Cipher: AES256, AES192, AES, CAST5, 3DES
         Digest: SHA1, RIPEMD160
         Compression: ZLIB, ZIP, Uncompressed
         Features: MDC

上から暗号、署名、圧縮、機能に使用するアルゴリズムを表示します。 これは最初に表示されているものから優先して使用する事ができます。 尚、この順番を入れ替えたり、特定のアルゴリズムを使用しないようにすることもできます。 これをするのにはsetprefオプションを使用します。
setprefコマンド

prefコマンドを使用すると以下のような表示を得る事ができます。

    Command> pref

    pub  1024D/565A5E2A  created: 2003-12-07 expires: never      trust: u/u
    (1). FooBar (Not a production key) [email protected]>
         S9 S8 S7 S3 S2 H2 H3 Z2 Z1 [mdc]

setprefコマンドと表示されているスタイルの指定をすることによりそれを指定する事ができます。 つまり、例えば3DESを使用したくない場合は、以下のように指定します。（厳密には3DESを無効にしても他に使用できるものが見つからない場合はこの設定を無視して3DESによる暗号化が行われます。これは3DESがOpenPGPで必須のアルゴリズムとされているためです。）

    setpref S9 S8 S7 S3 H2 H3 Z2 Z1

この時点ではこの変更は行われていません。 次に以下のコマンドを入力します。

    updpref

すると以下のように表示されます。

    Command> updpref

    Current preference list: S9 S8 S7 S3 H2 H3 Z2 Z1 [mdc]
    Really update the preferences?

ここでyを入力するとsetprefで行った変更を行うためにパスフレーズの入力を要求します。 そして、saveと入力してedit-keyモードから抜けると変更が有効になります。

# expireコマンド


expireコマンドではその有効期限を変更する事ができます。 expireコマンドの実行で以下のような設定をすることができます。

    Command> expire

    Changing expiration time for the primary key.
    Please specify how long the key should be valid.
             0 = key does not expire
            = key expires in n days
          w = key expires in n weeks
          m = key expires in n months
          y = key expires in n years

    Key is valid for? (0)

指定は0で無期限もしくは数字で日数、またはその後に、w、m、yの単位を入力することにより週、月、年の単位で指定する事ができます。 例えば1yと入力する事により一年間有効にする事ができます。

# 複数の鍵を使用する


指定した鍵に複数の副鍵がある場合は少し特殊な操作が必要にある必要があります。 副鍵がある場合、鍵を表示すると以下のような表示になります。

    Command> key
    pub  1024D/514D0EF4  created: 2003-12-08 expires: never      trust: u/u
    sub  1024g/88480126  created: 2003-12-08 expires: never
    sub  1024R/E5FFF9CD  created: 2003-12-08 expires: never
    (1). FooBar (Not for a production use)

普通に鍵の変更をしようとすると主鍵の変更となります。 どの鍵に対して変更をしようとしているかはコマンドを使用する時の表示で判別することができます。

## 通常の場合


    Command> expire

    Changing expiration time for the primary key.
    Please specify how long the key should be valid.

             0 = key does not expire
            = key expires in n days
          w = key expires in n weeks
          m = key expires in n months
          y = key expires in n years

    Key is valid for? (0)

上記の表示のように、”~ for the primary key.”という表示で主鍵に変更を加えようとしていることがわかります。
副鍵に変更を加えるにはkeyコマンドを使用します。

    gpg --edit-key foobar

    gpg (GnuPG) 1.2.3; Copyright (C) 2003 Free Software Foundation, Inc.

    This program comes with ABSOLUTELY NO WARRANTY.
    This is free software, and you are welcome to redistribute it
    under certain conditions. See the file COPYING for details.
    Secret key is available.

    pub  1024D/514D0EF4  created: 2003-12-08 expires: never      trust: u/u
    sub  1024g/88480126  created: 2003-12-08 expires: never
    sub  1024R/E5FFF9CD  created: 2003-12-08 expires: 2003-12-09

    (1). FooBar (Not for a production use)

    Command> key 2

    pub  1024D/514D0EF4  created: 2003-12-08 expires: never      trust: u/u
    sub  1024g/88480126  created: 2003-12-08 expires: never
    sub* 1024R/E5FFF9CD  created: 2003-12-08 expires: 2003-12-09

    (1). FooBar (Not for a production use)

ここで打ち込んだkey 2のコマンドによってE5FFF9CDの鍵に\*マークがついたのがわかると思います。 これにより今行う変更はこの副鍵に対して行われます。これは複数の鍵を選択する事も可能でこの場合は以下のようになります。

    gpg –edit-key foobar

    gpg (GnuPG) 1.2.3; Copyright (C) 2003 Free Software Foundation, Inc.
    This program comes with ABSOLUTELY NO WARRANTY.
    This is free software, and you are welcome to redistribute it
    under certain conditions. See the file COPYING for details.
    Secret key is available.

    pub  1024D/514D0EF4  created: 2003-12-08 expires: never      trust: u/u
    sub  1024g/88480126  created: 2003-12-08 expires: never
    sub  1024R/E5FFF9CD  created: 2003-12-08 expires: 2003-12-09
    sub  1024R/9A8AA276  created: 2003-12-10 expires: never

    (1). FooBar (Not for a production use)

    Command> key 2

    pub  1024D/514D0EF4  created: 2003-12-08 expires: never      trust: u/u
    sub  1024g/88480126  created: 2003-12-08 expires: never
    sub* 1024R/E5FFF9CD  created: 2003-12-08 expires: 2003-12-09
    sub  1024R/9A8AA276  created: 2003-12-10 expires: never

    (1). FooBar (Not for a production use)

    Command> key 3

    pub  1024D/514D0EF4  created: 2003-12-08 expires: never      trust: u/u
    sub  1024g/88480126  created: 2003-12-08 expires: never
    sub* 1024R/E5FFF9CD  created: 2003-12-08 expires: 2003-12-09
    sub* 1024R/9A8AA276  created: 2003-12-10 expires: never

    (1). FooBar (Not for a production use)

expireなどの一定のコマンドは一つの鍵のみが選択されている必要があります。
