---
layout: single
category: contest
tag: atcoder
title: COLOCON -Colopl programming contest 2018- Final
---

[COLOCON -Colopl programming contest 2018- Final（オープンコンテスト）](https://atcoder.jp/contests/colopl2018-final-open)

# Source codes

- [My submissions (AtCoder)](https://atcoder.jp/contests/colopl2018-final-open/submissions?f.User=kazunetakahashi)
- [My source codes (GitHub)](https://github.com/kazunetakahashi/atcoder/tree/master/2018/0120_colopl2018-final)

エントリがどんどん長くなっているよ。どうしてくれる…

# Solutions

## [A - ファイティング・タカハシ](https://atcoder.jp/contests/colopl2018-final-open/tasks/colopl2018_final_a)

全部 `A` なら $m = \| S \| \cdot N$ として $m(m+1)/2$ である。

そうでない場合は、得点は $K (N-1) + L$ の形になるはずなので、$N = 1$ として $L$ を求め、 $N = 2$ として $K + L$ を求める。

### ポイント

square869120Contest #4 の [C - Calendar 2](https://s8pc-4.contest.atcoder.jp/tasks/s8pc_4_c) の解法を覚えていたのでこれにたどり着いた。

## [B - 異世界数式](https://atcoder.jp/contests/colopl2018-final-open/tasks/colopl2018_final_b)

これは難しかったです。正しい文字列を出すだけなら、以下のコードで問題はない。

``` ruby
def henkan(str)
  op = str[0]
  if !['+', '-', '*', '/'].include?(op)
    return str
  end
  naka = str[2..-2]
  cnt = 0
  for i in 0...naka.size # ここから
    if naka[i] == '('
      cnt += 1
    elsif naka[i] == ')'
      cnt -= 1
    elsif naka[i] == ',' && cnt == 0
      naka[i] = '@'
    end
  end # ここまで
  ary = naka.split('@')
  for i in 0...ary.size
    ary[i] = henkan(ary[i])
  end
  return '(' + ary.join(op) + ')'
end
```

しかしこれだと「ここからここまで」のところで文字列を走査しているので、 $N$ を文字列のサイズとして $O(N^2)$ になってしまう。だから TLE になる。恐ろしい。

オーダーを落とすには、カンマ `,` の depth をあらかじめ調査しておくことである。 depth ごとにカンマの位置を set で持っておいて、 `lower_bound` で取り出してくる。そうすれば「重複なく」取り出せている。

最悪オーダーは $O(N \log N)$ だが、実際のところは depth とカンマの数は綱引きになるので、計算量はずっと小さいはずである。

### ポイント

よーく思い出してみると、実践的プログラミングの授業でも、 $S$ をグローバス変数で持っておいて $S[l, r)$ を評価するように関数を書いていたのだった。その基本に忠実に行動するべきだった。

## [C - スペースエクスプローラー高橋君](https://atcoder.jp/contests/colopl2018-final-open/tasks/colopl2018_final_c)

### 直後のコメント

わかりませんでした。 $b_k = a_k - a_{k-1}$ としておけば、

- $\min_{l} \{ \sum_{k=1}^l b_k \}$ の最小値を求める
- 全部の $b_k$ に $-2$ をする

の両方の操作を $O(\log N)$ でできるような構造があれば勝ちなのはわかったのだが。

### 正しい方法がわかった

これは Convex Hull Trick と呼ばれる典型手法に帰着されるとのことでした。順番に説明する。以下が参考文献：

- [hamayanhamayan's blog](http://hamayanhamayan.hatenablog.jp/entry/2018/01/21/161336) 公式の解説がないので非常に助かりました。これがなかったら私は終わっていた。感謝。
- [競技プログラミング+αなブログ](http://d.hatena.ne.jp/sune2/20140310/1394440369) プログラミングコンテストチャレンジブックの該当箇所がわかった。
- プログラミングコンテストチャレンジブック 第2版 p.306。以下では図を描いてないが、 p.305 に描いてあるのでそれを見るとわかりやすい。

### Convex Hull Trick とは

一次関数の集合 $\\{ f_j(x) = K_j x + L_j \\}$ と点の集合 $\\{ x_i \\}$ に対し $F(x_i) = \min_{j} f_j(x_i)$ を求めよという問題。一次関数の集合は *傾きが広義単調減少になるように* 追加されていき、 $F(x_i)$ は *値が小さい順* $x_0 \leq x_1 \leq x_2 \leq \dots$ のように走査されていくと仮定する。

`deque<int> Q` の中に、「今後最小値をとりえる一次関数の添字 $j$」を入れて管理していく。関数の挿入は後ろに挿入、値は先頭をみる。常に $K_{Q[j]} \geq K_{Q[j+1]}$ が成立している。

#### 関数を挿入する際

今から挿入する関数を $f_3 (x) = K_3 x + L_3$ とする。 $K_3$ は今までで一番傾きが小さいので、十分大きな $x$ に対しては $F(x) = f_3(x)$ にこの時点ではなる。だからこれは $Q$ の中には入らないといけない。ところがこいつが $Q$ の中にはいると、さっきまで後ろにいた人がクビになる可能性がある。末尾の関数を $f_2(x) = K_2 x + L_2$ とする。そのさらに 1 つ前の関数を $f_1(x) = K_1 x + L_1$ とする。この時、 $f_2 \geq \min(f_1, f_3)$ となっている可能性がある。この場合 $f_2$ を取り除く。

まずは $K_1 > K_2 > K_3$ としてこの条件を計算する。この時の条件は、 $f_1, f_3$ の交点 $(x_0, f_1(x_0))$ において $f_2(x_0) \geq f_1(x_0)$ が成立していることと同値である。 $x_0$ は $x_0 = (L_3 - L_1)/(K_1 - K_3)$ と求まる。 $f_2(x_0) \geq f_1(x_0)$ を計算して分母を払うと、これは

\\[ (K_1 - K_2)(L_3 - L_1) + (K_1 - K_3)(L_1 - L_2) \leq 0 \\]

と同値であることがわかる。 $K_1 = K_2$ の場合と $K_2 = K_3$ の場合もこれで大丈夫である。

`Q.size() >= 2` かつこの条件が満たされている限り末尾を削除していく。終わったら $f_3$ を挿入すればよろしい。

#### 値を求める際

上記のように直線を挿入し続けると値を求めたい $x$ に対しては

\\[ f_1(x) \geq f_2(x) \geq \dots \geq f_i(x) < f_{i+1}(x) \leq \dots \\]

となっており、さらに任意の $x' \geq x$ に対しても

\\[ f_1(x') \geq f_2(x') \geq \dots \geq f_i(x') \\]

となるしかない。前者の $i$ 番目以降は挿入の仕方により保証される。つまり隣同士の関数の交点がだんだん大きくなるように挿入していっているから。後者は $K_1 \geq K_2 \geq \dots$ によるのである。すなわち、今、そして今後は $f_1, \dots f_{i-1}$ は使用しないので、こいつは削除して良い。実装としては、 `Q.size() >= 2` である限り、先頭 $f_1$ 、その次 $f_2$ に対し $f_1(x) \geq f_2(x)$ になっていれば $f_1$ を削除するのを繰り返す。そうして先頭の $f$ に対し $f(x)$ を求めればよろしい。

詳しい実装は プログラミングコンテストチャレンジブック 第2版 p.306 を参照。

### この問題では

この問題は要するに $0 \leq i < N$ に対し $A_i = \min_j \left( a_j + (j - i)^2 \right)$ を求めよという問題である。ここで

\\[ A_i = \min_j \left( a_j + (j - i)^2 \right) = i^2 + \min_j \left(-2 ji + (a_j + j^2) \right) \\]

であることを考慮すると、 $K_j = -2j$, $L_j = a_j + j^2$ とすれば、 Convex Hull Trick で回答ができる。最初に全部挿入していき(そのまま入れるだけで単調減少)、あとは $x = 0, \dots, N-1$ まで全て求めれば良い。

### ポイント

知っていないとできないと思う。典型問題。

## [D - Chaos of the Snuke World](https://atcoder.jp/contests/colopl2018-final-open/tasks/colopl2018_final_d)

この問題は、石板の置き方を決める問題と、計算する問題に分かれる。それぞれ解く。

### 石板の置き方

$A_i \leq B_i$ として一般性を失わない。 $a$ と $b$ の書かれた石板を $(a, b)$ と書くことにする。以下のこの仮定を入れて解く。次の補題を示す：

> **補題**：
> 「隣り合う石板同士を入れ替える操作の必要回数の期待値が最小になる」ような石板の初期配置は $B_i$ が大きくなる順番に並べたものである。すなわち、次の DP パートにおいて $B_0 \leq B_1 \leq \dots \leq B_{N-1}$ を仮定してよい。

証明はいつもの奴を使う。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">私は普段無限を真正面から扱うから、最小値とか臨界値とかあること自体が問題になるんだけど、コンテストの問題は最適解が必ず(得てして複数)あるから、「ある最適解がある global な性質を持つ」を示すには「最適解を取ったときに、仮に local にその性質を持たないとすると、</p>&mdash; Kazune Takahashi (@kazunetakahashi) <a href="https://twitter.com/kazunetakahashi/status/934336005322129408?ref_src=twsrc%5Etfw">2017年11月25日</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">持つように変換すると、さらに良くなっているから、それも最適解」という論法が使える。昨年のクッキー食べる問題もこれで証明がなされる。今年の D はさらに飛躍しているけれども、やはりこれで解法の正当性が証明ができる。</p>&mdash; Kazune Takahashi (@kazunetakahashi) <a href="https://twitter.com/kazunetakahashi/status/934336302685622272?ref_src=twsrc%5Etfw">2017年11月25日</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

すなわち、ある部分で $(a, b)$ の右隣に $(c, d)$ があって、 $a \leq b$ かつ $c \leq d$ かつ $b > d$ を充すものとし、しかもこれが最善を与えていると仮定する。この置き方が、本来の置き方、すなわち $(c, d)$ の右隣に $(a, b)$ があるような置き方に比べて、どのくらい損をするのかを検証する。

「和の期待値は期待値の和」を用いると、結局他の場所がどのようになっていようと、この 2 枚の入れ替えが必要かどうかは、ここだけで決まっていることに注意されたい。

面が $b$ と $d$ の場合(面倒だからこういうのを $b \mapsto d$ などと書く)は、入れ替えが必要で、期待値は $1/4$ だけ損をする(大きくなる)。 $b \mapsto c$ も $1/4$ だけ損をしている。この時点で絶対得をしないのはわかるのだが、理解しにくい場所なので場合分けをして完全に示す。

- $c \leq d \leq a \leq b$ のとき： $a \mapsto d$, $a \mapsto c$ はどちらもそれぞれ $1/4$ だけ損をするか、イコールで損得 $\pm 0$ である。
- $c \leq a \leq d \leq b$ のとき： $a \mapsto d$ は $1/4$ だけ得をするか、イコールで損得 $0$ である。 $a \mapsto c$ は $1/4$ だけ損をするか、イコールで損得 $\pm 0$ である。
- $a \leq c \leq d \leq b$ のとき： $a \mapsto d$, $a \mapsto c$ はどちらもそれぞれ $1/4$ だけ得をするか、イコールで損得 $\pm 0$ である。

最善を与えているという仮定から、最後のやつだけしかありえない。しかしその場合も swap 回数の期待値が減ることにはならなかった( $1/4 + 1/4 - 1/4 - 1/4 = 0$ だから)。ゆえに、「ある部分で $(a, b)$ の右隣に $(c, d)$ があって、 $a \leq b$ かつ $c \leq d$ かつ $b > d$ を充すもの」が最善ならば、$(c, d)$ の右隣に $(a, b)$ があるようにそこだけ変更したものも最善を与えている。したがって補題が示された。

### 総和の計算をするところ

まず求めるものは、期待値の $2^N$ 倍である。これは要するに、列の総和 $2^N$ 通りの swap 数の総和である。

後から必要なくなるのだが、考察しやすいように DP でやる。 $\text{DP}[i]$ を $i$ 番目までの部分列の swap 数の総和とする。

$i$ 番目の総和を求める。まず $B_i$ の方が表の場合、この板は動かさなくてよろしい。だからこの場合の総和は、 $\text{DP}[i-1]$ である。 $A_i$ の方が表の場合、この場合は、まず$[0, i-1]$ の区間をまずソートしてから、そのあとで $A_i$ を動かすと考えてよろしい。だからまず $\text{DP}[i-1]$ が足される。ここから先は「和の期待値は期待値の和」を用いていく(まぁ今総和を求めているんだけども)。 $S = \\{ A_0, B_0, A_1, B_1, \dots, A_{i-1}, B_{i-1} \\}$ とする(重複も区別する)。$S$ の元のうち $A_i$ 以下の数とは swap しない。$S$ の元のうち $A_i$ よりも大きい数は必ず swap する。そのような数と swap するのは、総和にどのように影響しているかというと、その数が表になる場合の数だけ、その数と swap しているはずである。場合の数は $2^{i-1}$ である。だからその個数を $K$ とすると結局遷移は

\\[ \text{DP}[i] = 2 \cdot \text{DP}[i-1] + K \cdot 2^{i-1} \\]

である。答えは $\text{DP}[N-1]$ である。直前だけ覚えておけばいいので DP はいらない。

そしてどうやって $K$ を求めるかということになる。これは RSQ で答えられる。親切にもすでに座標圧縮がかかっているので $1$ から $2N+1$ の BIT を用意する。次に遷移する前に、座標 $A_i$, $B_i$ に $1$ だけ add する。そこまででできた $A_i$ よりも大きい数は `sum(A[i]+1, 2N+1)` で求まる。

### ポイント

後半は簡単だが、前半を自力で思いつくのは非常に難しい。この手の証明が必要なやつは必ず難しい。後半は ARC か AGC のどこかで **multiset では upper_bound 以上の数を $O(\log N)$ で答えられないけど bit で 1 個ずつ足していけば RSQ でできる** というのを見ていたので自力でクリアできた。調べたら ARC075 [E - Meaningful Mean](https://arc075.contest.atcoder.jp/tasks/arc075_c) だった。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">E: b_{i+1} = \sum_{k = 0}^{i} a_i として multiset に後ろから追加して b_i 以上の元がいくつあるのかを求める……でいいと思ったんだけど multiset に「引数以上の元がいくつあるか」というメソッドが無くて死亡</p>&mdash; Kazune Takahashi (@kazunetakahashi) <a href="https://twitter.com/kazunetakahashi/status/871000779028443137?ref_src=twsrc%5Etfw">2017年6月3日</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">なるほど。今回は大小だけだから、座標圧縮して、個数を持っておけばいいのか。BIT でできると。頑張って思いつきたかった……</p>&mdash; Kazune Takahashi (@kazunetakahashi) <a href="https://twitter.com/kazunetakahashi/status/871003759496667137?ref_src=twsrc%5Etfw">2017年6月3日</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

今回は思いつけたよ！ (まぁコンテスト時間は終わっているんだけど…)

## [E - キャプテン・タカハシ](https://atcoder.jp/contests/colopl2018-final-open/tasks/colopl2018_final_e)



### ポイント



## [F - 高橋くんの帰還](https://atcoder.jp/contests/colopl2018-final-open/tasks/colopl2018_final_f)



### ポイント



# Others
