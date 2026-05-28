---
title: 3. カノニカル分布と分配関数
---

## カノニカル分布

> [!definition] カノニカル分布の概要
> $$
> Z(\beta) \coloneqq \sum\limits_{i} e^{-\beta E_i} \qquad (\beta = \frac{1}{k_BT})
> $$
> で定義される**分配関数**導出することが目標である。これが導出できると
> 
> **物理量の期待値**: $$ \quad \langle \hat{f} \rangle_\beta^{can} = \frac{1}{Z(\beta)} \sum\limits_{i} f_i e^{- \beta E_i} $$  
> 特に**エネルギーの期待値**: $$ \quad \langle \hat{H} \rangle_\beta^{can} = -\frac{\partial}{\partial\beta}\log{Z(\beta)} $$  
> **ヘルムホルツエネルギー**: $$ \quad F(\beta, V, N) = -\frac{1}{\beta} \log{Z_{V,N}(\beta)} $$
>
> これらの物理量が、簡単な計算で分かるようになる。

カノニカル分布は温度が一定という状況を仮定しているので実験的に扱いやすく、かつ理論的にも計算がしやすい定式化である。
この定式化によって、例えばマクロの性質である理想気体の状態方程式、比熱、帯磁率などが簡単に計算できるようになる。
カノニカル分布はミクロな視点における物理現象をもとに導出したものであるから、ミクロな世界とマクロな世界を矛盾なく結合出来る理論体系ということになる。

### 導出

#### 基本的な設定

カノニカル分布は、注目する系と、その系が一定の温度になるようにエネルギーを交換する熱浴なる系が存在すると設定する。

熱浴は一種類の粒子からなる系だとして、その体積を$V_R$, 粒子数を$N_R$ とする。

前者の系のエネルギー固有状態を$i=1,2,3\cdots$と番号付けして、対応するエネルギー固有値を$E_i$とする。同様に、後者の熱浴となる系のエネルギー固有値を$B_k$とする。二つの系に相互作用がない場合、$E_i + B_k$と書けることになる。

#### 分配関数

平衡状態にあって、全系のエネルギーが $U_{tot}$ だとして、各系のエネルギー状態は以下の条件を満たさなければいけない。

$$

U_{tot} - V_R\delta \leq E_i + B_k  \leq U_{tot} \\
\iff U_{tot} - E_i - V_R\delta \leq B_k  \leq U_{tot} - E_i

$$

$i$を固定する。この条件を満たす$k$の数は、状態数を返す関数$\Omega()$を使って

$$

\begin{align*}
\Omega_i &= N_R! \Omega_R(U_{tot} - E_i) - N_R! \Omega_R(U_{tot} - E_i - V_R\delta)\\
& \sim N_R!\Omega_R(U_{tot} - E_i)
\end{align*}

$$

と書ける。
以上のように近似できるのは、体積$V_R$が大きくなるにしたがって、熱浴の状態数$\Omega_R$が指数的に大きくなって、かつ熱浴の体積$V_R$が系の体積$V$よりも十分に大きいためである。
具体的に数式で $\Omega_R(B) = \exp[V_R\sigma(\frac{B}{V_R}, \frac{N_R}{V_R}) + o(V_R)] $ とも表現できる。

次に、前準備を行う。この変形は、かなり端折っているので注意。最後の結果だけ気にすればok

$$
\begin{align*}

\log{ \frac{\Omega_R(U_{tot} - E_i)}{\Omega_R(U_{tot})} } 
& \sim -E_i \left. \frac{\partial}{\partial U}\log\Omega_R(U) \right |_{U=U_{tot}} \\

& = -\frac{E_i}{V_R} \frac{\partial}{\partial u} \{ V_R\sigma(u, \rho) + o(V_R) \} \\

& = -E_i \frac{\partial}{\partial u} \sigma(u, \rho) \\

& = -\beta (u, \rho) E_i \\

\therefore \frac{\Omega_R(U_{tot} - E_i)}{\Omega_R(U_{tot})}
&\sim e^{-\beta E_i}

\end{align*}

$$

$\beta (u, \rho)$ とあるが、この熱浴の変数を変化させることに興味はないので単に$\beta$と置いた。前準備は以上である。

エネルギー固有状態$i$を取る確率を$p_i = \frac{\Omega_i}{\Omega_1 + \Omega_2 + \cdots}$とすると

$$

\begin{align*}

