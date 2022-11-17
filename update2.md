  

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

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/home/abuild/rpmbuild/BUILD/com.samsung.tv.mdeconnect-1.1.1/inc/common',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/was-api/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/libpisa-ipc/',

'-isystem',

'/home/sjx/MDEConnect/inc/common/',

'-isystem',

'/home/sjx/MDEConnect/inc/ilinkhelper/',

'-isystem',

'/home/sjx/MDEConnect/inc/service/',

'-isystem',

'/home/sjx/MDEConnect/inc/CurlHelper/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/appcore-agent/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/vconf/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/aul/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/system/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/capi-system-system-settings/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/network/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/lib/glib-2.0/include/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/capi-system-info/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/smart-deadlock/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/glib-2.0/',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/dlog',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/notification',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/appfw',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/notification-vd',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/jsoncpp',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/VDCurl',

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

  

https://blog.huati365.com/c76c5f36a9d47d66

  

'-I',

'/home/sjx/MDEConnect/inc',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/notification',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/appfw',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/notification-vd',

'-isystem',

'/home/sjx/GBS-ROOT6.5/local/BUILD-ROOTS/scratch.armv7l.0/usr/tizen-studio/platforms/tizen-5.0/tv-samsung/rootstraps/tv-samsung-5.0-device.core/usr/include/jsoncpp'

  
  
  
  

https://www.jianshu.com/p/5aaae8f036c1

  

" YouCompleteMe

highlight PMenu ctermfg=black ctermbg=lightblue guifg=#ffffff guibg=#000000

highlight PMenuSel ctermfg=blue ctermbg=black guifg=#000000 guibg=#ffffff

  

目前还不能进行强大的补全

  

sudo apt-get install clangd-12
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMxNDUzNDc2MF19
-->