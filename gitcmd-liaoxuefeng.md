## git-cmd 

​               ——廖雪峰 www.liaoxuefeng.com

### 【操作流程】：

#### 一、本地仓库：

1. ##### 安装：www.git-scm.org

   ```
   // 安装好后，需增加两条代码，绑定用户名和邮箱地址
   $ git config --global user.name "xxx"
   $ git config --global user.email "xxx@xxx.com"
   ```

   参数1：--global 表示本机所有git仓库都用这个配置。

2. ##### 创建版本库： 

   - 第一步：先创建目录：mkdir

   ```
   // 在创建前，最好先切换到合适的目录
   $ cd xxx               // 先切换到合适目录
   $ mkdir learngit       // 创建learngit的目录
   $ cd learngit          // 切换到learngit目录
   $ pwd                  // 显示当前目录
   /Users/xxx/learngit
   ```

   - 第二步：将目录变成可以管理的git仓库：git init

   ```
   $ git init
   ```

   补充：ls -ah，可以看到目录下多了一个.git的文件，默认是隐藏的。

3. ##### 查看

   - 查看当前状态：git status
   - 查看具体修改的内容：git diff + 文件名
   - 查看历史记录： git log 
   - 查看当前版本内容：cat + 文件名
   - 查看过去的操作命令：git reflog

   ```
   $ git status             // 显示修改、删除的文件等
   $ git diff ReadMe.md     // 显示具体的操作内容
   $ git diff HEAD -- ReadMe.md // 查看工作区与版本库里最新版本的区别
   $ git log                // 显示所有版本的master id、作者、邮箱和日期，以及修改的描述
   $ git log --pretty=oneline // 只显示一个
   $ cat ReadMe.md            // 查看具体内容
   $ git reflog               // 记录了过去每一个次的命令
   ```

4. ##### 提交到仓库：

   - 工作区：修改文件的地方，如ReadMe.md
   - 提交到暂存区：git add + <文件名>
   - 提交到master分支区：git commit -m " string... "
   - 补充：可以多次add，再一次commit。（add与commit是一种组合）

   ```
   $ git add ReadMe.md      // 提交到暂存区
   $ git commit -m " adding gitcmd "
   ```

5. ##### 版本回退：reset

   - 当前版本：HEAD
   - 上一个版本：HEAD^
   - 上上一个版本：HEAD^^
   - 前100个版本：HEAD~100
   - 补充：HEAD指向哪个版本，则哪个版本就是当前版本。
   - 分支上回退：git reset --hard + <版本或id> 

   ```
   $ git reset --hard HEAD^  // 回退到上一个版本 
   $ git reset --hard xxx  // xxx指的是commit id，只需要写几位即可
   ```

6. ##### 撤销修改：

   - 工作区撤销：git checkout -- + <文件名>
   - 暂存区撤销：git reset HEAD + <文件名>

   ```
   $ git checkout -- ReadMe.md  // 将工作区的修改全部撤销 
   $ git reset HEAD ReadMe.md   // 将提交到暂存区的修改撤销掉，重新回到工作区
   ```

   补充：如果修改的文件已经提交到暂存区，则退回到暂存区前的状态；如果还没有提交到暂存区，则退回到和版本库一样。如果修改已经提交到分支，可以用“版本回退reset”处理。

7. ##### 删除文件：

   - 直接在文件管理器删除：rm + <文件名>
   - 用git rm删除：git rm + <文件名>

   ```
   $ rm ReadMe.md
   $ git rm ReadMe.md
   ```

#### 二、远程仓库：

1. 创建SSH kye：

   ```
   $ ssh-keygen -t rsa -C "youremail@example.com"
   ```

   补充：将生成的.pub文件的内容复制粘贴到 “github——>设置——>SSH——>new SSH key——xxx"

2. 

