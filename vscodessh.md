> 2022.10.31

# 配置vscode（Remote-SSH）

## Remote-SSH插件

简单用vscode配置remote ssh可以方便的实现通过ssh在线使用vscode编辑文件。

## vscode端

1.  安装插件
2.  设置界面：
    -   右键最左边的tab栏
    -   勾选远程资源管理器
3.  添加远程服务器：
    -   点击 + 号，输入ssh指令连接：ssh [sjx@109.123.120.146](mailto:sjx@109.123.120.146)
    -   选择一个文件作为存储：这里选择C:\Users\vscode_ssh
    -   这时候会在SSH TARGETS一栏，看见一个小电脑后面跟着109.123.120.146
    -   可以打开刚刚存储的文件C:\Users\vscode_ssh，将`Host 109.123.120.146`改成`Host sjx`

> 如果选择的文件没有访问权限，则无法显示出连接，需要修改一下文件夹或者文件的权限。

4.  连接服务器
    -   右键SSH TARGETS的小电脑，选择：Connect to Host in New Window，然后选择Linux
    -   会跳出来连接失败：Could not establish connection to "109.123.120.146"
    -   提示：Using commit id "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" and quality "stable" for server

## server端

连接失败的原因，是server端需要下载vscode-server。

1.  找到刚刚提示里的commit id：d045a5eda657f4d7b676dedbfa7aab8207f8a075
2.  根据commit_id下载对应版本的vscode-server：`https://update.code.visualstudio.com/commit:${commit_id}/server-linux-x64/stable`  
    如：[https://update.code.visualstudio.com/commit:d045a5eda657f4d7b676dedbfa7aab8207f8a075/server-linux-x64/stable](https://update.code.visualstudio.com/commit:d045a5eda657f4d7b676dedbfa7aab8207f8a075/server-linux-x64/stable)
3.  将下载下来的：vscode-server-linux-x64.tar.gz解压缩，得到vscode-server-linux-x64目录。
4.  `mkdir -p ~/.vscode-server/bin/${commit_id}`  
    如：mkdir -p ~/.vscode-server/bin/d045a5eda657f4d7b676dedbfa7aab8207f8a075
5.  将vscode-server-linux-x64目录下的所有文件拷贝到.vscode-server/bin/d045a5eda657f4d7b676dedbfa7aab8207f8a075/下
6.  在.vscode-server/下新建文件夹：extensions
7.  cp -r ${PATH_TO_YOUR_VSCODE_EXTENSIONS}/extensions/* ~/.vscode-server/extensions  
    如：cp -r /home/sjx/.vscode-server/bin/d045a5eda657f4d7b676dedbfa7aab8207f8a075/extensions/* ~/.vscode-server/extensions/

# 一键脚本
commit_id=XXX
PATH_TO_YOUR_VSCODE_SERVER=XXX

mkdir -p ~/.vscode-server/bin/${commit_id}
cp ${PATH_TO_YOUR_VSCODE_SERVER}/vscode-server-linux-x64.tar.gz ~/.vscode-server/bin/${commit_id}

cd ~/.vscode-server/bin/${commit_id}
tar -xzf vscode-server-linux-x64.tar.gz && rm vscode-server-linux-x64.tar.gz
mv vscode-server-linux-x64/* . && rm -r vscode-server-linux-x64

mkdir -p ~/.vscode-server/extensions
cp -r ${PATH_TO_YOUR_VSCODE_EXTENSIONS}/extensions/* ~/.vscode-server/extensions

8.  重新连接，输入密码，至此，应该大功告成。
9.  但是还是失败了。

## 坑

经过排查，发现是因为linux重装了系统，vscode本地（win本地）已经保存了该ip对应服务器的密钥。重置服务器当该ip对应的服务器发生变化时，连接的时候发现远程服务器发回来的密钥和之前对不上了，因此连接失败。

解决方法：

1.  vscode是在win下的客户端，而保存这种连接密钥的路径是：C:\Users\jx77.sun.ssh\known_hosts
2.  在win下删掉known_hosts文件即可
3.  重新连接，大功告成

## 配置无密码登录

每次连接服务器，或者打开文件夹都需要输入一遍密码，很麻烦。因此，配置无密码登录。

解决方法：

1.  在服务器上`ssh-keygen -t rsa -b 4096`,一路回车
2.  将用户目录下的.ssh/id_rsa.pub 文件内容上传到服务器的~/.ssh 下并且命名为 authorized_keys
3.  再次通过vscode连接服务器，发现可以直接连接，实现了免密登录
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5Nzk2NDQxNjZdfQ==
-->