#### 参考



#### vim程序编辑器

#### 变量

环境变量是全局变量，用户自定义变量是局部变量。

变量命名规则
1.变量名必须以字母或下划线打头，名字中间只能由字母、数字和下划线组成。
2.变量名的长度不得超过255个字符
3.变量名在有效范围内必须是唯一的
4.在Bash中，变量的默认类型都是字符串型
用户自定义变量
变量名=变量值（“=”等号前后不可以有空格）
set  #查看系统下的变量（包括环境变量和用户自定义变量）
   -u  #如果设定些选项，调用未声明变量时会报错（默认无任何提示）
unset 变量名   #删除变量


查阅环境变量的命令:env,export,set

##### 用env查看的环境变量

变量|描述
---|---
HOME|代表用户的主文件夹
SHELL|当前环境使用的shell是哪个程序，默认使用/bin/bash
HISTSIZE|记录历史命令的条数
MAIL|使用mail命令收信时系统读取的邮件信箱文件
PATH|执行文件查找的路径，目录与目录之间以(:)分隔，由于文件的查找是依序由PATH的变量内的目录来查询，所以目录的顺序很重要。
LANG|语系数据，很重要。如启动某些Perl程序语言文件时，它会主动去分析语系数据文件，如果发现有它无法解析的编码语系，可能会产生错误。
HOSTNAME|主机名
TERM|终端环境
SSH_CLIENT|当前操作环境是用ssh连接的，这里记录客户端ip
SSH_TTY|ssh连接的终端时pts/1
USER|当前登录的用户

RANDOM-随机数变量

随机数文件/dev/random相关的变量。BASH环境下执行"echo $RANDOM"，随机取出一个介于0~32767的数值。

```shell
#随机取出0~9之间的数值
#declare -i：将变量声明为整数型（integer）
[root@localhost ~]#declare -i number=$RANDOM*10/32767; echo $number
4
[root@localhost ~]#
```

##### 用set查看所有变量（含环境变量与）

bash中包含环境变量与bash操作接口相关的变量，以及用户自己定义的变量。set除了环境变量之外，还会将其他变量全部显示出来。

一般来说，不论是否为环境变量，只要跟我们目前这个shell的操作接口有关的变量，通常都是会被设置为大写字符，也就是说，基本上，在Linux默认的情况中，使用{大写字母}来设置的变量一般为系统内定需要的变量。

PS1变量-命令提示符设置

符号|意义
---|---
\d|显示日期，格式为"星期 月 日",如"Mon Feb 2"
\H|显示完整的主机名。如默认主机名"localhost.localdomain"
\h|显示主机名在第一个小数点之前的名字
\t|显示24小时制时间，格式为"HH:MM:SS"
\T|显示12小时制时间，格式为"HH:MM:SS"
\A|显示24小时制时间，格式为"HH:MM"
\@|显示12小时制时间，格式为"am/pm"样式
\u|显示当前用户名
\v|BASH的版本信息
\w|显示当前所在目录的完整名称，由根目录写起，但主文件夹会以~代替
\W|利用basename函数取得工作目录名称，显示当前所在目录的最后一个目录
\#|执行的第几个命令
\$|提示符。如果是root用户会显示提示符为"#"，如果是普通用户会显示提示符为"$"

$-本shell的PID

$本身也是变量。代表的是目前这个shell的线程代号，即所谓的PID(Process ID)。使用"echo $$"，查看PID号码。

?-上个执行命令的回传码

当我们执行某些命令时，这些命令都会回传一个执行后的代码。一般来说，如果成功执行该命令，则会回传一个0值；如果错误，一般是以非0的数值来代替

##### export自定义变量转成环境变量

子进程仅会继承父进程的环境变量，不会继承父进程的自定义变量，所以原本bash中的自定义变量在进入子进程后就会消失不见，一直到离开子进程并回到原本的父进程后，这个变量才会出现。

```shell
[root@localhost ~]#export
declare -x CLASS_PATH="./:/usr/java/default/lib"
declare -x HISTCONTROL="ignoredups"
declare -x HISTSIZE="1000"
declare -x HOME="/root"
declare -x JAVA_HOME="/usr/java/default"
declare -x LANG="zh_CN.UTF-8"
declare -x LESSOPEN="||/usr/bin/lesspipe.sh %s"
declare -x LOGNAME="root"
declare -x MAIL="/var/spool/mail/root"
declare -x PATH="/usr/java/default/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin"
declare -x PS1="[\\u@\\t \\W]\\\$"
declare -x PWD="/root"
declare -x SHELL="/bin/bash"
declare -x SSH_TTY="/dev/pts/0"
declare -x TERM="xterm-color"
declare -x USER="root"
#省略若干...

#设置变量
[root@localhost ~]# export 变量名=变量值
[root@localhost ~]# 变量名=变量值; export 变量名
```

