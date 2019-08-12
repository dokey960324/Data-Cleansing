
# 与SQL的比较
先导入pandas和numpy：

```python
import pandas as pd
import numpy as np
```

```python
url = 'https://raw.github.com/pydata/pandas/master/pandas/tests/data/tips.csv'
tips = pd.read_csv(url)
tips.head()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>16.99</td>
      <td>1.01</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10.34</td>
      <td>1.66</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21.01</td>
      <td>3.50</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>23.68</td>
      <td>3.31</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24.59</td>
      <td>3.61</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



## 选择

在SQL中， 用逗号将所要选择的列分隔开，来进行选择。（或用*表示选择所有列）：

SELECT total_bill, tip, smoker, time

FROM tips

LIMIT 5;

在pandas中，通过給DataFrame传递列名进行列选择：
```python
tips[['total_bill', 'tip', 'smoker', 'time']].head(5)
```


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>smoker</th>
      <th>time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>16.99</td>
      <td>1.01</td>
      <td>No</td>
      <td>Dinner</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10.34</td>
      <td>1.66</td>
      <td>No</td>
      <td>Dinner</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21.01</td>
      <td>3.50</td>
      <td>No</td>
      <td>Dinner</td>
    </tr>
    <tr>
      <th>3</th>
      <td>23.68</td>
      <td>3.31</td>
      <td>No</td>
      <td>Dinner</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24.59</td>
      <td>3.61</td>
      <td>No</td>
      <td>Dinner</td>
    </tr>
  </tbody>
</table>
</div>


如果没有说明列名，默认选择所有列

## WHERE 

通过WHERE子句完成SQL过滤。

SELECT *

FROM tips

WHERE time = 'Dinner'

LIMIT 5;

可以以多种方式筛选DataFrames;其中最直观的使用布尔索引。

```python
tips[tips['time'] == 'Dinner'].head(5)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>16.99</td>
      <td>1.01</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10.34</td>
      <td>1.66</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21.01</td>
      <td>3.50</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>23.68</td>
      <td>3.31</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24.59</td>
      <td>3.61</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



上述声明是通过給DataFrame传递一系列的真/假对象,返回所有真实的行。


```python
is_dinner = tips['time'] == 'Dinner'
```


```python
is_dinner.value_counts()
```




    True     176
    False     68
    Name: time, dtype: int64




```python
tips[is_dinner].head(5)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>16.99</td>
      <td>1.01</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10.34</td>
      <td>1.66</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21.01</td>
      <td>3.50</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>23.68</td>
      <td>3.31</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24.59</td>
      <td>3.61</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



就像SQL的or和and,通过使用|(or)和&(and)，可以将多个条件传递给DataFrame。

-- tips of more than $5.00 at Dinner meals

SELECT *


FROM tips


WHERE time = 'Dinner' AND tip > 5.00;


```python
# tips of more than $5.00 at Dinner meals
tips[(tips['time'] == 'Dinner') & (tips['tip'] > 5.00)]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>23</th>
      <td>39.42</td>
      <td>7.58</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>44</th>
      <td>30.40</td>
      <td>5.60</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>47</th>
      <td>32.40</td>
      <td>6.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>52</th>
      <td>34.81</td>
      <td>5.20</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>59</th>
      <td>48.27</td>
      <td>6.73</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>116</th>
      <td>29.93</td>
      <td>5.07</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>155</th>
      <td>29.85</td>
      <td>5.14</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>5</td>
    </tr>
    <tr>
      <th>170</th>
      <td>50.81</td>
      <td>10.00</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>172</th>
      <td>7.25</td>
      <td>5.15</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>181</th>
      <td>23.33</td>
      <td>5.65</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>183</th>
      <td>23.17</td>
      <td>6.50</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>211</th>
      <td>25.89</td>
      <td>5.16</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>212</th>
      <td>48.33</td>
      <td>9.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>214</th>
      <td>28.17</td>
      <td>6.50</td>
      <td>Female</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>239</th>
      <td>29.03</td>
      <td>5.92</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



-- tips by parties of at least 5 diners OR bill total was more than $45

