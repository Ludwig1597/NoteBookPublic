> 2022.11.26

# vim配置markdown

  

## 安装插件

  

### 编辑.vimrc

```shell

Plug 'iamcco/mathjax-support-for-mkdp'

Plug 'iamcco/markdown-preview.vim'

Plug 'godlygeek/tabular' "必要插件，安装在vim-markdown前面

Plug 'plasticboy/vim-markdown'

nnoremap <leader>p :MarkdownPreview<cr>

nnoremap <leader>s :MarkdownPreviewStop<cr>

nnoremap <leader>a :Toc<cr>

" let g:mkdp_auto_start = 1

let g:markdown_fenced_languages =['c', 'cpp', 'python', 'javascript','shell']

let g:vim_markdown_folding_disabled = 1

let g:vim_markdown_toc_autofit = 1

let g:vim_markdown_edit_url_in = 'tab'

let g:mkdp_path_to_chrome = "/opt/google/chrome/google-chrome"

```

  

### 快捷键

  

- `,p` 打开预览

- `,s` 关闭预览

- `[[` 跳转至上一个标题

- `]]` 跳转至下一个标题

- `]u` 跳转至副标题

- `zm` 折叠当前段落

- `zM` 折叠所有段落

- `zr` 打开当前折叠

- `zR` 打开所有折叠

- `zc` 折叠当前光标所在目录

- `zC` 递归折叠当前光标所在目录

- `za` 打开/关闭当前光标所在目录

- `zA` 递归打开当前光标所在目录

- `:Toc` 显示目录

- `:help vim-markdown` 查看vim-markdown帮助
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgwMjA4MjcxNF19
-->