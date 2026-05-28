---
title: 4. 古典近似
---

## 古典近似

> [!definition] 古典近似における分配関数
> $$
> Z(\beta) = \frac{1}{N!} \left( \frac{m}{2\pi \hbar^2 \beta} \right)^{\frac{3}{2}N} \int d^3\bm{r}_1 \cdots d^3\bm{r}_N \, e^{-\beta V(\bm{r}_1, \dots, \bm{r}_N)}
> $$

「互いに区別出来ないN個の系が、ある位置である運動量になる確率をエネルギーの重みに応じて全空間で足し合わせたもの」

分配関数とは、先ほど見たように離散的な値を取るものであった。
これはすなわち、系のとるエネルギー準位が離散的であったからだが、量子効果を無視できるほど温度が高かったり密度が低いマクロな視点において、その値は連続的とみなすことが出来るようになる。

よって、系のエネルギーの古典的な表示を用いて、分配関数を再び導出したものが、上記の式である。この表式によって、様々な物理現象が後で見るように簡潔に記述出来るようになる。

**導出**

1. 系のエネルギーを古典的な方法で記述する.
2. 確率密度を考えて、分配関数に相当する関数を見つける.
3. 分配関数に相当する関数の物理次元を調整する
4. 運動量部分の積分については分離できて、系の状態に依らずいつでも特定の値になることを示す

まず、系のエネルギーを古典的な方法で記述すると以下のようになる。

$$
V(\bm{r}_1, \dots, \bm{r}_N) = \sum_{\substack{i,j=1 \\ (i<j)}}^{N} V_{\mathrm{int}}(|\bm{r}_i - \bm{r}_j|) + \sum_{i=1}^{N} V_{\mathrm{ext}}(\bm{r}_i) \\

H(\bm{r}_1, \dots, \bm{r}_N, \bm{p}_1, \dots, \bm{p}_N) = \sum_{i=1}^{N} \frac{|\bm{p}_i|^2}{2m} + V(\bm{r}_1, \dots, \bm{r}_N)
$$

中々ゴツい見た目だが、運動エネルギーと位置エネルギーに分けて、更に位置エネルギーは相互作用によるエネルギーとそうでないエネルギーで分けているだけである。

すると、確率密度が次のように表せる。

$$
p^{(\mathrm{can}, \beta)} := \frac{e^{-\beta H}}{\int d^3\bm{r}_1 \cdots d^3\bm{r}_N \, d^3\bm{p}_1 \cdots d^3\bm{p}_N \, e^{-\beta H}}
$$

「位置と運動量を全部指定する」 $\\$
$\rightarrow$ 「エネルギー $H$ が一意に決まる」 $\\$
$\rightarrow$ 「その状態が出現する確率密度がボルツマン因子（$e^{-\beta H}$）の比で決まる」

ということである。

この確率密度の分母を眺めると、分配関数に相当するものではないかと考えることが出来る。

$$
Z(\beta)? = \int d^3\bm{r}_1 \cdots d^3\bm{r}_N \, d^3\bm{p}_1 \cdots d^3\bm{p}_N \, e^{-\beta H}
$$

しかし、分配関数とは本来無次元である。そこで、プランク定数$h$で次元を調整することを試みる。
分配関数の中身の値は変わってしまうが、実は分配関数の値に関して定数倍する分には、実は問題無いのだ。
また、それぞれの系は区別しないので$N!$で割ることを考えて、分配関数の古典近似における表式を得ることとなる。

$$
Z(\beta) = \frac{1}{N!h^{3N}} \int d^3\bm{r}_1 \cdots d^3\bm{r}_N \, d^3\bm{p}_1 \cdots d^3\bm{p}_N \, e^{-\beta H}
$$

ところで、$H = \sum_{i=1}^{N} \frac{|\bm{p}_i|^2}{2m} + V(\bm{r}_1, \dots, \bm{r}_N)$ は$e$の肩に乗っているから、$Z(\beta)=$ ($p$に関する項)$\times$(rに関する項)といった風に綺麗に分離することが出来る。

さらに、($p$に関する項)について、これは系に依らず毎回一定の値を取る。

$|p_i|^2 = p_x^2 + p_y^2 + p_z^2$であることと、ガウス積分を用いる。

$$
\int d^3\bm{p}_i \, e^{-\beta |\bm{p}_i|^2 / 2m} = \left( \int_{-\infty}^{\infty} dp \, e^{-\frac{\beta p^2}{2m}} \right)^3 = \left( \sqrt{\frac{2m\pi}{\beta}} \right)^3
$$

よって、これを元の分配関数の表式に代入することで、また$h=2\pi \hbar$であることを用いて、最初に述べた古典近似における分配関数の簡潔な表式を得ることが出来る。

### 具体例1: 調和振動子とエネルギー等分配則

上記の結論を、調和振動子に適用してみる。

まず、調和振動子1つからなる系について考える。ポテンシャルエネルギーは$V(x)=\frac{m\omega^2}{2}x^2$なので、分配関数はガウス積分を用いて次のように計算できる。

$$
\begin{align*}
Z(\beta) &= \left( \frac{m}{2\pi \hbar^2 \beta} \right)^{\frac{1}{2}} \int_{-\infty}^{\infty} dx \exp\left( -\beta \frac{m \omega^2}{2} x^2 \right) \\

