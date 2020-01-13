---
layout : post
title : "2. 분할정복 알고리즘 (3) Quick Sort"
description :
date : 2020-01-13
category : Algorithms
tags : [Algoritms, Quicksort]
use_math: true
comments : true
share : true

---

<br/>
Sanjoy Dasgupta가 저술한 책인 Algorithms과 [이기창님의 블로그](https://ratsgo.github.io/), [Heee님의 블로그](https://gmlwjd9405.github.io/)를 참고하였다.

<br/>

### 1. Quick Sort란?

: 리스트의 pivot(중앙값)을 선택한 뒤, pivot보다 작은 값과 큰 값으로 리스트를 둘로 분할하는 과정을 반복해 정렬하는 방법

Quick Sort(퀵 정렬)를 그림으로 쉽게 나타내면 다음과 같다.[(그림출처)](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)

<a href = "https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html"><img src = "https://gmlwjd9405.github.io/images/algorithm-quick-sort/quick-sort.png" width = "430" title = "source: heee.com"></a>

퀵 소트도 머지 소트처럼 분할(Divide) - 정복(Conquer) - 결합(Combine)의 순으로 정렬이 이루어진다.

1. 리스트에서 하나의 요소(pivot. 피벗)를 선택한다.

2. pivot보다 작은 값을 pivot 앞으로, pivot보다 큰 값을 pivot 앞으로 오도록 하여 리스트를 둘로 분할한다.

3. 분할된 리스트를 기준으로 1~2를 반복한다.(순환 호출)

4. 그럼 최종적으로 이쁘게 정렬된 하나의 데이터가 완성된다.

<br/>



### 2. Quick Sort의 특징

- **Unstable** 하다. 

  



### 3. Quick Sort의 특징





### 4. Quick Sort의 시간복잡도