SELECT *


FROM tips


WHERE size >= 5 OR total_bill > 45;


```python
tips[(tips['size'] >= 5) | (tips['total_bill'] > 45)]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>59</th>
      <td>48.27</td>
      <td>6.73</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>125</th>
      <td>29.80</td>
      <td>4.20</td>
      <td>Female</td>
      <td>No</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>6</td>
    </tr>
    <tr>
      <th>141</th>
      <td>34.30</td>
      <td>6.70</td>
      <td>Male</td>
      <td>No</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>6</td>
    </tr>
    <tr>
      <th>142</th>
      <td>41.19</td>
      <td>5.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>5</td>
    </tr>
    <tr>
      <th>143</th>
      <td>27.05</td>
      <td>5.00</td>
      <td>Female</td>
      <td>No</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>6</td>
    </tr>
    <tr>
      <th>155</th>
      <td>29.85</td>
      <td>5.14</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>5</td>
    </tr>
    <tr>
      <th>156</th>
      <td>48.17</td>
      <td>5.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>6</td>
    </tr>
    <tr>
      <th>170</th>
      <td>50.81</td>
      <td>10.00</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>182</th>
      <td>45.35</td>
      <td>3.50</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>185</th>
      <td>20.69</td>
      <td>5.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>5</td>
    </tr>
    <tr>
      <th>187</th>
      <td>30.46</td>
      <td>2.00</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>5</td>
    </tr>
    <tr>
      <th>212</th>
      <td>48.33</td>
      <td>9.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>216</th>
      <td>28.15</td>
      <td>3.00</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



使用notnull()和isnull()方法进行NULL检查。


```python
frame = pd.DataFrame({'col1': ['A', 'B', np.NaN, 'C', 'D'],
                      'col2': ['F', np.NaN, 'G', 'H', 'I']})
```


```python
frame
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>G</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C</td>
      <td>H</td>
    </tr>
    <tr>
      <th>4</th>
      <td>D</td>
      <td>I</td>
    </tr>
  </tbody>
</table>
</div>



SELECT *


FROM frame


WHERE col2 IS NULL;


```python
frame[frame['col2'].isnull()]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



SELECT *
FROM frame
WHERE col1 IS NOT NULL;



```python
frame[frame['col1'].notnull()]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C</td>
      <td>H</td>
    </tr>
    <tr>
      <th>4</th>
      <td>D</td>
      <td>I</td>
    </tr>
  </tbody>
</table>
</div>



## 分组

在pandas中,执行SQL的GROUP BY操作时使用同样的命名groupby()方法。groupby()通常是指一个过程,我们想把数据集分成组,应用一些函数(通常聚合),然后结合分组在一起。一个常见的SQL操作可以得到数据集中每组记录的数量。例如:

SELECT sex, count(*)

FROM tips

GROUP BY sex;

/*

Female     87

Male      157

*/

同理，The pandas是这样的：


```python
tips.groupby('sex').size()
```




    sex
    Female     87
    Male      157
    dtype: int64



注意,在pandas的代码中，我们使用size()并不是count()。这是因为count()函数适用于每一列,返回每个非空记录的数量。


```python
tips.groupby('sex').count()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>87</td>
      <td>87</td>
      <td>87</td>
      <td>87</td>
      <td>87</td>
      <td>87</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>157</td>
      <td>157</td>
      <td>157</td>
      <td>157</td>
      <td>157</td>
      <td>157</td>
    </tr>
  </tbody>
</table>
</div>



或者,我们可以用count()方法应用于一个单独的列:


```python
tips.groupby('sex')['total_bill'].count()
```




    sex
    Female     87
    Male      157
    Name: total_bill, dtype: int64



多样函数也可以应用。例如,我们想看看tip数量在一个星期中的变化，gg()允许您传递一个字典給分组DataFrame,表明函数适用于特定列。

SELECT day, AVG(tip), COUNT(*)

FROM tips

GROUP BY day;

/*

Fri   2.734737   19

Sat   2.993103   87

Sun   3.255132   76

Thur  2.771452   62

*/


```python
tips.groupby('day').agg({'tip': np.mean, 'day': np.size})
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tip</th>
      <th>day</th>
    </tr>
    <tr>
      <th>day</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Fri</th>
      <td>2.734737</td>
      <td>19</td>
    </tr>
    <tr>
      <th>Sat</th>
      <td>2.993103</td>
      <td>87</td>
    </tr>
    <tr>
      <th>Sun</th>
      <td>3.255132</td>
      <td>76</td>
    </tr>
    <tr>
      <th>Thur</th>
      <td>2.771452</td>
      <td>62</td>
    </tr>
  </tbody>
