# Ioskeley Mono Scoop bucket

通过 [Scoop](https://scoop.sh/) 安装 [Ioskeley Mono](https://github.com/ahatem/IoskeleyMono)。

## 安装

```powershell
scoop bucket add ioskeley https://github.com/DudeRenderer/scoop-ioskeley.git
scoop install ioskeley/ioskeley-mono
```

重启编辑器，在字体选择框中使用 `Ioskeley Mono`。
如果应用仍未显示该字体，可注销 Windows 后重新登录。

## 安装内容

- 从上游固定版本的 `IoskeleyMono.zip` 下载，并校验 SHA256；本仓库不托管字体文件。
- 仅安装 `Normal/Hinted` 下的 20 个 TTF（10 种字重，正体及斜体），包含编程连字。
- 不包含 Nerd Font 图标。Hinted/Unhinted 中有同名字体，因此只安装 Hinted。
- 默认安装到当前用户的 Windows 字体目录，无需管理员权限（Windows 10 1809 及以上）。
- 支持在管理员 PowerShell 中使用 `scoop install -g ioskeley/ioskeley-mono` 安装到所有用户字体目录。

## 更新与卸载

先关闭使用该字体的应用。

```powershell
scoop update
scoop update ioskeley-mono
```

卸载字体及对应的注册表条目：

```powershell
scoop uninstall ioskeley-mono
```

取消 bucket：

```powershell
scoop bucket rm ioskeley
```

移除 bucket 本身不会卸载已安装的字体。

## 维护清单

克隆此仓库，并在源码目录中运行：

```powershell
$scoopPath = scoop prefix scoop
& "$scoopPath\bin\checkver.ps1" -App ioskeley-mono -Dir .\bucket -Update
git diff -- bucket/ioskeley-mono.json
```

该命令检测最新正式 GitHub Release，并更新版本、下载 URL 和 SHA256。
发布前确认新 ZIP 的 `Normal/Hinted` 目录仍存在，并验证安装/卸载。

```powershell
git add bucket/ioskeley-mono.json
git commit -m "Update Ioskeley Mono"
git push
```

`checkver` 和 `autoupdate` 是供维护者更新清单的规则，不会自行定时执行。
本仓库没有配置定时任务。用户执行 `scoop update` 时获取的是此仓库已经提交的清单。

## 其他字体变体

上游还有 Term、NL 和各自的 Nerd Font 发布包。建议为不同字体家族创建独立 JSON。
需要同时更改包名、描述、下载 URL、SHA256、解压目录与 autoupdate URL，
并检查目标 ZIP 的实际结构；不要只改下载链接或递归安装整个标准 ZIP。

## 参考

- [Scoop Buckets](https://github.com/ScoopInstaller/Scoop/wiki/Buckets)
- [Scoop App Manifests](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests)
- [Scoop App Manifest Autoupdate](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifest-Autoupdate)
- [Ioskeley Mono Releases](https://github.com/ahatem/IoskeleyMono/releases)
