# 邏輯

有人說，邏輯是數學的基礎，所以從這裡開始寫。

寫完邏輯之後下一個應該是ZFC的東西。

# 基礎

## 符號

$P$, $Q$, $R$等大寫字母，是代表可以放入的**敘述**，或是說**命題**(Propositions)。
但我會看成一個個占位符，把想要的東西填進去。
> [維基百科](https://zh.wikipedia.org/zh-tw/%E5%91%BD%E9%A2%98%E9%80%BB%E8%BE%91)有關於命題的介紹。

$\implies$, $\lnot$是在公理系統中會遇到的兩個基礎符號，分別叫做**蘊含**(Implies)和**非**(not)。
不過，可以先當成兩個不知道怎麼運作的符號，他們的意義可以從公理系統推出來。
> [維基百科](https://zh.wikipedia.org/zh-tw/%E4%B8%80%E9%98%B6%E9%80%BB%E8%BE%91)有一系列推導與介紹，我也是從這裡看的。

$($, $)$左右**括弧**(parentheses)，用來分組用的，讓人知道括弧內的被視為一個敘述。

$\vdash$ 就是知道所有左側的東西是對的情形下，右側的東西是對的。

## 語法

> **語句**意味著完整的句子，不是說到一半，或有空缺的句子。

1. 單一**敘述**被視為合法的語句。

    $P$

2. **非**為單參數符號，後面接著合法語句，可以形成新語句。

    $(\lnot P)$

3. **蘊含**為雙參數符號，前後接個合法語句，可以形成新語句。

    $(P \implies Q)$

4. 以上規則生成的東西，就是合法語句，且只有這些是合法語句。

> 通常括弧與有參數的符號會分開講，但我這裡想一起說。

## 語法糖

通常，為了簡便，我們會省略一些括號，省略的邏輯如下：

1. **非**所攜帶的括弧，會被省略。

    $(\lnot P)$ 會變成 $\lnot P$

2. **蘊含**內的蘊含，在蘊含符號右側的會被省略。

    $(P \implies (Q \implies R))$ 會變成 $(P \implies Q \implies R)$

3. 最外層的括弧會被省略。

    $((P \implies Q) \implies R)$ 會變成 $(P \implies Q) \implies R$

## 其他符號

$|$ 是**謝費爾豎線**(Sheffer stroke)，單一個符號就可以表達需要 $\implies$, $\lnot$兩個符號的系統，但比較少在用。
> [維基百科](https://zh.wikipedia.org/zh-tw/%E8%B0%A2%E8%B4%B9%E5%B0%94%E7%AB%96%E7%BA%BF)有更詳細的敘述。

$\bot$ 是**矛盾**(contradiction)符號，可以借助蘊含表達**非**的概念。
$\lnot P$與 $P \implies \bot$在這個系統中是等價的。

## 個人習慣

這不是正式的，但在知道討論邏輯的情形下，我會習慣直接寫 $(P Q)$取代 $(P \implies Q)$， $(P 0)$ 取代 $(\lnot P)$。
因為這樣比較省符號，也會是統一用蘊含在表達。

## 公理

> **公理**是溝通時預設雙方認同的假設，若有改變，通常會額外說明。

### 常用公理

> 從[維基百科](https://zh.wikipedia.org/zh-tw/%E4%B8%80%E9%98%B6%E9%80%BB%E8%BE%91)抄的。

- (modus ponens, MP) $P \implies Q, P \vdash Q$

    這描述了怎麼從已有的東西知道新的東西。

1. (A1) $P \implies (Q \implies P)$

    如果$P$是對的，在假設 $Q$下， $P$是對的。
    換句話說，確認一個敘述是對的後，不論加什麼假設，這個敘述還是對的。

2. (A2) $(P \implies (Q \implies R)) \implies (P \implies Q) \implies (P \implies R)$

    在假設 $P$是對的情況下，知道 $Q \implies R$和$Q$都是對的，則在假設$P$下$R$是對的。
    這可以在做推論時，先將已知的假設丟一旁，做MP運算然後再把假設加回來。

3. (A3) $(\lnot P \implies \lnot Q) \implies (Q \implies P)$

    這是針對 $\lnot$性質的描述。

或是換我習慣的寫法：

- $P Q, P \vdash Q$
1. $P Q P$
2. $(P Q R) (P Q) (P R)$
3. $((P 0) (Q 0)) (Q P)$

# 推論

先一些直覺的：

$$
    P \vdash Q P
$$

<details>
    <summary> Proof </summary>

    1. P (已知)
    2. P Q P (A1)
    3. Q P (MP, 2, 1)

</details>

$$
    P Q R \vdash (P Q)(P R)
$$

<details>
    <summary> Proof </summary>

    1. P Q R (已知)
    2. (P Q R)(P Q)(P R) (A3)
    3. (P Q)(P R) (MP, 2, 1)

</details>

$$
    P Q R, P Q \vdash P R
$$

<details>
    <summary> Proof </summary>

    1. P Q R (已知)
    2. P Q (已知)
    3. (P Q)(P R) (1)
    4. P R (MP, 3, 2)

</details>

$$
    P Q R \vdash Q P R
$$

<details>
    <summary> Proof </summary>

    1. P Q R (已知)
    2. (P Q)(P R) (1)
    3. Q (P Q)(P R) (2)
    4. (Q P Q)(Q P R) (3)
    5. Q P Q (A1)
    6. Q P R (MP, 5, 4)

</details>

$$
    \vdash P P
$$

<details>
    <summary> Proof </summary>

    1. P (P P) P (A1)
    2. (P P P)(P P) (1)
    3. P P P (A1)
    4. P P (MP, 3, 2)

</details>
