python import pandas as pd

```python import os

os.getcwd() ```

'C:\\Users\\Administrator'
python df = pd.read_csv('examples/ex1.csv')

python df

a	b	c	d	message
0	1	2	3	4	hello
1	5	6	7	8	world
2	9	10	11	12	foo
python pd.read_table('examples/ex1.csv', sep=',')

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: read_table is deprecated, use read_csv instead.
  """Entry point for launching an IPython kernel.
a	b	c	d	message
0	1	2	3	4	hello
1	5	6	7	8	world
2	9	10	11	12	foo
python pd.read_csv('examples/ex2.csv', header=None)

0	1	2	3	4
0	1	2	3	4	hello
1	5	6	7	8	world
2	9	10	11	12	foo
python pd.read_csv('examples/ex2.csv', names=['a', 'b', 'c', 'd', 'message'])

a	b	c	d	message
0	1	2	3	4	hello
1	5	6	7	8	world
2	9	10	11	12	foo
python names = ['a', 'b', 'c', 'd', 'message'] pd.read_csv('examples/ex2.csv', names=names, index_col='message')

a	b	c	d
message				
hello	1	2	3	4
world	5	6	7	8
foo	9	10	11	12
python parsed = pd.read_csv('examples/csv_mindex.csv', index_col=['key1', 'key2']) parsed

value1	value2
key1	key2		
one	a	1	2
b	3	4
c	5	6
d	7	8
two	a	9	10
b	11	12
c	13	14
d	15	16
python list(open('examples/ex3.txt'))

['            A         B         C\n',
 'aaa -0.264438 -1.026059 -0.619500\n',
 'bbb  0.927272  0.302904 -0.032399\n',
 'ccc -0.264273 -0.386314 -0.217601\n',
 'ddd -0.871858 -0.348382  1.100491\n']
python result = pd.read_table('examples/ex3.txt', sep='\s+') result

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: read_table is deprecated, use read_csv instead.
  """Entry point for launching an IPython kernel.
A	B	C
aaa	-0.264438	-1.026059	-0.619500
bbb	0.927272	0.302904	-0.032399
ccc	-0.264273	-0.386314	-0.217601
ddd	-0.871858	-0.348382	1.100491
python pd.read_csv('examples/ex4.csv', skiprows=[0, 2, 3])

a	b	c	d	message
0	1	2	3	4	hello
1	5	6	7	8	world
2	9	10	11	12	foo
python result = pd.read_csv('examples/ex5.csv') result

something	a	b	c	d	message
0	one	1	2	3.0	4	NaN
1	two	5	6	NaN	8	world
2	three	9	10	11.0	12	foo
python pd.isnull(result)

something	a	b	c	d	message
0	False	False	False	False	False	True
1	False	False	False	True	False	False
2	False	False	False	False	False	False
python result = pd.read_csv('examples/ex5.csv', na_values=['NULL']) result

something	a	b	c	d	message
0	one	1	2	3.0	4	NaN
1	two	5	6	NaN	8	world
2	three	9	10	11.0	12	foo
python sentinels = {'message': ['foo', 'NA'], 'something': ['two']} pd.read_csv('examples/ex5.csv', na_values=sentinels)

something	a	b	c	d	message
0	one	1	2	3.0	4	NaN
1	NaN	5	6	NaN	8	world
2	three	9	10	11.0	12	NaN
python pd.options.display.max_rows = 10

python result = pd.read_csv('examples/ex6.csv') result

one	two	three	four	key
0	0.467976	-0.038649	-0.295344	-1.824726	L
1	-0.358893	1.404453	0.704965	-0.200638	B
2	-0.501840	0.659254	-0.421691	-0.057688	G
3	0.204886	1.074134	1.388361	-0.982404	R
4	0.354628	-0.133116	0.283763	-0.837063	Q
...	...	...	...	...	...
9995	2.311896	-0.417070	-1.409599	-0.515821	L
9996	-0.479893	-0.650419	0.745152	-0.646038	E
9997	0.523331	0.787112	0.486066	1.093156	K
9998	-0.362559	0.598894	-1.843201	0.887292	G
9999	-0.096376	-1.012999	-0.657431	-0.573315	0
10000 rows × 5 columns

python pd.read_csv('examples/ex6.csv', nrows=5)

one	two	three	four	key
0	0.467976	-0.038649	-0.295344	-1.824726	L
1	-0.358893	1.404453	0.704965	-0.200638	B
2	-0.501840	0.659254	-0.421691	-0.057688	G
3	0.204886	1.074134	1.388361	-0.982404	R
4	0.354628	-0.133116	0.283763	-0.837063	Q
python chunker = pd.read_csv('examples/ex6.csv', chunksize=1000) chunker

<pandas.io.parsers.TextFileReader at 0x5fac0f0>
python chunker = pd.read_csv('examples/ex6.csv', chunksize=1000)

python tot = pd.Series([]) for piece in chunker: tot = tot.add(piece['key'].value_counts(), fill_value=0)

python tot = tot.sort_values(ascending=False)

python tot[:10]

