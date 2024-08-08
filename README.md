#git命令大全
#### 全局配置

```
git config --global user.name 野c

git config --global credentail.helper store

git config --global user.email 1@qq.com
```

#### 解决乱码

```
$ git config --global core.quotepath false          # 显示 status 编码
$ git config --global gui.encoding utf-8            # 图形界面编码
$ git config --global i18n.commit.encoding utf-8    # 提交信息编码
$ git config --global i18n.logoutputencoding utf-8  # 输出 log 编码
$ export LESSCHARSET=utf-8
# 最后一条命令是因为 git log 默认使用 less 分页，所以需要 bash 对 less 命令进行 utf-8 编码
```

#### 初始化

```
git init
当前目录下初始化
git init my01
在当前目录下创建my01文件夹，初始化在my01目录下
xcopy my01 my01-ssh /E /H /Y
复制一个git仓库/E：复制目录子目录（包含空目录）/H：还复制隐藏文件和系统文件/Y: 禁止提示确认是否要覆盖现有目标文件。
```

#### ssh配置

- 首先

  ```
  新建一个4096位的密钥
  ssh-keygen -t rsa -b 4096
  
  Enter file in which to save the key (C:\Users\a/.ssh/id_rsa): test
  默认回车即可，重新创建请输入文件名
  
  Enter passphrase (empty for no passphrase):
  输入密码
  
  Enter same passphrase again:
  再一次输入密码
  
  SHA256:1NCYP
  指纹
  
  git clone git@github.com:yecaobupashao/my01.git
  测试完成
  ```

  

- 创建

  ```
  新建一个config文件
  写入：
  #github
  Host github.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/test
  ```

  

#### 添加远程仓库

```
git remote add yyy git@github.com:yecaobupashao/my01.git
yyy是仓库别名，最后一个参数是仓库地址

git push -u yyy main
yyy是远程仓库名，main是分支名

git remote -v
查看远程仓库

git pull yyy <本地分支名>：<远程分支名>
一般为				master：main
如果分支相同，可以省略括号后的

```



#### 常用

##### 暂存区

```
git add my01.txt
添加到暂存区
git add .
提交当前文件加的所有文件
git rm --cached my01.txt
移除暂存区的文件
git ls-files
查看暂存区
git add *.txt
提交所有txt结尾的文件
```

##### 上传

```
git commit
上传到本地仓库
git commit -am '学会忽略文件'
可以省略`git add .`命令
```

##### 状态

```
git status
查看状态
```

##### 提交记录

```
git log
查看提交记录
git log --oneline
查看简洁的提交记录
```

##### diff差异比较

需要先改为utf-8编码，否则识别不了

log文件识别不了

```bash
git diff
查看工作区和暂存区的不同
git diff HEAD
查看工作区和本地仓库的不同
git diff --cached
查看暂存区和本地仓库的不同
git diff c8ef435 c8ef435
比较两个版本库的不同
git diff c8ef435 HEAD
HEAD表示最近一次提交

git diff HEAD~ HEAD
表示查看最近两次提交有哪些更改
git diff HEAD^ HEAD
表示查看最近两次提交有哪些更改
git diff HEAD~2 HEAD
HEAD之前的第2个版本
git diff HEAD~2 HEAD file3.txt
HEAD之前的第2个版本 和现在的版本中 file3这个文件的差异
```

##### reset回退

- git reset `xxx` 版本号
  - --sorf保存工作区和暂存区所有内容
  - --hard丢弃暂存区和工作区的所有内容
  - --mixed保留工作区的内容，丢弃暂存区的内容
  
  ```
  git reset HARD *
  ```
  
  

##### reflog回溯

```
git reflog
查看历史操作记录，找到误操作的版本号
git reset --hard c8ef435
```

##### rm删除（暂存区和本地同时删除）

```
rm my02.txt
git add .
先删除工作区的，再提交删除后的到暂存区
git rm my02.txt
删除指定的文件
git rm -r *
递归删除当前目录下的所有文件
git rm --cached my01.txt
移除暂存区的文件
```

##### rm误操作恢复恢复

```
git rm *
git status
git reset HEAD *
git status
git restore *
```



##### 忽略文件

```
PS D:\A-yulequ\python\wusir\git_learn\my01-soft> echo '<111>' > access.log
PS D:\A-yulequ\python\wusir\git_learn\my01-soft> echo '<111>' > other.log
PS D:\A-yulequ\python\wusir\git_learn\my01-soft> dir


    目录: D:\A-yulequ\python\wusir\git_learn\my01-soft


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          2024/8/8      8:35             16 access.log
-a----          2024/8/8      8:34             13 my04.txt
-a----          2024/8/8      8:34             13 my05.cmd
-a----          2024/8/8      8:35             16 other.log
-a----          2024/8/8      8:34              4 test.txt


PS D:\A-yulequ\python\wusir\git_learn\my01-soft> echo access.log >.gitignore
PS D:\A-yulequ\python\wusir\git_learn\my01-soft> type .\.gitignore
access.log
```



#### win电脑命令

##### 帮助

```
copy /?
系统自带的参数帮助
```

##### 文件夹

```
mkdir git_learn
创建一个名为git_learn的文件夹
cd git_learn
进入到该文件夹

dir /a
查看被隐藏的文件
dir
查看当前目录的子目录
mkdir git_learn
创建一个名为git_learn的文件夹
cd git_learn
进入到该文件夹
cls
清空命令行
echo "wo丢的" >my01.txt
创建文件
type my01.txt
查看文件
ren my02.txt test.txt
重命名文件
```

##### 文件

```
echo "wo丢的" >my01.txt
创建文件
type my01.txt
查看文件
ren my02.txt test.txt
重命名文件
del .\my01.txt
```

##### 清空命令行

```
cls
清空命令行
```

