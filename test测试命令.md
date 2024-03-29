# *shell脚本的test测试指令*
## 1. test指令的作用
* Shell中的 test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。可以通是否要过&&以及||来作为前一个指令执行回传只对于后一个指令是否要进行的重要依据。
* 测试类型有三种：
	1. 数值测试		
		
		参数说明：
		
			-eq	---	 等于则为真
			-ne	---	 不等于则为真
			-gt	---	 大于则为真
			-ge	---	 大于等于则为真
			-lt	---	 小于则为真
			-le	---	 小于等于则为真
			
		实例演示：
		
			#!/bin/bash

			var=123
		    var1=234
			test $var -eq $var1 && echo "var等于var1" || echo "var不等于var1"   --将&& ||与test连用，如果test指令的返回结果为真，则执行“||”前面的语句，反之，则执行后面的语句
		
		演示结果：
		
			var不等于var1

	2. 字符串测试
	
		参数说明：
			
	 		= 	---	 等于则为真
			!=	---	 不相等则为真
			-z  ---	 字符串的长度为零则为真
			-n  ---	 字符串的长度不为零则为真

	3. 文件测试

		参数说明：

			-e 文件名	---  如果文件存在则为真
			-r 文件名	---	 如果文件存在且可读则为真
			-w 文件名	---	 如果文件存在且可写则为真
			-x 文件名	---	 如果文件存在且可执行则为真
			-s 文件名	---	 如果文件存在且至少有一个字符则为真
			-d 文件名	---	 如果文件存在且为目录则为真
			-f 文件名	---	 如果文件存在且为普通文件则为真
			-c 文件名	---	 如果文件存在且为字符型特殊文件则为真
			-b 文件名	---	 如果文件存在且为块特殊文件则为真
		多重条件判定
			
			-a  ---  （and）两状况同时成立。例：test -r file -a -x file 则file同时具有r与x权限时，才回传true
			-o	---   (or) 两状况成立任何一个
			！  ---    反相状态	

		实例演示：
			
			#!/bin/bash

			#1. 让使用者输入文档名称，并且判断使用者是否真的输入字符串？
			echo -e "Please input a filename. \n\n"
			read -p "Input a filename:" filename
			test -z ${filename} && echo "You MUST input a filename." && exit 0
			
			#2. 判断文件是否存在？若文件不存在则显示讯息并结束脚本
			test  ! -e ${filename} && echo "The filename '${filename}' DO NOT exist" && exit 0
			
			#3. 开始判断文件类型与属性
			test -f ${filename} && filetype="regulare file"
			test -d ${filename} && filetype="directory"
			test -r ${filename} && perm="readable"
			test -w ${filename} && perm="${perm} writable"
			test -x ${filename} && perm="${perm} exectable"
			
			#4. 开始输出信息
			echo  "The filename:${filename} is a ${filetype}"
			echo "And the permission for you are: ${perm}"