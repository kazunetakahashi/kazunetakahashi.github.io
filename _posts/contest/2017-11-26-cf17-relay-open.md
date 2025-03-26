---
layout: single
category: contest
tag: atcoder
title: Code Festival 2017 Team Relay
---

[Code Festival 2017 Team Relay](https://atcoder.jp/contests/cf17-relay-open)

# Source codes

- [My submissions (AtCoder)](https://atcoder.jp/contests/cf17-relay-open/submissions?f.User=kazunetakahashi)
- [My source codes (GitHub)](https://github.com/kazunetakahashi/atcoder/tree/master/2017/1129_code-fes-2017-relay)

# Solutions

寝る前につらつらやったらたくさん WA した。メモしてから寝る。あとでまた解く。

## [A - Kaiden](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_a)

基本は $(A-B) x + A \geq K$ を解いて最小値について $2x+1$ を出力すれば良いのだが、一発で超える場合と $A <= B$ の場合は異なる。

### ポイント

一発で超える場合を見逃していた。

## [B - Evergrowing Tree](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_b)

$0$-indexed として、$k$ の下には $kN+1$ から $N(k+1)$ までぶら下がる。だから $1$ を引いて $N$ で割ると親が出てくる。 $N \geq 2$ の場合はせいぜい $64$ 世代くらいだから愚直に求めればよろしい。ただし $N = 1$ の場合は小さい方が答え。

### ポイント

$N = 1$ の場合に TLE していた。

## [C - Garden](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_c)

答えの座標 $x$ を二分探索で求めることにする。 $i$ 番目の花は $x$ 以下の座標に $k$ 本植えられているとすると、 $k$ は $w_i + k d_i \leq x$ を充たす最大値である。ただし $w_i > x$ の場合は当然 $0$ である。この和が $K$ 以上かどうかを判定する。

最悪ケースはサンプルにある通りで、 `lb = 0` とし `ub = 1999999999000000000+10` とすれば十分である。

### ポイント

オーバーフローの可能性があるので、平均を求める時は $x/2 + y/2$ のようにする(余りも適切に処理する)。そして $w_i > x$ の場合を忘れないようにする。

## [D - Shock](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_d)

$0$-indexed とする。最終的なグラフは、 2 つの連結成分からなり、 $0$ を含む連結成分の完全グラフと $1$ を含む連結成分の完全グラフの無縁和である。初めから連結されている頂点はどちら側につくかは変えようがないが、問題は初めからどちらとも path がない頂点である。

> 全ての頂点からなる完全グラフの辺の数 = $0$ を含む連結成分の完全グラフ $G_0$ の辺の数 + $1$ を含む連結成分の完全グラフ $G_1$ の辺の数 + ($G_0$ と $G_1$ の間の辺の数)

であるので、最後の項が小さくなるようにする。$G_i$ の頂点の数を $n_i$ とすると、
($G_0$ と $G_1$ の間の辺の数) は $n_0 n_1$ である。そして $n_0 + n_1 = N$ の関係があるので、高校 1 年生の二次関数の知識でも使えば、 $n_0$ と $n_1$ の差が開けば開くほどこの数は小さくなる。

だから結論としては、初めからどちらとも path がない頂点は、頂点の数が多い連結成分の方に全てつける。答えは $n_0(n_0-1)/2 + n_1(n_1-1)/2 - M$ である。

### ポイント

直感的にすぐに解法がわかった。stack を pop せず手元で TLE した。

## [E - White and Blue](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_e)



### ポイント



## [F - Capture](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_f)



### ポイント



## [G - Coinage](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_g)



### ポイント



## [H - Akashic Records](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_h)



### ポイント



## [I - Nice to Meet You](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_i)



### ポイント



## [J - Indifferent](https://atcoder.jp/contests/cf17-relay-open/tasks/relay2_j)



### ポイント



# Others

いつものリレーよりずーっと難しいです。意地悪な問題も多い。もっと簡単でいいと思うんですけどね。教育的な問題が多いから練習としてやる分には良さそうですけど。

リレーってみんな AC するくらいでいいと思う。参加者なのに AC できなきゃ、嫌じゃないですか。そしてタイムを競うなら競技性も損なわれない。

これ、結果どうだったんでしょうかね。全完したチームがいたらすごいと思う。
