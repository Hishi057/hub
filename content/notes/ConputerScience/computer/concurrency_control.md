---
title: 並列性制御
---

## semapho(セマフォ)

利用できる数を制御する仕組みを抽象化したもの。atomicに数が増減出来るカウンタと、そのカウンタが0より減る時は待機する機能を持っている。  

具体的には、カウンタ(S)が0より大きいなら、atomicに1減らす**P操作**と、カウンタをatomicに1増やす**V操作**から構成されている。  
これを共有資源の管理に使うことで、同時にnつ以上のプロセスからアクセスできないように並列性制御に使える。  
一般的なOSにおいて、待機中のプロセスはスケジューラによって呼び出されるまでBLOCKED状態になっており、その間CPUなどは他の用途に使える。この待機方法を**ブロッキング**と呼ぶ。

### 具体例1: 実行順序の制御

```c
semaphore S = 0;

// スレッドA
data = 100;
signal(S);

// スレッドB
wait(S);
printf("%d", data);
```

### 具体例2: 生産者・消費者問題

カウンタは非負なだけで、上限は存在しないが、二つセマフォを用いることで実質的に上限を作ることが出来る。

```c
// (操作中以外)常に ne + nf = N となるようにするのがポイント
semaphore ne = {0, ∅};  // 資源数を表す
semaphore nf = {N, ∅};  // 空きの数を表す
queue buff = new_queue(N);
```

```c
// スレッドA: producer
while(True){
    data d = produce();

    wait(nf);
    enqueue(buff, d);
    signal(ne);
}

// スレッドB: consumer
while(True){
    data d;

    wait(ne);
    d = dequeue(buff);
    signal(nf);

    consume(d);
}
```

### 具体例3: Readers-Writers問題

読み込みは同時に何人出来ても良いが、書き込み中は誰もアクセスできないようにする。

以下の2つのセマフォと1つの変数を使って管理する。

```c
semaphore wrt = {1, ∅}; // writerとreaderの排他制御を行う
semaphore mtx = {1, ∅}; // readersとwrtの取得・解放を安全に行うため
int readers = 0; // 現在読み込み中の人数を管理
```

Readerは最初の一人(`readers == 0`)だけ`wait(wrt)`を行い、最後の一人が`signal(wrt)`を行う。また、Readerの数を`readers`で更新する。
ReaderもWriterもいない(`wrt.count == 1`)とき、Writerは`wait(wrt)`で書き込みが行える。

ここで、特に`wrt`の更新を行う際に`readers`なども更新するが、この一連の流れはatomicではないため、`mtx`を用いて排他的に行う。

---

## monitor(モニタ)

monitor内で定義された関数は、複数のスレッドが同時に実行することは出来ないようにすることで、並列性を制御する仕組み。  
ただし、条件変数を用いることで、セマフォにあたる`wait`や、`wait`していたスレッドを呼び出す(=`notify(c)`)ことが出来る。

**Hoare型**: `notify()`に実行権が伴う。  
**Mesa型**: `notify()`は待機者を起こすだけ。すぐに実行されるとは限らない。  

### 具体例： 生産者・消費者問題

```java
monitor PC{
    queue buff;
    condition notEmpty, notFull;

    public void put(data x){
        while(buff.isFull()) wait(notFull);
        buff.enqueue(x);
        notify(notEmpty);
    }

    public data get() {
        while(buff.isEmpty()) wait(notEmpty);
        data x = buff.dequeue();
        notify(notFull);
        return x;
    }
}

```