# 桌面端开发（tauri 框架）

原创2023-04-10 00:15·[盒你一起去月球](https://www.toutiao.com/c/user/token/MS4wLjABAAAA_jgmzmNpJOxu79mUM8vjZWVPMQeqf38lOY2physHFi4/?source=tuwen_detail)

# 1、介绍

Tauri 是一个框架，用于为所有主要桌面平台构建微小、极快的二进制文件。开发人员可以集成任何可编译为 HTML、JS 和 CSS 的前端框架来构建他们的用户界面。应用程序的后端是一个来自 rust 的二进制文件，带有一个前端可以与之交互的 API。

Tauri 应用程序中的用户界面目前tao在 MacOS 和 Windows 上用作窗口处理库，gtk在 Linux 上通过Tauri 团队孵化和维护的WRY，它创建了系统 web 视图（以及其他好东西，如菜单和任务栏）的统一界面，在 macOS 上利用 WebKit，在 Windows 上利用 WebView2，在 Linux 上利用 WebKitGTK。

# 2、支持平台

| 平台       | 版本         |
| ---------- | ------------ |
| Windows    | 7 及以上     |
| macOS      | 10.15 及以上 |
| Linux      | 见下文       |
| iOS/iPadOS | 即将退出     |
| 安卓       | 即将推出     |

如需开发Tauri 应用程序，请参阅tauri.app 上的入门指南（

https://tauri.app/v1/guides/getting-started/prerequisites/#setting-up-linux）。

对于运行Tauri 应用程序，我们支持以下配置（这些配置会自动添加为 .deb 的依赖项并与 AppImage 捆绑在一起，因此您的用户无需手动安装它们）：

> 安装了以下软件包的 Debian（Ubuntu 18.04 及更高版本或同等版本）：

- libwebkit2gtk-4.0-37, libgtk-3-0, libayatana-appindicator3-11

> Arch 安装了以下软件包：

- webkit2gtk, gtk3, libayatana-appindicator1

> 安装了以下软件包的 Fedora（最新 2 个版本）：

- webkit2gtk3, gtk3, libappindicator-gtk31



# 3、安全功能

- 本地主机免费
- 安全模式的自定义协议
- 动态提前编译 (dAoT) 与功能性 tree-shaking
- 功能地址空间布局随机化
- 在运行时对函数名称和消息进行 OTP 加盐
- CSP 注入

# 4、Tauri 和 Electron 的比较（官方）

| 细节                 | Tauri | Electron             |
| -------------------- | ----- | -------------------- |
| 安装程序 Linux       | 3.1MB | 52.1MB               |
| 内存消耗 Linux       | 180MB | 462MB                |
| 启动时间 Linux       | 0.39s | 0.80s                |
| 界面服务提供         | WRY   | Chromium             |
| 后端绑定             | Rust  | Node.js (ECMAScript) |
| 底层引擎             | Rust  | V8 (C/C++)           |
| FLOSS(自由/开源软件) | 是的  | 不是                 |
| 多线程               | 是的  | 是的                 |
| 字节码交付           | 是的  | 不是                 |
| 多窗口               | 是的  | 是的                 |
| 自动更新             | 是的  | 是的                 |
| 自定义应用程序图标   | 是的  | 是的                 |
| Windows Binary       | 是的  | 是的                 |
| macOS Binary         | 是的  | 是的                 |
| Linux Binary         | 是的  | 是的                 |
| iOS Binary           | 很快  | No                   |
| Android Binary       | 很快  | No                   |
| 桌面托盘             | 是的  | 是的                 |
| Sidecar Binaries     | 是的  | No                   |

> 1. Electron 在 Linux 上没有本机自动更新程序，但由 electron-packager 提供

> 2.打包后程序大小对比（在Macos系统下）

![img](./tauri/4bfacf0adc3f40febc321838fda41ba5.image)



![img](./tauri/52cfda793de44f2182cb948741820ed9.image)



# 5、安装前提条件-macOS

1、要安装 CLang 和 macOS 开发依赖项。为此，请在终端中运行以下命令：

```
xcode-select --install
```

2、要在 macOS 上安装 Rust，请打开终端并输入以下命令

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

在窗口中出现以下提示，代表安装成功

```
Rust is installed now. Great!
```

# 5、安装前提条件-Windows

1、Microsoft Visual Studio C++ 构建
您将需要安装 Microsoft Visual Studio C++ 构建工具。最简单的方法是安装Build Tools for Visual Studio 2022。当询问要安装哪些工作负载时，请确保选择“C++ 构建工具”和 Windows 10 SDK。

![img](./tauri/698b4018dd0347429e9f22b30f4d9c93.image)



2、Tauri 严重依赖 WebView2 在 Windows 上呈现 Web 内容，因此您必须安装 WebView2。最简单的方法是从Microsoft 网站下载并运行 Evergreen Bootstrapper 。
提示：WebView2 预装在 Windows 11 中

3、安装Rust，地址：

https://www.rust-lang.org/tools/install

6、开始创建tauri应用程序

```
npm create tauri-app
```

1、输入app的名字，不输入默认为tauri-app，直接回车。

![img](./tauri/53d5419971414670b8158002c34a7015.image)



2、输入窗口的标题，默认直接回车：

![img](./tauri/f1a3930b3a334675a8ccbd13c0ab62c6.image)



3、前端UI模板搭配选择：

![img](./tauri/bac132609c60416286f3bf4bc6105d0e.image)



4、是否添加tauri-apps/api包的依赖。

![img](./tauri/94e45c7717f940a299e55016c2cd27de.image)



5、选择vite的模板

![img](./tauri/aae4b65d2e8642a287fd80326bec8d42.image)



6、项目初始化完成，依赖已安装完成。

![img](./tauri/fffb15271fac4b97a305f50afdedaa5f.image)



7、进入tauri-app目录，运行命令：

```
npm run tauri dev
```



![img](./tauri/f5546be9e9a345d5a858b0110880017a.image)



在浏览器中，打开链接地址：http://localhost:5173/

![img](./tauri/2f1a022c900b4027a51561e67a0f51fb.image)



然后桌面端，程序没有打包,因为Rustde 第三方包都集中在crates.io网站上面,因为镜像问题，需要更换成国内镜像。
在 $HOME/.cargo/config 中添加如下内容：

```
# 放到 `$HOME/.cargo/config` 文件中
[source.crates-io]
#registry = "https://github.com/rust-lang/crates.io-index"

# 替换成你偏好的镜像源
replace-with = 'ustc'
#replace-with = 'sjtu'

# 清华大学
[source.tuna]
registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"

# 中国科学技术大学
[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"

# 上海交通大学
[source.sjtu]
registry = "https://mirrors.sjtug.sjtu.edu.cn/git/crates.io-index"

# rustcc社区
[source.rustcc]
registry = "git://crates.rustcc.cn/crates.io-index"
```

配置完成，重新运行命令，会看完整个编译结束。

![img](./tauri/ec069ad2008248998296ed4d1eeb3c3a.image)



出现桌面端的界面

![img](./tauri/37111081fdc54ce5b9ed3965ef8a7faf.image)



# 7、进行桌面打包

```
npm run tauri build
```



![img](./tauri/8de497410ff944ecb20cc91b17dfd2fb.image)



在target目录下面，生成对应桌面端app的文件，原文件大小**9M**，如下图所示：

![img](./tauri/c760fe4aad904abdb21aa63d6f29dd73.image)



***想了解更多，可以查看官方文档：

https://tauri.app/v1/guides/***