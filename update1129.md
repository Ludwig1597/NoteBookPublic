> 2022.11.9

  

# vim进阶

  

## 01 vim配置

  

.vimrc提供了一种持久化配置的方式，让我们自定义配置。

  

### 常用配置

  

```shell

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

```

  

可以新增的：

```shell

set foldmethod=indent "设置折叠方式

```

  

- `:h option-list` 可以看到所有设置的选项

  

### vim映射初认识

  

- `let mapleader=","` 设置leader键，常用逗号或空格

- `inoremap <leader>w <Esc>:w<cr>` 在insert模式下，使用`,w`提代退出冒号保存

- `inoremap jj <Esc>` 在insert模式下，使用`jj`提代esc键进入normal模式

  

> 为什么是jj因为英文中几乎没有两个j连起来的英文单词，所以几乎不会产生冲突

  

使用ctrl+h/j/k/l代替ctrl+w h/j/k/l去切换窗口

  

- `noremap <C-h> <C-w>h` 向左切换窗口

- `noremap <C-j> <C-w>j` 向下切换窗口

- `noremap <C-k> <C-w>k` 向上切换窗口

- `noremap <C-l> <C-w>l` 向右切换窗口

  

> 可以参考github上vim-go教程学习vimrc文件配置

  

当前我们的.vimrc文件如下所示：

```shell

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

colorscheme ron "设置主题色为darkblue

  

let mapleader=","

inoremap <leader>w <Esc>:w<cr>

inoremap jj <Esc>

noremap <C-h> <C-w>h

noremap <C-j> <C-w>j

noremap <C-k> <C-w>k

noremap <C-l> <C-w>l

```

  

## 02 vim映射

  

vim映射就是把一个操作映射到另一个操作。

用于不满现在的操作，或者设置一些方便的快捷键。

  

### 基本映射

  

基本映射指的是normal模式下的映射，

  

- `map` 使用map命令就可以实现映射。

如：`map - x` 按-就会x删除字符

如：`map <space> viw` 按空格就可以选中单词

- `unmap` 取消映射

如：`unmap -` 取消刚刚的按-就会删除字符

  

### 模式映射

  

vim常用模式normal/insert/visual模式都可以定制映射。

  

- `nmap` 定义只在normal模式下生效

- `imap` 定义只在insert模式下生效

- `vmap` 定义只在visual模式下生效

  

- `imap <C-d> <Esc>ddi` 在insert模式下使用ctrl+d删除一行

  

### 一个问题

  

`nmap - dd`

`nmap \ -`

这会递归映射。

  

*map系列命令有递归的风险。为了解决这种风险可以使用非递归映射。

  

### 非递归映射

  

vim提供了非递归映射，这些命令不会递归解释。

  

*map对应的非递归命令如下：

- `nnoremap` normal模式下（nore = no recursive）

- `inoremap` insert模式下

- `vnoremap` visual模式下

  

> 一个原则：任何时候都应该使用非递归映射，拯救自己和插件作者

  

- inoremap jj <Esc>`^ 使进入normal模式仍在当前编辑位置

  

> 可以使用:help `^ 查看命令是什么意思

  

使在insert模式和normal模式下都能使用`,w`进行保存：

- `let mapleader=","`

- `inoremap <leader>w <Esc>:w<cr>`

- `nnoremap <leader>w :w<cr>`

  

> 映射可以让vim按照我们想要的方式进行工作

> 参考书推荐：《笨方法学Vimscript》

  

## 03 vim插件

  

### 00 安装vim插件管理器vim-plug

  

首先，使用vim-plug插件管理器安装vim插件。

  

https://github.com/junegunn/vim-plug

  

使用命令：`curl -fLo ~/.vim/autoload/plug.vim --create-dirs \

https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim`

  

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

```shell

sjx@Samsung:~$ curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

% Total % Received % Xferd Average Speed Time Time Time Current

Dload Upload Total Spent Left Speed

100 83129 100 83129 0 0 121k 0 --:--:-- --:--:-- --:--:-- 121k

sjx@Samsung:~$

```

  

### 01 修改启动界面vim-startify

  

一个好用的vim开屏插件。

  

https://github.com/mhinz/vim-startify

  

1. vim .vimrc,增加该插件名称

```

call plug#begin('~/.vim/plugged')

Plug 'mhinz/vim-startify'

call plug#end()

```

