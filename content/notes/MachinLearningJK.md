---
title: 機械学習帳
---

情報工学系学士二年の選択必修講義。
[講義資料](https://chokkan.github.io/mlnote/index.html)

頭の中で導けるべき数式を中心にまとめていく

---

## 回帰

### 1. 単回帰

- パラメータの解析解：$a = \frac{Cov(X,Y)}{Var(X)}$, $b = \bar{y} - a\bar{x}$
- 残差の和が $0$：$\bar{e} = \frac{1}{n}\sum e_i = 0$
- 説明変数と残差の相関が $0$：$Cov(X,e) = \sum x_ie_i = \frac{\partial{L}}{\partial{a}} = 0$
- 目的変数の推定値 $\hat{y}$ と残差には相関がない：$Cov(\hat{y},e) = 0$
- 決定係数：$Var(Y) = Var(\hat{Y}) + Var(ε)$, $R^2 = \frac{Var(\hat{Y})}{Var(Y)}$

### 2. 重回帰

- 残差：$e = y - Xw$
- 目的関数：$\hat{L_D} = ||e||^2 = ||y-Xw||^2$
- 目的関数の偏微分：$\frac{\partial\hat{L_D}}{\partial{w_j}} = -2(X^Te)_j$
- パラメータの解析解：$\frac{\partial\hat{L_D}}{\partial{w}} = -2X^Te = 0 \iff w = (X^TX)^{-1}X^Ty$
  - 一次元の時 $xw = y \iff w = \frac{y}{x}$ なので $Xw = y \iff X^TXw = X^Ty \iff w = (X^TX)^{-1}X^Ty$
  - $X^T$ をかけるのは無理やり逆行列を持てるようにするため
- $f(x)$ が凸関数 $\iff (y-x)^T\nabla^2f(x)(y-x) \ge 0$

### 3. モデル選択

- $L_2$ 正則化(リッジ回帰)：$\hat{J} = \hat{L_D} + \alpha||w||^2$

### 4. 勾配法によるパラメータ推定

- 重み $w$ の更新：$w^{(t+1)} \coloneqq w^{(t)} - \eta\nabla \hat{L}_D(w)$
- 確率的勾配降下法：$L_D(w) = \sum l_{x_i,y_i}(w)$ と個別の事例の和に分解できる時 $w^{(t+1)} \coloneqq w^{(t)} - \eta\nabla l_{x_i,y_u}(w)$ とする
- **学習方式**
  - `バッチ学習`：すべての学習事例を通してパラメータを更新(最急降下法)
  - `オンライン学習`：少数の学習事例を通してパラメータを更新(SDG)

---

## 分類

### 5. 線形二値分類

- 確率推定：$P(\hat{y}=1|x) = \sigma(x^Tw)$
- 個別事例の尤度：$\hat{l}_{x,y}(w) = P(\hat{y}=y|x) = p^y(1-p)^{1-y}$
- 学習データ全体の尤度：$\hat{L_D}(w) = \prod \hat{l}_{x,y}(w)$
- 目的関数：$\hat{\mathcal{L}}_D^{MLE}(w) = -\log{\hat{L_D}(w)} = -\sum \log\hat{l}_{x,y}(w)$
- 目的関数のSDGにおける勾配：$\nabla \hat{l}_{x,y}(w) = (y-p)x$
  - つまり $w^{(t+1)} = w^{(t)} + \eta(p-y)x$
- **リッジ回帰ver**
  - 目的関数：$\hat{\mathcal{L}}_D^{MLE}(w) = -\sum \log\hat{l}_{x,y}(w) + \alpha||w||^2$
  - 勾配：$\nabla \hat{l}_{x,y}(w) = (y-p)x + \frac{2\alpha}{n}w$
  - 更新式：$w^{(t+1)} = (1-\frac{2\alpha\eta}{n})w^{(t)} + \eta(p-y)x$
- **評価**
  - 真陽性(TP)、偽陽性(FP)、偽陰性(FN)、真陰性(TN)
  - 正解率：$A = \frac{TP+TN}{All}$
  - 適合率：$P = \frac{TP}{TP+FP}$
  - 再現率：$R = \frac{TP}{TP+FN}$
  - F1スコア：$F_1 = \frac{2}{\frac{1}{TP}+\frac{1}{TN}}$ (調和平均)

### 6. 線形多クラス分類

- 予測：$\hat{y} = w^T_yx$ を最大値にする $y$
- ソフトマックス関数：$P(\hat{y}=j|x) = \frac{\exp(w_j^Tx)}{\sum \exp(w_i^Tx)}$

### 7. ニューラルネットワーク(1)

- **損失関数**
  - 二乗誤差：$l = (y-\hat{y})^2$
  - 二値クロスエントロピー：$l = -y\log{\hat{y}}-(1-y)\log{(1-\hat{y})}$
  - (一般化)クロスエントロピー：$l = -\sum y_i\log{\hat{y_i}}$

### 8. ニューラルネットワーク

- **自動微分**
  - 微分の連鎖率使って逆から微分値求めてるだけじゃね？

### 9. サポートベクトルマシン

---

## 教師なし学習

### 10. 非階層的クラスタリング

### 11. 階層的クラスタリング

- **凝集型(ボトムアップ型)**：各事例を全て異なるクラスタとして、併合していく手法
- **分割型(トップダウン型)**：全事例を一つのクラスタとして、異なるクラスタに分割してく手法
- **凝集型における距離関数**
  - 最短距離法
  - 最長距離砲
  - 群平均法
  - 重心法
  - ウォード法
    - あるクラスタ $C$ におけるクラスタ内平方和：$V(C) = \sum ||x - \mu_C||^2, \mu_C = \frac{1}{N}\sum x$
    - 二つのクラスタ内平方和を足した時の和が最小となる組を併合する

### 12. 主成分分析(1)

- $n$ 次元のデータの集まりを一本のベクトルに投影して、最も情報量が大きくなる向きはどこかみたいな話
- **第一主成分**
  - 残差の最小値 $x_i^2+y_i^2=a_i^2+e_i^2$ で、左辺は定数なので $\sum e_i^2$ が最小 $\iff \sum a_i^2$ が最大。つまり分散が最大になることを考えればok
  - 分散の最大値 $\sum a_i^2 = (Xu)^T(Xu) = u^TSu$ (ただし $||u||^2=1$ かつ $S \coloneqq X^TX$) となる $u$ を求めれば良い。
  - ラグランジュの未定乗数法 $\mathcal{L}(u, \lambda) = u^TSu - \lambda(u^Tu - 1)$ を考えて、$u$ で微分した値が $0$ になることを考えると、$Su = \lambda u$。これを解いて $\lambda$ の具体的な値を得る。後述する理由により、最も大きいものを選ぶ。
  - 固有値 (分散) $= u^TSu = u^T\lambda u = \lambda$
- **第 $k+1$ 主成分**
  - 第 $k$ 主成分までは $u_1, u_2, \dots, u_k$ として求まっているとする。この時、異なる $i, j$ に対して $u_i^Tu_j=0$ で、そうでないときは $1$
  - ラグランジュの未定乗数法 $\mathcal{L}(u_1, \dots, u_k, \lambda, u_{k+1}) = u^TSu - \lambda(u^Tu - 1) - \sum \alpha_iu_i^Tu_{k+1}$ 結局 $\alpha_1, \dots, \alpha_k$ は 0 になることが分かり、第一主成分の時と同じ固有値問題が得られる。
  - 結論：$Su_{k+1} = \lambda_{k+1}u_{k+1}$ つまり、第 $n$ 主成分の時の分散は $\lambda_n$ となる

### 13. 主成分分析(2)

- **スペクトル分解との関連性**
  - 先ほどの議論より $\begin{pmatrix} Sq_1 & \cdots & Sq_n\end{pmatrix} = \begin{pmatrix} q_1\lambda_1 & \cdots & q_n\lambda_n \end{pmatrix}$ なのでこれを $SQ = Q\Lambda$ とする
  - $q_i^tq_i=1$ より $Q^TQ = I$ である。したがって、$SQ=Q\Lambda \iff S = Q\Lambda Q^T$
- **第一主成分**
  - レイリー商 $||u||^2=1$ において $u^TSu$ の最大値を求める問題が、$||u|| \neq 0$ において $\frac{u^TSu}{u^Tu}$ の最大値を求める問題に変換できる
  - $z = uQ^T$ とすると、重み付き和の形になって第一主成分が求められる。
- **寄与率**：$\frac{\lambda_k}{\sum \lambda_i}$