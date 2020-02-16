---
layout : post
title : "1. Algorithm's Introduction & Time Complexity"
description :
date : 2020-01-10
category : Algorithms
tags : [Algoritms]
use_math: true
comments : true
share : true
---

<br/>
Sanjoy Dasgupta가 저술한 책인 Algorithms를 참고하였다.
<br/>
<br/>

### 1. Algorithm(알고리즘)

주어진 입력을 출력으로 변환하는 잘 정의된 일련의 계산 단계

말 그대로 어떤 입력이 어떠한 과정을 어떤 출력으로 변환될 때, 입력을 출력으로 변환하는 그 과정을 알고리즘이라고 한다.

<a href = "[https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C](https://www.inflearn.com/course/알고리즘-강좌)"><img src = "https://cdn.inflearn.com/wp-content/uploads/algorith.png" width = "500px" title = "source : inflearn.com/"></a>

<br/>

### 2. Time Complexity(시간복잡도)

알고리즘을 제대로 이해하기 위해서는 **시간복잡도**라는 개념을 이해해야한다.

**시간복잡도** : 알고리즘을 수행하는 데 걸리는 시간  
cf) 공간복잡도 : 알고리즘을 수행하는 데 필요한 공간(메모리 용량)

- Big-Ω : 최상의 경우
- Big-θ : 평균의 경우
- Big-O : 최악의 경우

알고리즘의 핵심은 복잡한 일련의 단계를 **최대한 빨리 끝내는 것**이다. 알고리즘을 설명하거나 비교할 때도, 빨리 끝나는 시간보다 늦게 끝나는(최대) 시간복잡도를 이용할 필요가 있다.

따라서 "이 알고리즘이 늦게 끝나면 최대 이 시간까지 걸린다"고 명시하여 알고리즘의 치욕스러운 밑바닥(?)을 알려주기 위해, 주로 **빅오 표기법(Big-O)**를 사용하고 있다.

빅오 표기법을 이용해 속도를 비교하면 다음과 같다. 당연히 클수록 오래 걸리는 것이다.

$$1 < \log_2n < n^p (0 < p < 1 ) < n < n\log_2n < n^p(p>1) < n^p\log_2n < 2^n < n!$$

이처럼, 알고리즘의 성능을 나타낼 때 시간복잡도의 빅오 표기법을 이용한다.  
당연히 그 시간이 짧을수록 성능이 좋은 알고리즘이다.
<br/>
<br/>

## 3. 알고리즘의 종류

알고리즘의 종류로는 정렬 알고리즘(ex. 머지소트, 퀵소트 등)과 BST, Dynamic Programming 등 다양하다. 이 알고리즘에 대해서 지금부터 공부하려한다!

<br/>