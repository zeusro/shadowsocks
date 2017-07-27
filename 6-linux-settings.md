# Linux 下 Shadowsocks 設置方法

## 1、桌面用戶安裝 GUI 客戶端 shadowsocks-qt5 使用

桌面端我們推薦使用shadowsocks-qt5 ，下面的教程fork 自開發者的[文檔](https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E5%AE%89%E8%A3%85% E6%8C%87%E5%8D%97)

### Ubuntu

通過 PPA 源安裝，僅支持 Ubuntu 14.04 或更高版本

```
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```

### Debian

可以嘗試安裝 Ubuntu PPA 源的 deb 包，如果不行，請自行編譯

```
dpkg-buildpackage -uc -us -b
```

在上級目錄中將會生成 shadowsocks-qt5 的 deb 包，通過 `sudo dpkg -i` 來安裝

注意：你可能需要安裝好的依賴關係：

```
sudo apt-get install qt5-qmake qtbase5-dev libqrencode-dev libqtshadowsocks-dev libappindicator-dev libzbar-dev libbotan1.10-dev
```

### Fedora

1. 使用 dnf 添加 shadowsocks 的 Copr 源

```
sudo dnf copr enable librehat/shadowsocks
```

2. 使用 dnf 更新 cache 並安裝

```
sudo dnf update
sudo dnf install shadowsocks-qt5
```

如果使用傳統的yum 包管理工具的話，需要從[Copr](https://copr.fedoraproject.org/coprs/librehat/shadowsocks/)下載相應版本的repo 文件放到`/etc/yum.repos.d /` 下，然後通過`yum` 安裝：

```
sudo yum update
sudo yum install shadowsocks-qt5
```

RHEL/CentOS 用戶請確認已經添加了[EPEL源](https://fedoraproject.org/wiki/EPEL)。

### Arch

[官方Community源](https://www.archlinux.org/packages/community/x86_64/shadowsocks-qt5/)

### Gentoo

[gentoo-zh](https://github.com/microcai/gentoo-zh)，由microcai維護

### 其他發行版

請自行抓取[源碼](https://github.com/shadowsocks/shadowsocks-qt5)編譯

## 2、服務器用戶命令行客戶端

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
