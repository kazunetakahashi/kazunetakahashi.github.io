---
layout: single
category: contest
tag: atcoder
title: 「みんなのプロコン 2019」
---

[「みんなのプロコン 2019」](https://atcoder.jp/contests/yahoo-procon2019-qual)

# Source codes

- [My submissions (AtCoder)](https://atcoder.jp/contests/yahoo-procon2019-qual/submissions?f.User=kazunetakahashi)
- [My source codes (GitHub)](https://github.com/kazunetakahashi/atcoder/tree/master/2019/0209_yahoo-procon2019-qual)

# Solutions

## [A - Anti-Adjacency](https://atcoder.jp/contests/yahoo-procon2019-qual/tasks/yahoo_procon2019_qual_a)

### コンテスト中に取った解法

1 個飛ばしに真面目に取っていった。

### 模範解答

$K$ 個の整数を $1$ つ飛ばしでとると、最大値と最小値の差は $2(K - 1)$ である。ゆえに $2(K - 1) \leq N - 1$ であるかどうかを判定すれば良い。

## [B - Path](https://atcoder.jp/contests/yahoo-procon2019-qual/tasks/yahoo_procon2019_qual_b)

オイラーの一筆書きの定理より、一筆書きができる必要十分条件は、次数が奇数の頂点が $0$ 個か $2$ 個であることである。

頂点が $4$ つの木は、同型を除いて $2$ 種類しかない。そのうち一筆書きができるものは、次数が $3$ の頂点を含まないものである。ゆえに、 multiset $\\{ a _ i, b _ i \\} _ {i = 0, 1, 2}$ で個数を数えれば良い。

## [C - When I hit my pocket...](https://atcoder.jp/contests/yahoo-procon2019-qual/tasks/yahoo_procon2019_qual_c)

まず $B - A \leq 2$ の場合は、ビスケットを愚直に増やすことが最善である。よって答えは $K + 1$ である。そうでない場合は、 $A$ 個までは愚直に増やして、あとは日本円を経由して $A$ 個を $B$ 個に変換するのが最善である。この回数を $x$ とすると、制約条件は $A - 1 + 2x \leq K$ である。 $x$ の最大値は $x = (K - (A - 1)) / 2$ である。ここで $x \leq 0$ ならば答えは $K + 1$ である。そうでないならば答えは $A + x(B - A)$ である、といきたいが、実際はもう $1$ 個増やせる可能性がある。つまり $K - (A - 1) + 2x = 1$ のときはもう $1$ ターン残っているから答えに $1$ を更に足す。

## [D - Ears](https://atcoder.jp/contests/yahoo-procon2019-qual/tasks/yahoo_procon2019_qual_d)

### コンテスト中の解法 (TLE)

散歩の仕方は $0 \leq a \leq b \leq c \leq d \leq L$ を充たす $(a, b, c, d)$ に対し、

- $[0, a)$ は徘徊しない
- $[a, b)$ は $2$ 以上偶数回数通る
- $[b, c)$ は 奇数回数通る
- $[c, d)$ は $2$ 以上偶数回数通る
- $[d, L)$ は徘徊しない

というものにまとめられる。よって累積和を使うとこの問題は $O(L^4)$ で解ける。この解法を投げたら TLE で返ってきたので間違いではない。

### 模範解答

$I _ 0 = [0, a)$, $I _ 1 = [a, b)$, $I _ 2 = [b, c)$, $I _ 3 = [c, d)$, $I _ 4 = [d, L)$ とする。

> $DP[i][j] = $ 区間 $[0, i)$ まで見たとき、区間 $I _ j$ にいる状態での最小値

とする。初期状態は、
\\[
  DP[0][0] = DP[0][1] = DP[0][2] = DP[0][3] = DP[0][4] = 0.
\\]
答えは
\\[
  \min(DP[L][0], DP[L][1], DP[L][2], DP[L][3], DP[L][4])
\\]
である。遷移は以下の通り。まず、 $f, g \colon \mathbb{N} \to \mathbb{N}$ を
\\[
  \begin{align}
    f(n) &=
    \begin{cases}
      2 & (n = 0), \\\\\
      n \\% 2 & (n \geq 1),
    \end{cases} \\\\\
    g(n) &= (n + 1) \\% 2
  \end{align}
\\]
と定める。 $i = 0, \dots, L - 1$ に対し、以下を順次実行する。
\\[
  \begin{align}
    mini &\gets DP[i][0], \\\\\
    DP[i + 1][0] &\gets mini + A[i], \\\\\
    mini &\gets \min(DP[i][1], mini), \\\\\
    DP[i + 1][1] &\gets mini + f(A[i]), \\\\\
    mini &\gets \min(DP[i][2], mini), \\\\\
    DP[i + 1][2] &\gets mini + g(A[i]), \\\\\
    mini &\gets \min(DP[i][3], mini), \\\\\
    DP[i + 1][3] &\gets mini + f(A[i]), \\\\\
    mini &\gets \min(DP[i][4], mini), \\\\\
    DP[i + 1][4] &\gets mini + A[i].
  \end{align}
\\]

### ポイント

あとは区間とみなして DP するだけだった。いやぁ。

## [E - Odd Subrectangles](https://atcoder.jp/contests/yahoo-procon2019-qual/tasks/yahoo_procon2019_qual_e)



### ポイント



## [F - Pass](https://atcoder.jp/contests/yahoo-procon2019-qual/tasks/yahoo_procon2019_qual_f)

### 部分問題

$1$-indexed とする。

> $DP[i][j] = i$ 番目までの操作で高橋君が手にしている可能性があるボールの列の場合の数のうち、赤色のボールは $j$ 個あるもの。

と定める。これを $i = 0, \dots, N$ で求めるという部分問題を考える。

$i$ 番目までの操作で高橋君が手にすることのできるボールは、 $i$ 番目までのすぬけ君が初期状態で持っている任意のボールである。したがって以下を計算しておく。

> $R[i] = i$ 番目までのすぬけ君が持っている赤ボールの総数、<br>
> $B[i] = i$ 番目までのすぬけ君が持っている青ボールの総数。

これは前から容易に計算できる。

さて $DP$ の計算に移る。初期状態は $DP[0][0] = 1$ である。遷移は以下の通り。$i = 0, \dots, N - 1$ に対し、 $j = 0, \dots, i$ に対し、まず $r = j$, $b = i - j$ とする。すると $R[i + 1] - r > 0$ の場合は、その後ろに赤ボールを接続できるので、
\\[
  DP[i + 1][j + 1] += DP[i][j]
\\]
とする。同様に $B[i + 1] - b > 0$ の場合は、
\\[
  DP[i + 1][j] += DP[i][j]
\\]
とする。これで求まる。

### 解答

$j = 0, \dots, N$ に対し、 $X[j] = R[N] - j$, $Y[j] = B[N] - (N - j)$ とする。つまり $DP[N][j]$ の後ろに $X[j]$ 個の赤ボールと $Y[j]$ 個の青ボールを接続することになるから、答えは以下で求まる。
\\[
  \sum _ {j = 0} ^ N \begin{pmatrix} X[j] + Y[j] \\\\ X[j] \end{pmatrix} DP[N][j].
\\]
ただし、組み合わせ数は $\begin{pmatrix} n \\\\ k \end{pmatrix}$ は $n < 0$ または $k < 0$ または $n - k < 0$ の場合は $0$ を出力するように規約したものとする。

### ポイント

配る DP なので、 $DP[i][j] = 0$ の時は `continue;` するべきである。

記録を見ると 30 分くらいで答えを出しています。 900 点とは思えないくらい簡単だった。

# Others

```
A - sample: 4, tle: 2.000, time: 02:43, from_submit: 113:42
B - sample: 3, tle: 2.000, time: 02:15, from_submit: 111:27
C - sample: 3, tle: 2.000, time: 09:52, from_submit: 101:35
D - sample: 3, tle: 2.000, time: 70:59, from_submit: 30:36
E - sample: 2, tle: 2.000, time: 00:00
F - sample: 3, tle: 2.000, time: 30:36, from_submit: 00:00
```

今まで `#define DEBUG 1` を活用していなかったので、これを自動提出機能にも及ぼすようにした。つまり文頭にある `#define DEBUG 1` を `#define DEBUG 0` に自動的に変更してから提出できるようにした。これで `cerr` をコメントアウトする必要がなくなる。
