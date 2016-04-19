



# Python 算法練習

匯總一下學習 Python 時的算法練習筆記。

> 有兩種方式構建軟件設計：一種是把軟件做得很簡單以至於明顯找不到缺陷；另一種是把它做得很複雜以至於找不到明顯的缺陷。
  — — C.A.R. Hoare
  
> 獲得人生中的成功需要的專注與堅持不懈多過天才與機會。
  — — C.W. Wendte
  
## 題頭
在Python中，題頭文件這麼寫：

```py
#!/usr/bin/python
# Filename: hello.py

print("Hello World!")
```

它被稱為組織行。

## 可執行的 Python 程序

給 Python 程序執行的許可：

```sh
$ chmod a+x hello.py
$ ./hello.py
```

因為源文件中添加了組織行指定了解釋器，因此無論將文件名及擴展名改成什麼，都不會影響執行。

### PATH 環境設置

在設置 PATH 之前，命令只能在其所在目錄執行，設置後，可以全局執行。

```sh
$ echo $PATH
/opt/mono/bin/:/usr/local/bin:/usr/bin:/usr/X11R6/bin:/home/swaroop/bin
$ cp hello.py /home/swaroop/bin/hello
$ hello
```

其中`swaroop`是系統用戶名，在配置文件中使用`PATH=$PATH:/home/swaroop/mydir`使命令可以全局使用。

## 獲取幫助

Python 自身帶有的`Python Doc`非常適合用來自我學習，配置`Python Doc`環境變量使用`env`命令：

```sh
$ env PYTHONDOCS=/usr/share/doc/python-docs-2.3.4/html/ python
```

之後在 Python 交互環境中就可以直接食用`help`命令來獲取幫助。

```sh
>>> help('sys')
```

`help`中的內容一定要帶有引號。

## 基本概念

### 字面意義上的常量

所有從字面上就可以理解其意義的符號被稱為字面意義上的常量。

```raw
5 123 'hello world' 1.45
```

這些固定不變的值都是字面意義上的常量。

### 數

* 整數：2
* 長整數：444594884
* 浮點數：3.14
* 複數：(1+2j)

### 字符串

字符的序列。

* 使用單引號：所有的空白都會照原樣保留。
* 使用雙引號：同單引號。
* 使用三引號：提示一個多行字符串，在其中可以自由地使用單引號或雙引號。
* 轉義符：`\`用來轉義字符，行末的`\`表示字符串在下一行繼續，而非開始一個新行。
* 自然字符串：字符串前綴`r`或`R`表示字符串內的字符不需要任何轉義，所有內容都直接輸出。
* Unicode 字符串：字符串前綴`u`或`U`表示字符串內可以使用 Unicode 文本，如中文。
字符串是不可變的。
* 級連字符串：如果將兩個字符串按字面意義相鄰放置，Python 會將它們自動級連，如`what is ` `your name` 會自動轉為`what is your name`。

### 變量

既可以儲存信息，又可以操作他們。

**標識符的命名**

* 第一個字符必須是字母或下劃線
* 其他字符由大小寫字母、數字、下劃線組成
* 大小寫敏感
* 不可使用連結符`-`

**數據類型**

變量可以處理不同類型的值，稱為數據類型。  
基本類型是數和字符串，也可以用類來創造自己的類型。

### 對象

在程序中用到的任何東西都稱為`對象` 。

使用變量時只需要給他們賦值，不需要聲明或定義數據類型。

### 邏輯行與物理行

邏輯行：編寫程序時所看見的，Python 假定每個物理行對應一個邏輯行。

當在一個物理行中寫多個邏輯行時，分號表示一個邏輯行的結束。  
當在多個物理行中寫同一個邏輯行時，`\`表示明確的行連接，`()`，`[]`，`{}`表示暗示的行連接。

### 縮進

邏輯行前的縮進用來決定語句的分組，同一層次的語句必須有相同的縮進，錯誤的縮進會引發錯誤。  
混合使用制表符或空格的縮進也會引發錯誤。

## 埃氏篩法篩選素數

第一種寫法：定義無限數列

```py
# !/usr/bin/python3
# Filename: Primes
def _odd_list():
    n = 1
    while True:
        n += 2
        yield n
def _not_div(n):
    return lambda x : x % n > 0
def primes():
    yield 2
    it = _odd_list()
    while True:
        n = next(it)
        yield n
        it = filter(_not_div(n), it)
for n in primes():
    if n < 100:
        print(n)
    else:
        break
```

第二種寫法：定義有限數列

```py
# !/usr/bin/python3
# Filename: Primes
def _not_div(n):
    lambda x : x % n > 0
print(2)
n = 3
it = filter(_not_div(n), range(3,1000,2))
while True:
    n = next(it)
    print(n)    
    it = filter(_not_div(n), it)
