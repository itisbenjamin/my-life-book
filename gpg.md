# PGP/GPG Command Line"

PGP/GPG加密的一些常用指令。

## 安裝

Linux系統下安裝指令：

`$ sudo pacman -S gnupg`

## 生成鑰匙對

`$ gpg --gen-key`

```sh
Please select what kind of key you want: 
(1) RSA and RSA(default)
(2) DSA and Elgamal
(3) DSA(sign only)
(4) RSA(sign only)
Your selection?
```
    
默認RSA。

```sh
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want?
```
    
默認2048位。

```sh
Please specify how long the key should e valid.
0 = key does not expire
<n> = key expires in n days
<n> w = key expires in n months
<n> y = key expires in n years
Key is valid for? (0)
```
    
默認永久有效。

```sh
Real name: 
Email address: 
Comment: 
```
    
這三行信息用以產生UID標識。

## 查看鑰匙對

<i class=""></i><strong> 查看公鑰</strong>

`$ gpg --list-keys`
    
在指令中使用UID標識時，前面必須加上"0x"。

<i class=""></i><strong> 查看私鑰</strong>

`$ gpg --list-secret-keys`

## 導出公鑰

`$ gpg -a --output --export UID`
    
UID可使用鑰匙對名稱或Email地址。

<i class=""></i><strong> 參數</strong>

* `-a`：文本輸出格式，默認二進制。

* `-output`：輸出文件名。

* `-export`： 執行輸出公鑰操作。

### 查看內容

`$ cat`
    
## 發佈公鑰

`$ gpg --keyserver key.gnupg.net --send-key ID`
    
### 參數

* `-keyserver`：指定公鑰服務器。

* `-send-key`：指定公鑰ID。

## 獲取公鑰

`$ gpg --keyserver keys.gnupg.net --search-key ID`
    
ID也可使用UID標識。

## 導入公鑰

服務器導入指令：

`$ gpg --keyserver keys.gnupg.net --recv-key UID`
    
本地導入指令：

`$ gpg --import key.public`
    
## 核對指紋並簽署

核對指令：

`$ gpg --fingerprint`
    
簽署指令：

`$ gpg --sign-key ID`
    
刪除指令：

`$ gpg --delete-keys ID`
    
## 刪除

### 公鑰

`$ gpg --delete-key ID`
    
### 私鑰

`$ gpg --delete-secret-key ID`

## 文件加密

### 加密

`$ gpg -a --output message-ciper.txt -r ID -e message.txt`
    
參數：

* `-a`：輸出文件格式。

* `-output`：輸出文件名。

* `-r`：信息接收者（recipient)公鑰ID。

* `-e`：加密（encrypt）操作。

如所加密文件為二進制，`-a`參數可省略。

### 解密

`$ gpg --output message-plain.txt -d message-ciper.txt`
    
參數：

* `-output`：輸出文件名。

* `-d`：解密（decrypt）操作。

## 數字簽名

### 方法A：生成獨立簽名文件

**簽名**

`$ gpg -a -b message.txt -u ID`
    
參數：

* `-a`：輸出文件格式。

* `-b`：以生成獨立的簽名文件的方式進行簽名。

* `-u`：指定私鑰。

**檢驗**

`$ gpg --verify message.txt.asc`
    
Good signature則通過檢驗。

### 方法B：不生成獨立簽名文件

**簽名**

`$ gpg -a --clearsign message.txt`
    
clearsign參數將簽名與原信息合併後生成一個新文件。

**檢驗**

`$ gpg --verify new.txt`
    
**提取信息**

`$ gpg --output message-original.txt -d new.txt`
    
---

<center>
<h4>「信息安全並非是讓人懷疑一切，而是讓每個人都能夠保有隱私的權利。」</h4>
</center>



