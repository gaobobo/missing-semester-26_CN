# Shell

> 主讲：Jon

---

## 什么是Shell？

如今，计算机有着各种各样的界面来执行命令：华丽的用户界面、语音界面、AR/VR（增强现实/虚拟现实），以及最近出现的LLM（大语言模型）。
这些界面适用于80%的使用场景，但是它们允许你做的事往往存在根本限制——你不能按下某个不存在的按钮，或对尚未编程东西发出语音指令。
为了充分利用计算机所提供的工具，我们必须回到“老掉牙”的文本界面：Shell。

几乎所有你能接触到的平台都有某种形式的Shell，而且很多都提供不同的Shell供你选择。
尽管在细节上有所不同，但它们的核心功能都大致相同：允许你运行程序、为程序提供输入，并以半结构化的方式检查程序输出。

要打开Shell*提示符（Prompt）*（输入命令的地方），你需要一个*终端（Terminal）*，它是与Shell交互的可视化界面。
你的设备可能已经预装了一个，或可以比较容易地安装一个：

- Linux：按下`Ctrl + Alt + T`（适用于绝大多数发行版）。
  或在你的应用程序菜单中搜索“终端（Terminal）”。
- Windows：按下`Win + R`，输入`cmd`或`powershell`，然后按`Enter`。
  或者，在开始菜单中搜索“终端（Terminal）”或“命令提示符（Command Prompt）”。
- macOS：按下`Cmd + 空格`，打开“聚焦搜索（Spotlight）”，输入“终端（Terminal）”，
  然后按`Enter`。或者，在访达的“应用程序（Applications） > 实用工具（Utilities） > 终端（Terminal）”

