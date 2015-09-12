+++
title = "GnuPGパラメータシート"
slug = "parameter"
categories = [
  "法的情報",
]
+++

<div id="table-of-contents">
<h2>&#30446;&#27425;</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. 暗号機能</a>
<ul>
<li><a href="#sec-1-1">1.1. 暗号機能は認証又はデジタル署名以外の目的を有するか。</a></li>
<li><a href="#sec-1-2">1.2. 暗号機能は本製品に搭載されているものか。</a></li>
<li><a href="#sec-1-3">1.3. 暗号機能は次のいずれかに該当するものか。</a></li>
</ul>
</li>
<li><a href="#sec-2">2. アルゴリズム及び鍵長</a></li>
<li><a href="#sec-3">3. 該非判定</a></li>
</ul>
</div>
</div>


パラメータシートとは暗号を輸出する際に輸出規制の対象となるか否かを税関が判断する情報です。本来パラメータシートはメーカーが作成するもので、また、GnuPGの場合公知の暗号とみなされるため、輸出規制の対象外となるかと思いますが、どういった表記になるかを書いてみました。

その使用可能性はまったく考慮していないので、何らかの形で使用される場合は表記の正確性に関しては別途、ご確認ください。

## 暗号機能



### 暗号機能は認証又はデジタル署名以外の目的を有するか。

* [ ] NO
* [X] YES

### 暗号機能は本製品に搭載されているものか。

* [ ] NO
* [X] YES

### 暗号機能は次のいずれかに該当するものか。

A. 対称アルゴリズムを用いたものであって、アルゴリズムの鍵の長さが56ビットを超えるもの
B. 非対称アルゴリズムを用いたものであって、(a) 512ビットを超える整数の素因数分解（RSA等）に基づくもの、(b) 有限体の乗法群における512ビットを超える離散対数の計算（Diffie-Hellman等）に基づくもの、(c) 上記に規定するもの以外の群における112ビットを超える離散対数の計算（楕円曲線上のDiffie-Hellman等）に基づくもの

* [ ] NO
* [X] YES

## アルゴリズム及び鍵長

「libcrypt組み込み」となっているものはGnuPG 2系のみ該当。

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="left" />

<col  class="right" />

<col  class="left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="left">アルゴリズム</th>
<th scope="col" class="right">鍵長</th>
<th scope="col" class="left">備考</th>
</tr>
</thead>

<tbody>
<tr>
<td class="left">IDEA</td>
<td class="right">128</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">Triple DES</td>
<td class="right">192</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">CAST5</td>
<td class="right">128</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">BLOWFISH</td>
<td class="right">128</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">AES</td>
<td class="right">128,192,256</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">TWOFISH</td>
<td class="right">128,256</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">CAMELLIA</td>
<td class="right">128,192,125</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">MD5</td>
<td class="right">128</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">SHA-1, SHA-2</td>
<td class="right">160,256,384,512</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">RIPE-MD</td>
<td class="right">160</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">RSA</td>
<td class="right">1024-8192</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">DSA/ElGamal</td>
<td class="right">1024-3072</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">DH</td>
<td class="right">&#xa0;</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">MD5-HMAC</td>
<td class="right">128</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">SHA-1-HMAC, SHA-2-HMAC</td>
<td class="right">160,256,384,512</td>
<td class="left">&#xa0;</td>
</tr>


<tr>
<td class="left">RIPEMD-HMAC</td>
<td class="right">160</td>
<td class="left">&#xa0;</td>
</tr>
</tbody>

<tbody>
<tr>
<td class="left">RC4</td>
<td class="right">&#xa0;</td>
<td class="left">libgcrypt組み込み</td>
</tr>


<tr>
<td class="left">SEED</td>
<td class="right">128</td>
<td class="left">libgcrypt組み込み</td>
</tr>


<tr>
<td class="left">TIGER</td>
<td class="right">192</td>
<td class="left">libgcrypt組み込み</td>
</tr>


<tr>
<td class="left">MD4</td>
<td class="right">&#xa0;</td>
<td class="left">libgcrypt組み込み</td>
</tr>


<tr>
<td class="left">Whirlpool</td>
<td class="right">&#xa0;</td>
<td class="left">libgcrypt組み込み</td>
</tr>


<tr>
<td class="left">TIGER-HMAC</td>
<td class="right">192</td>
<td class="left">libgcrypt組み込み</td>
</tr>


<tr>
<td class="left">MD4-HMAC</td>
<td class="right">&#xa0;</td>
<td class="left">libgcrypt組み込み</td>
</tr>


<tr>
<td class="left">Whirlpool-HMAC</td>
<td class="right">&#xa0;</td>
<td class="left">libgcrypt組み込み</td>
</tr>


<tr>
<td class="left">DES</td>
<td class="right">56</td>
<td class="left">libgcrypt組み込み</td>
</tr>


<tr>
<td class="left">ECDSA</td>
<td class="right">&#xa0;</td>
<td class="left">libgcrypt組み込み</td>
</tr>
</tbody>
</table>

## 該非判定

貿易関係貿易外取引等に関する省令 第九条 五項ニにより「ソースコードが公開されているプログラムを提供する取引」となるため、適応外。
