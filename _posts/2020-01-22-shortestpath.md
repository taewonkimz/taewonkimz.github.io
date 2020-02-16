---
layout : post
title : "4. Paths in Graphs (1) Introduction of Shortest Path Problem"
description :
date : 2020-01-22
category : Algorithms
tags : [Graph, Shortest Path]
use_math: true
comments : true
share : true



---

<br/>
Sanjoy Dasgupta가 저술한 책인 Algorithms과 [이기창님의 블로그](https://ratsgo.github.io/)를 참고하였다.

<br/>

### 1. 그래프의 거리

그래프의 거리를 알기 위해서는 앞서 공부한 그래프 탐색 기법인 DFS와 BFS를 사용한다.  
하지만 DFS의 경우 최단경로를 찾지 못한다는 단점이 있다. 따라서 최단경로를 구하기 위해서는 노드를 큐에 넣었다가 빼는 과정을 반복하는 BFS를 주로 사용한다.

<br/>

### 2. Shortest Path Problem(최단경로문제)

그래프의 최단경로를 구하는 문제의 유형은 크게 네가지로 나뉜다.

- **하나의 정점에서 다른 하나의 정점**까지 최단경로(Single source and Single destination S.P)
- **하나의 정점에서 다른 모든 정점**까지 최단경로(Single source S.P) : 다익스트라, 벨만-포드
- **여러 정점에서 하나의 정점**까지 최단경로(Single Destination S.P)
- **여러 정점에서 모든 정점**까지 최단경로 최단경로(All pairs S.P) : 플로이드 - 워셜

최단경로문제를 해결하기 위해 꼭 알고 넘어가야 하는 속성이 있다.

**Optimal Substructure** : 부분문제의 최적해를 이용해 전체문제의 최적해를 구할 수 있는 구조.  
따라서 특정 경로의 중간정점들이 각각 최단이 된다면 해당 경로는 최단경로인 것을 확인할 수 있다.

<a href="https://imgur.com/4s5a0iz"><img src="https://i.imgur.com/4s5a0iz.png" width="300px" title="source: imgur.com" /></a>

Optimal Substructure는 Overlapping Subproblem과 함께 Dynamic Programming의 특성으로 많이 알려져있다. 이 부분은 나중에 공부하도록 하자.

<br/>

### 3. 최단경로문제 알고리즘

최단경로를 구하는 알고리즘은 Edge Relaxation을 기본 연산으로 한다.

**Edge Relaxation** : 최단경로를 구하는 과정에서 더 길이가 짧은 경로를 발견한다면, 최단경로를 구성하고 있는 노드와 엣지, 거리의 합을 업데이트 해주는 것

<a href="https://imgur.com/nqdnANR"><img src="https://i.imgur.com/nqdnANR.png" width="350px" title="source: imgur.com" /></a>

대표적인 최단경로문제 알고리즘은 앞서 설명했던 다익스트라 알고리즘과 벨만-포드 알고리즘이 있다. 여러 정점끼리의 최단경로를 구하는 알고리즘으로는 플로이드-워셜 알고리즘이 있다.

이들을 이제부터 공부해보자.

<br/>