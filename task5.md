python import numpy as np

python import pandas as pd

python data = pd.Series(np.random.randn(9), index=[['a', 'a', 'a', 'b', 'b', 'c', 'c', 'd', 'd'], [1, 2, 3, 1, 3, 1, 2, 2, 3]]) data

a  1    0.123728
   2    0.865701
   3   -0.373345
b  1    2.828310
   3    1.511521
c  1    1.530925
   2    0.678367
d  2    0.940052
   3   -1.577014
dtype: float64
python data.index

MultiIndex(levels=[['a', 'b', 'c', 'd'], [1, 2, 3]],
           codes=[[0, 0, 0, 1, 1, 2, 2, 3, 3], [0, 1, 2, 0, 2, 0, 1, 1, 2]])
python data['b']

1    2.828310
3    1.511521
dtype: float64
python data['b':'d']

b  1    2.828310
   3    1.511521
c  1    1.530925
   2    0.678367
d  2    0.940052
   3   -1.577014
dtype: float64
python data.loc[['b','d']]

b  1    2.828310
   3    1.511521
d  2    0.940052
   3   -1.577014
dtype: float64
python data.loc[:, 2]

a    0.865701
c    0.678367
d    0.940052
dtype: float64
python data.unstack()

1	2	3
a	0.123728	0.865701	-0.373345
b	2.828310	NaN	1.511521
c	1.530925	0.678367	NaN
d	NaN	0.940052	-1.577014
python data.unstack().stack()

a  1    0.123728
   2    0.865701
   3   -0.373345
b  1    2.828310
   3    1.511521
c  1    1.530925
   2    0.678367
d  2    0.940052
   3   -1.577014
dtype: float64
python frame = pd.DataFrame(np.arange(12).reshape((4, 3)), index=[['a', 'a', 'b', 'b'], [1, 2, 1, 2]], columns=[['Ohio', 'Ohio', 'Colorado'], ['Green', 'Red', 'Green']]) frame

Ohio	Colorado
Green	Red	Green
a	1	0	1	2
2	3	4	5
b	1	6	7	8
2	9	10	11
python frame.index.names = ['key1', 'key2'] frame.columns.names = ['state', 'color'] frame

state	Ohio	Colorado
color	Green	Red	Green
key1	key2			
a	1	0	1	2
2	3	4	5
b	1	6	7	8
2	9	10	11
python frame['Ohio']

color	Green	Red
key1	key2		
a	1	0	1
2	3	4
b	1	6	7
2	9	10
python frame.swaplevel('key1', 'key2')

state	Ohio	Colorado
color	Green	Red	Green
key2	key1			
1	a	0	1	2
2	a	3	4	5
1	b	6	7	8
2	b	9	10	11
python frame.sort_index(level=1)

state	Ohio	Colorado
color	Green	Red	Green
key1	key2			
a	1	0	1	2
b	1	6	7	8
a	2	3	4	5
b	2	9	10	11
python frame.swaplevel(0, 1).sort_index(level=0)

state	Ohio	Colorado
color	Green	Red	Green
key2	key1			
1	a	0	1	2
b	6	7	8
2	a	3	4	5
b	9	10	11
python frame.sum(level='key2')

state	Ohio	Colorado
color	Green	Red	Green
key2			
1	6	8	10
2	12	14	16
python frame.sum(level='color', axis=1)

color	Green	Red
key1	key2		
a	1	2	1
2	8	4
b	1	14	7
2	20	10
python frame = pd.DataFrame({'a': range(7), 'b': range(7, 0, -1), 'c': ['one', 'one', 'one', 'two', 'two', 'two', 'two'], 'd': [0, 1, 2, 0, 1, 2, 3]}) frame

a	b	c	d
0	0	7	one	0
1	1	6	one	1
2	2	5	one	2
3	3	4	two	0
4	4	3	two	1
5	5	2	two	2
6	6	1	two	3
python frame2 = frame.set_index(['c', 'd']) frame2

