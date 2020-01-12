---
layout : post
title : "2. 분할정복 알고리즘 (2) Merge Sort"
description :
date : 2020-01-12
category : Algorithms
tags : [Algoritms, Mergesort]
use_math: true
comments : true
share : true
---

<br/>
Sanjoy Dasgupta가 저술한 책인 Algorithms과 [이기창님의 블로그](https://ratsgo.github.io/)를 참고하였다.

<br/>

### 1. Merge Sort란?

: 데이터를 쪼갤 수 없을 때 까지 쪼갠 뒤, 둘씩 크기를 비교하며 정렬하며 합치는 정렬 방법

Merge Sort(합병정렬)를 그림으로 쉽게 나타내면 다음과 같다.[(그림출처)](https://ko.khanacademy.org/computing/computer-science/algorithms/merge-sort/a/overview-of-merge-sort)

![](https://i.imgur.com/ood27RZ.png)

기존에 p(시작점)부터 r(끝점)까지 데이터가 있었다면 , q(기준점)를 기준으로 데이터를 두 개로 쪼갠 뒤, 다시 쪼개진 각각의 데이터의 p와 r로부터 q를 선정하여 쪼개면 이번에는 데이터가 4개로 분리된다.

이 과정을 계속...................계속...............쪼갤 수 없을때 까지 반복하면 데이터가 8개로 분리가 되고, 이렇게 쪼개진 데이터를 두 개씩 비교하며 정렬한다. 그리고 합친 뒤, 다시 합쳐진 두 데이터끼리 비교해서 정렬한다. 이 과정을 또 계속 반복하면 최종적으로 데이터가 다시 하나로 합쳐질 때 모두 정렬되는 것이다.

<br/>



### 2. Merge Sort의 특징

우선 정렬 알고리즘은 **Stable** 하는지, 또 **In-place** 하는지에 따라 성격이 구분된다.

***- Stable***  : 같은 값의 위치(순서)가 정렬 과정에서 뒤바뀌지 않는 경우

***- In-place*** : 탐색대상을 정렬할 때 추가적인 메모리 공간이 필요하지 않은 경우(데이터가 저장된 그 공간에서 정렬이 가능)

<br/>



Merge Sort는 Devide하는 단계에서 각 node의 index가 변화하지 않고, Merge하는 과정에서도 같은 key값을 가지는 node가 swap되지 않기 때문에 index가 변화하지 않는다. 따라서 ==**Stable**== 하다.

그리고 연결리스트와 배열 중 ==**자료구조로 무엇을 쓰느냐에 따라 In-place한지 아닌지**==를 알 수 있다.

<br/>



**1. 연결리스트(Linked list)** : 각 노드가 데이터와 포인터를 갖고 한 줄로 연결되어 있는 방식으로 데이터를 저장하는 자료구조

   <a href = "https://imgur.com/nbnpk50"><img src = "https://i.imgur.com/nbnpk50.png" width = "600px" title = "source: imgur.com"></a>

   연결리스트를 사용하게 되면 기존 저장공간에서 포인터만 바꾸는 형식으로 머지소트를 수행할 수 있다.

   따라서 따로 리스트를 저장할 별도의 공간이 필요하지 않기 때문에 **In-place** 하다.

   <br/>

   

**2. 배열(Array)** : 같은 종류의 데이터들이 순차적으로 저장된 자료구조

   <a href="https://imgur.com/kpDOStz"><img src="https://i.imgur.com/kpDOStz.png" width="600px" title="source: imgur.com" /></a>

   배열은 리스트를 쪼갤 경우 쪼개진 리스트를 별도로 저장할 공간이 없기 때문에 **In-place**하지 않다.

<br/>



따라서 머지소트의 경우 연결리스트와 배열 중 어떤 자료구조를 사용하느냐에 따라 **In-place** 할 수도 있고 아닐 수도 있다.

(이후에 공부할 Quick Sort와 Heap Sort는 모두 Unstable하고 In-Place하다!)

<br/>



### 3. Merge Sort의 시간복잡도

머지소트의 틀을 그림으로 나타내면 다음과 같다.

<a href = "https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html"><img src = "https://gmlwjd9405.github.io/images/algorithm-merge-sort/sort-time-complexity-etc.png" width = "600px" title = "source: gnlwjd9405"></a>

- 기존의 $n$개의 데이터를 각각 $n/2$인 데이터 2개로 쪼개고, 또 $n/2$인 데이터를 각각 쪼개서 4개의 $n/4$ 데이터를 만들고...........하는 방식이다.

- 이때, 가장 처음 $n$개의 데이터의 높이를 0이라고 하면, $n/2$일 때는 1, $n/4$일 때는 2....처럼 나타낼 수 있는데

  이 높이는 $k = \log_2n$으로 나타낼 수 있다.


- 그리고 각 높이별로 높이가 0일 때 $n$번 비교, 높이가 1일 때 $n/2 * 2 = n$번 비교..............처럼 매 높이마다 똑같이 $n$번 비교하는 것을 알 수 있다.

<br/>



따라서! 머지소트를 수행하는 동안 데이터로부터 만들어진 높이($\log_2n$)별로 각각 $n$번 비교하고 정렬하기 때문에 **Merge Sort의 시간복잡도는 $O(\log_2n) * O(n)$ = ==$O(n\log_2n)$==임을 알 수 있다.**