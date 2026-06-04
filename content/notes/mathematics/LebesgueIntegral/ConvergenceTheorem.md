---
title: 3. 収束定理
---

## 収束定理：極限と積分の交換

以下の順番で、極限と積分が交換できる範囲を拡張していく。

1. 単関数の単調収束定理： 単関数
2. 単調収束定理: 単調増加する非負可測関数列$f_n$
3. Fatouの補題： 非負可測関数の列
4. ルベーグの優収束定理： 一般の可測関数の列

### 単関数の単調収束定理

### 単調収束定理

> [!theorem] 単調収束定理
> 非負可測関数列$f_n$が次を満たすとする。
> $$
> \forall n ~ f_n \leq f_{n+1} ~ a.e.\\
> f = \lim\limits_{n\rightarrow \infty} f_n,\text{then} \quad
> \lim\limits_{n\rightarrow \infty} \int f_n d\mu = \int f d\mu
> $$

### Fatouの補題

> [!theorem] Fatouの補題
> 非負可測関数列$\{f_n\}$ならば、次が成り立つ
> $$
> \int \liminf\limits_{n \rightarrow \infty} f_n dx = \liminf\limits_{n \rightarrow \infty} \int f_n dx
> $$

後述するルベーグの優収束定理よりも、条件が緩く使いやすい。特に、優関数がなくてもこの補題を適用できる場面があるという強みがある。

補題の主張としては、各点において下限を考えて積分した値は、先に全体を積分した後に下限を考えた時の値を上回ることはないということになる。

### ルベーグの優収束定理

> [!theorem] ルベーグの優収束定理
> 可測関数列$f_n:\mathbb{R}→\bar{\mathbb{R}}$と可測関数$f,~$非負可積分関数$\Phi$は次を満たす。
> $$
> \quad f = \lim\limits_{n→\infty}f_n ~ \text{a.e.} \\
> \forall n \in \textbf{N}, ~ |f_n| \leq \Phi ~ \text{a.e.}
> $$
> このとき、$f_n,~f$は可積分であり、次が成り立つ。
> $$
> \lim\limits_{n→\infty}\int f_nd\mu = \int fd\mu
> $$

いわゆるこれが、"極限と積分が交換できる"というもので、適用条件はかなり緩い。普通に出会う関数はほとんどこれを満たすので、物理学科の人が何も条件を確認せず極限と積分を交換する様子を見て数学科の人がよく怒ったりしている。

## 優束定理の応用

### 連続パラメータ版ルベーグの優収束定理

> [!theorem] 連続パラメータ版ルベーグの優収束定理
> $a,b\in\mathbb{R}$,$~A \in \mathbb{R}^n$を可測集合として、$A \times (a,b)$上の可測関数$f$が次を満たす。
> $$
> \begin{align*}
> &(1) \qquad \forall t \in (a,b) ~\text{について、}f(x,t) \text{は}x \text{の関数として} A \text{上可積分}\\
> &(2) \qquad \text{a.e.}~ \forall x \in A \quad \lim\limits_{t→t_0} f(x,t) = f(x,t_0) \quad \\
> &(3) \qquad \exist g(x) \in L^1(A),~ \text{a.e.}~ \forall (x,t)\in A \times (a,b) \quad |f(x,t)| \leq g(x)
> \end{align*}
> $$
> このとき、以下が成り立つ。
> $$
> \lim\limits_{t→t_0} 
> \int_A f(x,t) dx 
> = \int_A \lim\limits_{t→t_0} f(x,t) dx
> $$

つまり、**多変数関数でも上から抑える優関数が存在すれば、一変数関数と同様に極限と積分を交換してok**と言える定理である。

### 微分と極限の交換

> [!theorem] 微分と極限の交換
> $a,b\in\mathbb{R}$,$~A \in \mathbb{R}^n$を可測集合として、$A \times (a,b)$上の可測関数$f$が次を満たす。
> $$
> \begin{align*}
> &(1) \qquad 任意に t \in (a,b) を固定したとき、f(x,t) は x の関数として A 上可積分\\
> &(2) \qquad 任意に~x\in A~を固定したとき、f(x,t)はtの関数として微分可能 \\
> &(3) \qquad \exist g(x) \in L^1(A),~ \text{a.e.}~ \forall (x,t)\in A \times (a,b) \quad |\frac{\partial f}{\partial t}(x,t)| \leq g(x)
> \end{align*}
> $$
> $$
> \dfrac{d}{dt} \int_{A} f(x,t) dx = \int_{A} \dfrac{\partial}{\partial t} f(x,t) dx \quad \text{for any } t \in (a,b).
> $$

