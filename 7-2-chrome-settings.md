# Chrome + Proxy SwitchyOmega 设置

這裏假設您已經配置好 Shadowsocks 客戶端，具體請參考

[Windows 下安裝配置 Shadowsocks 使用教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/2-windows-settings.md)

[macOS 下安裝配置 Shadowsocks 使用教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/3-macos-settings.md)

[Linux 下安裝配置 Shadowsocks 使用教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/6-linux-settings.md)

注：本文并不適合任何手機上的 Firefox 瀏覽器  

## 1、安裝擴展

您可以通過chrome商店安裝 [Proxy SwitchyOmega](https://chrome.google.com/webstore/detail/padekgcemlokbadohgkifijomclgjgif) 擴展

如果無法訪問，您也可以直接在 [Github](https://github.com/FelisCatus/SwitchyOmega/releases) 下載 .crx 文件并拖入 `chrome://extensions/` （請使用 Chrome 瀏覽器複製粘貼輸入地址欄並回車訪問）

## 2、擴展的配置(以下方法 2 選 1 即可)

### 1、使用本站提供的已經設置好的備份直接恢復配置（推薦）

通過這個鏈接下載 switchyomega 的配置文件

Windows 用戶[點擊這裏](https://portal.shadowsocks.la/dl.php?type=d&id=39)下載

macOS 用戶按客戶端不同分有兩種：

1. [shadowsocksx對應的switchyomega配置文件](https://portal.shadowsocks.la/dl.php?type=d&id=55)
2. [shadowsocksx-ng對應的switchyomega配置文件](https://portal.shadowsocks.la/dl.php?type=d&id=54)

然後打開 `Proxy SwitchyOmega` 的設置，選擇從備份文件恢復，然後選擇剛才下載的文件，如圖

![](https://ooo.0o0.ooo/2016/06/22/576a3a86d866b.png)

這時點擊 `switchyomega` 圖標，可以看到有三個模式

```
ss
ss-白名單
ss-黑名單
```

三個的區別，當你的代理模式選中

1. ss，所有的網址都經過代理。
2. ss-白名單，內置一個列表，所有匹配這個列表的網址，都不走代理，其它走代理
3. ss-黑名單，內置一個列表，所有匹配這個列表的網址，走代理，其它不走代理
注： 也可以選中系統代理，即使用上面所提到的系統代理

*記得一定要選擇 系統代理 / ss / ss-白名單 / ss-黑名單 四者其中之一，選直連不會走代理的*

（如果不准備使用本站提供的配置文件並且希望配合 GFWList 規則實現自動代理，請看下面內容）

**（如果使用了本站提供的配置文件，請忽視下面的內容）**

### 2、設置配合 GFWList 實現自動切換的模式

按照下圖所示

1. 單擊新建情景模式，在彈出的窗口中選中自動切換，並且將名稱填寫為自動切換或其他名稱
2. 在新的頁面，首先單擊添加在線規則
![](https://ooo.0o0.ooo/2016/06/22/576aaba960469.png)
3. 將規則列表規則對應的 ③ 的位置地方選為 Shadowsocks 對應的規則，如果之前是導入本站的備份的話，請選中 ss 即可。
4. 將規則列表格式選中 AutoProxy
5. 在規則列表網址中填入
`https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt`

![](https://ooo.0o0.ooo/2016/06/22/576aa998042f0.png)

之後可以可以通過選中該模式實現自動代理，如果特殊需要的域名也可以手動通過添加條件指定代理
