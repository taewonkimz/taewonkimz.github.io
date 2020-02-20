---
layout : post
title : "5. Greedy Algorithm (1) Introduction"
description :
date : 2020-01-25
category : Algorithms
tags : [Greedy Algorithm]
use_math: true
comments : true
share : true


---

<br/>
Sanjoy Dasgupta가 저술한 책인 Algorithms과 [이기창님의 블로그](https://ratsgo.github.io/)를 참고하였다.

<br/>

### 1. Greedy Algorithm

매 순간 최적이라고 생각되는 것을 선택해나가는 방식으로 진행하여 최종적으로 최적해에 도달하는 기법

그리디 알고리즘의 조건은 다음과 같다.

- **Greedy Choice Property(탐욕스런 선택 조건)** : 앞의 선택이 이후의 선택에 영향을 주지 않는다
- **Optimal Substructure(최적부분 구조 조건)** : 문제에 대한 최적해가 부분문제에 대해서도 최적해이다.

<br/>

### 2. Greedy Algorithm의 종류

여러가지 그리디 알고리즘의 종류에 대해 간단히 알아보고, 다음에 집중적으로 공부해보도록 하자.

- **[Kruskal Algorithm](https://taewonkimz.github.io/2020-02-15/MST/)**

  Minimum Spanning Tree(MST)를 구하기 위한 알고리즘. 사이클을 만들지 않는 선에서 가중치가 최소인 edge를 고르는 과정을 반복한다.

- **[Prim Algorithm](https://taewonkimz.github.io/2020-02-15/MST/)**

  Minimum Spanning Tree(MST)를 구하기 위한 알고리즘. 시작 정점과 가장 인접한 정점을 선택해 트리를 확장하고, 해당 트리와 가장 인접한 정점을 선택해 트리를 확장해 나간다.

- **Classroom Assignment**

  교실할당 문제. 자세한 내용은 [여기](https://ratsgo.github.io/data%20structure&algorithm/2017/11/22/greedy/) 참고

- **[Huffman Encoding](https://taewonkimz.github.io/2020-02-16/greedyetc/)**

  Greedy Algorithm을 이용해 데이터를 압축하는 기법.

- **[Set Cover](https://taewonkimz.github.io/2020-02-16/greedyetc/)**

  전체집합 $S$와 부분집합 $S'$가 주어졌을 때, $S'$ 중에서 가능한 한 적은 집합을 골라서 그들의 합집합이 $S$가 되도록 집합을 선택하는 문제

<br/>

### 3. Greedy Algorithm 기타 설명

그리디 알고리즘의 단점 : Local Optimum을 찾으면서 Global Optimum에 도달하는 방식이기 때문에 Global Optimum에 도달하지 못하고 Local Optimum에 빠져버릴 수 있다.

<br/>