p_i &= \frac{ N_R!\Omega_R{(U_{tot} - E_i)} }{ \sum\limits_{j=1}^{n}{ N_R!\Omega_R{(U_{tot})} }} \\

&= \frac{\Omega_R(U_{tot} - E_i)}{\Omega_R(U_{tot})} \{ \sum\limits_{j=1}^n  \frac{\Omega_R(U_{tot} - E_j)}{\Omega_R(U_{tot})} \}^{-1} \\

&= \frac{e^{- \beta E_i}}{Z(\beta)}

\end{align*}

$$

と簡潔な形で書けることになる。式の中に出てきた $$ Z(\beta) = \sum\limits_{j=1}^n  \frac{\Omega_R(U_{tot} - E_j)}{\Omega_R(U_{tot})} = \sum \limits_i {e^{-\beta E_i}} $$ は分配関数と呼ばれ、単なる規格化としての定数以上に熱力学的に重要な性質を持つ。

#### 分配関数とエネルギーの期待値

$$ 
\langle \hat{f} \rangle_\beta^{can} 
= \sum\limits_i{ f_i p_i}
= \frac{1}{Z(\beta)} \sum\limits_{i} f_i e^{- \beta E_i} 
$$ 

特にエネルギー$E_i$に着目するとき

$$ 

\begin{align*}

\langle \hat{H} \rangle_\beta^{can} 
& = \frac{1}{Z(\beta)} \sum\limits_{i} E_i e^{- \beta E_i} \\

& = \frac{1}{Z(\beta)} \frac{\partial}{\partial \beta} \sum\limits_{i} e^{- \beta E_i} \\

& = -\frac{1}{Z(\beta)} \frac{\partial}{\partial \beta} Z(\beta) \\

& = - \frac{\partial}{\partial \beta} \log Z(\beta)

\end{align*}

$$ 

#### 熱浴が理想気体のとき

話を具体的に、熱浴が単原子分子からなる理想気体からなると考えると、$\beta (u, \rho) = \frac{3\rho}{2u} = \frac{3N_R}{U_{tot}}$ となり、理想気体を温度計として定義すると$U_{tot} = \frac{3}{2}nRT = \frac{3}{2}N_Rk_BT \quad (k_B = \frac{R}{N_A}) $ なので、これを代入して

$$
\beta = \frac{1}{kT}
$$

という美しい関係式を得る。なんとこれは、熱浴が理想気体でなくとも、一般に成り立つ。なぜなら、(あとで書く)

#### 分配関数とヘルムホルツエネルギー

(後で書く)

$$ \quad F(\beta, V, N) = -\frac{1}{\beta} \log{Z_{V,N}(\beta)} $$

実質的に、分配関数の対数を取るだけでヘルムホルツエネルギーが得られるということになる。

### 性質

> [!theorem] 複数の系の分配関数
> 注目している量子系が、互いに独立しているN個の部分系からできてるとき、全系の分配関数は
> 以下のように書ける。
> $$
> Z(\beta) = \prod\limits_{j=1}^{N}Z_j(\beta)
> $$

> [!theorem] 分散の表式
> エネルギーの分散は、エネルギー期待値を微分するだけで求められる。
> $$
> \langle (E - \langle E \rangle)^2 \rangle = -\frac{\partial \langle E \rangle}{\partial \beta}
> $$

**ゆらぎ散逸定理**に繋がる。

### 具体例1：理想気体

$L^3$の空間に閉じ込められた互いに独立した$N$個の粒子からなる系、つまり理想気体を量子系で考える。
量子系において、粒子一つのエネルギーは3つの整数を用いて状態エネルギーを指定される。

$$
E = E_0 \times (n_x^2+n_y^2+n_z^2)
$$

このような粒子が$n$つ存在する。よって、分配関数は次の通り。

$$
\begin{align*}
Z_{V,N}(\beta) &= \frac{1}{N!} \sum \exp\left[ -\beta E_0 \sum_{a=x,y,z} \sum_{i=1}^{N} (n_a^{(i)})^2 \right] \\

&= \frac{1}{N!} \sum \exp\left[ -\beta E_0 \left( \{n_x^{(1)}\}^2 + \{n_x^{(2)}\}^2 + \dots + \{n_y^{(1)}\}^2 + \dots + \{n_z^{(1)}\}^2 + \dots \right) \right] \\

