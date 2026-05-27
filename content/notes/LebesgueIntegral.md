---
title: ルベーグ積分論
---

## 概要

**ルベーグ積分論**とは、なんか「大きさ」(=測度)というものをもっとちゃんと考えることで、大きさを考えられる対象を広げよう的なノリの分野である。

いつもならお気持ちをメモしていますが、そもそも分野の性質が「お気持ちとかじゃなくてもっと厳密にやろうぜ」みたいなノリなので難しい。でも、定義の動機みたいなところに着目しながらストーリーを立ててメモしていく。

---

## ルベーグ外測度

> [!definition] 定義：ルベーグ外測度
> $$
> \mu^*(A) \coloneqq \inf \sum\limits_{n=1}^\infty {|I_n|}
> $$
> ただし、区間 $I_n = [a_n,b_n)$ の集合は集合 $A$ を被覆する。

**解釈**：多少はみ出ても、とりあえず大きさなるものを定義したいらしい。これを元に、**ルベーグ測度**というちゃんとしたやつを定義していく。

### 重要な性質

> [!theorem] 単調性
> $$
> A \subset B \implies \mu^*(A) \leq \mu^*(B)
> $$

> [!theorem] 加算劣加法性
> $$
> \mu^*(A \cup B) \leq \mu^*(A) + \mu^*(B)
> $$
> （3つ以上の集合についても同様のことが成り立つ）

**注意**：$A \cap B = \emptyset$ ならば、常に等式が成り立つわけではない。しかしながら、そんな集合は変なので、これが成り立つやつだけを考えましょうという動機で生まれたのが後述する**ルベーグ測度**である。

---

## ルベーグ測度

> [!definition] 定義：ルベーグ測度
> 集合 $A \in 2^\mathbb{R}$ が **可測** であるとは、任意の集合 $B \in 2^\mathbb{R}$ について以下が成り立つこと：
> $$
> \mu^*(B) = \mu^*{(B \cap A)} + \mu^*{(B \cap A^c)}
> $$
> 可測集合を全て集めた集合をしばしば $\mathcal{M}$ と表記する。また、可測集合$A$に対して、$\mu(A) = \mu^*(A)$ とする。

**備考**：数学科以外の人が見る集合はほぼ全て可測であると言って良い。例えば $\{48, 1, 7\}, \{0.1\}, \{\pi\}, [1, 100), \mathbb{Q}$ が挙げられる。

### 重要な性質

> [!theorem] 基本的な操作
> $\mathcal{M}$に属する集合$A, B$について、それぞれの(1)補集合、(2)和、(3)積、(4)差についても$\mathcal{M}$に属する

つまり基本的な計算について、$\mathcal{M}$のなかで閉じているということ。(2)の証明がちょっと大変だが、(1),(3),(4)はほぼ明らか。

> [!theorem] 有限加法性
> 互いに素な $ A_1, A_2, ... A_n \in \mathcal{M} $ について、以下が成り立つ。
> $$
> \mu^*\left(B \cap \bigcup\limits_{k=1}^{n} A_k\right) = \sum\limits_{k=1}^{n}{ \mu^*(B \cap A_k) }
> $$
>
> 特に $B = \mathbb{R} $ のとき
> $$
> \mu^*\left(\bigcup\limits_{k=1}^{n} A_k\right) = \sum\limits_{k=1}^{n}{ \mu^*(A_k) }
> $$

> [!theorem] 加算無限和と加算共通部分
> 無限個の可測な集合の和と積も可測

**自明ではない**！

証明のアイデアは次の通りである。

無限個の可測な集合群$\{A_n\}$を考える。この無限和を$A$とし続けながら
集合群を互いに素となるように切り分ける。

$$

\begin{align*}
\mu^*(B) &= \sum{ \mu^*(B\cap A_n) } + \mu^*(B \cap A^c) \\
&\geq \mu^*(B \cap \bigcup A_n) + \mu^*(B \cap A^c) \\
&= \mu^*(B \cap A) + \mu^*(B \cap A^c)
\end{align*}

$$

$\leq$については加算劣加法性より常に成り立つため、$A$が可測であることは示された。
否定をとってドモルガンの法則を使えば、無限積についても可測であることが示される。