a	b
c	d		
one	0	0	7
1	1	6
2	2	5
two	0	3	4
1	4	3
2	5	2
3	6	1
python frame.set_index(['c', 'd'], drop=False)

a	b	c	d
c	d				
one	0	0	7	one	0
1	1	6	one	1
2	2	5	one	2
two	0	3	4	two	0
1	4	3	two	1
2	5	2	two	2
3	6	1	two	3
python frame2.reset_index()

c	d	a	b
0	one	0	0	7
1	one	1	1	6
2	one	2	2	5
3	two	0	3	4
4	two	1	4	3
5	two	2	5	2
6	two	3	6	1
python import numpy as np

python import pandas as pd

python df1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'], 'data1': range(7)}) df2 = pd.DataFrame({'key': ['a', 'b', 'd'], 'data2': range(3)}) df1 df2

key	data2
0	a	0
1	b	1
2	d	2
python df1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'], 'data1': range(7)}) df1

key	data1
0	b	0
1	b	1
2	a	2
3	c	3
4	a	4
5	a	5
6	b	6
python pd.merge(df1, df2)

key	data1	data2
0	b	0	1
1	b	1	1
2	b	6	1
3	a	2	0
4	a	4	0
5	a	5	0
python import numpy as np import pandas as pd

python df3 = pd.DataFrame({'lkey': ['b', 'b', 'a', 'c', 'a', 'a', 'b'], 'data1': range(7)}) df4 = pd.DataFrame({'rkey': ['a', 'b', 'd'], 'data2': range(3)}) pd.merge(df3, df4, left_on='lkey', right_on='rkey')

lkey	data1	rkey	data2
0	b	0	b	1
1	b	1	b	1
2	b	6	b	1
3	a	2	a	0
4	a	4	a	0
5	a	5	a	0
python df1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'], 'data1': range(7)}) df2 = pd.DataFrame({'key': ['a', 'b', 'd'], 'data2': range(3)}) df1 df2

key	data2
0	a	0
1	b	1
2	d	2
python pd.merge(df1, df2, how='outer')

key	data1	data2
0	b	0.0	1.0
1	b	1.0	1.0
2	b	6.0	1.0
3	a	2.0	0.0
4	a	4.0	0.0
5	a	5.0	0.0
6	c	3.0	NaN
7	d	NaN	2.0
python df1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'b'], 'data1': range(6)}) df2 = pd.DataFrame({'key': ['a', 'b', 'a', 'b', 'd'], 'data2': range(5)}) df1 df2 pd.merge(df1, df2, on='key', how='left')

key	data1	data2
0	b	0	1.0
1	b	0	3.0
2	b	1	1.0
3	b	1	3.0
4	a	2	0.0
5	a	2	2.0
6	c	3	NaN
7	a	4	0.0
8	a	4	2.0
9	b	5	1.0
10	b	5	3.0
python pd.merge(df1, df2, how='inner')

key	data1	data2
0	b	0	1
1	b	0	3
2	b	1	1
3	b	1	3
4	b	5	1
5	b	5	3
6	a	2	0
7	a	2	2
8	a	4	0
9	a	4	2
python left = pd.DataFrame({'key1': ['foo', 'foo', 'bar'], 'key2': ['one', 'two', 'one'], 'lval': [1, 2, 3]}) right = pd.DataFrame({'key1': ['foo', 'foo', 'bar', 'bar'], 'key2': ['one', 'one', 'one', 'two'], 'rval': [4, 5, 6, 7]}) pd.merge(left,right,on=['key1','key2'],how='outer')

key1	key2	lval	rval
0	foo	one	1.0	4.0
1	foo	one	1.0	5.0
2	foo	two	2.0	NaN
3	bar	one	3.0	6.0
4	bar	two	NaN	7.0
python pd.merge(left, right, on='key1')

key1	key2_x	lval	key2_y	rval
0	foo	one	1	one	4
1	foo	one	1	one	5
2	foo	two	2	one	4
3	foo	two	2	one	5
4	bar	one	3	one	6
5	bar	one	3	two	7
python pd.merge(left, right, on='key1', suffixes=('_left', '_right'))

