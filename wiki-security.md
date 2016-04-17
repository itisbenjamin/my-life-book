# 隱匿化使用 Wikipedia 

結合 proxychains 和 telnet 隱匿化使用 Wikipedia"

## Wikipedia-telnet

近期，Wikipedia 開放了 telnet 端口，同時支持自己搭建服務，源碼倉庫[在此](https://github.com/)。

使用 telnet 連接 Wikipedia 時，可以最大限度的保存自身上網瀏覽信息不會外洩，利用 Terminal 接收源碼，同時可以直接進行交互查找。

**搭建 wikipedia-telnet 環境**

```sh
$ npm install -g wikipedia-telnet
```

接下來就可以使用`wikipedia-telnet`來進行連接，默認監聽端口是`1081`，可以在命令後添加端口數來指定端口。

```sh
$ wikipedia-telnet 1888
```

此時監聽端口就是`1888`。

## Proxychains

接下來需要為`telnet`設置`proxy`，這裡使用的`proxychains`可以為 Terminal 內的所有命令行指定代理。

**搭建 proxychains 環境**

利用`brew`來安裝管理`proxychains`。

```sh
$ brew install proxychains-ng
```

**修改配置文件**

```sh
$ vim /usr/local/Cellar/proxychains-ng/4.11/etc/proxychains.conf
```

配置文件中的說明寫的非常詳細，如果有什麼其他需要可以一起按照說明添加，如果沒有的話在配置文件中加上需要配置的監聽端口就可以了，`proxychains`默認的是 Tor 的端口。

```raw
socks5 1080
socks5 9150
http/https 8787
```

上面分別是 shadowsocks 、 Tor 、以及 Lantern 的默認監聽端口，如果你有修改過，就填寫修改後的端口。

**使用 proxychains**

要想使用 proxychains，只需要在命令行前加上`proxychains4`就可以了，比如說安裝`npm`依賴包：

```sh
$ proxychains4 npm install -g wikipedia-telnet
```

這時候這行命令就會通過`proxychains`所指定的`proxy`來進行。

## 通過 Telnet 連接 Wikipedia

所有的準備工作都做好了，這時候就可以安全放心的連接到 Wikipedia 來進行資料搜索了。

**連接 wikipedia-telnet**

首先通過`proxychains`連接到`wikipedia-telnet`：

```sh
$ proxychains4 wikipedia-telnet 1888
```

這時候如果連接成功，Terminal 會顯示本地監聽端口在 `1888`。

**通過 telnet 連接 Wikipedia**

接下來通過`telnet`連接到 Wikipedia ：

```sh
$ proxychains telnet 127.0.0.1:1888
```

此時如果連接成功，就會顯示 Wikipedia 的主頁。

這時候已經進入交互界面，可以通過輸入關鍵字在 Wikipedia 中進行查找，最後輸入`quit`就可以結束連接。



