title: Sublime折腾记
date: 2016-08-27 11:42:01
tags:
- tech
- editor
---

## 1. why Sublime

针对一个后端是Java的前端空城师，那么这个年代我的编辑器/IDE选择有如下几个：

- (IntelliJ IDEA)[https://www.jetbrains.com/idea/]
- (WebStorm)[https://www.jetbrains.com/webstorm/]
- (Sublime Text)[http://www.sublimetext.com/]
- (Atom)[https://atom.io/]
- (Visual Studio Code)[https://code.visualstudio.com]

OK，下面开始撕逼，每个群里和论坛里都有旷日持久的编辑器大战，框架大战。其实最终的结论都是一个，**适合自己的才是最好的**，所以我说说我现在选择编辑器的几个因素：

- 尚未入职，电脑是Windows
- 后端是Java，使用Velocity模板引擎
- 前后端分离，且并行做项目，需要打开多个项目文件

首先，以上5款编辑器都用了个遍，先说IDEA，好处是IDEA UL版支持Velocity语法，缺点是好多都是针对Java的工具和插件，很多功能并不会用到，总感觉这么大我却用不到对我很不友好；WebStorm，不支持Velocity语法高亮，毕竟是IDE很多很多高效的插件。然而Jet家的这两款IDE由于占内存太大，并且不能打开多个项目而最终否定掉，index的时候也极慢，虽然我的内存有16GB，处理器是I7；Atom，这些编辑器里我最喜欢的就是Atom，GitHub出品，UI风格，基于Node.js编写，强大的插件生态等等等，然而他在Win上是在是不给力啊，烂泥扶不上墙啊，老特么崩溃，老特么卡死，敲两个字就卡那儿半天，卸了装卸了装好多次了，虐我千百遍，最终还是要抛弃你，等Atom稳定了或者换到Mac上再用吧；vs code，微软出品，vs团队开发，也是基于node，相当于封装了一下atom，然而强大的开发团队在优化上比atom好太多，不能加载多个Project文件被瞬间枪毙，一些快捷键风格也不是很统一，延续了vs的风格，记了这么多快捷键好累。

其实一入坑前端的时候就是Sublime，还特地去慕课上学了Petter的《快乐的Sublime编辑器》，然而后来为了追求时尚，心态浮躁，各种编辑器尝试来装X，喏，最后还得回归本源，支持veolicity，多项目文件，丰富的插件，熟悉的快捷键，唯一担心的是怕他以后的更新幅度慢了，开发者都转去其他编辑器。

## 2. let's Sublime

### 2.1 下载

链接在这儿 (Sublime Text)[http://www.sublimetext.com/]

### 2.2 破解

禁忌话题，你懂得，如果没有注册的话保存五次就会弹出提示框，很烦，去网上搜Lisence，一堆一堆的

### 2.3 DIY

拿来一款编辑器，首先要调整成自己喜欢的姿态，包括一堆插件和配置项

先改字体和字号，写程序就要用等宽字体，很多人推荐`Source Code Pro` 号称写程序专用，然而我喜欢`Consolas`更多一点，然后字号调整成14，有个什么说法忘记了

```
    "font_face": "Consolas",
    "font_size": 14,
```

有代码洁癖，我喜欢把所有空格显示出来，通过编辑器配置和安装高亮多余空格插件`Bracket Highlighter`

```
    "draw_white_space": "all",
```

将tab转换为4个空格

```
    "tab_size": 4,
    "translate_tabs_to_spaces": true
```

在选择前置括号时，自动匹配后置括号，安装插件`Trailing Spaces`


将某些中文会出现乱码的编码格式转换为UTF-8，安装插件`ConvertToUTF8`

为了让Side Bar更牛逼，安装插件`SideBarEnhancements`

前端必备`Emmet`

预览Markdown`Markdown Preview`