# Markdown Grammar"

Markdown語法總結。

## 標題

Markdown中共有六個字符大小的標題可以使用，分別用`#`的個數來予以區分。也可以在文字下部標出`=`或`-`來實現。

`# H1. Heading`

# H1. Heading

`## H2. Heading`

## H2. Heading

`### H3. Heading`

### H3. Heading

`#### H4. Heading`

#### H4. Heading

`##### H5. Heading`

##### H5. Heading

`###### H6. Heading`

###### H6. Heading


## 字體

Markdown中有三種可以變化的字體，同時有兩種實現方式。

### 斜體：

`*My Name*`

*My Name*

`_My Name_`

_My Name_

### 黑體：

`**My Name**`

**My Name**

`__My Name__`

__My Name__

### 黑斜體：

`***My Name***`

***My Name***

`___My Name___`

___My Name___

**同時支持Markdown語法內嵌**

`**My name is _My Name_**`

**My name is _My Name_**


## 序列

文字序列Markdown中分為兩種，一種是有序序列，一種是無序序列，也就是項目符號標識。

### 有序序列：

`1. 2. 3. `

1. First
2. Second
3. Third

### 無序序列：

無序序列有三種實現方式。

`* AAA`

* AAA
* BBB
* CCC

`- AAA`

- AAA
- BBB
- CCC

`+ AAA`

+ AAA
+ BBB
+ CCC

每個項目中可以包含多個段落，但段落前必須添加4個空格或1個Tab。
項目內也可以嵌入其他Markdown語法，但必須注意縮進問題。

## 引用

`> War is Peace`

`> Freedom is Slavery`

`> Ignorance is Strength`

> War is Peace

> Freedom is Slavery

> Ignorance is Strength

引用區也可內嵌Markdown其他語法。

`> * War is Peace`

`> * Freedom is Slavery`

`> * Ignorance is Stength`


> * War is Peace

> * Freedom is Slavery

> * Ignorance is Stength

## 鏈接

### 簡單鏈接

`<http://itisbenjamin.github.io>`

<http://itisbenjamin.github.io>

郵件地址也可按照這種方式直接插入，但容易造成信息洩漏。

### 文字鏈接

文字鏈接有兩種方法可以在Markdown語法中實現，一種是在全文中鏈接數目比較少的情況下：

`[Ben](www.itisbenjamin.github.io)`

[Ben](www.itisbenjamin.github.io)

而另一種是在全文鏈接數目較多的情況下，如果繼續按照第一種的方法在文中加入鏈接，代碼會顯得比較雜亂，這時候可以這樣做：

`[Something Important][1]`

然後在文章最後給出索引：

`[1]: some comments.`

這種方式被稱為參考式，這樣會顯得更加有條理一些。標注可以放在文中任何地方，同時鏈接地址也支持主機服務器文件地址。

### 鏈接描述

在鼠標懸浮連接上出現文字描述的實現方法。

`[Ben](www.itisbenjamin.github.io "Ben")`

[Ben](www.itisbenjamin.github.io "Ben")

參考式同理，只需將描述內容標注在鏈接地址後即可。無論是使用`""`、` `` `還是`()`標注描述，效果都是一樣的。

## 圖片

Markdown支持網絡圖片鏈接，也支持調用本地服務器內的圖片。

`![Codes](/img/code.png)`

![Codes](/img/code.png)

如果想要添加圖片懸浮描述，和鏈接描述添加方式一致。

`![Codes](/img/code.png "Codes")`

![Codes](/img/code.png "Codes")

在文後給出索引的方式在添加圖片時也是支持的。

## 代碼

在文中插入代碼時前後使用單反引號就可以實現。

`` `.default` ``

`.default`

整體插入一整段代碼框時，需要在代碼前加入4個空格，或1個Tab。

{% highlight html %}
<div class="post-header-container {% if page.cover %}has-cover{% endif %}" {% if page.cover %}    style="background-image: url({{ page.cover | prepend: site.baseurl }});"{% endif %}>
  <div class="scrim {% if page.cover %}has-cover{% endif %}">
    <header class="post-header">
        <h1 class="title">{{ page.title }}</h1>
        <p class="info">by <strong>{{ page.author }}</strong></p>
    </header>
    </div>
</div>
{% endhighlight %}

## 特殊符號

### 分割線

分割線有三種實現方式。

`---`

---

`***`

***

`- - - -`

- - - -

## 標注

在需要標明腳注的文字後添加`[^]`，同時在文後標明索引內容，即可實現標注。

`My name is My Name[^1].`

`[^1]: My Name is my name.`

My name is My Name[^1].

[^1]: My Name is my name.

## 刪除線

通過在文字前後添加2個波浪線來實現刪除線。

`~~There is no tree waiting for me.~~`

<del>There is no tree waiting for me.</del>

## 表格

### 最簡單的方式

也可以在代碼兩側添加外邊框，讓整體看起來更美觀整齊。表格代碼之間是否對齊並不影響輸出效果。

`A     | B     | C     | D `

`----- | ----- | ----- | -----`

`a     | b     | c     | d`


A     | B     | C     | D 
----- | ----- | ----- | -----
a     | b     | c     | d

### 文字對齊

在表格內實現文字的居中、居左、居右都由`:`的位置來標明。

`left      | center       | center       | right`
 
`:-------- | :----------: | :----------: | -----:`

`a         | b            | c            | d`


left      | center       | center       | right 
:-------- | :----------: | :----------: | -----:
a         | b            | c            | d

## 錨點

Markdown語法不支持錨點，需要通過HTML語法實現。

### 標題錨點

{% highlight html %}
[Hello World](#hello)
<h2 id="hello">Hello World</h2>
{% endhighlight %}

### 內容錨點

{% highlight html %}
<a href="#world">Explore a new world.</a>
<a name="world">This is a new world.</a>
{% endhighlight %}

*注意：錨點命名不可與頁面元素形成衝突，否則會造成難以預料的後果。*

<div class="eof"></div>


