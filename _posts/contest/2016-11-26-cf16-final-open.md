---
layout: single
category: contest
tag: atcoder
title: CODE FESTIVAL 2016 Final
---

[CODE FESTIVAL 2016 Final](https://atcoder.jp/contests/cf16-final-open)

模擬試験として 1 年ぶりにやってみました。

# Source codes

- [My submissions (AtCoder)](https://atcoder.jp/contests/cf16-final-open/submissions?f.User=kazunetakahashi)
- [My source codes (GitHub)](https://github.com/kazunetakahashi/atcoder/tree/master/2017/1124_code-fes-2016-final)

# Solutions

## [A - Where's Snuke?](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_a)

やるだけ。

## [B - Exactly N points](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_b)

貪欲に選ぶだけ。

## [C - Interpretation](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_c)

頂点＝言語と人、辺＝人が話せる言語、とし、人の頂点が連結かどうかを判定する。

## [D - Pair Cards](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_d)

基本的には $\mathrm{mod}~M$ でカードを分類し貪欲法とする。ただし、ペアに作れるものはできるだけ使わないようにする。そうして $i$ と $M-i$ のマッチングが終わった後にはペアを作る。

### ポイント

慎重にやらないと WA する(別にペナルティないから WA してもいいのだが)。 $0$ と $M/2$ のマッチングだけ別にしないといけないのだが、そこの処理をミスした。 1 年前より退化している…

## [E - Cookies](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_e)

食べる回数をまず決める。 $x_1, x_2, \dots, x_n$ 秒ずつ待って食べると $x_1 \cdot \dots  \cdot x_n$ のクッキーが手に入り、かかる時間は $x_1 + \dots + x_n + (n-1)K$ 秒である。クッキーが $N$ 個を超えていれば実現可能な方法である。

$x_i$ たちは、なるべく均等にするとうまくいく。その証明： $x_i - x_j >= 2$ となる $(i, j)$ が存在するとする。この時 $(x_i - 1)$ と $(x_j + 1)$ に置き換えると、かかる時間は同じでクッキーの数が増える。だからこれが最適解であるとするならば、そのように置き換えたものも必ず最適解になるはずである。よって全ての $(i, j)$ に対し $\lvert x_i - x_j \rvert \leq 1$ として差し支えない。並べ替えも結果に影響しないので、結局 $a = x_1 = x_2 = \dots x_i < x_{i+1} = x_{i+2} = \dots = x_n = a+1$ の場合だけ考察すればよろしい。 $a$ はほとんど $N$ の $n$ 乗根みたいなものである。

### ポイント

オーバーフローに苦しんだ。 $3$ 乗根以上は $0$ から順に試した。 $10^4$ くらいで終わるし。

1 年前の私は冴えていた。Ruby を使って $n$ 乗根を計算していた。

## [F - Road of the King](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_f)

DP する。まず $1$ から全ての国を回らないとゲームオーバーである。回った国のうち、 1 に戻れる国は、 $1$ から行ける国、つまり、今までと今後周る国全てに行けることになる。逆に 1 に戻れない国はアウトである。

旅行の途中の様子を考察する。すると、それまで訪れた国を順に並べると、あるところまでは 1 に戻れる(1 を含む強連結成分)。しかしあるところを境に戻れなくなる。

$dp[d][i][j]$ を $d$ 日目に (1 を含む頂点の強連結成分が $i$ 頂点) かつ (そうでないけど訪れた頂点が $j$ 頂点) となっている場合の数と定義する。

わかりやすくするため、 $j > 0$ すなわち、今は $1$ を含む強連結成分を構成する頂点にはいないことにする。すると、ここから今まで訪れたことのない頂点に行くのは

\\[ dp[d+1][i][j+1] += dp[d][i][j] \times (N - i - j) \\]

と遷移することになる。同様に、今まで訪れたことがあるけど強連結成分に属していない頂点に行くのは

\\[ dp[d+1][i][j] += dp[d][i][j] \times j \\]

と遷移し、強連結成分に属している頂点に行くのは、今までのものが全部強連結成分に入るので、

\\[ dp[d+1][i+j][0] += dp[d][i][j] \times i \\]

と遷移する。以上は $j = 0$ でも正しいので、これを DP すればよろしい。 $dp[0][1][0] = 1$ が初期状態で、 $dp[M][N][0]$ が答え。

計算量は $N \approx M \approx 300$ で $O(N^3)$ なので、これはかなりきついのだが、実際は計算しなくていいセルがあって、しかも計算自体が単純なので、十分間に合う。

### ポイント

chokudai さんの解説が印象に残っていた。次の問題もそうだ。復習するときに、誰かに解説してもらうとやっぱり勉強になる。綺麗な DP だと思ったものだ。

## [G - Zigzag MST](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_g)

グラフの張替えを行う。クラスカル法のアルゴリズムにより、ジグザグに張らなくてよろしい。辺は $(\text{cost}, v, w)$ で書くことにする。 $(C, A, B)$ を張ったら、あとは $(C+1, A, A+1)$、$(C+3, A+1, A+2)$、…を張って行けばよろしい。

$(C, A, B)$ は真面目に張る。 $(C+1, A, A+1)$ と $(C+2, B, B+1)$ は別枠で所持しておく。最小のコストのものを所持しておく。別枠で所持した分を $(X, A, A+1) \mapsto (X+2, A+1, A+2)$ と遷移して最小値をとる作業を 2 周(実装では 3 周が安全)しておく。こうやって残った辺だけ追加する。あとは Union-Find でクラスカル法。

### ポイント

$\mathrm{mod}~N$ の処理でミスして 1WA した。

## [H - Tokaido](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_h)

これは部分点はとりたかった。あとで復習する。

### ポイント



## [I - Reverse Grid](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_i)



### ポイント



## [J - Neue Spiel](https://atcoder.jp/contests/cf16-final-open/tasks/codefestival_2016_final_j)



### ポイント



# Others

解説を覚えていただけだとも言えるが、本番より 2 問多く解くことができた。

Code Festival は素晴らしい問題が多いと思う。実装はあっさり、アルゴリズムは有名なものばかり、だけど、一捻りが効いていて、そこを本番で突破することを求められる。「面白い。実に興味深い」Code Thanks Festival 本番では「初歩的なことだ、友よ」ができるように祈る。
