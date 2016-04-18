# Chmod Command Line

一開始做運維和系統管理的時候，就會遇到 `chmod` 命令，然而剛開始修改文件權限的時候總是要去查詢權限代碼（就是那幾個數字），後來發現不能這麼傻下去，不明白原理實在太痛苦，一定有更好的辦法，然後我就仔細的研究了一下 `chmod` 這個命令，為了以後查詢起來方便（已經忘了好幾次了），現在做一個總結。

## 分組權限

在 Linux 中，權限是分組賦予的，一般有三組：

* 所有者權限：文件創始者，與 root 權限相當，擁有對文件的讀、寫和執行權
* 同組權限：所有者所在的用戶組其他成員的權限
* 其他用戶權限：除所有者及其所在用戶組成員的其他用戶

在運行 `ls -l` 命令後所對應的三組權限說明，即對應上面這三組用戶。

## 訪問權限

Linux 系統中訪問權限有三種，分別是可讀、可寫、可運營權限。

* `r`：可讀權限，讀取文件或文件夾中的內容
* `w`：可寫權限，對文件進行編輯修改，寫入內容到目錄中
* 'x`：可執行權限，將文件作為執行文件執行，進入目錄並以目錄名稱作為路徑名訪問它所包含的子目錄和文件

**說明**

1. 對文件擁有 `w` 權限不可刪除文件，必須對文件所在目錄擁有 `w` 權限
2. 對目錄擁有 `w` 權限不能進入目錄，必須擁有 `x` 執行權限
3. 對目錄有 `x` 執行權，必須知道目錄名稱同時擁有 `r` 可讀權才能訪問目錄
4. 對目錄同時擁有 `rx` 權限才能使用 `ls` 命令列出目錄下文件
5. 對目錄擁有 `w` 可寫權限，可以對目錄下所有文件以及子目錄進行創建、修改、刪除

## 字母設定法

```sh
$ chmod [option] [mode] file
```

### Options

  `-c, --changes`          like verbose but report only when a change is made   在文件權限更改後再顯示更改動作  
  `-f, --silent, --quiet`  suppress most error messages   權限無法更改也不顯示錯誤信息  
  `-v, --verbose`          output a diagnostic for every file processed   輸出詳細信息   
      `--no-preserve-root`  do not treat '/' specially (the default)
      `--preserve-root`    fail to operate recursively on '/'
      `--reference=RFILE`  use RFILE's mode instead of MODE values
  `-R, --recursive`        change files and directories recursively   遞歸權限變更命令

### 對象
  
  `u`：user，文件或目錄所有者  
  `g`：group，所有者同組用戶  
  `o`：others，其他用戶  
  `a`：all，所有用戶，默認對象
  
### 操作符號
  
  `+`：增加權限  
  `-`：取消權限  
  `=`：增加某項權限後取消其他權限
  
### 權限

`r` ：可读  
`w` ：可写  
`x` ：可执行  
`X` ：只有目标文件对某些用户是可执行的或该目标文件是目录时才追加x 属性   
`s` ：在文件执行时把进程的属主或组ID置为该文件的文件属主。方式“u＋s”设置文件的用户ID位，“g＋s”设置组ID位  
`t` ：保存程序的文本到交换设备上  
`u` ：与文件属主拥有一样的权限  
`g` ：与和文件属主同组的用户拥有一样的权限  
`o` ：与其他用户拥有一样的权限  

## 數字設定法

這裡的數字指的是一個三位數，這三位數中每一個數字分別對應 User，Group，Others 三組用戶。

其中 `r` 為 4 , `w` 為 2 , `x` 為 1 , `-` 為 0。

  
  



