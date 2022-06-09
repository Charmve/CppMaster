# Q 1.1 ★★☆ 文件系统的原理，特别是 inode 和 block

## 文件系统的组成：

- inode：一个文件占用一个 inode，记录文件的属性，同时记录此文件的内容所在的 block 编号；
- block：记录文件的内容，文件太大时，会占用多个 block。

除此之外还包括：

- superblock：记录文件系统的整体信息，包括 inode 和 block 的总量、使用量、剩余量，以及文件系统的格式与相关信息等；
- block bitmap：记录 block 是否被使用的位域。

<div align="center"> <img src="https://gitee.com/CyC2018/CS-Notes/raw/master/docs/pics/BSD_disk.png" width="800"/> </div><br>

## block

在 Ext2 文件系统中所支持的 block 大小有 1K，2K 及 4K 三种，不同的大小限制了单个文件和文件系统的最大大小。

| 大小 | 1KB | 2KB | 4KB |
| :---: | :---: | :---: | :---: |
| 最大单一文件 | 16GB | 256GB | 2TB |
| 最大文件系统 | 2TB | 8TB | 16TB |

一个 block 只能被一个文件所使用，未使用的部分直接浪费了。因此如果需要存储大量的小文件，那么最好选用比较小的 block。

## inode

inode 具体包含以下信息：

- 权限 (read/write/excute)；
- 拥有者与群组 (owner/group)；
- 容量；
- 建立或状态改变的时间 (ctime)；
- 最近一次的读取时间 (atime)；
- 最近修改的时间 (mtime)；
- 定义文件特性的旗标 (flag)，如 SetUID...；
- 该文件真正内容的指向 (pointer)。

inode 具有以下特点：

- 每个 inode 大小均固定为 128 bytes (新的 ext4 与 xfs 可设定到 256 bytes)；
- 每个文件都仅会占用一个 inode。

inode 中记录了文件内容所在的 block 编号，但是每个 block 非常小，一个大文件随便都需要几十万的 block。而一个 inode 大小有限，无法直接引用这么多 block 编号。因此引入了间接、双间接、三间接引用。间接引用是指，让 inode 记录的引用 block 块记录引用信息。

<div align="center"> <img src="https://gitee.com/CyC2018/CS-Notes/raw/master/docs/pics/inode_with_signatures.jpg" width="600"/> </div><br>



# Q 1.2 ★★☆ 数据恢复原理


# Q 2. ★★★ 硬链接与软链接的区别

## 1.Linux的文件和目录
现代操作系统为解决信息能独立于进程之外被长期存储引入了文件，文件作为进程创建信息的逻辑单元可被多个进程并发使用。在 UNIX 系统中，操作系统为磁盘上的文本与图像、鼠标与键盘等输入设备及网络交互等 I/O 操作设计了一组通用 API，使他们被处理时均可统一使用字节流方式。换言之，UNIX 系统中除进程之外的**一切皆是文件**，而 Linux 保持了这一特性。为了便于文件的管理，Linux 还引入了目录（有时亦被称为文件夹）这一概念。目录使文件可被分类管理，且目录的引入使 Linux 的文件系统形成一个层级结构的目录树。清单 1.所示的是普通 Linux 系统的顶层目录结构，其中 /dev 是存放了设备相关文件的目录。

清单 1. Linux 系统的顶层目录结构  
```
/              根目录
├── bin     存放用户二进制文件
├── boot    存放内核引导配置文件
├── dev     存放设备文件
├── etc     存放系统配置文件
├── home    用户主目录
├── lib     动态共享库
├── lost+found  文件系统恢复时的恢复文件
├── media   可卸载存储介质挂载点
├── mnt     文件系统临时挂载点
├── opt     附加的应用程序包
├── proc    系统内存的映射目录，提供内核与进程信息
├── root    root 用户主目录
├── sbin    存放系统二进制文件
├── srv     存放服务相关数据
├── sys     sys 虚拟文件系统挂载点
├── tmp     存放临时文件
├── usr     存放用户应用程序
└── var     存放邮件、系统日志等变化文件
```

