---
title: 2. 相互情報量
---

> [!definition] 相互情報量
> $$
> \begin{aligned}
> I(X;Y) &\coloneqq - \sum_y\sum_x P(x,y)\log_2{\frac{P(x,y)}{P(x)P(y)}} \\
> &= H(X) - H(X|Y) = H(Y) - H(Y|X) \\
> &= H(X) + H(Y) - H(X,Y)
> \end{aligned}
> $$ 

2つの相互依存の尺度を表すと表現される。  
例えば、$I(X;Y)$が大きい時、$X$を知れば$Y$もほとんど分かるということを意味する。
実際に、$I(X;Y) = H(Y) - H(Y|X)$であるとき、$X$が知った時$Y$の驚きが減ると言われているのだから
$H(Y|X)$は小さくなることが予想される。よって、$I(X;Y)$は大きくなる。

> [!theorem] KLダイバージェンス
> $$
> D(p||q) \coloneqq \sum p(x) \log \frac{p(x)}{q(x)}
> $$

2つの確率分布$p(x)$,$q(x)$の距離を表すと説明されるが、
$D(p||q) = D(q||p)$とは限らないため、数学的な意味での距離ではない。

また、相互情報量はKLダイバージェンスの一種である。

$$
I(X;Y) = D(P(X,Y)||P(X)P(Y))
$$