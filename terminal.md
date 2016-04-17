# Mac OS X Terminal Command Line"

永遠記住
    <br>機器不會思考，它只會忠實執行你所下達的所有命令
    <br>一個空格甚至可能導致整個系統崩潰
    <br>在發出任何指令前，都必須經過深思熟慮。"

## Command Line

* Mac使用Unix文件系統。

* 訪問圖形界面無法顯示內容及Finder隱藏內容。

* 遠程訪問MAC（SSH）。

* 通過`sudo`命令獲得root權限

* 每條命令包含Command Name、Options、Arguments、Extras四部分，其中後三部分可選。<br>Options：`-`作為前導符，如命令只包含單個字母，則可合併。<br>Arguments：具體細化命令。<br>Extras：實現其他功能。

##  進入Terminal

### 圖形界面

Finder --> Applications --> Terminal

### 非圖形界面

開機F8 --> -s參數啓動 --> mount -uw /

## 獲得Root權限

`$ sudo -s`
    
注：輸入密碼時無任何圖形顯示。

## 幫助指令

全局幫助：

`$ man -k`

指定命令名稱：

`$ man command-name`
    
## 文件路徑

**在Unix系統書寫命令時對字母大小寫是敏感的，同時必須書寫文件擴展名。**

絕對路徑：

`$ /Users/Ben/Dropbox/message.txt`
    
相對路徑：

`$ /Dropbox/message.txt`
    
在Terminal中，同HTML語法一致，可使用`../..`來省略父級目錄。同時，`~`可以代表當前用戶home folder，如`~/Dropbox/message.txt`。

## 特殊字符