2. 保存然后source .vimrc

```

:w

:source ~/.vimrc

```

3. 执行:PlugInstall

```

:PlugInstall

```

报错：connect to [github.com](http://github.com/) port 443: Connection timed out

解决：

  

1. 打开 [https://github.com.ipaddress.com/](https://github.com.ipaddress.com/)

2. 复制IP Address

3. sudo vim /etc/hosts

在末尾添加：140.82.114.4 [github.com](http://github.com/)

4. source /etc/hosts

5. 重新下载，成功

  

Updated. Elapsed time: 0.015813 sec.

[=]

  

- Finishing ... Done!

- vim-startify: Already installed

  

### 02 状态栏美化vim-airline

  

https://github.com/vim-airline/vim-airline

  

Plug 'vim-airline/vim-airline'

Plug 'vim-airline/vim-airline-themes'

  
  

### 03 增加代码缩进线条indentline

  

https://github.com/Yggdroot/indentLine

  

Plug 'Yggdroot/indentLine'

  

### 04 vim文件目录nerdtree

  

使用nerdtree插件进行文件目录树管理。

解决跳转文件得问题。

  

https://github.com/preservim/nerdtree

  

Plug 'preservim/nerdtree'

  

1. :NERDTree命令用于打开目录

2. vim .vimrc 添加快捷键

  

nnoremap <leader>f :NERDTreeFind<cr>

nnoremap <leader>t :NERDTreeToggle<cr>

  

- `,t` 打开/关闭目录树

- `,f` 从文件跳到目录树位置(查找文件位置)

- `ctrl+w p` 从目录树跳回文件位置

  

### 05 快速搜索文件-模糊搜索器ctrlp

  

https://github.com/ctrlpvim/ctrlp.vim

  

Plug 'ctrlpvim/ctrlp.vim'

  

let g:ctrlp_map = '<c-p>'

let g:ctrlp_cmd = 'CtrlP'

  

快速根据文件名查找并且打开一个文件。

  

- vim

- ctrl+p 进入

- ctrl+c 退出

- 键入想要查找的文件名

- ctrl+j/k 上下选择

- ctrl+f/b 切换模式

- 回车

- ,f 快速定位到目录树位置

  

### 06 文件内快速定位插件easymotion

  

#### vim基础移动命令回顾

  

- `w`/`e` 移动到word开头，word结尾

- `gg`/`G` 移动到文件首尾

- `0`/`$` 移动到行首位

- `f{char}` 查询字符

- `ctrl+f`/`ctrl+u` 前后翻屏

  

那么如何移动到文件里的任意位置？

  

https://github.com/easymotion/vim-easymotion

  

Plug 'easymotion/vim-easymotion'

  

nmap ss <Plug>(easymotion-s2)

使用递归映射，因为easymotion-s2也是一个映射

  

使用：

- `ss` 进入搜索

- 输入两个字符

- 然后输入想到的位置的序列号，看高亮字母是什么

  

### 07 成双成对编辑vim-surround

  

如果快速更换一对单引号为双引号，查找替换可能会比较低效。

  

https://github.com/tpope/vim-surround

  

Plug 'tpope/vim-surround'

  

该插件主要作用是在normal模式下增加，删除，修改成对内容。

  

- `ds` delete a surrounding

- `ds"` 删除一对双引号

- `cs` change a surrounding

- `cs"'` 将双引号改为单引号

- `cs(]` 将圆括号改为方括号

- `ys` you add a surrounding

增加双引号：

如：cout<<hello<<endl;需要给hello加上双引号

- `ys` 增加一个surrounding

- `iw` inner word 选中当前单词

- `"` 添加一对双引号

  
  
  

### 08 彩虹括号vim-rainbow

  

对编程语言中的括号(小括号、方括号和大括号)使用不同的颜色区分，清晰明了，可以让你很清楚的了解那些括号是一对的。

  

https://github.com/frazrepo/vim-rainbow

  

Plug 'frazrepo/vim-rainbow'

  

let g:rainbow_active = 1

  

颜色太暗，暂时卸载了，以后装要重新配置

  

### 09 多文件模糊搜索fzf与fzf.vim

  

一个问题：我们经常需要在一个代码项目中模糊搜索一些文本，而vim自带的搜索/仅可以搜索当前文件，但是项目有很多文件。

  

fzf是一个强大的命令行模糊搜索工具，fzf.vim集成到了vim里。

  

https://github.com/

  

Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }

Plug 'junegunn/fzf.vim'

  

- `:Ag [PATTERN]` 模糊搜索字符串

- `:Files [PATH]` 模糊搜索目录，这个和ctrlp快速搜索文件很像

  

输入命令后，显示ag command is not found，我们需要安装ag命令

sudo apt-get install silversearcher-ag

  

这时候我们就可以愉快用Ag命令进行多文件搜索了

  

- `ctrl+j` 下移

- `ctrl+k` 上移

  

### 10 批量搜索替换插件far.vim

  

https://github.com/brooth/far.vim

  

Plug 'brooth/far.vim'

  

使用：

- `:Far foo bar **/*.cpp` 将foo替换成bar

- `:Fardo` 开始替换

  

> tip： `vim fileA fileB -O` 可以同时打开两个文件

  

### 11 愉快浏览代码tagbar

  

tagbar的意思是代码大纲。

https://github.com/preservim/tagbar

  

打开插件描述，看到需要下载依赖ctags：

https://ctags.io/

  

`sudo apt-get install ctags`

  

- `ctags –R *` :生成ctags索引文件。ctags命令的使用的前提是在为操作的文件建立索引文件的基础上进行的。所以在用ctags对文件检索前，先在当前文件目录下执行命令,来创建索引文件。

- `ctrl+]` 查找光标所在函数或者结构体的定义处

- `ctrl+t` 跳转到查找前光标所在的位置

  

> 这个后期考虑换成`,g`和`,b`意思为go和back，还有ctrl+o,ctrl+i

  

安装tagbar插件

Plug 'preservim/tagbar'

  

`nnoremap <leader>r :TagbarToggle<cr>` 打开关闭tagbar`,r`取自bar的r

  

### 12 高亮感兴趣的单词vim-interestingwords

  

https://github.com/lfv89/vim-interestingwords

  

Plug 'lfv89/vim-interestingwords'

  

- `<leader>k` 高亮显示感兴趣的单词

- `<leader>K`

- `N` 快速移动选择

  

我们浏览代码的时候经常需要知道一个变量的使用方式

我们可以使用这个插件同时高亮多个单词

  

### 13 强大的代码补全YouCompleteMe（史上最难安装）

  

#### step1 安装YCM

  

（前后安装了无数次，失败了无数次，快恶心吐了。。。）

  

https://github.com/ycm-core/YouCompleteMe

  

Plug 'ycm-core/YouCompleteMe'

Plug 'rdnetto/YCM-Generator'

  

安装完，报错：The ycmd server SHUT DOWN (restart with ':YcmRestartServer').

  

解决：执行`sudo apt install cmake`

  

继续安装：

1. cd /.vim/plugged/YouCompleteMe

2. python3 run_tests.py

  

报错：no module flake8

解决：pip3 install flake8

  

继续安装：

2. python3 run_tests.py

(坑)报错：ModuleNotFoundError: No module named 'hamcrest'

解决：pip3 install hamcrest

报错：sjx@Samsung:~/.vim/plugged/YouCompleteMe$ pip3 install hamcrest

ERROR: Could not find a version that satisfies the requirement hamcrest (from versions: none)

ERROR: No matching distribution found for hamcrest

解决：指定源：pip install hamcrest -i https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple/

继续报错，报一样的错误

解决：pip3 install Pyhamcrest

hamcrest的module叫Pyhamcrest

  

继续安装：

2. python3 run_tests.py

终于成功：

```

sjx@Samsung:~/.vim/plugged/YouCompleteMe$ python3 run_tests.py

Running flake8

Generating ycmd build configuration...OK

Compiling ycmd target: ycm_core...OK

Building regex module...OK

Building watchdog module...OK

.............................................................................................................................................................................................................s...............................................................................................................

----------------------------------------------------------------------

Ran 317 tests in 78.175s

  

OK (skipped=1)

```

  

继续安装：

3. python3 install.py --clangd-completer（基于语义的c++补全）

  

报错：卡在Setting up Clangd completer...不动弹

```

sjx@Samsung:~/.vim/plugged/YouCompleteMe$ python3 install.py --clangd-completer

Generating ycmd build configuration...OK

Compiling ycmd target: ycm_core...OK

Building regex module...OK

Building watchdog module...OK

Setting up Clangd completer...

```

解决：ctrl+z终止运行

4. 执行`/usr/bin/python3 /home/sjx/.vim/plugged/YouCompleteMe/third_party/ycmd/build.py --clangd-completer --verbose`

  

报错：卡在下载文件处不动弹

warning: no files found matching '*.h' under directory 'src'

writing manifest file 'src/watchdog.egg-info/SOURCES.txt'

Downloading Clangd from https://github.com/ycm-core/llvm/releases/download/15.0.1/clangd-15.0.1-x86_64-unknown-linux-gnu.tar.bz2...

^C^X

^Z

解决：点击https://github.com/ycm-core/llvm/releases/download/15.0.1/clangd-15.0.1-x86_64-unknown-linux-gnu.tar.bz2手动下载放到

文件夹`/home/sjx/.vim/plugged/YouCompleteMe/third_party/ycmd/third_party/clangd/cache/`下

然后：

5. cd .vim/plugged/YouCompleteMe/third_party/ycmd

6. vim build.py

7. 搜索：/ycm-core

找到这一行：download_url = ( 'https://github.com/ycm-core/

往下找几行注掉这句话：" DownloadFileTo( download_url, file_name )"

8. :wq

9. /usr/bin/python3 /home/sjx/.vim/plugged/YouCompleteMe/third_party/ycmd/build.py --clangd-completer --verbose

10. 安装成功！！

```

Using cached Clangd: /home/sjx/.vim/plugged/YouCompleteMe/third_party/ycmd/third_party/clangd/cache/clangd-15.0.1-x86_64-unknown-linux-gnu.tar.bz2

Extracting Clangd to /home/sjx/.vim/plugged/YouCompleteMe/third_party/ycmd/third_party/clangd/output...

Done installing Clangd

Clangd completer enabled. If you are using .ycm_extra_conf.py files, make sure they use Settings() instead of the old and deprecated FlagsForFile().

```

  

但这只是第一步。。

  

#### step2 为YCM配置ycm_extra_conf.py脚本

  

1. cp .vim/plugged/YouCompleteMe/third_party/ycmd/examples/.ycm_extra_conf.py ~/.ycm_extra_conf.py

2. 修改：

```python

import os

import ycm_core

  

flags = [

'-Wall',

'-Wextra',

'-Werror',

'-fexceptions',

'-DNDEBUG',

'-std=c++11',

'-x',

'-isystem',

'/home/sjx/MDEConnect/inc/common/',

'-isystem',

'/home/sjx/MDEConnect/inc/ilinkhelper/',

'-isystem',

'/home/sjx/MDEConnect/inc/service/',

'-isystem',

'/home/sjx/MDEConnect/inc/CurlHelper/',


]

  

compilation_database_folder = ''

  

if os.path.exists( compilation_database_folder ):

database = ycm_core.CompilationDatabase( compilation_database_folder )

else:

database = None

  

SOURCE_EXTENSIONS = [ '.cpp', '.cxx', '.cc', '.c', '.m', '.mm' ]

  

def DirectoryOfThisScript():

return os.path.dirname( os.path.abspath( __file__ ) )

  
  

def IsHeaderFile( filename ):

extension = os.path.splitext( filename )[ 1 ]

return extension in [ '.h', '.hxx', '.hpp', '.hh' ]

  
  

def GetCompilationInfoForFile( filename ):

# The compilation_commands.json file generated by CMake does not have entries

# for header files. So we do our best by asking the db for flags for a

# corresponding source file, if any. If one exists, the flags for that file

# should be good enough.

if IsHeaderFile( filename ):

basename = os.path.splitext( filename )[ 0 ]

for extension in SOURCE_EXTENSIONS:

replacement_file = basename + extension

if os.path.exists( replacement_file ):

compilation_info = database.GetCompilationInfoForFile(

replacement_file )

if compilation_info.compiler_flags_:

return compilation_info

return None

return database.GetCompilationInfoForFile( filename )

  
  

# This is the entry point; this function is called by ycmd to produce flags for

# a file.

def Settings( **kwargs ):

if not database:

return {

'flags': flags,

'include_paths_relative_to_dir': DirectoryOfThisScript()

}

filename = kwargs[ 'filename' ]

compilation_info = GetCompilationInfoForFile( filename )

if not compilation_info:

return None

  

# Bear in mind that compilation_info.compiler_flags_ does NOT return a

# python list, but a "list-like" StringVec object.

return {

'flags': list( compilation_info.compiler_flags_ ),

'include_paths_relative_to_dir': compilation_info.compiler_working_dir_

}

```

2. 编辑.vimrc添加：

let g:ycm_global_ycm_extra_conf='~/.ycm_extra_conf.py'

let g:ycm_confirm_extra_conf = 0 "停止提示是否载入本地ycm_extra_conf文件

  
  

#### step3 .vimrc配置YouCompleteMe

  

```shell

" YouCompleteMe

highlight PMenu ctermfg=black ctermbg=blue guifg=#ffffff guibg=#000000

highlight PMenuSel ctermfg=blue ctermbg=black guifg=#000000 guibg=#ffffff

let g:ycm_global_ycm_extra_conf='~/.ycm_extra_conf.py'

let g:ycm_confirm_extra_conf = 0

let g:ycm_collect_identifiers_from_tags_files=1 " 开启 YCM 基于标签引擎

let g:ycm_seed_identifiers_with_syntax=0 " 语法关键字补全

let g:ycm_warning_symbol = '⚠'

set completeopt=longest,menu "让vim的补全菜单行为和IDE一致

autocmd InsertLeave * if pumvisible() == 0|pclose|endif "离开插入模式后自动关闭预览窗口

nnoremap <leader>d :YcmCompleter GoToDefinitionElseDeclaration<CR>

" 跳转往回跳

nnoremap <leader>b <c-o>

"YCM-Generator配置

"更新.ycm_extra_conf.py文

nnoremap <C-y> :YcmGenerateConfig ./<CR>

```

  

参考：

https://blog.huati365.com/c76c5f36a9d47d66

https://www.jianshu.com/p/5aaae8f036c1

  

> 打开vim,执行:hi，可以查看配色信息

  
  
  

### 14 vim和git：vim-fugitive

  

https://github.com/tpope/vim-fugitive

  

Plug 'tpope/vim-fugitive'

  

- `:Gdiff` 查看当前文档做了哪些修改

  

> tmux可以开一个新的窗口

  

### 15 在vim中显示文件变动：vim-gitgutter

  

https://github.com/airblade/vim-gitgutter

  

Plug 'airblade/vim-gitgutter'

  

最左侧一栏：

  

- `~` 表示修改

- `-` 表示删减

- `+` 表示新增

  

### 16 在命令行查看提交记录：gv.vim

  

https://github.com/junegunn/gv.vim

  

Plug 'junegunn/gv.vim'

  

- `:GV` 可以浏览所有代码提交变更

- `:GV!` 列出只和当前文档相关的提交变更

  

### 17 代码格式化Neoformat

  

https://github.com/sbdchd/neoformat

  

Plug 'sbdchd/neoformat'

  

先安装c++的格式整理工具：`pip3 install clang-format`

  

- `:Neoformat` 自动代码格式整理

  

"Neoformat

nnoremap <leader>n :Neoformat<cr>

nnoremap <leader>s :source ~/.vimrc<cr>

  
  

### 18 vim快速注释代码：vim-commentary

  

https://github.com/tpope/vim-commentary

  

Plug 'tpope/vim-commentary'

  

- `gc`注释和取消注释

  

### 99 如何寻找到我们需要的插件

  

先有需求，后有插件。大部分插件托管在了github上。

1. 可以通过google搜索关键词去找到想要的插件。

2. https://vimawesome.com/

3. 浏览开源的vim配置借鉴想要的插件

  
  
  

> 我们可以通过vimscript脚本语言实现更多vim的控制，开发自己的插件

  

### 其他

  

#### 删除插件

删除插件，只需要将写在 .vimrc 配置文件内的插件删除，重启 vim 并执行命令 :PlugClean 即可：

  

#### 参考博客

1. http://t.zoukankan.com/davygeek-p-5765959.html

2. https://blog.csdn.net/qq_62357480/article/details/126854282?ops_request_misc=&request_id=&biz_id=102&utm_term=vim%20c++&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-126854282.nonecase&spm=1018.2226.3001.4187

3. https://blog.csdn.net/qq_41100010/article/details/121075296

4. https://github.com/vim-scripts/a.vim

A few of quick commands to swtich between source files and header files quickly.

5. https://www.bbsmax.com/A/qVdeyM1bdP/

  

#### 结语

  

vim是程序员送给程序员的精美礼物。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk5MTM5Mjk0MV19
-->