Linux 与其他类 UNIX 系统一样并不区分文件与目录：目录是记录了其他文件名的文件。使用命令 mkdir 创建目录时，若期望创建的目录的名称与现有的文件名（或目录名）重复，则会创建失败。

```
# ls -F /usr/bin/zi* 
/usr/bin/zip*       /usr/bin/zipgrep*  /usr/bin/zipnote* 
/usr/bin/zipcloak*  /usr/bin/zipinfo*  /usr/bin/zipsplit* 
 
# mkdir -p /usr/bin/zip 
mkdir: cannot create directory `/usr/bin/zip': File exists
```

Linux 将设备当做文件进行处理，清单 2.展示了如何打开设备文件 /dev/input/event5 并读取文件内容。文件 event5 表示一种输入设备，其可能是鼠标或键盘等。查看文件 /proc/bus/input/devices 可知 event5 对应设备的类型。设备文件 /dev/input/event5 使用 read() 以字符流的方式被读取。结构体 input_event 被定义在内核头文件 linux/input.h 中。

清单 2. 打开并读取设备文件

```
int fd; 
struct input_event ie; 
fd = open("/dev/input/event5", O_RDONLY); 
read(fd, &ie, sizeof(struct input_event)); 
printf("type = %d  code = %d  value = %d\n", 
            ie.type, ie.code, ie.value); 
close(fd);
```

## 2.硬链接和软连接的区别与联系

我们知道文件都有文件名与数据，这在 Linux 上被分成两个部分：用户数据 (user data) 与元数据 (metadata)。用户数据，即文件数据块 (data block)，数据块是记录文件真实内容的地方；而元数据则是文件的附加属性，如文件大小、创建时间、所有者等信息。在 Linux 中，元数据中的 inode 号（inode 是文件元数据的一部分但其并不包含文件名，inode 号即索引节点号）才是文件的唯一标识而非文件名。文件名仅是为了方便人们的记忆和使用，系统或程序通过 inode 号寻找正确的文件数据块。图 1.展示了程序通过文件名获取文件内容的过程。

图 1. 通过文件名打开文件

<div align="center"> <img src="https://www.ibm.com/developerworks/cn/linux/l-cn-hardandsymb-links/image001.jpg" width="800"/> </div><br>

清单 3. 移动或重命名文件

```
# stat /home/harris/source/glibc-2.16.0.tar.xz 
 File: `/home/harris/source/glibc-2.16.0.tar.xz'
 Size: 9990512      Blocks: 19520      IO Block: 4096   regular file 
Device: 807h/2055d      Inode: 2485677     Links: 1 
Access: (0600/-rw-------)  Uid: ( 1000/  harris)   Gid: ( 1000/  harris) 
... 
... 
# mv /home/harris/source/glibc-2.16.0.tar.xz /home/harris/Desktop/glibc.tar.xz 
# ls -i -F /home/harris/Desktop/glibc.tar.xz 
2485677 /home/harris/Desktop/glibc.tar.xz
```

在 Linux 系统中查看 inode 号可使用命令 stat 或 ls -i（若是 AIX 系统，则使用命令 istat）。清单 3.中使用命令 mv 移动并重命名文件 glibc-2.16.0.tar.xz，其结果不影响文件的用户数据及 inode 号，文件移动前后 inode 号均为：2485677。  

为解决文件的共享使用，Linux 系统引入了两种链接：硬链接 (hard link) 与软链接（又称符号链接，即 soft link 或 symbolic link）。链接为 Linux 系统解决了文件的共享使用，还带来了隐藏文件路径、增加权限安全及节省存储等好处。若一个 inode 号对应多个文件名，则称这些文件为硬链接。换言之，硬链接就是同一个文件使用了多个别名（见 图 2.hard link 就是 file 的一个别名，他们有共同的 inode）。硬链接可由命令 link 或 ln 创建。如下是对文件 oldfile 创建硬链接。

```
link oldfile newfile 
ln oldfile newfile
```

