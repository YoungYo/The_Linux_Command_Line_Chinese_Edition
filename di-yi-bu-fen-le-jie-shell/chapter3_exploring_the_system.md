# 第 3 章 探索 Linux 系统

既然我们已经知道了如何在文件系统中移动，那么是时候开始我们在 Linux 系统中的旅程了，但是在出发前，我们需要再多学习几个沿途能用得上的命令。

* `ls` - 列出目录中的内容
* `file`- 确定文件类型
* `less`- 查看文件内容

## 更加愉快地使用 ls

`ls`大概是使用最多的命令了吧，这是有充分理由的。使用`ls`可以查看一个目录包含的内容，并且知道一系列重要的文件和目录属性。就像我们已经知道的，我们可以简单地输入`ls`来获取当前工作目录包含的文件和子目录的列表。

```text
[me@linuxbox ~]$ ls
Desktop Documents Music Pictures Public Templates Videos
```

除了当前目录，我们还可以列出一个指定目录的内容，就像这样：

```text
me@linuxbox ~]$ ls /usr
bin games include lib local sbin share src
```

我们甚至可以指定多个目录。在下面的例子中，我们列出了家目录（用符号「~」表示）和`/usr`目录的内容。

```text
[me@linuxbox ~]$ ls ~ /usr
/home/me:
Desktop Documents Music Pictures Public Templates Videos
/usr:
bin games include lib local sbin share src
```

我们还可以改变输出的格式以展示更多内容。

```text
[me@linuxbox ~]$ ls -l
total 56
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Desktop
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Documents
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Music
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Pictures
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Public
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Templates
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Videos
```

通过给`ls`加`-l`选项，命令的输出变成了长格式。

### 选项和参数

上面的讨论引出了一个非常重要的话题——大多数命令是如何工作的。命令后面经常会跟一个或多个选项——这些选项会改变命令的行为——以及一个或多个参数——该命令作用于参数之上。所以大多数命令看起来都是下面这个样子：

```text
command -options arguments
```

大多数命令使用的选项都是由一个短横加一个字符组成，比如「`-l`」。许多命令（包括 GNU 项目中的命令）也支持长选项，长选项是由两个短横加一个单词组成。还有很多命令也允许多个短选项串起来一块使用。在下面的例子中，`ls`命令有两个选项，分别是`l`选项（产生长格式的输出）和`t`选项（根据文件的修改时间排序）。

```text
[me@linuxbox ~]$ ls -lt
```

然后我们再加上一个长选项`--reverse`，使之倒序排列。

```text
[me@linuxbox ~]$ ls -lt --reverse
```

> **注意：**与文件名一样，Linux 中的命令选项也是大小写敏感的。

`ls`命令支持很多选项，表 3-1 列出了最常用的几个。

| 选项 | 长选项 | 功能描述 |
| :--- | :--- | :--- |
| -a | --all | 列出所有的文件，包括那些文件名以「.」开头的隐藏文件。 |
| -A | --almost-all | 作用与上面的`-a`选项类似，但是不会列出「.」（当前目录）和「..」（上一层目录） |
| -d | --directory | 正常情况下，如果给`ls`命令指定一个目录，它会列出这个目录所包含的内容，而不是这个目录自身。将此选项与`-l`选项一起使用，可以查看有关目录而不是目录内容的详细信息。 |
| -F | --classify | 这个选项会在列出的每一个文件名后面添加一个指示符，例如，如果是一个目录，则会在目录名后面添加一个正斜杠（/）。 |
| -h | --human-readable | 在长格式的列表中，将文件大小以人类容易识别的方式展示出来，而不是展示字节数。 |
| -l |  | 以长格式的方式展示结果 |
| -r | --reverse | 以倒序排列的方式展示结果。正常情况下，`ls`按照字母排列顺序展示结果。 |
| -S |  | 将文件按照大小进行排序。 |
| -t |  | 将文件按照修改时间进行排序。 |

### 

### 深入理解长格式

正如我们在前面看到的，`-l`选项能够让`ls`命令以长格式的方式输出结果。这种格式包含很多有用的信息。下面展示的是 Ubuntu 系统的`Examples`目录：