**証明**

条件が成り立っていて、連続パラメータ版ルベーグの優収束定理を用いることが出来るとすれば(これが成り立つことは簡単に確認できる)
$$
F(t)= \int_{A} f(x,t) dx
$$
として
$$
\begin{align*}
F'(t_0) &= \lim\limits_{t→t_0}\frac{F(t)-F(t_0)}{t-t_0}\\
&= \lim\limits_{t→t_0} \int_A \frac{f(x,t)-f(x,t_0)}{t-t_0}dx \\
&= \int_A \lim\limits_{t→t_0} \frac{f(x,t)-f(x,t_0)}{t-t_0}dx \\
&= \int_A \frac{\partial}{\partial t}f(x,t_0)dx

\end{align*}
$$

### 応用例：ディラックのデルタ関数

> [!theorem] ディラックのデルタ関数
> $f \in L^1(\mathbb{R})~$, $~\int_{-\infty}^{\infty} f(x)dx=1~$, $f_n(x) = nf(nx)$ とする。
> $\mathbb{R}$上の有界な連続関数$g(x)$に対して次が成り立つ。
> $$
> \lim\limits_{n\rightarrow\infty} \int_{-\infty}^{\infty} g(x-y) f_n(y) \, dy = g(x)
> $$

**証明**

$f_n(x)$とは$f(x)$を$x=0$にギュッと縮めた関数である。この関数の性質をまず調べる。\
これの積分が$1$であることを示す。

$$
\begin{align*}
\int_{-\infty}^{\infty} f_n(x) \, dx &= \int_{-\infty}^{\infty} n f(nx) \, dx \\
&= \int_{-\infty}^{\infty} f(z) \, dz \\
&= 1
\end{align*}
$$

$x=0$にギュッと縮めているので、逆にそこを除いた積分をすると$0$となる。このことは、以下のようにルベーグの優収束定理から導ける。

$$
\begin{align*}
\lim\limits_{n\rightarrow\infty} \int_{|z| \ge \delta} n f(nx) \, dx &= \lim\limits_{n\rightarrow\infty} \int_{|y| \ge n\delta} f(y) \, dy \\
&= \lim\limits_{n\rightarrow\infty} \int_{-\infty}^{\infty} f(y) \chi_{\{|y| \ge n\delta\}} \, dy \\
&=  \int_{-\infty}^{\infty} \lim\limits_{n\rightarrow\infty} f(y) \chi_{\{|y| \ge n\delta\}} \, dy \\
&= 0
\end{align*}
$$

本筋の証明に入っていく。

$$
\left| \int_{-\infty}^{\infty} g(x-z) f_n(z) \, dz - g(x) \right|
\\
= \left| \int_{-\infty}^{\infty} g(x-z) f_n(z) \, dz - g(x) \int_{-\infty}^{\infty} f_n(z) \, dz \right|
\\
\le \int_{-\infty}^{\infty} |g(x-z) - g(x)| f_n(z) \, dz
\\
= \int_{|z| < \delta} |g(x-z) - g(x)| f_n(z) \, dz + \int_{|z| \ge \delta} |g(x-z) - g(x)| f_n(z) \, dz
$$

$\delta$は0以上の任意の定数とする。最後、積分範囲を原点近傍と遠点に分割した。それぞれ0に収束することを示す。

まず、原点近傍について関数$g$は連続なので、その定義を思い出す。

$$
\int_{|z| < \delta} |g(x-z) - g(x)| f_n(z) \, dz < \varepsilon \int_{|z| < \delta} f_n(z) \, dz \to 0
$$

$\delta$に応じて$\epsilon$はいくらでも小さくできることに注意。

次に、遠点について関数$g$は有界なので定数で抑えられる。

$$
\begin{align*}
&\lim_{n \to \infty} \int_{|y| \ge \delta} |g(x-y) - g(x)| f_n(y) \, dy 
\\
&\le \lim_{n \to \infty} C \int_{|y| \ge \delta} f_n(y) \, dy 
\\
&= 0
\end{align*}
$$

よって、題意が示された。

$$
\lim\limits_{n\rightarrow\infty} \left| \int_{-\infty}^{\infty} g(x-y) f_n(y) \, dy - g(x) \right| \rightarrow 0
$$
より
$$
\lim\limits_{n\rightarrow\infty} \int_{-\infty}^{\infty} g(x-y) f_n(y) \, dy = g(x)
$$