
# Pandas

##### 참고 : 파이썬 데이터 사이언스 핸드북 123p-136p


```python
import numpy as np
import pandas as pd
```

<br>

## Series 데이터 선택

##### In
```python
data = pd.Series([0.25, 0.5, 0.75, 1.0], index=['a', 'b', 'c', 'd'])
data
```
##### Out
    a    0.25
    b    0.50
    c    0.75
    d    1.00
    dtype: float64

<br>

##### In
```python
data['b']
```
##### Out
    0.5

<br>

##### In
```python
'a' in data
```
##### Out
    True

<br>

##### In
```python
data.keys()
```
##### Out
    Index(['a', 'b', 'c', 'd'], dtype='object')

<br>

##### In
```python
list(data.items())
```
##### Out
    [('a', 0.25), ('b', 0.5), ('c', 0.75), ('d', 1.0)]

<br>

##### In
```python
# column 추가
data['e'] = 1.25
data
```
##### Out
    a    0.25
    b    0.50
    c    0.75
    d    1.00
    e    1.25
    dtype: float64

<br>

### 슬라이싱

##### In
```python
data['a':'c']
```
##### Out
    a    0.25
    b    0.50
    c    0.75
    dtype: float64

<br>

##### In
```python
data[0:2]
```
##### Out
    a    0.25
    b    0.50
    dtype: float64

<br>

### 마스킹

##### In
```python
data[(data > 0.3) & (data < 0.8)]
```
##### Out
    b    0.50
    c    0.75
    dtype: float64

<br>

### 팬시 인덱싱

##### In
```python
data[['a', 'e']]
```
##### Out
    a    0.25
    e    1.25
    dtype: float64

<br>

### 인덱서

> .loc() <br>
> .iloc()

<br>

##### In
```python
data = pd.Series(['a', 'b', 'c'], index=[1, 3, 5])
data
```
##### Out
    1    a
    3    b
    5    c
    dtype: object

<br>

##### In
```python
print(data[1]) # 명시적
print(data.loc[1]) # 명시적
print(data.iloc[1]) # 암묵적
```
##### Out
    a
    a
    b
    
<br>

##### In
```python
print(data[1:3]) # 암묵적
print(data.loc[1:3]) # 명시적
print(data.iloc[1:3]) # 암묵적
```
##### Out
    3    b
    5    c
    dtype: object
    1    a
    3    b
    dtype: object
    3    b
    5    c
    dtype: object
    
<br>

## DataFrame 데이터 선택

##### In
```python
area = pd.Series({'California': 423697, 
                  'Texas': 695662,
                  'New York': 141297,
                  'Florida': 170312,
                  'Illinois': 149995})
pop = pd.Series({'California': 38332521,
                 'Texas': 26448193,
                 'New York': 19651127,
                 'Florida': 19552860,
                 'Illinois': 12882135})
data = pd.DataFrame({'area':area, 'pop':pop})
data
```
##### Out

<table>
    <tr>
      <th></th>
      <th>area</th>
      <th>pop</th>
    </tr>
    <tr>
      <th>California</th>
      <td>423697</td>
      <td>38332521</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>170312</td>
      <td>19552860</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>149995</td>
      <td>12882135</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>141297</td>
      <td>19651127</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>695662</td>
      <td>26448193</td>
    </tr>
</table>

<br>

##### In
```python
data['area']
```
##### Out
    California    423697
    Florida       170312
    Illinois      149995
    New York      141297
    Texas         695662
    Name: area, dtype: int64

<br>

##### In
```python
data.area
```
##### Out
    California    423697
    Florida       170312
    Illinois      149995
    New York      141297
    Texas         695662
    Name: area, dtype: int64

<br>

##### In
```python
data.area is data['area']
```
##### Out
    True

<br>

##### In
```python
data.pop is data['pop'] # DataFrame.pop() 함수가 있다.
```
##### Out
    False

<br>

##### In
```python
# column 생성할 때는 속성으로 접근하면 안된다.
data['density'] = data['pop'] / data['area']
data
```
##### Out

<table>
    <tr>
      <th></th>
      <th>area</th>
      <th>pop</th>
      <th>density</th>
    </tr>
    <tr>
      <th>California</th>
      <td>423697</td>
      <td>38332521</td>
      <td>90.471542</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>170312</td>
      <td>19552860</td>
      <td>114.806121</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>149995</td>
      <td>12882135</td>
      <td>85.883763</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>141297</td>
      <td>19651127</td>
      <td>139.076746</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>695662</td>
      <td>26448193</td>
      <td>38.018740</td>
    </tr>
</table>

<br>

##### In
```python
data.values
```
##### Out
    array([[4.23697000e+05, 3.83325210e+07, 9.04715422e+01],
           [1.70312000e+05, 1.95528600e+07, 1.14806121e+02],
           [1.49995000e+05, 1.28821350e+07, 8.58837628e+01],
           [1.41297000e+05, 1.96511270e+07, 1.39076746e+02],
           [6.95662000e+05, 2.64481930e+07, 3.80187404e+01]])

<br>

