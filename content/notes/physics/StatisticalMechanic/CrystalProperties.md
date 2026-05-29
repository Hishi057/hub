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
\therefore q_x(t) = \varphi_0 \cos\left( w(k) t + \theta_0 \right) \xi_x^{(k)}

\qquad

w(k) \coloneqq \sqrt{\frac{\alpha^{(k)}}{m}}
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
\\
\therefore w(k) = 2\sqrt{\frac{\kappa}{m}}\sin{\frac{ak}{2}}
$$

教科書において、固有ベクトルの導出はやや天下りになっている。
固有ベクトルは$e^{i\theta}$を含む形になっているとまず予測され、実際に整合性がとれることを確認したのでokという構成になっている。
両端の粒子を固定しているという条件を取り入れるために$x=0, (N+1)a$で$q_x = 0$とすると、$e^{i\theta}$が$\sin$に決定される。

解析力学を用いると、最終的なハミルトニアンはこうなる。

$$
\begin{aligned}
\psi_k &= \frac{\partial L(\boldsymbol{\varphi}, \dot{\boldsymbol{\varphi}})}{\partial \dot{\varphi}_k} 
\\
&= m \dot{\varphi}_k 
\\
&= m \sum_{x \in \mathcal{X}} \xi_x^{(k)} \dot{q}_x 
\\
&= \sum_{x \in \mathcal{X}} \xi_x^{(k)} p_x 
\end{aligned}
$$

$$
\begin{aligned}
H(\boldsymbol{\varphi}, \boldsymbol{\psi}) &\coloneqq \sum_{k \in \mathcal{K}} \psi_k \dot{\varphi}_k - L(\boldsymbol{\varphi}, \dot{\boldsymbol{\varphi}}) = \sum_{k \in \mathcal{K}} \left\{ \frac{1}{2m} (\psi_k)^2 + \frac{\alpha^{(k)}}{2} (\varphi_k)^2 \right\} \\

&= \sum_{k \in \mathcal{K}} \frac{1}{2m} \left\{ (\psi_k)^2 + m^2 (\omega(k))^2 (\varphi_k)^2 \right\}
\end{aligned}
$$

### 三次元の結晶

前節の結論を一般化すると、三次元における振動数は次のようになる。

$$
\omega(\vec{k}) = 2 \sqrt{\frac{\kappa}{m}} \sqrt{ \left(\sin \frac{a k_x}{2}\right)^2 + \left(\sin \frac{a k_y}{2}\right)^2 + \left(\sin \frac{a k_z}{2}\right)^2 }
$$

よって、調和振動子1つのエネルギー期待値を自由度$3N$の分だけかければよろしい。

$$
\langle \hat{H} \rangle_\beta^{\text{can}} = 3 \sum_{\vec{k} \in \mathcal{K}} \left( \frac{\hbar \omega(\vec{k})}{2} + \frac{\hbar \omega(\vec{k})}{e^{\beta \hbar \omega(\vec{k})} - 1} \right)
\\
= E_0 + 3 \sum_{\vec{k} \in \mathcal{K}} \frac{\hbar \omega(\vec{k})}{e^{\beta \hbar \omega(\vec{k})} - 1} \qquad \left( E_0 \coloneqq 3 \sum_{\vec{k} \in \mathcal{K}} \frac{\hbar \omega(\vec{k})}{2} \right)
$$

$$\hbar \omega(\vec{k}) \ll k_B T \iff \beta \hbar \omega(\vec{k}) \ll 1 \quad \text{のとき、} \quad \langle \hat{H} \rangle_\beta^{\text{can}} \to 3 N k_B T$$

以上のように、デュロン・プティの法則が成り立っていることが確認できる。

次に、低温状態$\hbar \omega(\vec{k}) \gg k_B T \iff \beta \hbar \omega(\vec{k}) \gg 1 $ における比熱について考える。

まず、低温状態において$sinx \simeq x$を用いると

$$
\omega(\vec{k}) \simeq \sqrt{\frac{\kappa}{m}}a|\vec{k}| = v_0 |\vec{k}|
$$

が得られる。これを元に、エネルギー期待値の式変形を行なっていく。
次の式変形は中々ハードである。

$$
\begin{aligned}
\langle \hat{H} \rangle_\beta^{\text{can}} &= E_0 + \frac{3V_0}{\pi^3} \int_{0}^{\frac{\pi}{a}} d^3k \frac{\hbar \omega(\vec{k})}{e^{\beta \hbar \omega(\vec{k})} - 1}
\\
&= E_0 + \frac{3V_0}{8\pi^3} \int_{-\frac{\pi}{a}}^{\frac{\pi}{a}} d^3k \frac{\hbar \omega(\vec{k})}{e^{\beta \hbar \omega(\vec{k})} - 1}
\\
&\simeq E_0 + \frac{3V_0}{8\pi^3} \int_{0}^{\infty} 4\pi k^2 dk \frac{\hbar \omega(\vec{k})}{e^{\beta \hbar \omega(\vec{k})} - 1}
\end{aligned}
$$

結果にあまり影響を及ぼさないので、積分範囲を広くした。 $x = \hbar \beta v_0 k $ で置換を行う。

$$
\begin{aligned}
\langle \hat{H} \rangle_\beta^{\text{can}} &= E_0 + \frac{3V_0}{2\pi^2} \cdot \frac{1}{\hbar^3 \beta^3 v_0^3} \int_{0}^{\infty} \frac{dx}{\hbar \beta v_0} \cdot \frac{(\hbar \beta v_0 k)^3}{e^{\hbar \beta v_0 k} - 1}
\\
&= E_0 + \frac{3V_0}{2\pi^2 \hbar^3 \beta^4 v_0^3} \int_{0}^{\infty} dx \frac{x^3}{e^x - 1} \qquad \left( \because \int_{0}^{\infty} \frac{x^3}{e^x - 1} dx = \frac{\pi^4}{15} \right)
\\
&= E_0 + \frac{\pi^2 V_0}{10 \hbar^3 v_0^3} \cdot (k_B T)^4
\end{aligned}
$$

$$
\therefore c(T) = \frac{d}{dT} \langle \hat{H} \rangle_\beta^{\text{can}} = \frac{2\pi^2 k_B^4 V_0}{5\hbar^3 v_0^3} T^3
$$

よって、低温状態のときに比熱が$T^3$のオーダーで減少していくことが示された。

ところで、複雑な計算を行ったがオーダーだけなら、実はこれが成り立つ理由は極めて雑な近似によってでも考えることが出来る。

低温状態でも、$\hbar \omega(\vec{k}) \leq k_B T$となって「生き残って」振動している粒子がいくつかは存在しているはずである。
$$
\hbar \omega(\vec{k}) = \hbar v_0k \leq k_B T \\
\therefore k \leq \frac{k_B T}{\hbar v_0}
$$
これは、原点から半径$k$以内に存在する粒子が「生き残る」ことを表している。その$k$は$T$に比例するから、
三次元において「生き残る」粒子の数は$T^3$に比例すると考えられる。