&= \frac{1}{N!} \left( \sum_{n=1}^{\infty} \exp\left[ -\beta E_0 n^2 \right] \right)^{3N} \\
\end{align*}
$$

最後の式変形は少し跳躍しているが、意味を考えれば当たり前でもある。

例えば$n_x^{(1)}$でも$n_y^{(100)}$でもなんでも、1つの変数について考えると、これらの変数は$1$以上整数であればどんな値でも取りうる(とはいえ、数字が大きくなればなるほどその確率は指数的に減っていく)$\\$
よって、取りうるエネルギー状態を全て足し合わせると$\sum_{n=1}^{\infty} \exp\left[ -\beta E_0 n^2 \right]$となり、
このような変数が$3$(次元)$\times N$個存在する。これらは完全に互いに独立しているので、$3N$乗すればよろしい。

このままの形では扱いにくいので、積分計算出来るように近似する。

$$
x = \sqrt{\beta E_0} \, n \quad \left( dx = \sqrt{\beta E_0} \right) \\
$$

$$
\begin{aligned}
\sum_{n=1}^{\infty} \exp(-x^2)
&= \frac{1}{\sqrt{\beta E_0}} \sum_{n=1}^{\infty} \sqrt{\beta E_0} \exp(-x^2) \\
&\simeq \frac{1}{\sqrt{\beta E_0}} \int_{0}^{\infty} dx \, \exp(-x^2) \\

&= \frac{\sqrt{\pi}}{2\sqrt{\beta E_0}} \qquad \left( E_0 \coloneqq \frac{\pi^2 \hbar^2}{2mL^2} \right) \\

&= \sqrt{\frac{m}{2\pi \hbar^2 \beta}} \, L \\

\therefore \quad Z_{V,N}(\beta) &\simeq \frac{V^N}{N!} \left( \frac{m}{2\pi \hbar^2 \beta} \right)^{\frac{3N}{2}}
\end{aligned}
$$

$V=L^3$とする。このように分配関数が扱いやすい形になったので、エネルギー期待値を計算する。

$$
\begin{aligned}
\langle \hat{H} \rangle_\beta^{can} 
&= -\frac{\partial}{\partial \beta} \left[ -\frac{3N}{2} \log \beta + \dots \right] \\
&= \frac{3}{2} \cdot \frac{N}{\beta} \\
&= \frac{3}{2} N k_B T
\end{aligned}
$$

こうして、高校物理でも扱った理想気体の熱容量の同じ結論が得られたが、そもそも理想気体を用いて絶対温度$T$を定義しているので、これは統計力学の成果ではなく、整合性を確認しただけに過ぎない。

次にヘルムホルツエネルギーから、圧力$P$を求める。

$$
F(\beta; V, N) = -\frac{1}{\beta} \log Z_V(\beta)
= -\frac{1}{\beta} \{ N \log V + \dots \}
$$
$$
\begin{aligned}
P(\beta; V, N) &= -\frac{\partial}{\partial V} F(\beta; V, N) \\

&= \frac{N}{\beta} \cdot \frac{1}{V} \\

&= \frac{N}{V} k_B T \\

\therefore PV &= N k_B T \quad ( = nRT )
\end{aligned}
$$

このようにして、理想気体の状態方程式が求められた。

### 具体例2: 常磁性体

絶縁体の結晶が存在し、各々の原子が不対電子を一つずつ持ってるとする。スピン同士は本来相互作用を及ぼすが、一旦独立してると考えて話を進める。
この物体が一様磁場$(0,0,H)$に置かれてると考えて、この系の性質を調べる。

いつも通り、まずはスピン一つからなる系から考える。

$$
E_\sigma = -\mu_0 H \sigma
= \begin{cases} -\mu_0 H & (\text{磁場と同じ向き}) \\ +\mu_0 H & (\text{磁場と違う向き}) \end{cases}
$$

$$
Z_1(\beta, H) = e^{\beta \mu_0 H} + e^{-\beta \mu_0 H}= 2 \cosh(\beta \mu_0 H)
$$

$$
\langle \hat{\sigma} \rangle_{\beta,H}^{\text{can}} = \frac{e^{\beta \mu_0 H} + (-1) e^{-\beta \mu_0 H}}{Z_1(\beta, H)} = \tanh(\beta \mu_0 H)
$$

以上のように、後々の計算が楽になるようにスピン$\sigma$の期待値まで求めた。

