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
예를 들어 주사위를 던져서 나올수 있는 결과들은 {1, 2, 3, 4, 5, 6} 입니다.
즉, 표본공간 S = {1, 2, 3, 4, 5, 6} 입니다.
<br>

**[In]**
```python
import random 
import matplotlib.pyplot as plt
import pandas as pd

# 1^6 중 랜덤하게 수를 리턴하는 주사위(dice) 함수
def dice_space_sample():
    return random.choice([1, 2, 3, 4, 5, 6])
  
for _ in range(10):
  space_sample.append(dice_space_sample())
```

**[Out]**
```python
[2, 5, 3, 1, 2, 3, 4, 2, 3, 6]
```
<br>

이처럼 Sample Space를 생성해봤습니다.