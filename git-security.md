# Github隱匿化使用

最近拜讀了編程隨想的Blog，發現自己雖然已經能夠做到現實身份同網絡身份分離，但網絡身份本身安全程度仍舊不高。為了增強自身隱匿性，我重新部署了一次自己的Github。

## 註冊

如編程隨想在Blog中所說，“如果你想要做到徹底隱匿，那麼從一開始就必須是隱匿的”，那麼從註冊的時候就要開始注意自身信息的洩漏。

雖說Google、Github這些公司還算是有些骨氣的，但只要我能想到一種追踪的方法，必然就能有一千萬個人能想到一千萬中方法追踪到我，漏洞不可避免，但在網絡安全方面，絕對不可心存僥倖。

註冊使用VPN + Tor雙重加密進行，其中Tor Browser全局禁止腳本，不到萬不得已，絕不打開。其中註冊的時候會臨時允許一次，但在過後一定要再次禁止。

## Github遠程服務器準備工作

<i class="fa fa-bookmark"></i> <strong>建立repository</strong>

在Github主機上建立一個空倉庫，此時仍舊使用VPN + Tor雙重加密。

<i class="fa fa-bookmark"></i> <strong>添加SSH key</strong>

在這步之後，所有對這個repository的pull以及push操作全部在本地終端進行，除非新建repository，不用再在圖形界面中登陸Github。

首先檢查自己是否已經擁有SSH key。

{% highlight shell %}
$ cd ~/.ssh
$ ls
{% endhighlight %}

查看目錄下是否有SSH key文件。

如果有，略過下面這一步，如果沒有，獲取SSH key。

{% highlight shell %}
$ ssh-keygen -t rsa -b 4096 -C "email- address"
{% endhighlight %}

接下來會要求輸入鑰匙對儲存地址和`passphrase`，按要求輸入後，SSH key文件就建立好了，`~/.ssh`目錄下會有私鑰`id_rsa`和公鑰`id_rsa. pub`兩個文件，其中私鑰文件*永遠不要告訴任何人*，為了盡可能的安全，我*從不會去打開它*。

打開公鑰文件，在Github的SSH key中添加自己的public key，然後在本地進行測試：

{% highlight shell %}
$ ssh -T git@github. com
{% endhighlight %}

如果收到Github傳送的“Hello Name ...” 這句話，就表示已經連接成功了。

## 本地準備工作

上一步結束後，就可以關閉圖形界面了，剩下的操作全部都在本地終端內進行。

<i class="fa fa-bookmark"></i> <strong>建立本地repository</strong>

Github對於本地對應repository的名稱不做要求，全部都可以在命令行內指定，但是為了方便查找不至於混亂，還是建議本地文件名稱對應遠程服務器名稱。

如果遠程倉庫是空的，那麼需要本地倉庫初始化後建立對應關係。

{% highlight shell %}
$ mkdir repository-name
$ cd repository-name
$ git init
{% endhighlight %}

這樣本地倉庫初始化就完成了。

如果遠程倉庫不是空的，這步可以使用`clone`命令進行替代。

{% highlight shell %}
$ git clone ssh://github. com/username/repository-name.git
{% endhighlight %}

這樣在當前目錄下就會有一個從遠程服務器拉取的repository。

*關於`ssh`加密方式的選擇，後面會另外進行說明。*

<i class="fa fa-bookmark"></i> <strong>本地編輯</strong>

Git最為方便以及安全的並不僅僅是版本庫的保存（這意味著只要操作得當你不會丟失任何東西），還有它方便的本地全部編輯完畢後進行整體推送功能（這意味著在進行編輯時不需要依賴網絡）。

在本地倉庫把代碼調試完畢後，之後再進行本地服務器對遠程服務器的推送。

<i class="fa fa-bookmark"></i> <strong>添加remote</strong>

在進行推送前，需要在本地添加遠程服務器地址。

首先檢查本地關聯服務器列表。

{% highlight shell %}
$ git remote -v
{% endhighlight %}

一般情況下，如果是`clone`的倉庫，會有一個`origin`服務器地址，檢查地址是否正確，如果不正確可以使用下面的命令進行修改：

{% highlight shell %}
$ git remote rm remote-name # delete remove  
$ git remote rename remote-name # rename remote  
{% endhighlight %}

如果服務器列表中沒有服務器地址，使用下面的命令進行添加：

{% highlight shell %}
$ git remote add remote-name remote-url
{% endhighlight %}

