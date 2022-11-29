> 2022.11.24

  

# vim后话

  

## 01 linux下强大目录跳转：autojump

  

安装完成后，访问过的文件夹，直接：

  

- `j 文件夹名` 进行跳转，进入到文件夹目录

  

## 02 vim和terminal：神器tmux

  

tmux 是一个终端复用工具，用于在一个终端窗口中运行多个终端会话。

安装：`sudo apt install tmux`

  

tmux默认的快捷前缀是`ctrl+b`。

  

### tmux中几个概念：

- 会话（session）：建立一个tmux工作区会话，会话可以长期驻留，重新连接服务器不会丢失，我们只需要重新tmux attach到之前的工作区就可以恢复会话，这样工作区就可以常驻服务器了。

- 窗口（window）：窗口可以容纳多个窗格

- 窗格（pane）：可以在窗口中分成多个窗格，每个窗格都可以独立运行各种命令

  

![](img/Image%20Pasted%20at%202022-11-24%2010-05.jpg)

  

### tmux中的操作

  

- `tmux new -s xxx` 新建名为xxx的session

- `tmux ls` 查看当前会话

- `tmux a` 重新接入之前attach的会话

- `tmux attach -t 0/xxx` 接入编号为0或名为xxx的会话

- `tmux kill-session -t 0/xxx` 杀死某个会话

- `tmux switch -t 0/xxx` 切换会话

- `tmux rename-session -t 0 xxx` 将0号会话重命名为xxx

  

- `ctrl+b d` d表示detach，脱离当前会话

- `ctrl+b x` 关闭当前窗格

- `ctrl+b s` 查看当前会话，可以使用j、k、l上下移动查看窗口

- `ctrl+b $` 重命名当前会话

- `ctrl+b %` 左右分屏

- `ctrl+b "` 上下分屏

- `ctrl+b c` 新建窗口

- `ctrl+b n` 前往下个窗口

- `ctrl+b p` 回到上个窗口

- `ctrl+b h` 窗格间左移

- `ctrl+b l` 窗格间右移

- `j`,`k`上下移动

- `ctrl+b 空格` 上下分屏与左右分屏的切换

- `ctrl+b alt+上下左右` 调整窗口大小

- `ctrl+b {` 当前窗格与上一个窗格交换

- `ctrl+b }` 当前窗格与下一个窗格交换

- `ctrl+b z` 当前窗格全屏显示，再用一次变回原来大小

- `ctrl+b ctrl+上下左右` 按箭头方向调整窗格大小

  

### tmux true color

  

遇到一个问题，在配置主题颜色的时候tmux的显示和不使用tmux时不一致。

  

解决：

1. 首先看shell支不支持真彩色：`curl -s https://raw.githubusercontent.com/JohnMorales/dotfiles/master/colors/24-bit-color.sh | bash`

2. 看到tmux外执行是渐变的，但是tmux内执行是断层的。

3. 修改.vimrc 与 .tmux.conf

```shell

# .vimrc

set -g default-terminal "xterm-256color"

set-option -ga terminal-overrides ",xterm-256color:Tc"

```

  

```shell

# .vimrc

  

set termguicolors

if &term =~# '^screen'

let &t_8f = "\<Esc>[38;2;%lu;%lu;%lum"

let &t_8b = "\<Esc>[48;2;%lu;%lu;%lum"

endif

```

4. 这时候会发现错误，因为我们终端模拟器默认的可能是8色而非256色

5. 查看自己当前的term与终端支持的颜色：`echo $TERM`+`tput colors`

```shell

sjx@Samsung:~$ echo $TERM

xterm

sjx@Samsung:~$ tput colors

8

sjx@Samsung:~$

```

6. 修改.bashrc,在文件结尾添加,并source一下

```shell

if [ "$TERM" == "xterm" ]; then

export TERM=xterm-256color

fi

```

7. 再次查看

```shell

sjx@Samsung:~$ echo $TERM

xterm-256color

sjx@Samsung:~$ tput colors

256

sjx@Samsung:~$

```

8. 进入tmux后发现还是没有生效

9. 原因：每次改完tmux的配置，一定要保证shell里面的tmux session!全部关闭!，重启tmux才能看到效果

10. 至此解决

  

## 03 buffer再探究

  

### 配置几个映射

  

```

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

  

" 使用tab键切换buffer

nnoremap <Tab> :bnext<cr>

  

" 使用,e关闭当前buffer

nnoremap <leader>e :bdelete<cr>

```

  

## 04 重新配置colorscheme

  

```

let g:airline_theme='bubblegum'

  

Plug 'sheerun/vim-polyglot'

Plug 'ghifarit53/tokyonight-vim'

Plug 'tomasr/molokai'

let g:rehash256 = 1

colorscheme molokai

```

  

## 05 vim嵌入开发工具

  

几乎所有流行的编辑器和IDE都支持vim插件。

  

## 06 一些深入方向

  

- 《Practical vim》

- 《笨方法学vimscript》

- 学习和开发自己的插件
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjg5NTY0MzFdfQ==
-->