```text
-rw-r--r-- 1 root root 3576296 2017-04-03 11:05 Experience ubuntu.ogg
-rw-r--r-- 1 root root 1186219 2017-04-03 11:05 kubuntu-leaflet.png
-rw-r--r-- 1 root root 47584 2017-04-03 11:05 logo-Edubuntu.png
-rw-r--r-- 1 root root 44355 2017-04-03 11:05 logo-Kubuntu.png
-rw-r--r-- 1 root root 34391 2017-04-03 11:05 logo-Ubuntu.png
-rw-r--r-- 1 root root 32059 2017-04-03 11:05 oo-cd-cover.odf
-rw-r--r-- 1 root root 159744 2017-04-03 11:05 oo-derivatives.doc
-rw-r--r-- 1 root root 27837 2017-04-03 11:05 oo-maxwell.odt
-rw-r--r-- 1 root root 98816 2017-04-03 11:05 oo-trig.xls
-rw-r--r-- 1 root root 453764 2017-04-03 11:05 oo-welcome.odt
-rw-r--r-- 1 root root 358374 2017-04-03 11:05 ubuntu Sax.ogg
```

表 3-2 为我们提供了其中一个文件的不同字段及其含义。

| 字段 | 含义 |
| :--- | :--- |
| -rw-r--r-- | 文件访问权限。第一个字符用于指示文件类型，短横表示这是一个普通文件， “d”表示这是一个目录。接下来的三个字符代表该文件的所有者对于该文件的 访问权限，再接下来的三个字符代表该文件的所属组成员对该文件的访问权限， 最后的三个字符代表除了前两种用户之外的所有用户（即其他用户）对该文件的访问权限。在第9章——“权限”中我们会详细讨论这一块的具体含义。 |
| 1 | 该文件的硬链接的个数。本章后面的内容“硬链接”和“链接”介绍关于链接的内容。 |
| root | 文件所有者的用户名。 |
| root | 文件所属组的名字。 |
| 32059 | 文件的大小，单位是字节。 |
| 2007-04-03 11:05 | 最后一次修改文件的日期和时间。 |
| oo-cd-cover.odf | 文件名。 |

## 用`file`命令确定文件类型

在我们探索 Linux 系统的时候，知道一个文件包含什么内容至关重要。要想做到这一点，我们可以使用`file`命令来确定一个文件的类型。 正如我们之前讨论的，Linux 中不通过文件名来反映文件的内容。例如一个名为「picture.jpg」的文件，虽然我们一般会认为其中包含的应该是 JPEG 压缩图像， 但是在 Linux 中则不一定。我们可以通过下面这种方式调用`file`命令：

```text
file filename
```

被调用后，`file`会输出简短的文件内容的介绍。例如：

```text
[me@linuxbox ~]$ file picture.jpg
picture.jpg: JPEG image data, JFIF standard 1.01
```

文件类型有很多，事实上，像 Linux 这样的所有类 Unix 操作系统的一个共同点是「一切皆文件」。在本教程的推进过程中，我们将看到这句话是多么正确。

你对系统中的很多文件应该都很熟悉，例如 MP3 文件和 JPEG 文件，但是也有很多文件的类型不是太明显，有一些甚至相当奇怪。

## 用`less`命令查看文件内容

`less`命令可以查看文本文件的内容。在Linux系统中，有很多文件的内容是人类可读的文本，`less`提供了一种简便的方式去查看这些文件。

{% hint style="info" %}
### 什么是「文本」？

在计算机中表达信息有很多种方式，而每一种方式都要考虑，如何定义信息和用来表示信息的数字之间的关系。 毕竟，计算机只认识数字，所以所有的数据最后都要转换成数字。

一些表示系统非常复杂（比如压缩视频文件），但是也有一些就很简单。其中最早被使用也是最简单的一种方式就是_ASCII 文本_。 ASCII（发音为「As-Key」）是美国信息交换标准代码（American Standard Code for Information Interchange）的简称。 这是一种简单的编码方案，最早在 Teletype 机器上用于将键盘字符映射为数字。

