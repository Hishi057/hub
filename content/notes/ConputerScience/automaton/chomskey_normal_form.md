---
title: チョムスキー標準形
---

## 概要

**チョムスキー標準形**(CNF)とは、後述する形式によってのみ構成される文脈自由文法のことを指す。

全ての文脈自由文法はCNFに変換可能である。つまり文脈自由文法の表現能力を損なうことがない。
その上で、例えばCNFにおける構文解析木は必ず二分木になるするため、機械的な処理や解析を行う上で便利である。
実際に、[自由文脈文法のポンピング補題](/notes/conputerscience/automaton/pumping_cfl.md)の証明で使われたりする。
ゆえに文脈自由文法をとりあえず一回CNFに変換するという作業を行うことが多々ある。

## チョムスキー標準形の定義

> [!definition] チョムスキー標準形
> **チョムスキー標準形**とは、以下の規則のみから構成される文脈自由文法を指す。
> 
> 1. $A \rightarrow a \qquad$ 非終端記号から終端記号1文字
> 2. $A \rightarrow BC \qquad$ 非終端記号から非終端記号2文字
> 3. $S \rightarrow \epsilon \qquad$ 開始記号から空文字

## CFGからCNFへの変換

先ほども述べたように、任意の文脈自由文法は一定のアルゴリズムでCNFに変換することが可能である。

[このサイト](https://shinoarchive.com/contents/3381/)に詳しく手法が書かれている。

手順の要約は以下の通りである。

1. $S \rightarrow AS$など開始記号$S$から開始記号$S$を生成する変換ルールがあるならば、新たな開始記号$S_0$を追加して$S_0 \rightarrow S$ を追加する。
2. $A \rightarrow \epsilon$ のような空文字への変換を消去する。 $S \rightarrow AAB$となっていれば$S \rightarrow B | AB | AAB$ とすることを忘れない
3. 単一変換規則を同じ要領で消去する。 $A \rightarrow A$や$A \rightarrow B$ など
4. $A \rightarrow a$ 以外の非終端記号への変換を消去する。具体的に$A \rightarrow aa$とあれば$A \rightarrow X_a, ~ X_a \rightarrow a$ のようにする
5. $A \rightarrow BCD$など 3つ以上の非終端記号への変換を分割することで消去する。具体的に$A \rightarrow BX, X \rightarrow CD$ とすれば良い

### 具体例

> $$
> \begin{cases} S \rightarrow ASA \mid A \\ A \rightarrow 000 \mid \varepsilon \end{cases}
> $$
> をCNFへ変換せよ

⓪  $S \rightarrow S_0$ の追加

$$
\begin{cases} S_0 \rightarrow S \\ S \rightarrow ASA \mid A \\ A \rightarrow 000 \mid \varepsilon \end{cases}
$$

① $A \rightarrow \varepsilon$ の消去

$$
\begin{cases} S_0 \rightarrow \varepsilon \mid S \\ S \rightarrow A \mid S \mid AS \mid SA \mid ASA \\ A \rightarrow 000 \end{cases}
$$

② $S \rightarrow A, S \rightarrow S$ の消去

$$
\begin{cases} S_0 \rightarrow \varepsilon \mid 000 \mid AS \mid SA \mid ASA \\ S \rightarrow 000 \mid AS \mid SA \mid ASA \\ A \rightarrow 000 \end{cases}
$$

③ 単一生成規則の消去

$$
\begin{cases} S_0 \rightarrow \varepsilon \mid X_0 X_0 X_0 \mid AS \mid SA \mid ASA \\ S \rightarrow X_0 X_0 X_0 \mid AS \mid SA \mid ASA \\ A \rightarrow X_0 X_0 X_0 \\ X_0 \rightarrow 0 \end{cases}
$$

④ 非終端記号の整理

$$
\begin{cases} S_0 \rightarrow \varepsilon \mid X_0 Y_{X_0 X_0} \mid AS \mid SA \mid A Y_{SA} \\ S \rightarrow X_0 Y_{X_0 X_0} \mid AS \mid SA \mid A Y_{SA} \\ A \rightarrow X_0 Y_{X_0 X_0} \\ Y_{X_0 X_0} \rightarrow X_0 X_0 \\ Y_{SA} \rightarrow SA \\ X_0 \rightarrow 0 \end{cases}
$$