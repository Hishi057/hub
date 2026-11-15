---
title: 分岐予測
---

例えば基本的な5段パイプライン(`IF`,`ID`,`EX`,`MEM`,`WB`)について考える。
条件分岐の判定は`EX`で行うため、真に行うべき`IF`,`ID`の処理を知るにはそれを待つ必要がある。しかしながら、もし真に行うべき処理を予測することが出来たら、実質的に条件分岐の判定を待つ必要がなくなるので、性能向上が見込める。よって、これを目的としていくつか条件分岐を予測する手段について考案されている。

## bimodal

bimodal分岐予測とは、`PC`(命令アドレス)の一部をindexとして取り出し、同じindexを実行した際の分岐結果(`PHT`)を元に、未来の分岐を予測する手法である。

過去の結果は`PHT`カウンタの各indexに記録する。つまり、indexごとに実際に分岐すれば$+1$,分岐しなければ$-1$する。ただし、通常2ビット飽和カウンタなので範囲は$0$~$3$である。

`PHT`カウンタが$0$or$1$のときに分岐不成立、$2$or$3$のときに分岐成立と予測する。

また通常、`BHT`の(`PHT`でも用いた)各indexに、前回の分岐先を記録する。

```c
// 予測
void bp_predict(unsigned int pc, int *pred, unsigned int *p_target){
    // 分岐先を引っ張っておく
    int btb_idx = (pc>>2) % BTB_SIZE;
    *p_target = btb[btb_idx];

    // PHTを元に、分岐の予測を行う
    int pht_idx = (pc>>2) % PHT_SIZE;
    *pred = (btb[btb_idx]!=0 && (pht[pht_idx] >> 1));
}

// 分岐判定完了後の処理
void bp_regist(unsigned int pc, int taken, unsigned int target){
    // 分岐先を記録しておく
    int btb_idx = (pc>>2) % BTB_SIZE;
    btb[btb_idx] = target;

    // 実際の分岐結果を元に、PHTを更新
    int pht_idx = (pc>>2) % PHT_SIZE;
    pht[pht_idx] = (taken) ? pht[pht_idx] + (pht[pht_idx]<3) :
                             pht[pht_idx] - (pht[pht_idx]>0);
}
```

## gshare

基本的な考え方はbimodal方式と同じだが、`PHT`のindexとして、`PC`(命令アドレス)の一部だけでなく、過去n回分の分岐結果を記録した`GHR`との排他的論理和を用いる。

```c
void bp_predict(unsigned int pc, int *pred, unsigned int *p_target){
    // 分岐先を引っ張っておく
    int btb_idx = (pc>>2) % BTB_SIZE;
    *p_target = btb[btb_idx];

    // PHTとGHRを元に、分岐の予測を行う
    int pht_idx = (pc>>2) % PHT_SIZE ^ ghr;
    *pred = (btb[btb_idx]!=0 && (pht[pht_idx] >> 1));
}

void bp_regist(unsigned int pc, int taken, unsigned int target){
    // 分岐先を記録しておく
    int btb_idx = (pc >> 2) % BTB_SIZE;
    btb[btb_idx] = target;

    // 実際の分岐結果を元に、PHTを更新
    int pht_idx = (pc>>2) % PHT_SIZE ^ ghr;
    pht[pht_idx] = (taken) ? pht[pht_idx] + (pht[pht_idx]<3) :
                             pht[pht_idx] - (pht[pht_idx]>0);

    // GHRの更新
    ghr = ((ghr << 1) | taken) & (GHR_SIZE - 1);
}
```