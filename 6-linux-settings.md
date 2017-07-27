# Linux 下 Shadowsocks 設置方法

## 1、GUI 客戶端

這裏我們推薦使用 [shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5)

1. [安裝方法](https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97)
2. [使用方法](https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C)
3. [常見問題](https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E5%92%8C%E8%A7%A3%E5%86%B3%E5%8A%9E%E6%B3%95)


## 2、命令行客戶端

下面我們以 [Python 版](https://pypi.python.org/pypi/shadowsocks)的 Shadowsocks 為例

### 1、更新系統

Debian / Ubuntu

```
sudo apt-get update
```

CentOS / RHEL / Fedroa

```
sudo yum update
```

### 2、根據自己的發行版安裝 PIP

Debian

```
sudo apt-get install python-dev build-essential python-pip
```

Ubuntu

```
sudo apt-get install python-pip
```

CentOS / RHEL / Fedora

```
sudo yum install python-pip
```

Archlinux

```
sudo pacman -S python-pip
```

### 3、升級 PIP
`pip install --upgrade pip`

### 4、用 pip 安裝 Shadowsocks 和相關依賴

```
pip install shadowsocks
```

### 5. 設置 Shadowsocks 配置文件

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

### 6、啓動 Shadowsocks

```
/usr/local/bin/sslocal -c /etc/shadowsocks.json -d start
```


### 7、安裝 proxychains

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

### 8、 在應用程序內代理

您衹需要將程式指定為**socks v5**的代理

服務器 127.0.0.1 端口 1080（應與 Shadowsocks 客戶端的本地端口對應，默認為1080）

### 9、 關閉 Shadowsocks

在終端輸入

```
lsof –i:1080
```

kill 相應 pid 即可

### 10、OpenSSL 1.1.0 錯誤

如果您在最新的 Debian 9.x 下遇到如下錯誤提示

```
AttributeError: /usr/lib/x86_64-linux-gnu/libcrypto.so.1.1: undefined symbol: EVP_CIPHER_CTX_cleanup
```

是因為 OpenSSL 1.1.x 版本中，廢棄了 `EVP_CIPHER_CTX_cleanup` 函數，我們可以用 `EVP_CIPHER_CTX_reset` 來代替此函數

修改文件 `/usr/lib/python2.7/site-packages/shadowsocks/crypto/openssl.py`

將第 52 行 `libcrypto.EVP_CIPHER_CTX_cleanup.argtypes = (c_void_p,)` 改為 `libcrypto.EVP_CIPHER_CTX_reset.argtypes = (c_void_p,)`

將第 111 行 `libcrypto.EVP_CIPHER_CTX_cleanup(self._ctx)` 改爲 `libcrypto.EVP_CIPHER_CTX_reset(self._ctx)`

然後重新啓動 Shadowsocks 即可

[參考](https://blog.lyz810.com/article/2016/09/shadowsocks-with-openssl-greater-than-110/)


## 3、瀏覽器使用方法

1. [Firefox 瀏覽器設置教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/7-1-firefox-settings.md)
2. [Chrome 瀏覽器設置教程](https://github.com/Shadowsocks-Wiki/shadowsocks/blob/master/7-2-chrome-settings.md)
