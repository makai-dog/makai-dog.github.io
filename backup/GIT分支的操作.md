# GIT分支的操作

在开发无人车的ROS包时,我们要在分支(即特性分支)上进行修改,合并到main主分支(主干分支)上

## 具体操作

1. 显示分支一览表

```bash
git branch
```

2. 创建和切换到新的分支feature-A

```bash
git branch feature-A
```

3. 合并分支的更改,到主干分支上
**假设特性分支已经实现完毕,想将它合并到主干分支main中**

```bash
git checkout main
switched to branch 'main'
```

```bash
git merge --no-ff feature-A
```

**在合并时加上--no-ff参数，因为了在历史记录中明确记录下，本次分支合并，所以需要创建合并提交**

4. 回溯历史版本

```bash
git reset --hard 目标时间点的哈希值
```
