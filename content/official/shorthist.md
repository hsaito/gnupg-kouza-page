+++
title = "A Short History of the GNU Privacy Guard（日本語版）"
slug = "shorthist"
+++

最初のバージョンのGNU Privacy Guard[^1]がリリースされてから10年たちました。この最初のバージョンはGnuPGとは呼ばれず、g10と呼ばれ、これはドイツの憲法の通信の自由を定義する第十項（Grundgesetz Artikel 10）及び、シークレットサービスがこの憲法をすり抜けることができる、G-10法に対する語呂合わせとして命名しました。

最初のバージョン0.0.0は1997年12月20日[^2]に公開され、これはぎりぎりRSAやIDEAの特許で保護されたアルゴリズムを使用せず、Elgamal及びBlowfishを使用したPGPとの互換性を持ったぎりぎり動作するものでした。これはテスト版としてマークされており、現在GnuPGで見られるほとんどの機能を含んでいませんでした。データのフォーマットはOpenPGPと互換性を持っておらず、よりPGP 2のフォーマットに近く、いくつかの拡張（データのストリームを可能にするなど）を含んでいました。OpenPGP作業会は1997年の秋に設立されており、その存在を知ったのは私がg10を作成するにあたり、当時すでに存在していたドラフトを参考にするには遅すぎました。著作権の問題から、PGP-5が使用するフォーマットをリバースエンジニアすることができなかったので、OpenPGP作業会は必要とされていたものが必要なタイミングに設立されたものでした。

GnuPGについて語る前に数年、時間を遡ってみましょう。1991年に政治活動家であったPhil ZimmermannがPretty Good Privacy (PGP)と呼ばれるソフトウェアを公開しました。PGPは簡単に使え、さらにバックドアが存在せず、ソースコード公開された暗号化ツールでした。PGPは暗号手法的に強力であり、pretty good（訳注：「けっこう優れた」）以上のものでしたが、初期的にはいくつかのバグがあり、自家製の暗号化アルゴリズムでした。ソースコードが公開されていたことで、コミュニティーのハッカー（Branko Lankester、Colin Plumb、Derek Atkins、Hal Finney、Peter Gutmann、他）などがこれらを修正し、信頼できるバージョン2をリリースしました。

この直後に問題が発生しました。ほとんどの国で暗号化のデバイスやソフトウェアの使用や輸出が強力に制限されていたように、米国においても例外ではありませんでした。一般的には弱い暗号しか認められていませんでした。PGPは非常に強力であり、またUsenetやFTP、BBSなどで公開されたために、他国でも事故的に漏れることとなり、Philはライセンスなしの軍需品輸出のため、起訴されました。これらの輸出管理はソフトウェアの時代に追随したものではなく、印刷したソフトウェア形態は規制がないという滑稽な効果を生み出しました。MIT PressはPGPのソースコードを本で出版し、米国外でこれをスキャンし、PGP-2i（iはinternationalの意）のベースとなりました。これは広く使われることになりました。

1996年にPhilに対する犯罪捜査は終了し、彼はPGP-5を書くため、PGP Incを設立しました。最初の公開版は1997年の春にリリースされました。同年の8月に、Munichで開かれた第39回IETF会議においてPhil ZimmermannとJon CallasがIETFに対してPGP-5で使用されているプロトコルを標準として発行する作業会の設立を要請しました。この大きな目的は、強力な暗号を広めるとともに、新しい会社がPGPの販売、サポートを停止した場合においてもそれを保てるように、ということでした。現にその数ヶ月後に、PGP IncはNetwork Associateにより買収され、2002年にPGPのサポートと開発が停止されました。（ただし、その後、PGPの製品はPGP Corporationにより継続されることになります。）

PGPはフリーソフトウェアとは言われていましたが、それはそのために要求される項目を満たしたものではありませんでした。PGP-5はれっきとした私有のソフトウェアでした。ソースコードが公開されていることだけではフリーとは呼べません。PGP-2は商用利用に一定の制限があり[^3]、これによってもフリーではありませんでした。他の問題として、PGP-2は特許が存在するRSAとIDEAアルゴリズムの使用を強制するものでした。RSAの特許は米国内でのみ有効でしたが、IDEAは多くの国でまだ有効[^4]なものとなっています。