由于硬链接是有着相同 inode 号仅文件名不同的文件，因此硬链接存在以下几点特性：
- 文件有相同的 inode 及 data block；
- 只能对已存在的文件进行创建；
- 不能交叉文件系统进行硬链接的创建；
- 不能对目录进行创建，只可对文件创建；
- 删除一个硬链接文件并不影响其他有相同 inode 号的文件。

清单 4. 硬链接特性展示

```
# ls -li 
total 0 
 
// 只能对已存在的文件创建硬连接
# link old.file hard.link 
link: cannot create link `hard.link' to `old.file': No such file or directory 
 
# echo "This is an original file" > old.file 
# cat old.file 
This is an original file 
# stat old.file 
 File: `old.file'
 Size: 25           Blocks: 8          IO Block: 4096   regular file 
Device: 807h/2055d      Inode: 660650      Links: 2 
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root) 
... 
// 文件有相同的 inode 号以及 data block 
# link old.file hard.link | ls -li 
total 8 
660650 -rw-r--r-- 2 root root 25 Sep  1 17:44 hard.link 
660650 -rw-r--r-- 2 root root 25 Sep  1 17:44 old.file 
 
// 不能交叉文件系统
# ln /dev/input/event5 /root/bfile.txt 
ln: failed to create hard link `/root/bfile.txt' => `/dev/input/event5': 
Invalid cross-device link 
 
// 不能对目录进行创建硬连接
# mkdir -p old.dir/test 
# ln old.dir/ hardlink.dir 
ln: `old.dir/': hard link not allowed for directory 
# ls -iF 
660650 hard.link  657948 old.dir/  660650 old.file
```

文件 old.file 与 hard.link 有着相同的 inode 号：660650 及文件权限，inode 是随着文件的存在而存在，因此只有当文件存在时才可创建硬链接，即当 inode 存在且链接计数器（link count）不为 0 时。inode 号仅在各文件系统下是唯一的，当 Linux 挂载多个文件系统后将出现 inode 号重复的现象（如 清单 5.所示，文件 t3.jpg、sync 及 123.txt 并无关联，却有着相同的 inode 号），因此硬链接创建时不可跨文件系统。设备文件目录 /dev 使用的文件系统是 devtmpfs，而 /root（与根目录 / 一致）使用的是磁盘文件系统 ext4。清单 5.展示了使用命令 df 查看当前系统中挂载的文件系统类型、各文件系统 inode 使用情况及文件系统挂载点。

清单 5. 查找有相同 inode 号的文件

```
# df -i --print-type 
Filesystem     Type       Inodes  IUsed    IFree IUse% Mounted on 
/dev/sda7      ext4      3147760 283483  2864277   10% / 
udev           devtmpfs   496088    553   495535    1% /dev 
tmpfs          tmpfs      499006    491   498515    1% /run 
none           tmpfs      499006      3   499003    1% /run/lock 
none           tmpfs      499006     15   498991    1% /run/shm 
/dev/sda6      fuseblk  74383900   4786 74379114    1% /media/DiskE 
/dev/sda8      fuseblk  29524592  19939 29504653    1% /media/DiskF 
 
# find / -inum 1114 
/media/DiskE/Pictures/t3.jpg 
/media/DiskF/123.txt 
/bin/sync
```

软链接与硬链接不同，若文件用户数据块中存放的内容是另一文件的路径名的指向，则该文件就是软连接。软链接就是一个普通文件，只是数据块内容有点特殊。软链接有着自己的 inode 号以及用户数据块（见 图 2.）。因此软链接的创建与使用没有类似硬链接的诸多限制：

- 软链接有自己的文件属性及权限等； 
- 可对不存在的文件或目录创建软链接；  
- 软链接可交叉文件系统；  
- 软链接可对文件或目录创建；  
- 创建软链接时，链接计数 i_nlink 不会增加；  
- 删除软链接并不影响被指向的文件，但若被指向的原文件被删除，则相关软连接被称为死链接（即 dangling link，若被指向路径文件被重新创建，死链接可恢复为正常的软链接）。  

图 2. 软链接的访问  
<div align="center"> <img src="https://www.ibm.com/developerworks/cn/linux/l-cn-hardandsymb-links/image002.jpg" width="800"/> </div><br>

