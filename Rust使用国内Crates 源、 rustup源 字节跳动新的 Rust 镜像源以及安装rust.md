# Rust使用国内Crates 源、 rustup源 |字节跳动新的 Rust 镜像源以及安装rust

- 文章目录
- 一、背景
- 二、字节跳动新的 Rust 镜像源以及安装rust
	- crates.io Mirror
	- Rustup Mirror
	- 安装Rust
- 三、rust 使用其他国内镜像以及安装rust
	- 使用国内源 (ustc) 之后依然无法下载最新包

## 一、背景 ##

Rust社区公开的第三方包都集中在crates.io网站上面,他们的文档被自动发布到doc.rs网站上。

rustup是一个管理 Rust 版本和相关工具的命令行工具。rustup 是一个命令行应用,能够下载并在不同版本的 Rust 工具链中进行切换

Rust开发时有时使用官方的源太慢,可以考虑更换使用国内的源。

## 二、字节跳动新的 Rust 镜像源以及安装rust ##

字节跳动搞的，希望能帮助建设国内的 rust 生态，感兴趣的话可以试用，无任何限速（实际上是 1000Gbps）。

地址：https://rsproxy.cn/

**crates.io Mirror**

    vi ~/.cargo/config

```
[source.crates-io]
replace-with = 'rsproxy'

[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"

[registries.rsproxy]
index = "https://rsproxy.cn/crates.io-index"

[net]
git-fetch-with-cli = true
```

**Rustup Mirror**

~/.zshrc or ~/.bashrc:

    vi ~/.bashrc

```
export RUSTUP_DIST_SERVER="https://rsproxy.cn"
export RUSTUP_UPDATE_ROOT="https://rsproxy.cn/rustup"
```

**安装Rust**

完成上面2步，然后执行：

```
# export the env above first

curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh         
```

## 三、rust 使用其他国内镜像以及安装rust ##

参考： http://mirrors.ustc.edu.cn/help/crates.io-index.html

由于rustup官方服务器在国外
如果直接按照rust官网的安装方式安装非常容易失败，即使不失败也非常非常慢

我们需要指定 RUSTUP_DIST_SERVER（默认指向 https://static.rust-lang.org）和 RUSTUP_UPDATE_ROOT （默认指向https://static.rust-lang.org/rustup），这两个网站均在中国大陆境外，因此在中国大陆访问会很慢，需要配置成境内的镜像。

方式一：

设置环境变量 RUSTUP_DIST_SERVER(用于更新 toolchain)
以及 RUSTUP_UPDATE_ROOT(用于更新 rustup)

    vi /etc/profile

```
# 清华大学

RUSTUP_DIST_SERVER=https://mirrors.tuna.tsinghua.edu.cn/rustup

# 中国科学技术大学

RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup

# 上海交通大学

RUSTUP_DIST_SERVER=https://mirrors.sjtug.sjtu.edu.cn/rust-static/
```

    source /etc/profile

使用国内镜像的方法

首先修改一下上面的命令，将安装脚本导出

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs > rust.sh
```

打开 rust.sh 脚本

修改环境变量

```
export RUSTUP_DIST_SERVER=https://mirrors.tuna.tsinghua.edu.cn/rustup
将 RUSTUP_UPDATE_ROOT 修改为
RUSTUP_UPDATE_ROOT=“https://mirrors.ustc.edu.cn/rust-static/rustup”
```

执行脚本

    bash rust.sh

测试是否安装成功

    rustc --version

**使用国内源 (ustc) 之后依然无法下载最新包**

中国科大的镜像不稳定，有单个 ip 的并发限制， 官方说添加 CARGO_HTTP_MULTIPLEXING=false 参考链接： mirrors.ustc.edu.cn/help/crates.io-…
Rust dependencies依赖管理crates.io原理梳理
原文链接：https://blog.csdn.net/mutourend/article/details/106415130

这个是说在使用 nightly 版本的时候可能会报错，我直接用的是官方的稳定版… 不过似乎半夜是可以下载的，可能是和国内用户访问的频率流量有关

rm /root/.cargo/config -f #删掉本地 中科大配置，使用默认官网下载

使用 nightly 版本时，Crates 源可能会出现 Couldn’t resolve host name (Could not resolve host: crates) 错误（见 https://github.com/ustclug/discussions/issues/294）。一个临时的解决方法是在运行 cargo 的时候加入环境变量 CARGO_HTTP_MULTIPLEXING=false。

还因各种原因，即使切换为国内镜像源，仍然无法从crates.io中下载各依赖包的情况。

经验证，无法下载是因为局域网内https://crates-io.proxy.ustclug.org/api/v1/crates被屏蔽无法连接，而https://crates.io/api/v1/crates 可连接成功。

最简单的方法就是切换为默认源，哪怕慢点。

————————————————

版权声明：本文为CSDN博主「西京刀客」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。

原文链接：https://blog.csdn.net/inthat/article/details/106742193
