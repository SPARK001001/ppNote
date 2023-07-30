git 是一种开源分布式版本控制系统，用于跟踪和管理代码的修改历史。常见托管服务有github.gitlab.bitbucket



 - 创建分支: git branch / git checkout -b 

  - 切换分支: git checkout 

  - 合并分支：

      -  git merge : 用于将**其他**分支的修改合并到当前分支，并保留各分支的提交历史，产生合并提交

      - git rebase: 用于将**当前**分支的修改提交历史应用到另一个分支上，将分支合并成一条直线，保持提交历史的间接和连续性

      - ```
        将feature分支合并到develop
        git checkout feature
        git rebase develop
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

  - 回滚： git revert，指撤销最近一次的提交。 例如提交A,B,C, D，执行git revert D会创建一个新的提交，撤销D引入的修改，代码库回滚到提交C的状态
  - 版本回退： git reset, 将Head指针和分支指针移动到指定的提交，版本回退会丢失回退点之后的提交历史。git reset --hard B 将回退到B的状态。不会新建分支。