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

## 性質

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