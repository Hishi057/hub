---
title: ベクトル空間
---

## ベクトル空間、部分空間

> [!definition] ($\mathbb{R}$上の)ベクトル空間
> ある集合に足し算とスカラー倍が定義されていて、その演算の結果も元の集合に属して次の公理を満たす、
> そのような集合を**ベクトル空間**と呼ぶ。
>
>  $\mathbf{x, y, z , 0}$ がベクトル空間 $\mathbf{V}$ に属して、$1,a,b \in \mathbb{R}$のとき、
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

要するに、あるベクトル空間内で"閉じている空間"のことを指す。
例えば変換によって集合からはみ出ないことが保証されることで、
変換後の値が元の集合に属していることを示さずに、
(元の集合が持つ)性質$A$を満たすことがわかる。
というようなシチュエーションが多い。

### 問題

> [!problem] x+y+z=0 は部分空間か？
> 次の集合が $\mathbb{R^3}$ の部分空間であることを示せ。
> $$
> W=\{(x,y,z)\in\mathbb R^3\mid x+y+z=0\}
> $$

この空間$W$が3つの性質を満たすことを示せば良いが、実践的には次のように2つの事柄を示せば良い

① $0 \in W$

$(x,y,z)=(0,0,0)$は明らかに$x+y+z=0$を満たすため、$W$に属する。

② $\alpha u + \beta v \in W$

また、$\mathbf{u},\mathbf{v} \in W$ として $u = (x,y,z)$, $v = (a,b,c)$ とすると$x+y+z = a+b+c = 0$ を満たす。
加えて、$\alpha,\beta \in \mathbb{K}$ とする。

$$
\alpha \mathbf{u}+\beta \mathbf{v} 
= (\alpha x + \beta a, \alpha y + \beta b, \alpha z + \beta c)
$$

であり、このベクトルは$\alpha (x+y+z) + \beta (a+b+c) = 0$ である。  
よって$\alpha \mathbf{u}+\beta \mathbf{v} \in W$に属する。