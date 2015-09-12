+++
title = "GnuPG 2のコンパイル手順"
slug = "gpg2compile"
categories = [
  "高度な情報",
]
+++

GnuPG 2のコンパイルはGnuPG 1.x系列に比べると依存が多く、より複雑なプロセスを要します。
ここではコンパイル方法をまとめました。

尚、以下の手順を半自動的に実行する [gnupg-buildkit](https://github.com/hsaito/gnupg-buildkit) を公開しています。こちらを使用することにより、GnuPG 2.1を入手し、コンパイルするのをほぼ自動化できます。尚、こちらの使用にはGnuPG (1.x系列でも構いません)が入っていることが前提になっています。

特にLinuxのリモート環境（ホスティングサーバ）などにインストールする際に役に立つと思います。Windowsでのコンパイルについては本項では言及しません。
尚、ホスティングサーバに置かれている秘密鍵など、ローカル管理に比べて比較的安全性が劣りますので留意しておいてください。

## 必要なソースコード


* GnuPG 2
* libgcrypt
* libksba
* DirMngr
* libgpg-error
* libassuan
* pinentry

このうち、pinentry以外はGnuPGの[ダウンロードページ](http://gnupg.org/download/index.en.html)からダウンロードできます。また、環境によってはBzip2ライブラリが必要です。（プレフィックスが特殊な場合はwith-bzip2オプションでincludeを指定のこと。）
PinentryもGnuPGのFTPサーバにあるのですが、上記のダウンロードページからリンクされていません。当該ディレクトリから最新版をダウンロードしてください。
GPGME、Entropy Gathering Daemonは通常は必要ありませんが環境、使用法によっては導入する必要があるかもしれません。（Entropy Gathering Daemonは/dev/randomが存在しない環境で必要です。）

GnuPG Modern (2.1.x系)の場合、DirMngrは組み込み済みであるため、別途入手、コンパイルする必要はありません。

## コンパイルの順番


コンパイルは依存の関係上、次の順番で行う必要があります。

* libgpg-error
* libksba
* libgcrypt
* libassuan
* DirMngr
* GnuPG 2
* pinentry

厳密にはいくつかのものは順番が入れ替わっても問題ありませんが、大方、上記のような順番で行う必要があります。
コンパイル自体は一般的なconfigure ; make ; make installとなりますが、特に依存関係のエラーを見落とさないようにしてください。
尚、特にホスティングサイトなどで特別なプレフィックスを使用している場合はbinディレクトリにパスが通っており、LD_LIBRARY_PATHがlibディレクトリに通っていることを確認してください。configureにprefixが通っていてもgnupg2のコンパイル時に失敗します。

## 注意点など

### dirmngrでリンキングに失敗する場合

ber_freeのシンボルで問題が出る場合、configureの際にLIBS=-llberを通すことで解決します。
