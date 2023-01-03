# 【Rust日报】2022-12-21~22 谷歌Android 团队的 Rust 教程

**谷歌Android 团队的 Rust 教程**

这是由 Android 团队开发的为期四天的 Rust 课程。课程涵盖基本语法到泛型等高级主题和错误处理。它还包括最后一天的Android特定内容。

课程的目标是教你用 Rust。我们假设你不了解 Rust

- 让你全面了解 Rust 语法和语言。

- 使您能够在 Rust 中修改现有程序和编写新程序。

- 向您展示常见的 Rust 语法。


在第 4 天，我们将介绍特定于 Android 的内容，例如

- 在 Rust 中构建 Android 组件。

- AIDL 服务器和客户端。

- 与 C、C++ 和 Java 的互操作性。


ReadMore: https://google.github.io/comprehensive-rust/

**rust-gpu - v0.4 发布**
例子：

```
use glam::{Vec3, Vec4, vec2, vec3};

#[spirv(fragment)]
pub fn main(
    #[spirv(frag_coord)] in_frag_coord: &Vec4,
    #[spirv(push_constant)] constants: &ShaderConstants,
    output: &mut Vec4,
) {
    let frag_coord = vec2(in_frag_coord.x, in_frag_coord.y);
    let mut uv = (frag_coord - 0.5 * vec2(constants.width as f32, constants.height as f32))
        / constants.height as f32;
    uv.y = -uv.y;

    let eye_pos = vec3(0.0, 0.0997, 0.2);
    let sun_pos = vec3(0.0, 75.0, -1000.0);
    let dir = get_ray_dir(uv, eye_pos, sun_pos);
     
    // evaluate Preetham sky model
    let color = sky(dir, sun_pos);
     
    *output = tonemap(color).extend(1.0)
}
```

ReadMore:https://github.com/EmbarkStudios/rust-gpu/

tabled - 一个易用的rust制表

```
use tabled::{Tabled, Table};

#[derive(Tabled)]
struct Language {
    name: &'static str,
    designed_by: &'static str,
    invented_year: usize,
}

let languages = vec![
    Language{
        name: "C",
        designed_by: "Dennis Ritchie",
        invented_year: 1972
    },
    Language{
        name: "Rust",
        designed_by: "Graydon Hoare",
        invented_year: 2010
    },
    Language{
        name: "Go",
        designed_by: "Rob Pike",
        invented_year: 2009
    },
];

let table = Table::new(languages).to_string();

let expected = "+------+----------------+---------------+\n\
                | name | designed_by    | invented_year |\n\
                +------+----------------+---------------+\n\
                | C    | Dennis Ritchie | 1972          |\n\
                +------+----------------+---------------+\n\
                | Rust | Graydon Hoare  | 2010          |\n\
                +------+----------------+---------------+\n\
                | Go   | Rob Pike       | 2009          |\n\
                +------+----------------+---------------+";

assert_eq!(table, expected);
```

ReadMore: https://google.github.io/comprehensive-rust/

**MacroKata**

一系列的练习去学习Rust宏。

Github: https://github.com/tfpk/macrokata

From 日报小组 冰山上的 mook && MalikHou

- 社区学习交流平台订阅：

- Rustcc论坛: 支持rss


微信公众号：Rust语言中文社区

————————————————

版权声明：本文为CSDN博主「Rust语言中文社区」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。

原文链接：https://blog.csdn.net/u012067469/article/details/128425558