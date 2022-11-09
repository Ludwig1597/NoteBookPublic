> 2022.11.7

# vim入门

## vim快捷键

### 01 进入/退出插入模式

#### 进入

1.  a append after current char
2.  A append after current line
3.  i insert before current char
4.  I insert before current line
5.  o open a line below
6.  O open a line above

#### 退出

1.  :w 保存
2.  :wq 保存并退出
3.  :qa 退出所有窗口

### 02 快速纠错

痛点：退格键太远，用起来不方便，我们可以抛弃退格键

需要先进入编辑模式或者在命令行中使用：

1.  ctrl+h 删除前一个字符
2.  ctrl+w 删除前一个单词
3.  ctrl+u 删除当前行到光标位置的所有字符

只可以在终端命令行中使用  
4. ctrl+a 光标快速移动到开头  
5. ctrl+e 光标快速移动到结尾  
6. ctrl+b 光标往前移  
7. ctrl+f 光标往后移

### 03 快速切换insert和normal模式

痛点：Esc按起来不方便，不方便切换到normal模式

-   ctrl+c 快速切到normal模式，但有可能会中断某些快捷键
-   ctrl+[ 快速切到normal模式
-   gi 在normal模式下快速跳转到最后一次编辑的地方并进入插入模式

### 04 vim快速移动大法

#### 左 下 上 右

反人类：hjkl  
坚持使用几天，就可以熟练。

#### 在单词之间飞舞

-   w 移动到下一个word开头
-   W 移动到下一个WORD开头
-   e 移动到下一个word尾部
-   E 移动到下一个WORD尾部
-   b 移动到上一个word开头
-   B 移动到上一个WORD开头

> 小写word指得是以非空白符分割的单词，大小WORD以空白符分割的单词

#### 行间搜索移动

同一行快速移动的方式其实是搜索一个字符并且移动到该字符。

-   f{char} 可以快速移动到该行char字符上，如：fe 快速移动到e字符上（find）
-   t{char} 移动到char的前一个字符上，如：te（until）
-   ; 继续搜该行下一个
-   ，继续搜该行上一个
-   F{char} 反过来搜前面的字符

#### vim的水平移动

-   0 快速移动到行首第一个字符
-   ^ 移动到该行第一个非空白字符
-   $ 移动到行尾
-   g_ 移动到行尾非空白字符

> 记住0 移动到行首，$移动到行尾就可以了。

-   0w 快速移动到该行第一个非空白字符上

> :help ( 可以查询命令的用法

#### vim页面移动

-   gg 快速移动到文件开头
-   G 快速移动到文件结尾
-   H 快速跳转到屏幕的开头（Head）
-   M 快速跳转到屏幕的中间（Middle）
-   L 快速跳转到屏幕的结尾（Lower）
-   ctrl+u 上翻页（upward）
-   ctrl+f 下翻页（forward）
-   ctrl+e 屏幕上移动一行
-   zz 把屏幕置为中间
-   ctrl+o 快速返回

> vim的normal模式提供了强大的命令来移动。

学习vim，让写代码就像弹钢琴，让别人眼睛的速度都跟不上你操作的速度。

### 05 vim快速增删改查

#### 增加

进入插入模式编辑文本。aio/AIO

#### 删除

normal模式下：

-   x 快速删除一个字符
-   dw 删除一个单词（delete a word）
-   daw 删除一个单词和旁边的空格（delete around word）
-   diw 删除一个单词不删除空格
-   dd 删除当前行
-   dt) 删除括号里的内容（delete to )）
-   dt" 删除到双引号
-   d$ 删除到行尾
-   d0 删除到开头
-   x和d可以搭配数字来执行多次
    -   2dd 删除两行
    -   4x 删除四个字符

> vim中 数字+命令 可以用于执行多次命令

可以搭配visual模式行选或块选快速删除。

#### 修改

相比删除，更常用修改。一般是删除之后改成我们希望的文本。

