---
title: 固有値
---

## 固有値

> [!definition] 固有値
> 
> $n$次正方行列$A$に対して、以下を満たす$\lambda \in \mathbf{C} $ 列ベクトル $x \in \mathbf{C}^n$ が存在するとする。
> $$
> Ax = \lambda x
> $$
> このとき$\lambda$を**固有値**と呼ぶ。それに対応する$x$を**固有ベクトル**と呼ぶ。
> 固有値とそれに対応する固有ベクトルは重複ありで$n$個存在する。
> ただし、$\lambda = 0$かつ$x \not = 0$

ベクトルと行列の積を、ベクトルとスカラーの積という単純な形に変形出来ると考えると、中々すごい。

一般に、以下の手順で固有値を求めることが出来る。

$$
Ax = \lambda x 
\\
\iff Ax - \lambda x = 0
\\
\therefore \det{(Ax - \lambda x)} = 0 
\\
\iff \det{(A-\lambda I_n)}\det{(x)} = 0
\\
\iff \det{(A-\lambda I_n)} = 0
$$

よって$\det{(A-\lambda I_n)} = 0$これを解くことで、固有値$\lambda$が求められる。

## 対角化

正方行列 $A$ が**対角化可能**とは、ある正則行列 $P$ と対角行列 $D$ が存在して
$$
P^{-1}AP = D
$$
と書けること。

固有値 $\lambda_1,\dots,\lambda_n$ に対応する一次独立な固有ベクトル $v_1,\dots,v_n$ が取れるとき（固有ベクトルが $n$ 本そろうとき）、
$$
P = [v_1\ v_2\ \cdots\ v_n],\quad D = \mathrm{diag}(\lambda_1,\dots,\lambda_n)
$$
と置けば $AP=PD$ となり、結果として $P^{-1}AP=D$ が成り立つ。

## 固有値の積

> [!theorem] 固有値の積
> $n$ 次正方行列 $A$について、その固有値を$\lambda_1, \lambda_2, \cdots, \lambda_n$とすると
> $$
> \det{(A)} = \lambda_1 \times \lambda_2 \cdots \times \lambda_n
> $$

## Gershgorinの定理

> [!theorem] Gershgorinの定理
> $n$ 次複素正方行列 $H = (h_{ij})$ の任意の固有値 $\lambda$ は
> $$
> G_k := \{z \in \mathbb{C} \mid |z - h_{kk}| \le r_k\}, 
> \quad r_k = \sum_{j=1, j \ne k}^{n} |h_{kj}|
> $$
> で定義される，複素平面上の $n$ 個の円 $G_k \ (k = 1, 2, \dots, n)$ の和集合 $\bigcup_{k=1}^{n} G_k$ の中にある

以上の定理は、つまり固有値の位置を大雑把に推定出来て、かつ固有値というのは対角成分の近くに位置しているということを示している。
この定理によって、例えば全ての固有値が$0$でないことと示せれば、その正方行列は正則であることになる。

**証明**

$$
Hx = \lambda x
\\
\Leftrightarrow

\begin{bmatrix} 
h_{11} & h_{12} & \\ h_{21} & h_{22} & \\ & & \ddots 
\end{bmatrix}
\begin{bmatrix} 
x_1 \\ x_2 \\ \vdots 
\end{bmatrix}

=

\lambda

\begin{bmatrix} 
x_1 \\ x_2 \\ \vdots 
\end{bmatrix}
$$

$k = \underset{1 \le i \le n}{\operatorname{arg\,max}} |x_i| \quad (\ne 0)$ として、$|x_i| \leq |x_k|$となるような$k$を選ぶことで

$$
\sum_{i=1}^n h_{ki} x_i = \lambda x_k
\\
\Leftrightarrow \sum_{\substack{i=1 \\ i \ne k}}^n h_{ki} x_i 
= \lambda x_k - h_{kk} x_k 
= (\lambda - h_{kk}) x_k
\\
\therefore |\lambda - h_{kk}| 
\le \sum_{\substack{i=1 \\ i \ne k}}^n |h_{ki}| \left| \frac{x_i}{x_k} \right| 
\le \sum_{\substack{i=1 \\ i \ne k}}^n |h_{ki}| 
= r_k
$$