##### 变量的有效范围

理论上：

- 当启动一个shell，操作系统会分配一记忆块给shell使用，此内存的变量可让子进程取用。

- 若在父进程利用export功能，可以让自定义变量的内容写到上述的记忆块中（环境变量）。

- 当加载另一个shell时（即启动子进程，而离开原本的父进程），子shell可以将父shell的环境变量所在的记忆块导入自己的环境变量块当中。

**这里的"环境变量"与"bash的操作环境"意思不太一样，举例来说，PS1并不是环境变量，但是这个PS1会影响到bash的接口(提示符)。**

```shell
#做过以下测试，上句大概是这个意思？？？

[root@00:09:39 test]#echo $PS1
[\u@\t \W]\$
[root@00:09:43 test]#
[root@00:09:43 test]#cat ps1_test.sh 
#!/usr/bin/bash

echo $PS1

if [ "$PS1" ];then
   echo 'true'
else 
   echo 'false'
fi

[root@00:09:48 test]#
[root@00:09:49 test]#./ps1_test.sh 

false
[root@00:10:01 test]#
[root@00:10:02 test]#source ps1_test.sh 
[\u@\t \W]\$
true
[root@00:10:06 test]#
```

3.删除环境变量：
unset 变量名
变量可以自定义，但是对系统生效的环境变量名和变量作用是固定的





locale   #查询当前系统语系
-- LANG ：定义系统主语系的变量
--LC_ALL：定义整体语系的变量
locale -a | more    #  查看Linux支持的所有语系
cat   /etc/sysconfig/i18n   #系统默认语系
位置参数变量
位置参数变量	作用
$n	n为数字，$0代表命令本身，$1-$9代表第一到第九个参数，十以上的参数需要用大括号包含，如${10}。
$*	这个变量代表命令行中所有的参数，$*把所有的参数看成一个整体
$@	这个变量代表命令行中所有的参数，不过$@把每个参数区别对待
$#	这个变量代表命令行中所有参数的个数

预定义变量
预定义变量	作用
$?	最后一次执行的命令的返回状态。如果这个变量的值为0，证明上一个命令正确执行;如果这个变量的值为非0（具体是哪个数，由命令自己来决定），则证明上一个命令执行不正确。
$$	当前进程的进程号（PID）
$!	后台运行的最后一个进程的进程号（PID）

read
read  [选项]  [变量名]
接受键盘输入

-选项：
    -p “提示信息”：在等待read输入时，输出提示信息。
-t   秒数：read命令会一直等待用户输入，使用此选项可以指定等待时间。
-n   字符数 ：read命令只接受指定的字符数，就会执行
-s   隐藏输入的数据，适用于机密信息的输入




#### Bash Shell的操作环境

#####环境配置文件

环境变量配置文件中主要是定义对系统操作环境生效的默认环境变量，如PATH等。正是这些配置文件的存在，让bash在启动时直接读取这些配置文件，以规划好bash的操作环境。
而这些配置文件又可以分为全体系统的配置文件以及用户个人偏好配置文件。

```shell
#修改配置文件后，必须注销重新登录才能生效，而以下命令可使配置文件立即生效。
#source或小数点(.)都可以将配置文件的内容读进目前的shell环境中。

[root@localhost ~]# source  配置文件
或
[root@localhost ~]# .  配置文件

```

**可以编写不同的环境变量配置文件方案，通过执行"source 变量文件"来切换工作环境的环境变量。**

主要的环境变量文件

- /etc/profile

每个用户登录取得bash时一定会读取的配置文件，如果想要对所有用户设置整体环境，那就是在这个文件修改。这个文件设置的变量主要有：

变量名|描述
---|---
PATH|依据UID决定PATH变量要不要含有sbin的系统命令目录
MAIL|依据账户设置好用户的mailbox到/var/spool/mail/账号名
USER|根据用户的账号设置此变量内容
HOSTNAME|依据主机的hostname命令决定此变量内容
HISTSIZE|历史命令记录条数

bash的login shell情况下所读取的整体环境配置文件其实只有/etc/profile，但是/etc/profile还会调用其他的配置文件。

