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

1. ##### 创建SSH kye：

   ```
   $ ssh-keygen -t rsa -C "youremail@example.com"   // 注意：ssh-keygen 是连体的
   ```

   【补充】：将生成的.pub文件(默认在c:/user/Aministrator/.ssh/)的内容复制粘贴到 “github——>设置——>SSH——>new SSH key——xxx"

   【特别注意】：新手在生成SSH 的时候不要去设置文件名和密码，否则会连接不了远程，需要多配置很多的信息。

2. ##### 本地连接到远程

   ```
   $ git remote add origin git@github.com:michaelliao/learngit.git
   ```

3. ##### 把本地所有内容推送到远程：

   - 推送push：与 add、commit组合成三步曲。


   ```
$ git push -u origin master
   ```

   参数：-u，第一次推送时才需要加，目的是将本地的master分支与远程master关联起来。

   补充：origin是远程库的名字，也可以取任意名称。

4. ##### 删除远程库：意外连接错地址时可用

   - 删除：git remove rm + <name>

   - 删除的意思：解除本地 与远程 的绑定关系。


   ```
$ git remove -v  // 建议删除远程库前先操作这一步
-> origin git@github.com:Aoo---.git (fetch)    // 输出的内容
-> origin git@github.com:Aoo---.git (push)     // 输出的内容
$ git remove rm origin
   ```

5. ##### 从远程克隆：建议开发时，先建立远程库！

   - 新建repo：勾选Initialize ...，可生成README.md文件；

   - 克隆clone：记得先切换目录

     ```
     $ git clone git@github.com:Aoo---.git // ssh协议
     $ git clone https://github.com/Aoo---.git // https协议
     ```

### 三、分支管理：

1. ##### 创建分支：git checkout -b + <name>

   ```
   $ git checkout -b dev  // 创建一个dev的分支
   
   // 有了参数-b，等价于下面两条命令
   $ git branch dev       // 创建不切换到dev
   $ git checkout dev     // 切换到dev分支
   ```

   参数：-b 表示创建并切换。可以对比工作区撤销也是用的checkout。

2. ##### 查看：

   - 查看当前所有分支：git branch

     ```
     $ git branch  // 列出所有分支，有星号*标记的，指代当前分支
     -> * dev
     -> main
     ```

   - 对文本【修改】 + 【添加+提交+切换】

     ```
     在README.md中添加内容进行修改："xxxxxxxxx"
     $ git add README.md                    // add——>添加到暂存区
     $ git commit -m "adding branch dev"    // commit——>提交到分支
     
     $ git checkout master  // 分支操作结束后，切换回主线    
     ```

3. ##### 合并分支：git merge + <name>

   ```
   $ git checkout master  // 合并前，确保先切回主分支
   $ git merge dev        // 将主分支与dev分支合并  
   ```

4. ##### 删除分支：git branch -d + <name>

   ```
   $ git branch -d dev    // 删除分支dev
   $ git branch           // 查看所有分支，则只剩下master
   ```

5. ##### 切换分支：为了避免混淆，新的切换命令用：git switch + <name>

   ```
   $ git switch -c dev        <===> git checkout -b dev
   $ git switch master        <===> git checkout master
   ```

6. ##### 合并冲突的处理：

   - 当主线和分支都对同一个文件修改时，合并会出错，需要重新打开文件，删除github自动添加的一堆符号：<<<<<< ==== >>>>>>>，这是区分不同分支的标记。

   ```
   //当前为master，合并分支featurel
   $ git merge feature1  // 出现冲突
   
   // 对文本修改后，重新添加和提交
   $ git add README.md
   $ git commit -m "fixed"
   
   // 删除分支
   $ git branch -d featurel
   ```

7. ##### 分支管理策略：

   - --no-ff：禁用Fast forward模式。可以在merge时，生成一个commit。默认是Fast forward模式，缺点是看不出曾经做过合并。
   - ![image-20221213202444550](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221213202444550.png)
   - master：该分支应该非常稳定，只用来发布正式的新版本；
   - dev：每个人都从该分支clone到本地干活，完成任务再合并；