次に、以下のように磁化と呼ばれる物理量を定義する。これは、統計力学関係なくよく用いられている物理量であり、「系がどのぐらい磁石となっているか」の目安となる。また、マクロに精密な測定が可能である。

$$
\text{磁化} : \hat{m} \coloneqq \frac{1}{N} \sum_{i=1}^{N} \mu_0 \hat{\sigma}_i
$$

$$
\langle \hat{m} \rangle_{\beta,H}^{\text{can}} = \frac{1}{N} \sum_{i=1}^{N} \mu_0 \langle \hat{\sigma}_i \rangle_{\beta,H}^{\text{can}}
= \mu_0 \tanh(\beta \mu_0 H)
$$

事前に計算を済ませたおかげで、簡潔に計算が進められる。
$N$が十分大きい時、この磁化の値が確定的になることを標準偏差を計算することによって求める。

$$
\begin{aligned}
\langle \hat{m}^2 \rangle_{\beta,H}^{\text{can}}
&= \frac{\mu_0^2}{N^2} \left\langle \left( \sum_{i=1}^{N} \hat{\sigma}_i \right)^2 \right\rangle \\
&= \frac{\mu_0^2}{N^2} \left( \sum_{i=1}^{N} \langle \hat{\sigma}_i^2 \rangle + \sum_{i \neq j} \langle \hat{\sigma}_i \hat{\sigma}_j \rangle \right) \\
&= \frac{\mu_0^2}{N^2} \left( N \cdot 1 + (N^2 - N) \{ \tanh(\beta \mu_0 H) \}^2 \right) \\
&= \mu_0^2 \left( \frac{1}{N} + \left( 1 - \frac{1}{N} \right) \{ \tanh(\beta \mu_0 H) \}^2 \right) \\
&= \mu_0^2 \left( \{ \tanh(\beta \mu_0 H) \}^2 + \frac{1 - \{ \tanh(\beta \mu_0 H) \}^2}{N} \right)
\end{aligned}
$$

$$
\begin{aligned}
\therefore \sigma_{\beta,H}^{\text{can}}[\hat{m}] &= \sqrt{ \langle \hat{m}^2 \rangle_{\beta,H}^{\text{can}} - \left[ \langle \hat{m} \rangle_{\beta,H}^{\text{can}} \right]^2 } \\

&= \mu_0 \cdot \frac{\sqrt{1 - \{ \tanh(\beta \mu_0 H) \}^2}}{\sqrt{N}} \\
&\xrightarrow[N \to \infty]{} 0
\end{aligned}
$$

磁化率とは、外部から磁場をかけた際に磁化がどれほど強くなるのかという指標になる物理量である。

$$
\begin{aligned}
\chi(\beta) &\coloneqq \left. \frac{\partial}{\partial H} \langle \hat{m} \rangle_{\beta,H}^{\text{can}} \right|_{H=0} \\

&= \mu_0^2 \beta \\

&= \frac{\mu_0^2}{kT}

\end{aligned}
$$

高温で磁化率が反比例するという振る舞いは実験的にも実際に確認されていて、**キュリーの法則**と呼ぶ。

次に、熱力学的な量についても計算を行う。いつもの流れで分配関数、ヘルムホルツエネルギーを求めて、そこからエントロピーを計算する。

$$
Z_N(\beta, H) = \{ 2 \cosh(\beta \mu_0 H) \}^N
$$

$$
F_N(\beta, H) = -\frac{N}{\beta} \log( 2 \cosh(\beta \mu_0 H) )

= -N k_B T \log\left( 2 \cosh\left( \frac{\mu_0 H}{k_B T} \right) \right)
$$

$$
\begin{aligned}
S_N(\beta, H) &= -\frac{\partial}{\partial T} F_N(\beta, H) \\

&= N k_B \log\left( 2 \cosh\left( \frac{\mu_0 H}{k_B T} \right) \right) - \frac{N \mu_0 H}{T} \tanh\left( \frac{\mu_0 H}{k_B T} \right) \\

&= f\left( \frac{H}{T} \right)
\end{aligned}
$$

最後の結果を見てほしい。エントロピー$S$は$\frac{H}{T}$の関数なので、$S$一定つまり断熱状態で$H$を小さくすると、$T$も小さくなるのだ。この手法で物質の温度を実際に下げることが出来て**断熱消磁**と呼ばれている。なんと、この方法によって$10^{-3}\text{K}$もの温度を実現出来るらしい。

### 具体例3: 二準位系と比熱

