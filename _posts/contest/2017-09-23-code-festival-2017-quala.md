---
layout: single
category: contest
tag: atcoder
title: CODE FESTIVAL 2017 qual A
---

[CODE FESTIVAL 2017 qual A](https://atcoder.jp/contests/code-festival-2017-quala)

# Source codes

- [My submissions (AtCoder)](https://atcoder.jp/contests/code-festival-2017-quala/submissions?f.User=kazunetakahashi)
- [My source codes (GitHub)](https://github.com/kazunetakahashi/atcoder/tree/master/2017/0923_cf-2017-quala)

# Solutions

## [A - Snuke's favorite YAKINIKU](https://atcoder.jp/contests/code-festival-2017-quala/tasks/code_festival_2017_quala_a)

やるだけ。

## [B - fLIP](https://atcoder.jp/contests/code-festival-2017-quala/tasks/code_festival_2017_quala_b)

何行目をフリップするかは関係ない。何行フリップするか。全探索。

*フリップフラッピング！*

## [C - Palindromic Matrix](https://atcoder.jp/contests/code-festival-2017-quala/tasks/code_festival_2017_quala_c)

回文だから左上 $1/4$ だけ作ればいい。 $H, W$ の偶数奇数で場合分け。

## [D - Four Coloring](https://atcoder.jp/contests/code-festival-2017-quala/tasks/code_festival_2017_quala_d)

距離空間 $X, Y$ を以下の通りに定める。

\\[ X = \mathbb{Z}^2, d_X((x_0, y_0), (x_1, y_1)) = \lvert x_0 - x_1 \rvert + \lvert y_0 - y_1 \rvert. \\]

\\[ Y = \mathbb{Z}^2, d_Y((x_0, y_0), (x_1, y_1)) = \max( \lvert x_0 - x_1 \rvert, \lvert y_0 - y_1 \rvert). \\]

$f \colon X \to Y$ を $(i, j) \mapsto (i+j, i-j)$ とする。すると $f$ は**等長変換**である。ゆえに、 $Y$ で条件を充たせばよろしい。あとは $d \times d$ の正方形の区画に区切ってぬるだけ。

### ポイント

$f$ の変換は念頭にあったが $l^1$ 距離空間から $l^\infty$ 距離空間への等長変換になっていることは知らず。覚えておきたい。

## [E - Modern Painting](https://atcoder.jp/contests/code-festival-2017-quala/tasks/code_festival_2017_quala_e)



### ポイント



## [F - Squeezing Slimes](https://atcoder.jp/contests/code-festival-2017-quala/tasks/code_festival_2017_quala_f)



### ポイント



# Others

今年の Code Festival ボーダー高すぎませんか？ 私が出られたら奇跡だよもう。

昨年までは、私のような弱小プレイヤーでも、努力すれば通過できて、たくさんの人と交流して刺激を受けられる場所だった。本戦進出者が 100 人だと、選ばれしプレイヤーの集いになるだろう。

最近はどんどん平均レベルも上がっているから Code Thanks Festival もいけるかどうか…

予選 B も C も頑張ります。
