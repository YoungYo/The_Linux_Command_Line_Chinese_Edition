# 译者序

本书翻译自《The Linux Command Line》网络版第 5 版，建议在 GitBook 上阅读，[GitBook 传送门](https://app.gitbook.com/@supermouse/s/the-linux-command-line/v/main/)。若在 GitHub 上阅读，可以打开 SUMMARY.md 查看目录。

{% file src=".gitbook/assets/the\_linux\_command\_line\_fifth\_internet\_edition.pdf" caption="点击此处下载原书电子版" %}

## 书中一些样式的约定

### 命令及文件名样式

行间命令及文件名用这种格式：`command`，比如下面句话：

> 用这条命令`ls /usr`可以查看`/usr`目录的内容。

如果是展示命令行内容，用这种格式：

```text
[me@linuxbox ~]$ ls
Desktop Documents Music Pictures Public Templates Videos
```

### 第一次出现的专业术语

如果是书中第一次出现的专有名词，会用斜体，以示强调。比如：

> `cd`命令可以切换工作目录，其用法是，在命令行中输入`cd`，然后输入你想切换的_路径名_。

其中「路径名」是一个专业术语，并且在整本书中是第一次出现，所以用斜体表示，以后再出现「路径名」这个词时，就不再用斜体了。

### 需要使用双引号的文字

在本书中，用「」代替双引号“”，因为在网页上显示时，前者更加美观。使用方法如下：

> Linux 中一个重要的理念是「一切皆文件」。

### 额外的解释信息

额外的解释信息用下面这种样式：

{% hint style="info" %}
### 少就是多

`less`程序是作为一个更早的 Unix 程序——`more`的升级替代品被设计出来的，「less」这个名字来自短语「less is more」（少就是多），这也是现代主义建筑师和设计师的座右铭。
{% endhint %}

### 警告信息

警告信息用下面这种样式：

{% hint style="warning" %}
不要在 Linux 命令行中尝试使用 Ctrl-C 和 Ctrl-V 进行复制粘贴，因为 Ctrl-C 不是复制，而是结束进程。
{% endhint %}