清单 7. 软链接特性展示

```
# ls -li 
 total 0 
 
 // 可对不存在的文件创建软链接
 # ln -s old.file soft.link 
 # ls -liF 
 total 0 
 789467 lrwxrwxrwx 1 root root 8 Sep  1 18:00 soft.link -> old.file 
 
 // 由于被指向的文件不存在，此时的软链接 soft.link 就是死链接
 # cat soft.link 
 cat: soft.link: No such file or directory 
 
 // 创建被指向的文件 old.file，soft.link 恢复成正常的软链接
 # echo "This is an original file_A" >> old.file 
 # cat soft.link 
 This is an original file_A 
 
 // 对不存在的目录创建软链接
 # ln -s old.dir soft.link.dir 
 # mkdir -p old.dir/test 
 # tree . -F --inodes 
 . 
├── [ 789497]  old.dir/ 
│   └── [ 789498]  test/ 
├── [ 789495]  old.file 
├── [ 789495]  soft.link -> old.file 
└── [ 789497]  soft.link.dir -> old.dir/
```

#Linux常用命令

**查看文本：cat、tac、more、less、head、tail**

# Q 3.1 ★★☆cat 文件内容查看

取得文件内容。

```
# cat [-AbEnTv] filename
-n ：打印出行号，连同空白行也会有行号，-b 不会
```

- tac：是cat的反向操作，从最后一行开始打印；  
- more：和cat不同的是它可以一页一页地查看文件内容，比较适合大文件的查看；  
- less：和more类似，但是多了一个向前翻页的功能；  
- head：取得文件前几行；  
- tail：取得文件后几行。  





# Q 3.2 ★★☆find 搜索文件

文件搜索，可以使用文件的属性和权限进行搜索。

```html
# find [basedir] [option]
example: find . -name "shadow*"
```
**① 与时间有关的选项** 

```html
-mtime  n ：列出在 n 天前的那一天修改过内容的文件
-mtime +n ：列出在 n 天之前 (不含 n 天本身) 修改过内容的文件
-mtime -n ：列出在 n 天之内 (含 n 天本身) 修改过内容的文件
-newer file ： 列出比 file 更新的文件
```

+4、4 和 -4 的指示的时间范围如下：

<div align="center"> <img src="https://gitee.com/CyC2018/CS-Notes/raw/master/docs/pics/658fc5e7-79c0-4247-9445-d69bf194c539.png" width=""/> </div><br>

**② 与文件拥有者和所属群组有关的选项** 

```html
-uid n
-gid n
-user name
-group name
-nouser ：搜索拥有者不存在 /etc/passwd 的文件
-nogroup：搜索所属群组不存在于 /etc/group 的文件
```

**③ 与文件权限和名称有关的选项** 

```html
-name filename
-size [+-]SIZE：搜寻比 SIZE 还要大 (+) 或小 (-) 的文件。这个 SIZE 的规格有：c: 代表 byte，k: 代表 1024bytes。所以，要找比 50KB 还要大的文件，就是 -size +50k
-type TYPE
-perm mode  ：搜索权限等于 mode 的文件
-perm -mode ：搜索权限包含 mode 的文件
-perm /mode ：搜索权限包含任一 mode 的文件
```

# Q 3.3 ★★☆cut

cut 对数据进行切分，取出想要的部分。

切分过程一行一行地进行。

```html
$ cut
-d ：分隔符
-f ：经过 -d 分隔后，使用 -f n 取出第 n 个区间
-c ：以字符为单位取出区间
```

示例 1：last 显示登入者的信息，取出用户名。

```html
$ last
root pts/1 192.168.201.101 Sat Feb 7 12:35 still logged in
root pts/1 192.168.201.101 Fri Feb 6 12:13 - 18:46 (06:33)
root pts/1 192.168.201.254 Thu Feb 5 22:37 - 23:53 (01:16)

$ last | cut -d ' ' -f 1
```

示例 2：将 export 输出的信息，取出第 12 字符以后的所有字符串。

