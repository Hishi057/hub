---
title: フーリエ級数
---

## 概要

フーリエ級数とは、三角関数(あるいは周期関数)の無限和によって、ある関数を表したものである。

例えば、以下は$f(x)=x \quad(x \in (-\pi, \pi))$をフーリエ級数で表すと以下のようになる。

$$
x = 2 \left( \sin x - \frac{\sin 2x}{2} + \frac{\sin 3x}{3} - \frac{\sin 4x}{4} + \cdots \right) = 2 \sum_{n=1}^\infty \frac{(-1)^{n-1}}{n} \sin(nx)
$$

フーリエ級数は元々、[熱方程式](/notes/mathematics/heat_equation.md)の一般的な解を求めるために当初研究されたという背景があるらしいが、今では特に工学を始めとして様々な分野で利用されている。フーリエ級数を知らずんば理系にあらず

## [-1,1]におけるフーリエ級数

以下、$L^2([-1,1])$空間を考える。つまり、$[-1,1]$で関数の絶対値の二乗を積分した時、値が有限になるような関数を考える。

まず、この範囲における関数について考えることで、任意の範囲について考えることが出来る。

> [!definition] $L^2([-1,1])$ 上の三角関数系
> $$
> \begin{cases}
> \varphi_{0}(x) := \frac{1}{\sqrt{2}} \\
> \varphi_{2n-1}(x) := \sin(n\pi x) \\
> \varphi_{2n}(x) := \cos(n\pi x)
> \end{cases}
> $$
> は、$[-1,1]$ 上の $L^2$ 空間における完全正規直交系である。

関数空間において、内積は一般に次のように定義される。

$$
\langle f, g \rangle := \int_{-1}^{1} f(x) g(x) dx
$$

これを踏まえて、完全正規直交系とは、つまり以下の内容を指す。

1. (正規性) $\langle \varphi_{n}, \varphi_{n} \rangle = \int_{-1}^1 |\varphi_{n}(x)|^2 dx = 1$
2. (直交性) $n \not = m$ ならば $\langle \varphi_{n}, \varphi_{m} \rangle = 0$
3. (完全性)$L^2([-1,1])$上の任意の関数は、$\varphi_{n}$の定数倍の無限和で表現することが出来る。

これより、上記の3点の内容について確認するが正規性と直交性はほぼ明らかなので、完全性について記述することとなる。

完全性を証明するにあたって、一般に次を示せば良い。

$$
\langle h, \varphi_{n} \rangle = 0 \quad (n = 1, 2, \dots) \implies h \equiv 0
$$

証明の流れとして、まず関数$h$が連続のときを考えた後に、それを拡張して一般の関数$h$について考えることとなる。

### 正規性

これは、実際に計算すれば明らかなので省略する。
強いて言えば、計算したら$1$になるというよりは、後から計算して$1$になるように係数を調整しているのだから当たり前である。

### 直交性

一般に、次の積分が成り立つ。

$$
\int_{-1}^{1}\sin(n\pi x)\sin(m\pi x)\,dx=\delta_{nm}
$$

$$
\int_{-1}^{1}\cos(n\pi x)\cos(m\pi x)\,dx=\delta_{nm}
$$

$$
\int_{-1}^{1}\sin(n\pi x)\cos(m\pi x)\,dx=0
$$

これより確認できる。

### 完全性: 関数$h$が連続関数

$h \equiv 0$でないと仮定する。$h$は連続なので、必要ならば$-h$を考えることで、どこかは$0$より大きくなっている領域があるはずである。つまり
$$
h(x) > \alpha > 0 \quad (x \in [x_0 - \delta, x_0 + \delta])
$$

を満たす$x_0$と$\delta$が存在するはずである。

ここで、唐突かもしれないが次のような新たな関数を定義する。

$$
g(x) := \cos(\pi(x - x_0)) + 1 - \cos(\pi \delta)
$$

この関数は、$h>0$となる点$x_0$の周辺で

$$
g(x) \ge 1 + \frac{\varepsilon}{2} \quad (x \in [x_0 - \delta', x_0 + \delta'])
$$

と$1$より大きくなるように三角関数から構成された関数であることに注意。

そして、内積$\langle h, g^N \rangle$の値について考える。
$g$は三角関数の和なので$g^N$も三角関数の和で表すことが出来る。
$h$は全ての$\varphi_{n}$に直交するので、この内積の値は$0$になるはずである。つまり$\langle h, g^N \rangle = 0 \quad (N = 1, 2 \dots)$

しかしながら、実際には$h > 0$となる領域があることで、$N$を大きくするとこの内積の値は無限に大きくすることが出来てしまう。具体的には、次のように計算を行えば良い。

$$
\begin{aligned}
\langle h, g^N \rangle &= \int_{-1}^{1} h(x) g(x)^N dx \\
&\ge \int_{x_0 - \delta'}^{x_0 + \delta'} h(x) g(x)^N dx - \int_{[-1, 1] \setminus (x_0 - \delta, x_0 + \delta)} |h(x)| |g(x)|^N dx \\
&\ge 2\delta' \alpha \left(1 + \frac{\varepsilon}{2}\right)^N - 2 \max_{[-1, 1]} |h|
\end{aligned}
$$

