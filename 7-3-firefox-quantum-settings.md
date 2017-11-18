# Firefox 配合 GFWList 實現自動切換代理 （安裝 ProxySwitch Omega 擴展）  
本文適用於 Firefox Quantum （Firefox 57 以上版本）  

這裏假設您已經配置好 Shadowsocks 客戶端，具體請參考

[Windows 下安裝配置 Shadowsocks 使用教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/2-windows-settings.md)

[macOS 下安裝配置 Shadowsocks 使用教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/3-macos-settings.md)

[Linux 下安裝配置 Shadowsocks 使用教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/6-linux-settings.md)

注：本文并不適合任何手機上的 Firefox 瀏覽器

## 安裝擴展

1、首先前往[插件商店頁面](https://addons.mozilla.org/zh-CN/firefox/addon/switchyomega/)安裝 ProxySwitch Omega 擴展

## 擴展的配置 

### 1、使用本站提供的已經設置好的備份直接恢復配置（推薦）

通過這個鏈接下載 switchyomega 的配置文件

Windows 用戶[點擊這裏](https://portal.shadowsocks.la/dl.php?type=d&id=64)下載

macOS 使用客戶端為 ShadowsocksX-NG 對應的配置文件：  
[ShadowsocksX-NG 對應的 SwitchyOmega 配置文件](https://portal.shadowsocks.la/dl.php?type=d&id=68)

然後打開 `Proxy SwitchyOmega` 的設置，選擇從備份文件恢復，然後選擇剛才下載的文件，如圖

![](https://ooo.0o0.ooo/2016/06/22/576a3a86d866b.png)

這時點擊 `switchyomega` 圖標，可以看到有兩個模式

```
全局模式
自動切換
```

兩個的區別，當你的代理模式選中

1. 全局模式，所有的網址都經過代理。
2. 自動切換，由 GFWlist 更新的被屏蔽網站的網址列表，所有匹配這個列表的網址，都走代理，其它不走代理。

*記得一定要選擇 系統代理 / 全局模式/ 自動切換 三者其中之一，選直連不會走代理的*
