# Linux/Ubuntu使用体验"

因为不满足于虚拟机上极端恶劣的开发环境，我将一台原本在闲置吃灰的VAIO重新安装了Ubuntu。

## 为什么选择Ubuntu

**选择Linux**

* 开源。这意味着安全以及便捷，不会出现盗版以及后门这种问题，直接从官网上就可以找到最新版本的系统镜像。
* Unix文件系统。因为我已經习惯了Mac的Unix命令行，Windows的DOS命令行实在是令我感到恐惧，相比之下还是同样基于Unix的Linux系统更加亲切。
* 字符界面。Linux有六个可以直接登陆的命令行界面端口，可以不进入图形界面直接登陆，这对我这个一打开系统四处找Terminal的人来说不能更方便。
* 信仰。不多说什么了。

**选择Ubuntu**

* 适合新手。除了虚拟机以外，我尚且没有直接接触过Linux系统，而Ubuntu的图形界面还是比较亲切的。
* 比较流行。这意味着至少Bug比较少，Linux作为一堆散乱的零件，还是Bug少一些的发行版本比较适合一开始的折腾。
* 这是我暂时了解的最多的Linux发行版本之一，所以我选择从它开始。

## 安装

**下载Ubuntu镜像**

Linux系统完全開源，直接[Ubuntu官网](http://www. ubuntu. com)下载就好。

接下来选择适合自己的版本，一般会有一个稳定版和一个测试版，测试版可能会出现比较多的Bug，但是有利有弊，它同样伴随着新功能。其实稳定版也不会差到那里去，这方面的选择根据自己的能力，量力而行。

**烧录**

从官网上下载下来的是一个`iso`镜像文件，需要进行烧录才能够安装，如果手边有闲置的光盘可以用是最好的，直接烧录进去就可以了。如果没有光盘，可以利用软件烧录在U盘里。在Ubuntu之前这台电脑使用的是Windows系统，所以我使用的是[ISO to USB](http://www. isotousb. com)来进行烧录(這是一個開源免費軟件），对于OS X以及Linux系统可以使用`dd`命令進行裸讀寫，命令行如下：

```sh
$ dd bs=4M if=~/xxx.iso of=/dev/sdb
```

*`if`參數後為ISO文件路徑，`of`參數後為輸出路徑。*

**引导安装**

在烧录完成后，U盘就变成了一个安装光盘，在U盘中打开Ubuntu，就可以看到它的引导页面。

建议最好选择由Ubuntu自己来引导安装，我第一次选择自己重启然后从光盘中启动，结果根本就没有找到光盘项，最后用Ubuntu自己来引导，傻瓜了很多。

**初始化**

在漫长的等待后（因为我选择了同时安装更新和第三方插件），算是把Ubuntu安装完成了一半。到这里系统算是装好了，但是另一半的安装仍旧需要根据自己的需求继续安装插件。

完成安装后，第一个建立的用户就是Administrator。

*这里提醒一点，如果你和我一样习惯使用Terminal来进行操作，那么系统语言一定要选英文，否则你的Terminal里所有的目录名称都将是中文，相信我，执行`cd`命令的时候你会想选择死亡。*

## 字符界面終端

拿到新系統當然要先熟悉目錄結構，Ubuntu有六個字符界面的登錄端口，分別是`tty1-6`，使用`Ctrl + Alt + F1-F6`進行切換，輸入用戶名和密碼就可以登錄。

**中文亂碼問題**

如果非要在字符界面編輯中文，那麼可以使用`fbterm`來實現，命令行：

```sh
$ sudo apt-get install fbterm fcitx im-config fcitx-frontend-fbterm
```

默認必須在root用戶下才能使用，因此需要執行如下命令賦予普通用戶使用權：

```sh
$ gpasswd -a user viedo
$ chmod u+s /usr/bin/fbterm
```

最後修改`~/.fbtermrc`配置，添加：

```sh
input-method=fcitx-fbterm
```

然而這樣仍舊體驗不是很好（不如圖形界面），所以我的建議是，如果你要在終端內編輯中文，還是回到圖形界面的Terminal吧。

## 圖形界面終端

因為字符界面的中文支持不是很好（很差），所以偶爾還是得切換到圖形界面的Terminal進行操作。

關於Terminal的配置可以參考[這篇博文](http://benjaminblog.ml/coding/colorfulterminal.html)，這裡需要說一下Linux系統和OS X一些不同的地方。

**Terminal 整體配色方案**

和OS X不同，Linux系統下不能直接打開Terminal配置文件然後設定為`default`，需要在用戶根目錄下創建一個`solarized.sh`的文件，然後將下面的代碼寫進去：

```sh
#!/bin/sh
#
# Shell script that configures gnome-terminal to use solarized theme
# colors. Written for Ubuntu 11.10, untested on anything else.
#
# Solarized theme: http://ethanschoonover.com/solarized
# 
# Adapted from these sources:
# https://gist.github.com/1280177
# http://xorcode.com/guides/solarized-vim-eclipse-ubuntu/

case "$1" in 
    "dark")
PALETTE="#070736364242:#D3D301010202:#858599990000:#B5B589890000:#26268B8BD2D2:#D3D336368282:#2A2AA1A19898:#EEEEE8E8D5D5:#00002B2B3636:#CBCB4B4B1616:#58586E6E7575:#65657B7B8383:#838394949696:#6C6C7171C4C4:#9393A1A1A1A1:#FDFDF6F6E3E3"
      BG_COLOR="#00002B2B3636"
	  FG_COLOR="#65657B7B8383"
      ;;
	"light")
								
PALETTE="#EEEEE8E8D5D5:#D3D301010202:#858599990000:#B5B589890000:#26268B8BD2D2:#D3D336368282:#2A2AA1A19898:#070736364242:#FDFDF6F6E3E3:#CBCB4B4B1616:#9393A1A1A1A1:#838394949696:#65657B7B8383:#6C6C7171C4C4:#58586E6E7575:#00002B2B3636"
	  BG_COLOR="#FDFDF6F6E3E3"
	  FG_COLOR="#838394949696"
	  ;;
	*)
	echo "Usage: solarize [light | dark]"
	exit
	;;																				
esac
																					
gconftool-2 --set "/apps/gnome-terminal/profiles/Default/use_theme_background" --type bool false
gconftool-2 --set "/apps/gnome-terminal/profiles/Default/use_theme_colors" --type bool false
gconftool-2 --set "/apps/gnome-terminal/profiles/Default/palette" --type string "$PALETTE"
gconftool-2 --set "/apps/gnome-terminal/profiles/Default/background_color" --type string "$BG_COLOR"
gconftool-2 --set "/apps/gnome-terminal/profiles/Default/foreground_color" --type string "$FG_COLOR"
```

接下來修改文件權限：

```sh
$ chmod -x solarized.sh
```

最後運行文件：

```sh
$ ./solarized dark
```

這樣就更改了Terminal的整體配色方案。

## 推薦擴展

Linux基本就是一個乾淨的系統框架，很多東西都是需要自行搭建的。

**Secure delete**

這是一個非常常用的安全刪除命令，它在OS X系統中是自帶的，然而Ubuntu需要自行安裝：

```sh
$ sudo apt-get install secure delete
```

使用命令行：

```sh
$ srm file-name
```

使用`srm`命令會將文件先覆寫38次再刪除，避免了刪除後被還原的可能性。

**GnuPG**

GPG對我來說必不可少，在Ubuntu下是自帶的，如果使用其他Linux系統，安裝以及使用可以參考[這篇博文](http://benjaminblog.ml/coding/gpg.html)。

**VeraCrypt**

磁盤加密軟件，重視隱私安全的人必不可少。同樣，Ubuntu系統安裝VeraCrypt比較麻煩，有兩個選擇，第一是從[VeraCrypt官網](https://veracrypt.codeplex.com)上下載源碼自己編譯，第二是採用下面的命令行：

```sh
$ sudo add-apt-repository ppa:unit193/encryption
$ sudo apt-get update
$ sudo apt-get install veracrypt
```

最後運行VeraCrypt：

```sh
$ veracrypt
```

卸載命令：

```sh
$ sudo apt-get remove veracrypt
```

## 優點

**比Windows使用體驗好**

在這之前這台電腦安裝的是Windows7旗艦版，硬件也不錯，內存500G，按理來說也算是個中配了，然而使用體驗很差，開機速度慢、運行卡頓、機身滾燙，我一直以為是因為是幾年前的機器該淘汰了，然而裝完Ubuntu我才知道是系統的問題。

現在開機速度很快，休眠耗電量少，風扇一般情況下不會轉，機身溫度保持在可以接受的範圍內。

**拯救了我的快捷鍵**

在這之前這台電腦上`Fn`鍵是不起作用的，我無法用快捷鍵調節亮度和聲音，結果Ubuntu完全拯救了我。

不僅如此，Ubuntu還支持觸摸板的快捷操作，比如雙指點按代表右鍵，雙指滾屏這一類的都完美支持。

**字符界面使用感受極佳**

字符界面除了不支持中文以外，其他功能都相當齊全，自帶語法高亮，平時管理文件修改系統文件非常方便。

## 缺點

**中文支持問題**

Linux系統向來對中文的支持非常之差，在Ubuntu下即使找到了一個能用的中文輸入法，也經常無法輸入正確字符，對於繁體的支持就更差了。

雖然有建議用搜狗輸入法，但是我覺得想想這種賣隱私的國產軟件還是可以放棄了。

總而言之，Linux對中文用戶很不親切，還是學好英文吧。

**一堆散亂的零件**

在這之前我看到過有人將Linux系統比作一堆散亂的零件，它經常不管不顧出現問題然後折騰一夜才能救活，現在我也是略有體會。

不僅所有的命令行都是得自己一點點搭建起來，還經常得自己重新編譯。

所以我還是建議在沒有命令行操作基礎的情況下不要碰Linux，先用Mac的Terminal把命令行練熟，否則在Linux系統下連管理文件都很費力。

---

參考內容：
<br><http://linuxg.net/how-to-install-veracrypt-1-0f-1-on-ubuntu-15-04-ubuntu-14-10-ubuntu-14-04-and-derivative-systems/> 
<br><http://www.guokr.com/blog/749084/> 
<br><http://www.cnblogs.com/KarryWang/p/4583436.html>



