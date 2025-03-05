# GitHub 快速入门指南

## 基本概念

GitHub 是一个基于 Git 的代码托管平台，帮助开发者存储和管理代码，并与他人协作开发项目。

- **仓库(Repository)**: 项目的存储空间，包含所有文件和修改历史
- **分支(Branch)**: 代码的独立开发线，可以安全地进行实验而不影响主代码
- **提交(Commit)**: 对文件的保存点，记录了修改内容和时间
- **拉取请求(Pull Request)**: 请求将你的修改合并到他人的项目中
- **Fork**: 复制他人的仓库到你自己的账户下

## 第1步：注册与设置

1. 访问 [github.com](https://github.com) 注册账号
2. 下载并安装 Git:
   - Windows: 下载 [Git for Windows](https://git-scm.com/download/win)
   - Mac: 使用 `brew install git` 或下载安装包
   - Linux: 使用 `sudo apt install git` 或适合你发行版的命令

3. 设置你的 Git 身份:
```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

## 第2步：创建第一个仓库

### 在网站上创建:
1. 登录 GitHub 后，点击右上角 "+" 图标，选择 "New repository"
2. 输入仓库名称，添加描述(可选)
3. 选择公开或私有
4. 勾选 "Initialize this repository with a README"
5. 点击 "Create repository"

### 或在本地创建后推送:
```bash
# 创建文件夹并初始化为Git仓库
mkdir 项目名称
cd 项目名称
git init

# 添加README文件
echo "# 项目名称" > README.md
git add README.md
git commit -m "初始提交"

# 链接到GitHub并推送
git remote add origin https://github.com/你的用户名/仓库名.git
git push -u origin main
```

## 第3步：基本Git操作

### 克隆仓库到本地:
```bash
git clone https://github.com/用户名/仓库名.git
cd 仓库名
```

### 日常工作流程:
```bash
# 查看当前状态
git status

# 创建并切换到新分支
git checkout -b 分支名

# 编辑文件...

# 添加修改的文件
git add 文件名    # 添加特定文件
git add .        # 添加所有修改

# 提交修改
git commit -m "修改描述"

# 推送到GitHub
git push origin 分支名
```

### 获取最新代码:
```bash
# 切换到main分支
git checkout main

# 拉取最新更改
git pull
```

## 第4步：协作与合并

1. **创建Pull Request**:
   - 在GitHub网站上打开你的仓库
   - 切换到你的分支
   - 点击 "Compare & pull request"
   - 填写标题和描述
   - 点击 "Create pull request"

2. **合并Pull Request**:
   - 审查代码变更
   - 如果没有冲突，点击 "Merge pull request"
   - 点击 "Confirm merge"

3. **处理冲突**:
   - 如果有冲突，GitHub会提示
   - 可以在网站上解决简单冲突
   - 复杂冲突需要在本地解决:
   ```bash
   git checkout main
   git pull
   git checkout 你的分支
   git merge main
   # 解决冲突后
   git add .
   git commit -m "解决合并冲突"
   git push origin 你的分支
   ```

## 常用命令速查表

```bash
# 基本操作
git clone [url]            # 克隆仓库
git status                 # 查看状态
git add [file]             # 添加文件到暂存区
git commit -m "[message]"  # 提交更改
git push origin [branch]   # 推送到远程
git pull                   # 拉取最新代码

# 分支操作
git branch                 # 列出分支
git branch [name]          # 创建分支
git checkout [name]        # 切换分支
git checkout -b [name]     # 创建并切换分支
git merge [branch]         # 合并分支
git branch -d [name]       # 删除分支

# 历史查看
git log                    # 查看提交历史
git log --oneline          # 简洁历史
git diff                   # 查看未暂存的更改
```

## 推荐工具

如果命令行让你感到困难，可以尝试这些GUI工具:

- **GitHub Desktop**: [desktop.github.com](https://desktop.github.com) - 官方客户端，适合初学者
- **Visual Studio Code**: 内置Git支持的代码编辑器
- **GitKraken**: 功能强大的Git客户端

## 文件操作指南

### 添加文件
```bash
# 创建新文件
touch 文件名.扩展名
# 或使用编辑器创建并编辑文件

# 将文件添加到Git跟踪
git add 文件名.扩展名

# 提交新文件
git commit -m "添加新文件"

# 推送到远程仓库
git push origin 分支名
```

### 删除文件
```bash
# 方法1: 使用Git命令删除
git rm 文件名.扩展名
git commit -m "删除文件"
git push origin 分支名

# 方法2: 手动删除后告知Git
rm 文件名.扩展名
git add -u  # 更新已跟踪的文件状态
git commit -m "删除文件"
git push origin 分支名
```

### 重命名文件
```bash
# 使用Git命令重命名
git mv 原文件名 新文件名
git commit -m "重命名文件"
git push origin 分支名
```

## 仓库管理

### 删除仓库
1. 在GitHub网站上:
   - 进入仓库页面
   - 点击"Settings"(设置)
   - 滚动到底部"Danger Zone"(危险区域)
   - 点击"Delete this repository"(删除此仓库)
   - 输入仓库名确认删除

### 修改仓库设置
1. 在GitHub网站上:
   - 进入仓库页面
   - 点击"Settings"(设置)
   - 可以修改:
     - 仓库名称
     - 描述
     - 默认分支
     - 可见性(公开/私有)
     - 协作者和权限

### 管理远程仓库连接
```bash
# 查看远程仓库
git remote -v

# 添加远程仓库
git remote add 名称 仓库URL

# 修改远程仓库URL
git remote set-url 名称 新URL

# 删除远程仓库连接
git remote remove 名称
```

## 常见问题解决

1. **推送被拒绝**
   ```bash
   git pull origin main
   git push origin main
   ```

2. **撤销最后一次提交**
   ```bash
   git reset HEAD~1    # 保留更改
   git reset --hard HEAD~1  # 丢弃更改
   ```

3. **暂存工作区**
   ```bash
   git stash       # 暂存当前工作
   git stash pop   # 恢复暂存的工作
   ```

4. **查看远程仓库**
   ```bash
   git remote -v
   ```

