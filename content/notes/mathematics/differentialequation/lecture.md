---
title: 講義ノート
---

## 第6回

ヒルベルト空間

$\{\varphi_n\} \in H: ONS$ とする

全ての $\varphi_n$ と直行する $h \in H$ が $h=0$ の時

$\{\varphi_n\}$ を完全正規直交系 という

**命題**

$\{\varphi_n\} \in H: ONS$ とする

この時

$\{\varphi_n\} \in H$ が完全
$\iff \forall f \in H, f = \sum{(f, \varphi_n)_H\varphi_n} \quad \text{in}. H$ 

**証明**

- $\leftarrow$ の証明

$h \in H \text{s.t.} (h, \varphi_n)_H = 0 \text{for all n}$とする。

このとき、$h=\sum{(h,\varphi_n)\varphi_n} = 0$

- $\rightarrow$ の証明

$f_N \coloneqq \sum\limits_{n=1}^{N}{(h,\varphi_n)_H \varphi_n}$

$f = f_\infty$ をいう。

$m=1,2,..., N>m$に対して

$$
(f_N,\varphi_m)_H 
= \sum\limits_{n=1}^N (f,\varphi_n)_H (\varphi_n, \varphi_m)_H
= (f,\varphi_m)_H
$$

$$
|(f_\infty - f \cdot \varphi_m)_H|
= |(f_\infty - f_N \cdot \varphi_m)_H| \\
\leq ||f_\infty - f_N||_H \cdot ||\varphi_m||_H \\
= 0 \cdot 1
$$

左辺はNに依らないので

$$
(f_\infty - f_N \cdot \varphi_m)_H = 0 \quad \text{for all} ~ n
$$
完全性 $f_\infty - f = 0$


-> $L^2$上のCONSをやる
まず一周期をベースにしたもの

**定理**

- $\varphi_0(x) \coloneqq \frac{1}{\sqrt{2}}$
- $\varphi_{2n-1}(x) \coloneqq \sin{n \pi x}$
- $\varphi_{2n}(x) \coloneqq \cos{n \pi x}$

として

$\{\varphi_n\}_{n=0}^\infty$は$L^2([-1, 1])$上のCONS

**証明**

ONSはやればOK

hと$\{\varphi_n\}_{n=0}^\infty$が直交ならば $h=0$を言えばOK

[1] $h \in C([-1,1])$ かつ $h \perp \{\varphi_n \}_{n=0}^\infty$ の時

背理法を用いる

$h \equiv 0$ (ある$x$で $h(x) \ne 0 $)と仮定して矛盾を導く

必要ならば$-h$を考えて

$\exist x_0 \in (-1,1)$

$\exist \alpha > 0, \exist \delta >0 ~ $ s.t.

- $[x_0 - \delta, x_0 + \delta] \subset (-1,1)$
- $h(x) > \alpha ~\text{for}~ \forall x \in [x_0 - \delta, x_0 + \delta]$

(方針) うまい関数を作って$h$のやばそうなところを作って矛盾を導く

ルベーグによる証明(?) らしい

ここで

$$
g(x) \coloneqq \cos{(\pi(x-x_0))} + 1 - cos(\pi \delta) \\
= \cos{(\pi(x-x_0))} + \epsilon
$$

(なんか先生色々言ってた)
$\delta$は必要なら小さく取り直す。初めから例えば、デルタを1/2未満にしておいても別に安全に過ごせる　と思いますが
まあその辺りは誰でも簡単にセッティングできると思うのであんまこだわんないことにして

ちょっとこの$g(x)$の図を細かくというかよくよく考えて書いておこうと思います

$x_0$は今プラスで書くことにします ふ〜

(パソコンじゃ図描けん)

よって

$\forall x \in [x_0 - \delta, x_0 + \delta] \quad g(x) \geq 1$

$\forall x \in [-1,1] \setminus [x_0 - \delta, x_0 + \delta] \quad |g(x)| \leq 1$

$0 < \exist \delta ' < \delta ~ \text{s.t.} ~ g(x) \geq 1 + \frac{\epsilon}{2} ~ for \forall x \in [x_0 - \delta', x_0 + \delta'] $

が成立。

今、$g^N (N=1,2,\cdots)$は加法定理、積和の公式から 
$\{\varphi_n\}_{n=0}^\infty$内の関数の有限個の線型結合で書ける.

$h \perp \{\varphi_n\}_{n=0}^\infty $ より $h \perp g^N$

つまり$(h,g^N)_{L^2} = 0 ~\text{for}~ \forall N = 1,2,\cdots$

一方、$(h,g^N)_{L^2} \rightarrow 0 ~(N\rightarrow 0)$もいえる

実際

$$
(h,g^N)_{L^2}

=