$N$を大きくすることで、この内積の値は$\infty$に飛ぶことが示された。

これは矛盾である。よって$h$が連続ならば、$h\equiv 0$以外にあり得ない。

### 完全性: hがL^2関数

前節の内容に帰着させることで、一般の関数についてもフーリエ級数で表すことが出来ると示す。

方針を説明する。前節と同様に$\langle h, \varphi_n\rangle = 0$を仮定する。
そして関数$h$を$[-1,x]$で積分して関数$g$を作る。
この関数$g$は必ず連続となるので、$g$は全ての$\varphi_n$と直交すれば前節の内容より$g \equiv 0$であることが分かる。よって、$h(x) = g'(x) = 0$が示される。

改めて、証明を行う。

まず、以下のように定義を行う。

$$
g(x) := \int_{-1}^{x} h(z) dz
$$

ここで、この関数$g$の性質について説明する。

$g(1)$の値については$\langle h, \varphi_0\rangle = \langle h, \frac1{\sqrt{2}}\rangle = 0$より得られる。

$$
\begin{cases}
g(-1) = 0 \\
g(1) = \int_{-1}^{1} h(z) dz = 0
\end{cases}
$$

また、関数$g$と三角関数の内積は$0$となる。これは、$g(-1)=g(1)=0$と、部分積分すると結局$\langle h, \varphi_n\rangle$を計算することになるためである。
$$
\langle g, \sin(n\pi \cdot) \rangle = \langle g, \cos(n\pi \cdot) \rangle = 0
$$

次に、関数$g$と$\varphi_0$の直交性について示せれば良いが、一般には成り立たなそうなので以下の工夫を行う。

$$
\tilde{g}(x) := g(x) - \frac{1}{2} \int_{-1}^{1} g(z) dz
$$

これは実際に計算すると

$$
\left\langle \tilde{g}, \frac{1}{\sqrt{2}} \right\rangle = 0
$$

となると、$\tilde{g}$と三角関数が直交することも$\tilde{g}$の定義に沿って計算するだけで簡単に分かる。

ゆえに$\tilde{g} \equiv 0$であるが、$g(x)=0$より結局$g \equiv 0$でもあるのだ。

したがって、$h(x) = g'(x) = 0$が示された。

## [0,1]におけるフーリエ級数

前節で、$x \in [-1,1]$におけるフーリエ級数の"妥当性"をチェックした。$x' = \frac{x}{a}$といった拡大・縮小操作を行うことで、$x \in [-a, a]$についてフーリエ級数の妥当性を簡単にチェックできることは想像に難くない。

ではしかし、これだと対称性のある値域でしかフーリエ級数の妥当性を確認できないのであろうか。そんなことはない。$[-1,1]$におけるフーリエ級数の特別な場合(具体的に、対象の関数が奇関数)を考えることによって$[0,1]$におけるフーリエ級数を考えることが出来る。

$[0,1]$で定義された関数$a(x)$をフーリエ級数で表すことを考える。

この時、$[-1,1]$におけるフーリエ級数に帰着させるため以下のような奇拡張について考えてみる。

$$
\tilde{a}(x) := \begin{cases}
a(x) & 0 \le x \le 1 \\
-a(-x) & -1 \le x < 0
\end{cases}
$$

この時、$\tilde{a}(x)$は奇関数なので、偶関数と直交する。すなわち

$$
\begin{cases}
\langle \tilde{a}, \cos(n\pi \cdot) \rangle_{L^2([-1, 1])} = 0 \\
\left\langle \tilde{a}, \frac{1}{\sqrt{2}} \right\rangle_{L^2([-1, 1])} = 0
\end{cases}
$$

よって、$\tilde{a}(x)$は$\sin{n \pi x}$の級数のみで表せそうなことが分かった。実際に

$$
\begin{aligned}
\tilde{a}(x) &= \sum_{n=1}^{\infty} \langle \tilde{a}, \sin(n\pi \cdot) \rangle_{L^2([-1, 1])} \sin(n\pi x) \\
&= 2 \sum_{n=1}^{\infty} \left( \int_{0}^{1} a(z) \sin(n\pi z) dz \right) \sin(n\pi x) \\
&= \sum_{n=1}^{\infty} \left( \int_{0}^{1} a(z) \sqrt{2}\sin(n\pi z) dz \right) \sqrt{2}\sin(n\pi x) \\
&= \sum_{n=1}^{\infty} \langle a(x), \sqrt{2}\sin(n\pi \cdot) \rangle_{L^2([0, 1])} \sqrt{2}\sin(n\pi x)
\end{aligned}
$$

である。ここで、扱う値域を$[0,1]$に戻してみる。この時、$\tilde{a}(x) = a$なのだから

$$
a(x) = \sum_{n=1}^{\infty} \langle a, \sqrt{2}\sin(n\pi \cdot) \rangle_{L^2([0, 1])} \sqrt{2}\sin(n\pi x)
$$

が得られる。これはつまり、$L^2([0,1])$上の関数$a(x)$が$\sin(n\pi x)$の級数で表せることが分かった。また、$L^2([-1,1])$における完全正規直交性は既に示したので、それを用いれば$L^2([0,1])$における完全正規直交性も簡単に示せる。