文本是字符到数字的简单映射，非常紧凑。50 个字符被翻译成了 50 个字节。文本只包含字符到数字的简单映射，理解这一点至关重要， 它与诸如 Microsoft Word 或LibreOffice Writer 创建的文字处理程序文档不同。与简单的 ASCII 文本相反，这些文件包含许多非文本元素，用于描述其结构和格式。 纯 ASCII 文本文件仅包含字符本身，还包含一些基本的控制代码，例如制表符，回车符和换行符。

在整个 Linux 系统中，许多文件以文本格式存储，并且有许多处理文本文件的 Linux 工具。甚至 Windows 也意识到这种格式的重要性， 众所周知的 NOTEPAD.EXE 程序就是纯 ASCII 文本文件的编辑器。
{% endhint %}

我们为什么要检查文本文件？因为许多包含系统设置的文件（我们称这类文件为_配置文件_）都是以这种格式存储的。 学会阅读这些文件可以给我们一个内部视角去观察系统是如何运作的。除此之外，一些系统使用的真实程序（我们称这类文件为_脚本_）也是以这种格式存储的。 在后面的章节中，我们将学习如何通过编辑文本文件修改系统设置，并学习编写我们自己的脚本。现在我们只是先查看文本文件的内容。

`less`命令的用法如下：

```text
less filename
```

打开文件之后，`less`程序允许我们在文件中前后滚动。 例如，要检查定义所有系统用户帐户的文件，请输入以下命令：

```text
[me@linuxbox ~]$ less /etc/passwd
```

一旦`less`程序启动起来，我们就可以查看这个文件的内容了。 如果这个文件的长度超过了一页，我们可以上下滚动。按下`q`键可以退出`less`。 表 3-3 列出了`less`最常用的键盘命令。

| 命令 |  功能描述 |
| :--- | :--- |
| Page Up 或 b | 向上翻页 |
| Page Down 或 space | 向下翻页 |
| 上键 | 向上滚动一行 |
| 下键 | 向下滚动一行 |
| G | 移动到文本文件的末尾 |
| 1G 或 g | 移动到文本文件的开头 |
| /_搜索内容_ | 向前搜索下一个_搜索内容_出现的位置 |
| n | 搜索上一次搜索的下一次出现 |
| h | 展示帮助信息 |
| q | 退出`less` |

{% hint style="info" %}
### 少就是多

`less`程序是作为一个更早的 Unix 程序——`more`的升级替代品被设计出来的，「less」这个名字来自短语「less is more」（少就是多），这也是现代主义建筑师和设计师的座右铭。

`less`属于被称为「分页器」的那一类程序，这类程序允许用户以逐页的方式轻松查看长文本文档。`less`支持上下来回翻页以及许多其他特性，而`more`只能向下翻页。
{% endhint %}

## 导览

Linux 系统上的文件系统布局与其他类 Unix 系统非常相似。该设计实际上是在称为_Linux文件系统层次结构标准_的已发布标准中指定的。 并非所有 Linux 发行版都完全符合该标准，但是大多数发行版都非常接近。接下来，我们将自己在文件系统中四处逛逛，看看是什么让 Linux 系统运行起来。 这将使我们有机会练习导航技能。我们将发现，许多有趣的文件都是纯人类可读的文本。 在进行游览时，请尝试以下操作：

1. 使用`cd`进入一个给定的目录
2. 使用`ls -l`列出该目录下包含的内容
3. 如果你看到了感兴趣的文件，使用`file`确定它的的内容
4. 如果这个文件看上去可能是文本文件，那么就用`less`命令查看它的内容
5. 如果我们不小心尝试查看了非文本文件，并且它扰乱了终端窗口，则可以通过输入`reset`命令来恢复

{% hint style="warning" %}
**别忘了复制粘贴的技巧！**如果你在使用鼠标，那么你可以通过在一个文件名上双击来复制这个文件名，然后按下鼠标中建将它粘贴到命令中。
{% endhint %}

当我们四处闲逛时，不要害怕看东西。普通用户被最大程度地限制了，以防他们把系统搞砸——搞砸系统是系统管理员的事情！ 如果一个命令报错了，请继续进行其他操作。花一些时间环顾四周，这是我们要探索的系统。 记住，在 Linux 中没有秘密！

