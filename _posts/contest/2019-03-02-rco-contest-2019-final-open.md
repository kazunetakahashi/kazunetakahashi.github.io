---
layout: single
category: contest
tag: atcoder
title: 第3回 RCO日本橋ハーフマラソン 本戦 (オープン)
---

[第3回 RCO日本橋ハーフマラソン 本戦 (オープン)](https://atcoder.jp/contests/rco-contest-2019-final-open)

# Source codes

- [My submissions (AtCoder)](https://atcoder.jp/contests/rco-contest-2019-final-open/submissions?f.User=kazunetakahashi)
- [My source codes (GitHub)](https://github.com/kazunetakahashi/atcoder/tree/master/2019/0302_rco-contest-2019-final-open)

# Solutions

## [A - めくってそろえる](https://atcoder.jp/contests/rco-contest-2019-final-open/tasks/rco_contest_2019_final_a)

いつものように、最低点である $1$ 点を狙うことにした。

$1$ 点を取るためにはある $1$ ケースで $1$ 点を獲得し、その他のケースでは全て $0$ 点を獲得することが必要である。そのためには、どうしてもテストケースの特定が必要である。

短期間マラソンの場合、採点に実際使われるテストケースが与えられている場合がある。この場合はそのテストケースで $1$ 点をとり、残りは無条件で $0$ 点をとれば十分である。

しかし今回の場合はそうではないので、 $1$ 点を取れるケースと、それ以外のケースを分ける必要がある。特に「それ以外のケース」は $0$ 点でなくてはならない。正の得点を獲得してはいけない。これは今回の場合は結構厳しい。次に表にする札が、さっき表にした札と同じであれば、得点が確定してしまう。

そこで、今回は次の戦略をとり、テストケースを特定することにした。 $n, X \in N$ は $n < X$ を充たすものとする。

- まず $n$ を出力する。そこで $a _ n = 1$ が却ってきたらその場合は続行、それ以外は WA となるコードを書き(今回の場合 `assert(false);` は WA 扱い)、 $0$ 点とする。
- 次に、 $i = n + 1, \dots, X - 1$ に対して、 $i$ を指定する。そして $a _ i = 1$ であるならこの時点で $1$ 点を獲得したことになるので、 TLE となるコードを書きを出力する。無限に $0$ と $49$ を出力しては入力を受け取ることを繰り返せば良い。
- それでも見つからなかった場合は WA となるコードを書く。

そして $n, X$ を調整して、 TLE が $1$ ケース、 WA が $49$ ケースとなる $n, X$ を発見すればよろしい。今回は複数の実行の末、 $n = 0$ では全部 WA になることがわかった。 $X = 5$ だと TLE が $2$ ケースであり、 $X = 4$ なら $1$ ケース、 $X = 3$ なら $0$ ケースであったようだから、結局 $n = 1$, $X = 4$ が答えの例を与える。あとは WA と TLE のところを AC にするように `cout << -1 << endl;` とすれば全体で $1$ 点が獲得できる。

## [B - まわしてそろえる](https://atcoder.jp/contests/rco-contest-2019-final-open/tasks/rco_contest_2019_final_b)

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">Bも最低点取ってください！！</p>&mdash; tomerun@3/2日本橋ハーフマラソン, 3/17板橋cityマラソン (@tomerun) <a href="https://twitter.com/tomerun/status/1101733628755664896?ref_src=twsrc%5Etfw">2019年3月2日</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

これはさすがに無理でしょw 満点取るのとほとんど同じレベルのプログラムが必要でしょう。

# Others

最低点狙いは、私みたいな異常値のような人にとっては楽しい営みだが、完全に個人の自己満足だと思っていた。今回の運営の、競技プログラミングめっちゃ強い tomerun さんから直接リプライいただけたのはとても恐縮で、嬉しかったです。

こういう楽しみ方を咎めず許容してもらえるのは、ありがたいなと思いました。