GNUプロジェクトではPGPの互換実装の必要性が数年に渡ってリストされていましたが、全ての公開鍵暗号のアルゴリズムが有効である限り、それを実装開始することは不可能でした。これは、基本的な公開鍵暗号の特許（Diffie-Hellman米国特許4200770）が1997年4月に、そしてさらに広義なHellman-Merkle特許（4218582）が期限切れになった時に変わりました。

その次の月にAachenで開催されたIndividual-Network Betriebstagung（訳注：独立ネットワーク年次会）[^5]においてBoFセッションにおいて、Richard Stallmanがヨーロッパのハッカーに公開鍵ソフトウェアを実装して欲しいと要請しました。米国の武器売買法においてGNUプロジェクトがそのようなソフトウェアを米国民が他国でそれを行ったとしても実装することができませんでした。そのため、ユニークな立場にいる、ヨーロッパのハッカーに対しGNUが暗号ソフトウェアを取りそろえるのを手伝って欲しいと頼んだわけです。

SMGLの変換ソフトウェアを書くのにつかれ、おもしろいプロジェクトがなかった私は、PGP-2のパーシングコードをRFC-1991とpgformat.txtファイルを参考にしてハックしていました。これは簡単なものでしたので、私はさらに続け、PGP-2のデータを復号し、作成するコードを仕上げることに成功しました。GNUにPGPの互換実装を行うことを伝えた後、私はその年の残りをIDEAをBlowfish、RSAをElgamalに変更した上、ストリーム暗号やその他の鍵管理を加え、コードを整理するのに費やしました。

当時、PSSTと呼ばれる、Secure Shellのフリーなバージョン（その後LSHとして知られる）の計画があり、それなりの人数がいるメーリングリストがあり、これはMartin Hamiltonにより管理されていました。Martinは寛大にg10のためのメーリングリストを設置してくれ、その旨をその（PSSTの）リストでアナウンスしてくれました。これにより最初のメンバーが加入しました。その後、私は最初のtarballを作成し、ドイツのUNIXユーザーグループのFTPサーバであるftp.guug.deにいれ、その旨をアナウンスしました。[^6]

その次の日にPeter Gutmannは/dev/randomが存在しないシステム向けに、乱数コードを提供することを申し入れてきました。これによりGnuPGを多数のプラットフォームに提供することを可能とすることになりました。その後、二ヶ月間はコードの更新及び、名称をどうするべきかということについて長い議論が交わされ、最終的にはAnand Kumriaの提案によるGnuPGに決定し、2月24日[^7]にその名称（gnupg-0.2.8）が使用されることになりました。その数日後に、Windowsにおける試験的なバージョンが公開されました。（このリリースは、Alphaシステムにおけるアライメントの問題によりログが蓄積大量に蓄積し、管理者に本当にこれをバックアップする必要があるのか、と聞かれる問題もまた解消しました。;-）

1998年7月にある程度のOpenPGPの準拠した草案がリリースされました。Matthew Skalaは新規にクリーンに仕上げたTwofishコードを提供しました。（当時、TwofishはAESの有力な候補であり、SchneierによりBlowfishの代わりとしての実装を推奨されましたが、リフェレンスコードに関して著作権の懸念がありました。）Michael RothはTriple-DES実装を提供し、その年の後半に、OpenPGPアルゴリズムの要件を満たしたものになりました。その次の年には一般的な問題が解消され、機能について議論され、それぞれの作者により他のソフトウェアよりのgpgのサポートや互換性が発表されました。

最終的に、1999年の9月7日、1.0.0が公開され、これにはMike AshleyによるGNU Privacy Handbook[^8]が含まれていました。その一年後の9月20日にRSA特許が切れる予定でしたが、その3週間前に特許保持者はそれをパブリックドメインとしたため、9月18日にはRSAサポートを含んだ1.0.3を公開することができました。暗号使用の大きな障害がまた一つ解消されたのです。（それは、かなり遅すぎました、もちろん）

