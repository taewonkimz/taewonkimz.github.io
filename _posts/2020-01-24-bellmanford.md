---
layout : post
title : "4. Paths in Graphs (3) Bellman-Ford Algorithm"
description :
date : 2020-01-24
category : Algorithms
tags : [Graph, Shortest Path, Bellman-Ford]
use_math: true
comments : true
share : true

---

<br/>
Sanjoy Dasgupta가 저술한 책인 Algorithms과 [이기창님의 블로그](https://ratsgo.github.io/)를 참고하였다.

<br/>

### 1. Bellman-Ford Algorithm

벨만-포드 알고리즘은 [최단경로문제](https://taewonkimz.github.io/2020-01-22/shortestpath/) 중, 하나의 정점에서 다른 모든 정점까지의 최단경로를 구하는 알고리즘이다. 이전에 배운 다익스트라 알고리즘과 목적은 같지만, 벨만-포드 알고리즘의 경우 음수 가중치를 갖는 간선에 이용할 수 있다는 특징이 있다.

최단경로는 같은 정점을 2번 지날 일이 없다. 즉, 최단경로의 간선은 많아봐야 $\left\vert V \right\vert - 1$개일 것이다. 벨만-포드 알고리즘은 이 사실에 기반하여 만들어진 알고리즘이다. 벨만-포드 알고리즘은 모든 엣지에 대한 Edge-Relaxation을 $\left\vert V \right\vert - 1$번 수행한다.

알고리즘은 다음과 같다.

1. 모든 노드를 무한대로 설정
2. 시작노드 선택. 시작노드로부터 시작노드까지 거리는 0이므로 노드의 숫자를 0으로 설정
3. 시작노드와 인접한 노드들의 거리 업데이트
4. 각 노드를 순환하며 거리 업데이트

그림으로 설명하면 다음과 같다.

<a href="https://imgur.com/JGvQFVi"><img src="https://i.imgur.com/JGvQFVi.png" title="source: imgur.com" /></a>

먼저 시작노드를 $A$로 설정한다. 그 뒤, Order 순서에 따라 Edge Relaxation을 수행한다.

$(B,E)$부터 $(C,D)$까지는 무한대 - 무한대이기 때문에 Edge Relaxation이 수행되지 않는다. 이어서 $(A,B), (A,C), (A,D)$에 따라 거리정보를 업데이트 해주면 상단 우측 그림과 같다. 이렇게 첫번째 Edge Relaxation이 끝났다.

<a href="https://imgur.com/01Be9h5"><img src="https://i.imgur.com/01Be9h5.png" title="source: imgur.com" /></a>

두번째 Edge Relaxation이 시작되었다. $(B,E)$의 경우 8 - 2 = 6이기 때문에 $E$를 6으로 업데이트 해준다. $(C, E)$는 -2 + 3 = 1이고, 이는 기존의 6보다 작으므로 1을 기록해준다. 이렇게 Edge Relaxation을 Order에 따라 반복하면 된다. 이해했으니 나머지 설명은 생략

여하튼 벨만-포드 알고리즘은 이렇게 시작노드를 제외한 나머지 모든 노드 수만큼 Edge Relaxation을 수행해준다. 위 그래프에서 노드는 6개이고 시작노드를 제외하면 5개이므로 5번 Edge Relaxation을 수행해주는 것이다. 물론 5번 다 할 필요는 없다. 최대 5번인 것이고 위 그래프도 4번 진행하면 이후부터는 바뀌지 않는다.

다른 그림으로 예를 들면 아래와 같다. 이 과정은 Edge Relaxation을 1번 진행한 것이다.

<a href="https://imgur.com/hcWT22F"><img src="https://i.imgur.com/hcWT22F.png" title="source: imgur.com" /></a>

<br/>

### 2. Bellman-Ford Algorithm 특징

벨만-포드 알고리즘은 이처럼 음수 가중치를 갖는 간선이 있는 그래프에 적용할 수 있다. 하지만, 만약 **음수 가중치가 사이클을 이루고 있다면 작동하지 않는다.**

<a href="https://imgur.com/46tJqd7"><img src="https://i.imgur.com/46tJqd7.png" width="400px" title="source: imgur.com" /></a>

위 그림에서 $c, d$의 경우 양수 사이클이므로 사이클을 돌 수록 경로 길이가 커져 최단경로를 구하는 데에 문제가 되지 않는다. 하지만 $e, f$의 경우는 음수 사이클이므로 사이클을 돌 수록 경로 길이가 짧아져 최단경로를 계~속 구해버리는 오류에 빠지게 된다. 따라서 만약 Edge Relaxation의 시행 횟수가 $\left\vert V \right\vert - 1$번을 넘어가 버린다면 알고리즘은 false를 반환하고 종료된다. 이를 *벨만-포드 알고리즘의 정확성* 이라고 한다.

<br/>

### 3. Bellman-Ford Algorithm 시간복잡도

시작노드를 제외한 나머지 모든 노드에 대해 Edge Relaxation을 진행하므로 $O(\left\vert V \right\vert - 1)$ 시간이 소요된다.  
그리고 이 과정에서 모든 엣지에 대해 Edge Relaxation을 수행하므로 $O( \left\vert E \right\vert)$ 시간이 소요된다.

따라서 최종 시간복잡도는 $O(\left\vert EV \right\vert)$이고, 보통 dense graph의 경우 $\left\vert E \right\vert \approx \left\vert V^2 \right\vert$이므로 최종 시간복잡도는 $O(\left\vert V^3 \right\vert)$이 된다. 다익스트라 알고리즘의 $O(\left\vert V^2 \right\vert)$보다는 오래 걸리지만, 음수 가중치에도 적용할 수 있기 때문에 그렇게 나쁘지만은 않다는 것을 알 수 있다.

<br/>



































