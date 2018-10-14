# 10yue14
## 只读变量：只能声明，但是不能修改和删除  
&ensp;&ensp;声明只读变量:   
&ensp;&ensp;redonly&ensp;name&ensp;&ensp;例如：readonly&ensp;pi=3.1415  
&ensp;&ensp;declare&ensp;-r&ensp;name  
&ensp;&ensp;只查看只读变量：  
&ensp;&ensp;&ensp;&ensp;redonly&ensp;-p  
&ensp;&ensp;位置变量  
&ensp;&ensp;&ensp;$0&ensp;命令本身&ensp;&ensp;&ensp;前边加basename显示基名&ensp;&ensp;is`basename $0`  
&ensp;&ensp;&ensp;$*传递给脚本的所有参数，全部参数合为一个字符串  
&ensp;&ensp;$@传递给脚本的所有参数，每个参数为独立字符串  
&ensp;&ensp;$#传递给脚本的参数的个数  
&ensp;&ensp;&ensp;$@$*只在被双引号包起来的时候才会有差异  
&ensp;&ensp;&ensp;set&ensp;--&ensp;清除所有位置变量  
抽取ip  
ifconfig&ensp;$1&ensp;|grep&ensp;netmask&ensp;|tr&ensp;-s&ensp;'&ensp;'&ensp;':'&ensp;|cut&ensp;-d":"&ensp;-f3  
Ip&ensp;|&ensp;抽取&ensp;netmask那行&ensp;|&ensp;压缩&ensp;重复&ensp;空格&ensp;以：代替&ensp;|&ensp;抽取&ensp;以:分割&ensp;&ensp;&ensp;第三列  
创建文件开头自动显示这些字符，并且＋执行权限...  
cat > $1 <<EOF
#!/bin/bash
#  
#********************************************************************  
#Author:&ensp;&ensp;&ensp;&ensp;&ensp;zhangwentian  
#QQ:&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;328343448  
#Date:&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;2018-10-10  
#FileName：&ensp;&ensp;&ensp;&ensp;&ensp;$1  
#Description：&ensp;&ensp;&ensp;&ensp;&ensp;The&ensp;test&ensp;script  
#Copyright&ensp;(C):&ensp;&ensp;&ensp;2018&ensp;All&ensp;rights&ensp;reserved  
#********************************************************************  
EOF  
chmod&ensp;+x&ensp;$1  
vim&ensp;+&ensp;$1  
## 退出状态  
- 进程使用退出状态来报告成功或失败  
&ensp;&ensp;0&ensp;代表成功&ensp;&ensp;1-&ensp;255代表失败  
&ensp;&ensp;$？标量保存最近的命令退出状态  
- 例如  
&ensp;&ensp;ping&ensp;-c1&ensp;-W1&ensp;hostdown&ensp;&>&ensp;/dev/null  

## 逻辑运算  
- 非：！  
&ensp;&ensp;！1=0&ensp;&ensp;！true&ensp;&ensp;true翻译真  
&ensp;&ensp;!0=1&ensp;&ensp;!&ensp;&ensp;false&ensp;&ensp;false翻译假的  
- 短路运算    
短路与  
&ensp;&ensp;第一个为0，结果必定为0  
&ensp;&ensp;&ensp;第一个为1，第二个必须参与运算  
&ensp;&ensp;&ensp;短路或  
&ensp;&ensp;&ensp;第一个为1，结果必定为1  
&ensp;&ensp;第一个为0，第二个必须参与运算    
&ensp;异或：^  
&ensp;&ensp;&ensp;异或的两个值，相同为假0，不同为真1  
&ensp;&ensp;0&ensp;^&ensp;0&ensp;&ensp;为0&ensp;&ensp;&ensp;&ensp;&ensp;0&ensp;^&ensp;1&ensp;&ensp;为&ensp;&ensp;&ensp;1  
&ensp;&ensp;&ensp;同或&ensp;&ensp;相同为1&ensp;&ensp;&ensp;不同为0  
## 条件性的执行操作符  
- 根据退出状态而定，命令可以有条件地运行  
&ensp;&ensp;&ensp;&&&ensp;代表条件性&ensp;&ensp;短路与  
&ensp;&ensp;||&ensp;&ensp;代表条件性&ensp;&ensp;短路或  
## 条件测试  
&ensp;&ensp;评估布尔声明，以便用在条件执行中  
- 若真，则返回0  
&ensp;&ensp;若假&ensp;&ensp;则返回1  
 - 测试命令  
