Format Type | Data Description | Reader | Writer
--- | --- | --- | ---
text | CSV | read_csv | to_csv
text | JSON | read_json | to_json
text | HTML | read_html | to_html
text | Local clipboard | read_clipboard | to_clipboard
binary | MS Excel | read_excel | to_excel
binary | HDF5 Format | read_hdf | to_hdf
binary | Feather Format | read_feather | to_feather
binary | Parquet Format | read_parquet | to_parquet
binary | Msgpack | read_msgpack | to_msgpack
binary | Stata | read_stata | to_stata
binary | SAS | read_sas | 
binary | Python Pickle Format | read_pickle | to_pickle
SQL | SQL | read_sql | to_sql
SQL | Google Big Query | read_gbq | to_gbq

---

I/O | 函数 | 用途
--- | --- | ---
导入 | pd.read_csv(filename) | 从CSV文件导入数据
导入 | pd.read_table(filename) | 从限定分隔符的文本文件导入数据
导入 | pd.read_excel(filename) | 从Excel文件导入数据
导入 | pd.read_sql(query, connection_object) | 从SQL表/库导入数据
导入 | pd.read_json(json_string) | 从JSON格式的字符串导入数据
导入 | pd.read_html(url) | 解析URL、字符串或者HTML文件，抽取其中的tables表格
导入 | pd.read_clipboard() | 从你的粘贴板获取内容，并传给read_table()
导入 | pd.DataFrame(dict) | 从字典对象导入数据，Key是列名，Value是数据
导出 | df.to_csv(filename) | 导出数据到CSV文件
导出 | df.to_excel(filename) | 导出数据到Excel文件
导出 | df.to_sql(table_name, connection_object) | 导出数据到SQL表
导出 | df.to_json(filename) | 以Json格式导出数据到文本文件
