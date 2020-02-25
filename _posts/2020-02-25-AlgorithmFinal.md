---
layout : post
title : "Algorithms Summary"
description :
date : 2020-02-25
category : Algorithms
tags : [Algorithms]
use_math: true
comments : true
share : true
---

<br/>

여태까지 배운 알고리즘에 관한 내용을 총 정리해보자.

<br/>

### 알고리즘 총정리

|                                                              | Description                                                  |      Time Complexity       |
| :----------------------------------------------------------: | :----------------------------------------------------------- | :------------------------: |
| **[Binary Search](https://taewonkimz.github.io/2020-01-17/2bst/)** | 오름차순으로 정렬된 리스트에서 특정한 값의 위치를 찾는 탐색 알고리즘. 중앙값을 기준으로 리스트를 이등분함 |        $O(\log n)$         |
| **[K-ary Search](https://taewonkimz.github.io/2020-01-17/2bst/)** | 오름차순으로 정렬된 리스트에서 특정한 값의 위치를 찾는 탐색 알고리즘. 중앙값을 기준으로 리스트를 $k$등분함 |        $O(\log_kn)$        |
|   **[BST](https://taewonkimz.github.io/2020-01-17/2bst/)**   | Binary Search를 기반으로 연결리스트를 이용하여 원하는 값을 탐색하는 알고리즘. 트리순회 방식을 기반으로 노드와 탐색값의 크기를 비교하며 탐색함 |  $O(\log n)$<br />$O(n)$   |
| **[AVL Tree](https://taewonkimz.github.io/2020-01-18/avltreebtree/)** | BF를 기반으로 서브트리의 높이를 적절하게 제어해 균형을 맞춘 BST |        $O(\log n)$         |
| **[B-Tree](https://taewonkimz.github.io/2020-01-18/avltreebtree/)** | 자식노드의 개수가 2개 이상이며 한 노드 내에 데이터가 1개 이상인 트리 |        $O(\log n)$         |
| **[Heap](https://taewonkimz.github.io/2020-01-14/Heapsort/)** | 완전이진트리의 일종으로, 데이터에서 최대/최소값을 빠르게 찾아내도록 만들어진 자료구조. 최대힙과 최소힙으로 구성됨 |        $O(\log n)$         |
| **[Insertion Sort](https://taewonkimz.github.io/2020-01-15/Anothersorting/)** | 배열의 앞에서부터 차례대로 이미 정렬된 앞부분과 비교하며 자신의 위치를 찾아 삽입하며 정렬하는 방법 |    $O(n)$<br />$O(n^2)$    |
| **[Bubble Sort](https://taewonkimz.github.io/2020-01-15/Anothersorting/)** | 서로 인접한 두 원소를 비교하여 크기 순서대로 정렬하는 방법. 여러 번의 회전을 통해 정렬이 이루어짐 |          $O(n^2)$          |
| **[Selection Sort](https://taewonkimz.github.io/2020-01-15/Anothersorting/)** | 최대/최소값을 찾은 뒤 맨 뒤/앞과 교환하며 정렬하는 방법. 여러 번의 회전을 통해 정렬이 이루어짐 |          $O(n^2)$          |
| **[Merge Sort](https://taewonkimz.github.io/2020-01-12/Mergesort/)** | 데이터를 쪼갤 수 없을 때까지 쪼갠 뒤, 둘씩 크기를 비교해 정렬하며 합치는 방법 |        $O(n\log n)$        |
| **[Quick Sort](https://taewonkimz.github.io/2020-01-13/Quicksort/)** | 리스트의 pivot을 선택한 뒤, pivot보다 작은 값과 큰 값으로 리스트를 둘로 분할하며 정렬하는 방법 | $O(n\log n)$<br />$O(n^2)$ |
| **[Heap Sort](https://taewonkimz.github.io/2020-01-14/Heapsort/)** | 데이터를 최대/최소힙 트리로 구성해 정렬하는 방법             |        $O(n\log n)$        |
|  **[DFS](https://taewonkimz.github.io/2020-01-21/dfsbfs/)**  | 하나의 시작 정점에서 출발해 더이상 나아갈 엣지가 없을 때까지 깊이 탐색하는 그래프 순회기법 |          $O(V+E)$          |
|  **[BFS](https://taewonkimz.github.io/2020-01-21/dfsbfs/)**  | 각 노드에 인접한 모든 노드를 우선 방문하는 그래프 순회기법   |          $O(V+E)$          |
| **[Dijkstra](https://taewonkimz.github.io/2020-01-23/dijkstra/)** | 하나의 정점에서 다른 모든 정점까지의 최단경로를 구함         | $O(E\log V)$<br />$O(V^2)$ |
| **[Bellman-Ford](https://taewonkimz.github.io/2020-01-24/bellmanford/)** | 하나의 정점에서 다른 모든 정점까지의 최단경로를 구함. 음수 가중치를 갖는 간선에 이용할 수 있음 |          $O(V^3)$          |
| **[Floyd-Warshall](https://taewonkimz.github.io/2020-02-23/DP3/)** | 여러 정점에서 모든 정점까지의 최단경로를 구함. 각 정점을 경유할 때 경로가 짧아지는지 아닌지를 검사함 |          $O(V^3)$          |
| **[Kruskal](https://taewonkimz.github.io/2020-02-15/MST/)**  | 그래프에서 가중치가 최소인 엣지를 사이클이 존재하지 않도록 순서대로 고르며 트리를 만들어 MST를 구성하는 알고리즘 |        $O(E\log E)$        |
|   **[Prim](https://taewonkimz.github.io/2020-02-15/MST/)**   | 시작 정점과 가장 인접한 정점을 선택해 트리를 확장하고, 만들어진 트리와 가장 인접한 정점을 선택해 트리를 확장해나가는 과정을 반복하며 MST를 구성하는 알고리즘 |        $O(E\log V)$        |
| **[Huffman Coding](https://taewonkimz.github.io/2020-02-16/greedyetc/)** | 그리디 알고리즘을 이용해 데이터를 2진수로 압축시키는 기법    |        $O(n\log n)$        |
| **[Set Cover](https://taewonkimz.github.io/2020-02-16/greedyetc/)** | 전체집합의 부분집합 중, 가장 적은 개수를 골라서 그들의 합집합이 전체집합이 되도록 하는 문제 |          $O(n^3)$          |
|   **[LIS](https://taewonkimz.github.io/2020-02-21/DP1/)**    | 수열 내에서 증가하는 순서대로 숫자를 고르면서 부분수열의 길이가 최대인 수열을 구하는 알고리즘 |        $O(n\log n)$        |
| **[Edit distance](https://taewonkimz.github.io/2020-02-21/DP1/)** | 두 문자열이 같아지기 위해 필요한 연산의 최대 횟수를 구하며 문자열간의 유사도를 알아내는 알고리즘 |          $O(mn)$           |
| **[Knapsack](https://taewonkimz.github.io/2020-02-22/DP2/)** | 일정 가치아 무게가 있는 짐을 배낭에 넣을 때, 배낭의 용량을 넘지 않는 선에서 짐들의 가치의 합이 최대가 되도록 짐을 고르는 문제 |          $O(nW)$           |
| **[Chain matrix multiplication](https://taewonkimz.github.io/2020-02-22/DP2/)** | 두 개 이상의 행렬을 곱할 때 곱셈횟수가 최소가 되도록 결합법칙을 구하는 문제 |          $O(n^3)$          |
|   **[TSP](https://taewonkimz.github.io/2020-02-23/DP3/)**    | 시작점에서 출발해 모든 도시들을 한번씩 방문하여 다시 돌아오는 데 걸리는 최단 시간을 구하는 문제 |        $O(n^2 2^n)$        |
| **[Independent sets in trees](https://taewonkimz.github.io/2020-02-23/DP3/)** | 하나의 트리 내에서 가장 큰 독립집합을 찾는 문제              |           $O(n)$           |



























