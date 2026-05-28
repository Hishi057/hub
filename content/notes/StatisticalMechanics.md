---
title: 統計力学
---

統計力学とは、ミクロな物理現象を基礎にして、マクロな視点における物体の性質を記述することを試みる分野である。

機械学習において有名な拡散モデルとやらは統計力学の理論が礎になっているというのを聞いて興味を持ち始めたので勉強してみます。
田崎晴明先生著の教科書を読んでいるので、それに沿って要約を行なっています。

---

## 熱力学の復習

いつかね。

---

## 量子力学の復習

いつかね。

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