E    368.0
X    364.0
L    346.0
O    343.0
Q    340.0
M    338.0
J    337.0
F    335.0
K    334.0
H    330.0
dtype: float64
python data = pd.read_csv('examples/ex5.csv') data

something	a	b	c	d	message
0	one	1	2	3.0	4	NaN
1	two	5	6	NaN	8	world
2	three	9	10	11.0	12	foo
python data.to_csv('examples/out.csv')

python import sys data.to_csv(sys.stdout, sep='|')

|something|a|b|c|d|message
0|one|1|2|3.0|4|
1|two|5|6||8|world
2|three|9|10|11.0|12|foo
python data.to_csv(sys.stdout, na_rep='NULL')

,something,a,b,c,d,message
0,one,1,2,3.0,4,NULL
1,two,5,6,NULL,8,world
2,three,9,10,11.0,12,foo
python data.to_csv(sys.stdout, index=False, header=False)

one,1,2,3.0,4,
two,5,6,,8,world
three,9,10,11.0,12,foo
python data.to_csv(sys.stdout, index=False, columns=['a', 'b', 'c'])

a,b,c
1,2,3.0
5,6,
9,10,11.0
python import numpy as np dates = pd.date_range('1/1/2000', periods=7) ts = pd.Series(np.arange(7), index=dates) ts.to_csv('examples/tseries.csv')

c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:4: FutureWarning: The signature of `Series.to_csv` was aligned to that of `DataFrame.to_csv`, and argument 'header' will change its default value from False to True: please pass an explicit value to suppress this warning.
  after removing the cwd from sys.path.
```python import csv f = open('examples/ex7.csv')

reader = csv.reader(f) ```

python for line in reader: print(line)

['a', 'b', 'c']
['1', '2', '3']
['1', '2', '3']
python with open('examples/ex7.csv') as f: lines = list(csv.reader(f))

python header, values = lines[0], lines[1:]

python data_dict = {h: v for h, v in zip(header, zip(*values))} data_dict

{'a': ('1', '1'), 'b': ('2', '2'), 'c': ('3', '3')}
python obj = """ {"name": "Wes", "places_lived": ["United States", "Spain", "Germany"], "pet": null, "siblings": [{"name": "Scott", "age": 30, "pets": ["Zeus", "Zuko"]}, {"name": "Katie", "age": 38, "pets": ["Sixes", "Stache", "Cisco"]}] } """

python import json result = json.loads(obj) result

{'name': 'Wes',
 'places_lived': ['United States', 'Spain', 'Germany'],
 'pet': None,
 'siblings': [{'name': 'Scott', 'age': 30, 'pets': ['Zeus', 'Zuko']},
  {'name': 'Katie', 'age': 38, 'pets': ['Sixes', 'Stache', 'Cisco']}]}
python asjson = json.dumps(result)

python siblings = pd.DataFrame(result['siblings'], columns=['name', 'age']) siblings

name	age
0	Scott	30
1	Katie	38
python data = pd.read_json('examples/example.json') data

a	b	c
0	1	2	3
1	4	5	6
2	7	8	9
python print(data.to_json())

{"a":{"0":1,"1":4,"2":7},"b":{"0":2,"1":5,"2":8},"c":{"0":3,"1":6,"2":9}}
python print(data.to_json(orient='records'))

[{"a":1,"b":2,"c":3},{"a":4,"b":5,"c":6},{"a":7,"b":8,"c":9}]
python import pandas as pd tables = pd.read_html('examples/fdic_failed_bank_list.html')

python len(tables)

1
python failures = tables[0]

python failures.head()

Bank Name	City	ST	CERT	Acquiring Institution	Closing Date	Updated Date
0	Allied Bank	Mulberry	AR	91	Today's Bank	September 23, 2016	November 17, 2016
1	The Woodbury Banking Company	Woodbury	GA	11297	United Bank	August 19, 2016	November 17, 2016
2	First CornerStone Bank	King of Prussia	PA	35312	First-Citizens Bank & Trust Company	May 6, 2016	September 6, 2016
3	Trust Company Bank	Memphis	TN	9956	The Bank of Fayette County	April 29, 2016	September 6, 2016
4	North Milwaukee State Bank	Milwaukee	WI	20364	First-Citizens Bank & Trust Company	March 11, 2016	June 16, 2016
python close_timestamps = pd.to_datetime(failures['Closing Date'])

python close_timestamps.dt.year.value_counts()

2010    157
2009    140
2011     92
2012     51
2008     25
2013     24
2014     18
2002     11
2015      8
2016      5
2004      4
2001      4
2007      3
2003      3
2000      2
Name: Closing Date, dtype: int64
python from lxml import objectify

python frame = pd.read_csv('examples/ex1.csv') frame

a	b	c	d	message
0	1	2	3	4	hello
1	5	6	7	8	world
2	9	10	11	12	foo
python frame.to_pickle('examples/frame_pickle')

python pd.read_pickle('examples/frame_pickle')

a	b	c	d	message
0	1	2	3	4	hello
1	5	6	7	8	world
2	9	10	11	12	foo
```python
```
