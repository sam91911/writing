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