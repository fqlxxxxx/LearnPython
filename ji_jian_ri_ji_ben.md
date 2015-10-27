# 极简日记本

##思路：
* 新建文件
* 输入内容
* 写入内容
* 循环输入
* 退出循环条件
* 退出确认
* 再次启动，检查文件名是否存在
* 不存在，添加日记到新文件中
* 存在，打印历史日记内容
* 然后，在存在的日记文件中追加内容

##细节：
* txt中一次输入写入一行，再次输入另起一行
* 每次纪录的日记自动生成日期和时间
* qiut命令不能写入到txt中

##技术要点：
* import exites ，datetime ，argv
* raw_input
* whlie
* if
* f.write(content)
* F.Read(c,"a")
* Open(file)
* Exites()
* Break
* Continue 
* Print

##遇到的难点：
* 需求不明确，走偏了
* 还没有看到while if break contiune，笨办法22课以后出现的
* 日期时间如何获取
* 时间如何用write写入到txt？write只接受字符串
* 写入txt的日记自动换行
* quit命令也写入到txt中了。代码顺序问题
* 确认时输入大写和小写n、y都应该可以。尝试用or连接，不可用，暂未解决。
* 多层嵌套的逻辑混乱。对循环还不熟悉。


##需要改进的问题：
* if冒号
* if第二行缩进
