# Git协作学习笔记

## 目录
1. [核心概念](#核心概念)
2. [基础操作](#基础操作)  
3. [分支管理](#分支管理)
4. [团队协作](#团队协作)
5. [冲突解决](#冲突解决)
6. [面试要点](#面试要点)
7. [命令速查](#命令速查)

---

## 核心概念

### Git是什么
Git是分布式版本控制系统，每个人都有完整的代码历史。

### 四个区域
```
工作区 --add--> 暂存区 --commit--> 本地仓库 --push--> 远程仓库
      <-checkout-     <-reset-           <-pull-
```
- **工作区**: 正在编辑的文件
- **暂存区**: 准备提交的文件  
- **本地仓库**: 本地版本历史
- **远程仓库**: 团队共享仓库

### 文件状态
- **已修改**: 文件改了但没暂存
- **已暂存**: 文件在暂存区
- **已提交**: 文件保存到仓库

---

## 基础操作

### 配置Git
```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"



```
### 日常流程

# 初始化仓库
git init

```bash
# 查看状态
git status

# 添加文件
git add .              # 添加所有文件
git add 文件名         # 添加指定文件

# 提交
git commit -m "提交说明"

# 推送
git push origin main
```

### 获取代码
```bash
git clone 仓库地址      # 第一次获取
git pull origin main   # 更新代码
```

### 查看历史
```bash
git log --oneline      # 简洁查看历史
git show 提交ID        # 查看具体提交
```

---

## 分支管理

### 分支操作
```bash
# 查看分支
git branch            # 本地分支
git branch -a         # 所有分支

# 创建分支
git checkout -b 分支名

# 切换分支
git checkout 分支名

# 删除分支
git branch -d 分支名
```

### 合并分支
```bash
git checkout main     # 切到主分支
git merge 功能分支    # 合并功能分支
```

### merge vs rebase
- **merge**: 保留分支历史，有合并记录
- **rebase**: 线性历史，看起来更清晰
- **建议**: 功能分支用merge，个人整理用rebase

---

## 团队协作

### GitHub Flow
1. 从main创建功能分支
2. 开发功能并提交
3. 推送分支到远程
4. 创建Pull Request
5. 代码审查
6. 合并到main

### 实际流程
```bash
# 1. 更新主分支
git checkout main
git pull origin main

# 2. 创建功能分支
git checkout -b feature/登录功能

# 3. 开发并提交
git add .
git commit -m "feat: 添加登录功能"

# 4. 推送分支
git push origin feature/登录功能

# 5. 在GitHub创建PR
# 6. 合并后清理
git checkout main
git pull origin main
git branch -d feature/登录功能
```

### 提交规范
```
类型: 简短描述

详细说明(可选)
```

常用类型：
- feat: 新功能
- fix: 修bug
- docs: 文档
- style: 格式
- refactor: 重构

---

## 冲突解决

### 什么是冲突
多人改同一文件的同一地方，Git不知道要哪个。

### 冲突标记
```
<<<<<<< HEAD
你的代码
=======
别人的代码
>>>>>>> 分支名
```

### 解决步骤
```bash
# 1. 查看冲突文件
git status

# 2. 编辑文件，删除标记，保留正确代码
# 3. 标记已解决
git add 冲突文件

# 4. 完成合并
git commit
```

### 预防冲突
- 经常同步: `git pull origin main`
- 小步提交
- 避免同时改相同文件

---

## 面试要点

### 必会问题

**Git和SVN区别？**
- Git分布式，SVN集中式
- Git本地有完整历史
- Git分支更轻量

**reset三种模式？**
- `--soft`: 只撤销提交
- `--mixed`: 撤销提交和暂存(默认)
- `--hard`: 撤销所有，回到指定状态

**如何撤销？**
```bash
git checkout -- 文件    # 撤销工作区
git reset HEAD 文件      # 撤销暂存区
git revert 提交ID       # 安全撤销已推送的
```

### 实战场景

**误提交敏感文件？**
```bash
git filter-branch --index-filter 'git rm --cached --ignore-unmatch 敏感文件' HEAD
```

**修改提交信息？**
```bash
git commit --amend -m "新信息"   # 最后一次
git rebase -i HEAD~3           # 多个提交
```

**找bug提交？**
```bash
git bisect start
git bisect bad      # 当前有bug
git bisect good v1.0 # v1.0正常
# 测试标记，直到找到
git bisect reset
```

---

## 命令速查

### 基础
```bash
git status              # 状态
git add .               # 暂存所有
git commit -m "信息"    # 提交
git push origin main    # 推送
git pull origin main    # 拉取
```

### 分支
```bash
git branch              # 查看分支
git checkout -b 分支名  # 创建切换
git merge 分支名        # 合并
git branch -d 分支名    # 删除
```

### 撤销
```bash
git checkout -- 文件    # 撤销修改
git reset HEAD 文件      # 撤销暂存
git reset --soft HEAD~1  # 撤销提交
git revert 提交ID       # 安全撤销
```

### 查看
```bash
git log --oneline       # 历史
git diff                # 工作区差异
git diff --cached       # 暂存区差异
git remote -v           # 远程仓库
```

### 高级
```bash
git stash               # 暂存工作
git stash pop           # 恢复暂存
git tag v1.0           # 打标签
git cherry-pick 提交ID  # 挑选提交
```

---

## 学习建议

### 新手路径 (2周)
1. **第1-3天**: 理解概念，配置Git
2. **第4-7天**: 练习基础命令
3. **第8-10天**: 学会远程操作  
4. **第11-14天**: 掌握分支和冲突

### 推荐资源
- [廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600) - 中文经典
- [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN) - 可视化练习
- [GitHub](https://github.com) - 实战练习

### 最佳实践
1. 每天开始先 `git pull`
2. 小功能小提交
3. 提交信息要清楚
4. 用分支开发功能
5. 重要代码要review

---

## 总结

Git核心就是：
1. 理解四个区域和文件状态
2. 熟练基础操作：add、commit、push、pull
3. 会用分支开发功能
4. 能解决冲突
5. 掌握团队协作流程

**记住：多练习，Git是用出来的！**

---

*更新时间: 2025年7月29日*
