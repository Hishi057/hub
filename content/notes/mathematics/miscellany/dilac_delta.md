---
title: ディラックのデルタ関数
---

スパイクのある関数を滑らかにする役割の持ち、工学などの分野でよく使われる関数である。
[収束定理](/notes/mathematics/lebesgueintegral/convergencetheorem.md)

## ディラックのデルタ関数

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