```html
$ export
declare -x HISTCONTROL="ignoredups"
declare -x HISTSIZE="1000"
declare -x HOME="/home/dmtsai"
declare -x HOSTNAME="study.centos.vbird"
.....(其他省略).....

$ export | cut -c 12-
```

# Q 3.4 ★★☆sort

```html
$ sort [-fbMnrtuk] [file or stdin]
-f ：忽略大小写
-b ：忽略最前面的空格
-M ：以月份的名字来排序，例如 JAN，DEC
-n ：使用数字
-r ：反向排序
-u ：相当于 unique，重复的内容只出现一次
-t ：分隔符，默认为 tab
-k ：指定排序的区间
```

示例：/etc/passwd 文件内容以 : 来分隔，要求以第三列进行排序。

```html
$ cat /etc/passwd | sort -t ':' -k 3
root:x:0:0:root:/root:/bin/bash
dmtsai:x:1000:1000:dmtsai:/home/dmtsai:/bin/bash
alex:x:1001:1002::/home/alex:/bin/bash
arod:x:1002:1003::/home/arod:/bin/bash
```

# Q 3.5 ★★☆grep

g/re/p（globally search a regular expression and print)，使用正则表示式进行全局查找并打印。

```html
$ grep [-acinv] [--color=auto] 搜寻字符串 filename
-c ： 统计个数
-i ： 忽略大小写
-n ： 输出行号
-v ： 反向选择，也就是显示出没有 搜寻字符串 内容的那一行
--color=auto ：找到的关键字加颜色显示
```

示例：把含有 the 字符串的行提取出来（注意默认会有 --color=auto 选项，因此以下内容在 Linux 中有颜色显示 the 字符串）

```html
$ grep -n 'the' regular_express.txt
8:I can't finish the test.
12:the symbol '*' is represented as start.
15:You are the best is mean you are the no. 1.
16:The world Happy is the same with "glad".
18:google is the best tools for search keyword
```

因为 { 和 } 在 shell 是有特殊意义的，因此必须要使用转义字符进行转义。

```html
$ grep -n 'go\{2,5\}g' regular_express.txt
```

# Q 3.6 ★★☆ awk

awk是一个强大的文本分析工具，相对于grep的查找，sed的编辑，awk在其对数据分析并生成报告时，显得尤为强大。简单来说awk就是把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行各种分析处理。

是由 Alfred Aho，Peter Weinberger, 和 Brian Kernighan 创造，awk 这个名字就是这三个创始人名字的首字母。

awk 每次处理一行，处理的最小单位是字段，每个字段的命名方式为：\$n，n 为字段号，从 1 开始，\$0 表示一整行。

示例：取出最近五个登录用户的用户名和 IP

```html
$ last -n 5
dmtsai pts/0 192.168.1.100 Tue Jul 14 17:32 still logged in
dmtsai pts/0 192.168.1.100 Thu Jul 9 23:36 - 02:58 (03:22)
dmtsai pts/0 192.168.1.100 Thu Jul 9 17:23 - 23:36 (06:12)
dmtsai pts/0 192.168.1.100 Thu Jul 9 08:02 - 08:17 (00:14)
dmtsai tty1 Fri May 29 11:55 - 12:11 (00:15)
```

```html
$ last -n 5 | awk '{print $1 "\t" $3}'
```

可以根据字段的某些条件进行匹配，例如匹配字段小于某个值的那一行数据。

```html
$ awk '条件类型 1 {动作 1} 条件类型 2 {动作 2} ...' filename
```

示例：/etc/passwd 文件第三个字段为 UID，对 UID 小于 10 的数据进行处理。

```text
$ cat /etc/passwd | awk 'BEGIN {FS=":"} $3 < 10 {print $1 "\t " $3}'
root 0
bin 1
daemon 2
```

awk 变量：

| 变量名称 | 代表意义 |
| :--: | -- |
| NF | 每一行拥有的字段总数 |
| NR | 目前所处理的是第几行数据 |
| FS | 目前的分隔字符，默认是空格键 |

示例：显示正在处理的行号以及每一行有多少字段

