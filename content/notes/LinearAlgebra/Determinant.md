---
title: 行列式
---

## 前提知識

- [[notes/LinearAlgebra/Basics|基本]]

## 概要

応用的な観点で、行列式についてまとめる。
行列式とは、正方行列について定義される値で、線形変換に伴う単位面積・体積あたりの拡大率と考えたりすることが出来る。

$$
\det{A} = 
\begin{vmatrix}
   1 & -2 \\
   1 & 2
\end{vmatrix}

= 4
$$

これは、原点と点$(1,1)$を頂点に持つ正方形が、ベクトル$(1,1)^T$と$(-2,2)^T$が張る
正方形に変換されると考えて、値は$4$となる。

### 定義

> [!definition] 定義：行列式
> $$
> \det{A} = \sum\limits_{\sigma \in S_n}{sgn(\sigma) a_{1\sigma(1)}a_{2\sigma(2)} \cdots a_{n\sigma(n)}}
> $$
> ただし、$S_n$とはn次置換群、$sgn(\sigma)$とは、偶置換であれば$1$, 奇置換であれば$-1$

置換についての説明は省略する。
この表式そのものを用いることは実はあまりなく、行列式の値を求めたいなら後述する定理などを使うのが楽である。  
まず性質について説明して、その後なぜそのような定義を採用するのかという説明を行う。

### 基本的な性質

出来るだけ直感的な記述、理由説明をするようにする。厳密な証明などは他で調べてほしい。  
また、以下で説明する性質は基本的に、列に対しても行に対しても成立する。  
これは、以下で説明するように行列式の値は、元の行列の転置をとっても不変であるためである。

> [!theorem] 転置
> $$
> \det{A} = \det{A^T}
> $$

(どんな説明が上手いんだろう。AIに聞いたら、多次元空間の対称性より、という回答が得られたけど)

> [!theorem] 定数倍
> $$
> \begin{vmatrix}
> \mathbf{x_1} & \cdots & \alpha \mathbf{x_i} & \cdots
> \end{vmatrix}
> =
> \alpha 
> \begin{vmatrix}
> \mathbf{x_1} & \cdots & \mathbf{x_i} & \cdots
> \end{vmatrix}
> $$

座標系の軸を定数倍すると考えれば良い。

> [!theorem] 多重線形性
> $$
> \begin{vmatrix}
> \mathbf{x_1} & \mathbf{x_2} + \mathbf{y_2} & \cdots & \mathbf{x_n}
> \end{vmatrix}
> =
> \begin{vmatrix}
> \mathbf{x_1} & \mathbf{x_2} & \cdots & \mathbf{x_n}
> \end{vmatrix}
> +
> \begin{vmatrix}
> \mathbf{x_1} & \mathbf{y_2} & \cdots & \mathbf{x_n}
> \end{vmatrix}
> $$

長方形、立方体の概念を一般化して、各軸に平行なn次元の図形を考える。  
ある一つの辺の長さを$a, b$として、その図形の体積を$f(x)$とする。
この時、$f(a+b) = f(a) + f(b)$が成り立つのは直感的には自然ではないだろうか。  
どこかの面に平行にスパッと図形を切れると考えても良い。

> [!theorem] 交代性
> $$
> \begin{vmatrix}
> \cdots & \mathbf{x_i} & \cdots & \mathbf{x_k} & \cdots
> \end{vmatrix}
> =
> (-1)
> \begin{vmatrix}
> \cdots & \mathbf{x_k} & \cdots & \mathbf{x_i} & \cdots
> \end{vmatrix}
> $$
> ここで、$\mathbf{x_i} = \mathbf{x_k}$ ならば $\det{A} = -\det{A}$ より $\det{A}=0$

座標系の軸を入れ替えると考えれば良い。

> [!theorem] 多重線形性と交代性から演繹される性質
> $$
> \begin{vmatrix}
> \cdots & \mathbf{x_i} & \cdots & \mathbf{x_k} & \cdots
> \end{vmatrix}
> =
> \begin{vmatrix}
> \cdots & \mathbf{x_i} + \alpha \mathbf{x_k}  & \cdots & \mathbf{x_k} & \cdots
> \end{vmatrix}
> $$

多重線形性と交代性により演繹される。幾何学的には、図形を剪断しても、
ある面で切った時の面積は不変のため体積も不変であるという風に解釈される。

### 定義に至る経緯

$$
A
=
\begin{pmatrix}
\mathbf{a_1} & \mathbf{a_2} & \cdots & \mathbf{a_n}
\end{pmatrix}
$$

として、デカルト座標系における正規直交基底
$ \mathbf{e_i} = \begin{pmatrix} 0 & \cdots & 1 & \cdots & 0\end{pmatrix}$
に各列を分解する。  
すると、1列目に関して多重線形性で和に分解して、定数倍になっていることを着目して積の形にして

$$
\sum\limits_{i_1 = 1}^n{
    a_{i_11}
    \begin{vmatrix}
        \mathbf{e_{i_1}} & \sum\limits_{i_2 = 1}^n{a_{i_22}\mathbf{e_{i_2}}} & \cdots & \sum\limits_{i_n = 1}^n{a_{i_nn}\mathbf{e_{i_n}}}
    \end{vmatrix}
}
$$

これを各列について繰り返して

$$
\sum\limits_{i_1 = 1}^n{
\sum\limits_{i_2 = 1}^n{
    \cdots
\sum\limits_{i_n = 1}^n{
    a_{i_11}
    a_{i_22}
    \cdots
    a_{i_nn}
    \begin{vmatrix}
        \mathbf{e_{i_1}} & \mathbf{e_{i_2}} & \cdots & \mathbf{e_{i_n}}
    \end{vmatrix}
}
}
}
$$

ここで、
$
    \begin{vmatrix}
        \mathbf{e_{i_1}} & \mathbf{e_{i_2}} & \cdots & \mathbf{e_{i_n}}
    \end{vmatrix}
$
について考える。この行列の行列式は、まず交代性より$i_n = i_m$となる組み合わせがあると、$0$になる。
よって、そうでないとき、列について並び替えると行列式は単位行列に$1$あるいは$-1$をかけた値になると分かる。
この正負は、何回列を入れ替えたかという回数に依存しているのだが、これを表す関数こそが$sgn(\sigma)$なのである。  
**転倒数**という概念があるが、これは今のことを数学的に厳密に表現するための道具と思えば良い。直感的な説明を優先するこの場では省略する。

### 余因子行列

### クラメルの公式