如目錄中含有空格、`()`、` "" `、`[]`、`!`、`$`、`&`、`*`、`;`、`|`、`\`等特殊字符，可使用`/`加以識別（同Markdown語法）。

## 基本命令

`pwd`：print working directory，顯示當前目錄的絕對路徑。

`cd`：change directory，改變當前目錄到指定目錄。如不指定，則返回home folder。

`mkdir`：建立新目錄。

`$ mkdir /Users/Ben/Dropbox/Applications`
    
`touch`：在當前目錄下建立新文件。文件前不可指定目錄。

`$ touch test.txt`
    
## 列出文件
    
`ls`：list directory contents，列出當前目錄內容。

`$ ls -w -l -a /Users/Ben/Dropbox`
    
**參數**

* `-w`：顯示中文。

* `-l`：顯示詳細信息。

* `-a`：顯示隱藏文件。

## 拷貝文件

`$ cp -R /Users/Ben/test.txt /Users/Ben/Dropbox`
    
指將test.txt文件拷貝至Dropbox目錄下。
    
**參數**

* `-R`：Recurive，對目錄進行遞歸操作。

## 移動文件

`$ mv /Users/Ben/test.txt /Users/Ben/Dropbox`
    
將test.txt移動至Dropbox文件夾內。僅指定新文件名，則重命名原文件。

## 刪除文件

### 文件

`$ rm -rf /Users/Ben/test.txt`
    
**參數**

* `-rf`：`-r`與`-f`的省略寫法，Recurive & Force，遞歸及強制。***此參數務必小心使用，如執行`rm -rf / `，則清除整個系統。***

**注：**

* 如使用`$ rm`命令刪除文件，磁盤上仍然可能存有殘留，此時可使用`$ srm`命令徹底安全的刪除文件。

* 刪除文件夾時可直接使用強制遞歸參數整體刪除。

## 檢視文件

### cat

concratenate，按順序讀取文件並輸出到Terminal窗口

`$ cat ../message1.txt >> message2.txt`
    
其中`>>`表示將`message1.txt`中的內容添加到`message2.txt`結尾。

### less

允許查找文本，適合長文本查看。可使用箭頭按鈕上下移動光標，使用空格翻頁，輸入`/`及關鍵字來檢索，按`Q`鍵退出使用指南頁面，按`V`鍵來使用`vi`文本編輯器。

### which

定位某個命令的文件路徑。

### file

輸出目標文件類型，即使文件擴展名缺失仍舊有效。

### find

根據搜索關鍵詞定位文件路徑。

`$ find ../Dropbox -name "test.txt"`
    
指以Dropbox目錄為起始路徑，搜索`test.txt`文件。

**注：**

* 使用參數`-x`檢索根目錄。

* 使用`mdfind`命令來調用Soptlight搜索服務。

## 通配符（Wildcard Characters）

### 星號（＊，Asterisk）

代表任何長度的任何字符。如`*.txt`代表所有格式為`txt`的文件。

### 問號（？，Question mark）

代表任何單個字符。如`m?ssage`匹配`message`但不匹配`messages`。

### 方括號（［］，Square brackets）

定義一定範圍的字符。如`[Mm]essage`匹配`Message`及`message`，`pic[1-9]`匹配`pic1`, `pic2`, ..., `pic9`。

## 文本編輯

`$ nano /Users/Ben/test.txt`
    
編輯test.txt文件。完成後Ctrl + O儲存，Ctrl + X退出。

## VI模式

Visual。是Command Line中最常見的文本編輯器，進入VI模式後，會佔用整個Terminal空間來顯示文件內容。

在進入VI模式時，默認進入Command模式，按`A`鍵進入編輯模式。

編輯結束後，按`esc`鍵回到Command模式，按住`Shift`鍵的同時按兩次`Z`鍵來保存並退出。如放棄保存，則輸入`:q !`執行強制退出命令。

## 更改文件權限

`$ chmod -R 755 /Users/Ben/test.txt`
    
將test.txt文件設定為root讀寫，其餘用戶只讀。

**參數**

* `-R`：Recurive，遞歸參數。

* `755`：各用戶權限。

## 更改文件屬主

將test.txt屬主改為root用戶。

`$ chown -R root:wheel /Users/Ben/test.txt`
    
修復整個系統文件權限：

`$ diskutil repairpermissions / `

## 利用Terminal開啓系統功能

### 顯示／隱藏Library

顯示：

`$ chflags nohiddden ~/Library/`
    
隱藏：

`$ chflags hidden ~/Library/`
    
### 顯示／隱藏文件

顯示：

{% highlight shell %}
$ defaults write com.apple.finder AppleShowAllFiles -bool true
$ killall Finder
{% endhighlight %}
    
隱藏：

{% highlight shell %}
$ defaults write com.apple.finder AppleShowAllFiles -bool false
$ killall Finder
{% endhighlight %}
    
### Finder標題欄顯示完整路徑 

{% highlight shell %}
$ defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES
$ killall Finder
{% endhighlight %}
    
### 改變截圖陰影

截圖：`Command-Shift-4`

去掉陰影：

{% highlight shell %}
$ defaults write com.apple.screencapture disable-shadow -bool true
$ killall SystemUSServer
{% endhighlight %}
    
保留陰影:

{% highlight shell %}
$ defaults write com.apple.screencapture disable-shadow -bool false
$ killall SystemUSServer
{% endhighlight %}
    
## 改變截圖保存位置

{% highlight shell %}
$ defaults write com.apple.screencapture location /Users/Ben/Screencapture
$ killall SystemUIServer
{% endhighlight %}
    
---

## 附錄：Unix系統命令參考

### 目錄操作

|   Command   |   Description   |   Example   |
| :------------ | :-------------: | ----------: |
| mkdir | 創建目錄 | mkdir test |
| rmdir | 刪除目錄 | rmdir test |
| mvdir | 移動或重命名目錄 | mvdir ../test ../test-2 |
| cd | 改變當前路徑 | cd ../test-2 |
| pwd | 顯示當前路徑名 | pwd  |
| ls | 顯示當前目錄中內容 | ls  |

### 文件操作

| Command | Description | Example |
| :------------ | :-------------: | ----------: |
| cat | 顯示或連接文件 | cat test.txt |
| od | 顯示非文本文件內容 | od -c test.app |
| cp | 拷貝文件或目錄 | cp ../test.txt ../test-2.txt |
| rm | 刪除文件或目錄 | rm test.txt |
| mv | 移動文件 | mv ../test.txt ../test.txt |
| find | 使用匹配表達式查找文件 | find . -name "*.c" -print |
| file | 顯示文件類型 | file test.txt |

### 選擇操作

| Command | Description | Example |
| :------------ | :-------------: | ----------: |
| head | 顯示文件最初幾行 | head -10 test.txt |
| tail | 顯示文件最後幾行 | tail -10 test.txt |
| cut | 顯示文件每行中的某些域 | cut -f1,7 -d: /etc/passwd |
| colrm | 從標準輸入中刪除若干列 | colrm 5 20 test.txt |
| diff | 比較並顯示兩個文件的差異 | diff file1 file2 |
| sort |	排序或歸並文件 |	sort -d -f -u file1 |
| uniq |	去掉文件中的重復行 |	uniq file1 file2 |
| comm |	顯示兩有序文件的公共和非公共行 | comm file1 file2 |
| wc |	統計文件的字符數、詞數和行數 | wc filename |
| nl	 | 給文件加上行號 | 	nl file1 >file2 | 

### 進程操作

| Command | Description | Example |
| :------------ | :-------------: | ----------: |
ps |	顯示進程當前狀態 |	ps u
kill |	終止進程 |	kill -9 30142

### 時間操作

| Command | Description | Example |
| :------------ | :-------------: | ----------: |
date |	顯示系統的當前日期和時間	 | date
cal	 | 顯示日曆	 | cal 8 1996
time |	統計程序的執行時間 |	time a.out

### 網絡與通信操作

| Command | Description | Example |
| :------------ | :-------------: | ----------: |
telnet |	遠程登錄 |	telnet hpc.sp.net.edu.cn
rlogin |	遠程登錄 |	rlogin hostname -l username
rsh	| 在遠程主機執行指定命令 |	rsh f01n03 date
ftp	| 在本地主機與遠程主機之間傳輸文件 | ftpftp.sp.net.edu.cn
rcp	 | 在本地主機與遠程主機 之間複製文件 | rcp file1 host1:file2
ping |	給一個網絡主機發送 回應請求 |	ping hpc.sp.net.edu.cn
mail | 閱讀和發送電子郵件	 | mail
write |	給另一用戶發送報文 |	write username pts/1
mesg | 	允許或拒絕接收報文 |	mesg n

### Korn Shell 命令

| Command | Description | Example |
| :------------ | :-------------: | ----------: |
history	| 列出最近執行過的 幾條命令及編號 | history
r	| 重復執行最近執行過的 某條命令 |	r -2
alias	| 給某個命令定義別名 |	alias del=rm -i
unalias	 | 取消對某個別名的定義 | 	unalias del

### 其它命令

| Command | Description | Example |
| :------------ | :-------------: | ----------: |
uname	| 顯示操作系統的有關信息 |	uname -a
clear	| 清除屏幕或窗口內容 |	clear
env	| 顯示當前所有設置過的環境變量 | env
who	| 列出當前登錄的所有用戶 |	who
whoami |	顯示當前正進行操作的用戶名 | whoami
tty	| 顯示終端或偽終端的名稱 |	tty
stty	| 顯示或重置控制鍵定義	| stty -a
du | 	查詢磁盤使用情況 | 	du -k subdir
df /tmp | 	顯示文件系統的總空間和可用空間 | df/tmp
w	| 顯示當前系統活動的總信息 | w

---

<center>
    「盡可能的榨取軟件的全部價值」
    <br>「所有程序都是數據的過濾器」
    <br>「沈默是金」
    <p>—</p>
    <p>The UNIX Philosophy</p>
</center>

<div class="eof"></div>

