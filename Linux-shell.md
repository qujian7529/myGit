## 格式
1.指定解释器 #！/bin/bash

2.脚本开头加版权等信息如：#DATE:时间，#author(作者)#mail：邮箱，#function（功能），#Version：版本

3.脚本注释（用英文注释 中文可能乱码。）

4.脚本以.sh结尾 不是必须的

5.成对的符号，一次性写全，退格补内容。特殊符号[ xxxx ] 中括号中间内容两边都有空格。

6 .代码有条理性（通过缩进）

## 变量与操作
支持　&& || ! ,支持 ++、--,+= /= 等复合语句,支持位运算

    v=""
    echo "$v"

对空格要求严格
基本操作

    a="10"
    b=3
    ret=`expr $a + $b`
    ret=`expr $a % $b`

expr实现算数操作

    ret=`expr $a + $b`
    ret=`expr $a % $b`
    ret=`expr $a \* $b`

let实现操作
    
    let "ret= a + b"
    let "ret= a ** b"
    let "a = a << 2"
    let "a /= b"
    let "a++"
    
