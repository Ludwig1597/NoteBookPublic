> 2022.10.10

  

# c++关于文件的相关操作

  

与文件有关的操作有：

- 判断文件/文件夹是否存在

- 创建文件/文件夹

- 遍历文件夹

- 删除文件/文件夹、

- 拷贝文件

- 查看文件具体信息

- 将文件读成二进制

- 将二进制字符写成文件

- 计算文件大小

  

## 01 判断文件/文件夹是否存在

  

- access()

  

```c++

bool m_IsFileExist(const string &path){

if(access(path.c_str(), F_OK) == 0)

{

_INFO("%s exist", path.c_str());

return true;

}

else

{

_ERR("%s not exist", path.c_str());

}

return false;

}

```

  

> access()函数参考`01 c++积累`中第11点。

  

## 02 创建文件/文件夹

  

### 创建文件

  

- open()

- fsync()

- close()

  

```c++

void m_CreateFile(const string &name)

{

if(access(name.c_str(), F_OK) == 0)

{

LOG_ERR("file %s exist", name.c_str());

return;

}

  

int fd = open(name.c_str(), O_CREAT|O_SYNC, 0644);

if(fd < 0)

{

LOG_ERR("open %s fail: %d", name.c_str(), fd);

return;

}

  

int ret = fsync(fd);

if(ret < 0)

{

LOG_ERR("fsync fail : %d", ret);

}

  

ret = close(fd);

if(ret < 0)

{

LOG_ERR("close fail : %d", ret);

}

}

```

  

### 创建文件夹

  

- mkdir()

  

```c++

int create_dir(const string &dir)

{

if (access(dir.c_str(), F_OK) == 0)

{

_INFO("dir [%s] already exist.", dir.c_str());

return 0;

}

auto result = mkdir(dir.c_str(), 0755);

if (result == -1)

{

_ERR("mkdir [%s] failed. errno = [%d]", dir.c_str(), errno);

return -1;

}

_INFO("mkdir [%s] success.", dir.c_str());

return 0;

}

```

  

## 03 遍历文件夹

  

### 遍历当前文件夹

  

- lstat()

- S_ISDIR()

- opendir()

- closedir()

  

```c++

void listFiles(const char* dir_name) {

struct stat s;

lstat(dir_name, &s);

if (!S_ISDIR(s.st_mode)){

cout<<"dir_name is not a valid directory !"<<endl;

return;

}

DIR * dir; // return value for opendir()

dir = opendir(dir_name);

if (NULL == dir){

cout<<"Can not open dir !"<<endl;

return;

}

cout<<"Successfully opened the dir !"<<endl;

  

struct dirent * filename; // return value for readdir()

/* read all the files in the dir ~ */

while ((filename = readdir(dir)) != NULL)

{

// get rid of "." and ".."

if (strcmp(filename->d_name, ".") == 0 ||strcmp(filename->d_name, "..") == 0)

continue;

cout<<"filename: "<<filename->d_name<<endl;

}

}

```

  

> 参考`02 linux中文件夹的遍历(c++).md`

  

### 递归遍历当前文件夹及其子文件夹下所有文件

  

暂无。

  

## 04 删除文件/文件夹

  

### 删除文件

  

- remove()

  

```c++

void m_DeleteFile(const string &name)

{

if(access(name.c_str(), F_OK) != 0)

{

LOG_ERR("file %s don't exist", name.c_str());

return ;

}

remove(name.c_str());

}

```

  

### 删除文件夹

  

- rmdir();

  

> rmdir()函数只能删除空文件夹。故需要遍历删除文件夹下所有文件再删除文件夹。

  

### 删除文件夹下所有文件

  

