---
title: 実ベクトル空間
---

## 実ベクトル空間、部分空間

> [!definition] 実ベクトル空間
> ある集合に足し算とスカラー倍が定義されていて、その演算の結果も元の集合に属して次の公理を満たす、
> そのような集合を**実ベクトル空間**と呼ぶ。
>
>  $\mathbf{x, y, z , 0}$ が実ベクトル空間 $\mathbf{V}$ に属して、$1,a,b \in \mathbb{R}$のとき、
> $$
> \begin{align*}
> &(V_1) \quad (\mathbf{x + y}) + \mathbf{z} = \mathbf{x} + (\mathbf{y + z})\\
> &(V_2) \quad \mathbf{x + 0} = \mathbf{x}\\
> &(V_3) \quad \mathbf{x + y} = \mathbf{y + x}\\
> &(V_4) \quad \mathbf{x + (-x)} = \mathbf{0}\\
> &(V_5) \quad a(b\mathbf{x}) = (ab)\mathbf{x}\\
> &(V_6) \quad 1\mathbf{x} = \mathbf{x}\\
> &(V_7) \quad a\mathbf{(x + y)} = a\mathbf{x} + a\mathbf{y}\\
> &(V_8) \quad (a+b)\mathbf{x} = a\mathbf{x} + b\mathbf{x}
> \end{align*}
> $$
> これが成り立つ。

要するに、世界には色々な集合があって、その中でも足し算や掛け算が定義されている集合の中で、
加法やスカラー積について良い感じの性質が成り立っている扱いやすい集合だけを考えましょうね。ということである。

> [!definition] 部分空間
> 実ベクトル空間$\mathbf{V}$の**空でない**部分集合も実ベクトル空間である時、その集合を**部分空間**と呼ぶ。
> そのことを示す際に、実ベクトル空間の公理全てを示す必要はなく、具体的に次の条件を調べられたら良い。
> 
> $$
> \begin{align*}
> &(1) \quad \mathbf{0 \in W}\\
> &(2) \quad \mathbf{x, y \in W} \implies \mathbf{x+y \in W} \\
> &(3) \quad \mathbf{x \in W}, c\in \mathbb{R} \implies c\mathbf{x} \in \mathbf{W}
> \end{align*}
> $$

つまり、実ベクトル空間と部分空間は本質的に一緒ではある。

---

## 線形写像の像, 核

> [!definition] 線形写像の像, 核
> $\operatorname{Im} f = f(\mathbf{V}) = \{f(\mathbf{x}) \mid \mathbf{x} \in V \}$  
> $\operatorname{ker} f = \{\mathbf{x} \mid \mathbf{x} \in V, f(\mathbf{x}) = \mathbf{0}\}$

どちらもあるベクトル空間$\mathbf{V}$上において、

$\operatorname{Im} f$ とは**像**のことで、線形写像$f$によって写し出される他のベクトル空間$\mathbf{W}$の部分集合を指す。これは$\mathbf{W}$の部分空間となる。

一方で、$\operatorname{ker} f$とは、線形写像$f$によって写し出されず$ \mathbf{0} $に圧縮されてしまう$\mathbf{V}$上の集合のことを指す。これは\mathbf{V}の部分空間となる。

### 性質

> [!theorem] 次元定理
> $$
> \operatorname{dim} V = \operatorname{dim} (\operatorname{Im} f) + \operatorname{dim} (\operatorname{ker} f)
> $$

$\operatorname{dim} (\operatorname{Im} f)$ は外部($\mathbf{W}$)に伝わる情報量、$\operatorname{dim} (\operatorname{ker} f)$ は内部で消失する情報量を表す。

つまりは、どれだけの情報量が線形写像$f$によって保たれるのか、犠牲になるのか、という関係を表した数式である。