<i class="fa fa-bookmark"></i> <strong>檢查分支</strong>

Git中一個倉庫可以擁有無數個分支，這些分支之間互相不影響，可以在修改後和主分支進行合併，也可以因為修改失誤直接刪除，*這些都不會對主分支造成任何影響*，因而也最大程度上保證了數據安全。

下面是一些關於分支的命令。

{% highlight shell %}
$ git branch # list branches  
$ git branch branch-name # add branch  
$ git checkout -b branch-name # add and switch to the new branch
$ git branch -d branch-name # delete branch  
$ git branch -D branch-name # force delete branch(ignore all changes on this branch)
$ git branch rename branch-name # rename branch
{% endhighlight %}

## 推送 push

在本地文件全部調試完成後，添加`.gitignore`文件過濾不需要追踪的文件，之後就可以開始push操作了。

<i class="fa fa-bookmark"></i> <strong>push操作分為三步</strong>

* 添加需要進行追踪的文件 

{% highlight shell %}
$ git add filename  
{% endhighlight %}
如果需要添加所有文件，可以使用下面兩個命令之一：  
{% highlight shell %}
$ git add .  
$ git add -A  
{% endhighlight %}
都代表追踪所有文件。  

* 提交commit  

在push之前，Github要求每次push都必須填寫commit，但對其中的內容不做要求，你可以填寫任何內容，但是*這些commits是公開的、不可刪除的，如果不想通過commit洩漏信息，請謹慎填寫*。  
{% highlight shell %}
$ git commit -m " " 
{% endhighlight %}
其中引號內填寫commit內容。  

* 推送  

這一步需要連接網絡，但是終端推送可以選擇`https`加密來進行push。
{% highlight shell %}
$ git push -u origin branch-name  
{% endhighlight %}
一般情況下默認的分支名稱是`master`，而`u`參數就是為了使本地`master`分支與遠程服務器`master`分支進行對應，在之後的push操作中可以省略，如果是一個`clone`後得到的倉庫，此參數也可省略。

<i class="fa fa-bookmark"></i> <strong>後續push操作</strong>

在完成第一次push操作後，本地倉庫已經和遠程倉庫進行了關聯，接下來很多步驟都可以進行的更加簡潔。

在對已追踪的文件進行修改後，可以將`add`和`commit`命令一起進行。

{% highlight shell %}
$ git commit -a -m " "
{% endhighlight %}

引號內填寫commit內容，如果不填寫，Git會彈出編輯器要求填寫。

## 更多Git終端操作命令

<i class="fa fa-bookmark"></i> <strong>fetch</strong>

在遠程服務器中文件內容被修改後，可以使用`fetch`命令獲取，`fetch`不會對本地文件內容造成任何影響。

{% highlight shell %}
$ git fetch
{% endhighlight %}

同時也可以指定主機名以及分支名。

<i class="fa fa-bookmark"></i> <strong>pull</strong>

`pull`意味著`fetch`後再進行`merge`，對本地文件內容會造成影響。

{% highlight shell %}
$ git pull
{% endhighlight %}

同時也可以指定主機名以及分支名。

## 加密傳送方式選擇

Git支持的常用傳送方式有`git`、`ssh`、`https`、`http`，分別是下面幾種地址格式：

{% highlight shell %}
git://github. com/username/repository-name. git  
ssh://github. com/username/repository-name. git  
https://github. com/username/repository-name. git  
http://github. com/username/repository-name. git  
{% endhighlight %}

<i class="fa fa-bookmark"></i> <strong>Git 協議</strong>

不進行加密，明文傳輸，不建議使用。

<i class="fa fa-bookmark"></i> <strong>HTTP 協議</strong>

不進行加密，明文傳輸，不建議使用。

<i class="fa fa-bookmark"></i> <strong>HTTPS 協議</strong>

加密傳輸，優點是即使沒有Github帳戶，也能夠`clone`倉庫。

<i class="fa fa-bookmark"></i> <strong>SSH 協議</strong>

加密傳輸，Github支持在使用SSH協議進行傳輸時不再需要輸入用戶名和密碼，同時能夠為每個項目都配置不同的鑰匙對，提高安全性。

如果不指配加密方式，Github默認使用SSH協議進行傳輸，命令行如下：
{% highlight shell %}
$ git clone git@github.com/username/repository-name.git
{% endhighlight %}

## SSH 鑰匙對

