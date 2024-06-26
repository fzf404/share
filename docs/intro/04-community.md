> Gitee / GitHub / Git

## Git 托管站

> 每一类群体都有自己的社区，程序员当然也不例外。
>
> CSDN 是写博客的地方，下面的这些网址就是分享代码的地方。
>
> [GitHub](https://github.com/)
>
> [GitHub 镜像站](https://hub.fastgit.org/)
>
> [Gitee](https://gitee.com/)

- 开源社区：人们将自己的源代码传到社区中，供所有人观看。
- 开源协议：允许使用的范围。

### 开源项目

- [VSCode](https://github.com/microsoft/vscode)
- [jQuery](https://github.com/jquery/jquery)
- [提问的艺术](https://github.com/tvvocold/How-To-Ask-Questions-The-Smart-Way)

### 功能

- `Star`：关注该项目
- `Issues`：向维护者反馈问题的地方
- `Pull request`：向维护者提交代码的地方
- `Releases`：发行版，比较成熟的代码/编译成功的软件

## 一个极为简单的项目流程

1. 访问 [Gitee](https://gitee.com/) 官网
2. 点击右上角 ➕ 号 -> 新建代码仓库
3. 填写仓库信息
4. 新建 `README.md` (约定俗成，每个仓库最好都写一个说明文档)
5. 进入 `WebIDE` 编辑文件
6. 发现问题为他提 `Issue`
7. 可以帮助解决则提交 `Pull Request`

### 参与

1. 提交 Issue：
   - 使用项目时遇到了问题
   - 或有一些好建议
2. Fork 项目，提交 PR：
   - 发现代码有 BUG，帮忙修改
   - 优化代码执行速度

!!! note Note

    大家回去不用做，只是让大家了解一下开源项目的流程

## Git 使用

> 上面的两个平台都是使用 Git 进行代码管理的
>
> 那 Git 究竟是个什么东西

### 安装&使用

> 从今天开始，咱们的所有代码都需要同步到 Gitee

1. 下载 [Git](https://git-scm.com/download/win)
2. 克隆开源项目

```bash
# 查看 git 版本
git --version

# 从 Gitee 上 Clone 下来一个 2048 游戏吧
git clone https://gitee.com/yeahmao/games_2048.git

# 在 VSCode 中运行
```

3. 新建 Gitee 仓库：`general-code`
4. 将自己之前的代码上传至 Gitee 吧

```bash
# 设置用户名及邮箱
git config --global user.name "xxx"
git config --global user.email "xxx@xx.xx"

# 初始化Git仓库
git init        # 多了一个 .git 文件夹
touch README.md        # 新建文件
git add README.md        # 添加到暂存区
git commit -m "first commit"    # 添加到归档区
# 添加远程地址 地址名为origin
git remote add origin https://gitee.com/xxx/general-code.git
# 将 master 分支归档区内容推送到 origin 服务器
git push -u origin master
```

### 命令

```bash
git status        # 当前提交状态
git add .         # 添加到暂存区
git status
git commit -m "我的第一次提交"   # 添加到归档区
git status
git push             # 推送到远程仓库
git push -f origin   # 强制推送
git pull             # 拉取远程更新的代码
```

### 使用 VSCode 上传代码

> 右侧 Git 源代码管理

### Git 的优势

> 我只是想传个代码，为什么这么复杂？
>
> 开发需要版本控制系统

1. 代码版本管理
   - [教案地址](https://github.com/fzf404/share/)
2. 多分支开发
   - [VSCode](https://github.com/microsoft/VSCode)
3. 遇到问题方便回滚

## 课后

### 作业

1. 将目前自己写过的所有代码进行整理，推送到 Gitee 仓库里

### 推荐阅读

[从零开始学习 GitHub](https://zhuanlan.zhihu.com/p/21269318)

[Git 入门指南](https://zhuanlan.zhihu.com/p/21193604)
