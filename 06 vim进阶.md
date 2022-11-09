> 2022.11.9

# vim进阶

## vim配置

.vimrc提供了一种持久化配置的方式，让我们自定义配置。

### 常用配置

set nu "显示行号
set shiftwidth=4 "设置缩进的空格数为4
set tabstop=4 "设置软制表符宽度为4
set autoindent "设置自动缩进
set cindent "使用C/C++语言的自动缩进方式
set showmatch "光标遇到圆括号、方括号、大括号时，自动高亮对应另一个括号
set ruler "在状态栏显示光标的当前位置（位于哪一行、哪一列）
set statusline=%f\ -\ FileType=%y "设置状态栏
set hlsearch "设置高亮显示搜素字符串（highlight search）
set incsearch "设置增亮搜索，边搜索边高亮
set t_Co=256 "启动256色
syntax on "高亮显示
syntax enable
colorscheme darkblue "设置主题色为darkblue

可以新增的：

set foldmethod=indent "设置折叠方式

-   `:h option-list` 可以看到所有设置的选项

### vim中的映射

#### vim映射初认识

-   `let mapleader=","` 设置leader键，常用逗号或空格
-   `inoremap <leader>w <Esc>:w<cr>` 在insert模式下，使用`,w`提代退出冒号保存
-   `inoremap jj <Esc>` 在insert模式下，使用`jj`提代esc键进入normal模式

> 为什么是jj因为英文中几乎没有两个j连起来的英文单词，所以几乎不会产生冲突

使用ctrl+h/j/k/l代替ctrl+w h/j/k/l去切换窗口

-   `noremap <C-h> <C-w>h` 向左切换窗口
-   `noremap <C-j> <C-w>j` 向下切换窗口
-   `noremap <C-k> <C-w>k` 向上切换窗口
-   `noremap <C-l> <C-w>l` 向右切换窗口

4.  ZZ 退出当前窗口

> 可以参考github上vim-go教程学习vimrc文件配置

## vim插件下载

### 00 安装vim插件管理器

首先，使用vim-plug插件管理器安装vim插件。

[https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug)

使用命令：curl -fLo ~/.vim/autoload/plug.vim --create-dirs [https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim)

第一个报错：Command 'curl' not found, but can be installed with:  
解决：sudo apt install curl

第二个报错：sjx@Samsung:~$ curl -fLo ~/.vim/autoload/plug.vim --create-dirs [https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim)  
% Total % Received % Xferd Average Speed Time Time Time Current  
Dload Upload Total Spent Left Speed  
0 0 0 0 0 0 0 0 --:--:-- 0:01:32 --:--:-- 0^C  
超时。  
解决：使用curl命令需要配置代理：

vim .curlrc  
cat ~/.curlrc  
proxy = "[http://109.123.97.11:8080](http://109.123.97.11:8080/)"  
insecure

sync

下载成功：

sjx@Samsung:~$ curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 83129  100 83129    0     0   121k      0 --:--:-- --:--:-- --:--:--  121k
sjx@Samsung:~$

### 01 vim-startify

一个好用的vim开屏插件。

[https://github.com/mhinz/vim-startify](https://github.com/mhinz/vim-startify)

1.  vim .vimrc,增加该插件名称

call plug#begin('~/.vim/plugged')
Plug 'mhinz/vim-startify'
call plug#end()

2.  保存然后source .vimrc

:w
:source ~/.vimrc

3.  执行:PlugInstall

:PlugInstall

报错：connect to [github.com](http://github.com/) port 443: Connection timed out  
解决：

1.  打开 [https://github.com.ipaddress.com/](https://github.com.ipaddress.com/)
2.  复制IP Address
3.  sudo vim /etc/hosts  
    在末尾添加：140.82.114.4 [github.com](http://github.com/)
4.  source /etc/hosts
5.  重新下载，成功

Updated. Elapsed time: 0.015813 sec.                                                
[=]    

- Finishing ... Done!                                                          
- vim-startify: Already installed    

### 02 nerdtree-vim文件目录和搜索插件

使用nerdtree插件进行文件目录树管理。  
解决跳转文件得问题。

[https://github.com/preservim/nerdtree](https://github.com/preservim/nerdtree)

Plug 'preservim/nerdtree'

1.  :NERDTree命令用于打开目录
2.  vim .vimrc 添加快捷键

> 我们可以通过vimscript脚本语言实现更多vim的控制，开发自己的插件
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYwNzc1MjU0Ml19
-->