```

## 篩選回數

回數：從左到右和從右到左是一個數，如`12321`。

第一種寫法：定義無限序列

```py
# !/usr/bin/python3
# Filename: Palindrome
def _odd_list():
    n = 10
    while True:
        n += 1
        yield n
def _filter_():
    return lambda x : str(x) == str(x)[::-1]
def palindrome():
    it = filter(_filter(), _odd_list())
    while True:
        n = next(it)
        yiled n
for n in palindrome():
    if n < 1000:
        print(n)
    else:
        break
```

第二種寫法：定義有限序列

```py
# !/usr/bin/python3
# Filename: Palindrome
def _palindrome_()
    return lambda x : str(x) == str(x)[::-1]
it = filter(_palindrome_(), range(10,1000))
while True:
    n = next(it)
    print(n)
```

### 兩種寫法

當定義有限序列時必須在最後輸出時加以限制，當定義無限序列時，會以無法定義`next(it)`結束。

## 排序函數

使用`sorted`來進行排序。

```py
# !/usr/bin/python
# Filename: Sorted
L = [('Bob', 75), ('Adam', 92), ('Bart', 66), ('Lisa', 88)]
def _by_name(t):
    return t[0].lower()
def _by_score(t):
    return t[1]
L1 = sorted(L, key=_by_name)
L2 = sorted(L, key=_by_score, reverse=True)
print(L1, L2)
```

簡寫：

```py
# !/usr/bin/python3
# Filename: Sorted
L = [('Bob', 75), ('Adam', 92), ('Bart', 66), ('Lisa', 88)]
L1 = sorted(L, lambda x : x[0].lower())
L2 = sorted(L, lambda x : x[1], reverse=True)
print(L1, L2)
```

## 為函數調用輸出log

在函數調用前以及調用後都輸出 log：

```py
# !/usr/bin/python3
# Filename: log
import functools
def log(begin, end):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print('%s %s' % (begin, func.__name__))
            func()
            print('%s' % end)
        return wrapper
    return decorator
@log('being called', 'end called')
def now():
    print('something')
now()
```

使函數既支持定義 log ，又支持無定義 log：

```py
# !/usr/bin/python3
# Filename: log
import functools
def _not_callable_(text):
    def decorater(func):
        @functools.wraps(func)
        def wrapper(*args, *kw):
            print('%s %s', (text, func.__name__)
        return wrapper
    return decotrator
def _callable_(func):
    @functools.wraps(func)
    def wrapper(*args, *kw):
        print('calling: %s', func.__name__)
    return wrapper
def log(func):
    if callable(func):
        return _callable_(func)
    else:
        return _not_callable_(func)
@log
def first():
    print('something')
@log('being called')
def second():
    print('other things')
first()
second()
```

## 內建模塊

書寫格式：

```py
# !/usr/bin/env python3
# -*- coding: utf-8 -*-
' some commits '
__author__ = 'Benjamin'
import sys
def test():
    args = sys.argv
    if len(args) == 1:
        print('Hello World')
    elif len(args) == 2:
        print('Hello %s' % args[1])
    else:
        print('Wrong input')
if __name__ == '__main__':
    test()
```

其中前兩行為題頭部分，第四行為模塊的註釋，第六行是模塊作者名稱，接下來是模塊內容。
最後兩行保證此模塊只能在命令行中運行，而不適用於交互環境。

## 使用第三方庫製作圖片縮略圖

庫：PIL

```py
# !/usr/bin/env python3
# -*- coding utf-8 -*-
# Filename: Thumbnail
from PIL import Image 
import sys
im = Image.open('%s', argv[1])
print(im.format, im.size, im.mode)
im.thumbnail((500, 300))
im.save('thumbnail.png', 'PNG')
```

## 利用裝飾器 @property 來構造不可變更的函數子類

```py
# !/usr/bin/env python3
# -*- coding: utf-8 -*-
# Filename: Property

class Screen(object):
    
    @property
    def width(self):
        return self._width
    
    @width.setter
    def width(self, value):
        self._width = value

    @property
    def height(self):
        return self._height

    @height.setter
    def height(self, value):
        self._height = value

    @property
    def resolution(self):
        return self._width * self._height

s = Screen()
s.width = 1024
s.height = 768
print(s.resolution)
```

## 利用類來輸出斐波那契數列 

```py
# !/usr/bin/env python3
# -*- coding: utf-8 -*-
# Filename: Fib

class Fib(object):
    def __init__(self):
        self.a , self.b = 0, 1

    def __iter__(self):
        return self

    def __next__(self):
        self.a , self.b = self.b , self.a + self.b
        if a > 1000:
            raise StopIteration()
        return self.a

for n in Fib():
    print(n)
```


