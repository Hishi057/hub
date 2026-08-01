---
title: ラプラス方程式
---

## 概要と方針

ラプラス方程式とは、次のような微分方程式を指す

> [!definition] (二次元)ラプラス方程式
> $\Omega\subset\mathbb R^2$ を領域（連結開集合）とする。
> $$
> \nabla^2u = \Delta u=0\qquad\text{in }\Omega
> $$
> 
> すなわち
> 
> $$
> \frac{\partial^2u}{\partial x^2}
> +\frac{\partial^2u}{\partial y^2}=0
> \qquad ((x,y)\in\Omega)
> $$
>
> これを満たす関数$u$を**調和関数**と呼ぶ

また、$n$次元において、ラプラス方程式は次のような微分方程式を指す。
$$
\frac{\partial^2u}{\partial x_1^2}+\cdots+
\frac{\partial^2u}{\partial x_n^2}=0
$$

特に、**この記事では境界の状態が既に決まっている状況におけるラプラス方程式の解法について考える**ことに注意。このようなラプラス方程式を**ディリクレ問題**と呼ぶ。

>[!definition] ラプラス方程式の境界値問題(ディリクレ問題)
> $f\in C(\partial\Omega)$ として
> $$
> \begin{cases}
> \Delta u=0, & \text{in }\Omega,\\
> u=f, & \text{on }\partial\Omega
> \end{cases}
> $$

ではラプラス方程式がなんなのかという話だが、主に平衡・定常状態に達した系の物理現象を記述するのによく用いられる。

例えば、熱の定常状態。つまり、熱の放出や吸収が無い系において、十分に時間が経った後に熱がどのように分布しているかを表すのが調和関数$u$である。
他にも、電磁気学において電荷が存在しない領域の電位、石鹸の膜やゴムの膜がどのように張られるかといった様々な現象で顔を出す物理現象である。

要するに、境界で値が決まっている時に、内側で"無理にない状態に落ち着く"ような物理現象はラプラス方程式に帰着出来ると言えるかもしれない。

まず、古典解の求め方について記述するが、基本的な流れは[熱方程式](/notes/mathematics/heat_equation.md)と同じである。つまり、次の手順を踏む。

1. 解の一意性を示す
2. 変数分離法とフーリエ級数で形式解を求める
3. その形式解が古典解であることを確認する。

## 弱最大値原理

解の一意性を示すため、以下の定理をまず示す。この定理が示されれば、後ほど記述するように解の一意性はほぼ自明となる。

> [!theorem] 弱最大値原理
> $\Omega\subset\mathbb R^2$ を有界領域とし、$u$ をラプラス方程式の境界値問題(ディリクレ問題)の古典解とする。このとき
>
> $$
> \min_{(x,y)\in\partial\Omega}u(x,y)
> \le u(x,y)\le
> \max_{(x,y)\in\partial\Omega}u(x,y)
> $$
>
> が$~\forall (x,y)\in\overline\Omega~$で成り立つ。

つまり、ある領域内における最小値と最大値は、境界における最小値と最大値を超えることがないと言うことである。これは、ラプラス方程式のそもそもの意味が分かっていれば直感的に明らかである。例えば、ゴム膜において内側が山のようになっていたとしたら、それは弛んでることを意味するがそれはラプラス方程式の対象ではない。

**証明**

以下のように定義を行う。方針は、内側の関数$u(x,y)$が領域内のどの点においても境界における最大値$M$を下回る、つまり$u(x,y) - M < 0 ~ \text{on} ~ \Omega$がどの点においても満たされれば良い。

$$
\begin{aligned}
\begin{cases}
M := \max_{(x, y) \in \partial \Omega} u(x, y) \\
v(x, y) := u(x, y) - M - \varepsilon (R^2 - (x^2 + y^2))
\end{cases}
\end{aligned}
$$

ただし$\varepsilon>0$は任意にとってよく、$\overline\Omega\subset\{(x,y)\ ;\ x^2+y^2<R^2\}$とすることに注意。つまり、式中の$R^2 - (x^2+y^2)$は常に正となる。