> [!theorem] 加算加法性
> 互いに素な可測集合 $A_1, A_2...$ について、次が成り立つ。
> $$
> \mu^*\left(\bigcup\limits_{k=1}^{\infty} A_k\right) = \sum\limits_{k=1}^{\infty}{ \mu^*(A_k) }
> $$

$n$が有限の場合は先ほど証明したが、無限でも成り立つ。

$$\mu^*(A) \geq \mu^*(\bigcup\limits_{k=1}^{n} A_k) = \sum\limits_{k=1}^{n}\mu^*(A_k) $$

とすれば、$\leq$については自動的に成り立つので、$n$を無限に飛ばして挟むことで証明完了

> [!theorem] 測度の連続性
> 可測集合からなる $A_1,A_2...$ に対して、次が成り立つ。
>
> $$
> A_{n} \subset A_{n+1} \implies \mu^*(\bigcup\limits_{n=1}^{\infty} A_n) = \lim_{n \to \infty} \mu^*(A_n) \\
>
> A_{n+1} \subset A_{n} \land \mu^*(A_n) < \infty \implies \mu^*(\bigcap\limits_{n=1}^{\infty} A_n) = \lim_{n \to \infty} \mu^*(A_n)
> $$

### テクニック

- ルベーグ積分論の文脈において、集合$A$は常に $\mu^*(B) \leq \mu^*{(B \cap A)} + \mu^*{(B \cap A^c)}$ が成り立っているので、$\mu^*(B) \geq \mu^*{(B \cap A)} + \mu^*{(B \cap A^c)}$ を示して可測であることを示すパターンが多い

## 有限加法族, σ-加法族

> [!definition] 定義：有限加法族, σ-加法族
>
> 1. $\mathbb{ \emptyset ,R} \in \mathcal{A}$
> 2. $A \in \mathcal{A} \implies A^c \in \mathcal{A}$
> 3. $A_1, A_2 \in \mathcal{A} \implies A_1 \cup A_2 \in \mathcal{A}$
> 4. $A_1, A_2 \cdots \in \mathcal{A} \implies \bigcup\limits_{i \geq 1} A_i \in \mathcal{A}$
>
> 条件1,2,3を満たすとき、集合族$\mathcal{A}$を有限加法族であるという。  
> 条件1,2,4を満たす時、集合族$\mathcal{A}$を$\sigma$-加法族であるという。
> 
> $\mathcal{M}$は$\sigma$-加法族である！

扱う対象が、既存の知っているルールで分析できるものであることを保証するためのもの。という風に解釈した。
特に、「∞」が含まれていても、既存の代数のルールが適用が変わらず適用できることを保証できることが嬉しい。
のだと思う。

## ほとんど至るところで

> [!definition] ほとんど至るところで
> ある集合$X$上で命題$P$について考える。その命題$P$が、$X \setminus Y$を除いて成り立ち、かつ $\mu(Y)=0$のとき、
> 例えば
> $P$ a.e. $x \in X$
> と表現する。

a.e. (=almost everywhere) ということであり、立派な数学用語である。

多少の例外は見逃すというものを数学的に厳密に表現したのが、この定義なのである。

---

ひと段落！
ここからは、**可測関数**なるものを定義して、実際のルベーグ積分について考えていく。

## 可測関数

> [!definition] 定義：可測関数
> 関数 $f:X → \bar{\mathbb{R}}$ が可測であるとは
> 次の性質を満たすものである。
> $$
> X \in \mathcal{M} \\
> \forall a\in \mathbb{R} \quad \{f(x)>a\} \in \mathcal{M}
> $$
> 特にこれを満たす関数$f$を**可測関数**と呼ぶ。

要するに、リーマン積分は縦状の短冊で区切って積み上げていたが、ルベーグ積分は横状の短冊で区切って積み上げたい。横状の短冊で区切るためには、"横の長さ"を"納得がいくような定義"をして測れるようにする必要がある。この"納得がいくような定義"こそが、ルベーグ測度である。

つまりこの定義は、**横の長さが人間の納得いくように測れる関数だけをこれから扱いますよという宣言**と思えば良い。

### 重要な性質

