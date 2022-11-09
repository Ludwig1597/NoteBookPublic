> 2022.11.2

# vim简单配置

使用vim的目的，是为了实现纯键盘编辑。

## vim模式

-   normal模式：默认模式
    -   普通模式下，可以进行各种命令操作和移动
    -   大部分情况下，我们是在浏览而不是在编辑，所以vim默认是normal模式
-   insert模式：编辑模式
-   command模式：normal模式下输入:之后执行命令
    -   比如退出保存，:wq
    -   比如全局替换：:% s/java/python/g 将全局的java替换成python
-   visual模式：一般用来块状选择文本
    -   normal模式下使用v进入visual选择
    -   V 整行选中
    -   ctrl+v 进行块状选择
    -   块状选中文本后，可以用d删除，y复制，p粘贴

## vim简单配置

    sjx@Samsung:~$ cat .vimrc
    set nu "显示行号
    set shiftwidth=4 "设置缩进的空格数为4
    set tabstop=4 "设置软制表符宽度为4
    set autoindent "设置自动缩进
    set cindent "使用C/C++语言的自动缩进方式
    set showmatch "光标遇到圆括号、方括号、大括号时，自动高亮对应另一个括号
    set ruler "在状态栏显示光标的当前位置（位于哪一行、哪一列）
    set statusline=%f\ -\ FileType=%y "设置状态栏
    set hlsearch "设置高亮显示搜素字符串
    set incsearch "设置增亮搜索，边搜索边高亮
    set t_Co=256 "启动256色
    syntax on "高亮显示
    syntax enable
    colorscheme darkblue "设置主题色为darkblue


sjx@Samsung:~$

### 修改colorscheme

最喜欢的主题是darkblue，但是，底下的状态栏，灰色和亮蓝色实在看不清。故作修改。

cd /usr/share/vim/vim81/colors/
sudo cp darkblue.vim darkblueTest.vim
sudo chown -R sjx darkblueTest.vim
vim darkblueTest.vim

将第35行：hi StatusLine guifg=blue guibg=darkgray gui=none ctermfg=blue ctermbg=gray term=none cterm=none  
的ctermfg=blue改成 ---> ctermfg=56 (紫色)

终端颜色表参考：[https://www.ditig.com/256-colors-cheat-sheet](https://www.ditig.com/256-colors-cheat-sheet)

状态栏看不清，error msg也看不清。  
第18行，也做修改。  
18 hi ErrorMsg guifg=#ffffff guibg=#287eff ctermfg=56 ctermbg=lightblue
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQwMzEyODUwXX0=
-->