$\varepsilon (R^2 - (x^2 + y^2))$については後述するが、$u(x,y) - M < 0$を"有利"にするものだと考えてくれたら良い。というのも、このようにしないと等号が成立してしまいギリギリ証明が出来ないのだ。

ここで、内側の領域$\Omega$で最大値を取る点$(x_0,y_0)$を考える。この点が$v(x_0,y_0) > 0$を満たすと仮定する。

このとき、$u_{xx}(x_0, y_0) \leq 0$ かつ $u_{yy}(x_0, y_0) \leq 0$となることが分かる。つまり、$\Delta v \leq 0$となることが分かる。
この事実は、$u$は滑らかなので山の頂点をイメージすれば直感的に明らかである。

一方で、先ほどの定義より$\Delta v$は以下のようにギリギリ正となることが分かる。
$$
\Delta v = \Delta u + 4 \varepsilon > 0 \quad \text{in } \Omega
$$

これは不合理なので、$v(x_0,y_0) > 0$という仮定が誤り。つまり、$v(x,y) < 0$が示された。
あとは$v$を$u$に戻すだけである。

$$
u(x, y) \le M + \varepsilon (R^2 - (x^2 + y^2)) \longrightarrow M \quad (\varepsilon \rightarrow 0)
$$

以上より、証明完了.

**疑問** $~\varepsilon (R^2 - (x^2 + y^2))$ とはなんだったのか

話を整理すると、以上の証明は次のような流れであった。もし領域内部で$M$より大きい最大値を取ると考えると$\Delta v \leq 0$となるわけだが、これは$v$の定義を2回微分することで得られる$\Delta v > 0$に反するという話だった。

ここで、$\varepsilon (R^2 - (x^2 + y^2))$を付け加えないとどうなるかというと、$\Delta v > 0$の部分が$\Delta v = 0$となってしまい仮定の下で導いた$\Delta v \leq 0$と矛盾しなくなってしまうのだ！

個人的な解釈だが、以下のように理解している。

元の関数そのまま($v(x, y) := u(x, y) - M$)としてしまうと、ギリギリ等号が成立して題意が証明できないから

1. $v$に絶妙に似てる (極限で$v$になる)
2. 数学的に扱いやすい
3. 題意に対して、"有利"になる

上記の性質を満たす関数を持ってきて、そこで題意が成り立つことを示してから、$v$に近づく極限を考えるって感じ

別の表現をすると、一回"ズル"をしている関数で証明してから、元の関数に近づけてるとも言える

## 解の一意性

> [!theorem] 解の一意性
> $\Omega\subset\mathbb R^2$ を有界領域、$f\in C(\partial\Omega)$ とする。このとき、ディリクレ問題の古典解は存在すれば一意である。

ディリクレ問題の2つの解$u_1,u_2$を用いて、その差を以下のように定義する。

$$
v := u_1 - u_2
$$

この$v$もディリクレ問題を実際に満たす。
ここで先ほど示した弱最大値原理により

$$
\min_{\partial \Omega} v \le v(x, y) \le \max_{\partial \Omega} v
$$

が成り立つが、境界における$v$の値はどの点でも$0$なので、$v \equiv 0$.

## ラプラス方程式の極座標変換

「一般的な」$\Omega$ での解の構成は難しい。できても明示的に書き下せるとは限らない。ここでは

$$
\Omega=B_1:=\{(x,y)\in\mathbb R^2;\ x^2+y^2<1\}
$$

単位球上で考える。

> [!theorem] 極座標表示におけるラプラシアン(2次元)
> $$
> \begin{aligned}
> \begin{cases}
> x = r \cos \theta \\
> y = r \sin \theta 
> \end{cases}
> \end{aligned}
> \\
> u(x,y)=\widetilde u(r,\theta)
> $$
> と極座標表示を行う。このとき
> $$
> \Delta_{x,y}u
> =\widetilde u_{rr}+\frac1r\widetilde u_r+\frac1{r^2}\widetilde u_{\theta\theta}
> $$

証明は機械的に計算するだけで、面白みはない。こちらのサイトが参考になる。

