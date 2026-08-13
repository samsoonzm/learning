# learning

用于日常学习开发

# GitHub 入门学习总结

日期：2026 年 8 月 13 日

## 一、今天完成了什么

今天完成了 GitHub 的第一轮完整入门实践：

1. 了解 Git、GitHub 和仓库的基本作用。
2. 在 GitHub 上创建仓库。
3. 配置本机 Git 提交身份。
4. 使用 HTTPS 地址将远程仓库克隆到电脑。
5. 了解 Personal Access Token（PAT）的用途。
6. 成功克隆真实仓库 `samsoonzm/learning`。
7. 进入本地仓库并使用 `git status` 检查状态。
8. 理解 `add`、`commit`、`push`、Pull Request 和 Issues 的关系。

成功克隆时，终端显示过：

```text
Receiving objects: 100%
done.
```

进入仓库并检查状态时，显示：

```text
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

这说明本地仓库已经建立，并与 GitHub 上的 `main` 分支保持一致。

## 二、Git 和 GitHub 分别是什么

- **Git**：安装在电脑上的版本管理工具，用来记录文件变化和保存历史版本。
- **GitHub**：托管 Git 仓库的网站，用于备份代码、展示项目和团队协作。
- **Repository（仓库）**：一个项目的文件及其完整版本历史。
- **本地仓库**：电脑上的工作副本，可以编辑、运行和测试。
- **远程仓库**：GitHub 上的云端版本，常用远程名称是 `origin`。

基本关系：

```text
GitHub 远程仓库
      ↓ git clone / git pull
电脑上的本地仓库
      ↓ 编辑、add、commit
本地新版本
      ↓ git push
GitHub 远程仓库更新
```



## 三、核心命令和含义



### 1. `git clone`：第一次下载仓库

```bash
git clone https://github.com/samsoonzm/learning
```

作用：把 GitHub 上的仓库完整复制到电脑，包括项目文件和版本历史。

`clone` 通常只在第一次下载仓库时使用。以后同步更新一般使用 `git pull`。

### 2. `cd`：进入目录

```bash
cd learning
```

作用：让终端进入 `learning` 文件夹。它不会自动弹出 Finder 窗口。

查看当前路径：

```bash
pwd
```

查看当前目录里的文件：

```bash
ls
```

在 Finder 中打开当前目录：

```bash
open .
```



### 3. `git status`：检查当前状态

```bash
git status
```

作用：查看当前分支、哪些文件被修改、哪些修改已暂存，以及是否有内容等待提交。

这是最适合新手频繁使用的安全检查命令。不确定下一步时，可以先运行它。

### 4. `git add`：选择下次提交的内容

选择一个文件：

```bash
git add README.md
```

选择当前目录中的全部改动：

```bash
git add .
```

`git add` 的作用是把指定修改放进“暂存区”，也就是确定哪些内容要进入下一次版本快照。

它不会生成版本，也不会把内容上传到 GitHub。

### 5. `git commit`：保存本地版本快照

```bash
git commit -m "完善 README 使用说明"
```

作用：把暂存区里的内容保存成一个本地版本。

提交说明应清楚描述做了什么，例如：

```text
添加项目安装步骤
修复登录按钮无响应问题
更新 README 使用说明
```

尽量避免只写“修改”“update”等含义不清的说明。

### 6. `git push`：上传本地提交

```bash
git push
```

作用：把已经 `commit` 的本地版本上传到 GitHub。

注意：没有提交的文件不能靠 `push` 直接上传。必须先 `add`，再 `commit`，最后 `push`。

### 7. `git pull`：同步云端更新

```bash
git pull
```

作用：把 GitHub 上的新提交下载并合并到当前本地分支。

多人协作时，开始工作前通常先执行 `git pull`。

## 四、一次完整的日常修改流程

在已经克隆并进入仓库的情况下：

```bash
git pull
git status
# 使用编辑器修改文件
git status
git add README.md
git status
git commit -m "更新 README"
git push
```

可以记成：

```text
pull → 修改 → status → add → commit → push
```

其中：

- `pull`：先取得别人或云端的最新版本。
- 修改：在电脑上编辑文件。
- `status`：确认发生了什么变化。
- `add`：选择要提交的变化。
- `commit`：保存本地版本快照。
- `push`：上传到 GitHub。



## 五、分支和 Pull Request



### 分支是什么

分支是独立的开发路线。稳定的主分支通常叫 `main`。开发新功能时，可以先创建新分支，避免直接影响 `main`。

```bash
git switch -c update-readme
```

完成修改后：

```bash
git add README.md
git commit -m "完善 README"
git push -u origin update-readme
```



### PR 是什么

PR 是 Pull Request，表示：

> 我已经在一个分支完成修改，请检查这些变化，并考虑把它们合并到目标分支。

`push` 和 PR 不是一回事：

- `push`：把本地提交上传到 GitHub。
- PR：请求审查和合并两个分支之间的改动。
- `merge`：正式把 PR 中的修改并入目标分支。

团队协作流程：

```text
创建分支
  → 修改文件
  → add
  → commit
  → push 分支
  → 创建 PR
  → 代码审查和自动测试
  → merge 到 main
