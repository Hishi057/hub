---
title: 4. 積分順序の変更
---

## フビニの定理,トネリの定理

> [!theorem] Tonelliの定理(省略)
> $\mathbb{R}^{k+l}$ 上の関数 $f(x,y)$ が非負関数であれば次が成り立つ。
> $$
> \int\int_{\mathbb{R}^{k+l}}f(x,y)dxdy = 
> \int_\mathbb{R^k}(\int_{\mathbb{R}^l}f(x,y)dy)dx
> \int_\mathbb{R^l}(\int_{\mathbb{R}^k}f(x,y)dx)dy
> $$
> この等式は、$\infty = \infty$でも成り立つ。

> [!theorem] Fubiniの定理(省略)
> $\mathbb{R}^{k+l}$ 上の関数 $f(x,y)$ が可積分関数であれば次が成り立つ。
> $$
> \int\int_{\mathbb{R}^{k+l}}f(x,y)dxdy = 
> \int_\mathbb{R^k}(\int_{\mathbb{R}^l}f(x,y)dy)dx
> \int_\mathbb{R^l}(\int_{\mathbb{R}^k}f(x,y)dx)dy
> $$
> この等式は、すべて有限である。

Tonelliの定理とFubiniの定理について、次の事実も成り立つ。

- (a) $\quad$ a.e. $x \in \mathbb{R}^k$ に対し, $f_x(y) := f(x,y)$ は $y \in \mathbb{R}^l$ に対し, 可測かつ可積分.
- (b) $\quad$ a.e. $y \in \mathbb{R}^l$ に対し, $f^y(x) := f(x,y)$ は $x \in \mathbb{R}^k$ に対し, 可測かつ可積分.
- (c) $\quad$ a.e. $x \in \mathbb{R}^k$ で $g(x) := \int_{\mathbb{R}^l} f(x,y)dy$ は定義でき, $g(x)$ は $x \in \mathbb{R}^k$ 上で可測かつ可積分.
- (d) $\quad$ a.e. $y \in \mathbb{R}^l$ で $h(y) := \int_{\mathbb{R}^k} f(x,y)dx$ は定義でき, $h(y)$ は $y \in \mathbb{R}^l$ 上で可測かつ可積分.

ゴツそうな定理だが言っていることは単純で、要するに、次のことを主張する定理である。

多変数関数の積分に対して、$\\$
**Tonelliの定理**: 非負関数だったら、$\infty$を取りうる関数でも積分の順序変更可能 $\\$
**Fubiniの定理**: 非負関数でなくとも、絶対値をとって$\infty$にならなければ積分の順序変更可能

以上の定理がなぜ成り立つのか、というより、なぜ成り立たない、つまり積分の順序が変更できない場合があるかを考える。
結論からいうと、$\infty - \infty$を計算してしまうと、計算式の整合性が成り立たなくなるからである。

