## Shell概述

shell是一个命令行解释器，它接收应用程序/用户命令，然后调用操作系统内核



#### 开头

```bash
#  指定解析器
#!/bin/bash
```





#### 执行方式

```bash
#  方法1，由bash解析器执行脚本，所以脚本本身不需要执行权限
bash helloworld.sh

#  方法2，直接执行，使用脚本的相对路径或绝对路径，需要脚本的x权限
./helloworld.sh  # 相对路径
#  为脚本添加 x 权限
chmod +x helloworld.sh
```





#### 变量的定义及使用

系统变量

```bash
$HOME  # home路径，例如：/home/byakuya
$PWD   # 当前路径
$SHELL # shell解析器的位置，一般为头文件的 /bin/bash
$USER  # 当前user的名字
```

自定义变量

```bash
#  变量名=值，=两边不能有空格，否则解析器会把变量名当做命令执行
a=10
b="helloworld"  #  如果字符串中没有空格或特殊字符，可以不使用双引号
c=(1,2,3)       #  数组
d=$a            #  与a相同
e=$(echo a)     #  与d相同

#  撤销变量
#  unset 变量名
unset a

#  输出变量 
#  echo $变量名
echo $b  #  输出 helloworld
```

特殊变量

```bash
#  $n
#  $0 代表脚本本身，$1~$n代表当前脚本的参数

#  脚本内：
echo "$0 $1 $2 $3"

#  执行：
bash test.sh 1 hello world
#  输出：
test.sh 1 hello world  #  $0代表脚本名，$1~$3分别代表后面的三个参数：“1”，“hello”，“world”
#  如果以相路径经或绝对路径执行，则$0会输出执行时的使用的相对路径或绝对路径
```

```bash
#  $#
#  输出脚本传入参数的个数

#  脚本内：
echo "$#"

#  执行：
bash test.sh 1 hello world
#  输出：
3  #  该脚本输入了3个参数
```

```bash
#  $*
#  传入的所有参数，将其当做一个整体输出

#  脚本内：
echo "$*"

#  执行：
bash test.sh 1 hello world
#  输出：
1 hello world  # 是一个整体
```

```bash
#  $@
#  传入的所有参数，将每个参数单独处理

#  脚本内：
echo "$*"

#  执行：
bash test.sh 1 hello world
#  输出：
1 hello world  #  三个参数是单独存在的
```

```bash
#  $?
#  返回最后一次执行命令的状态，执行成功返回0
```





#### 运算符

```bash
#  方法1： $((运算式)) 或 $[]
#  方法2： expr + - * / %  加减乘除取余

#  方法1
a=$[3*4%5]
a=$((3*4%5))  #  两者等价
echo $a

2  #  输出2


#  方法2
expr 1 + 1  #  运算符两边需要有空格
2  #  输出2

expr `expr 1 + 1` / 2
1  #  先计算+，后计算/，结果为2

a=10
b=20
expr $a + $b  #  输出30
c=$[$a + $b]  #  c的值为30
c=$a + $b  #  c的值为字符串，"10+20"
```





#### 数组

```bash
#  创建数组
arr=("hello" "world")
echo ${a[0]}  #  输出 hello
echo ${a[1]}  #  输出 world
```





#### 条件判断

```bash
#  [ 条件 ]
#  [ 20 -gt 10 ]  []中间有空格
```

常用条件：

- `-lt`    （less than）小于
- `-le`    （less equal）小于等于
- `-gt`    （greater than）大于
- `-ge`    （greater equal）大于等于
- `-eq`    （equal）等于
- `-ne`    （not equal）不等于

##### if语句

```bash
#  判断输入的第一个是否大于10
#  if 和 elif 后应该有then，else 后面不需要。最后写fi
if [ $1 -gt 10 ]
then
        echo "输入的值大于10"
elif [ $1 -eq 10 ]
then
        echo "输入的值等于10"
else
        echo "输入的值小于10"
fi
```

##### case语句

```bash
case $1 in
1)
	echo "输入值为1"
;;
2)
	echo "输入值为2"
;;
*)
	echo "未知输入"
;;
esac
```

##### for循环

```bash
for((i=0;i<10;i++))
do
	echo $i
done
```

```bash
for i in $*
do
	echo $i
done
```

##### while循环

```bash
s=0
i=1
while [ $i -le 100 ]
do
	s=$[$s + $i]
	#  或  ((s+=i))
	i=$[$i + 1]
	#  或  ((i++))
done
echo $s
```





#### 自定义函数

```bash
# 定义函数，计算从1到num的累加结果
calculate_sum() {
    local num=$1  # 接收参数num，local声明局部变量，不影响函数外部的同名变量
    local sum=0   # 初始化累加结果为0

    # 使用for循环计算累加结果
    for ((i=1; i<=num; i++)); do
        ((sum += i))
    done

    # 返回累加结果
    echo $sum
}

# 调用函数并传递参数
result=$(calculate_sum 5)  # 计算从1到5的累加结果
echo "Sum is: $result"    # 输出: Sum is: 15
```

































































