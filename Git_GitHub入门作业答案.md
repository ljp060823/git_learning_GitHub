# Git & GitHub 入门作业 - 答案

**学生：** ljp060823 (刘建平)  
**GitHub：** https://github.com/ljp060823  
**仓库链接：** https://github.com/ljp060823/git_learning_GitHub https://github.com/ljp060823?tab=repositories


**（1）Git 是什么？**  
Git 是一个版本管理工具，安装在自己电脑上。它能记录你每次修改了什么文件、改了什么内容，让你可以随时回退到任何一个历史版本，就像游戏的存档系统一样。

**（2）GitHub 是什么？**  
GitHub 是一个云端网站，专门用来存放 Git 仓库的。你可以把自己的代码备份到 GitHub 上的代码仓库，也可以和别人一起协作开发项目。

**（3）Git 和 GitHub 的关系是什么？**  
Git 是本地工具，GitHub 是云端平台。Git 负责在你电脑上管理版本，GitHub 负责在云端备份和共享。用 `git push` 把本地的提交推到 GitHub，用 `git pull` 把 GitHub 上的更新拉到本地，git是工具，github是放代码的仓库。

**4）你的本地电脑在这里面扮演什么角色？**  
本地电脑是实际写代码和开发的地方，用 Git 管理版本，然后推送到 GitHub 远程仓库做备份和协作。


### Q2：克隆完成后回答

**命令：**
```bash
gh repo clone ljp060823/git_learning_GitHub
```

**（1）克隆完成后，你的电脑上多了哪些东西？**  
克隆完成后，电脑上多了一个 `git_learning_GitHub` 文件夹，里面包含了仓库的所有文件（两个 PDF 文件），以及一个隐藏的 `.git` 文件夹。

**（2）这个项目目录里面的 .git 文件夹是做什么用的？**  
`.git` 文件夹是 Git 的核心，它存储了这个项目所有的版本历史记录，包括：每一次提交（commit）的记录  所有分支的信息 暂存区的状态 远程仓库的地址
没有这个文件夹，Git 就无法追踪这个项目的版本变化。

---

### Q3：新建 helo.txt 并提交

**操作：**
```bash
echo "Hello, this is my first git commit!" > helo.txt
git add .
git commit -m "Add helo.txt"
```

**（1）git add 做了什么？**  
`git add` 把修改的文件从 工作区 放到 暂存区 。暂存区就像一个待提交的清单，告诉 Git 这些修改我准备好了，下次提交时把它们带上。

**（2）git commit 做了什么？**  
`git commit` 把暂存区的所有内容打包成一个"提交记录"，保存到本地版本库。每个 commit 都有一个唯一的 ID 和提交信息），方便以后查看和回退。

**（3）为什么不能只 commit 而不 add？**  
因为 Git 需要你先明确"选择"哪些修改要提交。`add` 就是这个选择的过程。如果不 add，Git 不知道你要提交哪些改动。这样设计的好处是：你可以只提交部分修改，而不是把所有改动一次性提交。

---
### Q4：推送到 GitHub

**命令：**
```bash
git push origin main
```

**（1）推送之前和推送之后，GitHub 上有什么变化？**  
- 推送之前：GitHub 上没有 `hello.txt` 文件
- 推送之后：GitHub 上出现了 `hello.txt` 文件，以及对应的提交记录

**（2）你是怎么确认新的提交（commit）已经出现在 GitHub 上的？**  
在 GitHub 仓库页面上：看到新文件 `hello.txt` 出现在文件列表中 点击文件能看到内容 提交记录数量增加了 点击 commits 可以看到新的提交记录

---


### Q5：创建 feature/add-json 分支

**命令：**
```bash
git checkout -b feature/add-json
echo '{"name": "git learning", "author": "ljp060823"}' > sample.json
git add .
git commit -m "Add sample.json"
git push -u origin feature/add-json
```

**（1）为什么我们要用分支（branch），而不是直接在 main 上改？**  
因为 main 分支通常是稳定的、可运行的版本。如果直接在 main 上改，改错了就会影响整个项目。用分支可以在不影响主分支的情况下开发新功能，等开发完成、测试没问题后再合并到 main。

**（2）分支能帮我们解决什么样的实际问题？**  
比如我在做一个网站，main 分支是正在运行的线上版本。现在我要加一个新功能。如果直接在 main 上改，改到一半网站就挂了。所以我创建一个 `feature/login` 分支，在这个分支上慢慢开发，开发完了测试通过再合并到 main。这样线上网站一直正常运行，新功能也能安全开发。

---


### Q6：创建 PR 并合并


**（1）"合并（merge）"这一步实际上做了什么？**  
合并就是把 feature/add-json 分支上的所有改动（新增的 sample.json 文件）整合到 main 分支中。合并后，main 分支就有了 sample.json 文件，两个分支的代码保持一致。

**（2）合并之后，main 分支的代码和历史发生了什么变化？**  
- main 分支多了一个 sample.json 文件
- 提交历史中多了一条合并记录
- feature/add-json 分支的提交记录也出现在 main 的历史中

---


### Q7：制造冲突并解决

**操作步骤：**
1. 在 main 分支修改 helo.txt 为 "Helo from main - 修改版本"
2. 创建 feature/conflict-demo 分支，修改 helo.txt 为 "Helo from feature - 修改版本"
3. 尝试合并时出现冲突

**冲突内容：**
```
<<<<<<< HEAD
Helo from main - 修改版本
=======
Helo from feature - 修改版本
>>>>>>> feature/conflict-demo
```

**解决方式：** 保留双方内容
```
Helo from main - 修改版本
Helo from feature - 修改版本
(已解决冲突，保留双方内容)
```

**（1）为什么会产生冲突？用自己的话解释。**  
因为两个分支都修改了同一个文件（helo.txt）的同一个位置，而且修改的内容不一样。Git 无法自动判断应该保留哪个版本，所以就报冲突让你手动选择。

**（2）什么情况下，即使很多人同时改代码，也不会产生冲突？**  
当不同的人修改的是不同的文件，或者修改同一个文件的不同位置时，Git 可以自动合并，不会产生冲突。比如：A 改了 index.html，B 改了 style.css，就不会冲突；或者 A 改了 helo.txt 的第一行，B 改了 helo.txt 的第三行，也不会冲突。

---

### Q8：pull 和 fetch 的区别

**（1）git fetch 做了什么？**  
`git fetch` 只是从远程仓库下载最新的提交记录和文件到本地，但是**不会自动合并**到你当前的工作分支。它只是更新了本地的"远程追踪分支"（比如 origin/main），让你可以看到远程有什么新内容。

**（2）git pull 做了什么？**  
`git pull` = `git fetch` + `git merge`。它先下载远程的最新内容，然后**自动合并**到你当前的工作分支。

**（3）为什么通常认为 pull 比 fetch "更危险"一点？请结合"自动合并"来解释。**  
因为 `git pull` 会自动合并，如果你本地有未提交的修改，或者远程的修改和你的本地修改有冲突，自动合并可能会导致问题：
- 自动合并成功但代码可能不是你想要的
- 自动合并失败产生冲突，需要手动解决
- 可能覆盖你本地未提交的修改

而 `git fetch` 只是下载不合并，你可以先查看远程有什么变化，确认没问题后再手动 merge，更安全。

---
