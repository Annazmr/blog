# 常见目录说明
/bin： 存放二进制可执行文件(ls,cat,mkdir等)，常用命令一般都在这里；

/etc： 存放系统管理和配置文件；

/home： 存放所有用户文件的根目录，是用户主目录的基点，比如用户user的主目录就是/home/user，可以用~user表示；

/usr： 用于存放系统应用程序；

/opt： 额外安装的可选应用程序包所放置的位置。一般情况下，我们可以把tomcat等都安装到这里；

/proc： 虚拟文件系统目录，是系统内存的映射。可直接访问这个目录来获取系统信息；

/root： 超级用户（系统管理员）的主目录（特权阶级o）；

/sbin: 存放二进制可执行文件，只有root才能访问。这里存放的是系统管理员使用的系统级别的管理命令和程序。如ifconfig等；

/dev： 用于存放设备文件；

/mnt： 系统管理员安装临时文件系统的安装点，系统提供这个目录是让用户临时挂载其他的文件系统；

/boot： 存放用于系统引导时使用的各种文件；

/lib ： 存放着和系统运行相关的库文件 ；

/tmp：  用于存放各种临时文件，是公用的临时文件存储点；

/var： 用于存放运行时需要改变数据的文件，也是某些大文件的溢出区，比方说各种服务的日志文件（系统启动日志等。）等；

/lost+found： 这个目录平时是空的，系统非正常关机而留下“无家可归”的文件（windows下叫什么.chk）就在这里。

# 1  Linux基本命令

## 1.1 常用命令
1. pwd：查看当前路径

2. pwd -P：查看软链接的实际路径

3. **grep [option] pattern file|dir：全局正则表达式搜索**

    - 常用参数 [option]
    ```
    -A n --after-context显示匹配字符后n行
    -B n --before-context显示匹配字符前n行
    -C n --context 显示匹配字符前后n行
    -c --count 计算符合样式的列数
    -i 忽略大小写
    -l 只列出文件内容符合指定的样式的文件名称
    -f 从文件中读取关键词
    -n 显示匹配内容的所在文件中行数
    -R 递归查找文件夹
    ```
    - grep 的规则表达式 [pattern]
    ```
    ^  #锚定行的开始 如：'^grep'匹配所有以grep开头的行。
    $  #锚定行的结束 如：'grep$'匹配所有以grep结尾的行。
    .  #匹配一个非换行符的字符 如：'gr.p'匹配gr后接一个任意字符，然后是p。
    *  #匹配零个或多个先前字符 如：'*grep'匹配所有一个或多个空格后紧跟grep的行。
    .*   #一起用代表任意字符。
    []   #匹配一个指定范围内的字符，如'[Gg]rep'匹配Grep和grep。
    [^]  #匹配一个不在指定范围内的字符，如：'[^A-FH-Z]rep'匹配不包含A-R和T-Z的一个字母开头，紧跟rep的行。
    \(..\)  #标记匹配字符，如'\(love\)'，love被标记为1。
    \<      #锚定单词的开始，如:'\<grep'匹配包含以grep开头的单词的行。
    \>      #锚定单词的结束，如'grep\>'匹配包含以grep结尾的单词的行。
    x\{m\}  #重复字符x，m次，如：'0\{5\}'匹配包含5个o的行。
    x\{m,\}  #重复字符x,至少m次，如：'o\{5,\}'匹配至少有5个o的行。
    x\{m,n\}  #重复字符x，至少m次，不多于n次，如：'o\{5,10\}'匹配5--10个o的行。
    \w    #匹配文字和数字字符，也就是[A-Za-z0-9]，如：'G\w*p'匹配以G后跟零个或多个文字或数字字符，然后是p。
    \W    #\w的反置形式，匹配一个或多个非单词字符，如点号句号等。
    \b    #单词锁定符，如: '\bgrep\b'只匹配grep。
    ```
    - 示例
    ```
    查找指定进程：ps -ef | grep svn
    查找指定进程个数：ps -ef | grep svn -c
    从文件夹中递归查找以grep开头的行，并只列出文件：grep -lR '^grep' /tmp
    显示包含 ed 或者 at 字符的内容行：grep -E 'ed|at' test.txt
    ```

4. which：查找命令是否存在，以及命令的存放位置在哪儿，例如 which ls

5. whereis：只能用于搜索程序名，而且只搜索二进制文件（参数-b）、man说明文件（参数-m）和源代码文件（参数-s），例如 whereis vim

