# split() 正则表达式


split("\\^", 2)

 因为要保留^（因为^ 是正则表达式的元数据所以需要加\） 要保留\^  确保 \^ 给正则表达式解析，那就要 加\保留 \^ 让正则解析.
                              
表1.常用的元字符
代码	说明
.	匹配除换行符以外的任意字符
\w	匹配字母或数字或下划线或汉字
\s	匹配任意的空白符
\d	匹配数字
\b	匹配单词的开始或结束
^	匹配字符串的开始
$	匹配字符串的结束

如果你想查找元字符本身的话，比如你查找.,或者*,就出现了问题：你没办法指定它们，因为它们会被解释成别的意思。这时你就得使用\来取消这些字符的特殊意义。因此，你应该使用\.和\*。当然，要查找\本身，你也得用\\.


