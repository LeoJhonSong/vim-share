---
presentation:
  width: 1920
  height: 1400
  theme: league.css
  backgroundTransition: 'convex'
  # progress: false
  # center: false
  # controls: false
  transition: 'convex'
  enableSpeakerNotes: true
---

<!-- slide data-notes="更多分享我自己的使用经验, 而不是在基础使用上费口舌. (当然也会提一些)."
-->

# 我的vim经验分享

<!-- slide -->

## 温馨提示 🤗
<br />

- 如果你是在浏览器里看这个幻灯片, 你可以按 <kbd>F11</kbd> 来进入全屏, 获得更好的观看体验. 再次按 <kbd>F11</kbd>就能够退出全屏. (在macOS似乎不是这么操作的)
<br />

- 在有些页幻灯片的备注里也有一些文字, 通过按 <kbd>s</kbd> 来打开演讲者备注页面查看备注.
<br />

- 按 <kbd>?</kbd>你可以看到能在本幻灯片中使用的快捷键列表.

<!-- slide -->

### showoff

先来展示一张我的vim在编辑我的vim配置文件时的截图 😏

![](vim/showoff.png)

<!-- slide  -->

## 目录

---
1. 认识vim
2. 都2020了怎么还在用vim
3. vim操作入门
4. vim配置入门
5. 获得帮助

