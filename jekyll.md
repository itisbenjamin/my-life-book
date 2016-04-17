# Jekyll/Liquid Grammar"

Jekyll/Liquid常用語法記錄。

## What is Jekyll

Jekyll是一個靜態網站生成器。    
通過標記語言Markdown或textile和模版引擎liquid轉換生成網頁。    
Jekyll依賴於ruby開發平台。

## 目錄結構

通過`$ jekyll new SiteName`目錄可以迅速在當前目錄下生成一個基本的Jekyll結構目錄。

{% highlight shell %}
.
|-- _config.yml
|-- _includes/
|   |-- footer.html
|   |-- head.html
|-- _layouts/
|-- _posts/
|   |-- 2016-01-01-title.markdown
|   |-- 2016-01-02-title.markdown
|-- _drafts/
|   |-- title.markdown
|-- _data/
|   |-- feed.yml
|-- _site/
|-- index.html
{% endhighlight %}

**_config.yml**

全局配置文件，其中包含網站所有基礎信息，便於需要時調用。

**_drafts**

存放未發佈的文章。

**_includes**

存放關於網站header, footer, sidebar等公共部分，便於需要時調用。

**_layouts**

存放頁面基礎配置文件，如page, post頁面第一層設置，使用html語法編寫。   
頁面設置可以多層嵌套。  

在使用第一層配置時，使用layout來指定:   

{% highlight yml %}
---
layout: page
---
{% endhighlight %}

**_posts**

存放已發佈內容，命名必須按照`Y-M-D-title.markdown`來命名。  
語法必須使用Markdown, HTML或texile。

**_data**

存放`.yml`, `yaml`, `json`, `csv`等文件。用於設置全局變量。

**_site**

Jekyll用於生成網站的文件，需要在`.gitignore`中屏蔽。

**index.html**

主頁文件。

*所有存放在根目錄下並且不以下划線開頭的文件夾中有格式的文件都會被處理成page。*

## 全局變量配置

全局配置擁有默認配置，可以手動配置需要修改的地方。

**時區**

{% highlight yml %}
# timezone: America/Argentina/San_Luis
timesone: Timesone
{% endhighlight %}

**鏈接格式**

Post中的URL格式通過`permalink`來配置。

{% highlight yml %}
# /2016/01/01/title.html
permalink: /:year/:month/:day/:title.html

# /01-01-2016/title.html
permalink: /:month-:day-:year/:title.html
{% endhighlight %}

同時也有已有配置可以直接設置。

{% highlight yml %}
# /:category/:year/:month/:day/:title.html
permalink: date

# /:category/:year/:month/:day/:title.html
permalink: pretty

# /:category/:title.html
permalink: none
{% endhighlight %}

**分頁**

文章分頁變量：`paginate`, `paginate_path`。

{% highlight yml %}
paginate: 5
paginate_path: "blog/page:num/"
{% endhighlight %}

其中`/blog/`目錄為`baseurl`目錄。`page`是字符常量，變量是`:num`分頁頁碼，自動從第二頁開始編碼。

**默認值設定**

設置`author`, `layout`等默認值。  
在設定後可以隨時通過`post`題頭覆蓋這些默認值。

{% highlight yml %}
# in _cofig.yml
defaults:
 - 
  scope:
    path: ""  # empty means all files in the project
    type: "posts"  
  values:
    layout: "post"
    author: "Ben"

  -
   scope:
    path: "project"
    type: "pages"
   values: 
     layout: "project"
{% endhighlight %}

## Jekyll模版、變量

Jekyll模版分為兩部分，頭部定義以及Liquid語法。

**頭部定義**

定義制定模版的變量，這裡的所有設置都可以覆蓋全局變量中的基礎配置。

{% highlight yml %}
---
layout: post
title: title
subtitle: subtitle
date: date
category: category
decription: description
published: true
permalink: none
---
{% endhighlight %}

所有的變量都是樹節點，連接全局變量配置根節點。

全局根節點有：  
* site: `config_yml`全局配置信息
* page: 頁面配置信息。
* content: 包含頁面子視圖，用於引入子節點內容，不能在post和page文件中使用。
* paginator: 分頁信息。

*`post`變量僅作用於`for`循環內部。*

**site 變量**

變量 | 描述
:--- | ---
`site.time`|  當前時間   
`site.pages` |  所有頁面列表  
`site.posts`| 按時間逆排序所有文章列表  
`site.related_posts`| 包含最多近期十篇文章列表  
`site.static_files` | 所有靜態文件列表  
`site.html_pages`|  所有HTML頁面列表  
`site.collections`| 自定義對象集合列表  
`site.data`|  data目錄下YAML文件數據列表  
`site.documents` |  所有Collections文檔列表  
`site.categories.Category`|  所有Category類別下文章列表  
`site.tags.Tag`|  所有Tag標籤下列表  
`site.Configuration_Data`| 其他自定義變量  

**page 變量**

