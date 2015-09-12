+++
title = "GnuPGでサポートされている暗号図鑑"
slug = "sample"
+++

GnuPGでサポートされている対称暗号やハッシュ関数のサンプルをまとめてみました。順番はバージョン情報で表示される順です。

## 暗号方式

「gnupg」の文字列をgnupgのパスフレーズで暗号化したものです。圧縮は無効にしてあります。

### IDEA

    -----BEGIN PGP MESSAGE-----

    jA0EAQMC/cdy1kusWi/OpCFcI1Nkov6aASPD8qSPqnUrbosZNOBAK/1XkaNmbnNt
    hfg=
    =fwix
    -----END PGP MESSAGE-----

### 3DES (Triple DES)

    -----BEGIN PGP MESSAGE-----

    jA0EAgMCDDyvkjYMypDOpCFQ7gOW3n9E4yQIQebxPhwQ+my6n/Pd+T/YA/9BfhPp
    3Io=
    =PSFW
    -----END PGP MESSAGE-----

### CAST5

    -----BEGIN PGP MESSAGE-----

    jA0EAwMCpvy+v01TY3DOpCF6wG2Ii/2UHlvrruPcUx7frLzcAVvA0LXx5cKaP4Io
    FLg=
    =Mj+/
    -----END PGP MESSAGE-----

### BLOWFISH

    -----BEGIN PGP MESSAGE-----

    jA0EBAMC7+90cQ/nJg3OpCE91x/TQ5Th/yQM7srODYhpH3njKblHwMiO6Q/H+yoO
    mIE=
    =hygX
    -----END PGP MESSAGE-----

### AES (AES128)

    -----BEGIN PGP MESSAGE-----

    jA0EBwMCwaYw+iqJVGnO0kAB45Mx2CFo+iUC1z3sULLMGpEmC/Wv6AzzpD77RT3f
    LJJjaJPTTnswfIYKcB6+fE86D7wH0HKl+7RRRfsuqVUc
    =WZdG
    -----END PGP MESSAGE-----

### AES192

    -----BEGIN PGP MESSAGE-----

    jA0ECAMCNJYzJ36zLAbO0kAB1/9MoATb/BIb/61NvYwtHZs68etlKe6zINCuRL3h
    hfSJSjRfQgHU+YX0IyuU2+Y+OOmaLDwcjhStXKqyRF2e
    =tkqP
    -----END PGP MESSAGE-----

### AES256

    -----BEGIN PGP MESSAGE-----

    jA0ECQMC646zduYS4RjO0kABn2dzYlVyNPF9Hf8Wug0O70byrpV1v7y9fLaLnsiL
    OWNQxqZ3jxHZceK6q5oeP8InFBWOlszFxGTsrA57v5qR
    =60Ma
    -----END PGP MESSAGE-----

### TWOFISH

    -----BEGIN PGP MESSAGE-----

    jA0ECgMC6jjcw+2SUNLO0kAB/BP+9vbBqdDsvo2tFtgdAL8LLOYs5LTOa3B1RpI4
    5W+N5ZhxKqZr1YkYsksM95EQqVhb+TcYFT+V0tSepqZL
    =FUkc
    -----END PGP MESSAGE-----

### CAMELLIA128

    -----BEGIN PGP MESSAGE-----

    jA0ECwMCApak8b2GWfrO0kAB0PKCbLEUuGw6xTJRi68h3CH3i+GqoiXti4bBJ30R
    beOWp0kepgl464R8a4HG7/pTVPFJFxTHGuP76L0BH+Bp
    =wdZe
    -----END PGP MESSAGE-----

### CAMELLIA192

    -----BEGIN PGP MESSAGE-----

    jA0EDAMCCfxlF8wp/rXO0kABe/gX9CVlPWy4DdGu6Td5aMXMGNtbNeAV7EMyrwoO
    k/TPgoUBMMrYoHL8loYCU5DN7ZghrVV9IRAbhsgMgWV0
    =U8E+
    -----END PGP MESSAGE-----

### CAMELLIA256

    -----BEGIN PGP MESSAGE-----

    jA0EDQMCaLnEaKX4hGTO0kABN0o57JcecjriHgJLj/6OLoUh3fvQZ+aZSh0ih3eh
    p3BTqdksjPqwA7JdoYfbK7qfch01MFEnxhebj6vYYd9R
    =BONa
    -----END PGP MESSAGE-----

## ハッシュ関数

GnuPGのprint-md機能を使用し、gnupgという文字列から得られたハッシュです。

### MD5

    CE D0 72
    BC EE 66
    4F 97 49
    E5 85 26
    77 5C 52
    38

### SHA1

    12A2 2051 DA6C
    6B99 2A0F 17C1
    8C59 C729 D72D
    A5B3

## RIPEMD160

    4929 FE49 04F9
    BFC4 2D50 3599
    6491 4C76 2909
    5EB7

## SHA256

    87450705 D106D26A DFB67178
    44144643 5719F9E8 37A47BAE
    1C1CD197 CB41AD33

## SHA384

    8438202A B4C614EA CEAA915C
    0ED6097C 575F3C9C CD58CFF3
    E64E41B5 09F037C5 9B528A43
    FBCF611F 657CE394 7C1DA0E9

## SHA512

    1887AE07 16C9F4CF 6CCD63DA
    5F438562 48EFB2DF CCE59E61
    B3F8970D 4EDA8946 611D45E6
    0E779337 93581C8E E1426B4E
    EB984741 12C721C3 ED89C2B4
    2C5E1923

## SHA224

    1B68E694 92FEAC01 8B76ED43
    F4DC75B4 3568E7BA 7F457ABF
    D30571FA
