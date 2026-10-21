# Ioskeley Mono Scoop bucket

通过 [Scoop](https://scoop.sh/) 安装 [Ioskeley Mono](https://github.com/ahatem/IoskeleyMono) 的 Standard、Term、NL 和 Nerd Font 字体。

## 安装

```powershell
scoop bucket add ioskeley https://github.com/DudeRenderer/scoop-ioskeley.git
scoop install ioskeley/ioskeley-mono
```

按需选择以下安装包。所有包均使用 Normal 宽度；普通字体使用 Hinted。
SemiCondensed 和普通字体的 Unhinted 版本不在这些包的安装范围内。

| Scoop 包名 | 字体选择框中的名称 | TTF 数量 |
| --- | --- | ---: |
| `ioskeley-mono` | `Ioskeley Mono` | 20 |
| `ioskeley-mono-term` | `Ioskeley Mono Term` | 20 |
| `ioskeley-mono-nl` | `Ioskeley Mono NL` | 20 |
| `ioskeley-mono-nerd-font` | `IoskeleyMono Nerd Font`、`IoskeleyMono Nerd Font Mono` | 40 |
| `ioskeley-mono-term-nerd-font` | `IoskeleyMonoTerm Nerd Font`、`IoskeleyMonoTerm Nerd Font Mono` | 40 |
| `ioskeley-mono-nl-nerd-font` | `IoskeleyMonoNL Nerd Font`、`IoskeleyMonoNL Nerd Font Mono` | 40 |

- Standard：通用编辑器字体，含编程连字。
- Term：调整箭头和框线，适合终端，含编程连字。
- NL：不包含编程连字。
- Nerd Font（NF）：包含图标，部分图标可超过单字符宽度。
- Nerd Font Mono（NFM）：图标保持单字符宽度。每个 Nerd Font 包同时安装 NF 与 NFM。
- 每个字体家族包含 10 种字重及各自的正体、斜体。六个包共提供九个家族、180 个 TTF。
- Nerd Font 的真实 family 名称中 `IoskeleyMono`、`IoskeleyMonoTerm` 和 `IoskeleyMonoNL` 不含内部空格。

例如安装终端 Nerd Font：

```powershell
scoop install ioskeley/ioskeley-mono-term-nerd-font
```

一次安装全部六个包：

```powershell
$packages = @(
    'ioskeley/ioskeley-mono'
    'ioskeley/ioskeley-mono-term'
    'ioskeley/ioskeley-mono-nl'
    'ioskeley/ioskeley-mono-nerd-font'
    'ioskeley/ioskeley-mono-term-nerd-font'
    'ioskeley/ioskeley-mono-nl-nerd-font'
)
scoop install @packages
```

安装脚本会自动复制、注册并加载 TTF，再通知 Windows 刷新字体列表；不需要逐个双击 TTF 安装。
已经打开的应用可能缓存字体列表，请完全退出后重新打开，再选择表中的字体名称。

## 安装行为

从上游固定版本的 Releases 下载，并校验 SHA256；本仓库不托管字体文件。
默认安装到当前用户的 Windows 字体目录，无需管理员权限（Windows 10 1809 及以上）。
在管理员 PowerShell 中加入 `-g` 参数可安装到所有用户字体目录。
各包拥有不同的字体文件名，可以同时安装、分别卸载。
卸载及更新前会释放当前 Windows 会话中加载的字体资源；若其他应用仍占用字体，请关闭相关应用后重试。

## 更新与卸载

先关闭使用相关字体的应用。下列示例以终端 Nerd Font 为例：

```powershell
scoop update
scoop update ioskeley-mono-term-nerd-font
scoop uninstall ioskeley-mono-term-nerd-font
```

卸载会删除对应的字体文件及注册表条目。取消 bucket：

```powershell
scoop bucket rm ioskeley
```

移除 bucket 本身不会卸载已安装的字体。

## 维护清单

克隆此仓库，并在源码目录中运行：

```powershell
$scoopPath = scoop prefix scoop
& "$scoopPath\bin\checkver.ps1" -App '*' -Dir .\bucket -Update
git diff -- bucket
```

该命令检测最新正式 GitHub Release，并更新版本、下载 URL 和 SHA256。
发布前应确认普通 ZIP 的 `Normal/Hinted` 和 Nerd Font ZIP 的 `Normal` 目录结构未变，
并验证安装/卸载。

```powershell
git add bucket
git commit -m "Update Ioskeley Mono fonts"
git push
```

`checkver` 和 `autoupdate` 是供维护者更新清单的规则，不会自行定时执行。
本仓库没有配置定时任务。用户执行 `scoop update` 时获取的是此仓库已经提交的清单。

## 参考

- [Scoop Buckets](https://github.com/ScoopInstaller/Scoop/wiki/Buckets)
- [Scoop App Manifests](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests)
- [Scoop App Manifest Autoupdate](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifest-Autoupdate)
- [Ioskeley Mono Releases](https://github.com/ahatem/IoskeleyMono/releases)
