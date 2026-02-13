# 📦 如何将本地文件夹上传到 GitHub 新仓库

这是一个极简的“备忘单”，当你有一个本地文件夹需要变成 GitHub 项目时，照着做就行。

## 前提条件
1. 在 GitHub 网站上**新建一个空仓库**（Create a new repository）。
2. 注意：创建时**不要勾选** "Add a README file" 或 "Add .gitignore"，保持仓库为空（这样最简单）。

---

## 操作步骤

在你的本地文件夹中打开终端（Terminal / Git Bash / PowerShell），依次运行以下命令：

### 1. 初始化 (Initialize)
把当前文件夹变成 Git 仓库。
```bash
git init
```

### 2. 暂存文件 (Stage)
把文件夹里的所有文件交给 Git 管理。
```bash
git add .
```

### 3. 本地提交 (Commit)
把文件保存为一个版本。
```bash
git commit -m "Initial commit"
```

### 4. 重命名分支 (Branch)
把分支名改为标准的 `main`（GitHub 默认主分支名）。
```bash
git branch -M main
```

### 5. 关联远程仓库 (Remote)
告诉 Git 你的代码要传到哪里去。
*(请把下面的 URL 换成你刚才在 GitHub 创建的那个仓库地址)*
```bash
git remote add origin https://github.com/<你的用户名>/<你的仓库名>.git
```

### 6. 推送代码 (Push)
把代码真正上传到 GitHub。
```bash
git push -u origin main
```

---

## 🎉 搞定！
以后你修改了文件，只需要运行这三步：
1. `git add .`
2. `git commit -m "修改了什么内容"`
3. `git push`