</table>
</div>



传递一个列表給groupby()方法，完成多个列的分组。

SELECT smoker, day, COUNT(*), AVG(tip)


FROM tips


GROUP BY smoker, day;


/*

smoker day


No     Fri      4  2.812500

       Sat     45  3.102889
       
       Sun     57  3.167895
       
       Thur    45  2.673778
         
Yes    Fri     15  2.714000

       Sat     42  2.875476
       
       Sun     19  3.516842
       
       Thur    17  3.030000
       
*/


```python
tips.groupby(['smoker', 'day']).agg({'tip': [np.size, np.mean]})
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="2" halign="left">tip</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>size</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>smoker</th>
      <th>day</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">No</th>
      <th>Fri</th>
      <td>4.0</td>
      <td>2.812500</td>
    </tr>
    <tr>
      <th>Sat</th>
      <td>45.0</td>
      <td>3.102889</td>
    </tr>
    <tr>
      <th>Sun</th>
      <td>57.0</td>
      <td>3.167895</td>
    </tr>
    <tr>
      <th>Thur</th>
      <td>45.0</td>
      <td>2.673778</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Yes</th>
      <th>Fri</th>
      <td>15.0</td>
      <td>2.714000</td>
    </tr>
    <tr>
      <th>Sat</th>
      <td>42.0</td>
      <td>2.875476</td>
    </tr>
    <tr>
      <th>Sun</th>
      <td>19.0</td>
      <td>3.516842</td>
    </tr>
    <tr>
      <th>Thur</th>
      <td>17.0</td>
      <td>3.030000</td>
    </tr>
  </tbody>
</table>
</div>



##  连接

使用join()或merge()进行连接。默认情况下,join()将加入DataFrames索引。每个方法有参数允许您指定连接类型(LEFT, RIGHT, INNER, FULL)或列的连接(列名或索引)。


```python
df1 = pd.DataFrame({'key': ['A', 'B', 'C', 'D'],
                  'value': np.random.randn(4)})
```


```python
df2 = pd.DataFrame({'key': ['B', 'D', 'D', 'E'],
                  'value': np.random.randn(4)})
```

假设我们有两个与DataFrames同名同结构的数据库表。现在我们来讨论各种类型的连接

### 内连接

SELECT *

FROM df1

INNER JOIN df2

  ON df1.key = df2.key;


```python
# merge performs an INNER JOIN by default
pd.merge(df1, df2, on='key')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>value_x</th>
      <th>value_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>B</td>
      <td>1.536419</td>
      <td>1.767244</td>
    </tr>
    <tr>
      <th>1</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.050838</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.956527</td>
    </tr>
  </tbody>
</table>
</div>



当你想把DataFrame的列与另一个DataFrame索引连接时，merge()函数给出了其他参数。


```python
indexed_df2 = df2.set_index('key')
```


```python
indexed_df2
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>value</th>
    </tr>
    <tr>
      <th>key</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>B</th>
      <td>1.767244</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.050838</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.956527</td>
    </tr>
    <tr>
      <th>E</th>
      <td>-0.053910</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df1, indexed_df2, left_on='key', right_index=True)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>value_x</th>
      <th>value_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>1.536419</td>
      <td>1.767244</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.050838</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.956527</td>
    </tr>
  </tbody>
</table>
</div>



### 左外连接

-- show all records from df1

SELECT *

FROM df1

LEFT OUTER JOIN df2

  ON df1.key = df2.key;


```python
# show all records from df1
pd.merge(df1, df2, on='key', how='left')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>value_x</th>
      <th>value_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>-0.675068</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>1.536419</td>
      <td>1.767244</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>-0.777839</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.050838</td>
    </tr>
    <tr>
      <th>4</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.956527</td>
    </tr>
  </tbody>