6. locate：查看文件所在的所有位置
    ```
    locate w2v_200.txt（显示整个服务器上w2v_200.txt的位置）
    locate /etc/m（搜索etc目录下(仅限当前目录)所有以m开头的文件的位置）
    ```
7. find：实际搜寻硬盘查询文件名称 [参考](https://www.cnblogs.com/tongyan2/p/5517085.html)
    ```
    按文件类型查找：find test1 -type d（d表示目录文件）
    按文件名查找：  find /home/mrzhang -name w2v_200.txt：查找/home/mrzhang目录下（包括子目录）所有w2v_200.txt的位置
    按文件属主查找：find test1 -user wangmengting
    ```

8. du [选项] [文件]：查看文件所占空间
    ```
    -a 显示目录中所有文件大小
    -k 以KB为单位显示文件大小
    -m 以MB为单位显示文件大小
    -g 以GB为单位显示文件大小
    -h 以易读方式显示文件大小
    -s 仅显示总计
    -c或--total  除了显示个别目录或文件的大小外，同时也显示所有目录或文件的总和
    ```


## 1.2 目录切换命令
cd usr：  切换到该目录下usr目录

cd ..： 切换到上一层目录

cd /：  切换到系统根目录

cd ~：  切换到用户主目录

cd -：  切换到上一个操作所在目录

## 1.3 权限命令

操作系统中每个文件都拥有特定的权限、所属用户和所属组。权限是操作系统用来限制资源访问的机制，在Linux中权限一般分为读(readable)、写(writable)和执行(excutable)，分为三组。分别对应文件的属主(owner)，属组(group)和其他用户(other)，通过这样的机制来限制哪些用户、哪些组可以对特定的文件进行什么样的操作。

通过 ls -l 命令可以查看某个目录下的文件或目录的权限
![1](https://github.com/Annazmr/Note/blob/master/%E5%B7%A5%E5%85%B7%E7%AC%94%E8%AE%B0/Pic/Linux1.png)

第一列内容的解释如下：
![2](https://github.com/Annazmr/Note/blob/master/%E5%B7%A5%E5%85%B7%E7%AC%94%E8%AE%B0/Pic/Linux2.png)

**文件类型**

d：目录；-：文件；｜：软链接

**权限**

r：可读，也可用4表示；w：可写，也可用2表示；x：可执行，也可用1表示

**修改文件/目录的权限的命令：chmod**
修改aaa.txt的权限为属主（u）有全部权限，属主所在的组（g）有读写权限，其他用户（o）只有读的权限
chmod u=rwx,g=rw,o=r aaa.txt

# 2 用户、目录、文件

## 2.1 用户

### 2.1.1 普通用户

1. 创建用户：useradd testuser

    创建/更改用户密码：passwd testuser

2. 删除用户：userdel testuser

    例：删除用户user2：userdel user2

    例：删除用户user3，同时删除他的工作目录：userdel –r user3

3. 修改用户：usermod testuser

    例：将用户 user1的登录名改为u1：usermod –l u1 user1

    例：将用户 user1 加入到 users组中：usermod –g users user1

    例：将用户 user1 目录改为/users/u1：usermod –d /users/u1 user1

4. 查看用户账号密码信息：passwd -S testuser
    id命令查看一个用户的UID和GID, 例：查看user4的id：id user4

5. passwd -d testuser：清除用户密码

使用useradd指令所建立的帐号，实际上是保存在/etc/passwd文本文件中。passwd命令用于设置用户的认证信息，包括用户密码、密码过期时间等。系统管理者则能用它管理系统用户的密码。只有管理者可以指定用户名称，一般用户只能变更自己的密码。

### 2.1.2 用户组

1. 创建GID为888的用户组users：groupadd –g 888 users

2. 添加用户user1到users用户组：gpasswd -a user1 users

3. 删除用户user1从users用户组：gpasswd –d user1 users

    删除组users：groupdel users

4. 修改组名user为users：groupmod –n user users

## 2.2 目录

1. 创建目录：mkdir 目录名称

2. 删除目录：rm -rf 目录名称

    -r 向下递归，删除子目录和文件

    -f 直接强行删除，没有提示

3. 修改目录名称：mv 目录名称 新目录名称（mv语法也可以对文件、压缩包重命名）

    剪切文件：mv 文件名/目录名 路径

4. 查找/home目录及子目录下所有以“.txt”结尾的文件和文件夹：find /home -name "*.txt"，若忽略大小写：find /home -iname "*.txt"

    查找当前目录及子目录下所有以“.txt”和“.pdf”结尾的文件和文件夹：find .\(name "*txt" -o -name "*.pdf")或 find . -name "*txt" -o -name "*.pdf"

5. 将dir1整个目录下文件复制/剪切到dir2目录：cp/mv -r dir1路径 dir2路径

    若考虑到dir2目录下可能存在同名目录，则可先询问是否覆盖（-i）：cp -ri A/B/* A1/B1/   （若不想看到提示直接覆盖使用-rf）

## 2.3 文件

1. 创建文件：touch 文件名

2. 删除文件：rm -rf 文件名

3. 修改文件：vim 文件名

    - **打开、保存、关闭文件(vi命令模式下使用)**

        ```
        vi filename       //打开filename文件
        :w       //保存文件
        :w vpser.net //保存至vpser.net文件
        :q          //退出编辑器，如果文件已修改请使用下面的命令
        :q!        //退出编辑器，且不保存
        :wq         //退出编辑器，且保存文件
        ```
    - **插入文本或行(vi命令模式下使用)**
        ```
        a      //在当前光标位置的右边添加文本
        i       //在当前光标位置的左边添加文本
        A     //在当前行的末尾位置添加文本
        I      //在当前行的开始处添加文本(非空字符的行首)
        O     //在当前行的上面新建一行
        o     //在当前行的下面新建一行
        R    //替换(覆盖)当前光标位置及后面的若干文本
        J    //合并光标所在行及下一行为一行(依然在命令模式)
        ```
    - **删除、恢复字符或行(vi命令模式下使用)**
        ```
        x         //删除当前字符
        nx         //删除从光标开始的n个字符
        dd      //删除当前行
        ndd   //向下删除当前行在内的n行
        u       //撤销上一步操作
        U      //撤销对当前行的所有操作
        ```
    - **搜索(vi命令模式下使用)**
        ```
        /vpser     //向光标下搜索vpser字符串
        ?vpser     //向光标上搜索vpser字符串
        n           //向下搜索前一个搜素动作
        N         //向上搜索前一个搜索动作
        ```
    - **复制、粘贴(vi命令模式下使用)**
        ```
        yy    //将当前行复制到缓存区
        nyy   //将当前行向下n行复制到缓冲区
        yw    //复制从光标开始到词尾的字符。
        nyw   //复制从光标开始的n个单词。
        y^      //复制从光标到行首的内容。
        y$      //复制从光标到行尾的内容。
        p        //粘贴剪切板里的内容在光标后
        P        //粘贴剪切板里的内容在光标前
        ```
    - **替换(vi命令模式下使用)**
        ```
        :s/old/new      //用new替换行中首次出现的old
        :s/old/new/g         //用new替换行中所有的old
        :n,m s/old/new/g     //用new替换从n到m行里所有的old
        :%s/old/new/g      //用new替换当前文件里所有的old
        ```
    - **设置行号(vi命令模式下使用)**
        ```
        :set  nu     //显示行号
        :set nonu    //取消显示行号
        ```
    - **移动光标(vi命令模式下使用)**
        ```
        Enter  移动到下一行首
        -  移动到上一行首
        ```

4. 查看文件：cat/more/less/tail 文件名称

    cat： 查看显示文件内容

    more： 可以显示百分比，回车可以向下一行， 空格可以向下一页，q可以退出查看

    less： 可以使用键盘上的PgUp和PgDn向上 和向下翻页，q结束查看

    tail -10 ： 查看文件的后10行

    命令 tail -f 文件名 可以对某个日志文件进行动态监控


5. **压缩文件**（打包压缩后的文件后缀名为.tar.gz）

    tar -zcvf 压缩后的文件名 要打包的文件

    其中：z：调用gzip压缩命令进行压缩；c：打包文件；v：显示运行过程；f：指定文件名
    ```
    test目录下有三个文件分别是 :aaa.txt bbb.txt ccc.txt,如果我们要打包test目录并指定压缩后的压缩包名称为test.tar.gz
    tar -zcvf test.tar.gz /test/
    ```

    **解压文件**
    tar -xvf 压缩文件（x：代表解压）
    ```
    将/test下的test.tar.gz解压到当前目录：tar -xvf test.tar.gz
    将/test下的test.tar.gz解压到根目录/usr下:tar -xvf xxx.tar.gz -C /usr（- C代表指定解压的位置）
    ```




