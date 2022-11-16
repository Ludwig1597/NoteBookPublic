
### 13 强大的代码补全YouCompleteMe

  

https://github.com/ycm-core/YouCompleteMe

  

Plug 'ycm-core/YouCompleteMe'

Plug 'rdnetto/YCM-Generator'

  

安装完，报错：The ycmd server SHUT DOWN (restart with ':YcmRestartServer').

  

解决：

1. sudo apt install cmake

2. cd /.vim/plugged/YouCompleteMe

3. ./install.py

  

" YouCompleteMe

highlight PMenu ctermfg=black ctermbg=lightblue guifg=#ffffff guibg=#000000

highlight PMenuSel ctermfg=blue ctermbg=black guifg=#000000 guibg=#ffffff

  

目前还不能进行强大的补全

  

sudo apt-get install clangd-12

  
  

### 14 vim和git：vim-fugitive

  

https://github.com/tpope/vim-fugitive

  

Plug 'tpope/vim-fugitive'

  

- Gedit

- Gdiff

- Gblame

- Gcommit

  

> tmux可以开一个新的窗口

  
  

### 99 如何寻找到我们需要的插件

  

先有需求，后有插件。大部分插件托管在了github上。

1. 可以通过google搜索关键词去找到想要的插件。

2. https://vimawesome.com/

3. 浏览开源的vim配置借鉴想要的插件

  
  
  

> 我们可以通过vimscript脚本语言实现更多vim的控制，开发自己的插件

  

结语：vim是程序员送给程序员的精美礼物。

  

删除插件

删除插件，只需要将写在 .vimrc 配置文件内的插件删除，重启 vim 并执行命令 :PlugClean 即可：

  
  

1. http://t.zoukankan.com/davygeek-p-5765959.html

2. https://blog.csdn.net/qq_62357480/article/details/126854282?ops_request_misc=&request_id=&biz_id=102&utm_term=vim%20c++&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-126854282.nonecase&spm=1018.2226.3001.4187

3. https://blog.csdn.net/qq_41100010/article/details/121075296

4. https://github.com/vim-scripts/a.vim

A few of quick commands to swtich between source files and header files quickly.

5. https://www.bbsmax.com/A/qVdeyM1bdP/

  
  

" 关闭当前 buffer

"noremap <C-x> :w<CR>:bd<CR>

"<leader>1~9 切到 buffer1~9

map <leader>1 :b 1<CR>

map <leader>2 :b 2<CR>

map <leader>3 :b 3<CR>

map <leader>4 :b 4<CR>

map <leader>5 :b 5<CR>

map <leader>6 :b 6<CR>

map <leader>7 :b 7<CR>

map <leader>8 :b 8<CR>

map <leader>9 :b 9<CR>

  
  

```

sjx@Samsung:~$ cat .vimrc

set nu "显示行号

set shiftwidth=4 "设置缩进的空格数为4

set tabstop=4 "设置软制表符宽度为4

set autoindent "设置自动缩进

set cindent "使用C/C++语言的自动缩进方式

set showmatch "光标遇到圆括号、方括号、大括号时，自动高亮对应另一个括号

set ruler "在状态栏显示光标的当前位置（位于哪一行、哪一列）

set hlsearch "设置高亮显示搜素字符串

set incsearch "设置增量搜索，随着搜索进行高亮

set t_Co=256 "启动256色

syntax on "高亮显示

syntax enable

set statusline=%f\ -\ FileType=%y "设置状态栏

colorscheme darkblueTest

  

" 设置leader key

let mapleader=","

" insert&normal模式下用,w保存文件

inoremap <leader>w <Esc>:w<cr>

nnoremap <leader>w :w<cr>

" 使用jj进入normal模式

inoremap jj <Esc>

" 使用 ctrl+h/j/k/l移动光标

noremap <C-h> <C-w>h

noremap <C-j> <C-w>j

noremap <C-k> <C-w>k

noremap <C-l> <C-w>l

" 使用,数字打开不同buffer

map <leader>1 :b 1<CR>

map <leader>2 :b 2<CR>

map <leader>3 :b 3<CR>

map <leader>4 :b 4<CR>

map <leader>5 :b 5<CR>

map <leader>6 :b 6<CR>

map <leader>7 :b 7<CR>

map <leader>8 :b 8<CR>

map <leader>9 :b 9<CR>

  

call plug#begin('~/.vim/plugged')

Plug 'mhinz/vim-startify'

Plug 'octol/vim-cpp-enhanced-highlight'

Plug 'vim-airline/vim-airline'

Plug 'vim-airline/vim-airline-themes'

Plug 'Yggdroot/indentLine'

Plug 'preservim/nerdtree'

Plug 'ctrlpvim/ctrlp.vim'

Plug 'easymotion/vim-easymotion'

Plug 'tpope/vim-surround'

Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }

Plug 'junegunn/fzf.vim'

Plug 'brooth/far.vim'

Plug 'preservim/tagbar'

Plug 'lfv89/vim-interestingwords'

Plug 'ycm-core/YouCompleteMe'

Plug 'rdnetto/YCM-Generator'

Plug 'tpope/vim-fugitive'

call plug#end()

  

" airline

let g:airline#extensions#tabline#enabled = 1

let g:airline#extensions#tabline#buffer_nr_show = 1 "buffer显示编,

  

nnoremap <leader>f :NERDTreeFind<cr>

nnoremap <leader>t :NERDTreeToggle<cr>

  

let g:ctrlp_map = '<c-p>'

  

nmap ss <Plug>(easymotion-s2)

  

let g:rainbow_active = 1

  

nnoremap <leader>r :TagbarToggle<cr>

  

" YouCompleteMe

highlight PMenu ctermfg=black ctermbg=lightblue guifg=#ffffff guibg=#000000

highlight PMenuSel ctermfg=blue ctermbg=black guifg=#000000 guibg=#ffffff

let g:ycm_global_ycm_extra_conf='~/.ycm_extra_conf.py'

let g:ycm_confirm_extra_conf = 0

sjx@Samsung:~$

  

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDk1MTMxNjQ2XX0=
-->