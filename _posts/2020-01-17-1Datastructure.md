---
layout : post
title : "참고 1. Data Structure - Tree, Queue, Stack"
description :
date : 2020-01-17
category : Algorithms
tags : [Data Structure, Tree, Queue, Stack]
use_math: true
comments : true
share : true
---

<br/>
Sanjoy Dasgupta가 저술한 책인 Algorithms과 [이기창님의 블로그](https://ratsgo.github.io/), [Heee님의 블로그](https://gmlwjd9405.github.io/)를 참고하였다.

<br/>

### 1-1. Tree(트리)

트리를 재귀적 형태로 정의하면 다음과 같다

*재귀적 형태(Recurrence Relation) : 수열의 항 사이에서 성립하는 관계식. 즉, 자기 자신을 호출하는 점화식(ex. 피보나치 수열, 퀵소트*

**Tree(트리)** : 루트노드가 0개 이상의 자식 노드를 갖고, 그 자식 노드가 또 0개 이상의 자식 노드를 갖는 형태의 자료구조

<a href="https://imgur.com/6UeCp8t"><img src="https://i.imgur.com/6UeCp8t.png" width="500px" title="source: imgur.com" /></a>

- 노드(Node) : 데이터가 담기는 저장 공간. 정점이라고도 함
- 엣지(Edge) : 노드를 연결하는 선. 노드와의 관계 표시. 간선이라고도 함
- 경로(Path) : 노드-엣지-노드-엣지...와 같이 인접한 노드들을 잇는 엣지의 집합
- 경로의 길이(Length) : 경로에 속한 엣지의 수
- 깊이(depth) : 루트노드에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수. 0에서 시작
- 트리의 높이(height) : 루트노드에서 말단노드에 이르는 가장 긴 경로의 엣지 수
- 레벨(Level) : 트리의 특정 깊이를 갖는 노드의 집합. 1에서 시작

<br/>

### 1-2. Tree(트리)의 특징

- 계층 모델이다.
- DAG(Directed Acyclic Graphs. 유항비순환그래프)이다.
  - 루프(loop), 사이클(cycle)이 존재하지 않는다.
- 엣지의 개수 = 노드의 개수 - 1
- 노드간의 경로(임의의 노드에서 다른 노드로 가는 경로)는 유일하다.
- 루트노드를 제외한 모든 노드는 단 하나의 부모 노드만을 갖는다.
- 모든 노드는 서로 연결되어있다.
- 경로에서 엣지 하나를 자르면 트리가 두 개로 분리된다.

<br/>

### 1-3. Tree(트리)의 종류

**이진 트리(Binary Tree)** : 각 노드가 최대 두 개의 자식을 갖는 트리

cf) K-ary Tree : 각 노드가 최대 $k$ 개의 자식을 갖는 트리

이진트리를 기준으로 종류를 나누면 다음과 같다.

- **정이진트리(Full Binary Tree)** : 잎새노드를 제외한 모든 레벨이 꽉 채워진 이진트리

  <a href="https://imgur.com/edCd7lU"><img src="https://i.imgur.com/edCd7lU.png" width="200px" title="source: imgur.com" /></a>

  모든 노드의 개수 = $2^{k+1} - 1$ ($k$는 레벨)

- **완전이진트리(Complete Binary Tree)** : 마지막 레벨을 제외한 모든 레벨이 꽉 채워진 이진트리

  마지막 레벨은 꽉 안채워져 있어도 되지만, 노드가 **왼쪽부터** 채워져야 한다.

  <a href="https://imgur.com/mXssEqj"><img src="https://i.imgur.com/mXssEqj.png" width="200px" title="source: imgur.com" /></a>

- **균형이진트리(Balanced Binary Tree)** : 모든 잎새노드의 깊이 차이가 많아야 1인 이진트리

  <a href="https://imgur.com/hPuxfES"><img src="https://i.imgur.com/hPuxfES.png" width="200px" title="source: imgur.com" /></a>

  

앞서 공부한 [힙 정렬](https://taewonkimz.github.io/2020-01-14/Heapsort/)에 사용되는 max heap과 min heap은 모두 이진트리를 기반으로 만들어진 것이며, 앞으로 공부할 이진탐색트리(BST. Binary Search Tree)도 이진트리를 기반으로 만들어진 기법이다.

　*이진탐색트리 : 왼쪽 서브트리 $\leq$ 노드 $\leq$ 오른쪽 서브트리의 성질을 만족하는 이진트리*

<br/>

### 1-4. Tree Traversal(트리 순회)

트리순회 : 트리의 각 노드를 체계적인 방법으로 방문하는 과정

- Preorder(전위순회) : 노드 - 왼쪽 서브트리 - 오른쪽 서브트리
- Inorder(중위순회) : 왼쪽 서브트리 - 노드 - 오른쪽 서브트리
- Postorder(후위순회) : 왼쪽 서브트리 - 오른쪽 서브트리 - 노드

따라서, 다음 트리를 트리순회 방식대로 방문하면 다음과 같다.

<a href="https://imgur.com/zfrXerB"><img src="https://i.imgur.com/zfrXerB.png" width="150px" title="source: imgur.com" /></a>

> Preorder  : 1, 2, 4, 5, 3

> Inorder : 4, 2, 5, 1, 3

> Postorder : 4, 5, 2, 3, 1

만약 Binary Tree를 K-ary Tree로, 혹은 K-ary Tree를 Binary Tree로 바꾸고 싶다면 기존 Tree의 Tree Traversal 방식을 고려하여 바꿔주어야 한다.

<br/>

### 1-5. Tree(트리) 관련 알고리즘

- **트리의 높이**를 구하는 알고리즘

  아래 과정을 반복하는 재귀적 함수 작성. 탈출 조건은 더이상 더할 1이 없을 때!

  1. 왼쪽 서브트리의 높이와 오른쪽 서브트리의 높이를 구함

  2. 큰 값에 1을 더함(루트노드)

- **트리의 노드 수**를 구하는 알고리즘
  1. 왼쪽 서브트리로 가며 노드 수를 구하는 재귀함수 작성
  2. 오른쪽 서브트리로 가며 노드 수를 구하는 재귀함수 작성
  3. 두 재귀함수를 모두 더하고 최종적으로 1을 더함(루트노드)

- 트리의 **노드 중 최대값**을 구하는 알고리즘

  아래 과정을 반복하는 재귀적 함수 작성. 탈출 조건은 더이상 노드가 없을 때!

  1. 왼쪽 서브트리로 가며 최대값을 구함
  2. 오른쪽 서트리로 가며 최대값을 구함
  3. 1, 2의 값과 노드의 값을 비교해 최대값을 구함

<br/>

### 2-1. Queue

한쪽 끝으로 자료를 넣고, 반대쪽에서는 자료를 뺄 수 있는 자료구조

먼저 넣은 데이터가 먼저 나오는 FIFO(First In, First Out) 구조로 저장한다.[(그림출처)](https://monsieursongsong.tistory.com/5)

![](https://t1.daumcdn.net/cfile/tistory/2541CF34588E84760C)

위 그림에서는 Front, Rear이지만 Head, Tail로 바꿔 읽어주자.

Enqueue : 데이터 삽입. 큐에 새로운 데이터가 들어오면 큐의 끝 위치(Tail)에 저장됨

Dequeue : 데이터 삭제. 삭제할 때는 첫번째 위치(Head)의 요소가 삭제됨

<br/>

### 2-2. Queue(큐)의 구현

Enqueue와 Dequeue를 이용해 Queue를 구현한다. 구현 방식으로는 연결리스트를 이용하는 것과 배열을 이용하는 것이 있다.

다음의 enqueue와 dequeue의 예시로 Queue를 구현해보자.

> enqueue 5, enqueue 3, enqueue 1, dequeue, dequeue, enqueue 7

- 연결리스트로 구현

  <a href="https://imgur.com/e8jTWwp"><img src="https://i.imgur.com/e8jTWwp.png" width="350px" title="source: imgur.com" /></a>

  보이는 것처럼 enqueue를 하면 tail 위치에 삽입되고, dequeue를 하면 head 위치의 데이터가 삭제되는 것을 알 수 있다. 이런식으로 연결리스트를 이용해 큐를 구현할 수 있다.

  이때, enqueue의 경우 맨 끝 위치에 추가만 해주므로 시간복잡도는 $O(1)$이다.

  dequeue의 경우 맨 앞의 데이터를 삭제하고, 그 뒤에 있던 데이터들을 앞으로 한 칸씩 당겨줘야 하므로 시간복잡도는 $O(n)$이다.

- 배열로 구현

  <a href="https://imgur.com/W8XOGpU"><img src="https://i.imgur.com/W8XOGpU.png" width="250px" title="source: imgur.com" /></a>

  마찬가지로, enqueue의 경우 맨 끝 위치에 추가만 해주므로 시간복잡도는 $O(1)$이다.

  dequeue의 경우 맨 앞의 데이터를 삭제하고, 그 뒤에 있던 데이터들을 앞으로 한 칸씩 당겨줘야 하므로 시간복잡도는 $O(n)$이다.

<br/>

그렇다면 배열로 큐를 구현할 때, dequeue의 시간복잡도를 $O(1)$로 줄이려면 어떻게 해야할까?

Circular Array로 Queue를 구현하면 이를 해결할 수 있다. 즉, 위처럼 일련의 딱딱한 배열이 아니라, 원으로 Head와 Tail이 이어진 Circular Array를 이용하면 되는 것이다.

<a href="https://imgur.com/zzBmv5I"><img src="https://i.imgur.com/zzBmv5I.png" width="400px" title="source: imgur.com" /></a>

나중에 공부하겠지만 큐를 이용해서 "우선순위 큐"라는 것을 만들 수 있는데, 이는 우선순위를 가진 데이터를 저장하는 큐를 말한다. 즉, 일반적인 큐는 FIFO 방식대로 먼저 들어갔으면 먼저 나오게 되는데, 우선순위 큐는 들어간 순서에 상관없이 우선순위가 높은 데이터가 먼저 나오는 것이다.

<br/>

### 3-1. Stack(스택)

한쪽 끝에서만 자료를 넣고 뺄 수 있는 LIFO(Last In, First Out) 형식의 자료구조

책이 쌓여있는 것을 생각하면 쉽다. 쌓여있는 책 중 가장 최근에 놓은 책(가장 위에 있는 책)을 먼저 꺼낼 수 있는 것처럼 Stack도 가장 마지막에 넣은 데이터를 먼저 꺼낼 수 있는 것이다.

Push : 자료를 넣음

Pop : 자료를 꺼냄

만약 6, 4, 2를 차례대로 Push하고, 두 번 Pop한 다음, 7을 Push한다면 그 과정은 다음과 같다.

> 6 　...　6, 4　...　6, 4, 2　...　6, 4　...　6　...　6, 7

<br/>

### 3-2. Stack(스택)의 구현

Push와 Pop을 이용해 Stack을 구현한다. 구현 방식으로는 리스트, 연결리스트 등 다양한 자료구조로 가능하다.

리스트의 경우 파이썬 문법처럼 Append로 새 자료를 넣고, 제거할 때는 Pop하면 된다. 어떤 자료구조를 사용하던 각 행위의 시간복잡도는 모두 $O(1)$이다.

<br/>

### 3-3. Stack(스택)의 활용

Stack이 활용되는 대표적인 사례는 재귀함수이다.

- 재귀함수

  재귀함수란 지금 함수값을 구할 때 이전의 함수값을 이용하는 경우이다. 대표적인 예가 피보나치 수열이다.

  $F(n) = F(n-2) + F(n-1)$에서 $n = 3$일 때 $n = 1, 2$일 때의 값을 이용해야한다. 따라서 가장 최근의 함수값 2개를 필요로하기 때문에 가장 최근의 값이 먼저 나오도록 하는 Stack이 활용되는 것이다.

  

이밖에도 웹 브라우저의 방문기록(뒤로가기), 실행 취소(undo) 등에도 Stack이 활용된다.

<br/>

지금까지 자료구조로 Tree와 Queue, Stack에 대해 알아보았다.

이 밖에도 대표적인 자료구조로 Heap과 Graph가 있는데, [Heap](https://taewonkimz.github.io/2020-01-14/Heapsort/)은 이미 공부했고 Graph는 앞으로 자세히 공부할 예정이라 이 포스팅에는 적지 않았다.

<br/>