test&ensp;EXPRESSION  
&ensp;[[&ensp;EXPRESSION&ensp;]]  
&ensp;&ensp;&ensp;注意&ensp;&ensp;EXPRESSION&ensp;前后必须有空白字符  
&ensp;例如test&ensp;"$str1"&ensp;=&ensp;"$str2"  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;[&ensp;"$str1"&ensp;!=&ensp;"$str2"]  
&ensp;&ensp;&ensp;等于1&ensp;&ensp;&ensp;执行失败  
&ensp;-z&ensp;&ensp;空就为真&ensp;0  
------    
&ensp;&ensp;-gt是否大于  
&ensp;&ensp;-ge&ensp;是否大于等于  
&ensp;&ensp;-eq&ensp;&ensp;是否等于  
&ensp;&ensp;-ne是否不等于  
&ensp;&ensp;&ensp;-lt是否小于  
&ensp;&ensp;&ensp;-le 是否小于等于  
## 文本处理三剑客指SED  
# sed工具  
- 用法：   
&ensp;&ensp;sed&ensp;[option]...&ensp;'script'&ensp;inputfile..  
- 常用选项  
&ensp;&ensp;-n&ensp;&ensp;不输出模式空间内容到屏幕，即不自动打印  
&ensp;&ensp;-e&ensp;&ensp;多点编辑  
&ensp;&ensp;-f&ensp;/PATH/SCRIPT_FILE&ensp;从指定文件中读取编辑脚本  
&ensp;&ensp;-r&ensp;&ensp;&ensp;&ensp;&ensp;支持使用扩展正则表达式  
&ensp;&ensp;-i.bak&ensp;&ensp;备份文件并原处编辑  
- script  
&ensp;&ensp;'地址&ensp;&ensp;命令‘  
# sed工具  
- 地址定界：  
&ensp;&ensp;&ensp;（1）不给地址：对全文进行处理  
&ensp;&ensp;（2)单地址：  
&ensp;&ensp;&ensp;#：指定的行，&ensp;$:最后一行  
&ensp;&ensp;&ensp;/pattern/:&ensp;被此处模式所能够匹配到的每一行  
（3）地址范围：  
&ensp;&ensp;&ensp;#，#  
&ensp;&ensp;&ensp;#，+#  
&ensp;&ensp;&ensp;/pat1/,/pat2/  
&ensp;&ensp;&ensp;#,/pat1/  
(4)~:进步  
&ensp;&ensp;&ensp;1~2奇数行  
&ensp;&ensp;&ensp;2~2&ensp;偶数行  
 ## 编辑命令  
&ensp;&ensp;&ensp;d&ensp;&ensp;&ensp;删除模式空间匹配的行，并立即启用下一轮循环  
&ensp;&ensp;&ensp;p&ensp;&ensp;&ensp;打印当前模式空间内容，追加到默认输出之后  
&ensp;&ensp;&ensp;a&ensp;[\]text&ensp;&ensp;在指定行后面追加文本，支持使用\n实现多行追加  
&ensp;&ensp;i&ensp;&ensp;[\]text&ensp;&ensp;在行前面插入文本  
&ensp;&ensp;c[\]text&ensp;&ensp;&ensp;替换行为单行或者多行文本  
&ensp;&ensp;w&ensp;&ensp;/path/file&ensp;保存模式匹配的行至指定文件  
&ensp;&ensp;r&ensp;/path/file&ensp;&ensp;读取指定文件的文本至模式空间中匹配到的行后  
&ensp;=&ensp;&ensp;&ensp;为模式空间中的行打印行号  
&ensp;！&ensp;模式空间中匹配行取反处理  
&ensp;&ensp;#&ensp;&ensp;sed工具  
&ensp;s///&ensp;&ensp;查找替换，支持使用其他分隔符，&ensp;&ensp;s@@@&ensp;,&ensp;&ensp;&ensp;&ensp;s###  
&ensp;g&ensp;&ensp;行内全局替换  
&ensp;p&ensp;&ensp;显示替换成功的行  
&ensp;w /PATH/FILE&ensp;&ensp;&ensp;将替换成功的行保存至文件中  
