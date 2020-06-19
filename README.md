# PKP_Based_Cryptography

20200619

追記：ここで符号理論の常識からはみ出してみましょう。（ここからの議論は、もはや符号ではない）

PoWに依存しない方法を考えます。
通常、エラーとシンドロームが１対１の関係であるためには、エラーベクトルの重みが特定の数に決まっていなければなりません。
しかし、もしこの条件を取り除いてシンドロームと同じサイズのエラーを許せば、
部分符号の逆行列を計算するだけでどのような符号からも簡単にシンドロームに対応するエラーベクトルが決定できるかもしれない。
つまり、シンドロームと符号の特定の位置さえ決まってしまえば、それに対応するエラーベクトルを計算することは簡単だと思われます。
しかしそのような場合でも、長い符号のどの位置にそのベクトルが来るのか計算できなければ組み合わせ論的な計算爆発が起きて安全であることが保証できます。
この場合、秘密鍵はエラーの位置です。
バイナリ符号の場合は、値が変化しないのでこの方法がうまくいきそうな予感・・・。（検証はしてません）
異なる複数の符号間で１つのシンドロームに対応するエラーベクトルが生成できるかもしれない。
しかし、これではどんなベクトルであろうと答えになるので、エラーパターンのハッシュ値かHMACと併用する必要がありますね。
（これは多重線形写像だろうか?という疑問があるけど、それは自分がペアリングの一般化を理解していない証拠でもある）

例えば、３２バイトの任意のシンドローム（例えばメールアドレス）に対応するエラーベクトルを計算したいものとする。
この場合、リードソロモン符号を使うなら、このシンドロームに対応するエラーを計算するために、任意の３２個の位置から符号列を取り出す。
そうして作られた正方行列の逆行列を計算してやり、シンドロームにかけてやれば、この場合メールアドレスに対応するエラーベクトルが決まるという訳です。

しかしこの問題は符号であるという前提を無視しているので、単なる長方形をした大きな行列で計算しているのと変わりがありません。
どちらかといえばPKP（Permuted Kernel Problem）と呼ばれる問題に近いのかもしれません。
誰も格子暗号が長方形をした行列を公開鍵に持つ暗号だと言わないだけで、もしかしたらこの方法が格子に基づく暗号なのかもしれない。（ちなみに格子暗号は全く知らない）
ランダム行列に対する特定の入出力計算に関する問題になるので、結局訂正限界を無視した前提を利用するのは、符号に関する問題ではないですね。

結論：しかしこれはアフィン暗号と同じになってしまうので簡単に解読できますね。
小さな情報だけで復号できるところが符号ベースの暗号の強みというものでしょうか。
誰も格子暗号が長方形をした行列を公開鍵に持つ暗号だと言わないだけで、格子暗号みたいなものかもしれないです。
ちなみに格子暗号は全く知りません。ｗ

誰も格子暗号が長方形をした行列を公開鍵に持つ暗号だと言わないだけで、これは格子暗号の一種なのかもしれない。
で、バイナリのランダム行列を作った場合、そのバイナリ正方行列が正則である確率はかなり低い。
この実験を通して、あるバイナリ行列の特定の列を組み合わせた時だけ逆行列を計算できるようにトラップドアを仕掛けておく。
そしてその組み合わせの位置を知っている人だけが、メッセージを復元できるようにするというのもアイデアになる。