-   r normal模式下使用r可以替换一个字符（replace）
    -   ra 把光标所指字符改成a
-   R 直接开始向下替换
-   c 配合文本对象，快速进行修改（change）
    -   cw 删除当前单词并进入插入模式
    -   ct" 删除到双引号并进入插入模式
-   s 删除当前字符并进入插如模式（substitute）
-   4s 删除4个字符并进入插如模式
-   S 整行删除，并进入插如模式

#### 查询

-   / 进行前向搜索
-   ? 进行反向搜索
-   n 跳转到下一个匹配
-   N 跳转到上一个匹配
-   `*` 光标在单词上，使用*号，进行当前单词的前向匹配，找到相同的单词（向下）
-   `#` 进行当前单词的后向匹配（向上）
-   :noh 搜索结束后，让高亮的字符不再高亮

#### 搜索替换

substitute命令允许我们查找并且替换掉文本，支持正则表达式

-   :[range]s/{pattern}/{string}/[flags]
    -   range表示范围，比如：10,20 表示10-20行，%表示全部
    -   pattern表示要替换的文本
    -   string是替换后的文本
    -   flags是替换的标志位
        -   g 全局范围内执行（global）
        -   c 表示确认，可以确认或者拒绝修改（confirm）
        -   n 报告匹配的次数而不替换，用来查询匹配次数（number）

如 `:% s/self/this/g` 将全局的self替换成this  
如 `:1,6 s/self/this/g` 将1-6行的self替换成this  
如 `:% s/self//n` 查看全文有多少self  
如 `:% s/\<quack\>/this/g` 使用正则表达式，精确匹配所有quack，而不会有_quack等

> 延伸：可以使用插件批量搜索替换多个文件中的匹配

### 06 vim多文件操作

Buffer、Window、Tab

-   Buffer：是指打开的一个文件的内存缓冲区
-   Window：窗口是指Buffer可视化的分割区域
-   Tab：Tab可以组织窗口为一个工作区

#### Buffer

-   vim打开一个文件后会加载文件内容到缓冲区
-   之后的修改都会针对内存中的缓冲区，并不会直接保存到文件
-   直到我们执行:w（write）的时候才会把修改内容写入到文件里

如何在buffer之间切换？

-   `:ls` 会列举当前缓冲区，然后使用`:b n`跳转到第n个缓冲区
-   :bp 向前跳（buffer previous）
-   :bnect 向后跳
-   :bfirst 跳到第一个
-   :bl 跳到最后一个（buffer last）
-   :b buffer_name/buffer_number 加上tab补全来跳转，如 :b1 跳到第一个缓冲区
-   :e 文件名 再打开一个缓冲区

#### 窗口

窗口是可视化的分割区域。  
一个缓冲区可以分割成多个窗口，每个窗口也可以打开不同缓冲区

-   ctrl+w s/:sv 水平分割
-   ctrl+w v/:vs 垂直分割(w是window的意思)

每个窗口可以继续被无限分割（看屏幕是否足够大）  
可以在不同的窗口用:e 文件名 打开不同的buffer  
不同窗口编辑同一个buffer，都会生效，因为编写的都是同一块内存里的内容

-   ctrl+w H 将光标所在位置的窗口移到左边
    
-   ctrl+w J 将光标所在位置的窗口移到下边
    
-   ctrl+w K 将光标所在位置的窗口移到上边
    
-   ctrl+w L 将光标所在位置的窗口移到右边
    
-   ctrl+w = 使所有窗口等宽、等高
    
-   ctrl+w _ 最大化活动窗口的高度
    
-   ctrl+w | 最大化活动窗口的宽度
    
-   [N]ctrl+w _ 把活动窗口的高度设置为N行，如40ctrl+w _
    
-   [N]ctrl+w | 把活动窗口的宽度设置为N列
    

#### Tab（标签页）