```

个人练习项目可以直接在 `main` 上 `push`，但通过分支和 PR 练习更接近正式团队工作方式。

## 六、Issues 是什么

Issue 是项目中的任务单或问题单，用于记录“需要解决什么”，但它本身不修改代码。

常见用途：

- 报告 Bug。
- 提出新功能。
- 记录待办任务。
- 讨论技术方案。
- 分配负责人和跟踪进度。

Issue 与代码工作的关系：

```text
Issue：描述问题或任务
  → 创建开发分支
  → 修改代码
  → commit 和 push
  → 创建 PR
  → 审查并 merge
  → 关闭 Issue
```

PR 描述中写：

```text
Closes #1
```

表示该 PR 合并后自动关闭编号为 `#1` 的 Issue。

简单区分：

- Issue：要解决什么？
- Branch：在哪里修改？
- Commit：保存了哪一批修改？
- Push：把提交上传到哪里？
- PR：这些修改是否可以合并？
- Merge：正式纳入目标分支。



## 七、今天实操中出现的错误



### 错误 1：直接照抄教程占位符

曾执行：

```bash
git clone https://github.com/你的用户名/hello-github.git
```

结果：

```text
Repository not found
```

原因：“你的用户名”和 `hello-github` 是教学示例，不是真实账号和仓库。

改进方法：从 GitHub 仓库页面点击绿色 **Code** 按钮，复制真实 HTTPS 地址，不要凭记忆拼写。

最终成功使用的真实地址是：

```bash
git clone https://github.com/samsoonzm/learning
```



### 错误 2：仓库名称猜错

曾尝试 `hello-github` 和 `learning-github`，但真实仓库名是 `learning`。

GitHub 地址必须准确符合：

```text
https://github.com/仓库所有者/仓库名
```

账号显示名、Git 提交作者名、GitHub 用户名和仓库名是不同概念，不能互相替代。

### 错误 3：把两条命令粘在同一行

配置用户名和邮箱时，两条 `git config` 命令一度连在了一起，因此 Git 输出了 `usage: git config...` 帮助信息。

正确方式是每次执行一条：

```bash
git config --global user.name "samsoonzm"
git config --global user.email "你的邮箱"
```

看到命令执行完并重新出现 `%` 提示符后，再输入下一条。

### 错误 4：把终端提示文字当成命令

曾把下面的提示手动输入终端：

```text
Username for 'https://github.com':
```

随后又单独输入 `samsoonzm`，结果出现：

```text
zsh: command not found: Username
zsh: command not found: samsoonzm
```

原因：`Username for...` 是 Git 在执行过程中显示的问题，不是一条命令。只有在 Git 自动显示该提示时，才输入用户名。

识别方法：

- 出现类似 `MacBook-Air ... %`：终端正在等待一条完整命令。
- 出现 `Username for...`：正在等待用户名回答。
- 出现 `Password for...`：正在等待 Token。



### 错误 5：混淆 GitHub 密码和 PAT

GitHub 的 HTTPS Git 操作不接受普通账户密码。在终端的 `Password` 位置，应粘贴 Personal Access Token（PAT）。

正确对应关系：

```text
Username：GitHub 用户名
Password：PAT，不是登录密码
```

Fine-grained PAT 应授权正确的仓库，并至少给 `Contents` 读取权限；需要推送时应给 `Read and write`。

Token 与密码一样敏感：