```c++

int delete_specified_folder_files(const char *dir_name)

{

_DBG("Folder path is: %s", dir_name);

struct stat s;

lstat(dir_name, &s);

if (!S_ISDIR(s.st_mode))

{

_DBG("dir_name is not a valid diretory!");

rsp["reason"] = "dir_name is not a valid diretory";

return -1;

}

DIR *dir = opendir(dir_name);

if (NULL == dir)

{

_DBG("Can not open dir!");

rsp["reason"] = "can not open dir";

return -1;

}

_DBG("Opened the dir successfully!");

struct dirent *file;

while ((file = readdir(dir)) != NULL)

{

if (strcmp(file->d_name, ".") == 0 || strcmp(file->d_name, "..") == 0)

continue; // get rid of "." and ".."

string filename = file->d_name;

string path = dir_name;

path += "/";

path += filename;

_DBG("fullpath is %s,remove", path.c_str());

remove(path.c_str());

}

closedir(dir);

return 0;

}

```

  

### 递归遍历删除文件夹及其子文件夹下所有文件

  

暂无。

  

## 05 拷贝文件

  

### 方式一 使用fwrite和fread

  

- fopen()

- fseek()

- fread()

- fwrite()

- fclose()

  

```c++

int copy_file(const string &from, const string &to)

{

FILE* fSrc = fopen(from.c_str(),"rb");

if (NULL == fSrc)

{

_ERR("failed to open: %s, error reason: %s", from.c_str(),strerror(errno));

return -1;

}

FILE* fDes = fopen(to.c_str(), "wb");

if (NULL == fDes)

{

_ERR("failed to create file: %s,error reason: %s", to.c_str(),strerror(errno));

return -1;

}

unsigned char* buf;

unsigned int length;

fseek(fSrc, 0, SEEK_END);

length = ftell(fSrc);

buf = new unsigned char[length+1];

memset(buf, 0, length+1);

fseek(fSrc, 0, SEEK_SET);

fread(buf, length, 1, fSrc);

fwrite(buf, length, 1, fDes);

_INFO("result: [%s]", buf);

fclose(fSrc);

fclose(fDes);

delete [] buf;

return 0;

}

```

  

### 方式二 使用popen(shell命令方式) 更简单

  

- popen()

- fread()

- pclose()

  

```c++

int copy_file(const string &from, const string &to)

{

string command = "cp " + from + " " + to;

_INFO("command is [%s]", command.c_str());

FILE *fp = popen(command.c_str(), "r");

if (NULL == fp)

{

_ERR("failed to execute command: [%s]", command.c_str());

return -1;

}

else

{

char result[1024];

memset(result, 0, 1024);

fread(result, 1, 1024, fp);

_INFO("result: [%s]", result);

pclose(fp);

}

}

```

  

## 06 查看文件具体信息

  

```c++

int read_specified_file_info(const string type,string path,Json::Value &fileInfo){

_INFO("read_specified_file_info");

fileInfo["type"] = type;

fileInfo["fullPath"] = path;

  

struct stat statbuf;

lstat(path.c_str(), &statbuf);

string file_name = path.erase(0,path.find_last_of("/")+1);

fileInfo["name"] = file_name;

char tmp[50];

memset(tmp, 0, 50);

snprintf(tmp, 50, "%ld", statbuf.st_size);

fileInfo["size"] = tmp;

memset(tmp, 0, 50);

snprintf(tmp, 50, "%ld", statbuf.st_atim.tv_sec);

fileInfo["lastAccess"] = tmp;

memset(tmp, 0, 50);

snprintf(tmp, 50, "%ld", statbuf.st_mtim.tv_sec);

fileInfo["lastModify"] = tmp;

_INFO("fileInfo = %s",fileInfo.toStyledString().c_str());

return 0;

}

```

  

## 07 将文件读成二进制

  

### 方式一

  

```c++

char* readFileToBytes(const char* pathName){

int Exist=access(pathName,F_OK);

_DBG("Exist %d",Exist);//检测文件是否存在：0 存在 1 不存在

FILE* fp=NULL;

fp=fopen(name,"rb");

if(fp==NULL){

_DBG("can not open the file");

return NULL;

}

fseek(fp,0,SEEK_END);

len=ftell(fp);

_DBG("len = %d",len);

char* ret=new char[len];

fseek(fp,0,SEEK_SET);

fread(ret,1,len,fp);

fclose(fp);

return ret;

}

```

  

### 方式二

  

