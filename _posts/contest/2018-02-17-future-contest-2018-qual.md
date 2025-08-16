---
layout: single
category: contest
tag: atcoder
title: HACK TO THE FUTURE 2018予選
---

[HACK TO THE FUTURE 2018予選](https://atcoder.jp/contests/future-contest-2018-qual)

# Source codes

- [My submissions (AtCoder)](https://atcoder.jp/contests/future-contest-2018-qual/submissions?f.User=kazunetakahashi)
- [My source codes (GitHub)](https://github.com/kazunetakahashi/atcoder/tree/master/2018/0217_hack-to-the-future-2018)

# Solutions

## [A - 山型足し算](https://atcoder.jp/contests/future-contest-2018-qual/tasks/future_contest_2018_qual_a)

97 億点しか取れなくて、そこから先からどうするかやる気なくして FGO やっていた。

chokudai さんの解説放送を聞く。

46 億点は $Q = 0$ を出せば良い。 96 億点はランダムでできる。 97 億点は、貪欲法でできる。 98 億点は、「超えない」ではなく「できるだけ高い点数」の貪欲法でいける。

ランダムと貪欲を組み合わせると多少マシになる。半分ランダムでやって、貪欲をやる。これで 99 億 8000 万点くらいまでいけるという。生成がランダムなので、中央について山形になる。ランダムでやると中央について山形になる。つまり差がべったりになる。ここから貪欲にするとうまくいく。

山をずらす場合、差分計算をすると、 $+1$ の領域と $-1$ の領域にざっと分かれる。区間を小さくするのは全区間に $-1$ をすることに対応する。この改良をする。山登り法をちゃんと実装し高速化もすると 99 億 9700 万点になる。高速化する際には累積和を使う。更新する時だけ累積和を更新する。

焼きなまし法で、だんだん悪い方向への移動確率を下げていく。 99 億 9800 万点までいけるらしい。 99 億 9900 万点までいけるかもしれないとのことだった。

Q: 遷移はどのくらいがいいか？ A:よほどのことがない限り最小単位で動かす。遷移の種類を増やすといい。

これが解説でした。

決勝のオープンコンテストもあるよ！ 終わり。

# Others

うーん、ずらすのは最後にやればよかったのか。
