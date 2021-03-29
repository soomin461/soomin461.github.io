---
title:  "[Python Data Science] 확률/통계 기초 알아보기"
excerpt: "Python으로 확률/통계 공부"

categories:
  - Python
tags:
  - Python
  - Data science
  - Statistics
  - Machine Learning

toc: true
toc_sticky: true
 
date: 2021-03-28
last_modified_at: 2021-03-28
---

# 1. 개요
확률의 기초를 파이썬으로 구현해보자.
데이터를 이해하고, 처리하는 방법을 익혀보자.

# 2. 확률 개념
* 표본공간 (Sample Space)  
표본공간은, 발생가능한 결과들의 집합입니다.  
예를 들어 동전을 던져서 나올수 있는 결과들은 {'앞', '뒤'} 2가지 입니다.
즉, 표본공간 S = {'앞', '뒤'} 입니다.

<br>

```python
import random 
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
from collections import Counter

# '앞', '뒤' 중 랜덤하게 리턴하는 함수
def space_sample_coin():
    return random.choice(['앞', '뒤'])

space_sample = []

# 5번씩 굴려서 list에 저장
for _ in range(1000):
    space_sample.append("".join([space_sample_coin() for x in range(5)]))

space_sample[:10]
```

```python
    ['앞앞뒤앞뒤',
     '앞앞앞앞앞',
     '뒤앞뒤뒤앞',
     '뒤앞뒤뒤앞',
     '앞앞뒤앞뒤',
     '뒤뒤앞앞뒤',
     '뒤앞뒤앞앞',
     '앞뒤앞뒤앞',
     '뒤뒤뒤앞뒤',
     '뒤앞뒤앞뒤']
```



```python
# collection을 통하여, 각각의 항목이 몇번 나왔는지 dict화 할 수 있습니다.
print(Counter(space_sample))
```

    Counter({'뒤뒤앞뒤뒤': 42, '뒤뒤앞앞뒤': 40, '뒤앞앞앞뒤': 40, '앞뒤앞뒤앞': 39, '뒤앞앞뒤뒤': 39, '앞앞뒤앞뒤': 37, '뒤앞앞앞앞': 37, '앞앞뒤앞앞': 37, '뒤앞뒤앞앞': 34, '앞뒤뒤앞뒤': 34, '뒤뒤앞뒤앞': 34, '앞앞앞앞앞': 33, '앞앞앞뒤뒤': 33, '앞뒤뒤뒤뒤': 33, '뒤앞뒤뒤앞': 32, '앞뒤앞뒤뒤': 32, '뒤뒤뒤뒤앞': 31, '앞뒤뒤뒤앞': 30, '뒤뒤뒤앞앞': 30, '뒤앞앞뒤앞': 30, '뒤앞뒤뒤뒤': 30, '뒤뒤앞앞앞': 30, '앞뒤앞앞뒤': 29, '뒤뒤뒤앞뒤': 28, '앞앞뒤뒤뒤': 27, '앞뒤뒤앞앞': 27, '앞뒤앞앞앞': 26, '앞앞뒤뒤앞': 25, '뒤앞뒤앞뒤': 24, '앞앞앞뒤앞': 23, '뒤뒤뒤뒤뒤': 18, '앞앞앞앞뒤': 16})
    


```python
# 카운터의 most_common(n)를 통해서 가장 많이 나온 3가지를 확인가능
print(Counter(space_sample).most_common(3))
```

    [('뒤뒤앞뒤뒤', 42), ('뒤뒤앞앞뒤', 40), ('뒤앞앞앞뒤', 40)]
    


```python
df = pd.DataFrame(data = space_sample, columns = ['sample'])
df.head(10)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sample</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>앞앞뒤앞뒤</td>
    </tr>
    <tr>
      <th>1</th>
      <td>앞앞앞앞앞</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뒤앞뒤뒤앞</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뒤앞뒤뒤앞</td>
    </tr>
    <tr>
      <th>4</th>
      <td>앞앞뒤앞뒤</td>
    </tr>
    <tr>
      <th>5</th>
      <td>뒤뒤앞앞뒤</td>
    </tr>
    <tr>
      <th>6</th>
      <td>뒤앞뒤앞앞</td>
    </tr>
    <tr>
      <th>7</th>
      <td>앞뒤앞뒤앞</td>
    </tr>
    <tr>
      <th>8</th>
      <td>뒤뒤뒤앞뒤</td>
    </tr>
    <tr>
      <th>9</th>
      <td>뒤앞뒤앞뒤</td>
    </tr>
  </tbody>
</table>
</div>




```python
# '앞'을 카운트 해보자
def count_dice(sample):
    return sample.count('앞')
```


```python
df['count'] = df['sample'].map(count_dice)
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sample</th>
      <th>sample_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>앞앞뒤앞뒤</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>앞앞앞앞앞</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>뒤앞뒤뒤앞</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>뒤앞뒤뒤앞</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>앞앞뒤앞뒤</td>
      <td>3</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>995</th>
      <td>뒤뒤앞앞뒤</td>
      <td>2</td>
    </tr>
    <tr>
      <th>996</th>
      <td>뒤앞앞뒤앞</td>
      <td>3</td>
    </tr>
    <tr>
      <th>997</th>
      <td>뒤뒤앞뒤앞</td>
      <td>2</td>
    </tr>
    <tr>
      <th>998</th>
      <td>뒤앞뒤앞앞</td>
      <td>3</td>
    </tr>
    <tr>
      <th>999</th>
      <td>뒤뒤뒤앞뒤</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 2 columns</p>
</div>




```python
df['sample_count'].value_counts()
```




    3    324
    2    322
    1    164
    4    139
    5     33
    0     18
    Name: sample_count, dtype: int64



# 시각화 (matplotlib)


```python
data = df['sample_count'].value_counts().sort_index() / 1000 
data
```




    0    0.018
    1    0.164
    2    0.322
    3    0.324
    4    0.139
    5    0.033
    Name: sample_count, dtype: float64




```python
# matplotlib 시각화 도중 한글이 깨져서 폰트 추가 ########
import matplotlib.font_manager as fm

font_path = r'C:\Users\user\NanumGothic.ttf'
fontprop = fm.FontProperties(fname=font_path, size=18)
#######################################################

# figure 생성
fig = plt.figure()
fig.set_size_inches(10, 10)

# axes 설정
ax1 = fig.add_subplot(211)
ax1.set_title('앞면이 나온 횟수별 확률', fontproperties = fontprop)

# 각 확률을 누적하여 더한 것
ax2 = fig.add_subplot(212)
ax2.set_title('누적분포함수', fontproperties = fontprop)

# bar 차트로 확인
data.plot.bar(ax = ax1, color='k')
data.cumsum().plot.bar(ax = ax2, color='g')
```
    <matplotlib.axes._subplots.AxesSubplot at 0x1f5da8abfc8>

![image](https://user-images.githubusercontent.com/50326455/112842212-4b920e00-90dc-11eb-9340-7550b2d8ccf1.png)