&= \left( \frac{m}{2\pi \hbar^2 \beta} \right)^{\frac{1}{2}} \left( \frac{2\pi}{\beta m \omega^2} \right)^{\frac{1}{2}} \\

&= \frac{1}{\hbar \omega \beta}
\end{align*}
$$

次に、互いに独立した$n$つの粒子と、そのうちの$m$つが調和振動子である系を考える。
ハミルトニアンは次の通りであるから

$$
H = \sum_{i=1}^{N} \frac{p_i^2}{2m_i} + \sum_{i=1}^{M} \frac{m_i \omega_i^2 }{2}x_i^2
$$

分配関数を求める。直前の調和振動子一つだけの系の計算結果を用いることと、その後に残る項を次のように置き換えることに注意する。$\nu_{N-M} = \int dx_{M+1}dx_{M+2}\cdots dx_N$

$$
\begin{align*}
Z(\beta) &= \left( \frac{m}{2\pi \hbar^2 \beta} \right)^{\frac{3N}{2}} \int_{-\infty}^{\infty} dx_1 dx_2 \dots dx_N \exp\left( -\beta \frac{m_i \omega_i^2 x_i^2}{2} \right)\\
&=
\beta^{-\frac{M+N}{2}} \times \mathcal{V}_{N-M} \prod_{i=1}^{N} \left( \frac{m_i}{2\pi \hbar} \right)^{\frac{1}{2}} \prod_{i=1}^{M} \left( \frac{2\pi}{m_i \omega_i^2} \right)^{\frac{1}{2}}
\end{align*}
$$

エネルギーの期待値を考えるにあたって$\beta$に依存しない係数に興味はない。
分配関数が明らかになったので、エネルギー期待値は一瞬で求められる。

$$
\log Z(\beta) = -\frac{M+N}{2} \log \beta + \log ( \, \sim \, ) \\

\therefore
-\frac{d}{d\beta} \log Z(\beta) = \frac{M+N}{2} \cdot \frac{1}{\beta}
= (M+N)\frac{k_B T}{2}
$$

この驚くほど単純な計算結果に着目する。
実は、**ハミルトニアンが位置座標の二乗と運動量の二乗の和で記述できる系**において、項の数だけエネルギー$\frac{kT}{2}$が配分されていると考えると、複雑な積分計算をしなくともエネルギー期待値の値を出すことが出来るのだ。この事実を**エネルギー等分配則**と呼ぶ。

### 具体例2: 一様重力中における理想気体

$N$個の粒子が$L \times L \times H$の空間を飛び回る系を考える。
ハミルトニアンは次の通り

$$
H = \sum_{i=1}^{N} \frac{\boldsymbol{p}_i^2}{2m} + \sum_{i=1}^{N} mgz_i
$$

まず、$N=1$における分配関数を計算する。

$$
\begin{align*}

\int d^3\boldsymbol{r} \, e^{-\beta m g z} &= \int_{0}^{L} dx \int_{0}^{L} dy \int_{0}^{H} e^{-\beta m g z} dz\\

&= L^2 \int_{0}^{H} e^{-\beta m g z} dz \\

&= \frac{L^2}{\beta m g} \left( 1 - e^{-\beta m g H} \right)
\end{align*}
$$

これを元に、一般のときの分配関数を計算すると次の通り。

$$
\begin{align*}
Z(\beta) &= \frac{1}{N!} \left( \frac{m}{2\pi \hbar^2 \beta} \right)^{\frac{3N}{2}} \int d^3\boldsymbol{r}_1 \dots d^3\boldsymbol{r}_n \, e^{-\beta \sum_{i} m g z_i} \\

&= \frac{1}{N!} \left( \frac{m}{2\pi \hbar^2 \beta} \right)^{\frac{3N}{2}} \left( \frac{L^2}{\beta m g} \right)^N \left( 1 - e^{-\beta m g H} \right)^N \\

&= \left( \frac{1 - e^{-\beta m g H}}{\beta^{\frac{5}{2}}} \right)^N \cdot (\sim)
\end{align*}
$$

$\beta$に着目してエネルギー期待値を計算すると

$$
\langle \hat{H} \rangle_\beta^{can} = \frac{5}{2} N k_B T - \frac{N m g H}{e^{\beta m g H} - 1}
$$

この計算結果について考える。

$(\text{i})~$高温つまり $\beta mgH \ll 1 ~ \therefore mgH \ll k_B T$ において $\\$
$~$ $e^{\beta m g H} \simeq 1+\beta mgH$と近似できるので $\\$
$$
\langle \hat{H} \rangle_\beta^{can} \rightarrow \frac{3}{2} N k_B T
$$

高校物理の気体分子運動論で導いた単原子理想気体のモル比熱と結果が一致する。また、自由度は$3$なのでエネルギー等分配則が成り立っている。

$(\text{ii})~$低温つまり $\beta mgH \gg 1 ~ \therefore mgH \gg k_B T$ において
$$
\langle \hat{H} \rangle_\beta^{can} \rightarrow \frac{5}{2} N k_B T
$$

重力が強く、低い位置に粒子が溜まっていると考えられる。そのためモル比熱が大きくなるのは、温度を上げる際に粒子を持ち上げるためのエネルギーも必要と解釈することが出来る。

