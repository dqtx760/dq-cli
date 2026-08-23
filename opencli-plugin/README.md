# 大强博客 OpenCLI 插件

这是一个给 [OpenCLI](https://github.com/jackwener/opencli) 使用的博客搜索插件。

安装以后，你可以让 OpenCLI 在命令行中读取大强博客的公开文章：查看最新文章、按关键词搜索、读取单篇文章正文。

## 先分清两个命令

这个项目里有两个入口，用途不同：

| 命令 | 用途 | 适合谁 |
| --- | --- | --- |
| `dq` | 带上下键、鼠标和预览的可视化搜索界面 | 普通用户、粉丝 |
| `opencli dqtx ...` | 返回结构化结果，方便 Agent 和脚本调用 | AI Agent、开发者 |

如果你只是想搜索博客并打开文章，优先使用 `dq`。本 README 主要介绍 `opencli dqtx ...` 这一组命令。

## 使用前必须知道

`dq` 和 OpenCLI 插件是两个独立入口：

- 只使用 `dq`：不依赖 OpenCLI，只需要 Node.js 20 或更高版本，以及可以访问互联网。
- 使用 `opencli dqtx ...`：必须先安装 OpenCLI 1.8.6 或更高版本，再安装本插件。

如果你是普通用户，只想搜索文章并在浏览器中打开，安装并运行 `dq` 即可，不需要安装 OpenCLI。

## 界面示例

下面是 `dq` 的终端搜索界面：

![dq 终端搜索界面](https://gitee.com/da-qiang-classmate/typora/raw/master/image/9a06d1620f57afe98c08e7fa880336b4.webp)

## 这个插件能做什么？

- 查看博客最新文章；
- 按标题、分类或文章 URL 后缀搜索；
- 读取公开文章的正文；
- 返回文章标题、日期、分类和网页地址。

这是一个公开只读插件：

- 不需要登录博客；
- 不需要 Chrome 浏览器扩展；
- 不读取你的本地草稿；
- 不会发布、修改或删除博客文章。

## 安装前需要什么？

根据你使用的入口，前置条件不同：

- 使用 `dq`：Node.js 20 或更高版本，以及可以访问互联网；
- 使用 `opencli dqtx ...`：Node.js 20 或更高版本、OpenCLI 1.8.6 或更高版本，以及可以访问互联网。

下面的“安装插件”步骤只针对 `opencli dqtx ...`，不适用于单独使用的 `dq`。

在终端检查 OpenCLI：

```powershell
opencli --version
```

如果提示找不到 `opencli`，先安装：

```powershell
npm install --global @jackwener/opencli
```

## 安装插件

项目已经公开发布到 GitHub：

https://github.com/dqtx760/dq-cli

这个仓库同时包含 `dq` 搜索器和 OpenCLI 插件。由于插件位于仓库的 `opencli-plugin` 子目录，当前请先下载项目，再从本地目录安装插件。

在 PowerShell 中运行：

```powershell
git clone https://github.com/dqtx760/dq-cli.git
cd dq-cli
opencli plugin install "file://$((Resolve-Path .\opencli-plugin).Path)"
```

安装成功后，检查插件是否存在：

```powershell
opencli plugin list
```

列表中应该能看到：

```text
dqtx-blog
```

再运行验证：

```powershell
opencli validate dqtx
```

看到 `PASS` 就说明安装成功。

## 基本使用

### 查看最新文章

```powershell
opencli dqtx latest --limit 5
```

这里的 `5` 表示显示 5 篇文章，可以改成其他数量。

### 搜索文章

```powershell
opencli dqtx search OpenCLI
```

也可以搜索中文关键词：

```powershell
opencli dqtx search 余额 --limit 10
```

当前这个 OpenCLI 搜索命令主要匹配文章标题、分类和 URL 后缀。如果你想搜索正文内容，使用可视化命令 `dq` 更合适。

### 读取单篇文章

```powershell
opencli dqtx article opencli
```

也可以使用文章标题、文章路径或完整 URL：

```powershell
opencli dqtx article "/posts/aihacks/open-cli/"
opencli dqtx article "https://blog.dqtx.cc/posts/aihacks/open-cli/"
```

这个命令会返回文章正文和文章地址，但不会自动打开浏览器。需要打开网页时，可以复制返回的 URL；或者直接使用：

```powershell
dq
```

## 常用维护命令

查看已安装插件：

```powershell
opencli plugin list
```

更新插件：

```powershell
opencli plugin update dqtx-blog
```

卸载插件：

```powershell
opencli plugin uninstall dqtx-blog
```

## 常见问题

### 1. 提示找不到 `dqtx`

先检查插件是否安装：

```powershell
opencli plugin list
```

如果列表里没有 `dqtx-blog`，重新执行安装命令。

### 2. 提示博客请求失败

这个插件读取的是[大强博客](https://blog.dqtx.cc/)的公开页面。请先确认浏览器可以打开博客，再重新运行命令。

### 3. `opencli doctor` 提示浏览器扩展未连接

这个插件是公开网页读取，不依赖浏览器扩展。只要 `opencli validate dqtx` 通过，就可以正常使用。

## 给项目维护者

插件源代码在当前目录的 `dqtx.js` 中，插件名称是 `dqtx-blog`，OpenCLI 命令命名空间是 `dqtx`。

项目已公开发布到 GitHub；如果只是想使用可视化搜索器，可以在项目根目录执行 `npm link`，然后运行 `dq`。

## 关于作者


**大强同学** — 科技博主，也是一名github开源作者，非科班出身，以实践驱动开发，践行Build in Public成长理念，深耕 Windows效率生态，擅长将AI Agent从构想转化为可落地的实用方案，我坚信AI与智能体将重塑个人做事方式，愿以自身技术积累，助力个体把握智能时代机遇，高效提升自身创作、办公与成长效率。

| 平台         | 链接                                                                                                                                             |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| 🌐 官网      | [dqtx.cc](https://www.dqtx.cc/)   [os.dqtx.cc](https://os.dqtx.cc/)                                                                         |
| 𝕏 Twitter | [@Derek Zhao](https://x.com/dqtx760)                                                                                                           |
| 📺 B站      | [大强同学_](https://space.bilibili.com/491358682/upload/video)                                                                                     |
| ▶️ YouTube | [@Derek Zhao](https://www.youtube.com/@dqtx760/videos)                                                                                         |
| 💬 公众号     | 微信搜「大强同学」或扫码关注 ↓                                                                                                                               |
|            |                                                                     |
