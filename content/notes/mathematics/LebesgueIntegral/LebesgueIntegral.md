---
title: 2. ルベーグ積分
---

## ほとんど至るところで

> [!definition] ほとんど至るところで
> ある集合$X$上で命題$P$について考える。その命題$P$が、$X \setminus Y$を除いて成り立ち、かつ $\mu(Y)=0$のとき、
> 例えば
> $P$ a.e. $x \in X$
> と表現する。

a.e. (=almost everywhere) ということであり、立派な数学用語である。

多少の例外は見逃すというものを数学的に厳密に表現したのが、この定義なのである。

## 可測関数

> [!definition] 定義：可測関数
> 関数 $f:X → \bar{\mathbb{R}}$ が可測であるとは
> 次の性質を満たすものである。
> $$
> X \in \mathcal{M} \\
> \forall a\in \mathbb{R} \quad \{f(x)>a\} \in \mathcal{M}
> $$
> 特にこれを満たす関数$f$を**可測関数**と呼ぶ。

要するに、リーマン積分は縦状の短冊で区切って積み上げていたが、ルベーグ積分は横状の短冊で区切って積み上げたい。横状の短冊で区切るためには、"横の長さ"を"納得がいくような定義"をして測れるようにする必要がある。この"納得がいくような定義"こそが、ルベーグ測度である。

つまりこの定義は、**横の長さが人間の納得いくように測れる関数だけをこれから扱いますよという宣言**と思えば良い。

### 重要な性質

> [!theorem] 可測関数の四則演算
> 可測関数同士の四則演算の結果も可測関数
> $$
> (f+g)(x) \in \mathcal{M} \\
> (f-g)(x) \in \mathcal{M} \\
> (f \cdot g)(x) \in \mathcal{M} \\
> \frac{f}{g}(x) \in \mathcal{M}
> $$

## ルベーグ積分

次の手順で、ルベーグ積分を定義する。

1. 有限個の値を取りうる関数、単関数の面積を定義する。
2. 非負関数の積分を、そのような単関数の面積(の上限)として定義する。
3. 上の定義を、負の値を取りうる関数にも拡張する。

### 特性関数, 単関数

> [!definition] 定義：特性関数, 単関数
> 次のような関数を、**特性関数**と呼ぶ。
> $$
> \chi_A(x) :=
> \begin{cases}
> 1 & (x \in A) \\
> 0 & (x \in A^c)
> \end{cases}
> $$
>
> そして、関数$s:\mathbb{R} → \mathbb{R}$が有限の値を取りうるとき、**単関数**と呼ぶ。具体的には、次を満たすことをいう。
> $$
> A_1, A_2 \cdots A_n \in \mathcal{M} \\
> \mathbb{R} = A_1 \sqcup \cdots \sqcup A_n \\
> s = \sum\limits_{i=1}^{n}a_i \chi_{A_i}
> $$
> ただし数列$\{a_i\}$は重複を許す。

また、この単関数の積分を次のように定義する。

> [!definition] 定義：単関数の積分
> $$
> \int s d\mu \coloneqq \sum\limits_{i=1}^{n}a_i \mu{(A_i)}
> $$

この積分は、単純な長方形の和であるから、リーマン積分かルベーグ積分かそうでない積分なのか、問題にならない。

### 可測関数の積分の定義

> [!definition] 定義：非負可測関数の積分
> $f$を非負可測関数とする。
> $$
> \int f d\mu \coloneqq 
> \sup\limits_{0\leq s \leq f}
> \int s d\mu
> $$

この定義を、一般の可測関数にも拡張する。

> [!definition] 定義：可測関数の積分(ルベーグ積分)
> $f$を可測関数とする。
>
> $f^+ \coloneqq \max{ \{f, 0\} }, \quad f^- \coloneqq \max{ \{-f, 0\} }$
>
> とすると
> $$
> \int f d\mu \coloneqq 
> \int f^+ d\mu
> - \int f^- d\mu
> $$

これを、**ルベーグ積分**と呼ぶ。

> [!definition] 積分確定、可積分
> $f$を可測関数とする。
>
> $\int f^+ d\mu < \infty$ または $\int f^- d\mu < \infty$ ならば、$f$の積分結果は不定形とならないので**積分確定**と呼ぶ。
>
> $\int f^+ d\mu < \infty$ かつ $\int f^- d\mu < \infty$ $\iff \int |f|d\mu < \infty $ ならば、$f$の積分結果は必ず有限となるので、**(ルベーグ)可積分**と呼ぶ。

## 関数空間$L^1(A)$

> [!definition] 関数空間$L^1(A)$
> ある関数$f:A\rightarrow [-\infty , \infty]$が関数空間$L^1(A)$に属するとは、
> $f$がルベーグ可積分であることである。

この関数空間に属する関数は、この後に見ていく積分と極限の交換といった操作が安全に行える。

以下、ある関数$f$が可積分である、つまり$L^1(A)$に属する際の典型手法についてまとめる

### 可積分であることの証明の常套手段

**典型的な流れ**

1. $A \subset \mathbb{R}^n$が可測であることを示す
2. $f$が$A$上で可測であることを示す
3. $\int_A |f(x)|dx \leq \int_B g(x)dx~$である $~A \subset B~$と$~ g(x) \in L^1(B) ~$ を見つける

ここで、通常3番の手順が一番大変なのだが、初等的な関数であれば積分領域を分割して$|x|^\alpha$で抑えることで楽に見つけることが出来ることが多い。

> [!theorem] |x|^αの積分の収束性
> $~B_r \in \{x \in \mathbb{R}^n ; |x| < r\}~,f(x) \coloneqq |x|^\alpha$ (ただし$x=0$における値は問わない)ならば
> - 原点の周辺 $~\int_{B_r} f(x)dx ~$が可積分 $\quad \iff ~\alpha + N > 0~$
> - 空間遠方 $~\int_{\mathbb{R}^n \setminus B_r} f(x)dx ~$が可積分 $\quad \iff ~\alpha + N < 0$
> 
> が成り立つ。

#### 具体例

$$
f(x) \coloneqq |x|^Ne^{-|x|^2}, A=\mathbb{R}^N
$$
これがルベーグ可積分であることを示す。\
まず、第一に$A=\mathbb{R}^n$は可測である。\
第二に、$x=0$を除いて$|x|$は可測関数で、$e^{-|x|^2}$も可測関数なので、その積である$f(x)$も可測関数。\
第三に、$f(x)$を抑える関数$g(x)$を見つける。

$$
\begin{aligned}
\int_{A} f(x)dx &= \int_{B_r} f(x)dx + \int_{\mathbb{R}^N \setminus B_r} f(x)dx
\\
&\leq \int_{B_r} dx + \int_{\mathbb{R}^N \setminus B_r} |x|^N\frac{1}{1+|x|^2+ \cdots +\frac{1}{M!}|x|^{2M}}
\\
&\leq \mu(B_r) + \int_{\mathbb{R}^N \setminus B_r} |x|^N\frac{1}{\frac{1}{M!}|x|^{2M}}
\\
&= \mu(B_r) + \int_{\mathbb{R}^N \setminus B_r} M!|x|^{N-2M}
\end{aligned}
$$

途中で、$e^{|x|^2}$のマクローリン展開を用いた。整数$M$はいくらでも大きく出来るので、
$(N - 2M) + N < 0$となるように$M$をとれば、上から抑える優関数$g(x)$が構成できる。
