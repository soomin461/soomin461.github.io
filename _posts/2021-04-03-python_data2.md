---
title:  "[Python Data Science] 정규분포"
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

<br>

# 1. 정규분포 

<br>

확률변수 X의 확률 밀도함수 f(x)가 아래 수식처럼 주어지는 경우, <br>
X의 확률분포를 **정규분포**라고 합니다.<br>

![image](https://user-images.githubusercontent.com/50326455/113477719-c8e3c700-94be-11eb-95ae-ab02ae1826be.png)

이때, N(μ, σ<sup>2</sup>)의 성질을 가집니다.<br>
μ은 평균을 의미하며 종모양의 그래프의 중심에 위치합니다. <br>
σ<sup>2</sup>, 표준편차의 제곱은 분산을 의미합니다. <br>
분산은 그래프의 모양을 보여주며 값이 작을수록 그래프의 모양이 뾰족해집니다. <br>
σ는, 표준편차를 의미합니다. <br>
<br>

![image](https://user-images.githubusercontent.com/50326455/113477809-8c649b00-94bf-11eb-9200-c9ac72e8cd60.png)

<li> 정규분포
    <ul>
        <li> 1) 평균 μ를 기준으로 대칭입니다. </li>
        <li> 2) 모든 곡선과 x축 사이의 면적의 합은 1입니다. </li>
        <li> 3) 모든 실수 x에 대해서, f(x) >= 0 입니다. </li>
    </ul>
</li>
<br>

# 2. 표준정규분포


예를 들어, P(Z<=0.5)의 확률을 구한다면, 좌측의 Z에서, 0.5를 찾고 상단의 0.00을 찾아 이에 해당하는 값을 찾습니다. <br>
여기에선, 0.6975가 될 것 입니다. <br>

![image](https://user-images.githubusercontent.com/50326455/113477890-2debec80-94c0-11eb-95e5-48342033cbe7.png)

## 2-1. 표준화(Z)

확률변수 X의 평균이 μ이고, 표준편차가 σ 일때,  확률변수 (X-m)/σ 의 평균은 0, 표준편차는 1입니다.<br>
**정규분포 N(μ, σ<sup>2</sup>)를 따를때, 확률변수 Z = (X-μ)/σ 는 표준정규분포 N(0, 1<sup>2</sup>)를 따릅니다.** <br>
정규분포를 따르는 확률변수 X를 표준화(Z = (X-μ)/σ)하여 확률변수 Z로 변경하는 것을 **'표준화'** 라고 합니다. <br>


## 2-2 예제

<table width="100" cellpadding="2" cellspacing="2">
  <tr>
    <td> z </td>
    <td> P(0≤Z≤z) </td>
  </tr>
  <tr>
    <td rowspan="4"> 0.5 <br> 1.0 <br> 1.5 <br> 2.0 </td>
    <td rowspan="4"> 0.1915 <br> 0.3413 <br> 0.4332 <br> 0.4772 </td>
  </tr>
</table>

Q. 확률변수 X가 정규분포 N(60, 2<sup>2</sup>)를 따를때 각 확률을 구해보자.
* P(X≥58)
* P(57≤X≤63)

<br>

A-1) <br>

표준화를 하기 위해서 Z=(X-μ)/σ = (X-60)/2 를 진행해줍니다.<br>
P(X≥58) = P(Z>=-1) = P(Z>=0) + P(-1<=Z<=0) = 0.5 + 0.3413 = 0.8413 <br>

![image](https://user-images.githubusercontent.com/50326455/113495832-21eb4380-952f-11eb-81da-b9b5eb9f3177.png)

<br>

A-2) <br>
표준화를 진행하게 되면 P(57≤X≤63) = p(-1.5≤Z≤1.5)로 바꿔쓸 수 있습니다.<br>
p(-1.5≤Z≤1.5) = 2 * P(Z≤1.5) = 2 * 0.4332 = 0.8664 <br>

![image](https://user-images.githubusercontent.com/50326455/113496449-9d032880-9534-11eb-8fac-4e189b029e5c.png)

```python
import matplotlib.pyplot as plt
import numpy as np

#표준정규분포 (평균 = 0, 표준편차 1)
mu, sigma = 0, 1

# np.random.normal은 평균이 mu, 표준편차가 sigma인 난수를 생성합니다.
x = np.random.normal(mu, sigma, 100000) 
plt.hist(x, bins=1000) #히스토그램으로 plot (bins는 막대의 개수입니다.)
```

그래프를 보면 알 수 있듯이, np.random.noraml의 난수의 개수를 늘리고, 히스토그램의 bins값을 증가시킨다면 매끄럽게 표현이 가능할 것 입니다. <br>

![image](https://user-images.githubusercontent.com/50326455/113496539-9aed9980-9535-11eb-9e71-78d159cd03cb.png)<br>