- /etc/inputrc

- /etc/profile.d/*sh

这是个目录内的众多文件。只要在/etc/profile.d/这个目录内且扩展名为.sh，另外用户能够具有r的权限，那么该文件就会被/etc/profile调用。在CentOS 5.x中，这个目录下面的文件规定了bash操作接口的颜色、
语系、ll与ls命令的命令别名、vi的命令别名、which的命令别名等。如果你需要帮所有用户设置一些共享的命令别名时，可以在这个目录下自行创建扩展名为.sh的文件，并将所需要的数据写入即可。

- /etc/sysconfig/i18n

这个文件是由/etc/profile.d/lang.sh调用的。这也是bash默认使用何种语系的重要配置文件。文件里最重要的就是LANG这个变量的设置。

- ~/.bash_profile

bash在读完整体环境设置的/etc/profile并借此调用其他配置文件后，接下来则是会读取用户的个人配置文件。在login shell的bash环境中，所读取的个人偏好配置文件其实主要有三个，依序分别是：

1. ~/.bash_profile

2. ~/.bash_login

3. ~/.profile

其实bash的login shell设置只会读取上面三个文件中的其中一个，而读取的顺序则是按照上面的顺序。如果~/.bash\_profile存在，其他两个文件不会被读取；如果~/.bash\_profile不存在才会读取~/.bash\_login，而前两者都不存在才会读取~/.profile

- ~/.bashrc

non-login shell会读

- /etc/bashrc

1. 依据不同的UID规定umask的值

2. 依据不同的UID规定提示符（就是PS1变量）

3. 调用/etc/profile.d/*.sh的设置

/etc/bashrc是CentOS特有的（其实是 Red Hat 系统特有的），其他不同的distributions可能会放置不同的文件名就是了。

由于这个~/.bashrc会调用/etc/bashrc及/etc/profile.d/*.sh，所以万一没有~/.bashrc，bash提示符就会变成:

>-bash-3.2$

这是因为没有调用/etc/bashrc来规定PS1变量，这种情况不会影响bash的使用。这时可以复制/etc/skel/.bashrc到主文件夹~/.bashrc，再修改一下你想要的内容，执行source ~/.bashrc，命令提示符就会回来了。

登录shell：作为Linux用户登录到Linux操作系统,或者用su - username切换到其他用户，都为登录shell，环境变量也同时切换。

非登录shell，用su username，即为非登录shell，环境变量仍为当前用户的环境变量。

根据是否为登录shell，读取环境变量配置文件是不同的。

登录shell读取环境变量顺序：

![](http://olke8cow1.bkt.clouddn.com/Shell_20170510004312.png)

实线的方向是主线流程，虚线的方向则是被调用的配置文件。有背景色部分也是非登录shell读取环境变量顺序。

其他环境变量文件
./bash_history
./bash_logout
/etc/man.config
/etc/issue
/etc/issue.net
1.转义符在/etc/issue.net文件中不能使用 
2.是否显示欢迎信息，由ssh的配置文件/etc/ssh/sshd_config决定，加入“Banner 	/etc/issue.net”行才能显示（记得重启SSH服务）
/etc/motd



运算符
declare
  declare声明变量类型，格式：
  declear  [+/-]  [选项]  变量名
  -：给变量设定类型属性
  +：取消变量的类型属性
  -a：将变量声明为数组型
    $ movie[0]=zp
    $ movie[1]=tp
    $ declare -a movie[2]=live
    $ echo ${movie}
    $ zp
    $ echo ${movie[2]}
    $ live
    $ echo ${movie[*]}
    $ zp tp live
  -i：将变量声明为整数型（integer）
    $  aa=11
    $  bb=22
    $  declare  -i  cc=$aa+$bb  (不声明结果为11+22)
    $  echo $cc
    $  33
   -x：将变量声明为环境变量
    $ declare  -x  test=123
    # 和export作用相似，但其实是declare 命令的作用
   -r：将变量声明为只读变量
    # 只读属性会让变量不能修改，不能删除，甚至不能取消只读属性
   -p：显示指定变量的被声明的类型
    $ declare  -p
    # 查询所有变量的属性
    $ declare  -p  变量名
    # 查询指定变量的属性


### Oh My ZSH

#### Install zsh and set up zsh as default 

1. yum install zsh 

2. Verify installation by running zsh --version. Expected result: zsh 4.3.9 or more recent.

3. Make it your default shell: chsh -s $(which zsh)