```html
$ last -n 5 | awk '{print $1 "\t lines: " NR "\t columns: " NF}'
dmtsai lines: 1 columns: 10
dmtsai lines: 2 columns: 10
dmtsai lines: 3 columns: 10
dmtsai lines: 4 columns: 10
dmtsai lines: 5 columns: 9
```

# Q 4 ★★★ 僵尸进程与孤儿进程的区别

## 进程状态

| 状态 | 说明 |
| :---: | --- |
| R | running or runnable (on run queue) |
| D | uninterruptible sleep (usually I/O) |
| S | interruptible sleep (waiting for an event to complete) |
| Z | zombie (terminated but not reaped by its parent) |
| T | stopped (either by a job control signal or because it is being traced) |
<br>
<div align="center"> <img src="https://gitee.com/CyC2018/CS-Notes/raw/master/docs/pics/76a49594323247f21c9b3a69945445ee.png" width=""/> </div><br>

## SIGCHLD

当一个子进程改变了它的状态时（停止运行，继续运行或者退出），有两件事会发生在父进程中：

- 得到 SIGCHLD 信号；
- waitpid() 或者 wait() 调用会返回。

其中子进程发送的 SIGCHLD 信号包含了子进程的信息，比如进程 ID、进程状态、进程使用 CPU 的时间等。

在子进程退出时，它的进程描述符不会立即释放，这是为了让父进程得到子进程信息，父进程通过 wait() 和 waitpid() 来获得一个已经退出的子进程的信息。

<div align="center"> <img src="https://gitee.com/CyC2018/CS-Notes/raw/master/docs/pics/flow.png" width=""/> </div><br>

## wait()

```c
pid_t wait(int *status)
```

父进程调用 wait() 会一直阻塞，直到收到一个子进程退出的 SIGCHLD 信号，之后 wait() 函数会销毁子进程并返回。

如果成功，返回被收集的子进程的进程 ID；如果调用进程没有子进程，调用就会失败，此时返回 -1，同时 errno 被置为 ECHILD。

参数 status 用来保存被收集的子进程退出时的一些状态，如果对这个子进程是如何死掉的毫不在意，只想把这个子进程消灭掉，可以设置这个参数为 NULL。

## waitpid()

```c
pid_t waitpid(pid_t pid, int *status, int options)
```

作用和 wait() 完全相同，但是多了两个可由用户控制的参数 pid 和 options。

pid 参数指示一个子进程的 ID，表示只关心这个子进程退出的 SIGCHLD 信号。如果 pid=-1 时，那么和 wait() 作用相同，都是关心所有子进程退出的 SIGCHLD 信号。

options 参数主要有 WNOHANG 和 WUNTRACED 两个选项，WNOHANG 可以使 waitpid() 调用变成非阻塞的，也就是说它会立即返回，父进程可以继续执行其它任务。

## 孤儿进程

一个父进程退出，而它的一个或多个子进程还在运行，那么这些子进程将成为孤儿进程。

孤儿进程将被 init 进程（进程号为 1）所收养，并由 init 进程对它们完成状态收集工作。

由于孤儿进程会被 init 进程收养，所以孤儿进程不会对系统造成危害。

## 僵尸进程

一个子进程的进程描述符在子进程退出时不会释放，只有当父进程通过 wait() 或 waitpid() 获取了子进程信息后才会释放。如果子进程退出，而父进程并没有调用 wait() 或 waitpid()，那么子进程的进程描述符仍然保存在系统中，这种进程称之为僵尸进程。

僵尸进程通过 ps 命令显示出来的状态为 Z（zombie）。

系统所能使用的进程号是有限的，如果产生大量僵尸进程，将因为没有可用的进程号而导致系统不能产生新的进程。

要消灭系统中大量的僵尸进程，只需要将其父进程杀死，此时僵尸进程就会变成孤儿进程，从而被 init 所收养，这样 init 就会释放所有的僵尸进程所占有的资源，从而结束僵尸进程。





# 参考文章

- [理解 Linux 的硬链接与软链接](https://www.ibm.com/developerworks/cn/linux/l-cn-hardandsymb-links/index.html)