變量 | 描述
:--- | ---
`page.content`	| 頁面的內容
`page.title`	| 頁面的標題
`page.excerpt`	| 未渲染的摘要
`page.url`	| 不帶域名的頁面鏈接
`page.date`	| 指定每一篇 post 的時間
`page.id`	| 每一篇 post 的唯一標示符(在RSS中非常有用)
`page.categories`	| post 隸屬的一個分類列表，可在 YAML 頭部指定
`page.tags`	| post 隸屬的一個標籤列表，可在 YAML 頭部指定
`page.path`	| 頁面的源碼地址
`page.next`	| 按時間順序排列的下一篇文章
`page.previous`	| 按時間順序排列的上一篇文章

**paginator 變量**

變量 |	描述
:--- | ---
`paginator.per_page` | 	每一頁的 post 數量
`paginator.posts`| 	當前頁面上可用的 post 列表
`paginator.total_posts`| 	所有 post 的數量
`paginator.total_pages`	| 分頁總數
`paginator.page`	| 當前頁的頁碼，或者 nil
`paginator.previous_page`	| 上一頁的頁碼，或者 nil
`paginator.previous_page_path`	| 上一頁的路徑，或者 nil
`paginator.next_page`	| 下一頁的頁碼，或者 nil
`paginator.next_page_path`	| 下一頁的路徑，或者 nil

## Liquid 語法

Liquid是Ruby的一個模版引擎庫，Jekyll中用到Liquid標記有兩種：**輸出**和**標籤**。

* Output標記：變成文本輸出，被2層成對花括號包住。  
* Tag標記：執行命令，被成對的花括號和百分號包住。

## Jekyll 輸出 Output

{% highlight ruby %}
Hello  { { name } }
Hello  { { user.name } }
Hello  { { 'Ben' } }
{% endhighlight %}

Output標記可以使用過濾器Filters對輸出內容進行簡單處理。
多個Filters間用竪線隔開，從左到右依次執行，Filter左邊總是輸入，返回值為下一個Filter的輸入或最終結果。

{% highlight ruby %}
Hello { { 'Ben' | upcase } }  # 轉換為大寫輸出
Hello Ben has { { 'Ben' | size } } letters. # 字符串長度
Hello { { '*Ben*' | markdownify | upcase } }  # 將Markdown字符串轉換成HTML大寫文本輸出
Hello { { 'now' | date: "%Y %M %D" } }  # 按照指定格式輸出當前時間
{% endhighlight %}

## 過濾器Filters

下面是常用的過濾器方法，更多API需要查閱源碼，一般主要看兩個Ruby Plugin文件：`filters.rb`（Jekyll）和`standardfilters.rb`（Liquid）。

* `date` - 將時間戳轉化為另一種格式   
* `capitalize` - 輸入字符串首字母大寫   
* `downcase` - 輸入字符串轉換為小寫  
* `upcase` - 輸入字符串轉換為大寫  
* `first` - 返回數組中第一個元素  
* `last` - 返回數組數組中最後一個元素  
* `join` - 用特定的字符將數組連接成字符串輸出  
* `sort` - 對數組元素排序  
* `map` - 輸入數組元素的一個屬性作為參數，將每個元素的屬性值映射為字符串  
* `size` - 返回數組或字符串的長度   
* `escape` - 將字符串轉義輸出   
* `escape_once` - 返回轉義後的HTML文本，不影響已經轉義的HTML實體  
* `strip_html` - 刪除 HTML 標籤  
* `strip_newlines` - 刪除字符串中的換行符(\n)   
* `newline_to_br` - 用HTML` <br/>` 替換換行符 \n  
* `replace` - 替換字符串中的指定內容    
* `replace_first` - 查找並替換字符串中第一處找到的目標子串   
* `remove` - 刪除字符串中的指定內容   
* `remove_first` - 查找並刪除字符串中第一處找到的目標子串    
* `truncate` - 截取指定長度的字符串，第2個參數追加到字符串的尾部    
* `truncatewords` - 截取指定單詞數量的字符串   
* `prepend` - 在字符串前面添加字符串    
* `append` - 在字符串後面追加字符串   
* `slice` - 返回字符子串指定位置開始、指定長度的子串   
* `minus` - 減法運算   
* `plus` - 加法運算   
* `times` - 乘法運算   
* `divided_by` - 除法運算  
* `split` - 根據匹配的表達式將字符串切成數組   
* `modulo` - 求模運算   

## Jekyll Tag

標籤用於模版中的執行語句。下面是目前Jekyll/Liquid標準標籤庫：

Tags | Description
:--- | ---
assign	| 為變量賦值
capture	| 用捕獲到的文本為變量賦值
case	| 條件分支語句 case…when…
comment	| 注釋語句
cycle	| 某些特定值間循環選擇，如顏色、DOM類
for	| 循環語句
if	| if/else 語句
include	| 包含另一個模版，文件在 `_includes` 目錄
raw	| 禁用範圍內的 Tag 命令，避免語法衝突
unless	| if 語句的否定語句

**Comments**

起到注釋Liquid代碼作用。

{% highlight ruby  %}
This is Benjamin. { % comment % } Comments { % endcomment % }
{% endhighlight %}

**Raw**

臨時禁止執行Jekyll Tag命令。

