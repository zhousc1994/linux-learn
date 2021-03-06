# vim编辑器
## 1.vim的三种模式
    命令模式：  默认模式                 
    编辑模式：  a,i,o键进入输入模式
        a:  在光标后一个字符追加
        i:  光标不变
        o:  新开一行增加内容
    末行模式：   ：进入

## 2.命令模式常用操作
### 1）复制、移动删除文件内容
    yy: 复制光标所在行
    nyy: 复制光标所在行开始向下的N行
    dd:  剪切光标所在行
    ndd:  剪切光标所在行向下N行
    p(小)：粘贴到光标所在行的下面
    P(大)：粘贴到光标所在行的上面
    
    D：删除光标所在行
    dG:删除光标所在行到末尾行所有
    
### 2）撤销和重复执行操作
    u: 撤销上次操作
    nu: 撤销n次操作
    ctrl+r: 撤销刚刚所撤销的那个操作
### 3）跳转相关操作
    nG: 跳转到第n行
    G：跳转最后一行
    
    0，^：跳转行首      home
    $   : 跳转行尾      end
    
    ctrl+f： 向下翻屏    pg up
    ctrl+b:  向上翻屏    pg down
### 4)替换相关操作
    r: 替换一个字符 R：替换模式
### 5）查找
    /string   在文件中搜索
    n         正向查找
    N         反向查找
    
## 3.末行模式下的常用操作
 

### 1）.第一类命令：行号

    set nu：显示行号
    
    set nonu：关闭行号

 

### 2).第二类命令：跳转

    num：直接跳转到第num行
    
    $：直接跳转到最后一行

 

### 3).第三类命令：取消匹配到的内容的高亮

    nohl

 

### 4).第四类命令：替换

    start,end s/原始内容/替换内容/g

    （分隔符不一定是/，只要是三个相同的符号即可）

**注意：**
    
    如果不用g，那么仅仅会替换每行的第一个找到的对象
    
    如果使用g，那么会将范围内所有找到的对象全部做替换
 
**示例**
    
    例子：将文件中全部的echo替换为bajie
    
    :1,$ s/echo/bajie/g
    
    或
    
    :% s/echo/bajie/g
    
    例子：将文件的50-100行行首添加一个#
    
    :50,100 s/^/#/g
    
    例子：将全部行首的#删除
    
    :1,$ s/^#//g
    
    例子：在1-5行的末尾添加一个#
    
    :1,5 s/$/#/g
    
    例子：将文件中全部的/替换为+
    
    :% s@/@+@g
    
    补充1：
    
    ^：表示行首
    
    $：表示行位
### 5）.保存和退出
    
    w：执行保存操作（保存到原始文件中）
    
    w /path/to/file：实现文件另存为
    
### 6）.高级操作

    r /path/to/file：将file中的内容导入到当前文件中
    
    set tabstop=4：将tab缩进的字符数设置为4个
    
    set ai：设置自动缩进
    
    set noai：取消自动缩进
    
### 7）.复制、移动、删除多行的操作

    start,end d：删除多行
    
    start,end m dest：将多行移动到指定行的下面
    
    start,end co dest：将多个复制到指定行的下面
    
## 4.分屏操作

    vim -o file1 file2：实现水平分屏
    
    vim -O file1 file2: 实现垂直分屏
    
    ctrl+w：切换到另一个分屏
    
## 5.vi的配置文件
 

    /etc/vimrc：全局配置文件，在这个文件中做的配置，会对所有用户生效
    
    ~/.vimrc：(默认不存在，需要自己手动创建)用户配置文件，仅仅对当前用户生效
    
     
    
    1. 编辑vi的配置文件，实现可以自动显示行号、缩进4个字符、自动对齐
    
    # vi ~/.vimrc
    
    :set nu
    
    :set ai

    :set tabstop=4
## 6.vi崩溃缓存机制
    用vim编辑一个文件的是，如果文件没有正常的关闭（wq、q、q!），那么就会生成一个崩溃缓存文件
    
    崩溃缓存文件的和作用
    
    1. 缓存文件是隐藏文件
    
    2. 缓存文件基本格式是 .file.swp
    
    3. 缓存文件的作用是用于在系统意外关机的情况下，恢复文件中的内容（修改了文件内容，意外关掉终端或者系统）
    
    4. 缓存文件的使用方式
    
    第一步：# vim -r file
    
    第二步：保存退出
    
    第三步：删除缓存文件