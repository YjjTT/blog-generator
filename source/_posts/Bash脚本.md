---
title: Bash脚本
date: 2019-01-03 13:13:34
tags: Bash, Script
---

### 脚本

> 脚本语言 (Scripting language), 例如JavaScript是一门动态类型, 面向对象的脚本语言.一个脚本通常是解释运行而非编译.

### 写一个脚本

**注意以下命令行的注释都不要写**

1. 在Desktop新建一个文件夹local, 然后cd到local创建一个文件demo.txt

```shell
mkdir local
cd local/  #一定要运行这个命令
touch demo.txt
```

1. 编辑demo.txt, 内容如下:

```shell
pwd #确认下当前路径, /Users/yjjtt/Desktop/local
vi demo.txt 或者直接open demo.txt 进行编辑demo.txt
在里面输入图中的五行命令,然后保存
```

![](https://user-gold-cdn.xitu.io/2018/12/10/1679857648d83231?w=1128&h=212&f=png&s=18196)

1. (windows用户可以跳过这一步) 给demo.txt 添加执行权限 `chmod +x demo.txt`,如果不执行这一步,则无法运行此脚本,会提示permission denied: demo.txt
2. 如果觉得demo.txt的txt后缀看着别扭,也可以去掉`mv demo.txt demo`这样执行 `sh ~/Desktop/local/demo`就可以了

```shell
mv demo.txt demo
sh ~/Desktop/local/demo
```

1. 如果觉得执行`sh ~/Desktop/local/demo`还是很麻烦, 可以将~/Desktop/local加到PATH里

- 临时设置PATH

```shell
pwd #查看下loacl所在的绝对路径
export PATH="local的绝对路径:$PATH" # 这句话就是将local目录加到PATH里
```

![](https://user-gold-cdn.xitu.io/2018/12/10/167985764950aead?w=1130&h=298&f=png&s=45235)

- 永久设置PATH, 上面的PATH在重启Bash后就会失效

```shell
touch ~/.bashrc # 创建~/.bashrc
vi ~/.bashrc # 编辑~/.bashrc
在编辑器里写入 export PATH="local的绝对路径:$PATH"
source ~/.bashrc # 保存编辑,这句命令一定要写
demo # 运行demo
```

### PATH

1. PATH的作用就是每次在Bash里面输入一个命令时, Bash都会去PATH列表里面去找对应的文件,找到了就执行, 脚本其实就是一个可执行的文件(ls, cd, mkdir..)
2. 可以输入命令`echo $PATH`查看所有的路径,Bash就会在这些路径中依次查找
3. `type demo`可以查看查找过程
4. `which demo`可以看到查找结果

### 给脚本加个参数

上面的脚本demo只能创建一个demo的目录, 现在来让目录名是可变的.

```shell
vi demo # 编辑脚本
mkdir $1 # 将demo换成$1, $1就表示你传的第一个参数(目录名), 第二个参数就是$2,以此类推
cd $1 
mkdir css js
touch index.html css/style.css js/main.js
exit
# 同样是五行命令
```

上面编辑完保存后, 直接demo xxx 就会创建一个名叫xxx的目录

### 判断目录是否存在

编辑demo, 注意下面的Bash脚本, 一个空格也不能多,一个也不能少

```shell
if [ -d $1 ]; then # 如果目录存在
	echo 'error: dir exists'
	exit 1 # 返回值1 代表错误代码为1 
else
    mkdir $1
    cd $1 
    mkdir css js
    touch index.html css/style.css js/main.js
    echo 'success'
    exit 0 # 返回值0 代表成功
fi
```