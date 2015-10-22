# 笨办法学 Python笔记

复习22课之前的命令

print 打印

\# 注释

" '双引号和单引号

""" 打印并换行

\\n 换行

\\ 转义符,前置被转义字符前

###运算符
\+ 加号

\- 减号

/ 除

\* 乘

% 百分号  ?

< 小于号

\> 大于号

<= 小于等于

\>= 大于等于



###格式化字符

%s  (采用str()的显示)：显示应该显示的内容，比如\n，显示换行,打印出来没有单引号yes

%r  (采用repr()的显示)：显示输入的内容，\n显示\n  , 打印出来有单引号’yes’

%d  十进制整数


```
y = 10

x = "There are %d types of people." % y 
```
```
x = mary
y = jerry

print "%s like the girl, %s . % (x, y)
```
###输入脚本

raw_input()   输入,括号内填写输入时的提示语

导入并解包变量, 输入方式

```
from sys import argv 

script, first, second, third = argv

```
验证文件是否存在脚本, 如果存在 True, 不存在false


```
from os.path improt exists

print "Does the output file exist? %r" % exists( filename)
```

###读取脚本
open(filename) 括号中放要读取的文件名

open(filename. 'W') 打开文件并允许写入

filename.read() 读文件, 与 open 配合使用

filename.close() 关闭打开的文件

 filename.truncate 清空文件,小心使用

filename.write(要写入的内容) 与 open 有写入权限的命令配合

filename.seek() 查找

rewind(filename)

writeline() 是输出后换行，下次写会在下一行写

write()是输出后光标在行末不会换行，下次写会接着这行写

###其他脚本
cat test.txt 显示文档内容


###函数
 注意冒号,第二行缩进四个空格
```
def text1(x, y):
    print x, y
    
a = 你好
b = jerry
text1(a, b)

结果: 你好, jerry

```

return 返回计算数值,在 def 函数中使用, 
可以对结果进行引用


```
def add(a, b)
    print "adding %d + %d" % (a, b)
    return a + b
    
A = add(1, 2)

print A
结果:3
```