8. Bug分支：

   - 储存当前的工作现场：git stash

   - ```
     $ git stash     // 比如当前在dev，为了先修改bug，只能把当前工作现场先保存起来。
     ```

   - 创建临时分支：比如在master分支上修复bug

     ```
     $ git switch master            // 切换到主分支
     $ git checkout -b issue-101    // 新建bug的分支
     
     $ git add README.md              // 修改完bug文件后，添加  
     $ git commit -m "fix issue-101"  // 提交
     
     $ git swich master               // bug处理完后，切回主分支
     $ git merge --no-ff -m "merge bug fix 101" issue-101   // 合并临时的bug分支
     
     $ git switch dev     // 切回原来保存的现场
     $ git status         // 查看当前状态
     $ git stash list     // 查看工作现场在哪里
     
     // 恢复并删除stash内容
     $ git stash apply    //恢复
     $ git stash drop     //删除   
     $ git stash pop      //恢复+删除 等价于上面两条命令
     
     // 恢复指定的stash
     $ git stash apply stash@{0}
     
     // 若dev也有和master一样的bug需要修复，只需要check-pick + id 
     git check-pick 211a5c 
     ```

     总结：保存工作现场git stash，修复bug，回到工作现场git check-pick。

9. feature分支：功能分支

   ```
   git swith -c feature-vulcan   // 新建一个功能分支
   ... 开发完一个vulcan.py
   git add vulcan.py
   git commit -m "add feature vulcan"
   
   git switch dev               // 切换到开发分支，准备合并，然而没执行合并，而是要取消
   git branch -d feature-vulcan // 错误！！！
   git branch -D feature-vulcan // 正确！！！未合并就要强制执行删除操作，需要用大D
   ```

   总结：丢弃未合并的功能 git  branch -D + <branch name>

10. 多人协作：

    ```
    // 查看远程库信息
    git remote       // 粗略
    git remote -v    // 详细
    
    // 推送分支：本地提交到远程，需要写明提交哪个分支
    // 通常只需要推送master和dev分支，bug和feature一般不需要推送
    git push origin master
    git push origin dev 
    
    // 抓取分支：
    $ git clone git@github.com:Aoo...git   
    $ git branch 
    -> *master         					// 只能看到主分支
    $ git checkout -b dev origin/dev      // 必须自己再创建远程的dev到本地
    
    // 当推送出现冲突时，先git pull，再本地合并merge，再解决冲突，再推送git push
    // 同时，拉取需要先指定本地与远程的链接,通常失败会提示no tracking information
    $ git branch --set-upstream-to=origin/dev dev       // 没有这一步，则拉取会失败
    $ git pull                                          // 从远程抓取分支回本地
    
    $ git commit -m "fix env conflict"   // 修复冲突
    $ git push origin dev
    ```

    总结：推送 git push origin + <branch name>

11. Rebase：重设基点

    ```
    git rebase         // 效果是将本地未push的分支提交历史整理成一条直线
    ```

### 四、标签管理：

1. 创建标签：

   ```
   $ git tag v1.0                  					// 创建普通标签
   $ git tag -a v1.0 -m "version 1.0 released" 142s5a    // 创建带有说明的标签
   
   $ git log --pretty=oneline --abbrev-commit // 找id
   $ git tag v0.9 5482s5a       			  // 忘记打标签，可以找出id，再重新打上
   ```

2. 查看所有标签

   ```
   $ git tag   
   ```

3. 标签信息：git show + <tag-name>

   ```
   $ git show v1.0 
   ```

4. 操作标签：

   - 删除标签：

     ```
     $ git tag -d v1.0    // 删除本地标签
     
     $ git tag -d v1.0
     $ git push origin :refs/tags/v1.0    // 这两步一起才能从远程库里删除标签
     ```

   - 推送标签到远程
   $ git push origin v1.0     // 推送指定标签
   $ git push origin --tags   // 推送全部标签