##### In
```python
data.values[0]
```
##### Out
    array([4.23697000e+05, 3.83325210e+07, 9.04715422e+01])

<br>

##### In
```python
data.T
```
##### Out

<table>
    <tr>
      <th></th>
      <th>California</th>
      <th>Florida</th>
      <th>Illinois</th>
      <th>New York</th>
      <th>Texas</th>
    </tr>
    <tr>
      <th>area</th>
      <td>4.236970e+05</td>
      <td>1.703120e+05</td>
      <td>1.499950e+05</td>
      <td>1.412970e+05</td>
      <td>6.956620e+05</td>
    </tr>
    <tr>
      <th>pop</th>
      <td>3.833252e+07</td>
      <td>1.955286e+07</td>
      <td>1.288214e+07</td>
      <td>1.965113e+07</td>
      <td>2.644819e+07</td>
    </tr>
    <tr>
      <th>density</th>
      <td>9.047154e+01</td>
      <td>1.148061e+02</td>
      <td>8.588376e+01</td>
      <td>1.390767e+02</td>
      <td>3.801874e+01</td>
    </tr>
</table>

<br>

### 인덱싱
> .loc() <br>
> .iloc() <br>
> .ix()

<br>

##### In
```python
data.loc[:'Illinois', :'pop']
```
##### Out

<table>
    <tr>
      <th></th>
      <th>area</th>
      <th>pop</th>
    </tr>
    <tr>
      <th>California</th>
      <td>423697</td>
      <td>38332521</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>170312</td>
      <td>19552860</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>149995</td>
      <td>12882135</td>
    </tr>
</table>

<br>

##### In
```python
data.iloc[:3, :2]
```
##### Out

<table>
    <tr>
      <th></th>
      <th>area</th>
      <th>pop</th>
    </tr>
    <tr>
      <th>California</th>
      <td>423697</td>
      <td>38332521</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>170312</td>
      <td>19552860</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>149995</td>
      <td>12882135</td>
    </tr>
</table>

<br>

##### In
```python
data.ix[:3, :'pop']
```
##### Out

<table>
    <tr>
      <th></th>
      <th>area</th>
      <th>pop</th>
    </tr>
    <tr>
      <th>California</th>
      <td>423697</td>
      <td>38332521</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>170312</td>
      <td>19552860</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>149995</td>
      <td>12882135</td>
    </tr>
</table>

<br>

##### In
```python
data.loc[data.density > 100, ['pop', 'density']]
```
##### Out

<table>
    <tr>
      <th></th>
      <th>pop</th>
      <th>density</th>
    </tr>
    <tr>
      <th>Florida</th>
      <td>19552860</td>
      <td>114.806121</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>19651127</td>
      <td>139.076746</td>
    </tr>
</table>

<br>

##### In
```python
data.iloc[0, 2] = 90
data
```
##### Out

<table>
    <tr>
      <th></th>
      <th>area</th>
      <th>pop</th>
      <th>density</th>
    </tr>
    <tr>
      <th>California</th>
      <td>423697</td>
      <td>38332521</td>
      <td>90.000000</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>170312</td>
      <td>19552860</td>
      <td>114.806121</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>149995</td>
      <td>12882135</td>
      <td>85.883763</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>141297</td>
      <td>19651127</td>
      <td>139.076746</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>695662</td>
      <td>26448193</td>
      <td>38.018740</td>
    </tr>
</table>

<br>

### 슬라이싱
> 인덱싱 : 열 참조 <br>
> 슬라이싱 : 행 참조

<br>

##### In
```python
data['Florida':'Illinois']
```
##### Out

<table>
    <tr>
      <th></th>
      <th>area</th>
      <th>pop</th>
      <th>density</th>
    </tr>
    <tr>
      <th>Florida</th>
      <td>170312</td>
      <td>19552860</td>
      <td>114.806121</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>149995</td>
      <td>12882135</td>
      <td>85.883763</td>
    </tr>
</table>

<br>

##### In
```python
data[1:3]
```
##### Out

<table>
    <tr>
      <th></th>
      <th>area</th>
      <th>pop</th>
      <th>density</th>
    </tr>
    <tr>
      <th>Florida</th>
      <td>170312</td>
      <td>19552860</td>
      <td>114.806121</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>149995</td>
      <td>12882135</td>
      <td>85.883763</td>
    </tr>
</table>

<br>

##### In
```python
data[data.density > 100]
```
##### Out

<table>
    <tr>
      <th></th>
      <th>area</th>
      <th>pop</th>
      <th>density</th>
    </tr>
    <tr>
      <th>Florida</th>
      <td>170312</td>
      <td>19552860</td>
      <td>114.806121</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>141297</td>
      <td>19651127</td>
      <td>139.076746</td>
    </tr>
</table>

<br>

## 데이터 연산

##### In
```python
rng = np.random.RandomState(42)
ser = pd.Series(rng.randint(0, 10, 4))
ser
```
##### Out
    0    6
    1    3
    2    7
    3    4
    dtype: int32

<br>

##### In
```python
df = pd.DataFrame(rng.randint(0, 10, (3, 4)), columns=['A', 'B', 'C', 'D'])
df
```
##### Out

