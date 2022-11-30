> 2022.11.30

  

# 从0配置vim

  

## step1 新建账户

  

- `sudo adduser xxx`

  

## step2 配置基础设置和基础映射

  

- vim .vimrc

```vim

" 基础设置

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

set cursorline

  

" 基本映射

" 设置leader key

let mapleader=","

" 使用jj进入normal模式

inoremap jj <Esc>

" insert&normal模式下用,w保存文件

inoremap <leader>w <Esc>:w<cr>

nnoremap <leader>w :w<cr>

" normal模式下source.vimrc文件

nnoremap <leader>s :source ~/.vimrc<cr>

" 使用,q退出vim

nnoremap <leader>q :q<cr>

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

" 使用tab键在buffer之间移动

nnoremap <Tab> :bnext<cr>

" 使用,e退出buffer

nnoremap <leader>e :bdelete<cr>

```

  

- source ~/.vimrc

  

## step3 安装插件管理器vim-plug

  

- 配置代理

```

vim .curlrc

  

proxy = "http://109.123.97.11:8080"

  

insecure

  

sync

```

- 安装vim-plug

```

curl -fLo ~/.vim/autoload/plug.vim --create-dirs \

https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim`

```

## setp4 安装并配置除YouCompleteMe以外的所有插件

  

- vim .vimrc

```vim

" 安装插件

call plug#begin('~/.vim/plugged')

Plug 'mhinz/vim-startify' " vim开屏工具

Plug 'preservim/nerdtree' " vim目录树

Plug 'vim-airline/vim-airline' " vim状态栏美化

Plug 'vim-airline/vim-airline-themes' " vim状态栏主题

Plug 'Yggdroot/indentLine' " 增加代码缩进线条

Plug 'ctrlpvim/ctrlp.vim' " 快速搜索文件，模糊搜索器

Plug 'easymotion/vim-easymotion' " 文件内快速定位插件

Plug 'tpope/vim-surround' " 成双成对编辑插件

Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }

Plug 'junegunn/fzf.vim' " 多文件模糊搜索

Plug 'brooth/far.vim' " 批量搜索替换插件

Plug 'preservim/tagbar' " 代码大纲插件

Plug 'lfv89/vim-interestingwords' " 高亮感兴趣的单词插件

Plug 'ycm-core/YouCompleteMe' " YCM代码补全插件

Plug 'rdnetto/YCM-Generator' " YCM生成器插件

Plug 'octol/vim-cpp-enhanced-highlight' " c++代码高亮插件

Plug 'tpope/vim-fugitive' " git插件

Plug 'airblade/vim-gitgutter' " 左侧数字栏显示文件变动

Plug 'junegunn/gv.vim' " 查看代码提交记录

Plug 'sbdchd/neoformat' " 代码格式化插件

Plug 'tpope/vim-commentary' " 快速注释插件

Plug 'sheerun/vim-polyglot' " 主题相关的插件

Plug 'ghifarit53/tokyonight-vim' " tokyonight主题

Plug 'tomasr/molokai' " molokai主题

Plug 'iamcco/mathjax-support-for-mkdp' " markdwon相关的插件

Plug 'iamcco/markdown-preview.vim'

Plug 'godlygeek/tabular' "必要插件，安装在vim-markdown前面

Plug 'plasticboy/vim-markdown'

call plug#end()

  

" 插件配置

" nerdtree

nnoremap <leader>f :NERDTreeFind<cr>

nnoremap <leader>t :NERDTreeToggle<cr>

  

" airline

let g:airline#extensions#tabline#enabled = 1

let g:airline#extensions#tabline#buffer_nr_show = 1 "buffer显示编号

  

" airline theme

let g:airline_theme='bubblegum'

  

" ctrlp.vim

let g:ctrlp_map = '<c-p>'

  

" easymotion

nmap ss <Plug>(easymotion-s2)

  

" tagbar

nnoremap <leader>r :TagbarToggle<cr>

" 跳转往回跳

nnoremap <leader>b <c-o>

  

" YouCompleteMe

highlight PMenu ctermfg=black ctermbg=blue guifg=#ffffff guibg=#000000

highlight PMenuSel ctermfg=blue ctermbg=black guifg=#000000 guibg=#ffffff

let g:ycm_global_ycm_extra_conf='~/.ycm_extra_conf.py'

let g:ycm_confirm_extra_conf = 0

let g:ycm_collect_identifiers_from_tags_files=1 " 开启 YCM 基于标签引擎

let g:ycm_seed_identifiers_with_syntax=0 " 语法关键字补全

let g:ycm_warning_symbol = '⚠'

" set completeopt=longest,menu "让vim的补全菜单行为和IDE一致

autocmd InsertLeave * if pumvisible() == 0|pclose|endif "离开插入模式后自动关闭预览窗口

nnoremap <leader>d :YcmCompleter GoToDefinitionElseDeclaration<CR>

  

"YCM-Generator配置

"更新.ycm_extra_conf.py文

nnoremap <C-y> :YcmGenerateConfig ./<CR>

  

" gitgutter

" 设置更新时间为100ms

set updatetime=100

"Neoformat

nnoremap <leader>n :Neoformat<cr>

  

" markdonw-preview

let g:mkdp_path_to_chrome = "/opt/google/chrome/google-chrome"

" let g:mkdp_brower = 'google-chrome'

nnoremap <leader>p :MarkdownPreview<cr>

nnoremap <leader>o :MarkdownPreviewStop<cr>

nnoremap <leader>a :Toc<cr>

" let g:mkdp_auto_start = 1

let g:markdown_fenced_languages =['c', 'cpp', 'python', 'javascript', 'shell']

let g:vim_markdown_folding_disabled = 1

let g:vim_markdown_toc_autofit = 1

let g:vim_markdown_edit_url_in = 'tab'

let g:rainbow_active = 1

  

" colorscheme

set termguicolors

if &term =~# '^screen'

let &t_8f = "\<Esc>[38;2;%lu;%lu;%lum"

let &t_8b = "\<Esc>[48;2;%lu;%lu;%lum"

endif

let g:rehash256 = 1

colorscheme molokai

````

- source ~/.vimrc

- :PlugInstall

  

## step5 配置YCM

  

- cd /.vim/plugged/YouCompleteMe

- python3 run_test.py

- pip3 install flake8

- pip3 install Pyhamcrest

- python3 install.py --clangd-completer

- 点击https://github.com/ycm-core/llvm/releases/download/15.0.1/clangd-15.0.1-x86_64-unknown-linux-gnu.tar.bz2手动下载放到

文件夹/home/xxx/.vim/plugged/YouCompleteMe/third_party/ycmd/third_party/clangd/cache/下

- cd .vim/plugged/YouCompleteMe/third_party/ycmd

- vim build.py

- 搜索：/ycm-core

找到这一行:``download_url = ( 'https://github.com/ycm-core/``

往下找几行注掉这句话：" DownloadFileTo( download_url, file_name )"

- :wq

- /usr/bin/python3 /home/sjx/.vim/plugged/YouCompleteMe/third_party/ycmd/build.py --clangd-completer --verbose
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc2NTA5ODY4NF19
-->