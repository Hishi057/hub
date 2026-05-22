---
title: 二次形式
---

## 前提知識

[[notes/LinearAlgebra/Basics#固有値|固有値]] 固有値が重要となる。

## 概要

二次形式とは、二次の複数変数を行列で、特に次の形で表したものである。

> [!definition] 二次形式
> 
> $ x \in \mathbb{R}^n$,$Q$を定数行列として
> $$
> g(x) = x^TQx = \sum{\sum{q_{i,j}x_ix_j}}
> $$
> の形で表される多項式のことを二次形式と呼ぶ。

「最小値があるか」「安定か」「楕円の形はどうか」「どの方向に大きいか」などが、二次形式で表した行列の固有値を通すことで簡単に分かるようになる。

> [!definition] 半正定値
> $$
> \begin{align*}
> 
> \text{Q は半正定値} &\overset{\text{def}}{\iff} u^\top Qu \ge 0, \quad \forall u \in \mathbb{R}^n \\
> \text{Q は正定値} &\overset{\text{def}}{\iff} u^\top Qu > 0, \quad \forall u \neq 0 \\
> \text{Q は半負定値} &\overset{\text{def}}{\iff} u^\top Qu > \le 0, \quad \forall u \in \mathbb{R}^n \\
> \text{Q は負定値} &\overset{\text{def}}{\iff} u^\top Qu < 0, \quad \forall u \neq 0
> \end{align*}
> 
> $$
> いずれにも当てはまらない場合、不定値と呼ぶ。
> 特に、 以下の表記に注意。
> 
> 半正定値: $Q \succeq O$, $\quad$ 正定値: $Q \succ O$

正定値であるとはつまり、どのように$u$を動かしても二次式の値が大きくなるという意味である。

## 関数の極値

一変数関数における極値の概念が、他変数関数においても半正定値の概念を用いることで容易に記述出来るになる。

ある多変数関数$f$の$x=x^*$におけるテイラー展開は以下のようになる。

$$
f(x) \approx f(x^*) + \nabla f(x^*)^\top (x - x^*) + \frac{1}{2} (x - x^*)^\top \nabla^2 f(x^*) (x - x^*)
$$

この時、以下の性質が成り立つ。

$$
\begin{align*}
x^*がfの極小点 &\implies \nabla f(x^*)=0, \nabla^2 f(x^*)が半正定値 \\
x^*がfの極小点 &\impliedby \nabla f(x^*)=0, \nabla^2 f(x^*)が正定値
\end{align*}
$$

極大値と半負定値についても同様の性質が成り立つ。

## Qが対角行列

$$
Q = \begin{bmatrix}
\lambda_1 & 0 & \cdots & 0 \\
0 & \lambda_2 & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & \lambda_n
\end{bmatrix}
$$

Qが対角行列のとき

$$
x^TQx = \lambda_1x_1^2 + \lambda_2x_2^2 + \cdots \lambda_nx_n^2
$$

であるため、前節よりすべての固有値が非負の時$Q$は半正定値、すべての固有値が正の時$Q$は正定値、半負定値と負定値でも同様のことが成り立つ。