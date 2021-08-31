# 物品過濾器

在這個[github](https://github.com/Kyromyr/D2Stats/releases)下載新版的  
D2Stats-3.xx.x.rar 這個檔

按 home+shift 就可以切換是否，過濾物品模式  
按 home 切換是不是要，一值顯示物品  
按 x 可以切換，沒按 alt 顯示物品的狀態下  
遊戲內滑鼠左鍵是否，會點擊並拾取物品

解壓縮並執行程式之後  
會有一個叫 notifier 的分頁  
那個分頁就是寫一些  
物品掉落提示跟顯示/隱藏地上物品的代碼

hotkey 那個分頁是設定熱鍵  
預設按 shift+home 就是載入 notifier(物品過濾器)  
再按一次 shift+home 就會退出 notifier

notifer 代碼分兩個部分  
1.一個是當物品掉落, 螢幕上會出現提示  
2.另外一個是當你按 alt, 地上要顯示或是隱藏的物品  
不過當你設定了該物品掉落, 螢幕上出現提示  
按 alt 該物品就會顯示  
即使他在你設定要隱藏的種類裡面

預設的 notifer 的代碼  
長的類似下面這樣

#general  
1 2 3 4 unique # Tiered uniques  
sacred unique # Sacred uniques  
rare "Ring$|Amulet$"  
"^(On|Lai|Nih|Xar) Rune$"  
"Ring$|Amulet\$|Jewel" unique # Unique jewelry  
"Quiver" unique  
set  
"Belladonna"  
"Shrine \(10" # Shrines

#是註解的意思  
#後面該行的文字他都不會執行  
通常是給人看的  
說明那一行是在做什麼  
1 2 3 4 unique 意思  
就是當品級 1,2,3,4 的獨特物品掉落的時候  
就會出現提示  
下一行 sacred unique  
就是神聖獨特物品的意思  
這邊的 unique  
可以改成 low normal superior magic rare 等等  
可以連著寫在一起  
他就變成 or  
只要符合其中一個他就出現提示  
所以寫成 1 2 3 4 low normal superior magic rare  
他意思就是當掉落的物品是  
品級 1 或是 2 或是 3 或是 4 的低劣或是普通或是強化或是魔法或是稀有的物品的時候  
他就會出現提示

當有被雙引號包起來的時候  
表示裡面的東西是字串文字  
例如  
"Belladonna"表示當掉落的物品文字有 Belladonna  
他就會出現提示  
假如你是玩中文版  
這字串也可以寫中文  
例如  
3 rare "短劍"  
就是當品級 3, 稀有的, 短劍掉落的時候, 出現提示

字串不一定要完全符合  
只要有包含他就會出現提示  
例如  
1 magic "Helm"  
當掉落的物品是品級 1, Great Helm 的魔法物品  
他也算是有符合  
因為物品 Great Helm, 名稱中有 Helm  
PS:注意大小寫有區別, 第一個英文字母都是大寫, 最保險就是去官方文件複製他上面寫的英文字母

字串有支援正規表示法  
正規表示式稍難  
不過 google,網路上很容易就找到教學  
已經是寫程式的範疇了  
"^(On|Lai|Nih|Xar) Rune$"  
意思是當On或是Lai或是Nih或是Xar符文掉落的時候出現提示  
你要在多加其他符文, 例如Lah  
就是在Xar後面|Lah  
所以就變成  
"^(On|Lai|Nih|Xar|Lah) Rune$"

假如你要隱藏物品  
就是用上面的規則寫出物品  
然後在前面多一個 hide  
例如  
hide "Rune"  
他就會把物品裡面有 Rune 的隱藏起來  
這樣就把 1~50 號符文都隱藏起來了  
假如你在 hide "Rune"下一行寫  
show "^(On|Lai|Nih|Xar|Lah) Rune\$"  
他就會把這些符文顯示出來  
代碼是逐行執行的  
所以有點類似說  
現在有四個窗戶  
我第一行先把四個窗戶都關起來  
第二行寫打開第三個跟第四個窗戶  
這樣就會變成 1 2 是關的, 3 4 是開的

多多嘗試  
看一下他是不是如你預期  
你就知道怎麼玩了