```c++

int read_file(const string &file_name, std::shared_ptr<unsigned char> &buffer, int &buffer_size)

{

int f = open(file_name.c_str(), O_RDONLY);

if (f == -1)

{

_ERR("Failed to open %s with flag [O_RDONLY], errno = [%d]", file_name.c_str(),errno);

return -1;

}

_INFO("opened file: [%s]", file_name.c_str());

struct stat fileState;

int r = fstat(f, &fileState);

if (r == -1)

{

_ERR("fstat for [%s] failed, errno = [%d]", file_name.c_str(), errno);

close(f);

return -1;

}

_INFO("fstat to get file size success.");

size_t fileSize = fileState.st_size;

buffer_size = fileSize;

_INFO("File [%s] size is : %u", file_name.c_str(), fileSize);

if (fileSize == 0)

{

close(f);

return 0;

}

buffer = std::shared_ptr<unsigned char>(new unsigned char[fileSize]);

if (buffer.get() == NULL)

{

_ERR("malloc failed. errno = [%d]", errno);

if (errno == ENOMEM)

{

_ERR("Out of memory.");

}

close(f);

return -1;

}

_INFO("malloc buffer for reading file success.");

ssize_t readSize = read(f, buffer.get(), fileSize);

if (readSize != fileSize)

{

_ERR("readSize = %u, but fileSize = %u, errno = [%d]", readSize, fileSize, errno);

close(f);

return -1;

}

close(f);

return 0;

}

```

  

## 08 将二进制写成文件

  

### 简写

  

```c++

void writeBytesToFile(unsigned char* desbuffer,size_t len,const string &file_name){

FILE* fp;

_DBG("plaintext_len = %d",len);

fp=fopen(file_name.c_str(),"wb");

fwrite(desbuffer,len,1,fp);

fclose(fp);

}

```

  

### 完整写法

```c++

int write_file(void *buffer, int buffer_size, const string &file_name)

{

FILE *fp = fopen(file_name.c_str(), "w+");

if (fp == NULL)

{

_ERR("open file %s failed. errno = [%d]", file_name.c_str(), errno);

return -1;

}

_INFO("opened file: [%s]", file_name.c_str());

size_t writtenSize = fwrite(buffer, 1, buffer_size, fp);

_INFO("written size: %d", writtenSize);

fclose(fp);

return writtenSize;

}

```

## 09 将string写进文件

  

```cpp

#include <iostream>

#include <fstream>

#include <string>

  

int main(){

std::string str = "hello";

  

std::ofstream file;

file.open("/home/sjx/test");

file<<str;

file.close();

return 0;

}

```

  

## 10 将文件里的字符读到string

  

```cpp

#include <iostream>

#include <fstream>

#include <string>

  

int main(){

std::string str;

  

std::ifstream file;

file.open("/home/sjx/test");

file>>str;

file.close();

  

std::cout<<str<<std::endl;

return 0;

}

```

  

## 11 计算文件/文件夹大小

  

### 计算文件大小

  

```c++

long get_file_size(const string &path){

struct stat statbuf;

lstat(path.c_str(), &statbuf);

return statbuf.st_size;

}

```

  

### 计算文件夹大小

  

```c++

long get_dir_size(const string &dir)

{

auto opened_dir = opendir(dir.c_str());

if (opened_dir == NULL)

{

_ERR("open [%s] failed. errno = %d", dir.c_str(), errno);

return -1;

}

struct dirent *entry;

struct stat statbuf;

statbuf.st_size = 0;

auto total_size = statbuf.st_size;

string file_full_name;

while ((entry = readdir(opened_dir)) != NULL)

{

file_full_name = dir + "/" + entry->d_name;

lstat(file_full_name.c_str(), &statbuf);

_INFO("checking [%s], statbuf.st_mode = [%d]", entry->d_name, statbuf.st_mode);

if (S_ISDIR(statbuf.st_mode))

{

_INFO("it is not regular file.");

continue;

}

else

{

_INFO("it is file, it's size is [%ld].", statbuf.st_size);

total_size += statbuf.st_size;

}

}

closedir(opened_dir);

return total_size;

}

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg0MjU5Nzg2OV19
-->