[KIT数学ナビゲーション:極座標表示におけるラプラシアン (2次元)](https://w3e.kanazawa-it.ac.jp/math/category/bibun/henbibun/henkan-tex.cgi?target=/math/category/bibun/henbibun/rapurashian-2_1.html)

## 極座標表示におけるラプラス方程式の形式解と古典解

解が一意であることは既に示したので、変数分離$u(r, \theta) = \varphi(r) \eta(\theta)$を行って形式解を求める。

この変数分離によって

$$
\varphi'' \eta + \frac{1}{r} \varphi' \eta + \frac{1}{r^2} \varphi \eta'' = 0
$$

の関係式が得られるので、これを変形すると定数$\lambda$を用いて

$$
\frac{r^2 \varphi''}{\varphi} + \frac{r \varphi'}{\varphi} = -\frac{\eta''}{\eta} = \lambda
$$

を得る。これらは、非常によく知られた微分方程式なのでこれを解いて、フーリエ級数によって任意の関数を表現することで以下を得る。

$$
\begin{aligned}
\begin{cases}
\varphi(r) = r^n \\
u(r, \theta) = \displaystyle\sum_{n=1}^{\infty} r^n \left( C_n^{(1)} \cos(n\theta) + C_n^{(2)} \sin(n\theta) \right)
\end{cases}
\end{aligned}
$$

よって、次のようにラプラス方程式は解くことができる。これが実際に古典解であることもこれから示す。

> [!theorem] ラプラス方程式の古典解
> $f\in C^2(\partial B_1)$ とする。このとき
>
> $$
> \begin{aligned}
> \widetilde u(r,\theta)
> &=\frac1{2\pi}\int_0^{2\pi}f(\sigma)\,d\sigma\\
> &\quad+\sum_{n=1}^{\infty}r^n
> \left(
> \int_0^{2\pi}f(\sigma)\frac1{\sqrt\pi}\sin(n\sigma)\,d\sigma
> \right)\frac1{\sqrt\pi}\sin(n\theta)\\
> &\quad+\sum_{n=1}^{\infty}r^n
> \left(
> \int_0^{2\pi}f(\sigma)\frac1{\sqrt\pi}\cos(n\sigma)\,d\sigma
> \right)\frac1{\sqrt\pi}\cos(n\theta)
> \end{aligned}
> $$
>
> として、
>
> $$
> u(x,y):=\widetilde u(r,\theta)
> $$
>
> とすると、$u$ は
>
> $$
> \begin{cases}
> \Delta_{x,y}u=0, & \text{in }B_1,\\
> u=f, & \text{on }\partial B_1
> \end{cases}
> $$
>
> の古典解。

これが古典解であることを示す上で、再確認しておくとやることは簡単で$~\Delta_{x,y}u=0 \text{in }B_1~$と$~u=f, \text{on }\partial B_1~$を示すだけである。

しかしながら、微分・極限を考えるにしても無限級数が登場するので、そのために本当にそれらの操作が出来るのかという確認が必要なのである。

まず、$\widetilde u(r,\theta)$の各項を$u_n$とする。

$$
u_n = r^n (a_n \cos(n\theta) + b_n \sin(n\theta))
$$

ここで、$|a_n|$と$|b_n|$を上から抑える不等式を作っておく。$f$は2回微分可能であることに注意すると、部分積分を行うことで以下のような評価が出来る。

$$
\begin{aligned}
|a_n| &= \left| \frac{1}{\sqrt{\pi}} \int_0^{2\pi} f(\sigma) \frac{1}{\sqrt{\pi}} \cos(n\sigma) \, d\sigma \right| \\
&= \left| -\frac{1}{n^2 \pi} \int_0^{2\pi} f''(\sigma) \cos(n\sigma) \, d\sigma \right| \\
&\le \left( \max_{\sigma \in [0, 2\pi]} |f''(\sigma)| \right) \frac{2}{n^2} \\
&= \frac{C}{n^2}
\end{aligned}
$$

$|b_n|$についても同様の評価が可能。

以下、$0 \leq r \le h < 1$ の領域について考える。

**$~\Delta_{x,y}u=0 \text{in }B_1~$ 項別微分の正当性**

まず、微分級数の和が収束することを示す。$k=a+b$に注意。

$$
\begin{aligned}
\frac{\partial^k}{\partial r^a \partial \theta^b} u_n &= n(n-1)\cdots(n-a+1) \, r^{n-a} 
\left[ a_n \cdot n^b \frac{d^b}{d\theta^b}(\cos n\theta) + b_n \cdot n^b \frac{d^b}{d\theta^b}(\sin n\theta) \right] \\
&< n^k r^{n-a} (a_n + b_n) \\
&< n^k h^{n-a} (a_n + b_n)
\end{aligned}
$$

$$
|n^k h^{n-a} (a_n + b_n)| \le C n^{k-2} h^{n-a} =: M_n
$$

と定義して、この$M_n$の級数が収束することが示せれば良い。実際に、ダランベールの収束判定法を用いることでこのことは簡単に確認できる。

$$
\lim_{n \to \infty} \frac{M_{n+1}}{M_n} = \lim_{n \to \infty} \left( \frac{n+1}{n} \right)^{k-2} h = h < 1
$$

以上より、微分級数が一様収束することが確認できた。

よって、単位球$B_1$上で、何階でも項別微分して良いことが示された。あとは機械的な計算を行うだけで$~\Delta_{x,y}u=0 \text{in }B_1~$が簡単に示される。

**境界条件の確認**

まず、$\sum$と$\lim$の交換を正当化するために$0 < r \leq 1$上で$u$が一様収束することを示す。$0<r<1$の時は先ほど示した通りである。

$$
\vert{}u_n(r, \theta)\vert{} \le 1^n \cdot (\vert{}a_n\vert{} + \vert{}b_n\vert{}) \le \frac{2C}{n^2} =: N_n
$$

で、$N_n$は$n^{-2}$のオーダーなのでこの級数は収束することが分かる。(ゼータ関数などを使えば良い)

ここで、$r \rightarrow 1-$を考える。

$$
\begin{aligned}
\lim_{r \to 1^-} \tilde{u}(r, \theta) &= \lim_{r \to 1^-} \left( \frac{a_0}{2} + \sum_{n=1}^{\infty} r^n (a_n \cos(n\theta) + b_n \sin(n\theta)) \right) \\
&= \frac{a_0}{2} + \sum_{n=1}^{\infty} \lim_{r \to 1^-} \left\{ r^n (a_n \cos(n\theta) + b_n \sin(n\theta)) \right\} \\
&= \frac{a_0}{2} + \sum_{n=1}^{\infty} (a_n \cos(n\theta) + b_n \sin(n\theta)) \\
&= f(\theta)
\end{aligned}
$$

> $f\in C^2(\partial B_1)$ なので、$f$ を $2\pi$周期関数とみなせば、そのフーリエ級数は一様収束し $f$ に一致することに注意

なので、$\lim_{r \to 1^-} \tilde{u}(r, \theta) = f(\theta)$が示された。よって境界条件も満たされる。

## ポアソン核による古典解の表示

> [!definition] ポアソン積分
>
> $$
> P(r,\theta):=\frac1{2\pi}\cdot
> \frac{1-r^2}{1+r^2-2r\cos\theta}
> $$
>
> を**ポアソン核**と呼ぶ。
> また、$f(\theta)$ を周期 $2\pi$ の連続関数として、
>
> $$
> \int_0^{2\pi}P(r,\theta-\sigma)f(\sigma)\,d\sigma
> \qquad(0\le r<1,\ 0\le\theta<2\pi)
> $$
>
> を **ポアソン積分** という。


先ほど、我々はラプラス方程式の古典解を得たわけだが、ポアソン核を用いることで以上のように変形出来る。これが実際に解になっていることは後ほど示す。

ポアソン積分とはつまり、境界の値のみ内部の値が決まるという事実を端的に示した数式であるとも言える。ポアソン核の部分は、境界の値に依らないため、実質的に$u$を決めているのは$f(\theta)$つまり境界の値だけなのだ。

$$
\begin{aligned}
u(r, \theta) &= \frac{1}{2\pi} \int_0^{2\pi} f(\sigma) \, d\sigma + \sum_{n=1}^{\infty} \frac{r^n}{\pi} \int_0^{2\pi} f(\sigma) \{ \cos(n\sigma) \cos(n\theta) + \sin(n\sigma) \sin(n\theta) \} \, d\sigma \\
&= \frac{1}{2\pi} \int_0^{2\pi} f(\sigma) \left( -1 + 2 \sum_{n=0}^{\infty} r^n \cos(n(\theta - \sigma)) \right) d\sigma
\end{aligned}
$$

最後、$\sum$について$n=1$からではなく$n=0$からになったことに注意。

$$
\begin{aligned}
-1 &+ 2 \sum_{n=0}^{\infty} r^n \cos(n(\theta - \sigma)) \\
&= -1 + 2 \operatorname{Re} \sum_{n=0}^{\infty} \left( r e^{i(\theta - \sigma)} \right)^n \\
&= -1 + \operatorname{Re} \frac{1}{1 - r e^{i(\theta - \sigma)}} \\
\cdots &= \frac{1 - r^2}{1 + r^2 - 2r \cos(\theta - \sigma)}
=: P(r,\theta)
\end{aligned}
$$

よって
$$
u = \int_0^{2\pi}P(r,\theta-\sigma)f(\sigma)\,d\sigma
$$

## ディラック問題におけるポアソン積分

> [!theorem] ディラック問題におけるポアソン積分
> $f$ を周期 $2\pi$ の連続関数とする。
>
> $$
> \widetilde u(r,\theta)
> =\int_0^{2\pi}P(r,\theta-\gamma)f(\gamma)\,d\gamma
> \qquad
> (0\le r<1,\ 0\le\theta<2\pi)
> $$
>
> で定める。
>
> このとき $\widetilde u$ は $r=1$ まで連続的に拡張でき、
>
> $$
> u(x,y)=\widetilde u(r,\theta)
> $$
>
> とおくと、
>
> $$
> \begin{cases}
> \Delta u=0, & \text{in }B_1,\\
> u=f, & \text{on }\partial B_1
> \end{cases}
> $$
>
> の一意な古典解となる。

まず、ポアソン核に以下の性質があることを確認しておく。以下の性質は、[ポアソン核の記事](/notes/mathematics/poisson_kernel.md)で説明するのでここでは省く。

$$
\begin{aligned}
\begin{cases}
P(r, \theta) > 0 \quad (0 \le r < 1, \, 0 \le \theta < 2\pi) & \text{(i)} \\
\displaystyle\int_0^{2\pi} P(r, \theta) \, d\theta = 1 & \text{(ii)} \\
\displaystyle\lim_{r \to 1^-} \sup_{\delta \le |\theta| \le \pi} P(r, \theta) = 0 \quad (0 < \delta \le \pi) & \text{(iii)}
\end{cases}
\end{aligned}
$$

**1. $\Delta u=0, \text{in }B_1$ を示す**

省略

**2. $\lim_{r \to 1^-} \tilde{u}(r, \theta) = f(\theta)$ を示す**

$$
\begin{aligned}
\tilde{u}(r, \theta) - f(\theta) &= \int_0^{2\pi} P(r, \theta - \sigma) f(\sigma) \, d\sigma - f(\theta) \int_0^{2\pi} P(r, \theta - \sigma) \, d\sigma \\
&= \int_0^{2\pi} \{ f(\sigma) - f(\theta) \} P(r, \theta - \sigma) \, d\sigma
\end{aligned}
$$

を考える。ポアソン核の性質(iii)を使うために、次のように積分領域を分割する。

$$
\begin{aligned}
\begin{cases}
I_1 = \displaystyle\int_{|\sigma - \theta| < \delta} \{ f(\sigma) - f(\theta) \} P(r, \theta - \sigma) \, d\sigma \\[12pt]
I_2 = \displaystyle\int_{\delta \le |\sigma - \theta| \le \pi} \{ f(\sigma) - f(\theta) \} P(r, \theta - \sigma) \, d\sigma
\end{cases}
\end{aligned}
$$

$I_1$について考える。ポアソン核の性質(ii)を用いて以下のように評価できる。
また、$f$は連続なことに注意すると
$
|\gamma-\theta|<\delta \quad\Longrightarrow\quad |f(\gamma)-f(\theta)|<\varepsilon
$
だから

$$
\begin{aligned}
|I_1| &\le \int_{|\sigma - \theta| < \delta} |f(\sigma) - f(\theta)| P(r, \theta - \sigma) \, d\sigma \\
&\le \varepsilon \int_0^{2\pi} P(r, \theta - \sigma) \, d\sigma \\
&= \varepsilon
\end{aligned}
$$

$I_2$について考える。$|f(\sigma) - f(\theta)| \le 2 \sup |f|$だから

$$
\begin{aligned}
|I_2| &\le 2 \sup |f| \int_{\delta \le |\sigma - \theta| \le \pi} P(r, \theta - \sigma) \, d\sigma \\
&\le 2 \sup |f| \sup_{\delta \le |\sigma| \le \pi} P(r, \sigma) \int_{\delta \le |\sigma - \theta| \le \pi} d\sigma
\end{aligned}
$$

$$
\lim_{r \to 1^-} |I_2| \le 2 \sup |f| \lim_{r \to 1^-} \sup_{\delta \le |\sigma| \le \pi} P(r, \sigma) \int_{\delta \le |\sigma - \theta| \le \pi} d\sigma = 0
$$

以上、$|I_1|$と$|I_2|$が上から評価できたので

$$
\limsup_{r \to 1^-} |\tilde{u}(r, \theta) - f(\theta)| \le \varepsilon
$$

で、$\varepsilon > 0$は任意であったので、以下を得る。

$$
\tilde{u}(r, \theta) \longrightarrow f(\theta) \quad (r \to 1^-)
$$

## 平均値の性質

> [!theorem] 平均値の性質
> $\Omega\subset\mathbb R^2$ を領域とし、$u$ を $\Omega$ 上の調和関数とする。
>
> $\overline{B_r(x,y)}\subset\Omega$ かつ $r>0$ ならば、
>
> $$
> u(x,y)
> =\frac1{2\pi}
> \int_0^{2\pi}
> u(x+r\cos\theta,y+r\sin\theta)\,d\theta
> $$
> $$
> u(x,y)
> =\frac1{\pi r^2}
> \iint_{B_r(x,y)}u(s,t)\,ds\,dt
> $$
>
> である。

ポアソン積分より、$(x,y)=(0,0)$において

$$
u(0,0) = \frac1{2\pi}\int_0^{2\pi}u(r\cos\theta,r\sin\theta)\,d\theta
$$

$(0,0)$以外の点$(x_0,y_0)$についても、その分平行移動すれば良いだけなので一般にこれは成り立つ。

また、面積についても

$$
\begin{aligned}
\iint_{B_r(x,y)}u(s,t)\,ds\,dt
&=\int_0^r\int_0^{2\pi}
u(x+\rho\cos\theta,y+\rho\sin\theta)\,d\theta\,\rho\,d\rho\\
&=\int_0^r 2\pi u(x,y)\rho\,d\rho\\
&=\pi r^2u(x,y).
\end{aligned}
$$

よって、

$$
u(x,y)
=\frac1{\pi r^2}
\iint_{B_r(x,y)}u(s,t)\,ds\,dt.
$$

## 強最大値原理

> [!theorem] 強最大値原理
> $\Omega\subset\mathbb R^2$ を有界な領域とする。
> $u$ は $\Omega$ 上調和で、$\overline\Omega$ 上連続とする。
>
> このとき、もし $u$ が $\Omega$ 内で境界を含めた最大値を達成するならば、$u$ は定数関数である。
>
> すなわち、
>
> $$
> \exists (x_0,y_0)\in\Omega
> \quad\text{s.t.}\quad
> u(x_0,y_0)=\max_{\overline\Omega}u
> $$
>
> ならば、$u$ は定数である。

## Leouvilleの定理

> [!theorem] Liouville の定理
> $\mathbb R^2$ 上の有界な調和関数は定数関数である。