</table>
</div>



### 右连接

-- show all records from df2

SELECT *

FROM df1

RIGHT OUTER JOIN df2

  ON df1.key = df2.key;


```python
# show all records from df2
pd.merge(df1, df2, on='key', how='right')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>value_x</th>
      <th>value_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>B</td>
      <td>1.536419</td>
      <td>1.767244</td>
    </tr>
    <tr>
      <th>1</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.050838</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.956527</td>
    </tr>
    <tr>
      <th>3</th>
      <td>E</td>
      <td>NaN</td>
      <td>-0.053910</td>
    </tr>
  </tbody>
</table>
</div>



### 全连接

pandas还允许全连接,显示两边的数据集,无论是否找到列匹配。全连接不支持所有RDBMS(MySQL)。

-- show all records from both tables

SELECT *

FROM df1

FULL OUTER JOIN df2

  ON df1.key = df2.key;


```python
 pd.merge(df1, df2, on='key', how='outer')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>value_x</th>
      <th>value_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>-0.675068</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>1.536419</td>
      <td>1.767244</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>-0.777839</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.050838</td>
    </tr>
    <tr>
      <th>4</th>
      <td>D</td>
      <td>1.973574</td>
      <td>0.956527</td>
    </tr>
    <tr>
      <th>5</th>
      <td>E</td>
      <td>NaN</td>
      <td>-0.053910</td>
    </tr>
  </tbody>
</table>
</div>



## 联合

使用concat()联合所有。


```python
df1 = pd.DataFrame({'city': ['Chicago', 'San Francisco', 'New York City'],
                    'rank': range(1, 4)})
df2 = pd.DataFrame({'city': ['Chicago', 'Boston', 'Los Angeles'],
                    'rank': [1, 4, 5]})
```

SELECT city, rank

FROM df1

UNION ALL

SELECT city, rank

FROM df2;

