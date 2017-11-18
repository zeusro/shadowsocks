# Linux 下 Shadowsocks 設置方法

## 1、GUI 客戶端 （ 尚不支持 chacha20-ietf-poly1305 加密方式，請使用命令行客戶端 ）

這裏我們推薦使用 [shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5)

1. [安裝方法](https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97)
2. [使用方法](https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C)
3. [常見問題](https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E5%92%8C%E8%A7%A3%E5%86%B3%E5%8A%9E%E6%B3%95)


## 2、命令行客戶端
使用最新的 Python 版本或是 Shadowsocks-libev

### 1. 安裝：
Python : https://github.com/shadowsocks/shadowsocks/tree/master#install  
Shadowsocks-libev: https://github.com/shadowsocks/shadowsocks-libev#installation

下面我們以 [Python 版](https://pypi.python.org/pypi/shadowsocks)的 Shadowsocks 為例


### 2. 設置 Shadowsocks 配置文件

創建一個 `/etc/shadowsocks.json` 文件，格式如下

```
{
    "server":"服務器IP或域名",
    "server_port":端口號,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"密碼",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```

### 3、啓動 Shadowsocks
Python 版客戶端命令是 sslocal ， Shadowsocks-libev 客戶端命令為 ss-local  

```
/usr/local/bin/sslocal -c /etc/shadowsocks.json -d start
```


### 4、安裝 proxychains

這裏以 Debian / Ubuntu 爲例

```
sudo apt-get install proxychains
```

編輯 `/etc/proxychains.conf`

修改最後一行為

```
socks5 127.0.0.1 1080
```

接著我們就可以直接用

```
sudo proxychains apt-get xxxx
sudo proxychains wget xxxx
```

類似的命令使用 Shadowsocks 進行操作程序

### 5、 在應用程序內代理

您衹需要將程式指定為 **socks v5** 的代理

服務器 127.0.0.1 端口 1080（應與 Shadowsocks 客戶端的本地端口對應，默認為1080）

### 6、 關閉 Shadowsocks

在終端輸入

```
lsof –i:1080
```

kill 相應 pid 即可

## 3、瀏覽器使用方法

1. [Firefox 瀏覽器設置教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/7-1-firefox-settings.md)
2. [Chrome 瀏覽器設置教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/7-2-chrome-settings.md)
