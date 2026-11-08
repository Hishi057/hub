---
title: 線形写像
---

## 線形写像

> [!definition] 線形写像
> $V,W$が[ベクトル空間](vector_space.md)であるとき、$f : V \rightarrow W$が以下の条件を満たすとき、**線形写像**であると呼ぶ
>
> 1. $~ f(\mathbf{x}+\mathbf{y}) = f(\mathbf{x}) + f(\mathbf{y})$
> 2. $~ f(k\mathbf{x}) = kf(\mathbf{x})$
>

足し算とかけ算が一番シンプルに成り立つ性質、いわゆる(関数の)線形性をキッチリと定義したものである。
高校数学まででも、ベクトル、微分、和のシグマ、積分、期待値など、線形性が成り立つものはたくさん登場している。

試験において、任意の$\mathbf{x,y} \in \mathbb{V}$と$a,b \in \mathbb{K}$において、
$$
f(a\mathbf{x}+ b\mathbf{y}) = af(\mathbf{x})+bf(\mathbf{y})
$$
が成り立つことを示すのが手っ取り早い。

## 像と核

> [!definition] 線形写像の像, 核
> $f$を線形写像とする。
> $$
> \operatorname{Im} f = f(\mathbf{V}) = \{f(\mathbf{x}) \mid \mathbf{x} \in V \} \\
> \operatorname{ker} f = \{\mathbf{x} \mid \mathbf{x} \in V, f(\mathbf{x}) = \mathbf{0}\}
> $$

どちらもあるベクトル空間$\mathbf{V}$上において、

$\operatorname{Im} f$ とは**像**のことで、線形写像$f$によって写し出される他のベクトル空間$\mathbf{W}$の部分集合を指す。これは$\mathbf{W}$の部分空間となる。

一方で、$\operatorname{ker} f$とは、線形写像$f$によって写し出されず$ \mathbf{0} $に圧縮されてしまう$\mathbf{V}$上の集合のことを指す。これは$\mathbf{V}$の部分空間となる。

### 性質

> [!theorem] 次元定理
> $$
> \operatorname{dim} V = \operatorname{dim} (\operatorname{Im} f) + \operatorname{dim} (\operatorname{ker} f)
> $$

$\operatorname{dim} (\operatorname{Im} f)$ は外部($\mathbf{W}$)に伝わる情報量、$\operatorname{dim} (\operatorname{ker} f)$ は内部で消失する情報量を表す。

つまりは、どれだけの情報量が線形写像$f$によって保たれるのか、犠牲になるのか、という関係を表した数式である。