在Linux和macOS上，上述步骤通常会打开“Bourne Again SHell”，简称“bash”。
bash是广泛使用的Shell之一，其语法和你在其他的Shell见到过的类似。
在Windows上，你会看到“批处理”（Batch）或“PowerShell”，这些Shell是Windows特有的，尽管知识点是相同的，但这些都不是我们课程的重点。
对于Windows系统，你需要一个“[适用于Linux的Windows子系统](https://learn.microsoft.com/zh-cn/windows/wsl/)”（Windows Subsystem for Linux，WSL）或者Linux虚拟机。

还有其他的Shell，相较于bash，它们在人体工学方面有诸多改进。（fish和zsh是最为常见的）
虽然这些Shell非常流行（所有讲师都在使用其中的某一个），但它们远不如bash普及，而且有很多概念都和bash相同，因此我们不会重点介绍它们。

## 为什么要考虑使用Shell？

使用Shell不仅（通常）比“点个什么东西”要快得多，而且其表现力也是图形界面望尘莫及的。
正如我们所看到的一样，Shell给予你*融合*程序的能力，以创造性的方式去自动化几乎所有任务。

熟悉Shell从某种意义上也为你打开了开源软件的大门（开源软件通常在安装指南里面要求与Shell交互），同时在为你的软件项目构建持续集成（如[代码质量](/docs/90_代码质量.md)一讲所述），以及其他程序故障时调试都非常有用。

## 在Shell中导航

当你启动终端，你会看见一个“提示符”，通常长这样：

```console
missing:~$
```

这是Shell的主文本界面。
它告诉你，你正在`missing`的机器上工作。
随后就是“当前工作目录”，也就是你当前所处的目录，即`~`（“home”的缩写）。
`$`告诉你，你正在处于“非root用户”（稍后会进一步说明）。
当前提示符你可以输入“命令”（Command），其会被Shell解释。
最基本的命令是执行一个程序：

```console
missing:~$ date
Fri 10 Jan 2020 11:49:31 AM EST
missing:~$
```

在这里，我们执行了`date`这个程序，其（不出所料）打印出了当前的日期和时间。
然后，Shell会询问我们下一个要执行的命令。
我们也可以运行带“参数”（Argument）的命令：

```console
missing:~$ echo hello
hello
```

在这个例子中，我们告诉Shell执行`echo`这个程序，但传入参数`hello`。
`echo`命令仅仅会打印传入的参数。
Shell在解析时会以空格作为分隔符，并将第一个单词视为要运行的程序，而随后的内容会视为参数，并把单词一个个传递给该程序。
如果想要提供包含空格会其他特殊字符，（例如，一个名为`My Photos`的目录，）可以用引号`'`或`"`括起来（如`"My Photos"`），或者使用`\`进行转义（如`My\ Photos`）。

对于初学者来说，最重要的命令莫过于`man`，“manual”（手册）的缩写。
`man`和其他同类程序允许你查阅当前系统上的所有命令的更多信息。
例如，如果你运行`man date`，它会解释什么是`date`，以及你可以传递怎样参数来改变他的行为。
你也可以在大多数命令中传入`--help`参数，通常会获得简单的说明。

> [!TIP]
>
> 除了`man`之外，可以考虑下[`tldr`](https://tldr.sh/)，因为其可以在终端显示最常用的用法示例。大语言模型通常也能很好地解释命令如何工作，以及怎样调用它们来达成你想要的效果。

在了解什么是`man`之后，另一个需要学习的重要命令是`cd`，即“change directory”（改变目录）。
该命令实际上是Shell内置的，并非一个独立的程序（例如，`which cd`会显示“no cd found”）。
你只需要传递一个路径，然后当前工作目录就是这个路径了。
你也会在Shell提示符中看到工作目录的提示：

```console
missing:~$ cd /bin
missing:/bin$ cd /
missing:/$ cd ~
missing:~$
```

> [!TIP]
>
> Shell自带自动补全功能，所以按`<Tab>`可以更快地输入路径！

除非另行指定，否则许多命令都是基于当前工作目录进行操作。
如果你不确定当前的目录，可以运行`pwd`或打印`$PWD`环境变量（使用`echo $PWD`），两种方法都可以获得当前工作目录。

当前工作目录还有另一个好处：其允许我们使用*相对路径*（Relative Path）。
到目前为止，所有我们见过的路径都是“绝对路径”（Absolute）——它们以`/`开头，然后紧随从根目录（`/`）到某个位置所经过的所有的目录。
在相对路径中（所有*不*以`/`开头的目录），路径的第一部分是在当前工作目录查找，然后再按剩余的目录继续遍历查找。
例如：

```console
missing:~$ cd /
missing:/$ cd bin
missing:/bin$
```

每个目录都有两个“特别”的部分：`.`和`..`。
`.`是“当前目录”，而`..`是“父目录”。
因此：

```console
missing:~$ cd /
missing:/$ cd bin/../bin/../bin/././../bin/..
missing:/$
```

通常情况下，你可以再任何命令的参数中使用绝对路径和相对路径，但使用相对路径时，记得注意下当前工作目录是什么。

> [!TIP]
>
> 考虑安装并使用[`zoxide`](https://github.com/ajeetdsouza/zoxide)来简化`cd`的使用——`z`将记住你最常访问的路径，让你用最少的字符来访问这些路径。

## Shell中到底有哪些可用命令？

问题来了，Shell是如何找到像`date`或`echo`这类程序呢？
当Shell被要求执行一个命令时，它会查询一个名为`$PATH`的“环境变量”（Environment Variable），该变量列出了Shell在哪个目录中查找指定的程序：

```console
missing:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
missing:~$ which echo
/bin/echo
missing:~$ /bin/echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

当我们运行`echo`命令时，Shell会先知道它应该执行`echo`程序，然后在`$PATH`的以`:`分隔的目录中寻找。找到后，
我们不妨尝试列出`$PATH`上所有的目录内容，可以将指定目录路径传递给`ls`来实现，然后就会列出文件：

```console
missing:~$ ls /bin
```

> [!TIP]
>
> 考虑下[`eza`](https://eza.rocks/)，其能提供更人性化的`ls`输出。

通常，绝大多数电脑上会打印出*很多*程序，但我们先关注几个比较重要的程序。
首先，一些简单的程序有：

- `cat file`：打印`file`中的内容；
- `sort file`：按一定顺序打印`file`中的行；
- `uniq file`：删除`file`中连续且重复的行；
- `head file`、`tail file`：打印`file`中的头几行和后几行。

> [!TIP]
>
> 考虑安装并使用[`bat`](https://github.com/sharkdp/bat)代替`cat`，前者能提供语法高亮与文本滚动。

还有一个`grep pattern file`命令，它可以在`file`中寻找符合`pattern`的行。
这个工具值得我们展开讲讲，因为它真的*非常*有用，它能干的事情可能超出你的预期。
`pattern`实际上是一个*正则表达式*（Regular Expression），这种东西能够表达非常复杂的匹配模式——
我们将在[“代码质量”一节](/course/90_代码质量.md)说说它的更多内容。
当然，除了指定文件，也可以指定一个目录（或者用`.`留空），并传递`-r`来在目录中递归搜索。

> [!TIP]
>
> 考虑安装并使用[`ripgrep`](https://github.com/BurntSushi/ripgrep)而不是`grep`，前者可以获得更快、更友好的（但可移植性较差）的替代方案。`ripgrep`甚至默认就使用递归来搜索当前工作目录。

还有一些接口略显复杂但却非常有用的工具。
其中一个工具就是`sed`，它是一个程序化文件编辑器，甚至有着自己的编程语言，用于自动化文档的编辑。
但它最常见的用法是：

```console
missing:~$ sed -i 's/pattern/replacement/g' file
```

这会替换所有`pattern`为`replacement`的实例。
而`-i`表示我们希望就地更改（而不是不保存`file`的修改并打印替换后的内容）。
`s/`在sed编程语言中表示我们想要进行替换操作。
`/`是查找模式与替换内容的分隔符。
尾的`/g`代表我们希望逐行替换*所有*符合条件的实例，而不是只替换第一个。
与`grep`类似，这里的`pattern`也是一个正则表达式，提供强大的表达能力。
正则表达式还可以让`replacement`引用匹配到的内容，我们稍后会用一个案例讲讲。

接下来是`find`，它可以（递归地）查找符合条件的文件。
比如：

```console
missing:~$ find ~/Downloads -type f -name "*.zip" -mtime +30
```

这会查找下载目录中超过30天的ZIP文件。

```console
missing:~$ find ~ -type f -size +100M -exec ls -lh {} \;
```

再比如，这可以查找并列出`home`目录中大于100M的文件。
注意，`-exec`需要一个以`;`结尾的独立命令（就像我们需要转义空格一样），而其中的`{}`会被`find`替换为每个匹配到的文件路径。

```console
missing:~$ find . -name "*.py" -exec grep -l "TODO" {} \;
```

这个例子则是查找所有包含TODO项的`.py`文件。

`find`的语法可能有点让人头皮发麻，不过还是希望你能感受到它的强大之处！

> [!TIP]
>
> 考虑安装并使用[`fd`](https://github.com/sharkdp/fd)，其能够比`find`提供更加人性化（但可移植性较差）的体验。

接下来要介绍的是`awk`，它和`sed`一样，有着自己的编程语言。
`sed`专为编辑文件而构建，而`awk`专注解析文件。
截至目前，`awk`最常见的用途就是处理具有规律性语法的文件（比如CSV文件），这样你就可以得到每条记录（行）中的特定部分：

```console
missing:~$ awk '{print $2}' file
```

在这个例子中，`file`以空格作为分隔符，并打印第二列内容。
如果加上`-F`，他会以逗号作为分隔符，打印第二列的内容。
`awk`能干的事情远不止这些——过滤行、聚合计算等——练习题里面有更多内容。

将上面的工具组合起来，就能实现一些非常花哨的功能，比如：

```console
missing:~$ ssh myserver 'journalctl -u sshd -b-1 | grep "Disconnected from"' \
  | sed -E 's/.*Disconnected from .* user (.*) [^ ]+ port.*/\1/' \
  | sort | uniq -c \
  | sort -nk1,1 | tail -n10 \
  | awk '{print $2}' | paste -sd,
postgres,mysql,oracle,dell,ubuntu,inspur,test,admin,user,root
```

这个命令会从远程服务器获取SSH日志（我们会在[下节](/course/20_命令行环境.md)中讨论`ssh`），搜索断开链接的消息，并提取出每条消息中的用户名，然后以逗号作为分隔符打印前10个用户名。
而如此复杂的问题只需要一条命令即可解决！
我们将详细讲讲其中的每一步。

## Shell语言（bash）

前面的例子介绍了一个新概念：管道（`|`）。
管道允许你将某个程序的输入与另一个程序的输入连接起来。
之所以可能，是因为如果没有给`file`传递参数，大多数命令行程序都会将操作映射到“标准输入”（通常是键盘打字的地方）。
`|`将它之前的程序的“标准输出”（通常是打印到你终端中的内容）作为“标准输入”传递给`|`后面的程序。
这允许你*组合*不同的Shell程序，也让Shell成为了一个极其高效的工作环境。

事实上，多数Shell实现了一个完整的编程语言（如bash），就像Python和Ruby一样。
它有着变量、条件语句、循环和函数。
当你在Shell中运行命令时，实际上就是让Shell解释并执行一小段代码。
当然，我们不可能教会你bash的方方面面，但会教给你一些特别有用的东西：

首先是重定向`>file`，它可以让你将某个程序的标准输出写入到`file`中，而不是在终端显示。
这允许你很方便地进行事后分析。
`>>file`会将内容尾随到`file`中，而不是完全覆盖它。
还有`<file`，代表让Shell从`file`读取并作为某个程序的标准输入，而不是从键盘读取。

> [!TIP]
>
> 是时候提一下`tee`了。`tee`会将标准输入打印到标准输出（就像`cat`！），但是*也会*写入文件。
> 所以`verbose cmd | tee verbose.log | grep CRITICAL`会将完整的verbose日志写入到文件，并且不会搞乱你的终端！

接下来是条件语句`if command1; then command2; command3; fi`，它可以在`command1`没有产生错误时，执行`command2`和`command3`。
如果你需要，还可以有一个`else`分支。
最常用作`command1`的命令是`test`，通常使用它的缩写`[`。
`test`命令允许你评估条件，比如“文件是否存在”（`test -f file`或`[ -f file ]`），或“字符串是否相等”（`[ "$var" = "string" ]`）。
在bash中，还内置了一个“更安全”的`test`命令`[[ ]]`，旨在减少引号方面的行为异常。

bash还有两种循环，分别是`while`和`for`。
`while command1; do command2; command3; done`函数与`if`命令类似：只要`command1`不出错，那么它就会不停地执行整个过程。
`for varname in a b c d; do command; done`会执行`command`四次，每次都会将`$varname`分别赋予值`a`、`b`、`c`和`d`。
与其显式地列出项目，你或许会更加常用“命令替换”，比如：

```console
for i in $(seq 1 10); do
```

这会执行`seq 1 10`（该命令会打印从1到10的数字），然后替换掉整个`$()`，并将其替换为该命令的输出，从而实现迭代10次的for循环。
在一些老代码中，你会看见反引号（如`for i in `seq 1 10`; do`），而不是`$()`。
但或许你会更加喜欢`$()`，因为`$()`还可以嵌套。

虽然*可以*直接在提示符中直接写一个很长的Shell脚本，但或许你会更愿意把他们写进`.sh`中。
例如，这里有一个脚本，它会在程序失败之前一直循环运行，直到最后打印失败时的输出，同时在后台为CPU持续施压（例如，用于复现不稳定测试（Flaky Test））。

```shell
#!/bin/bash
set -euo pipefail

# 在后台开始CPU压力测试
stress --cpu 8 &
STRESS_PID=$!

# 设置日志文件
LOGFILE="test_runs_$(date +%s).log"
echo "Logging to $LOGFILE"

# 运行测试，直到失败
RUN=1
while cargo test my_test > "$LOGFILE" 2>&1; do
    echo "Run $RUN passed"
    ((RUN++))
done

# 清理并汇报结果
kill $STRESS_PID
echo "Test failed on run $RUN"
echo "Last 20 lines of output:"
tail -n 20 "$LOGFILE"
echo "Full log: $LOGFILE"
```

这里面包含了一些没有提到过的东西，我建议你花点时间研究一下，这些Shell调用的东西都非常有用。
比如，后台任务（`$`）、复杂的[Shell重定向](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)、[算数扩展](https://www.gnu.org/software/bash/manual/html_node/Arithmetic-Expansion.html)。

开头的那两行值得注意下。
第一行是“Shebang”，你也会在其他的文件顶部看到。
当文件以魔法命令`#!/path`开头是，Shell会从`/path`启动程序，并将文件内容作为输入传递。
对于Shell脚本来说，上面的例子代表将Shell脚本的内容传递给`/bin/bash`。
当然，你也可以用`/usr/bin/python`的Shebang来编写Python脚本！

第二行是让bash“更严格”的方法之一，可以减少编写Shell脚本的许多潜在风险。
`set`可以接受很多参数。
简而言之，`-e`可以在命令发生任何错误时提前退出；
`-u`代表当使用未定义的变量时崩溃，而非使用默认值空字符串；
`-o pipefail`可以让在`|`中的一系列程序失败时，整个Shell脚本也会提前退出。

> [!NOTE]
> Shell编程是一个深奥的主题，这和其他编程语言类似。
> 不过，有一点需要我们注意：bash有许多不寻常的陷阱。
> 有几个网站列出了这些陷阱：
>
> - [tldp.org](https://tldp.org/LDP/abs/html/gotchas.html)
> - [wooledge.org](https://mywiki.wooledge.org/BashPitfalls)
>
> 我强烈建议编写时多多使用[ShellCheck](https://www.shellcheck.net/)。
> 当然，LLM在编写和调试Shell脚本等方面也很出色，并且如果bash过于复杂时（超过100行），LLM可以将其翻译成“真正意义上的”编程语言（如Python）。

## 下一步

此时你已经足够熟悉Shell，也能独立完成一些基本任务了。
你现在应该可以找到你感兴趣的文件，并使用多数程序的基本功能。
在下一讲中，我们将进一步讨论如何使用Shell和其他命令行工具来自动化更复杂的任务。

## 练习

所有课程都配套一系列的练习。
有些练习会给你一个具体的任务，但有些问题是开放式的，比如“尝试使用X和Y程序”。
无论如何，我们都非常鼓励你去试一下。

我们还没有发布这些练习的参考答案。
如果你在某个问题卡住了，欢迎在[Discord](https://ossu.dev/#community)的`#missing-semester-forum`询问！
或者直接给我们发邮件，说说你已经尝试过的方法，我们会尽力帮忙。
也可以试试将这些练习喂给LLM，这样你就可以与LLM互动，更深入地探讨问题。
这些练习真正的价值在于挖掘答案的过程，而非答案本身。
我们鼓励你在完成练习之余多去想想“为什么”，而非寻找某个问题的最佳答案。

> [!TIP]
>
> 译者注：
>
> 译者在仓库提供了题目的个人作答结果，请参阅：
>
> [/answers/10_Shell概论/README.md](/answers/10_Shell概论/README.md)

1. 对于这门课程，你需要使用Unix Shell，比如Bash或ZSH。
   如果是Linux或MacOS，通常不需要额外安装或额外的准备。
   如果是Windows，你需要确保没有运行`cmd.exe`或PoerShell。
   你可以使用“适用于Linux的Windows子系统”（Windows Subsystem for Linux，WSL），或弄一个Linux虚拟机来使用Unix风格的命令行工具。
   为了确保你正在用的Shell是正确的，你可以尝试运行命令`echo $SHELL`。
   如果显示类似`/bin/bash`或`/usr/bin/zsh`等内容，那么该Shell就是我们想要的。
2. `ls`的`-l`标志是做什么的？试试`ls -l /`并观察输出。
   每行的前10个字符代表什么意思？（提示：`man ls`）
3. 在命令`find ~/Downloads -type f -name "*.zip" -mtime +30`，`*.zip`是一个“glob”。
   什么是“glob”？创建包含一些文件的测试目录，试试`ls *.txt`、`ls file?.txt`和`ls {a,b,c}.txt`等模式。
   参考Bash手册的“[模式匹配](https://www.gnu.org/software/bash/manual/html_node/Pattern-Matching.html)”一节。
4. `'single quotes'`、`"double quotes"`和`$'ANSI quotes'`之间有什么区别？
   写一个命令，输出一个包含`$`、`!`和换行符的字符串。参见“[引号](https://www.gnu.org/software/bash/manual/html_node/Quoting.html)”一节。
5. Shell有三个标准流：stdin(0)、stdout(1)、stderr(2)。
   运行`ls /nonexistent /tmp`并将stdout重定向到一个文件。
   如何将两者重定向到同一个文件？
   参见“[重定向](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)”一节。
6. `$?`用于捕获最后一个命令的退出状态（0=成功）。
   `&&`只有先前的命令成功后才运行下一个命令，`||`只有先前的命令失败才运行。
   写一个单行命令，只有在`/tmp/mydir`不存在时才创建它。
   参见“[退出状态](https://www.gnu.org/software/bash/manual/html_node/Exit-Status.html)”一节。
7. 为什么`cd`命令必须内置于Shell本身，而非作为一个独立的程序。
   （提示：想想子进程可以或不可以影响父进程的什么。）
8. 编写一个脚本，将文件名作为参数（`$1`），并使用`test -f`或`[ -f ... ]`检查文件是否存在。
   根据文件是否存在，打印不同的消息。
   参见“[Bash条件表达式](https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html)”一节。
9. 将上一个练习的脚本保存为文件（例如`check.sh`），尝试使用`./check.sh somefile`运行它，看看会发生什么？
   现在，运行`chmod +x check.sh`并再试一次。
   为什么需要这一步？
   （提示：通过`ls -l check.sh`看看运行`chmod`前后的差异）
10. 如果在你的脚本中添加`-x`标志到`set`会发生什么？
    尝试用一个简单的脚本测试并观察输出。
    参见“[内置命令Set](https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin.html)”一节。
11. 编写一个命令，将文件复制并备份，并将备份的文件名以今天的日期结尾（如`notes.txt`->`notes_2026-01-12.txt`）。
    （提示：`$(date +%Y-%m-%d)`）
    参见“[命令替换](https://www.gnu.org/software/bash/manual/html_node/Command-Substitution.html)”一节。
12. 修改讲座中的“不稳定测试”脚本，使其将测试命令作为参数传入，而非将测试命令`cargo test my_test`硬编码。
    （提示：`$1`或`$@`）
    参见“[特殊参数](https://www.gnu.org/software/bash/manual/html_node/Special-Parameters.html)”一节。
13. 使用管道查找你主目录中5种常见的文件扩展名。
    （提示：结合`find`、`grep`或`sed`或`awk`、`sort`、`uniq -c`和`head`）
14. `xargs`将标准输入的行转换为命令的参数。
    使用`find`和`xargs`（不要使用`find -exec`）来查找目录中所有的`.sh`文件，并使用`wc -l`统计每个文件中的行数。**附加题：使其可以处理带有空格的文件名。**
    （提示：使用`-print0`和`-0`）
    参见`man xargs`。
15. 使用`curl`获取课程网站（`https://missing.csail.mit.edu/`）的HTML，并将其通过管道传输给`grep`来统计并列出讲座的数量。
    （提示：寻找一个可以“查找每个讲座只出现一次”的模式，使用`curl -s`来抑制进度输出）
16. `jq`是处理JSON数据的强大工具。
    使用`curl`从`https://microsoftedge.github.io/Demos/json-dummy-data/64KB.json`获取示例数据，并使用`jq`提取版本号大于6的人名。
    （提示：先通过管道传递给`jq .`以查看结构，然后尝试`jq '.[] | select(...) | .name'`）
17. `awk`可以根据列值过滤行并操作输出。
    例如，`awk '$3 ~ /pattern/ {$4=""; print}'`仅打印第三列匹配`pattern`的行，同时省略第四列。
    编写一个`awk`命令，仅打印第二列大于100的行，并交换第一列和第三列。
    使用`printf 'a 50 x\nb 150 y\nc 200 z\n'`进行测试。
18. 分析讲座中的SSH日志管道：每个步骤的作用是什么？
    然后构建一个类似的功能，从`~/.bash_history`（或`~/.zsh_history`）中找出你最常用的Shell命令。
