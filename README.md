# dq

大强博客的终端搜索器。运行 `dq` 后，可以搜索博客文章、用上下键或鼠标选择，并在浏览器打开文章。

## 使用

```powershell
dq
```

支持：

- 搜索文章标题、摘要和正文；空格分隔多个关键词。
- ↑↓ 移动选择，右侧查看文章预览。
- Enter 打开当前文章；鼠标单击选择，双击打开。
- Esc 或 Ctrl+C 退出。

也可以在进入界面时直接带关键词：

```powershell
dq OpenCLI
```

## 本地缓存与更新

第一次运行会从博客公开的 `https://blog.dqtx.cc/rss.xml` 获取文章索引，并保存到本机缓存：

```text
Windows: %LOCALAPPDATA%\dq\index.json
macOS/Linux: ~/.cache/dq/index.json
```

缓存有效期为 6 小时。在有效期内再次运行 `dq`，直接读取本地缓存，不重复请求博客。缓存过期后，下一次运行会自动获取最新索引；如果网络暂时不可用，会继续使用已有缓存。

需要立即获取最新文章时：

```powershell
dq --refresh
```

因此，博客发布新文章后，粉丝不需要重新安装工具。最多等待缓存有效期，或主动运行一次 `dq --refresh` 即可看到新文章。

## 本机开发

```powershell
npm link
dq
```

## 从 GitHub 使用

当前 npm 包还没有发布。粉丝可以先从 GitHub 下载项目：

```powershell
git clone https://github.com/dqtx760/dq-cli.git
cd dq-cli
npm link
dq
```

以后如果发布到 npm，安装方式会简化为：

```powershell
npm install --global dqtx-cli
dq
```

## OpenCLI 插件

`opencli-plugin` 目录保留了给 Agent 和脚本使用的只读 OpenCLI 插件：

```powershell
opencli plugin install "file://$((Resolve-Path .\opencli-plugin).Path)"
opencli dqtx search OpenCLI
opencli dqtx article opencli
```

裸命令是 `dq`；OpenCLI 插件命名空间仍是 `dqtx`，两者用途不同。

## 发布状态

项目已公开发布到 GitHub：

https://github.com/dqtx760/dq-cli
