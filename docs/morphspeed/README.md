# 變熊/狼攻速如何計算

<!-- <SpeedTable/> -->

![speed](./images/speed01.png)

先連到[攻速器網址](https://dev.median-xl.com/speedcalc/)  
選好了角色跟武器之後  
左邊的 attack speed 跟 右邊的 weapon attack speed  
填入`武器上`的攻速(兩邊一樣的值)  
不包含其他防具或是護符給的攻速  
變身系的攻速幾乎只看武器上的 (看下面公式解釋)

如下面這張圖  
攻速就是 4F  
4 的右邊數字剛好是 0

那左邊數字到底填入多少好  
看上面第一張圖右邊的數字  
填那幾組數字去嘗試就對了

![speed2](./images/speed02.png)

#### 講些觀念

- 裝備上面的攻速要經過效率公式轉化成 eias
- 技能給的攻速，就直接是 eias，例如 motw 給了 20%的 eias
- 變熊會多 200%ias
- 武器上面的 wias 也包含在裝備 ias

#### 計算方式

wias 是武器上面的攻速  
otherIas 除了武器以外裝備的攻速總和  
wsm 是武器的基速

詳細公式如下:

WereBear 的 FPA = 無條件進位(12 x 256/denominator) - 1  
denominator = 無條件捨去(animSpeed x (100 + speedModifier)/100)

animSpeed = 無條件捨去(256 x 7/delay);  
delay = 無條件捨去(256 x 17/e1)  
e1 = 無條件捨去(100 + wias - wsm) x 2.56

speedModifier = 取大值(eias - wsm, 75)  
eias = 無條件捨去(120 x gearIas/(120 + gearIas)) + 20(motw)  
gearIas(裝備總攻速) = otherIas + wias + 200

#### 關於變身除了武器以外，其他部位要不要裝攻速 ?

因為 speedModifier 最多就 75  
以拿基速最慢的 Giant Axe(25)為例  
考慮全程 motw 一直開著  
算一下 speedModifier 最大值 75 的話, otherIas 要多少

(120 x gearIas / (120 + gearIas)) = 80  
gearIas = 240 = otherIas + wias + 200  
也就是裝備的攻速(包含武器)超過 40%  
就達到 speedModifier 上限了(隨便都達到)  
那就是為何除了武器，其他部位不用稱攻速