また、同1999年にドイツの政府は強力な暗号は規制されず、誰でも使うことを推奨する判断を下します。これを公的にサポートするために、財務省はGnuPGをMicrosoft Windowsに移植するための資金提供[^9]を行いました。米国はそれに対して良く思わなく、規制なしに暗号のソフトウェアが配布されることに関してドイツ政府に考え直す働きかけ[^10]を試行しました。これはうまくいかず、やがて米国もその輸出ルールを緩和するしかありませんでした。

GnuPGは現在もヨーロッパにあるサーバ上で開発されていますが、この新しい米国の輸出規制により、米国内のハッカーがGnuPGの開発に寄与することができるようになりました。2001年にDavid Shawがプロジェクトに参加し、それから現在に至るまでもっともアクティブなGnuPGハッカー及び共同管理者となっています。

GnuPGが楽しいプロジェクトとして管理できる時は遠い過去のこととなり、私は現在、ほとんどのプロフェッショナルとして、GnuPGの管理や拡張を生業としています。2001年に私はGnuPGやその関連ソフトウェアの開発やサポート業務を行うフリーソフトウェア会社、g10 Codeを設立しました。そのもっともよく知られたプロジェクトは恐らく、GnuPG-2で、NewPGとしてAegyptenプロジェクトの広義としてスタートしました。Aegyptenのメインの目標として、よく知られた中ではKMailなどの他のメールクライアントにクリーンに統合できる、S/MIMEのGNU/Linux上での実装でした。2004年よりアクティブに使用されていましたが、2.0.0のリリースはわずか一年前でした。

X.509/CMS（一般的にはS/MIMEとして知られる）ソフトウェアを書くのはエレガントで相互互換性のあるOpenPGPを書くのに比べてあまりおもしろいものではありませんでした。これをマスターした後に、他のS/MIME実装とうまく機能するソフトウェアを書くのに成功しました。また私は、最近のPOSIXプラットフォームが必要であるとの意見とは違い、GnuPG-2をWindowsに移植することも可能であることがわかりました。この開発によりフリーソフトウェアをビジネスとして開発するのは実行可能であるとを見せるものとなりました。

新しいツールにより、またユーザの目から見るとS/MIMEとOpenPGPはそんなに差がないように見えるようになります。ただ、今日RSAのヨーロッパカンファレンスにおいての簡単な人気投票により、OpenPGPは世界でもっとも広く使われている暗号プロトコルということが公表された時にはスマイルせずにはいられませんでした。

GnuPGは一つのツールにしか過ぎないということを思い出してください。他にもプライバシーの問題を解決するためのツールが多数公開されています。長年プライバシーツールを書き、公開している皆さんに賛辞を述べたいと思います。

ハッピーハッキング！

文中敬称略、和訳：斉藤英樹

[原文](http://lists.gnupg.org/pipermail/gnupg-users/2007-December/032250.html)

[^1]: http://www/gnupg.org
[^2]: ftp://ftp.gnupg.org/gcrypt/historic/g10-0.0.0.tar.gz
[^3]: pgpdoc2.txtより「PGPを商業製品に変え、お金を儲けたい場合、私も儲ける方法に合意しないといけません。[…]PGPはこのPGPユーザーガイドを含む、PGPのドキュメンテーションなしに配布することができません。
[^4]: 「有効」は特許保持者がそれを行使することであり、私はソフトウェア特許が有効なコンセプトであるとは考えていません。詳しくは http://www.fsfeurope.org/projects/swpat/background.en.html
[^5]: http://www.dascon.de/IN-BT97/programm.html
[^6]: http://lists.gnupg.org/pipermail/gnupg-devel/1997-December/014131.html 12月に特許に関するいくつかのメールがあります。
[^7]: http://lists.gnupg.org/pipermail/gnupg-devel/1998-February/014208.html
[^8]: http://lists.gnupg.org/pipermail/gnupg-announce/1999q3/000037.html
[^9]: http://partners.nytimes.com/library/tech/99/11/cyber/articles/19encrypt.html
[^10]: http://www.heise.de/tp/r4/artikel/5/5124/1.html
