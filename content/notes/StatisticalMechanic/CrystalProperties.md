---
title: 5. 結晶の性質
---

---

## 結晶の性質

これまでの成果──特に、調和振動子の結果を応用して、結晶の物的性質について調べる。田崎晴明「統計力学 I」の第六章に沿って、以下の順番で話を進める。

1. 歴史的経緯の説明
2. 格子振動の力学(1次元)
3. 格子振動の力学(3次元)
4. 三次元の結晶の低温での振る舞い

### 歴史的経緯

結晶中の粒子が、お互いに干渉せず各々の位置で振動していると考える最も単純なモデルを考えると、調和振動子のエネルギーの期待値の結果より、結晶全体のエネルギー期待値とモル比熱は

$$
\langle \hat{H} \rangle_\beta^{can} = 3NkT = 3nRT \\
\therefore ~c(T) \coloneqq \frac{d}{dT}(\frac{\langle \hat{H} \rangle_\beta^{can}}{n}) = 3R
$$

となる。
実際に、デュロンとプティによって1819年、多くの固体のモル比熱が$3R \simeq 24.9 ~ \text{J{(mol K)}}^{-1} $ に近い値を取ることが観測された。(これだけ単純なモデルでも、統計力学の成果が出ているのはすごい！)

ところが、このモデルでは低温でモル比熱が$3R$より小さくなったり、物質ごとに異なる理由が説明できなかった。

その後アインシュタインの提唱したモデルによって、低温部分の理論的説明について前進はしたものの、また新たな問題点が生じていくこととなる。その問題点を今から見る統計力学(というか量子力学？)の成果によって解決していくこととなる。

### 格子振動の力学(1次元)

設定は次の通りである。

$N$個の粒子が、横一列に間隔$a$を保って並んでいるとする。つまり$x \in \chi \coloneqq \{a,2a,\cdots ,Na \}$とする。隣り合う粒子は、自然長$a$バネ定数$\kappa$のバネで結ばれているとする。

特に左から$k$番目の粒子は中心$ka$の何かしらの振動をすると予想されるが、座標$x$からの相対座標を$q_x$とする。$x$は、粒子そのものを指してると考えても良い。

座標$x$に位置した粒子にのみ着目した運動方程式は次の通りである。

$$
\begin{align*}
m \ddot{q}_x(t) &= -\kappa (q_x(t) - q_{x+a}(t)) -\kappa (q_x(t) - q_{x-a}(t)) \\
&= -2\kappa q_x(t) + \kappa q_{x+a}(t) + \kappa q_{x-a}(t)
\end{align*}
$$

この式が$N$本立つわけだが、煩わしいので以下に示す**実対称行列**$K$を導入することにする。

$$
K_{x,x'} =
\begin{cases} 2\kappa & x = x' \\ -\kappa & |x - x'| = a \\ 0 & \text{otherwise}
\end{cases}
\\
K = \begin{bmatrix} 2\kappa & -\kappa & 0 & 0 & \\ -\kappa & 2\kappa & -\kappa & 0 & \\ 0 & -\kappa & 2\kappa & -\kappa & \\ 0 & 0 & -\kappa & 2\kappa & \\ & & & & \ddots 
\end{bmatrix}
$$

これによって、元の運動方程式は以下のように記述できるようになる。

$$
m \ddot{q}_x(t) = -\sum_{x' \in X} K_{x,x'} q_{x'}(t)
$$
更に、以下のように記述する。
$$
m
\begin{pmatrix} 
\ddot{q}_0(t) \\ \ddot{q}_1(t) \\ \vdots 
\end{pmatrix} 
= -K 
\begin{pmatrix} 
q_0(t) \\ q_1(t) \\ \vdots 
\end{pmatrix}
$$

$$
\Leftrightarrow m \ddot{\boldsymbol{q}}(t) = -K \boldsymbol{q}(t)
$$

ここまでで、行列を用いて$N$本の運動方程式を簡潔に記述できるようになった。
これより線形代数の性質を用いて、この運動について調べていく。

行列$K$は実対称行列なので、線形代数の成果によって
$N$本の固有値とそれに対応する固有ベクトルが存在することが分かっている。更に、互いに異なる固有ベクトルは直交することが知られている。

$\alpha^{(k)}$ : $k$番目の固有値$\\$
$\boldsymbol{\xi}^{(k)}$ : $k$番目の固有ベクトル（規格化済み）$\\$

$$
K \boldsymbol{\xi}^{(k)} = \alpha^{(k)} \boldsymbol{\xi}^{(k)}

\\

\Leftrightarrow K 
\begin{pmatrix} 
\xi_0^{(k)} \\ \xi_a^{(k)} \\ \vdots 
\end{pmatrix} = \alpha^{(k)} 
\begin{pmatrix} 
\xi_0^{(k)} \\ \xi_a^{(k)} \\ \vdots 
\end{pmatrix}

\\

\therefore \sum_{x' \in X} K_{x,x'} \xi_{x'}^{(k)} = \alpha^{(k)} \xi_x^{(k)}
$$

運動方程式の特殊解について考える。
運動が一つの固有振動で、次の通りに表されるとする： $q_x(t) = \varphi(t) \xi_x^{(k)}$

これによって、行列$K$の計算を固有ベクトルを用いて単純化することによって、解析解が求められるようになる。

$$
\begin{cases} 
q_x(t) = \varphi(t) \xi_x^{(k)} \\ m \ddot{q}_x(t) = -\sum_{x' \in X} K_{x,x'} q_{x'}(t) 
\end{cases}
\\
\begin{align*}
\Rightarrow m \ddot{\varphi}(t) \xi_x^{(k)} 
&= -\varphi(t) \sum_{x' \in X} K_{x,x'} \xi_{x'}^{(k)}\\
&= -\varphi(t) \alpha^{(k)} \xi_x^{(k)} \\
\iff \ddot{\varphi}(t) &= -\alpha^{(k)} \varphi(t)
\end{align*}
$$

$\varphi_0$,$\theta_0$は初期条件の定数として、解析解は次の通りである。
$$
\therefore q_x(t) = \varphi_0 \cos\left( \sqrt{\frac{\alpha^{(k)}}{m}} t + \theta_0 \right) \xi_x^{(k)}
$$

ところでだが、元々の運動方程式は線形微分方程式であるから、今求めた解を異なる$k$について足し合わせて、最終的に一般解を以下のように表すことが出来る。

$$
q_x(t) = \sum_{k \in \mathcal{K}} \varphi_k(t) \xi_x^{(k)}
$$

また、固有ベクトルと固有値の具体的な値は次の通りである。

$$
\begin{cases}
\xi_x^{(k)} = \sqrt{\frac{2}{N+1}} \sin(kx) \\ 
\alpha^{(k)} = 4K \left( \sin \frac{ak}{2} \right)^2 
\end{cases}
$$

最終的なハミルトニアンはこうなる。

$$
H(Q, P) = \sum_{k \in \mathcal{K}} \left( \frac{P_k^2}{2m} + \frac{1}{2} m \omega_k^2 Q_k^2 \right)
$$