<!-- slide data-transition="zoom" data-background-image="vim/vim_drill_small.jpg" data-background-transition="zoom"
data-notes="vim是什么? 是电钻驰名品牌吗?
这张图来自vim官网
顺带一提因为vim作者曾去过乌干达, vim一直很热衷于帮助贫穷乌干达儿童 (但我在vim官网看到的的vim作者在乌干达的活动照他去的地方并没那么差😏"
-->

## 认识vim

<!-- slide -->

### 历史

推荐阅读: [Vim 和 Neovim 的前世今生](https://jdhao.github.io/2020/01/12/vim_nvim_history_development/)

<!-- slide -->

### 常见困惑与误解 🤤

<!-- slide data-center=false data-height=2000
data-notes="前几年vim或许有些方面跟不上时代, 但随着vim8推出vim变得较为潮流. 从另一方面它从未过时
任何工具都有其局限性, vim只能呈现纯文本, 无法显示网页, 图片等需要渲染的东西. markdown-preview.nvim是以一个位置同步的浏览器页面来实现markdown文件预览的. 但也有其他方式, 比如一个终端浏览器. 只要终端支持显示图片, 那么就基本完美.
vim的剪贴板如何表现是可以自己设定的, 可以设置为选中即放入系统粘贴板. 这个后面会提到.
下方有一张Google搜vim图片"
-->

- 代码高手都会vim吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->
- 都有如此多现代编辑器了vim是不是早已经过时了 <!-- .element: class="fragment fade-in-then-semi-out"  -->
- vim是最好的编辑器没有之一吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->
- vim和其他软件之间的复制粘贴很麻烦吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->
- vim操作起来很麻烦吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->
- vim配置起来很麻烦吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->
   vim甚至提供了一个vimrc样例. 在终端输入`vim ~/.vimrc`来创建一个vimrc并进入, 然后输入:
   `:r $VIMRUNTIME/vimrc_example.vim`

    💡 我的$VIMRUNTIME为`/usr/local/share/vim/vim82`
- 每个vim用户的vim都长得很不一样吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->
  
  - 大多数普通vim用户的vim界面是长得差不多的. (也就是我在showoff中展示的那样) 正如在下面这个在谷歌图片搜索vim的结果, 可以看到这些vim都长得差不多: 顶部是标签页以及缓冲区的显示, 底部是状态栏, 左边是文件树, 右边可能会有ctag之类的东西.

<!-- slide vertical=true -->

![](vim/vim_in_google.png)

<!-- slide data-notes="我的$VIMRUNTIME之所以在那里是因为这是我自己编译的vim最新版. 从apt安装的是vim8.0
evim: 傻瓜模式😏
neovim与vim的具体关系可以看上面那个讲vim与nvim历史的文章
neovim的默认开启功能更多, 但一般vim用户都会有配置文件, 因此这没什么所谓
neovim社区更加开放, vim的开发一直由vim作者把控, 十分谨慎
neovim大幅重构, 通常新功能比vim发布得快
neovim促进vim发展
下面是一段从less这个应用的man里截取的文字."
-->

- vi, vim, vim8, gvim,evim, rvim, mvim, nvim之间是什么关系啊😵 <!-- .element: class="fragment fade-in-then-semi-out"  -->
  - vim: **V**i **IM**proved
  - vim8: 指vim第8版
  - gvim: GUI模式的vim
  - evim: 简单模式的gvim
  - rvim: 受限模式的evim
  - mvim: macvim, 专门为mac适配了的GUI模式vim
  - nvim: neovim, (new vim谐音)新生代vim. neovim与vim不完全兼容, 但有一些很有意思的功能. 比如可以通过**MessagePack-RPC protocol**从其他程序接入neovim. [这个](https://marketplace.visualstudio.com/items?itemName=asvetliakov.vscode-neovim)是用于在VSCode集成完整版neovim的插件.
- vim在Windows用不了吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->
- vim里只能用键盘操作, 不能用鼠标吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->
- vim无法自动保存吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->

  - [vim-auto-save](https://github.com/907th/vim-auto-save)
- vim适合什么语言的开发呢🤔 <!-- .element: class="fragment fade-in-then-semi-out"  -->
- 打开大文件认准vim吗 <!-- .element: class="fragment fade-in-then-semi-out"  -->

  > Less does not have to read the entire input file before starting, so with large input files it starts up faster than text editors like vi (1).

<!-- slide data-notes="以下是我自己的体会, 仅代表个人观点
"
-->

## 都2020了怎么还在用vim 😏

<!-- slide -->

### 应用场景 🉑

- 编辑在性能不好的服务器上的代码

  有的编辑器提供很强大的支持, 比如VSCode的[Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)允许在服务器上安装VSCode插件, 这样通过这个插件可以用本地VSCode进行服务器端的开发. 但这需要服务器性能还不错, 才能获得良好的体验. 而在编辑树莓派3等性能不太好的服务器的代码时vim可能是一个更好的选择.

- 重复性工作

  比如在稍微底层的开发中经常需要写一些敲就完事的switch case等无脑代码, 也有时候需要处理一些类似于csv文件这样的格式比较固定的文件. 通过宏录制, 块编辑等功能减少工作量. 稍后会有一个演示.

- 需要自己开发插件使用

  当编辑器本身以及社区提供的功能无法满足你的需求时你就需要自己写一些代码开发一个"插件"来满足你的需求, vim会是一个很好的选择. 因此vimscript是一种**语法十分简单**的语言, 单纯是把vim操作放在一起, 因此写一小段vimscript十分简单. 理论上vim也允许你使用你熟悉的**任何**语言来进行插件开发. 而如果是在VSCode中开发插件你需要去了解TypeScript, 你需要去阅读大量文档. 如果你需要的仅仅是一个小功能, 那么开发VSCode插件的性价比很低.

<!-- slide -->

### 亮点 ✨

- 全平台

  vim在绝大多数平台都是可用的, 从Linux, macOS到Windows, 甚至许多arm架构的系统. 因为vim只是一个终端应用, 实现起来相对没那么复杂.

- 资源十分丰富

  vim的社区仍然十分活跃, 有大量插量可用

- 块编辑

  下方一页👇是一个用块编辑删除一个471行的文件中第一列数据的gif

- 简单组合命令就能实现一些神奇的功能, 比如**重复行查找**, **不需要版本管理系统就可以可视化对比文件改动前后差异**

  通过下面这两行的按键就可以在vim中轻松的完成**重复行的查找**

  `:sort`
  `/^\(.\+\)$\n\1`

- 宏录制

  宏录制实在是一个很强大的功能, 能够录制你的操作, 配合vim灵活的命令能极大地减少工作量. 后一页👉是一个展示宏录制之强大的一个gif.

  💡 有时候宏录制可能执行得很慢, 可能是因为**重绘窗口消耗了大量时间**. 通过在配置文件中加一行`set lazyredraw`让vim惰性重绘窗口, 在执行宏期间不会重绘窗口, 能极大提升执行宏的速度.

<!-- slide vertical=true data-background-image="vim/v-block.gif" data-background-size="contain" -->


<!-- slide data-background-image="vim/macro.gif" data-background-size="contain" -->

 gif里左上角窗口是我从[SDL Keycode Lookup Table](https://wiki.libsdl.org/SDLKeycodeLookup)复制下来的markdown格式表格, 右上角窗口是[input-event-codes.h](https://github.com/torvalds/linux/blob/master/include/uapi/linux/input-event-codes.h), 而下方的窗口是在写一个C语言的**switch case**.


<!-- slide -->

### 亮点 ✨

- 更为强大的查找与替换

  vim默认使用正则表达式来进行查找, 而在替换时可以指定替换行数

  通过按`:2,5s/old/new/gi`可以无需确认地将第二到第五行的所有**old**替换为**new**. 命令中的`g`表示替换同一行中所有匹配项, 否则只替换第一个, `i`则是忽略大小写. 还有一个较为常用的flag是`c`, 是否每一次替换前都需要确认.

  💡 更多替换时可用参数可以在vim中按`:h :s_flags`来查看

- 可扩展性极强

  vimscript语法十分简单, 就是能在命令模式使用的命令的组合. 对于简单的一行脚本可以直接绑定给按键组合. 另外因为vim可以运行外部命令, 因此理论上可以用任何语言进行插件开发.

  只需要下方这行代码加入到配置文件, 当你忘记使用sudo地编辑了一个需要管理员权限的文件, 不需要退出vim加上sudo重新来编辑一次, 只需要按 <kbd>Ctrl</kbd> <kbd>W</kbd> 然后输入密码, 就写入了这个文件. 此时由于vim检测到外部程序改动当前文件, 会询问你怎么处理, 只需按 <kbd>L</kbd> <kbd>Enter</kbd>就好了.

  ```vim
  nnoremap <C-w> :w !sudo tee > /dev/null %
  ```

  解释一下这行代码: 首先这是一条不可递归的normal模式**键映射**, 将`:w !sudo tee > /dev/null %`这个命令绑定到按键组合 <kbd>Ctrl</kbd> <kbd>W</kbd>. 而这个命令的意思是将当前缓冲区的内容传递给`tee`这个数据重定向命令 (这是vim外部的, 是linux命令), 而tee将得到的vim缓冲区内容分别写入到了黑洞设备`/dev/null` (传到这里的东西相当于被丢弃掉了)以及当前文件 (vim的%寄存器里存储的是当前文件名) 🔗关于这个命令更为详细的解释请看[这条stackoverflow回答及其评论](https://stackoverflow.com/q/2600783/10088906)

<!-- slide -->

### 与其他代码工具的关系 💬

- 与大型IDE的区别

  IDE即集成开发环境, 这类软件通常是**开箱即用**的**针对某一个应用场景**的一整套开发工具. 比如[Clion](https://www.jetbrains.com/clion/)专注于C/C++开发, 而[Pycharm](https://www.jetbrains.com/pycharm/)专注于科学计算 Python/Web Python开发. 号称宇宙第一IDE的[Visual Studio](https://visualstudio.microsoft.com/)能应对的应用场景相对于编辑器来说也不算多.

  而只要你安装相应插件编辑器就可以用于任何应用场景, 完全可以称得上**万金油**. 缺点是因为使用的是不同插件作者们提供的插件, 因此在整体上基于编辑器自己搭建的开发环境可能**在逻辑, 操作上风格没那么一致**. 因为开发人员的优势IDE的各个组件会更像一个整体. (但这也导致你很难对IDE进行高度个性化)

- 与VSCode等现代编辑器的关系

  我认为vim与VSCode等现代编辑器是**互补关系**, 而不是使用了vim就不该使用这些编辑器了. 正如前面所说, vim也有其局限性, **只能呈现文本内容**, etc. 比如我更喜欢用VSCode来编辑markdown文件, 因为可以在窗口里实时预览等; 我也喜欢在VSCode中进行版本管理, 因为VSCode本身集成的源代码管理功能以及[GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)这个插件给我提供了很多图形化按钮能让我版本管理时的体验大幅提升. 再比如我很喜欢VSCode的[小地图](https://code.visualstudio.com/docs/getstarted/userinterface#_minimap), 但这注定是vim中无法实现的功能.

<!-- slide data-notes="只挑选一些内容来介绍" -->

## vim操作入门 😎

<!-- slide -->

### vim多文件编辑中的三个重要概念

- 窗口 (window)
- 标签页 (tab)
- 缓冲区 (buffer)

  vim帮助文档中对这三个概念的总结是这样的:

  >Summary:
  >   A buffer is the in-memory text of a file.
  >   A window is a viewport on a buffer.
  >   A tab page is a collection of windows.

  确切的说当你打开vim你编辑的是一个用于呈现一个缓冲区的, 包含在一个标签页中的窗口😏

  也就是说窗口, 标签页, 缓冲区这三个概念是用户依次越来越接触不到的. 其中缓冲区的表现我觉得**和一个硬件设备的缓冲区很像**. 比如在键盘上按键后按键被储存到了键盘的缓冲区, 在C语言中可以通过`scanf()`函数来读取键盘缓冲区的内容. 在vim中我们在编辑文件时实际编辑的是包含文件内容的缓冲区, 在用`:w`命令将缓冲区内容写入文件前文件本身并没有被改动.

  更多关于这三个概念的解释, 操作请在vim输入`:h windows-intro`查看文档, 或者看[vim多文件编辑](https://harttle.land/2015/11/14/vim-window.html)

<!-- slide -->

### 移动 🏃

❗️ 我只是列出了**我常用**的移动方式, 实际上移动方式还有**很多**, 也有一些好用但我个人不习惯的,
也有更加技巧性但可能也没那么容易的方式. 这些都等待由你探索 👀

- 窗口内

  - 光标移动

    vim给出的记住`hjkl`的小技巧:

    > The h key is at the left and moves left.
    > The l key is at the right and moves right.
    > The j key looks like a down arrow.

    给出一些常用的光标移动方式:
    - `h`, `j`, `k`, `l`, 方向键
    - 行内移动: `w`(ord), `e`(nd), `b`(ack), `0` (一行的开头), `^` (一行的第一个非空格字符处), `$` (一行的最后)
    - 页内移动: `H`(igh), `M`(iddle), `L`(ow)
    - `gg` (文件第一行的第一个非空格字符处), `G` (文件的最后一行第一个非空格字符处)
    - [vim-easymotion](https://github.com/easymotion/vim-easymotion)插件

    ✔️ 详情请在vim输入`:h motion.txt`查看

  - 窗口滚动

    - 整屏翻页: <kbd>Ctrl</kbd> <kbd>F</kbd>(orward), <kbd>Ctrl</kbd> <kbd>B</kbd>(ackward)
    - 半屏翻页: <kbd>Ctrl</kbd> <kbd>U</kbd>(p), <kbd>Ctrl</kbd> <kbd>D</kbd>(own)
    - 将光标所在行移动到: `zt`(op, 窗口顶部), `zz` (窗口正中), `zb`(ottom, 窗口底部)

    ✔️ 详情请在vim输入`:h scroll.txt`查看

<!-- slide -->

### 移动 🏃

- 窗口间

  以 <kbd>Ctrl</kbd> <kbd>W</kbd> 起手的是**窗口命令**, 然后可以接`hjkl`或者方向键来在窗口间移动.
  有一个比较特别的是 <kbd>Ctrl</kbd> <kbd>W</kbd>  <kbd>Ctrl</kbd> <kbd>W</kbd> 可以移动到对角线方向窗口

- 标签页间

  标签页间的移动的常用默认快捷键是 <kbd>Ctrl</kbd> <kbd>PgDn</kbd> (下一标签页)和 <kbd>Ctrl</kbd> <kbd>PgUp</kbd> (上一标签页). 如果你觉得这两个快捷键不合理你也可以重新映射, 因为这两个快捷键本身只是`:tabnext`和`:tabprevious`两个命令的键映射

  💡 更详细说明请输入`:h tabpage.txt`查看

- 缓冲区间

  缓冲区间的移动我目前使用得还不多, 但看起来是很强大的功能, 这里我放上一个链接吧.
  🔗[Vim 多文件编辑：缓冲区](https://harttle.land/2015/11/17/vim-buffer.html)

<!-- slide -->

### 关于窗口大小调整不再在此赘述, 请`:h window-resize`查看 😜

<!-- slide -->

### 寄存器

💡 看表格可能并不那么直观, 可以按`:registers`显示所有**有值**的寄存器的类型和值.

| 类型                | 标识               | 读写者 | 是否为只读 | 包含的字符来源                                               |
| ------------------- | ------------------ | ------ | ---------- | ------------------------------------------------------------ |
| Unnamed             | `"`                | vim    | 否         | 最近一次的复制或删除操作 (`d`, `c`, `s`, `x`, `y`)           |
| Numbered            | `0`到`9`           | vim    | 否         | 寄存器`0`是最近一次复制. 寄存器`1`是最近一次删除. 寄存器`2`是倒数第二次删除, 以此类推. 对于寄存器`1`至`9`, 他们其实是只读的最多包含 9 个元素的队列. 这里的队列即为queue数据类型 |
| Small delete        | `-`                | vim    | 否         | 最近一次行内删除                                             |
| Named               | `a`到`z` `A`到`Z` | 用户   | 否         | 如果你通过复制操作存储文本至寄存器`a`, 那么`a`中的文本就会被完全覆盖. 如果你存储至`A`, 那么会将文本添加给寄存器`a`, 不会覆盖之前已有的文本 |
| Read-only           | `:`和`.`和`%`      | vim    | 是         | `:`是最近一次使用的命令, `.`是最近一次插入的文本, `%`是当前的文件名 |
| Alternate buffer    | `#`                | vim    | 否         | 大部分情况下, 这个寄存器是当前窗口中, 上一次访问的缓冲区. 请参阅`:h alternate-file`来获取更多帮助 |

<!-- slide -->

| 类型                | 标识               | 读写者 | 是否为只读 | 包含的字符来源                                               |
| ------------------- | ------------------ | ------ | ---------- | ------------------------------------------------------------ |
| Expression          | `=`                | 用户   | 否         | 确切的说这不是一个储存文本的寄存器, 而是一种在用到寄存器的命令里使用表达式的技巧 |
| Selection           | `+`和`*`           | vim    | 否         | `*` 和 `+` 是剪贴板寄存器. 区别在于`*`在使用X窗口系统的系统里是对应的PRIMARY剪贴板. 想知道PRIMARY是什么请看[X选区原理科普](https://blog.lilydjwg.me/2019/7/22/fcitx-paste-primary.214679.html), 想了解如何更好地使用剪贴板寄存器请看[这个stackoverflow回答](https://vi.stackexchange.com/a/96/23650)    |
| Drop                | `~`                | vim    | 是         | 最后一次拖拽到vim的文本 (需要"+dnd"支持, 暂时只支持GTK GUI. 请参阅`:help dnd`及`:help quote~`) |
| Black hole          | `_`                | vim    | 否         | 黑洞寄存器. 黑洞寄存器不会储存任何值. 对于当前操作, 如果你不希望在其他寄存器中保留文本, 那就在命令前加上`_`. 比如, `"_dd`命令不会将文本放到寄存器`"`, `1`, `+`或`*`中. |
| Last search pattern | `/`                | vim    | 否         | 最近一次通过`/`, `?`或`:global`等命令调用的匹配条件      |

<!-- slide -->

## vim配置入门 👴

<!-- slide data-background-image="vim/vim--version.png" data-background-size="100% 100%" -->

### 在进行配置与插件安装之前你最好在终端运行`vim --version`打印出vim的版本信息, 查看你的**vim版本**以及**哪些功能开启了支持**.

- 如果你的vim版本小于, 建议更新至至少vim8.0, 这样很多很有必要的新功能才能够使用
- 比如如果你想使用vim进行python3的开发那你最好能看到included features里有 **+python3** 开头的词, 这表示开启了python3的支持, 这样你才能更好地进行python3的开发以及使用一些用于开发python3的插件 (比如YouCompleteMe)
- 而如果你想要将vim中的文本复制到系统粘贴板你需要看到 **+clipboard**
- 如果你缺少你需要的功能你可以下载[vim源码](https://github.com/vim/vim)自己编译. 在源码的`src/Makefile`文件里有详细的编译说明, 在里面根据说明设置你想要的参数就好.

<!-- slide -->

### 基础设置

因为较长所以直接放出[我的vimrc](https://github.com/LeoJhonSong/vimrc/blob/master/default.vim). 我的vimrc基本是按照VSCode的图形化设置里对配置的分类方式分类的. 其中**Workbench Settings**和**Editing Settings**部分即我的基础设置

<!-- slide -->

### 颜色主题

这里有一份关于创建自己的颜色主题的幻灯片[Creating Your Lovely Color Scheme](https://speakerdeck.com/cocopon/creating-your-lovely-color-scheme)可供参考

获取/设计颜色主题:
[Vivify](http://bytefluent.com/vivify/)
[vimcolors](https://vimcolors.com/)

- 值得一提的是, 如果你的终端的文字的背景颜色是有透明度的, 那么你的vim背景颜色也会是带透明度的. 这有优点也有缺点. 一方面就像下面这个是我在macOS的**terminal.app**里的vim, 会很好看, 但另一方面因为文字前景颜色, 也就是文字颜色加了透明度会变得难以看清, 但不加透明度的话, 如果你使用powerline样式的终端提示符, 会明显看出有破绽.

  💡 你可以输入`echo -e "\e[1;33;41m 我怎么变色了 \e[0m"`看输出文字的背景颜色是否有透明度来得知你的终端是哪种情况

<img src="vim/transparent.jpg" style="width: auto; height: 680px;" ></img>

<!-- slide data-notes="设计一套自己喜欢的键映射逻辑" -->

### 键映射

- 在vim里按`:h map-which-keys`可以看到vim给出的设计键映射的建议
- 在vim里按`:h index`可以看到一份列出了每个模式所有命令
- 技巧: 插入模式下按<kbd>Ctrl</kbd> <kbd>V</kbd>后按键

❗️ 在**终端vim**中[有些键无法被捕捉, 有些键无法使用](https://vimhelp.org/vim_faq.txt.html#faq-20.4).

<!-- slide -->

### 插件

首先管理vim的插件你可以手动管理, 也可以使用vim的插件管理器. 我推荐[vim-plug](https://github.com/junegunn/vim-plug).

- 借助vim-plug我们只需要在.vimrc中以很简单的语法提及一个插件vim-plug就会**自动下载**好它, 可以**指定在下载好插件后需要执行的命令** (有的插件还需要执行一些命令来安装, 比如YouCompleteMe), 可以**指定在什么条件下加载插件** (减少不必要的加载能让vim变得更快). 具体使用方式详见上方vim-plug网页.
- 我推荐的插件请参见我的vimrc里我安装的插件.

<!-- slide -->

### vimscript

主要用于**小规模功能**的实现. 比如一个函数或者一行代码的解决方式.

- 当需要的功能较为复杂时仍使用vimscript来进行插件开发可能就不是很好的选择了, 因为这时**开发以及维护**会变得困难起来. 因为在vim里可以调用外部命令因此理论上你可以使用**任何语言**来进行插件开发. 比如代码补全插件[YouCompleteMe](https://github.com/ycm-core/YouCompleteMe)主要使用**Python**, 另一个代码补全插件[CoC.nvim](https://github.com/neoclide/coc.nvim)则主要使用**TypeScript**

<!-- slide -->

## 获得更多帮助 👍

<!-- slide -->

### vim内置帮助文档

- vim帮助文档提供的说明一定是**最权威**的, 通常也是最**清晰简洁**的. 建议在看网上污七糟八的教程前先试着看看帮助文档. 这里列出一些大家可能想查看的内容

  💡 如果你不确定要查的内容有没有, 可以`h xxx`后按 <kbd>Ctrl</kbd> <kbd>D</kbd> 然后所有包含**xxx**的可查询内容都会被列出

  💡 如果你对自己的英文没有自信, 有中文版帮助文档可供安装

| 想查询的内容                | 查询方式                 |
| --------------------------- | ------------------------ |
| 帮助文档主文件              | `:h`                     |
| vim编辑模式间切换           | `:h mode-switching`      |
| 常用命令速览                | `:h quickref`            |
| 用户手册目录                | `:h usr_toc`             |
| vim帮助文档使用的记号的说明 | `:h notation`            |
| vimscript                   | `:h vimscript`           |
| 几个寄存器的详细说明           | `:h registers`           |
| 键映射                      | `:h map.txt`         |
| 特殊键盘按键的名称          | `:h keycodes`            |
| 块编辑                      | `:h blockwise-operators` |
| 鼠标设置                    | `:h mouse`               |
| vim内置终端                 | `:h terminal`            |

<!-- slide data-notes="(我觉得翻译得很一般)" -->

### vimtutor

- 在终端输入`vimtutor`进入vim自带的英语零基础者入门教程 (阅读时长大致25-30分钟)

  💡 可以加参数来打开其他语言版本vimtutor. 比如`vimtutor zh_cn`打开中文版vimtutor. 进入`$VIMRUNTIME/tutor`目录查看提供的语言版本.

### Cheat Sheet

- 你可以使用vim小抄插件[vim-cheat40](https://github.com/lifepillar/vim-cheat40)或者使用下面这样的图片形式小抄, 在你最开始使用vim, 还有许多命令记不清时帮你快速想起一些东西

给出几个我比较喜欢的图片形式小抄的链接:  
[🖼与操作效果对应的小抄](https://people.csail.mit.edu/vgod/vim/vim-cheat-sheet-en.png) [🖼与键盘对应的小抄](https://people.csail.mit.edu/vgod/vim/vim-cheat-sheet-en.png) [🖼很详细的小抄](https://cdn.shopify.com/s/files/1/0165/4168/files/preview.png)

![](vim/vim-cheat-sheet-en.png)

<!-- slide -->

### 推荐的vim教程

[一份渐进式的新手友好的教程](https://coolshell.cn/articles/5426.html)
[十分全切且言简意赅的教程](https://github.com/wsdjeg/vim-galore-zh_cn)
[vim常用操作列表](https://github.com/ruanyf/articles/blob/master/dev/vim/operation.md)
[一份列举了许多vim用户使用vim原因的文章](http://www.viemu.com/a-why-vi-vim.html)
[比较合理的vim键映射设置参考](http://blog.guorongfei.com/2015/09/03/vim-shortcut/)
[Xterm256色颜色列表](https://jonasjacek.github.io/colors/)

<!-- slide -->

### 我使用vim至今一年多点, 因为编程水平有限所以暂时没有更加深入的需求, 而因为使用时间还不够长因此也没有了解更多可能很便捷的功能. 很明显我的分享出于一个不上不下的水平, 仅希望这能帮到想了解vim的人以及vim初入门者. 我会慢慢继续探索的! 希望我以后能有机会做更进一步的分享, 也祝愿大家vim用得越来越丝滑.

### 诸君共勉 💪

<!-- slide -->

## 为了感谢你看到最后这里有两个彩蛋! 🎊

<!-- slide -->

## 在vim里输入`:smile`会有惊喜😏

<!-- slide -->

## 点击观看视频 👀

[![](vim/bilibili.png)](https://www.bilibili.com/video/BV1LQ4y1T7Zb)

<!-- slide -->

# 完

## 感谢您的观看 🤗