{% highlight ruby %}
{ % raw % }
 This is a raw line. { % includ head % } will not show.
{ % endraw % }
{% endhighlight %}

**If/Else**

條件語句，可以使用關鍵字有：`if`, `unless`, `elseif`, `else`。

**Case**

適用於條件實例很多的情況。

{% highlight ruby %}
{ % case template % }
{ % when 'label' % }
{ % when 'product' % }
{ % else % }
{ % endcase % }
{% endhighlight %}

**Cycle**

經常需要在相似的任務間選擇時，可以使用`cycle`標籤。

{% highlight ruby %}
{ % cycle 'one', 'two', 'three' % }
{ % cycle 'one', 'two', 'three' % }
{% endhighlight %}

同時可以指定循環名稱進行分組處理。

{% highlight ruby %}
{ % cycle 'group1': 'one', 'two', 'three' % }
{% endhighlight %}

**For loops**

循環遍歷數組。

{% highlight ruby %}
{ % for item in array % }
{ { item } }
{ % endfor % }
{% endhighlight %}

循環迭代Hash散列，`item[0]`是鍵，`item[1]`是值。

{% highlight ruby %}
{ % for item in hash % }
{ { item[0] } }: { { item[1] } }
{ % endfor % }
{% endhighlight %}

每個循環週期，提供下面幾個可用的變量：

{% highlight ruby %}
forloop.length  # => length of the entire for loop
forloop.index  # => index of the current iteration
forloop.index0  # => index of the current iteration (zero based)
forloop.rindex  # => how many items are still left? 
forloop.rindex0  # => how many items are still left? (zero based)
forloop.first  # => is this the first iteration? 
forloop.last  # => is this the last iteration? 
{% endhighlight %}

還有幾個屬性用來限定循環過程：

`limit:int`：限制循環迭代次數   
`offset:int`：從第n個item開始迭代   
`reversed`：反轉循環順序  

**Variable Assignment**

為變量賦值，用於輸出或其他Tag。

{% highlight ruby %}
{ % assign index = 1 % }
{ % assign name = 'freestyle' % }

{ % for t in collections.tags % }{ % if t == name % }
  Freestyle!
{ % endif % }{ % endfor % }


/ 變量是布爾類型 /

{ % assign freestyle = false % } 

{ % for t in collections.tags % }{ % if t == 'freestyle' % }
  { % assign freestyle = true % }
{ % endif % }{ % endfor % }

{ % if freestyle % }
  Freestyle!
{ % endif % }
{% endhighlight %}

`capture`允許將大量字符串合併為單個字符串並賦值給變量，而不會輸出顯示。

## 其他模版語句

**格式化時間**

{% highlight ruby %}
{ { site.time | date_to_xmlschema } }     # => 2008-11-07T13:07:54-08:00
{ { site.time | date_to_rfc822 } }        # => Mon, 07 Nov 2008 13:07:54 -0800
{ { site.time | date_to_string } }        # => 07 Nov 2008
{ { site.time | date_to_long_string } }   # => 07 November 2008
{% endhighlight %}

**代碼語法高亮**

安裝`pygments.rb`的`gem`組件和Python 2.x後，配置文件添加`highlighter:pygmnts`，就可以使用語法高亮了。

{% highlight ruby %}
{ % highlight ruby linenos % }
# some ruby codes
{ % endhighlight % }
{% endhighlight %}

*參數*  
`ruby`：指定語言  
`linenos`：顯示行號  

在給代碼著色時，需配置相對應的CSS文件。

**生成摘要**

配置文件中設定`excerpt_separator`取值，每篇post都會自動截取從開始到這個值間的內容作為這篇文的摘要`post.excerpt`使用。  
如果要禁用某篇文章的摘要，可以在該篇文章YAML頭部設定`excerpt_separator: ""`。

{% highlight html %}
{ % for post in site.posts % }
<a href="{ { post.url } }">{ { post.title } }</a>
{ { post.exceerpt | remove: 'test' } }
{ % endfor % }
{% endhighlight %}

**刪除HTML標籤**

這個在摘要作為`head`標籤里的`meta="description"`內容輸出時很有用。

{% highlight ruby %}
{ { post.excerpt | strp_html } }
{% endhighlight %}

**刪除指定文本**

過濾器`remove`可以刪除變量中的指定內容。

{% highlight ruby %}
{ { post.url | remove: 'http' } }
{% endhighlight %}

**CGI Escape**

通常用於將URL中的特殊字符轉義為`%xx`形式。

{% highlight ruby %}
{ { "foo.bar;baz?" | cgi_escape } }  # => foo%2Cbar%3Bbaz%3F
{% endhighlight %}

**排序**

{% highlight ruby %}
# Sort an array. Optional arguments for hashes:
#   1. property name
#   2. nils order ('first' or 'last')

{ { site.pages | sort: 'title', 'last' } }
{% endhighlight %}

## Assets 樣式文件

Jekyll支持Sass和CoffeeScript，通過新建`.sass`, `.scss`, `.coffee`格式文件，並在開頭添加一堆`---`來使用這個功能。



