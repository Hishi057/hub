---
title: 1. 外測度・測度
---

## ルベーグ外測度

> [!definition] 定義：ルベーグ外測度
> $$
> \mu^*(A) \coloneqq \inf \sum\limits_{n=1}^\infty {|I_n|}
> $$
> ただし、区間 $I_n = [a_n,b_n)$ の集合は集合 $A$ を被覆する。

**解釈**：多少はみ出ても、とりあえず大きさなるものを定義したいらしい。これを元に、**ルベーグ測度**というちゃんとしたやつを定義していく。

### 重要な性質

1. **加算劣加法性** $~$ $\mu^*(A \cup B) \leq \mu^*(A) + \mu^*(B)$ $\quad$ 3つ以上の集合についても同様
2. 単調性 $~$ $A \subset B \implies \mu^*(A) \leq \mu^*(B)$
3. 劣平移不変性: $~$ $\mu^*(A+x) = \mu^*(A) \quad x\in \mathbb{R}$
4. $\mu^*([a,b]) = \mu^*([a,b)) = \mu^*((a,b]) = \mu^*([a,b]) = |b-a|$

**注意**：$A \cap B = \emptyset$ ならば、常に等式が成り立つわけではない。
しかしながら、そんな集合は変なので、これが成り立つ集合だけを考えましょうという動機で生まれたのが後述する**ルベーグ測度**である。\
つまり、1番の性質を=に置き換えたいと言い換えても良い。

---

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
> 後述する可測集合族$\mathcal{M}$は$\sigma$-加法族である！

後述する可測集合は、無限回の操作を許しても可測集合のままでいてくれる偉い性質を持った集合なのである。
この偉い性質というのを抽象化してルベーグ積分論以外にも適用できるようにしたものが、上記の定義である。

---

## ルベーグ測度


> [!definition] 定義：ルベーグ測度
> 集合 $A \in 2^\mathbb{R}$ が **可測** であるとは、任意の集合 $B \in 2^\mathbb{R}$ について以下が成り立つこと：
> $$
> \mu^*(B) = \mu^*{(B \cap A)} + \mu^*{(B \cap A^c)}
> $$
> 可測集合を全て集めた集合をしばしば $\mathcal{M}$ と表記する。また、可測集合$A$に対して、$\mu(A) = \mu^*(A)$ とする。

- 数学科以外の人が見る集合はほぼ全て可測であると言って良い。例えば $\{48, 1, 7\}, \{0.1\}, \{\pi\}, [1, 100), \mathbb{Q}$ が挙げられる。
- この定義から直接導ける性質は、**有限個の集合でのみ成り立つ**ことに注意。といっても、同様の性質は無限個の集合についても結果的に成り立つのだが、この有限から無限へのジャンプこそが、ルベーグ積分論への要でもある。
- 上記の定義に沿って証明する際に、外測度の加算劣加法性より $\mu^*(B) \leq \mu^*{(B \cap A)} + \mu^*{(B \cap A^c)}$ が自動的に成り立つので、$\mu^*(B) \geq \mu^*{(B \cap A)} + \mu^*{(B \cap A^c)}$ を示して可測であることを示すパターンが多い

### 有限個の集合における性質

1. **有限加法性**: $A_1, A_2, \cdots A_n \in \mathcal{M}$ で、これらの集合が互いに素ならば $~$ $\mu(A_1 \cup A_2 \cdots \cup A_n) = \mu(A_1) + \mu(A_2) \cdots + \mu(A_n)$
2. $A,B \in \mathcal{M}~$ ならば$~A^c, A \cap B,A \cup B, A\setminus B ~\in \mathcal{M}$

### 無限個の集合における性質

> [!theorem] 可算無限和と可算共通部分
> 無限個の可測な集合の和と積も可測

無限個の可測な集合群$\{A_n\}$を考える。この無限和を$A$とし続けながら
集合群を互いに素となるように切り分ける。

$$

\begin{align*}
\mu^*(B) &= \sum\limits_{n=1}^{\infty}{ \mu^*(B\cap A_n) } + \mu^*(B \cap A^c) \\
&\geq \mu^*(B \cap \bigcup A_n) + \mu^*(B \cap A^c) \\
&= \mu^*(B \cap A) + \mu^*(B \cap A^c)
\end{align*}

$$

$\leq$については可算劣加法性より常に成り立つため、$A$が可測であることは示された。
否定をとってドモルガンの法則を使えば、無限積についても可測であることが示される。

> [!theorem] 完全加法性
> 互いに素な可測集合 $A_1, A_2...$ について、次が成り立つ。
> $$
> \mu\left(\bigcup\limits_{k=1}^{\infty} A_k\right) = \sum\limits_{k=1}^{\infty}{ \mu(A_k) }
> $$

有限加法性より、次が成り立つ。

$$
\mu^*(A) \geq \mu(\bigcup\limits_{k=1}^{n} A_k) = \sum\limits_{k=1}^{n}\mu(A_k) 
$$

$\leq$については自動的に成り立つので、$n$を無限に飛ばして挟むことで証明完了

> [!theorem] 測度の連続性
> 可測集合からなる $A_1,A_2...$ に対して、次が成り立つ。
>
> $$
> A_{n} \subset A_{n+1} \implies \mu(\bigcup\limits_{n=1}^{\infty} A_n) = \lim_{n \to \infty} \mu(A_n) \\
>
> A_{n+1} \subset A_{n} \land \mu(A_n) < \infty \implies \mu(\bigcap\limits_{n=1}^{\infty} A_n) = \lim_{n \to \infty} \mu(A_n)
> $$

集合の極限を$\lim$という数学で扱いやすい対象として捉えれることを示している。