标签页用于将窗口分组。Tab是可以容纳一系列窗口的容器

vim的tab和其他编辑器不太一样，可以想象成Linux的虚拟桌面  
比如一个Tab全用来编辑python文件，一个tab全是html文件  
相比窗口，tab一般用的比较少，tab太多管理起来也比较麻烦

-   :tabnew 文件名 在新的标签页中打开文件
-   ft 在nerdtree中可以在光标选中的文件目录下新建标签页
-   :tabe[dit] {filename} 在新标签页中打开文件
-   ctrl+w T 把当前窗口移到一个新的标签页中
-   :tabc[lose] 关闭当前标签页及其中的所有窗口
-   :tabo[nly] 只保留活动标签页，关闭所有其他标签页

Tab标签页切换操作如下：

命令模式下：

-   :tabn[ext]{N} 切换到编号为{N}的标签页
-   :tabn[ext] 切换到下一个标签页
-   :tabp[revious] 切换到上一个标签页

normal模式下

-   {N}gt 切换到编号为{N}的标签页
-   gt 切换到下一个标签页
-   gT 切换到上一个标签页
-   ft 新建一个空的tab标签页

> 标签页一般建立两个就好，太多不好操作

> Note: 后面会配合ctrlp插件和nerdtree快速操作多个文件

### 07 vim的text object

#### 什么是Text Object(文本对象)

vim里文本也有对象的概念，比如一个单词，一段句子，一个段落  
很多其他编辑器经常只能操作单个字符来修改文本，比较低效，但vim删除一个单词只要dw  
通过操作文本对象来修改要比只操作单个字符高效

#### 如何操作文本对象

-   [number][text object]
    -   数字表示操作几次
    -   command表示操作命令,如d(delete),c(change),y(yank)复制
    -   text object表示文本对象,如单词w,句子s,段落p

#### 示例1

iw表示inner word。如果键入`viw`命令，那么首先v将进入选择模式（visual模式），然后iw将选中当前单词。  
aw表示around word。它不仅会选中当前单词，还会包含当前单词之后的空格。  
以下用[]表示作用范围：

-   iw This is a ...[test]... sentence.
    
-   aw This is a ...[test ]sentence.
    
-   iW This is a [...test...] sentence.
    
-   aW This is a [...test... ]sentence.
    
-   is ...sentence. [This is a sentence.] This...
    
-   as ...sentence. [This is a sentence. ]This...
    
