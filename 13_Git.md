## 1,起步

Git是一个开源的分布式版本控制系统

Git之所以快速和高效,主要依赖于他的两个特性:

1,直接记录快照,而非差异比较

2,近乎所有的操作都是本地执行

Git快照:在原有文件版本的基础上重新生成了一份新的文件,类似于备份.若文件没有修改,Git不再重新存储该文件,二十只保留一个链接指向去之前存储的文件.

Git中的三个区域: **工作区,暂存区,Git仓库**

Git中的三种状态:

已修改:(modified)表示修改了文件,但还没将修改的结果放到暂存区

已暂存:(staged)表示对已修改文件的当前版本做了标记,使之包含在下次提交的列表中

已提交:(committed) 表示文件已经安全的保存在本地的Git仓库中.

## 2,Git基础

git config --global user.name "xxx"

git config --global user.email "xxx" :设置自己的用户名和邮箱

git config --list --global :查看所有的全局配置项

git config user.name:查看指定的全局配置项

git help config:打开帮助手册



git init: 在现有目录中初始化Git仓库

git status : 查看文件状态

git status -s  以简短的形式查看文件状态

git add  :1可以用它来开始跟踪文件 2,把已跟踪的,且已修改的文件放到暂存区 3,把有冲突的文件标记为已解决状态

git commit -m:将暂存区的等待被提交的文件提交到仓库保存

git checkout -- 文件:撤销对文件的修改,恢复到仓库中文件的状态,撤销后不能恢复.

git add . :一次性的将所有的新增或修改过的文件加入暂存区中

git reset HEAD 要移除的文件名称: 从缓存区中移除对应的文件

git reset HEAD  . :移除暂存区中所有的文件

git commit -a -m:跳过暂存区,直接把所有已跟踪过的文件暂存起来一并提交,从而跳过 git add 步骤

git rm -f 文件名:从仓库和工作区同时移除文件

git rm --cached 文件名:只移除仓库中的文件,保留工作区的文件

**忽略文件:**创建一个名为.gitignore的配置文件,列出要忽略的文件的匹配模式

1,以#开头的时注释

2,以/结尾的时目录

3,以/开头的时防止递归

4,以!开头的是取反

5,可以使用glob模式进行文件和文件夹的匹配

**glob模式:** 简化后的正则表达式

1,*:表示匹配零个或多个任意字符

2,[abc]匹配任何一个列在方括号中的字符

3,? 只匹配一个任意字符

4,[0-9] 匹配0-9之间的任意字符

5,两个**表示匹配任意中间目录



git log :按时间顺序列出所有提交历史,最近的提交排在最上面

git log -2:展示最新的两条提交历史,数字可以按需填写

git log -2 --pretty=oneline:在一行上展示最近两条提交历史

git log -2 --pretty=format:"%h \|  %an | %ar | %s" :在一行上展示最近两条提交历史信息,并自定义输出的格式"%h 提交的简写哈希值  %an作者名字 %ar 作者修订日期,按多久i以前的方式显示 %s提交说明

回退到指定版本:

git log --pretty=oneline:在一行上展示所有的提交历史.

git reset --hard <CommitID> :根据指定的提交ID回退到指定版本

git reflog --pretty=oneline :在旧版本中查看命令操作的历史 

## 3,Github

**生成SSH key:**

ssh-keygen -t rsa -b 4096 -C"704250133@qq.com"

连续敲击三次回车,即可在C:\Users\用户名\.ssh目录总生成id_rsa和id_rsa.pub两个文件

**配置SSH key:**

**检测Github的SSH key是否配置成功**

ssh -T git@github.com

**将远程仓库克隆到本地:**

git clone 远程仓库地址

## 4,Git分支

