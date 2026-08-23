# dq：大强博客终端搜索器

`dq` 是一个在命令行里搜索大强博客文章的小工具。

安装以后，粉丝可以输入 `dq`，搜索文章的标题、摘要和正文，再用上下键或鼠标选择文章，并在浏览器中打开。

## 先说结论

- 普通用户只需要安装 Node.js 和本项目，不需要安装 OpenCLI。
- `dq` 读取博客公开的文章索引，不需要登录，也不会读取或修改用户的本地文件。
- 如果你是 Agent 或开发者，想通过 OpenCLI 获取结构化结果，请查看 [OpenCLI 插件说明](./opencli-plugin/README.md)。

## 界面示例

下面是 `dq` 的终端搜索界面：

![dq 终端搜索界面](https://gitee.com/da-qiang-classmate/typora/raw/master/image/9a06d1620f57afe98c08e7fa880336b4.webp)

## 安装前需要什么？

下面以 Windows PowerShell 为例。使用 macOS 或 Linux 时，可以在终端执行相同的命令。

1. 安装 Node.js 20 或更高版本。
2. 确保电脑可以访问互联网，因为首次运行需要从博客获取文章索引。
3. 如果使用下面的 GitHub 备用安装方式，再安装 Git；没有 Git 时，也可以在 GitHub 页面点击 **Code → Download ZIP** 下载项目并解压。

注意：普通用户不需要安装 OpenCLI，也不需要安装浏览器扩展。

## 推荐安装方式：从 npm 安装

项目发布到 npm 后，普通用户不需要下载源码，直接运行：

```powershell
npm install --global @daqiang520/dqtx-cli
dq
```

虽然 npm 包名是 `@daqiang520/dqtx-cli`，但安装后的命令仍然是 `dq`。

检查安装是否成功：

```powershell
dq --version
```

## 备用安装方式：从 GitHub 安装

打开 PowerShell，依次运行：

```powershell
git clone https://github.com/dqtx760/dq-cli.git
cd dq-cli
npm link
```

`npm link` 会把项目里的 `dq` 命令注册到本机，之后可以在任意目录运行它。

安装完成后，检查命令是否可用：

```powershell
dq --version
```

如果能看到版本号，就可以运行：

```powershell
dq
```

如果系统提示找不到 `dq`，请关闭当前终端窗口，重新打开 PowerShell 后再试一次；仍然不行时，在项目目录重新运行 `npm link`。

## 怎么使用？

进入 `dq` 后，直接输入关键词即可搜索：

```powershell
dq
```

也可以启动时直接带关键词：

```powershell
dq OpenCLI
```

搜索支持标题、摘要和正文；多个关键词之间用空格分隔。

- `↑` `↓`：移动选择；
- 鼠标单击：选择文章；
- `Enter` 或鼠标双击：在默认浏览器打开文章；
- `Esc` 或 `Ctrl+C`：退出。

## 本地缓存和文章更新

第一次运行时，`dq` 会从博客公开的 RSS 地址获取文章索引，并保存到本机缓存：

```text
Windows：%LOCALAPPDATA%\dq\index.json
macOS/Linux：~/.cache/dq/index.json
```

缓存有效期为 6 小时。在有效期内再次运行 `dq`，会直接使用本地缓存，不重复下载索引。

博客发布新文章后，粉丝不需要重新安装工具。缓存过期后，下一次运行会自动获取最新文章；也可以立即执行：

```powershell
dq --refresh
```

如果网络暂时不可用，工具会优先使用已有缓存。之后网络恢复时，再运行 `dq --refresh` 即可更新。

## 更新工具本身

如果项目后续发布了新版本，在项目目录执行：

```powershell
git pull
npm link
```

博客文章更新不需要执行这一步；只有工具代码发生变化时才需要更新项目本身。

## OpenCLI 插件（高级用法）

`opencli-plugin` 目录是给 OpenCLI、AI Agent 和脚本使用的只读插件。

使用这部分功能需要先安装 OpenCLI 1.8.6 或更高版本，然后在项目目录执行：

```powershell
opencli plugin install "file://$((Resolve-Path .\opencli-plugin).Path)"
opencli validate dqtx
```

验证通过后，可以使用：

```powershell
opencli dqtx latest --limit 5
opencli dqtx search OpenCLI
opencli dqtx article opencli
```

普通用户只使用 `dq` 时，不需要安装 OpenCLI。更多插件命令请看 [OpenCLI 插件说明](./opencli-plugin/README.md)。

## 项目地址

[https://github.com/dqtx760/dq-cli](https://github.com/dqtx760/dq-cli)

## 关于作者

**大强同学** — 科技博主，也是一名github开源作者，非科班出身，以实践驱动开发，践行Build in Public成长理念，深耕 Windows效率生态，擅长将AI Agent从构想转化为可落地的实用方案，我坚信AI与智能体将重塑个人做事方式，愿以自身技术积累，助力个体把握智能时代机遇，高效提升自身创作、办公与成长效率。

| 平台 | 链接 |
| --- | --- |
| 🌐 官网 | [dqtx.cc](https://www.dqtx.cc/)　[os.dqtx.cc](https://os.dqtx.cc/) |
| 𝕏 Twitter | [@Derek Zhao](https://x.com/dqtx760) |
| 📺 B站 | [大强同学_](https://space.bilibili.com/491358682/upload/video) |
| ▶️ YouTube | [@Derek Zhao](https://www.youtube.com/@dqtx760/videos) |
| 💬 公众号 | 微信搜「大强同学」或扫码关注 ↓ |
