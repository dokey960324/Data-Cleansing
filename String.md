功能 | 公式 | 备注
--- | --- | ---
大小写转换 | S.lower() | 
大小写转换 | S.upper() | 
所有单词首字母大写且其他字母小写 | S.title() | 
首字母大写、其他字母全部小写 | S.capitalize() | 
大写-->小写，小写-->大写 | S.swapcase() | 
测试字符串S是否是数字 | S.isdecimal() | 对于非Unicode字符串，前3个方法是等价的
测试字符串S是否是数字 | S.isdigit() | 
测试字符串S是否是数字 | S.isnumeric() | 
测试字符串S是否是字母 | S.isalpha() | 
测试字符串S是否是字母或数字 | S.isalnum() | 
判断是否小写 | S.islower() | 要求S中至少要包含一个字符串字符，否则直接返回False。例如不能是纯数字。
判断是否大写 | S.isupper() | 要求S中至少要包含一个字符串字符，否则直接返回False。例如不能是纯数字。
判断是否首字母大写 | S.istitle() | 判断时会对每个单词的首字母边界判断。例如，word1 Word2、word1_Word2、word1()Word2中都包含两个单词，它们的首字母都是"w"和"W"。因此，如果用istitle()去判断它们，将返回False，因为w是小写
判断字符串是否是空白(空格、制表符、换行符等)字符 | S.isspace() | 没有任何字符是不算是空白
判断字符串是否是可打印字符(例如制表符、换行符就不是可打印字符，但空格是) | S.isprintable() | 
判断字符串是否满足标识符定义规则 | S.isidentifier() | 标识符定义规则为：只能是字母或下划线开头、不能包含除数字、字母和下划线以外的任意字符
移除左右两边的字符 | char	S.strip([chars]) | if不指定chars/指定为None，则认移除空白(空格、制表符、换行符)。chars可以是多个字符序列。只要是这个序列中的字符，都会被移除。
移除左边的字符 | char	S.lstrip([chars]) | 如果不指定chars或者指定为None，则默认移除空白(空格、制表符、换行符)
移除右边的字符 | char	S.rstrip([chars]) | 如果不指定chars或者指定为None，则默认移除空白(空格、制表符、换行符)
从左向右分割字符串，并生成一个列表 | S.split(sep=None, maxsplit=-1) | maxsplit用于指定分割次数，如果不指定maxsplit或者给定值为"-1"，则会从左向右搜索并且每遇到sep一次就分割直到搜索完字符串。如果不指定sep或者指定为None，则改变分割算法：以空格为分隔符，且将连续的空白压缩为一个空格。
从右向左分割字符串，并生成一个列表 | S.rsplit(sep=None, maxsplit=-1) | maxsplit用于指定分割次数，如果不指定maxsplit或者给定值为"-1"，则会从左向右搜索并且每遇到sep一次就分割直到搜索完字符串。如果不指定sep或者指定为None，则改变分割算法：以空格为分隔符，且将连续的空白压缩为一个空格。
专门用来分割换行符，并生成一个列表 | S.splitlines([keepends=True]) | 
将可迭代对象(iterable)中的元素使用S连接起来 | S.join(iterable) | iterable中必须全部是字符串类型，否则报错
搜索字符串S中是否包含子串sub，如果包含，则返回sub的索引位置，否则返回"-1" | S.find(sub[, start[, end]]) | 
从右往左搜索字符串S中是否包含子串sub，如果包含，则返回sub的索引位置，否则返回"-1" | S.rfind(sub[, start[, end]]) | 
同上 | S.index(sub[, start[, end]]) | 
同上 | S.rindex(sub[, start[, end]]) | 
获取Python字符串中的某字符可以使用索引 | lang[0] | 
截取字符串中的一段字符串可以使用切片，切片在方括号中使用冒号:来分隔需要截取的首尾字符串的索引，方式是包括开头，不包括结尾 | lang[1:4] | 
当尾索引和头索引都没有给出的时候，默认返回整个字符串，不过这只是一个浅拷贝 | lang[:] | 
当头索引为负数时，则是指从字符串的尾部开始计数，最末尾的字符记为-1。if尾索引指明的位置<=头索引，then返回空字符串'' | lang[-2:] | 
获取字符串长度 | len(lang) | 
使用in操作符判断某个子字符是否在字符串中 | 'p' in lang | 
使用max()和min()方法获取字符串中编码最值对应的字符 | max(lang) | 
使用*操作符对字符串进行重复 | lang * 2 | 
使用cmp()方法对两个字符串进行对比，比较方式是先比较两个字符串的第一个字符的ASCII值，相同则比较第二个，依次类推，如果相等则返回0，第一个更小则返回-1，第一个大则返回1 | cmp(lang, lang2) | 
使用chr()方法将数值作为ASCII值转化为字符，类似于JavaScript中的String.fromCharCode()方法 | chr(97) | 
使用ord()方法获取字符的ASCII值，类似于JavaScript中字符串实例的charCodeAt()方法 | ord('a') | 
使用str()方法将其他数据类型转化为字符串 | str(3.14) | 
使用split()方法将字符串按照指定的字符串分隔，返回数组 | 'hello world'.split(' ') | 
使用swapcase()方法对字符串中所有的字符进行大小写互转，即小写变大写，大写变小写 | 'Abc'.swapcase() | 
使用join()方法连接字符串数组 | -'.join(['hello', 'world']) | 
使用find()方法判断一个字符串中是否含有某个子字符串，三个参数，第一个为必须，是指需要搜索的字符串，第二个和第三个参数则是指搜索的起始位置和终止位置，搜索得到则返回索引值，得不到则返回-1 | 'hello world'.find('llo') | 
使用endswith()和startswith()方法判断一个字符串是否是以某个字符串结尾、开头，参数和find()一致 | 'hello'.startswith('he') | 
反转字符串 | a = lang[::-1] | 
使用count()方法获取某个字符在字符串中出现的次数 | aaa111223'.count('a') | 
使用index()方法获取某个字符在字符串中首次出现的位置的索引 | lang.index('a') | 
首字母转为大写、其余转小写后的Series/Index of objects | Series.str.capitalize | 
全部转为大写后的Series/Index of objects | Series.str.lower | 
全部转为小写后的Series/Index of objects | Series.str.upper | 
每个单词的首字母转为大写、其余转小写后的Series/Index of objects | Series.str.title | 
全部小写转大写、大写转小写后的Series/Index of objects | Series.str.swapcase | 
Convert df['date'] from string to datetime | pd.to_datetime(df['date']) | 
