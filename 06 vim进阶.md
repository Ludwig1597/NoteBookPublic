> 2022.11.9

# vim进阶

## vim下载插件

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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAyODczNTA4N119
-->