- 不要发送给别人。
- 不要贴进聊天或截图。
- 不要写进代码或提交到仓库。
- 如果泄露，立即在 GitHub 设置中撤销并重新创建。



### 错误 6：克隆失败后仍执行 `cd`

仓库克隆失败时，目标文件夹并未创建，因此执行：

```bash
cd hello-github
```

会得到：

```text
cd: no such file or directory
```

正确做法：先确认 `git clone` 出现成功信息，再执行 `cd 仓库名`。

### 错误 7：已经进入仓库后再次 `cd learning`

终端已经显示：

```text
MacBook-Air learning %
```

这代表当前就在 `learning` 文件夹。再次执行 `cd learning`，相当于寻找 `learning/learning`，所以报错。

改进方法：养成查看终端提示符，以及使用以下命令确认位置的习惯：

```bash
pwd
ls
```



### 错误 8：以为 `cd` 会弹出本地文件夹

`cd learning` 只是改变终端当前目录，不会打开 Finder。

如果需要在 Finder 中显示当前目录：

```bash
open .
```

如果安装并配置了 VS Code 命令，可以在编辑器中打开：

```bash
code .
```



## 八、容易混淆的概念对照


| 概念           | 实际作用            | 不会做什么             |
| ------------ | --------------- | ----------------- |
| `git clone`  | 第一次把整个远程仓库复制到本地 | 不会自动进入目录          |
| `cd`         | 改变终端当前目录        | 不会打开 Finder       |
| `git add`    | 选择下次提交的修改       | 不会保存版本或上传         |
| `git commit` | 创建本地版本快照        | 不会自动上传 GitHub     |
| `git push`   | 上传本地提交          | 不会提交尚未 commit 的修改 |
| `git pull`   | 获取并合并远程更新       | 不是第一次完整克隆仓库       |
| Issue        | 描述任务、问题或需求      | 不会直接修改代码          |
| PR           | 请求审查并合并分支       | 不等同于上传代码          |
| Merge        | 把改动正式并入目标分支     | 不等同于本地 commit     |




## 九、新手操作守则

1. 教程中的“你的用户名”“仓库名”等文字必须替换为真实值。
2. 仓库地址优先从 GitHub 的 **Code** 按钮复制。
3. 一次只执行一条命令，等待终端重新出现 `%`。
4. 不确定当前在哪里时，运行 `pwd` 和 `ls`。
5. 不确定 Git 当前状态时，运行 `git status`。
6. 只有在 Git 自动询问时才输入 Username 或 PAT。
7. 看到错误后先读最后两三行，不要立刻连续重试。
8. `Repository not found` 优先检查仓库所有者、仓库名和访问权限。
9. `Invalid username or token` 优先检查用户名、PAT、有效期和权限。
10. 永远不要把 PAT 提交到 GitHub。



## 十、下一次建议练习

在 `learning` 仓库里完成一次最小修改闭环：

1. 进入仓库并确认位置：
  ```bash
   cd learning
   pwd
   git status
  ```
2. 修改 `README.md`，增加一句学习记录。
3. 查看并暂存修改：
  ```bash
   git status
   git add README.md
   git status
  ```
4. 保存本地版本：
  ```bash
   git commit -m "记录 GitHub 学习进度"
  ```
5. 上传并在网页确认：
  ```bash
   git push
  ```

熟练之后，再练习“创建分支 → 修改 → push → 创建 PR → merge”，并用一个 Issue 记录任务。

## 十一、命令速查表

```bash
# 查看当前位置
pwd

# 查看目录文件
ls

# 进入仓库
cd learning

# 在 Finder 中打开当前目录
open .

# 查看 Git 状态
git status

# 同步远程更新
git pull

# 暂存一个文件
git add README.md

# 暂存全部修改
git add .

# 创建本地版本
git commit -m "清楚说明本次修改"

# 上传提交
git push

# 创建并切换到新分支
git switch -c 分支名

# 切换回主分支
git switch main
```



## 十二、一句话总结

今天已经完成了从“在 GitHub 创建仓库”到“把真实仓库成功克隆到本地”的完整入门，并理解了后续协作链路：

```text
Issue 提出任务
→ Branch 隔离修改
→ add 选择修改
→ commit 保存本地版本
→ push 上传分支
→ PR 请求审查与合并
→ merge 纳入 main
```

