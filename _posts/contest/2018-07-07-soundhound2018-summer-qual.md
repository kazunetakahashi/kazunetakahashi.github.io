---
layout: single
category: contest
tag: atcoder
title: SoundHound Inc. Programming Contest 2018 -Masters Tournament-
---

[SoundHound Inc. Programming Contest 2018 -Masters Tournament-](https://atcoder.jp/contests/soundhound2018-summer-qual)

# Source codes

- [My submissions (AtCoder)](https://atcoder.jp/contests/soundhound2018-summer-qual/submissions?f.User=kazunetakahashi)
- [My source codes (GitHub)](https://github.com/kazunetakahashi/atcoder/tree/master/2018/0707_soundhound2018-summer-qual)

# Solutions

## [A - F](https://atcoder.jp/contests/soundhound2018-summer-qual/tasks/soundhound2018_summer_qual_a)

問題文の指定通りにやるだけである。

## [B - Acrostic](https://atcoder.jp/contests/soundhound2018-summer-qual/tasks/soundhound2018_summer_qual_b)

改行を実際にする必要はない。 $i = 0$ からスタートして $i < \lvert S \rvert$ である限り $S[i]$ 文字目を取り出し $i += w$ とする。

## [C - Ordinary Beauty](https://atcoder.jp/contests/soundhound2018-summer-qual/tasks/soundhound2018_summer_qual_c)

最初の $2$ 文字が美しい文字列は $d = 0$ の時 $n \cdot n^{m-2}$ 個あるし、 $d > 0$ の時は $2 (n - d) \cdot n^{m-2}$ 個ある。期待値の和は和の期待値を用いて、あとはこれに $(m - 1)$ をかけて $n^m$ で割る。

## [D - Saving Snuuk](https://atcoder.jp/contests/soundhound2018-summer-qual/tasks/soundhound2018_summer_qual_d)

都市を頂点として扱いたいのだが、円をスヌークに両替したあとは「世界」をシフト(ワープ)して、別の頂点に移動し、もう戻ってこれないものとみなすことにする。すると「円」の世界で $S$ から各都市への最短距離を求めておき、「スヌーク」の世界で各都市から $T$ への最短距離を求めておけば( $T$ から各頂点へ求めれば良い)、それぞれの都市についてそれらの和を取れば、その都市で両替した場合の最短距離が求まる。あとは imos 法で $\min$ をとる。

### ポイント

問題文が妙に複雑で作為をごまかしているように思う。 $10^{15}$ から引いた値を出力するのは美しくない。

## [E - + Graph](https://atcoder.jp/contests/soundhound2018-summer-qual/tasks/soundhound2018_summer_qual_e)

連結グラフであるから、ある頂点に $x$ という数字を書くと他の頂点に書くべき数字は決まる。問題は $x$ を書けるかどうか、その範囲、その値の決定ということになる。そこで `tuple<bool, ll> I` で多項式 $\pm x + v$ を持つことにする。基本的には BFS して多項式を決定していく。まだ訪れていない点に $\mp x + (w - v)$ を持たせる。問題は訪れている点同士に張られた辺である。これは以下のように場合分けされる。

- $\pm x + v\_1$ と $\pm x + v\_2$ に $w$ が張られている場合
  - $x = (w - v\_1 - v\_2) / \pm 2$ と決まる。これが正の整数でなければ答えは $0$ である。
  - こいつを `set<ll> value` へ入れておく。ここに $2$ 個以上の数が入ったら答えは $0$ である。
- $\pm x + v\_1$ と $\mp x + v\_2$ に $w$ が張られている場合
  - $v\_1 + v\_2 = w$ でなければ答えは $0$ である。

ここまでクリアし、全てが終わったとする。この時 $A = \min \\{ v \in \mathbb{Z} \mid x + v \\}$, $B = \min \\{ v \in \mathbb{Z} \mid -x + v \\}$ とし $A \gets \max(0, -A)$ とする。ここでも場合分けが生じる。

- `value` が値を $1$ 個含む場合
  - $A < x < B$ であれば答えは $1$ であり、それ以外は答えは $0$ である。
- 含まない場合
  - $A \geq B$ または $B \leq 1$ の時は答えは $0$ であり、それ以外は $A < x < B$ を充たす全ての $x \in \mathbb{Z}$ の個数が答えになる。つまり $B - A - 1$ である。

### ポイント

6WA も出してしまった。「これが正の整数でなければ答えは $0$ である」を正しく処理できていなかった。これだけ場合分けがあるとなかなか大変である。

# Others

```
A - sample: 3, tle: 2.000, time: 02:09, from_submit: 60:58
B - sample: 3, tle: 2.000, time: 02:16, from_submit: 56:03
C - sample: 2, tle: 2.000, time: 08:22, from_submit: 47:40
D - sample: 2, tle: 2.000, time: 23:36, from_submit: 24:04
E - sample: 3, tle: 2.000, time: 63:58, from_submit: 00:00
```

やっぱり前から順番に解こうかな。
