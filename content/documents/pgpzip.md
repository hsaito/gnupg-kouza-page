+++
title = "PGP Zipの取り扱い方法"
slug = "pgpzip"
categories = [
  "機能解説",
]
+++

PGPにはPGP Zipと呼ばれるアーカイブの作成をすることができるようになっています。

## ファイル構造

PGP Zipはファイル構成的には複数のファイルをtarにより単一化したものを暗号化するという構成をとっています。PGP Zipそのものがサポートされていない環境においてもこの処理を手動で行うことにより、PGP Zipとして扱えるファイルを作成することができます。

## コマンドラインの例


### gpg-zipスクリプトがGnuPGに同梱されている環境の場合


gpg-zipスクリプトがGnuPGとともに配布されている環境（シェルスクリプトが使用できる環境）である場合はgpg-zipスクリプトを使用することにより互換性のあるファイルが作成できます。

    gpg-zip -e [ファイル名１] [ファイル名２] …

### gpg-zipスクリプトが使用できない場合


gpg-zipが使用できない場合はtarコマンド（もしくは7-zipなど、tarファイルが作成できるソフト）を使用することにより可能です。（尚、基本的にはtar環境が標準で使用できる環境にいる場合は恐らくgpg-zipコマンドも使用できる可能性が高いです。）尚、Windows環境で動作するtarコマンドはGNU utilities for Win32で入手できます。

#### tarファイルの作成


tarコマンドを使用してファイルを作成する場合は以下のようにします。

    tar -c ファイル名 > file.tar

#### 暗号化・署名


作成したtarファイルを暗号化する際に、–set-filenameオプションを使用します。

    gpg -o file.pgp -e file.tar –set-filename “foo.tar”

fooのところは任意の名称で構いません。この–set-filenameで.tarの名前がついたファイル名が指定されていない場合は正常動作しません。（後述）
この方法で作成したファイルはPGPでもPGP Zipとして取り扱えるようになります。

##### 上記を組み合わせた方法


パイプを使うことにより上記を組み合わせることもできます。

    tar -c [ファイル名] | gpg -o file.pgp -e –set-filename “foo.tar”

#### 復号化


PGPや上記の方法で作成したPGP Zipファイルを復号化する際は反対に暗号化されているものをtarファイルに復号化した後、tarファイルを解凍する方法になります。

    gpg -o file.tar -d file.pgp tar xvf file.tar

パイプを使用した場合は次のとおりです。

    gpg -d file.pgp | tar xv

尚、処理系が異なると日本語のファイル名は文字化けします。（特にWindowsとMac/Linuxの間）ただし、検証自体は処理間の形式に対して行われますので署名の判定に関しては正しいものとなります。

#### Macの場合の注意

Macの場合はtarコマンドではなくgnutarコマンドを使用してください。尚、環境変数としてCOPYFILE\_DISABLE=trueが指定されていないとAppleDouble（file.txtに対応する.\_file.txtのようなファイルとして）として拡張属性が含まれてしまいますのでご注意ください。

## Kleopatraのオプションは使用できるか（Gpg4Win Windows、KDE環境）

Kleopatraを使用しファイルをKleopatraウインドウにドラッグ・ドロップした上で、Encrypt/Signを選択、Archive files with:のチェックボックスを有効にしTAR (PGP®-compatible)を選択することができるようになっています。バージョン2.1.0で検証してみると、これを使用した場合、ファイル名が正常に埋めこまれないため、PGP（10.2で検証）ではtarファイルをファイルとして扱う挙動を見せてしまいます。そのため、現状は受け取ったPGP Zipファイルを復号することは可能ですが、暗号化には使用しない方がいいでしょう。

### 埋めこまれたファイル名の違い

#### Kleopatraで作成した場合


    :literal data packet:
    mode b (62), created 1315533132, name=”",
    raw data: unknown length

#### PGPで作成した場合

    :literal data packet:
    mode b (62), created 0, name=”pgpTmpArchive2020.tar”,
    raw data: unknown length