\int_{[x_0-\delta, x_0+\delta]} hg^N
+
\int_{ [-1,1] \setminus [x_0 - \delta, x_0 + \delta]} hg^N

\\
\geq

\int_{[x_0-\delta', x_0+\delta']} hg^N
-
\int_{ [-1,1] \setminus [x_0 - \delta, x_0 + \delta]} |h||g|^N

\\
\geq

\alpha (a+\frac{\epsilon}{2})^N 2\delta' 

- (\text{max}_{[-1,1]} |h|)\cdot 1 \cdot 2

\\

\rightarrow \infty ~ (N \rightarrow \infty)

$$

よって矛盾

ステップ1 連続関数の時の証明は終わり

[2] $h \in L^2([-1,1])$ かつ $h \perp \{\varphi_n \}_{n=0}^\infty$ の時

何らかの方法で連続関数verに辿り着ければOK

なんかもっと直接的な方法がルベーグによって知られているのでそれをやる。
さっきまでの$g$は忘れて、改めて$g$を定義する

$$
g(x) \coloneqq \int_{[-1,x]} h(y)dy
$$
と置く。目標は$h=0$ つまり$h(x) = 0 \text{~for a.e. in [-1,1]}$

$$
\int_{[-1,x]} |h|

\leq

\int_{[-1,1]} |h|

\leq

\left(\int_{[-1,1]} |h|^2 \right)^{\frac{1}{2}}

\left(\int_{[-1,1]} 1^2 \right)^{\frac{1}{2}}

< \infty
$$

最後はヘルダーの不等式のよくある使い方らしい

最後の1個めの因数は$L^2$に属してるので有限
2個目の因数も有限

より、各$x \in [-1,1]$に対して$g(x)$が定まる

つまり、$g$はwell-defined

(ここはルベーグ積分の深いところまでやらないといけないし、ルベーグ積分の講義でも扱わなかったので詳しくは省く)

更に、実は$g \in C([-1,1])$も言えて、部分積分もできる

気になる人は、微分積分学の基本定理、原始関数、不定積分、あたりをルベーグ本で探す

$$
(g,sin(n \pi))_{L^2}
= \int_{[-1,1]} g(x)\sin{(n\pi x)}dx
\\
= 
[g(x)(-\frac{cos(n \pi x)}{n\pi})]_{-1}^{1}

- \int_{-1}^{1} h(x)(-\frac{cos(n \pi x)}{n\pi}) dx
$$

$g$に具体的に代入してみる
$g(-1) = 0$, $g(1) = \int_{-1}^1 h(y)dy = (h, \frac{1}{\sqrt{2}})_{L^2}\sqrt{2} = 0$ (最後は直交するので)

$$
= \frac{1}{n \pi} (h, \cos{(n \pi \cdot)})_{L^2}
= 0
$$

同様に $(h, \cos{(n \pi \cdot)})_{L^2}$

ここで

$$
\tilde{g(x)} \coloneqq g(x) - \frac{1}{2}\int_{-1}^1g(y)dy
$$

とすれば

$$
(\tilde{g(x)}, \frac{1}{\sqrt{2}})_L^2
= \int_{-1}^1 \tilde{g(y)} \frac{1}{\sqrt{2}} dy \\
= \int_{-1}^1 (g(x) - \frac{1}{2}\int_{-1}^1g(y)) \frac{1}{\sqrt{2}} dy \\
= \frac{1}{\sqrt{2}} \int_{-1}^1g(x)dx
- \frac{2}{2\sqrt{2}} aaa
$$

(微妙に最後書けなかった)

更に
$(\tilde{g},cos(n\pi \cdot))_{L^2} = (\tilde{g},sin(n\pi \cdot))_{L^2} = 0$

以上より

$\tilde{g} \perp \{\varphi_n \}_{n=0}^\infty$

$\tilde{g} \in C([-1,1])$

であり、[1]から $\tilde{g} ≡ 0$
つまり全ての$x$について$g(x)$は定数となる。

微分して
$h(x) = 0 \text{for (a.e.)} x \in [-1,1]$

以上より$L^2([-1.1])$のCONSを得た

$\alpha \in L^2([0,1])$ の時、$\alpha \in L^2([0,1])$を奇拡張した

$$
\tilde{a} \\
\quad \coloneqq a(x) ~ (0\leq x \leq 1) \\
\quad \coloneqq -a(-x) ~ (-1 \leq x \leq 0)
$$
は$L^2([-1,1])$に入る

故に$\int_{-1}^1 |\tilde{a}|^2 < \infty$

よって定理と命題から

$\tilde{a}(x) = \sum{(\tilde{a}, \varphi_n)}_{L^2([-1,1])} \varphi_n(x)$
と、$L^2([-1,1])$上で展開できる

次回、偶奇に着目して$(\tilde{a}, \varphi_n)_{L^2([-1,1])}$を計算