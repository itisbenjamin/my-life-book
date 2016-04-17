# 結合 Carina 部署 Docker 鏡像 

最近一篇使用 Carina 搭建 SS 服務的博文在 Twitter 上很火，雖然第二天 Carina 就禁用了 SS 的鏡像，但是這並不妨礙使用 Carina 做一些其他有趣的事。

也是因為這次事件，Carina 禁用了所有中國大陸地區 +86 的手機號碼驗證，因此如果要想使用 Carina 的免費服務器，就必須有一個國外的手機號來進行驗證。但即使你沒有國外的手機，我也相信聰明的你一定會找到辦法。

## 關於 Carina 和 Docker

我也是在這次事件後才知道 Carina，之前有聽說過 Docker，但一直都沒有使用，以為 Docker 就和 npm 或者 Git 差不多這個樣子，這次才逐漸的了解了一些關於 Docker 的內容。

簡單來說，Docker 就像一個虛擬機倉庫，或者官法說法——容器。它之中有很多個鏡像源，比如從 Docker 拉取 Debian 鏡像後，你拉取的是一個擁有可讀權限的鏡像，在你進行修改過後，會在上面覆蓋一層可寫層，因此底層鏡像永遠不會遭到損壞。這個可寫層可以覆蓋最多127層，基本已經滿足了正常需要。

說了這麼多，Docker 能用來做什麼呢？

它可以用來演示一些新功能，免去了自己重新部署的麻煩，也可以用來測試一些不穩定的代碼，或者折騰一些危險的活動。因為在使用完畢後，不用擔心對自己系統的困擾，直接刪除鏡像就可以了。

而 Carina 為 Docker 提供了一個免費的服務器內存，這樣所有 Docker 鏡像的部署都在 Carina 服務器上，而非自己的電腦上，並且這個服務器是可以對外訪問的，所以你也就能想到它能做什麼了吧。

搭建 Blog 啊，網站啊，下載地址啊，等等等等。

## 安裝 Docker 和 Carina

Docker 和 Carina 都可以通過命令行安裝，如果你需要圖形界面，可以通過官網下載，分別是 [Docker](https://docker.com) 和 [Carina](https://getcarina.com)

```sh
$ brew update
$ brew install docker
$ brew install carina
```

接下來通過命令行呼出 `docker` 和 `carina` 就可以看到它們的幫助說明，其中 Docker 的命令行比較繁雜，可以看看官方文檔多加了解。

## Client & Server API

在最新的 Docker 更新了之後，使用的 Client API 端口版本是 1.23，Go 語言版本是 1.5.4，而 Carina 使用的 Server API 端口版本是 1.22，Go 語言版本是 1.5.3，所以因為這個版本衝突，如果不引入 Docker Client 版本管理插件，是不能訪問 Carina 服務器的。

如果彈出了如下警告，就必須使用 dvm 來進行版本管理。

```sh
Error response from daemon: client is newer than server (client API version: 1.23, server API version: 1.22)
```

### OS X / Linux

Terminal 命令行：

```sh
$ curl -sL https://download.getcarina.com/dvm/latest/install.sh | sh
```

### Windows

PowerShell 命令行：

```sh
> iex (wget https://download.getcarina.com/dvm/latest/install.ps1)
```

### 使用 dvm

在配置完 PATH 後接下來就可以使用 `dvm` 命令了。

```sh
$ dvm upgrade     // upgrade dvm to the latest version
$ dvm ls     // list all API versions and point out which version has been used
$ dvm use      // use the Client API version which fit the Server API version
$ dvm install     // install Client API version
```

上面幾行命令就是比較常見的 dvm 命令行，在連接 Docker 容器後執行 dvm 命令可以不用指定版本， dvm 會自行匹配 Server API version 然後進行安裝。

## 進入 Docker 容器

在做好了準備工作後，就可以在 Carina 上開始部署 Docker 容器了。

首先在 Carina 後台創建一個 Cluster，下載 `Get access` 文件到本地，接下來 `source` 一下自己需要的版本，就連結到 Carina 服務器了。

下面是一些比較常用的 Docker 命令行。

```sh
$ docker info     // list the information about your server
$ docker images     // list all images on your server
$ docker ps -a    // list all processes
$ docker rm $(docker ps -a -q)     // remove all images which has been stopped
```

創建容器：

```sh
$ docker pull debian
```

進入容器進行操作：

```sh
$ docker run -i -t debian /bin/bash
```

更多命令行可以參考官方文檔。

因為操作的是連接的 Carina 服務器，因此直接進入容器操作速度會有些慢。

## 部署一個 Ghost Blog

因為 Carina 的服務器是可以對外訪問的，因此可以用它來搭建網站。除了速度有些略慢以外，滿足跟人需求綽綽有餘。

```sh
$ docker network create wordnet
$ docker run --detach --name ghost --net wordnet --publish 80:2368 ghost
```

因為 Docker 強大的鏡像拉取功能，這兩行命令就可以搭建起一個 Ghost Blog。

接下來查詢 Blog 地址以及端口：

```sh
$ docker port ghost
80/tcp -> 146.20.69.19:80 
```

這就是搭建成功已經可以訪問的 Ghost Blog 了。








