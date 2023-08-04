git 是一种开源分布式版本控制系统，用于跟踪和管理代码的修改历史。常见托管服务有github.gitlab.bitbucket



 - 创建分支: git branch / git checkout -b 

  - 切换分支: git checkout 

  - 合并分支：

      - git merge : 用于将**其他**分支的修改合并到当前分支，并保留各分支的提交历史，产生合并提交

           -  git merge --squash ftr_p: 合并其他分支，但不保留其他分支的提交记录。需要commit来提交新记录

      - git rebase: 用于将其他分支的修改提交历史应用到当前分支上，将分支合并成一条直线，保持提交历史的间接和连续性。不产生新的提交

      - ```
           A---B---C   feature
          /
         D---E---F---G  develop
         如果在feature分支上执行git rebase develop，则Git会将feature分支的提交历史应用到develop分支的顶部
          D---E---F---G---A'---B'---C'  feature (rebased)
                            develop
          
        ```

      - 

  - 解决冲突:

      - 拉取最新代码 git pull
      - 查看冲突，特殊标记 《《《head  ===>>>
      - 手动解决冲突
      - 保存修改
      - 添加解决后的代码： git add 
      - 提交解决 git commit
      - 继续合并或拉取。

- 回滚和版本回退：

  - 回滚： git revert，指撤销某次提交。 例如提交A,B,C, D，执行git revert D会**创建一个新的提交**，撤销D引入的修改，代码库回滚到提交C的状态。保留历史的提交记录
  - 版本回退： git reset, 将Head指针和分支指针移动到指定的提交，版本回退会丢失回退点之后的提交历史。git reset --hard B 将回退到B的状态。不会新建分支。

- 标签管理

  - 轻量标签( lightweight tags)： git tag v1.0.0
  - 附注标签 （annotated tage）： git tag v.1.0.0 -m "tag message"
- git tag ： 列出所有标签
  
  - git show v1.0.0: 查看附注标签的详情
  
- 其他：

     - 丢弃当前本地的修改： git reset --hard
     - 删除分支test：先切换到其他分支。在 git branch -d test。 或-D 强制删除
     - 删除远程分支origin/test: git push origin --delete test
     - git diff: 比较当前工作区和暂存区的差别，也即是提交和未提交的区别; git diff commit1 commit2,比较两提交之间的差别； git diff dev, 比较当前分支与dev分支的区别