key1	key2_left	lval	key2_right	rval
0	foo	one	1	one	4
1	foo	one	1	one	5
2	foo	two	2	one	4
3	foo	two	2	one	5
4	bar	one	3	one	6
5	bar	one	3	two	7
python left1 = pd.DataFrame({'key': ['a', 'b', 'a', 'a', 'b', 'c'], 'value': range(6)}) right1 = pd.DataFrame({'group_val': [3.5, 7]}, index=['a', 'b'])

python left1

key	value
0	a	0
1	b	1
2	a	2
3	a	3
4	b	4
5	c	5
python right1

group_val
a	3.5
b	7.0
python pd.merge(left1, right1, left_on='key', right_index=True)

key	value	group_val
0	a	0	3.5
2	a	2	3.5
3	a	3	3.5
1	b	1	7.0
4	b	4	7.0
python pd.merge(left1, right1, left_on='key', right_index=True, how='outer')

key	value	group_val
0	a	0	3.5
2	a	2	3.5
3	a	3	3.5
1	b	1	7.0
4	b	4	7.0
5	c	5	NaN
python lefth = pd.DataFrame({'key1': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada'], 'key2': [2000, 2001, 2002, 2001, 2002], 'data': np.arange(5.)}) righth = pd.DataFrame(np.arange(12).reshape((6, 2)), index=[['Nevada', 'Nevada', 'Ohio', 'Ohio', 'Ohio', 'Ohio'], [2001, 2000, 2000, 2000, 2001, 2002]], columns=['event1', 'event2'])

python lefth

key1	key2	data
0	Ohio	2000	0.0
1	Ohio	2001	1.0
2	Ohio	2002	2.0
3	Nevada	2001	3.0
4	Nevada	2002	4.0
python righth

event1	event2
Nevada	2001	0	1
2000	2	3
Ohio	2000	4	5
2000	6	7
2001	8	9
2002	10	11
python pd.merge(lefth, righth, left_on=['key1', 'key2'], right_index=True)

key1	key2	data	event1	event2
0	Ohio	2000	0.0	4	5
0	Ohio	2000	0.0	6	7
1	Ohio	2001	1.0	8	9
2	Ohio	2002	2.0	10	11
3	Nevada	2001	3.0	0	1
python pd.merge(lefth, righth, left_on=['key1', 'key2'], right_index=True, how='outer')

key1	key2	data	event1	event2
0	Ohio	2000	0.0	4.0	5.0
0	Ohio	2000	0.0	6.0	7.0
1	Ohio	2001	1.0	8.0	9.0
2	Ohio	2002	2.0	10.0	11.0
3	Nevada	2001	3.0	0.0	1.0
4	Nevada	2002	4.0	NaN	NaN
4	Nevada	2000	NaN	2.0	3.0
python left2 = pd.DataFrame([[1., 2.], [3., 4.], [5., 6.]], index=['a', 'c', 'e'], columns=['Ohio', 'Nevada']) right2 = pd.DataFrame([[7., 8.], [9., 10.], [11., 12.], [13, 14]], index=['b', 'c', 'd', 'e'], columns=['Missouri', 'Alabama']) left2

Ohio	Nevada
a	1.0	2.0
c	3.0	4.0
e	5.0	6.0
python right2

Missouri	Alabama
b	7.0	8.0
c	9.0	10.0
d	11.0	12.0
e	13.0	14.0
python pd.merge(left2, right2, how='outer', left_index=True, right_index=True)

Ohio	Nevada	Missouri	Alabama
a	1.0	2.0	NaN	NaN
b	NaN	NaN	7.0	8.0
c	3.0	4.0	9.0	10.0
d	NaN	NaN	11.0	12.0
e	5.0	6.0	13.0	14.0
python left2.join(right2, how='outer')

Ohio	Nevada	Missouri	Alabama
a	1.0	2.0	NaN	NaN
b	NaN	NaN	7.0	8.0
c	3.0	4.0	9.0	10.0
d	NaN	NaN	11.0	12.0
e	5.0	6.0	13.0	14.0
python left1.join(right1, on='key')

key	value	group_val
0	a	0	3.5
1	b	1	7.0
2	a	2	3.5
3	a	3	3.5
4	b	4	7.0
5	c	5	NaN
python another = pd.DataFrame([[7., 8.], [9., 10.], [11., 12.], [16., 17.]], index=['a', 'c', 'e', 'f'], columns=['New York', 'Oregon']) another

New York	Oregon
a	7.0	8.0
c	9.0	10.0
e	11.0	12.0
f	16.0	17.0
python left2.join([right2, another])

Ohio	Nevada	Missouri	Alabama	New York	Oregon
a	1.0	2.0	NaN	NaN	7.0	8.0
c	3.0	4.0	9.0	10.0	9.0	10.0
e	5.0	6.0	13.0	14.0	11.0	12.0
python left2.join([right2, another], how='outer')

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\frame.py:6848: FutureWarning: Sorting because non-concatenation axis is not aligned. A future version
of pandas will change to not sort by default.

To accept the future behavior, pass 'sort=False'.

To retain the current behavior and silence the warning, pass 'sort=True'.

  verify_integrity=True)
Ohio	Nevada	Missouri	Alabama	New York	Oregon
a	1.0	2.0	NaN	NaN	7.0	8.0
b	NaN	NaN	7.0	8.0	NaN	NaN
c	3.0	4.0	9.0	10.0	9.0	10.0
d	NaN	NaN	11.0	12.0	NaN	NaN
e	5.0	6.0	13.0	14.0	11.0	12.0
f	NaN	NaN	NaN	NaN	16.0	17.0
python arr = np.arange(12).reshape((3, 4)) arr

array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])
python np.concatenate([arr, arr], axis=1)

