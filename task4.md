python import numpy as np

python import pandas as pd

python string_data = pd.Series(['aardvark', 'artichoke', np.nan, 'avocado']) string_data

0     aardvark
1    artichoke
2          NaN
3      avocado
dtype: object
python import numpy as np import pandas as pd

python from numpy import nan as NA

python data = pd.Series([1, NA, 3.5, NA, 7]) data.dropna()

0    1.0
2    3.5
4    7.0
dtype: float64
python data[data.notnull()]

0    1.0
2    3.5
4    7.0
dtype: float64
python data = pd.DataFrame([[1., 6.5, 3.], [1., NA, NA], [NA, NA, NA], [NA, 6.5, 3.]])

python cleaned = data.dropna()

python data

0	1	2
0	1.0	6.5	3.0
1	1.0	NaN	NaN
2	NaN	NaN	NaN
3	NaN	6.5	3.0
python cleaned

0	1	2
0	1.0	6.5	3.0
python data.dropna(how='all')

0	1	2
0	1.0	6.5	3.0
1	1.0	NaN	NaN
3	NaN	6.5	3.0
python data[4] = NA

python data

0	1	2	4
0	1.0	6.5	3.0	NaN
1	1.0	NaN	NaN	NaN
2	NaN	NaN	NaN	NaN
3	NaN	6.5	3.0	NaN
python data.dropna(axis=1, how='all')

0	1	2
0	1.0	6.5	3.0
1	1.0	NaN	NaN
2	NaN	NaN	NaN
3	NaN	6.5	3.0
python df = pd.DataFrame(np.random.randn(7, 3))

python df.iloc[:4, 1] = NA

python df.iloc[:2, 2] = NA

python df

0	1	2
0	-0.674843	NaN	NaN
1	-1.940305	NaN	NaN
2	-1.803935	NaN	0.058140
3	-0.937351	NaN	0.909948
4	-0.225786	1.756217	1.210888
5	1.013621	0.646347	-0.045784
6	0.156114	0.763175	-0.860102
python df.dropna()

0	1	2
4	-0.225786	1.756217	1.210888
5	1.013621	0.646347	-0.045784
6	0.156114	0.763175	-0.860102
python df.dropna(thresh=2)

0	1	2
2	-1.803935	NaN	0.058140
3	-0.937351	NaN	0.909948
4	-0.225786	1.756217	1.210888
5	1.013621	0.646347	-0.045784
6	0.156114	0.763175	-0.860102
python df.fillna(0)

0	1	2
0	-0.674843	0.000000	0.000000
1	-1.940305	0.000000	0.000000
2	-1.803935	0.000000	0.058140
3	-0.937351	0.000000	0.909948
4	-0.225786	1.756217	1.210888
5	1.013621	0.646347	-0.045784
6	0.156114	0.763175	-0.860102
python df.fillna({1: 0.5, 2: 0})

0	1	2
0	-0.674843	0.500000	0.000000
1	-1.940305	0.500000	0.000000
2	-1.803935	0.500000	0.058140
3	-0.937351	0.500000	0.909948
4	-0.225786	1.756217	1.210888
5	1.013621	0.646347	-0.045784
6	0.156114	0.763175	-0.860102
python _ = df.fillna(0, inplace=True)

python df

0	1	2
0	-0.674843	0.000000	0.000000
1	-1.940305	0.000000	0.000000
2	-1.803935	0.000000	0.058140
3	-0.937351	0.000000	0.909948
4	-0.225786	1.756217	1.210888
5	1.013621	0.646347	-0.045784
6	0.156114	0.763175	-0.860102
python df = pd.DataFrame(np.random.randn(6, 3))

python df.iloc[2:, 1] = NA df.iloc[4:, 2] = NA

python df

0	1	2
0	-0.528508	-0.979999	0.039006
1	-0.962534	0.109910	0.078351
2	1.289836	NaN	-0.954930
3	-1.108509	NaN	-0.266195
4	1.025095	NaN	NaN
5	-0.684276	NaN	NaN
python df.fillna(method='ffill')

0	1	2
0	-0.528508	-0.979999	0.039006
1	-0.962534	0.109910	0.078351
2	1.289836	0.109910	-0.954930
3	-1.108509	0.109910	-0.266195
4	1.025095	0.109910	-0.266195
5	-0.684276	0.109910	-0.266195
python df.fillna(method='ffill', limit=2)

0	1	2
0	-0.528508	-0.979999	0.039006
1	-0.962534	0.109910	0.078351
2	1.289836	0.109910	-0.954930
3	-1.108509	0.109910	-0.266195
4	1.025095	NaN	-0.266195
5	-0.684276	NaN	-0.266195
python data = pd.Series([1., NA, 3.5, NA, 7])

python data.fillna(data.mean())

0    1.000000
1    3.833333
2    3.500000
3    3.833333
4    7.000000
dtype: float64
python data = pd.DataFrame({'k1': ['one', 'two'] * 3 + ['two'], 'k2': [1, 1, 2, 3, 3, 4, 4]})

python data

k1	k2
0	one	1
1	two	1
2	one	2
3	two	3
4	one	3
5	two	4
6	two	4
python data.duplicated()

0    False
1    False
2    False
3    False
4    False
5    False
6     True
dtype: bool
python data.drop_duplicates()

k1	k2
0	one	1
1	two	1
2	one	2
3	two	3
4	one	3
5	two	4
python data['v1'] = range(7)

python data.drop_duplicates(['k1'])

k1	k2	v1
0	one	1	0
1	two	1	1
python data.drop_duplicates(['k1', 'k2'], keep='last')

k1	k2	v1
0	one	1	0
1	two	1	1
2	one	2	2
3	two	3	3
4	one	3	4
6	two	4	6
