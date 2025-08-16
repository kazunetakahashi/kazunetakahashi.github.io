---
layout: single
category: contest
tag: atcoder
title: CODE FESTIVAL 2017 qual C
---

[CODE FESTIVAL 2017 qual C](https://atcoder.jp/contests/code-festival-2017-qualc)

# Source codes

- [My submissions (AtCoder)](https://atcoder.jp/contests/code-festival-2017-qualc/submissions?f.User=kazunetakahashi)
- [My source codes (GitHub)](https://github.com/kazunetakahashi/atcoder/tree/master/2017/1021_CF2017-qualC)

# Solutions

## [A - Can you get AC?](https://atcoder.jp/contests/code-festival-2017-qualc/tasks/code_festival_2017_qualc_a)

やるだけ。 `include?` を使うだけ。

## [B - Similar Arrays](https://atcoder.jp/contests/code-festival-2017-qualc/tasks/code_festival_2017_qualc_b)

確率で言うところの余事象を取る。

## [C - Inserting 'x'](https://atcoder.jp/contests/code-festival-2017-qualc/tasks/code_festival_2017_qualc_c)

これもやるだけ。 `left++`, `right--` する。

## [D - Yet Another Palindrome Partitioning](https://atcoder.jp/contests/code-festival-2017-qualc/tasks/code_festival_2017_qualc_d)

まず、区間 $[l, r)$ が回文をなす条件は、 $[l, r)$ に含まれる文字種別の個数が「全て偶数個」であるか「1つだけ奇数個」である。これを bit がたつかたたないかに置き換えることにする。つまり、区間$[0, l)$ に奇数個の文字が入っている時に bit をたたせることにすると、$[0, l)$ の bit と $[0, r)$ の bit の bitwise xor を取った時に立っている bit の個数が 0 か 1 であることに条件が置き換えられる。

`map<int, int> SS` を $SS[bit] = $ bit を bit とする点での **最小分割数** とする。$dp[i]$ を $[0, i)$ の最小分割数として、更新していく。

### ポイント

惜しかった。方針はぼぼ正解でした。わかっていなかったのは最小分割数のところ。最小分割数を直接持っておけばよかったんだ。何を忘れて良いかをしっかり考察すれば、こんな簡単なところでは引っかからないはずなのだ…
ここで謎の貪欲法を発動し、最初に bit を達成した点だと思ってしまっていた。
これは間違いだった。自力で気づくにはテスターが必要だったように思う。

やっぱり dp は苦手ですね。

## [E - Cubes](https://atcoder.jp/contests/code-festival-2017-qualc/tasks/code_festival_2017_qualc_e)



### ポイント



## [F - Three Gluttons](https://atcoder.jp/contests/code-festival-2017-qualc/tasks/code_festival_2017_qualc_f)



### ポイント

# Others

```
A - sample: 5, tle: 2.000, time: 01:08, from_submit: 135:52
B - sample: 4, tle: 2.000, time: 04:09, from_submit: 131:42
C - sample: 4, tle: 2.000, time: 12:52, from_submit: 118:51
D - sample: 4, tle: 3.000, time: 118:51, from_submit: 00:00
E - sample: 6, tle: 2.000, time: 00:00
F - sample: 5, tle: 2.000, time: 00:00
```

予選通過ならずだろう。もしかしたら Code Thanks Festival の方は可能かもしれないが期待しないで待っていよう。

私はコンテスト界隈では後期高齢者なので、瞬発力はない。じっくり問題に当たれるコンテストでないと低い点数になりがちである。

私より若くて有望な人にコンテスト参加権利がいくのはとてもいいことである。と同時に、今後はどんなコンテストに参加すればいいのかなとも思う。