array([[ 0,  1,  2,  3,  0,  1,  2,  3],
       [ 4,  5,  6,  7,  4,  5,  6,  7],
       [ 8,  9, 10, 11,  8,  9, 10, 11]])
python s1 = pd.Series([0, 1], index=['a', 'b']) s2 = pd.Series([2, 3, 4], index=['c', 'd', 'e']) s3 = pd.Series([5, 6], index=['f', 'g'])

python pd.concat([s1, s2, s3])

a    0
b    1
c    2
d    3
e    4
f    5
g    6
dtype: int64
python pd.concat([s1, s2, s3], axis=1)

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: Sorting because non-concatenation axis is not aligned. A future version
of pandas will change to not sort by default.

To accept the future behavior, pass 'sort=False'.

To retain the current behavior and silence the warning, pass 'sort=True'.

  """Entry point for launching an IPython kernel.
0	1	2
a	0.0	NaN	NaN
b	1.0	NaN	NaN
c	NaN	2.0	NaN
d	NaN	3.0	NaN
e	NaN	4.0	NaN
f	NaN	NaN	5.0
g	NaN	NaN	6.0
python s4 = pd.concat([s1, s3]) s4

a    0
b    1
f    5
g    6
dtype: int64
python pd.concat([s1, s4], axis=1)

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: Sorting because non-concatenation axis is not aligned. A future version
of pandas will change to not sort by default.

To accept the future behavior, pass 'sort=False'.

To retain the current behavior and silence the warning, pass 'sort=True'.

  """Entry point for launching an IPython kernel.
0	1
a	0.0	0
b	1.0	1
f	NaN	5
g	NaN	6
python pd.concat([s1, s4], axis=1, join='inner')

0	1
a	0	0
b	1	1
python pd.concat([s1, s4], axis=1, join_axes=[['a', 'c', 'b', 'e']])

0	1
a	0.0	0.0
c	NaN	NaN
b	1.0	1.0
e	NaN	NaN
python result = pd.concat([s1, s1, s3], keys=['one', 'two', 'three']) result

