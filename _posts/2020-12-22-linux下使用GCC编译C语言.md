---
title:  linux下使用GCC编译C语言
date: 2020-12-22 23:31:06
categories:
- GCC
tags:
- GCC
---


# 1.GCC

## 1.1 查看GCC版本

```
cc -v
```

## 1.2 编译c语言文件

```
cc main.c #不指定输出文件
cc main.c -o main.out    #指定到输出文件
```

### 同时编译多个文件

多个程序一起编译，使主函数能够调用其他文件中的函数。

如max.c中包含int max(int a , int b)，在main中无需定义可直接使用，且不需要再头文件中声明包含max.c文件

```
cc max.c main.c -o main.out
```



## 1.3 先编译文件

效果与前文一样，但是提前编译好，其他文件可以提高编译的速度

```
cc -c max.c -o max.o       #先将文件编译成二进制文件
cc max.o main.c -o main.out     #
```

## 1.4 生成并执行

```
cc main.c -o main.out && ./main.out
```

## 1.5查看执行返回结果

```
echo $?          #返回0表示正常执行，返回表示程序错误
```



# 2.管道流

```
stdin  #输入文件
stdout  #输出文件
stderr  #错误文件
```

```
fprintf(stdout,"cotent");     #等价于
printf("cotent");
```

```
fscanf(stdin,"input");        #等价于
scanf("%d",&input);
```

```
fprintf(stderr,"error");
```

# 3.重定向

```
./a.out >> a.txt             #向文件a.txt中追加输出内容
./a.out > a.txt              #覆盖文件内容
./a.out < input.txt           #从文件向程序输入内容
./a.out 1 >> a.txt 2>>f.txt
```

```
ls /etc/ | grep ab
```

# 4.makefile

4.1 查看版本

```
make -v
vi Makefile    #兴建文件，注意名字不能改
```

4.2 编写Makefile文件

```
main.out:max.o main.c
		gcc max.o main.c -o main.out
		#gcc max.o main.c     #效果一样
max.o:max.c
		gcc -c max.c -o max.o   #编译为二进制文件，无法执行
		
```

4.3 执行

```
make
```

