既然我们已经知道了如何在文件系统中移动，那么是时候开始我们在 Linux 系统中的旅程了，但是在出发前，我们需要再多学习几个沿途能用得上的命令。

- `ls` - 列出目录中的内容
- `file`-确定文件类型
- `less`-查看文件内容

# 更加愉快地使用 ls

`ls`大概是使用最多的命令了吧，这是有充分理由的。使用ls`，我们可以查看一个目录包含的内容，并且知道一系列重要的文件和目录属性。就像我们已经知道的，我们可以简单地输入`ls`来获取当前工作目录包含的文件和子目录的列表。

```
[me@linuxbox ~]$ ls
Desktop Documents Music Pictures Public Templates Videos
```

除了当前目录，我们还可以列出一个指定目录的内容，就像这样：

```
me@linuxbox ~]$ ls /usr
bin games include lib local sbin share src
```

我们甚至可以指定多个目录。在下面的例子中，我们列出了家目录（用符号「~」表示）和`/usr`目录的内容。

```
[me@linuxbox ~]$ ls ~ /usr
/home/me:
Desktop Documents Music Pictures Public Templates Videos
/usr:
bin games include lib local sbin share src
```

我们还可以改变输出的格式以展示更多内容。

```
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

## 选项和参数

上面的讨论引出了一个非常重要的话题——大多数命令是如何工作的。命令后面经常会跟一个或多个选项——这些选项会改变命令的行为——以及一个或多个参数——该命令作用于参数之上。所以大多数命令看起来都是下面这个样子：

```
command -options arguments
```

大多数命令使用的选项都是由一个短横加一个字符组成，比如「-l」。许多命令（包括 GNU 项目中的命令）也支持<i>长选项</i>，长选项是由两个短横加一个单词组成。还有很多命令也允许多个短选项串起来一块使用。在下面的例子中，`ls`命令有两个选项，分别是`l`选项（产生长格式的输出）和`t`选项（根据文件的修改时间排序）。

```
[me@linuxbox ~]$ ls -lt
```

然后我们再加上一个长选项`--reverse`，使之倒序排列。

```
[me@linuxbox ~]$ ls -lt --reverse
```

> **注意：**与文件名一样，Linux 中的命令选项也是大小写敏感的。

`ls`命令支持很多选项，表 3-1 中列出了最常用的几个。

| 选项 | 长选项           | 功能描述                                                     |
| ---- | :--------------- | :----------------------------------------------------------- |
| -a   | --all            | 列出所有的文件，包括那些文件名以「.」开头的隐藏文件。        |
| -A   | --almost-all     | 作用与上面的`-a`选项类似，但是不会列出「.」（当前目录）和「..」（上一层目录） |
| -d   | --directory      | 正常情况下，如果给`ls`命令指定一个目录，它会列出这个目录所包含的内容，而不是这个目录自身。将此选项与`-l`选项一起使用，可以查看有关目录而不是目录内容的详细信息。 |
| -F   | --classify       | 这个选项会在列出的每一个文件名后面添加一个指示符，例如，如果是一个目录，则会在目录名后面添加一个正斜杠（/）。 |
| -h   | --human-readable | 在长格式的列表中，将文件大小以人类容易识别的方式展示出来，而不是展示字节数。 |
| -l   |                  | 以长格式的方式展示结果                                       |
| -r   | -reverse         | 以倒序排列的方式展示结果。正常情况下，`ls`按照字母排列顺序展示结果。 |
| -S   |                  | 将文件按照大小进行排序。                                     |
| -t   |                  | 将文件按照修改时间进行排序。                                 |

<center><i><font face="楷体">表3-1 ls命令的选项</i></font></center>

## 深入理解长格式

![image-20200725105449898](image-20200725105449898.png)

正如我们在前面看到的，`-l`选项能够让`ls`命令以长格式的方式输出结果。这种格式包含很多有用的信息。下面展示的是 Ubuntu 系统的`Examples`目录：

```
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

![image-20200725105831596](image-20200725105831596.png)

表 3-2 为我们提供了其中一个文件的不同字段及其含义。

| 字段 | 含义 |
| ---- | ---- |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |

