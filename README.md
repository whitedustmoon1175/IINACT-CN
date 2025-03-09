![icon](https://github.com/marzent/IINACT/blob/main/images/icon.ico?raw=true)

[English](https://github.com/whitedustmoon1175/IINACT-CN/main/README-EN.md)

# IINACT

一个用于在类[ACT](https://advancedcombattracker.com/)环境下运行 [FFXIV_ACT_Plugin](https://github.com/ravahn/FFXIV_ACT_Plugin)的[Dalamud](https://github.com/goatcorp/Dalamud) 插件，并使用针对现代 .NET 的[Overlay Plugin](https://github.com/OverlayPlugin/OverlayPlugin) 端口进行大量修改。

此处的数据源仅基于 `Dalamud.Game.Network` 不需要任何使用 [Deucalion](https://github.com/ff14wed/deucalion) 的额外注入或使用提升权限的网络捕获。

本插件 **不会** 自己渲染覆盖层，请使用[Browsingway](https://github.com/Styr1x/Browsingway), [Next UI](https://github.com/kaminaris/Next-UI), [hudkit](https://github.com/valarnin/hudkit) (仅限Linux) 或者 [Bunny HUD](https://github.com/marzent/Bunny-HUD) (仅限macOS) 等插件来显示覆盖层。


## 原因

- 在原作者看来，对于仅想通过 WebSocket 服务器解析和提供游戏数据的需求来说，ACT 太不方便了
- 比 ACT 效率高得多，部分原因是 .NET 7.0，部分是更合理的日志行处理（磁盘 I/O 不会阻止 LogLineEvents，而是发生在单独的较低优先级线程上）
- 由于上述原因，并且完全在游戏进程内运行，与基于网络的捕获相比，在 Wine 下运行时，CPU 使用率将降低几个数量级（这里没有夸大）
- 使用基于 [NetCoreServer](https://github.com/chronoxor/NetCoreServer)的超快速低延迟 WebSocket 服务器
- 不使用会伤害 Linux 和 macOS 用户的旧式技术
- 遵循 Unix 的理念，只做一件事并把它做好  

## 安装

> **警告**  
> 任何 Dalamud 官方支持渠道都不会为此插件提供支持。任何支持请求请使用 [Issues](https://github.com/marzent/IINACT/issues) 页或[Discord](https://discord.gg/pcexJC8YPG) 提出。不要去 [XIVLauncher & Dalamud Discord](https://discord.gg/holdshift)寻求支持, 那里只是插件平台，不提供对第三方插件的支持。（当然如果是中文版iinact独有的问题请在 [Issues](https://github.com/whitedustmoon1175/IINACT-CN/issues) 提出，如果我知道如何解决会尽量提供支持）

安装说明可以[这里](https://www.iinact.com/installation/)找到，但与任何其他第三方插件存储库无关。

## 如何搭建

只需在装有[.NET 8 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
的Linux, macOS 或 Windows 计算机上运行。
```
git clone --recurse-submodules https://github.com/whitedustmoon1175/IINACT-CN.git
cd IINACT-CN
dotnet build
``` 

您还需要能够引用 Dalamud，这意味着需要分别在 Windows 和 macOS 上安装 [XL](https://github.com/goatcorp/FFXIVQuickLauncher) 或者 [XOM](https://github.com/marzent/XIV-on-Mac) 。 在 Linux 上`DALAMUD_HOME` 需要被正确设置(例如`$HOME/.xlcore/dalamud/Hooks/dev`)。

## FAQ

**我的logs文件在哪里？**

- 在您的 Documents 文件夹中。对于 Windows 用户，在 `C:\Users\[user]\Documents\IINACT`. 对于 Mac/Linux 用户，情况相同，但与 wine 前缀相关。

**这些logs文件与 FFLog 兼容吗？我可以使用 FFLogs Uploader 吗？**

- 当然！100% 兼容。