<i class="fa fa-bookmark"></i> <strong>不修改鑰匙對的前提下修改passphrase</strong>

假設鑰匙對使用本文所提到的`rsa`算法進行加密，修改passphrase命令如下：

{% highlight shell %}
$ ssh-keygen -f ~/.ssh/id_rsa -p
{% endhighlight %}

<i class="fa fa-bookmark"></i> <strong>管理多組鑰匙對</strong>

可以通過創建`~/.ssh/config`文件來管理多組鑰匙對，每一個SSH服務器對應一組鑰匙對，提高安全性。

{% highlight shell %}
Host SERVERNAME
  PreferredAuthentications	publickey
  IdentityFile			~/.ssh/id_rsa_SERVERNAME
  Port				443
  User				git
{% endhighlight %}

更多配置方法可調用`config`配置幫助：
{% highlight shell %}
$ man ssh_config 5
{% endhighlight %}

## 進一步提高隱匿性

如果還有在前文基礎上還有更多需求，下面是一些進一步提高隱匿性的做法。

<i class="fa fa-bookmark"></i> <strong>關聯郵箱</strong>

* 設置郵箱隱私

在Github設置中將郵箱地址設置為private。

* 修改commit配置

因為commit的所有內容都是公開的，因此需要在本地設置commit所顯示的郵箱以及用戶名：
{% highlight shell %}
$ git config --global user.name " "
$ git config --global user.email " "
{% endhighlight %}
在配置完畢後，每次commit所顯示的用戶名和郵箱都是配置後的內容。

* 註冊郵箱

這是最後一道防線，如果最終還是被發現了註冊郵箱，那麼註冊郵箱的地址以及註冊方式就至關重要。

我在註冊Github帳號之前，先使用VPN + Tor註冊了一個sigaint郵箱，再用它用來註冊Github。

總之，永遠不要輕視你的對手。

<i class="fa fa-bookmark"></i> <strong>配置Tor</strong>

為HTTPS以及SSH配置Tor代理。

* HTTPS 協議

命令如下：
{% highlight shell %}
$ git config --global http.proxy SOCKS5h://address:端口號
{% endhighlight %}

*假如Tor運行在本機，那麼地址為：127.0.0.1，否則替換為運行Tor的主機IP地址。*

*如果Tor用的是Tor Browser，端口號是`9150`，如果用的是其他軟件包，端口號為`9050`。*

* SSH 協議

SSH協議的配置通過Netcat來實現（按照編程隨想的方法，暫時不會其他的，據說proxychains也能實現，改天研究）。

首先檢查系統是否已經搭建好`nc`環境，Linux大部分發行版都配置有Netcat，我的Mac也是系統自帶`nc`環境。

測試SSH through Tor SOCKS:  
{% highlight shell %}
$ ssh -o "ProxyCommand=nc -X 5 -x address:端口號 %h %p" -T ssh.github.com
{% endhighlight %}

*地址與端口號配置同HTTPS協議配置方法*

最終Github會拒絕訪問，這樣就SSH說明已經通過SOCKS連結到Github了。

最後在`~/.ssh/config`配置文件中添加如下配置：  
{% highlight shell %}
ProxyCommand /usr/bin/nc -X 5 -x address:端口號 %h %p
{% endhighlight %}

<i class="fa fa-bookmark"></i> <strong>代碼風格</strong>

到了這裡，幾乎所有在Github上公開顯示的和個人隱私相關的內容就只剩下了源代碼，所以要再進一步提高隱匿性，就必須從這裡下手。

* 代碼混淆

做這一切都是為了最大程度的隱匿，不是為了保護源代碼，代碼混淆不符合開源精神，不建議採用這種方法。

* 改變代碼風格

刻意製定一種特殊的代碼風格，與自身原風格不同，但容易掌握。比如將`id`的命名方式由簡稱改為全稱，將`_`改為`-`，縮進風格由制表符改為空格等。

如果是不重要的代碼組成部分，可以使用他人的源碼替代來達到同等效果。

* 更換語言

使用一種自己平時不常用的語言來書寫代碼，或一種小眾語言來書寫。

*當然，如果是Github的付費用戶，可以將倉庫設為私有，如果使用GitLab一類的替代品，可以擁有無限的私有倉庫，但是私有化將失去一切開源的價值和意義。*

---

參考內容：

<https://program-think.blogspot.com/2016/03/GitHub-Security-Tips.html>  
<https://wiki.archlinux.org/index.php/SSH_keys_(简体中文)>




