1. $表示字符串的结尾
1. 
1. \b表示单词的边界
1. 
1. re.sub(sub,src,s)
1. 
1. 在字符串之前添加r表示原始字符串
1. 
1. ^表示一个字符串的开始
1. 
1. re.search(pattern,obj)：查看obj能否匹配pattern所能表示的串，若可以，返回一个SRE_Match对象，否则放回None。
1. 
1. M?表示匹配0或1个M
1. 
1. (x|y|z)表示匹配x，y，z中的一个。
1. 
1. M{m,n}表示M出现m到n次。
1. 
1. 在search函数中将第三个参数赋值为re.VERBOSE表示松散正则，允许添加注释。
1. 
1. re.compile(patternStr):返回一个模式对象pattern，可以调用pattern.search(obj)来匹配obj串看其是否满足模式；该函数返回对象的groups()函数可以将匹配结果的分组给出（在patternStr中用小括号分割，最终以一个tuple返回）。
1. 
1. \d表示任何一个数字；\D表示任何一个非数字。
1. 
1. +表示1个或任意个前面出现的字符。
1. 
1. *表示0个或任意个前面出现的字符。
1. 
1. .匹配任意一个字符
1. 
1. [abc]匹配3个字符中的任意1个。
1. 
1. [0-4]匹配0到4范围内一个数字
1. 
1. [a-f]匹配a到f范围内一个字符
1. 
1. [^m]匹配1个非m字符
1. 
1. \s一个空白符，\S一个非空白符
1. 
1. \w任意1个数字或字母（包括大小写）以及下划线，\W反之
1. 
1. re.DOTALL设置后'.'表示任何一个字符包括newline，否则包括除newline外的所有字符。
1. 
1. match仅仅匹配一个字符串的开始，而search匹配整个字符串。使用^后，search也可以匹配字符串的开始，但是在MULTILINE模式下，search配合^匹配每一行的开始，而match仅匹配整个字符串的开始。
1. 
1. re.MULTILINE设置后，整个字符串被划分为多个行，^和$匹配每一行的开始和结束。默认情况下，二者仅仅匹配整个字符串的开始和结束。此处开始束表示每行的开始或者newline之后，结束表示newline之前。
1. 
1. re.split(pattern ,obj, maxsplit=0, flags=0):利用pattren将obj分割为几个部分，返回一个str列表。如果pattern包括组，那么组匹配的信息也会被返回，maxsplit指示分割的次数，flags设置为re.IGNORECASE时可以忽略大小写。
1. 
1. re.findall(pattern,string):默认返回一个str列表，当pattren中有多于一个组时，将返回一个tuple的列表。
1. 
1. 