-   ip [This is a [paragraph.It](http://paragraph.it/) has two sentences.]
    
    The next.  
    End of previous paragraph.
    
-   ap [This is a [paragraph.It](http://paragraph.it/) has two sentences.
    
    ]The next.  
    End of previous paragraph.
    

#### 练习1

This is a "word".

-   删除前面三个单词包括空格：0w3dw（0w先定位到第一个单词起始位置，3dw删除三个单词）
-   删除前面三个单词不包括空格：0w3diw
-   删除引号里的word换成hello: fwcw（fw先定位到word的起始位置，然后用cw，删除word并进入插入模式）

#### 示例2

-   i( or i) 1*([ 2 + 3 ]) 不包括括号 用于函数参数定义时
-   a( or a) 1*[( 2 + 3 )] 包括括号
-   i< or i> The <[tag]>
-   a< or a> The []
-   i{ or i} int main(){[return 0]} 可用于选择一个代码段
-   a{ or a} int main()[{return 0}]
-   i[ or i] some [code block](https://file+.vscode-resource.vscode-cdn.net/c:/Users/jx77.sun/Desktop/%E5%B7%A5%E4%BD%9C%E6%95%B4%E7%90%86/02%20Linux%E7%9B%B8%E5%85%B3/code_block.md) 可用写json时
-   a[ or a] some [code block](https://file+.vscode-resource.vscode-cdn.net/c:/Users/jx77.sun/Desktop/%E5%B7%A5%E4%BD%9C%E6%95%B4%E7%90%86/02%20Linux%E7%9B%B8%E5%85%B3/code_block.md)
-   i" The "[best]" 可用于打印log
-   a" The ["best"]
-   i`The`[best]` 可用于markdown文档
-   a`The [`best`]

#### 练习2

_INFO("this is a test");

-   删除双引号里的内容：f"vi"x
-   更改双引号里的内容：f"ci" (删除并进入插入模式)

map = {  
"name" : "j".  
"age" : 13  
}

-   快速修改这个map：ci"

> 文本对象最常搭配d(delete)、c(change)、v(visual)、y(yank)复制使用

> 我们需要拜托低效的字符操作，使用文本对象提高效率

### 08 vim命令模式分屏

#### 分屏

-   `:vs` 将当前文件垂直分屏(vertical split)
-   `:vs [file]` 创建新文件并垂直分屏
-   `:sv`/`:sp` 水平分屏
-   `:sv [file]` 创建新文件并水平分屏

#### 分屏间光标移动

-   `ctrl+w h` 切换到左边窗口
-   `ctrl+w j` 切换到下边窗口
-   `ctrl+w k` 切换到上班窗口
-   `ctrl+w l` 切换到右边窗口
-   `ctrl+w w` 在窗口之间循环切换

#### 分屏移动

-   `ctrl+w H` 将当前分屏移到最左边
-   `ctrl+w J` 将当前分屏移到最下边，并拓展到整个屏幕宽度
-   `ctrl+w K` 将当前分屏移到最上边，并拓展到整个屏幕宽度
-   `ctrl+w L` 将当前分屏移到最右边

#### 关闭分屏

-   `ctrl+w c` 关闭当前子屏
-   `:hide` 关闭当前窗口
-   `:only` 只保留当前窗口，关闭其他窗口
-   `:qall` 关闭所有窗口
-   `:wall` 保存所有修改过得窗口

### 09 vim复制粘贴和寄存器的使用

#### normal模式下的复制粘贴

-   `y` 复制（yank）
-   `d` 剪切（delete）
-   `p` 粘贴（put）

> 我们可以用v命令选中所要复制的地方，然后使用y复制使用p粘贴

此外配合文本对象使用：

-   `yiw` 复制一个单词
-   `yy` 复制一行

#### insert模式下的复制粘贴

之前我们用鼠标进行选中，然后用ctrl+v或cmd+v进行粘贴。  
但是vim中粘贴代码有一个坑。如果设置了autoindent，粘贴python代码会导致缩紧错乱。  
这个时候需要使用`:set paste`和`:set nopaste`解决。

#### 什么是vim的寄存器

一个问题：vim在normal模式下复制/剪切的内容去了哪里？  
vim里操作的是寄存器而不是系统剪切板。  
默认我们使用d删除或者y复制的内容都放到了"无名寄存器"中。

小tip: `xp`可以调换两字符。比如self打成了sefl时可以使用。

#### 深入寄存器

vim不使用单一剪贴板进行剪贴，复制和粘贴，而是使用多组寄存器。

-   `"{register name}` 指定寄存器，如：`"a` 使用a寄存器  
    如果不指定，则使用无名寄存器。
-   `"ayiw` 复制一个单词到寄存器a中
-   `"bdd` 删除当前行保存到寄存器b中
-   `:reg a` 查看a寄存器里的内容
-   `"ap` 使用a寄存器里的内容进行粘贴

> a-z每个字母都能当作寄存器来使用。

还有一些其他寄存器：

-   `"0` 复制专用寄存器，使用y复制文本同时会被拷复制寄存器0
-   `"+` 系统剪切板，使可以在别处进行粘贴，也可以将别处粘贴进来
-   `"%` 当前文件名
-   `".` 上次插入的文本
-   `:set clipboard=unnamed` 可以直接复制粘贴系统剪贴板的内容  
    该选项可以放到.vimrc中

insert模式中：

-   `ctrl+R` 打出双引号
-   `+` 粘贴系统剪切板里内容

normal模式中:

-   `"+p` 粘贴系统剪切板里的内容

### 10 vim宏（macro）

一个需求：如果要给多行url链接加上双引号，应该怎么做？

https://code.sec.samsung.net/confluence/pages/viewpage.action?spaceKey=SVACEGUIDEC&title=SIGNED_TO_BIGGER_UNSIGNED  
https://code.sec.samsung.net/codegrok/
https://defcon.sec.samsung.net/package/list?name=Alsa&platform=TIZEN_MAIN&size=10
https://platz.sec.samsung.net/cpp
http://it4u.sec.samsung.net

#### 什么是vim宏

宏可以看成是一系列命令的集合  
我们可以使用宏去『录制』一系列操作，然后用于『回放』  
宏可以非常方便地把一系列命令用在多行文本上

#### 如何使用宏

宏的使用分为录制和回放，在normal模式下使用：

-   `q` 开始录制和结束录制
-   `q{register}` 选择录制要保存到的寄存器，把录制的命令保存其中  
    如：`qa` 将命令保存到a寄存器中
-   `@{register}` 回放寄存器中保存的一系列命令

#### 用宏解决刚才的问题

先给一行加上双引号，然后再回放到其他所有行：

-   `qa` 开始录制
    
-   `0i"esc` 0进入该行开头，i进入编辑模式，输入"，esc退出编辑模式
    
-   `g_a"esc` g_到该行最后一个非空白字符，a进入编辑模式，输入"，esc退出编辑模式
    
-   `q` 结束录制
    
-   `VG` V进入visual模式选中该行，G一直选中到行尾
    
-   `:normal @a` :在visual模式下进入命令模式,normal表示使用normal模式命令，@a回放
    

对于类似批量操作都可以使用宏。

其实还有其他方法可以执行此批量操作，比如：

-   `ggVG` 全选
-   `:normal I"enter` 进入命令行模式，执行normal命令，I是在该行前进行插入，插入",回车
-   `:ctrl p` 进入命令行模式，ctrl p用于执行上一个命令
-   `backspace backspace A"enter` 删除I" 执行A在行尾插入"

### 11 vim补全大法

补全是根据当前环境上下文由编辑器去猜我们想输入的东西。  
比如补全一个单词、文件名、或者代码中的函数名，变量名等。  
vim中提供了多种补全功能，还可以由插件拓展功能实现代码补全。

-   `ctrl+n` 补全普通关键字  
    如，c++的普通关键字有：main、cout、endl、include等。  
    这个最常用。
-   `ctrl+x ctrl+n` 补全当前缓冲区关键字
-   `ctrl+x ctrl+i` 包含文件关键字
-   `ctrl+x ctrl+]` 标签文件关键字
-   `ctrl+x ctrl+k` 字典查找
-   `ctrl+x ctrl+l` 整行补全
-   `ctrl+x ctrl+f` 文件名补全
-   `ctrl+x ctrl+o` 全能（Omni）补全

#### 常见的三种补全类型

-   `ctrl+n`和`ctrl+p` 补全单词，n表示next，p表示previous上一个
-   `ctrl+x`和`ctrl+f` 补全当前文件夹下文件名
-   `ctrl+x`和`ctrl+o` 全能补全，需要开启文件类型检查，安装插件

> 目前匹配都是基于文本匹配的，插件可以实现代码补全

### 12 vim更换配色

-   `:colorscheme` 显示当前的主题配色，默认是default
-   `:colorscheme ctrl+d` 可以显示当前所有配色
-   `:colorscheme 配色名` 修改配色，可以使用tab键切换或补全

默认的配色没有喜欢的可以上github：[https://github.com/flazz/vim-colorschemes](https://github.com/flazz/vim-colorschemes)  
安装之后，就有大量的主题可以更换了。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1ODY5NTIwN119
-->