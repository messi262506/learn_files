# 毕业设计论文 GitHub 版本管理教程

## 前置准备

- Git 已安装：`E:\Program Files\Git`（版本 2.54.0）
- 打开方式：桌面右键 → **Git Bash Here**

---

## 一、配置身份（只做一次）

```bash
git config --global user.name "你的姓名"
git config --global user.email "你的邮箱@example.com"
```

验证：
```bash
git config --global user.name
git config --global user.email
```

---

## 二、整理文件夹

在桌面创建统一文件夹 `毕业设计-完整版`：

```bash
cd ~/Desktop
mkdir 毕业设计-完整版
```

然后将以下文件/文件夹移入：
- `毕业论文.docx`
- `毕业论文.pdf`
- `22级软件2班...2202050244.docx`
- `2202050244...` 文件夹（证明材料）
- `前期准备` 文件夹（开题报告、任务书等）
- `毕业设计附件` 文件夹

---

## 三、初始化 Git 仓库

```bash
cd ~/Desktop/毕业设计-完整版
git init
```

---

## 四、创建 .gitignore（排除临时文件）

```bash
cat > .gitignore << 'EOF'
# Word 临时文件
~$*.docx
~$*.doc
~WRL*.tmp
*.tmp

# 系统文件
Thumbs.db
Desktop.ini
EOF
```

---

## 五、第一次提交

```bash
git add .
git status
git commit -m "初始版本：论文及全部配套材料"
```

---

## 六、推送到 GitHub

### 6.1 创建 GitHub 仓库

1. 打开 [github.com](https://github.com) 登录
2. 右上角 **"+"** → **"New repository"**
3. 仓库名填 `graduation-thesis`
4. 选择 **Private**（私人仓库）
5. **不要勾选** "Add a README file"
6. 点击 **Create repository**

### 6.2 关联并推送

```bash
git remote add origin https://github.com/你的用户名/graduation-thesis.git
git branch -M main
git push -u origin main
```

---

## 七、日常使用流程

每次修改论文后，三步走：

```bash
cd ~/Desktop/毕业设计-完整版

# 第1步：查看改动
git status

# 第2步：暂存并提交
git add .
git commit -m "描述本次改了什么"

# 第3步：推送到 GitHub
git push
```

### 提交信息示例

```bash
git commit -m "完成摘要和关键词"
git commit -m "完成第三章需求分析"
git commit -m "根据导师意见修改第二章"
git commit -m "调整格式，添加参考文献"
```

---

## 八、常用命令速查

| 命令 | 作用 |
|------|------|
| `git status` | 查看哪些文件有改动 |
| `git log --oneline` | 查看提交历史 |
| `git diff` | 查看具体改了什么内容 |
| `git pull` | 拉取远程最新版本 |
| `git checkout 提交ID -- 文件名` | 恢复某个文件到历史版本 |
| `git reset --hard 提交ID` | 回退整个仓库到某个版本（谨慎使用） |

---

## 九、分支工作流（可选进阶）

如果导师要批注修改，可以开新分支，改完再合并：

```bash
git checkout -b 导师修改第一轮    # 创建并切换到新分支
# ... 修改论文 ...
git add .
git commit -m "按导师意见修改完毕"
git checkout main                # 切回主分支
git merge 导师修改第一轮          # 合并修改
git push
```

---

## 十、注意事项

- **每次写完一个章节就提交一次**，不要攒到最后
- **先 commit 再 push**，commit 是本地保存，push 是上传到 GitHub
- **提交前用 `git status` 检查**，确保没有提交不该提交的文件
- **不要在 GitHub 网页上直接编辑**，否则本地和远程会产生冲突
- **大文件**：Word 的 `.docx` 是二进制文件，Git 无法显示具体修改内容（无法看 diff），但可以完整保存每个版本，随时回退下载