> [!theorem] 可測関数の四則演算
> 可測関数同士の四則演算の結果も可測関数
> $$
> (f+g)(x) \in \mathcal{M} \\
> (f-g)(x) \in \mathcal{M} \\
> (f \cdot g)(x) \in \mathcal{M} \\
> \frac{f}{g}(x) \in \mathcal{M}
> $$

## ルベーグ積分

次の手順で、ルベーグ積分を定義する。

1. 有限個の値を取りうる関数、単関数の面積を定義する。
2. 非負関数の積分を、そのような単関数の面積(の上限)として定義する。
3. 上の定義を、負の値を取りうる関数にも拡張する。

### 特性関数, 単関数

> [!definition] 定義：特性関数, 単関数
> 次のような関数を、**特性関数**と呼ぶ。
> $$
> \chi_A(x) :=
> \begin{cases}
> 1 & (x \in A) \\
> 0 & (x \in A^c)
> \end{cases}
> $$
>
> そして、関数$s:\mathbb{R} → \mathbb{R}$が有限の値を取りうるとき、**単関数**と呼ぶ。具体的には、次を満たすことをいう。
> $$
> A_1, A_2 \cdots A_n \in \mathcal{M} \\
> \mathbb{R} = A_1 \sqcup \cdots \sqcup A_n \\
> s = \sum\limits_{i=1}^{n}a_i \chi_{A_i}
> $$
> ただし数列$\{a_i\}$は重複を許す。

また、この単関数の積分を次のように定義する。

> [!definition] 定義：単関数の積分
> $$
> \int s d\mu \coloneqq \sum\limits_{i=1}^{n}a_i \mu{(A_i)}
> $$

この積分は、単純な長方形の和であるから、リーマン積分かルベーグ積分かそうでない積分なのか、問題にならない。

### 可測関数の積分の定義

> [!definition] 定義：非負可測関数の積分
> $f$を非負可測関数とする。
> $$
> \int f d\mu \coloneqq 
> \sup\limits_{0\leq s \leq f}
> \int s d\mu
> $$

この定義を、一般の可測関数にも拡張する。

> [!definition] 定義：可測関数の積分(ルベーグ積分)
> $f$を可測関数とする。
>
> $f^+ \coloneqq \max{ \{f, 0\} }, \quad f^- \coloneqq \max{ \{-f, 0\} }$
>
> とすると
> $$
> \int f d\mu \coloneqq 
> \int f^+ d\mu
> - \int f^- d\mu
> $$

これを、**ルベーグ積分**と呼ぶ。

> [!definition] 積分確定、可積分
> $f$を可測関数とする。
>
> $\int f^+ d\mu < \infty$ または $\int f^- d\mu < \infty$ ならば、$f$の積分結果は不定形とならないので**積分確定**と呼ぶ。
>
> $\int f^+ d\mu < \infty$ かつ $\int f^- d\mu < \infty$ $\iff \int |f|d\mu < \infty $ ならば、$f$の積分結果は必ず有限となるので、**(ルベーグ)可積分**と呼ぶ。

## 収束定理：極限と積分の交換

以下の順番で、極限と積分が交換できる範囲を拡張していく。

1. 単関数の単調収束定理： 単関数
2. 単調収束定理: 単調増加する非負可測関数列$f_n$
3. Fatouの補題： 非負可測関数の列
4. ルベーグの優収束定理： 一般の可測関数の列

### 単関数の単調収束定理

### 単調収束定理

### Fatouの補題

### ルベーグの優収束定理

> [!theorem] ルベーグの優収束定理
> 可測関数列$f_n:\mathbb{R}→\bar{\mathbb{R}}$と可測関数$f,~$非負可積分関数$\Phi$は次を満たす。
> $$
> \begin{align}
> \quad f = \lim\limits_{n→\infty}f_n ~ \text{a.e.} \\
> \forall n \in \textbf{N}, ~ |f_n| \leq \Phi ~ \text{a.e.}
> \end{align}
> $$
> このとき、$f_n,~f$は可積分であり、次が成り立つ。
> $$
> \lim\limits_{n→\infty}\int f_nd\mu = \int fd\mu
> $$

いわゆるこれが、"極限と積分が交換できる"というもので、条件$(1),~(2)$はかなり緩い。普通に出会う関数はほとんどこれを満たすので、物理学科の人が何も条件を確認せず極限と積分を交換する様子を見て数学科の人がよく怒ったりしている。

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