one    a    0
       b    1
two    a    0
       b    1
three  f    5
       g    6
dtype: int64
python result.unstack()

a	b	f	g
one	0.0	1.0	NaN	NaN
two	0.0	1.0	NaN	NaN
three	NaN	NaN	5.0	6.0
python pd.concat([s1, s2, s3], axis=1, keys=['one', 'two', 'three'])

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: Sorting because non-concatenation axis is not aligned. A future version
of pandas will change to not sort by default.

To accept the future behavior, pass 'sort=False'.

To retain the current behavior and silence the warning, pass 'sort=True'.

  """Entry point for launching an IPython kernel.
one	two	three
a	0.0	NaN	NaN
b	1.0	NaN	NaN
c	NaN	2.0	NaN
d	NaN	3.0	NaN
e	NaN	4.0	NaN
f	NaN	NaN	5.0
g	NaN	NaN	6.0
python df1 = pd.DataFrame(np.arange(6).reshape(3, 2), index=['a', 'b', 'c'], columns=['one', 'two']) df2 = pd.DataFrame(5 + np.arange(4).reshape(2, 2), index=['a', 'c'], columns=['three', 'four']) df1

one	two
a	0	1
b	2	3
c	4	5
python df2

three	four
a	5	6
c	7	8
python pd.concat([df1, df2], axis=1, keys=['level1', 'level2'])

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: Sorting because non-concatenation axis is not aligned. A future version
of pandas will change to not sort by default.

To accept the future behavior, pass 'sort=False'.

To retain the current behavior and silence the warning, pass 'sort=True'.

  """Entry point for launching an IPython kernel.
level1	level2
one	two	three	four
a	0	1	5.0	6.0
b	2	3	NaN	NaN
c	4	5	7.0	8.0
python pd.concat({'level1': df1, 'level2': df2}, axis=1)

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: Sorting because non-concatenation axis is not aligned. A future version
of pandas will change to not sort by default.

To accept the future behavior, pass 'sort=False'.

To retain the current behavior and silence the warning, pass 'sort=True'.

  """Entry point for launching an IPython kernel.
level1	level2
one	two	three	four
a	0	1	5.0	6.0
b	2	3	NaN	NaN
c	4	5	7.0	8.0
python pd.concat([df1, df2], axis=1, keys=['level1', 'level2'], names=['upper', 'lower'])

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:2: FutureWarning: Sorting because non-concatenation axis is not aligned. A future version
of pandas will change to not sort by default.

To accept the future behavior, pass 'sort=False'.

To retain the current behavior and silence the warning, pass 'sort=True'.
upper	level1	level2
lower	one	two	three	four
a	0	1	5.0	6.0
b	2	3	NaN	NaN
c	4	5	7.0	8.0
python df1 = pd.DataFrame(np.random.randn(3, 4), columns=['a', 'b', 'c', 'd']) df2 = pd.DataFrame(np.random.randn(2, 3), columns=['b', 'd', 'a']) df1

a	b	c	d
0	-1.432160	-0.049389	0.865020	-1.450277
1	-0.021684	-0.566213	0.045547	0.579430
2	-0.332484	1.085832	-0.755399	0.964101
python df2

b	d	a
0	0.085256	0.674549	0.282105
1	0.398885	0.921410	0.934299
python pd.concat([df1, df2], ignore_index=True)

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: Sorting because non-concatenation axis is not aligned. A future version
of pandas will change to not sort by default.

To accept the future behavior, pass 'sort=False'.

To retain the current behavior and silence the warning, pass 'sort=True'.

  """Entry point for launching an IPython kernel.
a	b	c	d
0	-1.432160	-0.049389	0.865020	-1.450277
1	-0.021684	-0.566213	0.045547	0.579430
2	-0.332484	1.085832	-0.755399	0.964101
3	0.282105	0.085256	NaN	0.674549
4	0.934299	0.398885	NaN	0.921410
```python
```
