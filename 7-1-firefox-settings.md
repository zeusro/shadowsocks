# Firefox 配合 GFWList 實現自動切換代理 （安裝 Foxyproxy-standard 擴展）

這裏假設您已經配置好 Shadowsocks 客戶端，具體請參考

[Windows 下安裝配置 Shadowsocks 使用教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/2-windows-settings.md)

[macOS 下安裝配置 Shadowsocks 使用教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/3-macos-settings.md)

[Linux 下安裝配置 Shadowsocks 使用教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/6-linux-settings.md)

注：本文并不適合任何手機上的 Firefox 瀏覽器

目前因為 Firefox 插件 AutoProxy 的作者已經很久沒更新了，導致該擴展在最新版的 Firefox 擴展上已經無法訂閱 GFWList 規則，所以不能正常使用，使用 [foxyproxy-standard](https://addons.mozilla.org/zh-CN/firefox/addon/foxyproxy-standard/) 擴展，可以替代實現其功能。

## 安裝擴展

1、首先前往[插件商店頁面](https://addons.mozilla.org/zh-CN/firefox/addon/foxyproxy-standard/)安裝 foxyproxy-standard 擴展

2、安裝後重啟 Firefox ，通過單擊地址欄右側**小狐狸**圖標或者是 Firefox 附件組件 擴展 頁面 **foxyproxy-standard** 的選項按鈕打開擴展的設置界面，如圖

![](https://ooo.0o0.ooo/2016/06/22/576a4678571c9.png)

![](https://ooo.0o0.ooo/2016/06/22/576a4678697b5.png)

3、在設置界面 單擊新建代理服務器 ，打開添加代理服務器的頁面，按照下圖所示添加一個 地址為 127.0.0.1 端口為 1080 的 socks v5 的代理

![](https://ooo.0o0.ooo/2016/06/22/576a4678703ee.png)

4、在設置界面單擊模式訂閱，再空白處單擊鼠標右鍵，選中添加新的模式訂閱

![](https://ooo.0o0.ooo/2016/06/22/576a46789433e.png)

5、在添加訂閱的界面，按照如圖所示添加一個 GFWList 的訂閱

![](https://ooo.0o0.ooo/2016/06/22/576a46789e6f1.png)

然後填入 gfwlist 的地址

```
https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
```

6、返回最開始的設置界面，將工作模式設置為 使用基於其預定模式的代理服務器

![](https://ooo.0o0.ooo/2016/06/22/576a46789ccad.png)

7、測試代理是否可用，當網站經過代理時，地址欄的小狐狸會旋轉，而不經過則不會轉動

![](https://ooo.0o0.ooo/2016/06/22/576a49af63c9b.gif)
![](https://ooo.0o0.ooo/2016/06/22/576a49af91a0b.gif)

*注：可以通過鼠標中鍵單擊地址欄的小狐狸圖標切換代理模式 *
*包括 不適用代理（帶禁止圖標的小狐狸）、自動模式、全局模式 *
*請按照自己需要的模式選擇使用 *
 

如果您在安裝插件的時候提示 火狐瀏覽器安裝插件的時候提示此附加組件無法安裝，因為它未經驗證

請在地址欄輸入 `about:config` 後進入並修改 `xpinstall.signatures.required` 為 `false`

具體看下圖

![](https://ooo.0o0.ooo/2015/12/21/56782ec25c2c3.jpg)
![](https://ooo.0o0.ooo/2015/12/21/56782f83c05cb.png)