/*

         city  rank
         
      Chicago     1
      
      Chicago     2

     New York     3

      Chicago     1
      
       Boston     4
       
      Angeles     5


```python
pd.concat([df1, df2])
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>-0.675068</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>1.536419</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>-0.777839</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>1.973574</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B</td>
      <td>1.767244</td>
    </tr>
    <tr>
      <th>1</th>
      <td>D</td>
      <td>0.050838</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>0.956527</td>
    </tr>
    <tr>
      <th>3</th>
      <td>E</td>
      <td>-0.053910</td>
    </tr>
  </tbody>
</table>
</div>



SQL’s UNION和UNION ALL相似,而UNION 删除重复行

SELECT city, rank

FROM df1

UNION

SELECT city, rank

FROM df2;

-- notice that there is only one Chicago record this time

/*

         city  rank
         
      Chicago     1
      
      Chicago     2

     New York     3

      Chicago     1
      
       Boston     4
       
      Angeles     5

在pandas中，使用drop_duplicates()删除重复行。


```python
pd.concat([df1, df2]).drop_duplicates()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>-0.675068</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>1.536419</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>-0.777839</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>1.973574</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B</td>
      <td>1.767244</td>
    </tr>
    <tr>
      <th>1</th>
      <td>D</td>
      <td>0.050838</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>0.956527</td>
    </tr>
    <tr>
      <th>3</th>
      <td>E</td>
      <td>-0.053910</td>
    </tr>
  </tbody>
</table>
</div>



pandas等价于一些SQL解析和聚合函数

### 带有偏移量前N行

-- MySQL

SELECT * FROM tips

ORDER BY tip DESC

LIMIT 10 OFFSET 5;


```python
tips.nlargest(10+5, columns='tip').tail(10)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>183</th>
      <td>23.17</td>
      <td>6.50</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>214</th>
      <td>28.17</td>
      <td>6.50</td>
      <td>Female</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>47</th>
      <td>32.40</td>
      <td>6.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>239</th>
      <td>29.03</td>
      <td>5.92</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>3</td>
    </tr>
    <tr>
      <th>88</th>
      <td>24.71</td>
      <td>5.85</td>
      <td>Male</td>
      <td>No</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>2</td>
    </tr>
    <tr>
      <th>181</th>
      <td>23.33</td>
      <td>5.65</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>2</td>
    </tr>
    <tr>
      <th>44</th>
      <td>30.40</td>
      <td>5.60</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>52</th>
      <td>34.81</td>
      <td>5.20</td>
      <td>Female</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
    <tr>
      <th>85</th>
      <td>34.83</td>
      <td>5.17</td>
      <td>Female</td>
      <td>No</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>4</td>
    </tr>
    <tr>
      <th>211</th>
      <td>25.89</td>
      <td>5.16</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



### 每组前n行

-- Oracle's ROW_NUMBER() analytic function

SELECT * FROM (

  SELECT
  
    t.*,
    
    ROW_NUMBER() OVER(PARTITION BY day ORDER BY total_bill DESC) AS rn
    
  FROM tips t
  
)

WHERE rn < 3

ORDER BY day, rn;


```python
 (tips.assign(rn=tips.sort_values(['total_bill'], ascending=False)
                      .groupby(['day'])
                    .cumcount() + 1)
     .query('rn < 3')
        .sort_values(['day','rn'])
    )

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
      <th>rn</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>95</th>
      <td>40.17</td>
      <td>4.73</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Fri</td>
      <td>Dinner</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>90</th>
      <td>28.97</td>
      <td>3.00</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Fri</td>
      <td>Dinner</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>170</th>
      <td>50.81</td>
      <td>10.00</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>212</th>
      <td>48.33</td>
      <td>9.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>156</th>
      <td>48.17</td>
      <td>5.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>182</th>
      <td>45.35</td>
      <td>3.50</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>197</th>
      <td>43.11</td>
      <td>5.00</td>
      <td>Female</td>
      <td>Yes</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>142</th>
      <td>41.19</td>
      <td>5.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>5</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



使用rank(method=’first’)函数


```python
(tips.assign(rnk=tips.groupby(['day'])['total_bill']
                       .rank(method='first', ascending=False))
       .query('rnk < 3')
     .sort_values(['day','rnk'])
   )
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_bill</th>
      <th>tip</th>
      <th>sex</th>
      <th>smoker</th>
      <th>day</th>
      <th>time</th>
      <th>size</th>
      <th>rnk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>95</th>
      <td>40.17</td>
      <td>4.73</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Fri</td>
      <td>Dinner</td>
      <td>4</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>90</th>
      <td>28.97</td>
      <td>3.00</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Fri</td>
      <td>Dinner</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>170</th>
      <td>50.81</td>
      <td>10.00</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>3</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>212</th>
      <td>48.33</td>
      <td>9.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sat</td>
      <td>Dinner</td>
      <td>4</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>156</th>
      <td>48.17</td>
      <td>5.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>6</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>182</th>
      <td>45.35</td>
      <td>3.50</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Sun</td>
      <td>Dinner</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>197</th>
      <td>43.11</td>
      <td>5.00</td>
      <td>Female</td>
      <td>Yes</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>4</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>142</th>
      <td>41.19</td>
      <td>5.00</td>
      <td>Male</td>
      <td>No</td>
      <td>Thur</td>
      <td>Lunch</td>
      <td>5</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>



-- Oracle's RANK() analytic function

SELECT * FROM (

  SELECT
  
    t.*,
    
    RANK() OVER(PARTITION BY sex ORDER BY tip) AS rnk
    
  FROM tips t
  
  WHERE tip < 2
  
)

WHERE rnk < 3

ORDER BY sex, rnk;

## 更新

UPDATE tips

SET tip = tip*2

WHERE tip < 2;


```python
 tips.loc[tips['tip'] < 2, 'tip'] *= 2
```

## 删除

DELETE FROM tips

WHERE tip > 9;

在pandas中，我们选择应该留下剩下的行,而不是删除它们


```python
tips = tips.loc[tips['tip'] <= 9]
```
