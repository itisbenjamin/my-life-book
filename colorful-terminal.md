# Mac Terminal 提升使用體驗

最近重新配置了Mac Terminal，改變了Vim的整體語法高亮配色方案，添加了樹狀圖列表，大幅提升了使用體驗。"

## Solarized

先從整體配色方案開始，用的是Solarized。

![](/img/blog/solarized-yinyang.png)

`$ git clone git://github.com/altercation/solarized.git`

首先在`osx-terminal.app-colors-solarized`文件夾中安裝Terminal整體配色方案，有兩個README。選擇自己喜歡的配色方案後設置為default。

接下來在`vim-colors-solarized`文件夾中將`autoload`和`colors`兩個文件夾中的內容移動到`~/.vim`中相對應的位置，這裡完成的事Terminal中Vim的配色方案設置。

**重要：如果選擇的是`xterm-256color`中的配色方案，在這一步中一定要閱讀`doc`文件夾中的`solarized.txt`，裡面有`.vimrc`的參數設置。**

最後在`.vimrc`的配置中添加：

{% highlight html %}
syntax enable
set background=dark
colorscheme solarized
{% endhighlight %}

具體更多配置方案可以參見solarized的README。

## Pathogen

在安裝插件之前，先安裝一個管理插件的插件，否則`.vim`目錄管理起來會比較混亂。

![](/img/blog/pathogen.png)

`$ git clone git://github.com/tpope/vim-pathogen.git`

Pathogen會在`.vim`目錄下通過`bundle`進行管理，這樣`.vim`文件夾中一般只會有`autoload`, `bundle`, `doc`這三個文件，管理起來比較方便，尤其是我這種懶惰的插件重度依賴者。

`$ git clone`命令完成後，在`.vim`文件夾下建立autoload和bundle目錄，將`pathogen.vim`文件移動到`autoload`目錄下。

最後在`.vimrc`中配置：

`call pathogen#infect()`

## NERD Tree

這是一個在Vim中要比樹狀圖顯示目錄更方便的目錄插件。

![](/img/blog/nerdtree.png)

`$ git clone git://github.com/scrooloose/nerdtree.git`

將`nerdtree`文件移動到`bundle`目錄下。

最後可以在`.vimrc`中配置快捷鍵，NERD Tree的喚出命令是`:NERDTree`。

## Coreutils

如果對文件列表高亮要求不是很高，可以在`.bash_profile`中設置`ls -G`的`alias`，我用的是Coreutils插件來實現這一點。

{% highlight shell %}
$ brew install coreutils
$ gdircolors --print-database > ~/.dir_colors
{% endhighlight %}

最後配置`.bash_profile`

{% highlight shell %}
if brew list | grep coreutils > /dev/null ; then
  PATH="$(brew --prefix coreutils)/libexec/gnubin:$PATH"
  alias ls='ls -F --show-control-chars --color=auto'
  eval `gdircolors -b $HOME/.dir_colors`
fi
{% endhighlight %}

## Powerline

這個插件單純追求使用美感，用在Vim下底部顯示狀態欄。具體效果見上方兩張Terminal的底部狀態欄。

`$ git clone git://github.com/Lokaltog/vim-powerline.git`

將`vim-powerline`文件移動到`bundle`目錄下。

最後在`.vimrc`中進行配置：

{% highlight html %}
set guifont=PoerlineSymbols\for\Powerline
set nocompatible
set t_Co=256
let g:Powerline_symbols = 'fancy'
{% endhighlight %}

## .vimrc

這裡專門說一下`.vimrc`文件的配置。

**自動插入文件描述及題頭**

新建`.c`, `.h`, `.sh`, `.java`文件時自動插入描述的配置方法。

{% highlight shell %}
autocmd BufNewFile *.cpp,*.[ch],*.sh,*.java exec ":call SetTitle()"

func SetTitle()

if &filetype == 'sh'

	call setline(1,"\##################")

	call append(line("."), "\# File Name: ".expand("%"))

	call append(line(".")+1, "\# Author: Author")

	call append(line(".")+2, "\# mail: email address")

	call append(line(".")+3, "\# Created Time: ".strftime("%c"))

	call append(line(".")+4, "\###################")

	call append(line(".")+5, "\#!/bin/bash")

	call append(line(".")+6, "")

else

	call setline(1, "/*****************")

	call append(line("."), "	> File Name: ".expand("%"))

	call append(line(".")+1, "	> Author: Author")

	call append(line(".")+2, "	> Mail: email address")

	call append(line(".")+3, "	> Created Time: ".strftime("%c"))

	call append(line(".")+4, " ******************/")

	call append(line(".")+5, "")

endif
{% endhighlight %}

下面是自動插入題頭的配置：

{% highlight shell %}
if &filetype == 'cpp'

	call append(line(".")+6, "#include<iostream>")

	call append(line(".")+7, "using namespace std;")

	call append(line(".")+8, "")

endif

if &filetype == 'c'

	call append(line(".")+6, "#include<stdio.h>")

	call append(line(".")+7, "")

endif

autocmd BufNewFile * normal G

endfunc
{% endhighlight %}

可以根據自己的需要進行添改。

**快捷鍵設置**

對於鍵盤命令，用NERDTree舉例：

`map <C-T> :NERDTree <CR>`

這條配置的意思就是將`:NERDTree`命令設置為`<C-T>`後回車。可以根據這條配置設置其他的命令快捷鍵。

**編譯運行**

下面是C，C++自動編譯運行快捷鍵配置。

{% highlight shell %}
map <F5> :call CompileRunGcc()<CR>

func! CompileRunGcc()

	exec "w"

	if &filetype == 'c'

		exec "!g++ % -o %<"

		exec "! ./%<"

	elseif &filetype == 'cpp'

		exec "!g++ % -o %<"

		exec "! ./%<"

	elseif &filetype == 'java'

		exec "!javac %"

		exec "!java %<"

	elseif &filetype == 'sh'

		:!./%

	endif

endfunc
{% endhighlight %}
	
---

內容參考：    

<http://www.cnblogs.com/ma6174/archive/2011/12/10/2283393.html>  
<http://www.cnblogs.com/chijianqiang/archive/2012/11/06/vim-3.html>    
<http://linfan.info/blog/2012/02/27/colorful-terminal-in-mac/>