<table>
    <tr>
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>9</td>
      <td>2</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7</td>
      <td>4</td>
      <td>3</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>2</td>
      <td>5</td>
      <td>4</td>
    </tr>
</table>

<br>

##### In
```python
np.exp(ser)
```
##### Out
    0     403.428793
    1      20.085537
    2    1096.633158
    3      54.598150
    dtype: float64

<br>

##### In
```python
np.sin(df * np.pi / 4)
```
##### Out

<table>
    <tr>
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>0</th>
      <td>-1.000000</td>
      <td>7.071068e-01</td>
      <td>1.000000</td>
      <td>-1.000000e+00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.707107</td>
      <td>1.224647e-16</td>
      <td>0.707107</td>
      <td>-7.071068e-01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.707107</td>
      <td>1.000000e+00</td>
      <td>-0.707107</td>
      <td>1.224647e-16</td>
    </tr>
</table>

<br>

### Series 간 연산

##### In
```python
area = pd.Series({'Alaska':1723337, 'Texas':695662, 'California':423967}, name='area')
population = pd.Series({'California':38332521, 'Texas':26448193, 'New York':19651127}, name='population')
population / area
```
##### Out
    Alaska              NaN
    California    90.413926
    New York            NaN
    Texas         38.018740
    dtype: float64

<br>

##### In
```python
area.index | population.index
```
##### Out
    Index(['Alaska', 'California', 'New York', 'Texas'], dtype='object')

<br>

##### In
```python
A = pd.Series([2, 4, 6], index=[0, 1, 2])
B = pd.Series([1, 3, 5], index=[1, 2, 3])
A + B
```
##### Out
    0    NaN
    1    5.0
    2    9.0
    3    NaN
    dtype: float64

<br>

### DataFrame 간 연산

##### In
```python
A = pd.DataFrame(rng.randint(0, 20, (2, 2)), columns=list('AB'))
A
```
##### Out

<table>
    <tr>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>1</td>
    </tr>
</table>

<br>

##### In
```python
B = pd.DataFrame(rng.randint(0, 10, (3, 3)), columns=list('BAC'))
B
```
##### Out

<table>
    <tr>
      <th></th>
      <th>B</th>
      <th>A</th>
      <th>C</th>
    </tr>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>8</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
      <td>2</td>
      <td>6</td>
    </tr>
</table>

<br>

##### In
```python
A + B
```
##### Out

<table>
    <tr>
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>15.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13.0</td>
      <td>6.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
</table>

<br>

<table>
    <tr> <td>+</td> <td>.add()</td> </tr>
    <tr> <td>-</td> <td>.sub() , .subtract()</td> </tr>
    <tr> <td>*</td> <td>.mul() , .multiply()</td> </tr>
    <tr> <td>/</td> <td>.truediv() , .div() , .divide()</td> </tr>
    <tr> <td>//</td> <td>.floordiv()</td> </tr>
    <tr> <td>%</td> <td>.mod()</td> </tr>
    <tr> <td>**</td> <td>.pow()</td> </tr>
</table>

<br>

##### In
```python
fill = A.stack().mean()
A.add(B, fill_value=fill)
```
##### Out

<table>
    <tr>
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>15.0</td>
      <td>13.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13.0</td>
      <td>6.0</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6.5</td>
      <td>13.5</td>
      <td>10.5</td>
    </tr>
</table>

<br>

### Series, DataFrame 간 연산

##### In
```python
A = rng.randint(10, size=(3,4))
A
```
##### Out
    array([[3, 8, 2, 4],
           [2, 6, 4, 8],
           [6, 1, 3, 8]])

<br>

##### In
```python
A - A[0]
```
##### Out
    array([[ 0,  0,  0,  0],
           [-1, -2,  2,  4],
           [ 3, -7,  1,  4]])

<br>

##### In
```python
df = pd.DataFrame(A, columns=list('QRST'))
df - df.iloc[0]
```
##### Out

<table>
    <tr>
      <th></th>
      <th>Q</th>
      <th>R</th>
      <th>S</th>
      <th>T</th>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1</td>
      <td>-2</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>-7</td>
      <td>1</td>
      <td>4</td>
    </tr>
</table>

<br>

##### In
```python
df.subtract(df['R'], axis=0)
```
##### Out

<table>
    <tr>
      <th></th>
      <th>Q</th>
      <th>R</th>
      <th>S</th>
      <th>T</th>
    </tr>
    <tr>
      <th>0</th>
      <td>-5</td>
      <td>0</td>
      <td>-6</td>
      <td>-4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-4</td>
      <td>0</td>
      <td>-2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>0</td>
      <td>2</td>
      <td>7</td>
    </tr>
</table>

<br>

##### In
```python
halfrow = df.iloc[0, ::2]
halfrow
```
##### Out
    Q    3
    S    2
    Name: 0, dtype: int32

<br>

##### In
```python
df - halfrow
```
##### Out

<table>
    <tr>
      <th></th>
      <th>Q</th>
      <th>R</th>
      <th>S</th>
      <th>T</th>
    </tr>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.0</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
</table>


