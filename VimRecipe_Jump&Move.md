Vim 进阶 - 移动和跳转

相信你已经知道了 `hjkl` 的含义，如果不知道的话，[看这里](VimRecipe_0.md)。

## `hjkl` 也可以更快！

在这里我（不带任何倾向性地）假设你使用的是 MacBook，打开 `系统偏好设置 > 键盘`，把「按键重复」和「重复前延迟」都调整到最快。

「按键重复」决定了当你长按某一个按键的时候系统会以多快的速度重复输入这个按键，「重复前延迟」决定了当你开始长按多久过后系统会开始重复输入。把这两个选项都调到最快，可以让光标的移动更快。

但是，仅靠长按这四个按键来移动，是非常初级、低效、应该被避免的操作。如果你已经决定用 Vim 来进行文本编辑却还用这种方式移动光标，人民群众会仇恨你，你的朋友和家人也会嘲笑你，唾弃你<sup>[^](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)</sup>。

## 什么是屏幕行

如果你使用的是现代 ide 的 Vim 模式，那么在屏幕左侧应该已经有行号标识了。如果你是在终端当中使用 Vim，你可能需要 `:set number` 命令打开行号显示。

[![rGNpGt.png](https://s3.ax1x.com/2020/12/17/rGNpGt.png)](https://imgchr.com/i/rGNpGt)

如图所示，光标现在在第 3 行开头 `_N_isi` 位置，此时我们按下 `j`，光标移动到了第四行，而不是 `Nisi` 下面的 `qui`。这是因为 `jk` 是按照实际行，也就是文本在文档中真实的行，进行移动的。而当一行文本的长度超过的窗口的宽度，Vim 会把这一行折行显示，文件中的一行可能会显示成屏幕上的若干行。

在 Vim 中想要按屏幕行上下移动（本例中从 `_N_isi` 移动到 `qui`），可以用 `gj` 和 `gk` 命令。

移动到行首和行尾的 `0` 和 `$` 命令同样也有屏幕行和实际行之分，按屏幕行的首尾移动，可以使用 `g0`、`g$`。

## 基于单词的移动

| 命令 | 移动位置                                    |
| ---- | ------------------------------------------- |
| `w`  | 到下一个单词的开头 - for**w**ard / **w**ord |
| `b`  | 到当前单词、上一个单词的开头 - **b**ackward |
| `e`  | 到当前单词、下一个单词的结尾                |
| `ge` | 到上一个单词的结尾                          |

> `ea` 连在一起可以实现「移动到当前单词结尾并在后面插入」，记住它，使用频率很高。

## 查找字符

`f{char}`、`F{char}`、`t{char}`、`T{char}` 这四个命令是 Vim 中进行查找/移动最快的方式，可以分别记忆为 **f**ind、**t**ill。

其中，`f{char}` 代表移动光标到当前行的下一个 `{char}`，而 `t` 代表移动光标到当前行的下一个 `{char}` 的前面一个字符。与这两个命令对应的大写，`F{char}`、`T{char}`，则分别代表向前查找。

例如，`fo` 代表将光标移动到当前行的下一个 `o`。

想要查找再下一个、第二个第三个 `o`，并不需要再按一次 `fo`，Vim 为我们提供了重复这步操作的命令：`;` 表示向下继续寻找，`,` 表示向上继续寻找。

而这几个命令的用处不仅仅在于移动光标，配合 `d` delete、`c` change、`v` visual、`y` yank 也非常好用。

例如，`dtn` 可以理解为「从当前光标删除到下一个 `n` 之前」，可以简单记忆为「delete **t**ill n」。`ctm` 可以理解为 「从当前光标删除到下一个 `n` 之前并进入插入模式」，亦即「change **t**ill m」。`vfa`，「从当前光标位置选中到下一个 a」，`yfa`，「从当前光标位置复制到下一个 a」。

实践上，在和 `d`、`c` 一起使用时，倾向于用 `tT`，而在其他移动或者和 `v`、`y` 一起使用时，倾向于用 `fF`。

但是，`fFtF` 也有局限性：只能寻找一个字符，且只能在当前行寻找。

| 命令       | 移动位置                                 |
| ---------- | ---------------------------------------- |
| `fF{char}` | 移动到上/下一个 `{char}`                 |
| `tT{char}` | 移动到上/下一个 `{char}` 的前/后一个字符 |
| `,` `;`    | 向前/后移动                              |

## 跨行文本查找

在 Vim 中可以用 `/{char}⏎` 来进行多字符、跨行的查找，类似于在 ide 中按下 cmd + f 之后输入 `{char}` 并按回车的效果。

与之匹配的前一个/后一个的命令是 `N/n`（**n**ext），大写向前，小写向后。

## 标记

有的时候，我们可能要在两个位置间来回跳转。这个时候，最方便的办法就是使用「标记」。

`m{a-zA-Z}` 会用紧跟着输入的字母标记当前光标所在位置，例如 `ma` 把当前位置标记为 `a`。标记好之后，当我们移动到另外一个地方的时候，只要两个键就能跳转回来。

跳转回来有两种方式，以刚刚提到的标记 `a` 为例，`'a` 会跳转到标记的所在行的第一个非空白字符，而 `` `a `` 不仅会跳转到标记所在行，还会定位到标记所在的确切位置，也就是标记所在的列。

大多数时候，只要反复使用 `mm` 和 `` `m `` 就可以方便地来回跳转了。

Vim 还提供了一些默认的标识供我们跳转，见下表：

| 命令     | 跳转到                         |
| -------- | ------------------------------ |
| ` `` `   | 当前文件上次跳转动作之前的位置 |
| `` `. `` | 上次修改的地方                 |
| `` `^ `` | 上次插入的地方                 |
| `` `[ `` | 上次修改或复制的起始位置       |
| `` `] `` | 上次修改或复制的结束位置       |
| `` `< `` | 上次高亮选区的起始位置         |
| `` `> `` | 上次高亮选区的结束位置         |

## 括号内的跳转和选中

代码中经常有圆括号、尖括号、方括号、引号、html 标签等内容，Vim 也有一系列命令可以对和括号等内容相关的文本进行操作，在 Vim 中，我们把这些命令操作的内容称作「文本对象」。

文本对象由两个字符组成，第一个字符永远是 `i` 或 `a`。可以把 `i` 想象成 **i**nner 或者 **i**nside，而把 `a` 想象成 **a**round。下面，用一些例子来讲解文本对象的具体用法。

| 命令  | 选中范围                             |
| ----- | ------------------------------------ |
| `vi]` | 选中方括号包围的内部                 |
| `va]` | 选中方括号包围的内容，**包括**方括号 |
| `vi"` | 选中双引号包围的内部                 |
| `va"` | 选中双引号包围的内容，**包括**双引号 |
| `vat` | 选中一对 html 标签                   |
| `vit` | 选中 html 标签内部                   |

[![rG0jZ8.jpg](https://s3.ax1x.com/2020/12/17/rG0jZ8.jpg)](https://imgchr.com/i/rG0jZ8)

> `vi"` vs `va"`

同样，文本对象也可以搭配 `d` delete、`c` change、`y` yank 命令进行操作，例如：`da"` - 删除一对双引号及之间的内容（delete **a**round "），`cit` - 修改一对 html 标签之内的内容。

`i`、`a` 还可以搭配上面提到的 `w` 使用，例如：`diw` 删除当前单词，`diw` 删除当前单词及后面的空格，搭配 `c`、`v`、`y` 也类似。

## 括号间的跳转

`%` 命令让我们可以在匹配的括号间来回跳转。这个命令无需我们手动指明要跳转的括号，而是自动根据当前光标所在位置的上一层括号来进行跳转。
