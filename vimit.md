## 普通模式

| 命令        | 用途                                         |
| ----------- | -------------------------------------------- |
| `b`         | 把光标**移动**到单词的开头                   |
| `d{motion}` | **删除** - [motion](#MOTION)                 |
| `dd`        | 删除整行                                     |
| `D`         | **删除**到行尾                               |
| `{visual}D` | **删除**选中的行                             |
| `e`         | **移动**到当前/下一个单词**结尾**            |
| `f{char}`   | 正向**移动**到下一个                         |
| `F{char}`   | 反向**移动**到下一个                         |
| `g`         | [g](#G)                                      |
| `H`         | **移动**到当前窗口左上角                     |
| `J`         | **J**oin two lines                           |
| `L`         | **移动**到当前窗口右上角                     |
| `p`         | 在后面**放**                                 |
| `P`         | 在前面**放**                                 |
| `r`         | 替换 **r**eplace 一个字符                    |
| `R`         | 替换 **r**eplace 模式                        |
| `t{char}`   | 正向**移动**到下一个的前一个字符上           |
| `T{char}`   | 反向**移动**到上一个的后一个字符上           |
| `u`         | **撤销**                                     |
| `v`         | 进入[**可视**模式](#V)                       |
| `V`         | 选中当前行（start **Visual** mode linewise） |
| `w`         | **移动**到下一个单词的开头                   |
| `x`         | **删除**光标下的字符                         |
| `X`         | **删除**光标前面的字符                       |
| `y`         | 复制 **y**ank                                |
| `yy`        | 复制 **y**ank 整行                           |
| `Y`         | 复制 **y**ank 整行（=== `yy`）               |
| `z`         | [**滚动**屏幕](#Z)                           |

## XXX 并进入插入模式

| 命令        | 用途                                             |
| ----------- | ------------------------------------------------ |
| `a`         | 在当前光标之后添加 **a**ppend（进入插入模式）    |
| `A`         | 在当前行的结尾添加 **a**ppend（进入插入模式）    |
| `c{motion}` | 修改 **c**hange - [motion](#MOTION)              |
| `cc`        | 删除整行并进入插入模式                           |
| `C`         | 从光标处**删除到行尾**并进入插入模式             |
| `i`         | 进入插入模式                                     |
| `I`         | 行の始まり(文字の開始位置)からインサートモードへ |
| `o`         | 在下面**插入新行**并进入插入模式                 |
| `O`         | 在上面**插入新行**并进入插入模式                 |
| `s`         | **删除**光标下的字符并进入插入模式               |
| `S`         | **清空当前行**并进入插入模式                     |

## MOTION

| 命令   | 用途                               |
| ------ | ---------------------------------- |
| `cl`   | 修改一个字符（等同于 `s` or `c→`） |
| `d5j`  | 删除 5 行                          |
| `dh`   | 删除前一个字符（`d←`）             |
| `dl`   | 删除一个字符（等同于 `x` or `d→`） |
| ------ | ------------------------           |
| `daw`  | delete a word                      |
| `d2w`  | delete 2 word                      |
| `db`   | 删除光标起始到单词开头             |
| `ndd`  | n 行削除                           |
| `dw`   | カーソル上の一語を削除             |
| `d$`   | カーソル位置から行の最後までを削除 |

> [`daw` vs `diw`](https://stackoverflow.com/questions/7267375/what-does-vaw-mean-in-vim-in-normal-mode-and-also-caw-and-daw)

## G

| 命令         | 用途                          |
| ------------ | ----------------------------- |
| `ga`         | 显示字符的编码                |
| `ge`         | 上一个单词的结尾              |
| ---------    | -------------------------     |
| `g~{motion}` | Switch case of {motion} text. |
| `gu{motion}` | 转换为小写                    |
| `gU{motion}` | 转换为大写                    |
| ---------    | -------------------------     |
| `gj/gk`      | 按屏幕行向下/上               |

> `~` - 切换光标下字符大小写

## V

| 命令  | 用途                                                        |
| ----- | ----------------------------------------------------------- |
| `vi}` | 选中当前 `}` 内（**i**nner / **i**nside）的所有内容         |
| `va}` | 选中包括 `}` 在内的括起来的所有（**a**ll / **a**round）内容 |

> `}` 也可以是 `` ` `` `'` 等等

## Z

| 命令 | 用途                                                 |
| ---- | ---------------------------------------------------- |
| `z.` | Center the screen on the cursor                      |
| `zt` | Scroll the screen so the cursor is at the **T**op    |
| `zb` | Scroll the screen so the cursor is at the **B**ottom |

## 缩进

| 命令 | 用途     |
| ---- | -------- |
| `>`  | 增加缩进 |
| `<`  | 减少缩进 |
| `=`  | 自动缩进 |

## 在插入模式 INSERT 中

| 命令                           | 用途                                          |
| ------------------------------ | --------------------------------------------- |
| `<⌃h>`                         | 删除前一个字符（=== `⌫` ）                    |
| `<⌃w>`                         | 删除前一个单词                                |
| `<⌃u>`                         | 删除到行首                                    |
| `<⌃r>`                         | 使用寄存器中的内容                            |
| `<⌃v>{123}`<br />`<⌃v>u{1234}` | 以十进制 / 十六进制编码输入字符               |
| `<^k>{a}{e}`                   | 插入二合字母（例如 `ae` -> `æ`、`?I` -> `¿`） |

## 返回普通模式

- `⎋ esc`

- `<⌃[>`

- `<⌃o>`（插入-普通模式）

> 什么是插入-普通模式？在插入模式使用此命令，可以执行一次普通模式命令，然后返回插入模式

## 移动光标

| 命令             | 用途                               |
| ---------------- | ---------------------------------- |
| `hjkl`           | 左下上右                           |
| `0`              | 行首                               |
| `$`              | 行尾                               |
| `^`<br />`<⇧ 6>` | 第一个非空白字符                   |
| `g<hjkl0$^>`     | 按屏幕行移动                       |
| `%`              | 移动到和当前光标下的括号配对的括号 |
| `nG`             | 跳到第 n 行的行首                  |
| -------------    | ----------------------------       |
| `b`              | **移动**到当前/上一个单词的开头    |
| `w`              | **移动**到下一个单词的开头         |
| `e`              | **移动**到当前/下一个单词**结尾**  |
| `ge`             | **移动**到上一个单词**结尾**       |

### 标记和返回

`m{a-zA-Z}` 标记当前光标所在位置。

`'{mark}` 调到标记位置所在行。

`` `{mark} `` 跳到标记位置所在行 and 列。

#### 自动标记

| 命令     | 跳转到                         |
| -------- | ------------------------------ |
| ` ` ``   | 当前文件上次跳转动作之前的位置 |
| `` `. `` | 上次修改的地方                 |
| `` `^ `` | 上次插入的地方                 |
| `` `[ `` | 上次修改或复制的起始位置       |
| `` `] `` | 上次修改或复制的结束位置       |
| `` `< `` | 上次高亮选区的起始位置         |
| `` `> `` | 上次高亮选区的结束位置         |

### 在匹配的括号之间跳转

`%` 在匹配的括号之间跳转。

## 查找

| 命令        | 用途                               |
| ----------- | ---------------------------------- |
| `/{chars}⏎` | 查找                               |
| `f{char}`   | 正向**移动**到下一个               |
| `F{char}`   | 反向**移动**到下一个               |
| `t{char}`   | 正向**移动**到下一个的前一个字符上 |
| `T{char}`   | 反向**移动**到上一个的后一个字符上 |

> 在 `t` `T` `f` `F` 的结果中，用 `;` 可以继续移动，用 `,` 跳回来。

## 寄存器

| 命令  | 用途                 |
| ----- | -------------------- |
| `xp`  | 调换光标下的两个字符 |
| `ddp` | 调换光标下的两行     |

指明操作所需的寄存器：`"{reg}`，例如 `"ayiw`、`"bdd`，等。

| 寄存器 | 内容                   |
| ------ | ---------------------- |
| `""`   | 无名剪贴板             |
| `"0`   | `y{motion}` 复制的     |
| `"+`   | 系统剪贴板（双向访问） |
| `"%`   | 当前文件名             |
| `"#`   | 轮换文件名             |
| `".`   | 上次插入的文本         |
| `":`   | 上次执行的命令         |
| `"/`   | 上次查找的模式         |

- `v{motion}` 在 `p` 可以防止无名寄存器中本来要 put 的内容被覆盖。

- 在插入模式中使用 `<ctrl>r{reg}` 来访问寄存器。

## Recipes

### Replace text with yanked text

```bash
yiw # yank text
# move to the text you want to replace
viwp # select replaced text and put yanked text
```

### find yanked text

```bash
yiw # yank text
/<⌃ r>0⏎ # find text in register (default 0) (which we yanked)
```