表 3-4 仅列出了我们可以探索的目录中的几个，根据我们的 Linux 发行版，可能会有一些细微的差异。 不要害怕，环顾四周，然后尝试更多操作！

_表 3-4：Linux 操作系统中的目录_

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x76EE;&#x5F55;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>/</code>
      </td>
      <td style="text-align:left">&#x6839;&#x76EE;&#x5F55;&#x3002;&#x4E00;&#x5207;&#x90FD;&#x5F00;&#x59CB;&#x4E8E;&#x6B64;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/bin</code>
      </td>
      <td style="text-align:left">&#x5305;&#x542B;&#x7CFB;&#x7EDF;&#x542F;&#x52A8;&#x548C;&#x8FD0;&#x884C;&#x65F6;&#x5FC5;&#x987B;&#x5B58;&#x5728;&#x7684;&#x4E8C;&#x8FDB;&#x5236;&#x6587;&#x4EF6;&#xFF08;&#x7A0B;&#x5E8F;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/boot</code>
      </td>
      <td style="text-align:left">&#x5305;&#x542B; Linux &#x5185;&#x6838;&#x3001;&#x521D;&#x59CB; RAM &#x78C1;&#x76D8;&#x6620;&#x50CF;&#xFF08;&#x5F15;&#x5BFC;&#x65F6;&#x6240;&#x9700;&#x7684;&#x9A71;&#x52A8;&#x7A0B;&#x5E8F;&#xFF09;&#x548C;&#x5F15;&#x5BFC;&#x52A0;&#x8F7D;&#x7A0B;&#x5E8F;&#x3002;&#x5176;&#x4E2D;&#x6709;&#x4E00;&#x4E9B;&#x6709;&#x8DA3;&#x7684;&#x6587;&#x4EF6;&#xFF1A;<code>/boot/grub/grub.conf</code>&#x6216;&#x8005;<code>menu.lst</code>&#xFF0C;&#x7528;&#x4E8E;&#x914D;&#x7F6E;&#x5F15;&#x5BFC;&#x52A0;&#x8F7D;&#x7A0B;&#x5E8F;&#xFF1B;<code>/boot/vmlinuz</code>&#xFF08;&#x6216;&#x8005;&#x4E0E;&#x6B64;&#x7C7B;&#x4F3C;&#x7684;&#x6587;&#x4EF6;&#xFF09;&#xFF0C;Linux
        &#x5185;&#x6838;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/dev</code>
      </td>
      <td style="text-align:left">&#x8FD9;&#x662F;&#x4E00;&#x4E2A;&#x5305;&#x542B;<em>&#x8BBE;&#x5907;&#x8282;&#x70B9;</em>&#x7684;&#x7279;&#x6B8A;&#x76EE;&#x5F55;&#xFF0C;&#x300C;&#x4E00;&#x5207;&#x7686;&#x6587;&#x4EF6;&#x300D;&#x7684;&#x601D;&#x60F3;&#x540C;&#x6837;&#x9002;&#x7528;&#x4E8E;&#x8BBE;&#x5907;&#xFF0C;&#x8FD9;&#x91CC;&#x662F;&#x5185;&#x6838;&#x7EF4;&#x62A4;&#x5B83;&#x652F;&#x6301;&#x7684;&#x6240;&#x6709;&#x8BBE;&#x5907;&#x5217;&#x8868;&#x7684;&#x5730;&#x65B9;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/etc</code>
      </td>
      <td style="text-align:left">
        <p>&#x5305;&#x542B;&#x914D;&#x7F6E;&#x6587;&#x4EF6;&#x548C; shell &#x811A;&#x672C;&#xFF0C;&#x6240;&#x6709;&#x80FD;&#x591F;&#x5F71;&#x54CD;&#x7CFB;&#x7EDF;&#x5168;&#x5C40;&#x8303;&#x56F4;&#x7684;&#x914D;&#x7F6E;&#x6587;&#x4EF6;&#x5747;&#x5728;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x4E0B;&#xFF0C;&#x7CFB;&#x7EDF;&#x542F;&#x52A8;&#x65F6;&#xFF0C;&#x4F1A;&#x6267;&#x884C;<code>/etc</code>&#x76EE;&#x5F55;&#x4E0B;&#x7684;&#x811A;&#x672C;&#xFF0C;&#x4EE5;&#x542F;&#x52A8;&#x4E00;&#x4E9B;&#x670D;&#x52A1;&#x3002;<code>/etc</code>&#x76EE;&#x5F55;&#x4E0B;&#x7684;&#x6240;&#x6709;&#x6587;&#x4EF6;&#x90FD;&#x662F;&#x53EF;&#x8BFB;&#x7684;&#x6587;&#x672C;&#x6587;&#x4EF6;&#x3002;</p>
        <p><code>/etc</code>&#x76EE;&#x5F55;&#x4E0B;&#x51E0;&#x4E2A;&#x6BD4;&#x8F83;&#x91CD;&#x8981;&#x7684;&#x6587;&#x4EF6;&#xFF08;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x4E0B;&#x7684;&#x6587;&#x4EF6;&#x90FD;&#x5F88;&#x91CD;&#x8981;&#xFF0C;&#x8FD9;&#x91CC;&#x8BF4;&#x51E0;&#x4E2A;&#x76F8;&#x5BF9;&#x6765;&#x8BF4;&#x6BD4;&#x8F83;&#x91CD;&#x8981;&#x7684;&#xFF09;&#xFF1A;</p>
        <ol>
          <li><code>/etc/crontab</code>&#xFF0C;&#x914D;&#x7F6E;&#x5B9A;&#x65F6;&#x4EFB;&#x52A1;&#x7684;&#x6587;&#x4EF6;&#x3002;&#x6709;&#x4E2A;&#x547D;&#x4EE4;<code>crontab -e</code>&#xFF0C;&#x53EF;&#x4EE5;&#x914D;&#x7F6E;&#x5B9A;&#x65F6;&#x4EFB;&#x52A1;&#xFF0C;&#x5176;&#x5B9E;&#x8FD9;&#x4E2A;&#x547D;&#x4EE4;&#x6700;&#x7EC8;&#x4E5F;&#x662F;&#x4FEE;&#x6539;&#x4E86;&#x6587;&#x4EF6;<code>/etc/crontab</code>&#x3002;&#x800C;&#x547D;&#x4EE4;<code>crontab -l</code>&#x662F;&#x67E5;&#x770B;&#x5F53;&#x524D;&#x7CFB;&#x7EDF;&#x4E2D;&#x5DF2;&#x6709;&#x7684;&#x5B9A;&#x65F6;&#x4EFB;&#x52A1;&#xFF0C;&#x5176;&#x5B9E;&#x4E5F;&#x662F;&#x663E;&#x793A;&#x7684; <code>/etc/crontab</code>&#x8FD9;&#x4E2A;&#x6587;&#x4EF6;&#x7684;&#x5185;&#x5BB9;&#x3002;</li>
          <li><code>/etc/fstab</code>&#xFF0C;&#x8BB0;&#x5F55;&#x5F53;&#x524D;&#x7CFB;&#x7EDF;&#x7684;&#x5B58;&#x50A8;&#x8BBE;&#x5907;&#x4EE5;&#x53CA;&#x4ED6;&#x4EEC;&#x7684;&#x6302;&#x8F7D;&#x70B9;&#x3002;</li>
          <li><code>/etc/passwd</code>&#xFF0C;&#x8BB0;&#x5F55;&#x5F53;&#x524D;&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;&#x6240;&#x6709;&#x7528;&#x6237;&#x4FE1;&#x606F;&#x3002;</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/home</code>
      </td>
      <td style="text-align:left">&#x5728;&#x9ED8;&#x8BA4;&#x7684;&#x914D;&#x7F6E;&#x4E2D;&#xFF0C;&#x7CFB;&#x7EDF;&#x4F1A;&#x5728;/home&#x76EE;&#x5F55;&#x4E2D;&#x7ED9;&#x6BCF;&#x4E00;&#x4E2A;&#x7528;&#x6237;&#x5206;&#x914D;&#x4E00;&#x4E2A;&#x5BB6;&#x76EE;&#x5F55;&#xFF0C;&#x666E;&#x901A;&#x7528;&#x6237;&#x53EA;&#x80FD;&#x5728;&#x4ED6;&#x4EEC;&#x81EA;&#x5DF1;&#x7684;&#x5BB6;&#x76EE;&#x5F55;&#x4E2D;&#x5199;&#x6587;&#x4EF6;&#xFF0C;&#x8FD9;&#x79CD;&#x9650;&#x5236;&#x662F;&#x4E3A;&#x4E86;&#x4FDD;&#x62A4;&#x7CFB;&#x7EDF;&#x4E0D;&#x88AB;&#x7528;&#x6237;&#x9519;&#x8BEF;&#x7684;&#x884C;&#x4E3A;&#x7834;&#x574F;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/lib</code>
      </td>
      <td style="text-align:left">&#x5305;&#x542B;&#x6838;&#x5FC3;&#x7CFB;&#x7EDF;&#x7A0B;&#x5E8F;&#x4F7F;&#x7528;&#x7684;&#x5171;&#x4EAB;&#x5E93;&#x6587;&#x4EF6;&#xFF0C;&#x7C7B;&#x4F3C;&#x4E8E;
        Windows &#x4E2D;&#x7684;&#x52A8;&#x6001;&#x94FE;&#x63A5;&#x5E93;&#xFF08;DLL&#xFF09;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/lost+found</code>
      </td>
      <td style="text-align:left">&#x6BCF;&#x4E00;&#x4E2A;&#x4F7F;&#x7528; Linux &#x6587;&#x4EF6;&#x7CFB;&#x7EDF;&#xFF08;&#x6BD4;&#x5982;
        ext4&#xFF09;&#x7684;&#x683C;&#x5F0F;&#x5316;&#x5206;&#x533A;&#x6216;&#x8BBE;&#x5907;&#x90FD;&#x6709;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#xFF0C;&#x5F53;&#x5206;&#x533A;&#x4ECE;&#x6587;&#x4EF6;&#x7CFB;&#x7EDF;&#x4E2D;&#x65AD;&#x4E8B;&#x4EF6;&#x4E2D;&#x6062;&#x590D;&#x65F6;&#xFF0C;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x5C31;&#x4F1A;&#x6D3E;&#x4E0A;&#x7528;&#x573A;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/media</code>
      </td>
      <td style="text-align:left">&#x5728;&#x73B0;&#x4EE3; Linux &#x64CD;&#x4F5C;&#x7CFB;&#x7EDF;&#x4E2D;&#xFF0C;<code>/media</code>&#x76EE;&#x5F55;&#x4E3A;&#x53EF;&#x79FB;&#x52A8;&#x5A92;&#x4F53;&#xFF08;&#x6BD4;&#x5982;
        USB &#x9A71;&#x52A8;&#x5668;&#x3001;CD-ROM &#x7B49;&#xFF09;&#x63D0;&#x4F9B;&#x6302;&#x8F7D;&#x70B9;&#xFF0C;&#x8FD9;&#x4E9B;&#x53EF;&#x79FB;&#x52A8;&#x5A92;&#x4F53;&#x5728;&#x63D2;&#x5165;&#x65F6;&#x4F1A;&#x81EA;&#x52A8;&#x6302;&#x8F7D;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/mnt</code>
      </td>
      <td style="text-align:left">&#x5728;&#x8001;&#x7684; Linux &#x64CD;&#x4F5C;&#x7CFB;&#x7EDF;&#x4E0A;&#xFF0C;&#x53EF;&#x79FB;&#x52A8;&#x8BBE;&#x5907;&#x5FC5;&#x987B;&#x624B;&#x52A8;&#x6302;&#x8F7D;&#xFF0C;<code>/mnt</code>&#x4E3A;&#x5B83;&#x4EEC;&#x63D0;&#x4F9B;&#x6302;&#x8F7D;&#x70B9;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/opt</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/proc</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/root</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/sbin</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/tmp</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/usr</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/usr/bin</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/usr/local</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/usr/sbin</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/usr/share</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/usr/share/doc</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/var</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/var/log</code>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>



