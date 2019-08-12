功能 | 函数 | 解释
--- | --- | ---
创建测试对象 | pd.DataFrame(np.random.rand(20,5)) | 创建20行5列的随机数组成的DataFrame对象
创建测试对象 | pd.Series(my_list) | 从可迭代对象my_list创建一个Series对象
创建测试对象 | df.index = pd.date_range('1900/1/30', periods=df.shape[0]) | 增加一个日期索引
查看数据 | df.head(n) | 查看DataFrame对象的前n行
查看数据 | df.tail(n) | 查看DataFrame对象的最后n行
查看数据 | df.shape() | 查看行数和列数
查看数据 | df.info() | 查看索引、数据类型和内存信息
查看数据 | df.describe() | 查看数值型列的汇总统计
查看数据 | s.value_counts(dropna=False) | 查看Series对象的唯一值和计数
查看数据 | df.apply(pd.Series.value_counts) | 查看DataFrame对象中每一列的唯一值和计数
数据选取 | df[col] | 根据列名，并以Series的形式返回列
数据选取 | df[[col1, col2]] | 以DataFrame形式返回多列
数据选取 | s.iloc[0] | 按位置选取数据，可输入1:7，也可输入布尔数组True, False,False，当索引是日期时'20130102':'20130104'
数据选取 | s.loc['index_one'] | 按索引选取数据，可输入'a':'f'(此处左右都是闭区间)，也可输入布尔数组True, False,False
数据选取 | df.iloc[0,:] | 返回第一行
数据选取 | df.iloc[0,0] | 返回第一列的第一个元素
数据清理 | df.columns = ['a','b','c'] | 重命名列名
数据清理 | pd.isnull() | 检查DataFrame对象中的空值，并返回一个Boolean数组
数据清理 | pd.notnull() | 检查DataFrame对象中的非空值，并返回一个Boolean数组
数据清理 | df.dropna() | 删除所有包含空值的行
数据清理 | df.dropna(axis=1) | 删除所有包含空值的列
数据清理 | df.dropna(axis=1,thresh=n) | 删除所有小于n个非空值的行
数据清理 | df.fillna(x) | 用x替换DataFrame对象中所有的空值
数据清理 | s.astype(float) | 将Series中的数据类型更改为float类型
数据清理 | s.replace(1,'one') | 用‘one’代替所有等于1的值
数据清理 | s.replace([1,3],['one','three']) | 用'one'代替1，用'three'代替3
数据清理 | df.rename(columns=lambda x: x + 1) | 批量更改列名
数据清理 | df.rename(columns={'old_name': 'new_ name'}) | 选择性更改列名
数据清理 | df.set_index('column_one') | 更改索引列
数据清理 | df.rename(index=lambda x: x + 1) | 批量重命名索引
筛选、排序、合并 | df[df[col] > 0.5] | 选择col列的值大于0.5的行
筛选、排序、合并 | df.sort_values(col1) | 按照列col1排序数据，默认升序排列
筛选、排序、合并 | df.sort_values(col2, ascending=False) | 按照列col1降序排列数据
筛选、排序、合并 | df.sort_values([col1,col2], ascending=[True,False]) | 先按列col1升序排列，后按col2降序排列数据
筛选、排序、合并 | df.groupby(col) | 返回一个按列col进行分组的Groupby对象
筛选、排序、合并 | df.groupby([col1,col2]) | 返回一个按多列进行分组的Groupby对象
筛选、排序、合并 | df.groupby(col1)[col2] | 返回按列col1进行分组后，列col2的均值
筛选、排序、合并 | df.pivot_table(index=col1, values=[col2,col3], aggfunc=max) | 创建一个按列col1进行分组，并计算col2和col3的最大值的数据透视表
筛选、排序、合并 | df.groupby(col1).agg(np.mean) | 返回按列col1分组的所有列的均值
筛选、排序、合并 | data.apply(np.mean) | 对DataFrame中的每一列应用函数np.mean
筛选、排序、合并 | data.apply(np.max,axis=1) | 对DataFrame中的每一行应用函数np.max
数据合并 | df1.append(df2) | 将df2中的行添加到df1的尾部
数据合并 | df.concat([df1, df2],axis=1) | 将df2中的列添加到df1的尾部
数据合并 | df1.join(df2,on=col1,how='inner') | 对df1的列和df2的列执行SQL形式的join
数据统计 | df.mean() | 返回所有列的均值
数据统计 | df.corr() | 返回列与列之间的相关系数
数据统计 | df.count() | 返回每一列中的非空值的个数
数据统计 | df.max() | 返回每一列的最大值
数据统计 | df.min() | 返回每一列的最小值
数据统计 | df.median() | 返回每一列的中位数
数据统计 | df.std() | 返回每一列的标准差
查看数据 | s[::-1] | 按照索引倒序排列
数据选取 | s[::2] | 一行跳一行地取
数据选取 | df.loc[:, df.loc['a'] > 0] | a行数据为正数的那一列
查看数据 | list('abcde') | =['a','b','c','d','e']
查看数据 | s.isin([2, 4, 6]) | 所有数据的布尔型结果df
数据选取 | s[s.isin([2, 4, 6])] | 结果为True的那些数据
数据选取 | s.reindex([2, 4, 6]) | index中有2、4的数据会按照2、4的顺序挑出来，index中没有6的会用NaN填充，且原本的int64会变成float64
