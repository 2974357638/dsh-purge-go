# dsh-purge · DSH Go 版

在 DSH Go 的手机本机引擎中管理宿主补丁、提示词和规则，并查看状态、备份与回滚。安装后可减少连续任务中的重复确认和中断。

当前版本 **1.6.85**。本仓库基于 [dsh-purge Community 1.6.84](https://github.com/kingcharleslzy-ai/dsh-purge/releases/tag/v1.6.84)，社区版源自 [小杨 / YuJunZhiXue 的 dsh-purge](https://github.com/YuJunZhiXue/dsh-purge)。保留原作者署名和 MIT 许可证；本项目不是 DeepSeek、DSH Go 或上游作者的官方发行。[English](docs/README.en.md)

## 适用范围

本说明面向 **DSH Go 1.0.12 的手机本机引擎**，其内置 DSH 版本为 0.2.2-rc.1。使用者此前在一台 Android 设备上测试过社区版的安装和基本功能。

安装目标取决于当前主机。先在 DSH Go 切换到「本机」，确认本机引擎已启动且处于正常模式；如果当前连接电脑或服务器，在那边执行命令会安装到远程主机。手机本机引擎使用 `web` profile。[DSH Go 主机与插件文档](https://github.com/ccch1mneyyy/dsh-Go/blob/main/docs/plugins/hosts.md)

内部包名仍是 `dsh-purge-community`，命令仍是 `purge-community`，以保持社区版的安装兼容性；GitHub 仓库与界面名称显示为「DSH Go 版」。

## 第一步：在 App 终端用 Bash 安装

打开 DSH Go 自带的「终端」，在本机环境的 Bash 中运行：

```bash
dsh plugin --profile web add "https://github.com/2974357638/dsh-purge-go/releases/download/v1.6.85/dsh-purge-community-1.6.85.tgz"
```

命令成功后，打开「设置 › 插件 › 已安装」，确认 `dsh-purge-community` 已安装并启用。**这一步只安装插件包，不会自动完成宿主补丁应用和 shim 注入。** 不要把地址换成裸 npm 包名，也不要在手机外的终端执行后误以为装进了手机。

## 第二步：应用补丁、备份和 shim 注入

1. 在插件详情打开网页界面；若 App 没有显示完整面板，点「在网页版打开」。在网页版左侧栏进入「DSH Go 版 › 状态」。
2. 点击 **「应用」**。插件会先备份宿主文件，再写入适用的清洗补丁，并处理所需的 shim 注入。备份、补丁和 shim 属于这一轮操作，并非三个独立按钮。
3. 等待结果，查看补丁、备份和 shim 的逐项状态。若补丁仍「待应用」或「没对上」、备份失败，或 shim 报错，请先查看诊断；某项 shim 标为「不适用」时，无需强行要求它显示「已注入」。

插件升级或内置 DSH 更新后，也要重新点击「应用」。若页面提示无法定位宿主，先确认当前选中手机本机引擎和 `web` profile。[DSH Go 插件界面说明](https://github.com/ccch1mneyyy/dsh-Go/blob/main/docs/guide/zh/08-plugins.md)

## 第三步：重启本机引擎并核对

应用成功后，在 DSH Go 打开 **「设置 › 本机引擎 › 重启」**。重启会中断进行中的对话，请在当前任务结束后操作。仅刷新网页版或关闭页面，不会让运行中的引擎加载已写入的宿主代码。[DSH Go 本机引擎指南](https://github.com/ccch1mneyyy/dsh-Go/blob/main/docs/guide/zh/03-engine-hosts.md)

引擎重新启动后，回到「DSH Go 版 › 状态」刷新，确认补丁不再待应用，备份和 shim 状态符合本机报告。若 App 终端能找到该 profile 的命令，也可运行 `purge-community selfcheck --text` 查看逐层诊断；找不到该命令时以面板为准，不要另装同名 npm 包。

## 更新与排查

从本仓库升级时，在**同一个本机 `web` profile**重新运行上述 Bash 命令，再「应用」并重启本机引擎。已有社区版时无需先卸载。安装包及校验文件见 [v1.6.85 Release](https://github.com/2974357638/dsh-purge-go/releases/tag/v1.6.85)。

如果安装报错、状态未变或补丁没对上，保留错误信息，先核对当前主机、profile、补丁状态和本机备份。安装命令退出成功不代表补丁已经生效。问题可提交至 [Issues](https://github.com/2974357638/dsh-purge-go/issues)。

## 参考与致谢

- [社区版功能与桌面参考说明](docs/COMMUNITY-DESKTOP-REFERENCE.md)
- [原社区版仓库](https://github.com/kingcharleslzy-ai/dsh-purge)
- [版权与衍生说明](NOTICE.md) · [MIT 许可证](LICENSE)

<!-- CONTRIBUTORS:START -->
<table>
  <tr>
    <td align="center" width="120"><a href="https://github.com/YuJunZhiXue"><img src="https://avatars.githubusercontent.com/u/188421097?s=112" width="56" height="56" alt="YuJunZhiXue" /><br /><sub>YuJunZhiXue</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/kingcharleslzy-ai"><img src="https://avatars.githubusercontent.com/u/260348840?s=112" width="56" height="56" alt="kingcharleslzy-ai" /><br /><sub>kingcharleslzy-ai</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/luowang-ui"><img src="https://avatars.githubusercontent.com/u/62333101?s=112" width="56" height="56" alt="luowang-ui" /><br /><sub>luowang-ui</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/heigit"><img src="https://avatars.githubusercontent.com/u/8845668?s=112" width="56" height="56" alt="heigit" /><br /><sub>heigit</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/OGHong"><img src="https://avatars.githubusercontent.com/u/130678941?s=112" width="56" height="56" alt="OGHong" /><br /><sub>OGHong</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/Wangxiaolu0716"><img src="https://avatars.githubusercontent.com/u/110671501?s=112" width="56" height="56" alt="Wangxiaolu0716" /><br /><sub>Wangxiaolu0716</sub></a></td>
  </tr>
  <tr>
    <td align="center" width="120"><a href="https://github.com/wtfsb19"><img src="https://avatars.githubusercontent.com/u/70636030?s=112" width="56" height="56" alt="wtfsb19" /><br /><sub>wtfsb19</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/MingShi350"><img src="https://avatars.githubusercontent.com/u/47762455?s=112" width="56" height="56" alt="MingShi350" /><br /><sub>MingShi350</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/loLollipop"><img src="https://avatars.githubusercontent.com/u/168881978?s=112" width="56" height="56" alt="loLollipop" /><br /><sub>loLollipop</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/youki258"><img src="https://avatars.githubusercontent.com/u/177468176?s=112" width="56" height="56" alt="youki258" /><br /><sub>youki258</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/SimonQvQ"><img src="https://avatars.githubusercontent.com/u/154972131?s=112" width="56" height="56" alt="SimonQvQ" /><br /><sub>SimonQvQ</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/alexopenfan-xiaxin"><img src="https://avatars.githubusercontent.com/u/267281196?s=112" width="56" height="56" alt="alexopenfan-xiaxin" /><br /><sub>alexopenfan-xiaxin</sub></a></td>
  </tr>
  <tr>
    <td align="center" width="120"><a href="https://github.com/Minervaowl7"><img src="https://avatars.githubusercontent.com/u/127482476?s=112" width="56" height="56" alt="Minervaowl7" /><br /><sub>Minervaowl7</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/ShiTan-677"><img src="https://avatars.githubusercontent.com/u/91113050?s=112" width="56" height="56" alt="ShiTan-677" /><br /><sub>ShiTan-677</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/Minggle"><img src="https://avatars.githubusercontent.com/u/35053182?s=112" width="56" height="56" alt="Minggle" /><br /><sub>Minggle</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/Steooenwolf-666"><img src="https://avatars.githubusercontent.com/u/156271754?s=112" width="56" height="56" alt="Steooenwolf-666" /><br /><sub>Steooenwolf-666</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/a320583781-create"><img src="https://avatars.githubusercontent.com/u/234735967?s=112" width="56" height="56" alt="a320583781-create" /><br /><sub>a320583781-create</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/longyanbo1224-debug"><img src="https://avatars.githubusercontent.com/u/334267419?s=112" width="56" height="56" alt="longyanbo1224-debug" /><br /><sub>longyanbo1224-debug</sub></a></td>
  </tr>
  <tr>
    <td align="center" width="120"><a href="https://github.com/0xnuu"><img src="https://avatars.githubusercontent.com/u/113989865?s=112" width="56" height="56" alt="0xnuu" /><br /><sub>0xnuu</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/21hbguo"><img src="https://avatars.githubusercontent.com/u/139569698?s=112" width="56" height="56" alt="21hbguo" /><br /><sub>21hbguo</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/AkiraNyx"><img src="https://avatars.githubusercontent.com/u/176532870?s=112" width="56" height="56" alt="AkiraNyx" /><br /><sub>AkiraNyx</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/cracer4869"><img src="https://avatars.githubusercontent.com/u/46320829?s=112" width="56" height="56" alt="cracer4869" /><br /><sub>cracer4869</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/fomaper"><img src="https://avatars.githubusercontent.com/u/38674512?s=112" width="56" height="56" alt="fomaper" /><br /><sub>fomaper</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/Kilig1058674225"><img src="https://avatars.githubusercontent.com/u/68159061?s=112" width="56" height="56" alt="Kilig1058674225" /><br /><sub>Kilig1058674225</sub></a></td>
  </tr>
  <tr>
    <td align="center" width="120"><a href="https://github.com/Legeo969"><img src="https://avatars.githubusercontent.com/u/79903511?s=112" width="56" height="56" alt="Legeo969" /><br /><sub>Legeo969</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/LinyiAIGC"><img src="https://avatars.githubusercontent.com/u/68159061?s=112" width="56" height="56" alt="LinyiAIGC" /><br /><sub>LinyiAIGC</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/lyufeng000"><img src="https://avatars.githubusercontent.com/u/168790556?s=112" width="56" height="56" alt="lyufeng000" /><br /><sub>lyufeng000</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/Musan-34"><img src="https://avatars.githubusercontent.com/u/279201993?s=112" width="56" height="56" alt="Musan-34" /><br /><sub>Musan-34</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/qianxuno"><img src="https://avatars.githubusercontent.com/u/179305118?s=112" width="56" height="56" alt="qianxuno" /><br /><sub>qianxuno</sub></a></td>
    <td align="center" width="120"><a href="https://github.com/TLcmmmm"><img src="https://avatars.githubusercontent.com/u/167976723?s=112" width="56" height="56" alt="TLcmmmm" /><br /><sub>TLcmmmm</sub></a></td>
  </tr>
  <tr>
    <td align="center" width="120"><a href="https://github.com/Tofu707"><img src="https://avatars.githubusercontent.com/u/178003727?s=112" width="56" height="56" alt="Tofu707" /><br /><sub>Tofu707</sub></a></td>
  </tr>
</table>
<!-- CONTRIBUTORS:END -->

以上名单保留原项目及社区版贡献者的署名。
