# 組合子

> 參考：
> - [B,C,K,W系統](https://zh.wikipedia.org/zh-tw/B,C,K,W%E7%B3%BB%E7%BB%9F)
> - [SKI组合子演算](https://zh.wikipedia.org/wiki/SKI%E7%BB%84%E5%90%88%E5%AD%90%E6%BC%94%E7%AE%97)
> - [B, C, K, W system](https://en.wikipedia.org/wiki/B,_C,_K,_W_system)
> - [SKI combinator calculus](https://en.wikipedia.org/wiki/SKI_combinator_calculus)

**組合子**(Combinator)，我認為是一套可以自我描述執行的系統。
從B, C, K, W開始說的話，每次執行動作皆是：

1. 取出最前面的元素，決定執行什麼動作。
2. 保留下一個元素。
3. 對後續的元素執行動作。
4. 放回被保留的元素。
5. 回到 1 重複

- Bxyz = x(yz)

    將兩元素打包成一個元素。

- Cxyz = xzy

    交換兩個元素。

- Kxy = x

    刪除元素。

- Wxy = xyy

    複製元素。

而SK系統把**打包**、**交換**、**複製**的功能合併到同一算子。變成：

- Sxyz = xz(yz)

    打包yz並放在複製的z後面。

這兩個系統有個共通點，都是對第一個元素x不動。

> 為何要保留第一個元素？
>
> 這樣只要把要跳過的東西打包成一個元素，就可以跳過任意數量的元素操作後面的東西。

## SK

SK 是個五循環的複合操作：

1. SKSK = K
2. KSK = S
3. SSK
4. SSKSK = SKS
5. SKSSK = SK

並且S(Kx)yz相當於Bxyz，對後續打包：

    S(Kx)yz = Kxz(yz) = x(yz) = Bxyz

而要對多數元素打包，可以嵌套多層：

    B(Bx)yzw = Bx(yz)w = x(yzw)
    B(B(Bx))yzwv = B(Bx)(yz)wv = Bx(yzw)v = x(yzwv)


>> 參考[Iota and Jot](https://en.wikipedia.org/wiki/Iota_and_Jot)
>
> Jot中的`1`亦是如此w(`1`)$^n$是對stack上的$n+1$個元素做打包

## lambda calculus

> 參考[Lambda calculus](https://en.wikipedia.org/wiki/Lambda_calculus)

**λ-演算**也是自我描述執行的系統，並且更容易閱讀，所以比SK或BCKW常用。
而規則如下：

1. (λx.N) M = N[x:=M]

    也就是，看到λ時，後面是要取代的佔位符號，例如這裡是x，在應用時，將`.`之後的敘述，也就是N，其中的佔位符號取代成(M)。

用λ-演算的寫法寫SK和BCKW的話，如下：

- B = λx.λy.λz.x(yz)
- C = λx.λy.λz.xzy
- K = λx.λy.x
- W = λx.λy.xyy
- S = λx.λy.λz.xz(yz)

而用SK代替的邏輯也簡單，如下：

1. λx.x = SKK

    SKKw = Kw(Kw) = w = (λx.x) w
2. λx.c = Kc

    Kcw = c = (λx.c) w
3. λx.cx = c

    cw = (λx.cx) w
4. λx.yz = S(λx.y)(λx.z)

    S(λx.y)(λx.z)w = ((λx.y)w)((λx.z)w)
    = y[x:=w]z[x:=w] = (λx.yz) w

而在多參數時，由內至外取代。

依此演算，可將BCKW用SK表達：
- B
    <details>
    <summary> expend </summary>

        B = λx.λy.λz.x(yz)
        = λx.λy.S(λz.x)(λz.yz)
        = λx.λy.S(Kx)y
        = λx.S(Kx)
        = S(λx.S)(λx.Kx)
        = S(KS)K

        S(KS)Kxyz
        = KSx(Kx)yz
        = S(Kx)yz
        = Kxz(yz)
        = x(yz)
    </details>

- C
    <details>
    <summary> expend </summary>
        C = λx.λy.λz.xzy
        = λx.λy.S(λz.xz)(λz.y)
        = λx.λy.Sx(Ky)
        = λx.S(λy.Sx)(λy.Ky)
        = λx.S(K(Sx))K
        = S(λx.S(K(Sx)))(λx.K)
        = S(S(λx.S)(λx.K(Sx)))(KK)
        = S(S(KS)(S(λx.K)(λx.Sx)))(KK)
        = S(S(KS)(S(KK)S))(KK)

        S(S(KS)(S(KK)S))(KK)xyz
        = S(KS)(S(KK)S)x(KKx)yz
        = KSx(S(KK)Sx)Kyz
        = S(KKx(Sx))Kyz
        = K(Sx)y(Ky)z
        = Sx(Ky)z
        = xz(Kyz)
        = xzy
    </details>

- W

    <details>
    <summary> expend </summary>
        W = λx.λy.xyy
        = λx.S(λy.xy)(λy.y)
        = λx.Sx(SKK)
        = S(λx.Sx)(λx.(SKK))
        = SS(K(SKK))

        SS(K(SKK))xy
        = Sx(K(SKK)x)y
        = xy(SKKy)
        = xy
    </details>
