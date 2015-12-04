+++
title = "GNU Privacy Guard講座 トップ"
slug = "main"
+++

## ニュース
* [Let's Encrypt](http://letsencrypt.org)の証明書により、暗号化接続が可能になりました。[https://gnupg.hclippr.com](https://gnupg.hclippr.com)で接続できます。HSTSを使用しており、一度暗号接続を行うと最終アクセスより一週間、自動的に平文版に接続した場合でも暗号接続に切り替わります。
* 当サイトは試験的運用として、[Tor](http://torproject.org)よりのアクセスに対応しました。次の秘匿サービスURLが使用できます。http://gnupg4na2oymu5ls.onion

## GNU Privacy Guardとは？

GnuPGはGNUプロジェクトのRFC4880で定義されるOpenPGP標準の完全でフリーな実装です。GnuPGを使用することによりデータや通信 を暗号化したり署名したりすることができ、多機能の鍵管理システムや、多くの種類の公開鍵ディレクトリへのアクセスを可能にするモジュールが用意されています。

GnuPGはGPGとも呼ばれ、他のアプリケーションとの統合を容易に可能にするコマンドラインツールです。多くのフロントエンドアプリケーション やライブラリが存在します。バージョン２ではS/MIMEの機能も採り入れています。

GnuPGはフリーソフトウェア（自由の意味でのフリー）です。GNU General Public Licenseに基づき、これはフリーに使用、変更、配布することができます。

GnuPGは二種類用意されており、ポータブルなスタンドアロンバージョンである1.4.x、そして、コンパイルの難易度が高いですが、より多くの機能を提供する2.0.xです。GnuPGはGNUプロジェクトのRFC4880で定義されるOpenPGP標準の完全でフリーな実装です。

## 最新情報

現在GnuPGは三種類、提供されています。それらはGnuPG stable、GnuPG modern、GnuPG classicとなります。

本サイトにおいて、これらは以下のようなバージョン系列で呼称されている場合があります。

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="left" />

<col  class="left" />

<col  class="left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="left">呼称</th>
<th scope="col" class="left">バージョン系列</th>
<th scope="col" class="left">内容</th>
</tr>
</thead>

<tbody>
<tr>
<td class="left">GnuPG stable</td>
<td class="left">2.0系</td>
<td class="left">OpenPGPとSMIME、Secure Shellなどのサポートを含むモジュラーな構成</td>
</tr>


<tr>
<td class="left">GnuPG modern</td>
<td class="left">2.1系</td>
<td class="left">GnuPG stableに加え、楕円暗号など先進的なサポートを含むバージョン(将来的にはGnuPG stableの後継になります。)</td>
</tr>


<tr>
<td class="left">GnuPG classic</td>
<td class="left">1.4系</td>
<td class="left">古いプラットフォームなどでも動作する先進的な機能を含まないバージョン。</td>
</tr>
</tbody>
</table>

* GnuPG stable / GnuPG modernはより多くの機能を含みますが、構築は難しくなります。詳細は[GnuPG 2のコンパイル手順](/documents/gpg2compile)をご覧ください。
* GnuPG stable / GnuPG modernではパスフレーズの入力にpinentryが必須になります。(GnuPG classicではオプション。)
* GNU Privacy Guard講座ではLinux環境向けに、[GnuPG modernを構築、インストールするためのスクリプト群](https://github.com/hsaito/gnupg-buildkit)を用意しています。
  * 予備サイトとして[HidekiSaitoComレポジトリ](http://git.hidekisaito.com)でも[公開](http://git.hidekisaito.com/?p=gnupg-buildkit.git)しています。
  * こちらを元にした[Dockerコンテナ](https://hub.docker.com/r/hsaito/gnupg2/)を使用し、実環境から切り離してGnuPG modernを使用することも可能です。
 

## ダウンロード

GnuPGのダウンロードは[gnupg.org](http://gnupg.org/)から可能です。

* [ソースコード](http://gnupg.org/download/index.en.html)
* Windows向けはバイナリ入手にいくつかの方法があります。
  * [Gpg4win](http://gpg4win.org/)はGnuPG本体の他、その運用に役に立つツールがバンドルされています。(Stable版)
  * [GnuPG Download](https://gnupg.org/download/index.html)ではModern版、Classic版がダウンロードできます。(こちらはGnuPGの本体のみになります。コマンドラインで使用するユーザー向けです。)
* Mac向けは[GPGTools](https://gpgtools.org/)を使用してください。

## 情報ページ

* [GnuPGの使い方](/documents/howto)
* [GnuPG Tips](/documents/tips)

## 公式発表等（翻訳版）

* [16 Years of protecting privacy（日本語版）](/official/16th-announcement)
* [A Short History of the GNU Privacy Guard（日本語版）](/official/shorthist)

## 特集

### GnuPG関連

* [16 Years of protecting privacy (日本語版)](/official/16th-announcement)
* [GnuPGパラメータシート](/extra/parameter)
* [GnuPGでサポートされている暗号図鑑](/extra/sample)
* [受信者秘匿機能の利用](/documents/anonymous-recipients)
* [edit-keyオプションの使い方](/documents/editkey)
* [GnuPG 2のコンパイル手順](/documents/gpg2compile)
* [Paperkeyを使った秘密鍵のバックアップ](/documents/paperkey)
* [PGP Zipの取り扱い方法](/documents/pgpzip)

### 暗号技術

* [会社環境での暗号運用の問題点](/papers/company)
* [暗号運用の問題点](/papers/problem)

## その他

### 更新履歴
* 当サイトの編集履歴は[GitHub](https://github.com/hsaito/gnupg-kouza-page)で閲覧可能です。
  * 予備サイトとして[HidekiSaitoComレポジトリ](http://git.hidekisaito.com/)でも[公開](http://git.hidekisaito.com/?p=gnupg-kouza-page.git)しています。

### Tor秘匿サービスでのアクセス
* 当サイトは[Tor](http://torproject.org)よりのアクセスに対応しております。次の秘匿サービスURLが使用できます。http://gnupg4na2oymu5ls.onion
  * 秘匿サービスは完全に別システムで運用されているため、通常版が使用できる場合でも繋がらない場合があります。その場合は時間をおいて試してみて下さい。
  * Torをインストールしていない環境では[tor2web](https://onion.to/)を使用してアクセスすることが可能ですが、Torでアクセスすることの利点は失われます。それでも試してみたい方は、次のうちのどれかのURLを使用して下さい。
	* http://gnupg4na2oymu5ls.onion.to
	* http://gnupg4na2oymu5ls.onion.city
	* http://gnupg4na2oymu5ls.onion.cab
	* http://gnupg4na2oymu5ls.onion.direct
