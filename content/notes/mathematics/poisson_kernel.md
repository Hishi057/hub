---
title: ポアソン核
---

## 概要

ポアソン核とは、以下のような関数を指す。

> [!definition] ポアソン核
> $$
> P(r,\theta):=\frac1{2\pi}\cdot
> \frac{1-r^2}{1+r^2-2r\cos\theta}
> $$

## 基本的な性質

### 正値性

> [!theorem] theorem
> $P(r,\theta)>0\quad(0\le r<1,\ 0\le\theta<2\pi)$

### 正規化条件

> [!theorem] 正規化条件
> $\displaystyle \int_0^{2\pi}P(r,\theta)\,d\theta=1\quad(0\le r<1)$

### 原点への集中性

> [!theorem] 原点への集中性
> $0<\delta\le\pi$ に対して
> $$
> \lim_{r\to1-}\sup_{\delta\le |\theta|\le\pi}P(r,\theta)=0.
> $$