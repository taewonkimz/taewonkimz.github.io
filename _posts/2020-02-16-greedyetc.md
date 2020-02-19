---
layout : post
title : "5. Greedy Algorithm (3) Huffman Coding, Set Cover"
description :
date : 2020-02-16
category : Algorithms
tags : [Greedy Algorithm, Huffman Coding, Set Cover]
use_math: true
comments : true
share : true

---

<br/>
Sanjoy Dasgupta가 저술한 책인 Algorithms과 [햄과함께IT](https://withhamit.tistory.com/12)님의 블로그를 참고하였다.

<br/>

### 1-1. Huffman Coding(허프만 코딩)

그리디 알고리즘을 이용해 데이터를 2진수로 압축시키는 기법. 빈도가 높은 값에 대해서는 짧은 코드로 인코딩하고 빈도가 낮은 값에 대해서는 긴 코드로 인코딩함.

데이터는 Symbol 별로 Code가 주어지고 Frequency가 주어진다. 아래 표를 보자.

| Symbol | Code | Frequency |
| ------ | ---- | --------- |
| A      | 00   | 6         |
| B      | 01   | 2         |
| C      | 10   | 3         |
| D      | 11   | 1         |

위 경우 데이터를 저장하는데 6x2 + 2x2 + 3x2 + 1x2 = 24비트가 필요한 것을 알 수 있다.  
하지만 필요 비트를 더 줄일 수 있지 않을까? ㅇㅇ 허프만 코딩을 이용하면 가능하다.

허프만 코딩 알고리즘의 작동 과정은다음과 같다.

1. 빈도수가 낮은 것부터 merge 해서 이들의 합을 부모노드로 함
2. 그 다음 빈도수를 1의 부모노드와 merge하여 이들의 합을 부모노드로 함
3. 더이상 merge할 빈도수가 없을 때까지 반복

이때, **우측 노드는 반드시 좌측 노드보다 크거나 같아야한다 (좌측 노드 $\leq$ 우측노드)**  
만약 2번 과정에서 위 규칙을 지킬 수 없다면 반대편 서브트리에서 해당 과정을 진행한다.

*참고 ! 허프만 코딩을 왜 그리디 알고리즘을 이용해 구현할까 ?*  
*허프만 코딩은 빈도수가 낮은 것부터 merge하는 과정을 반복하며 이진 트리를 구축한다. 이때, prefix code가 겹치지 않도록 구축해야 하기 때문에 최소를 추구하는 그리디 알고리즘을 사용하는 것이다.*

<br/>

말로는 이해하기 어려우니 그림을 보자.

<a href = "https://withhamit.tistory.com/12"><img src = "https://t1.daumcdn.net/cfile/tistory/998A4C435BD6F62610" width = "500px" title = "source : withhamit.tistory.com/12"></a>

각 Symbol별로 빈도수가 나타나있다. 허프만 코드를 만들기 위해서는 먼저 트리를 만들어야 한다. 이때, 앞서 설명한 것처럼 빈도수가 낮은 것끼리 merge하며 이들의 합을 부모노드로 하는 과정을 반복한다.

첫번째 단계는 다음과 같다.

<a href = "https://withhamit.tistory.com/12"><img src = "https://t1.daumcdn.net/cfile/tistory/992084435BD6F62609" width = "450px" title = "source : withhamit.tistory.com/12"></a>

빈도수가 낮은 1과 2를 merge하였고, 이들의 합인 3을 부모노드로 하였다. 그리고 이 3과 그 다음 빈도수인 C : 3을 merge 한다. 결과는 아래와 같다.

<a href = "https://withhamit.tistory.com/12"><img src = "https://t1.daumcdn.net/cfile/tistory/99180E435BD6F62617" width = "500px" title = "source : withhamit.tistory.com/12"></a>

이 과정을 쭉 ~ 반복하면 아래와 같이 허프만 코딩이 완료된 최종 결과를 얻을 수 있다.

<a href = "https://withhamit.tistory.com/12"><img src = "https://t1.daumcdn.net/cfile/tistory/99839F435BD6F62603" width = "400px" title = "source : withhamit.tistory.com/12"></a>

위의 결과에서 1, 2부터 차근차근 merge되다가 갑자기 D : 4와 E : 5가 다른 서브트리에서 merge된 이유는 3과 C : 3의 합인 부모노드 6이 이들보다 크기 때문이다("좌측 노드 $\leq$ 우측노드"를 지키지 못함).  
따라서 D와 E는 반대편 서브트리에서 merge 해준 것이고, 그 다음 빈도수인 F : 6을 기존에 있던 6과 merge 해주었다. **이렇게 완성한 트리 노드의 왼쪽 간선에는 0, 오른쪽 간선에는 1의 가중치를 둔다.**

루트노드로부터 이어진 간선들의 가중치들의 합이 허프만 코드(가변 길이 코드)가 된다.  
EX) A : 1-0-0-0, 　E : 0-1

트리의 비용은 루트노드를 제외한 노드들과 모든 잎들의 빈도수의 합이다. 참고만 해두자.

<br/>

### 1-2. Huffman coding pseudocode

```python
C : n개의 문자로 이루어진 문자열
|C| : C의 문자 개수
Q : 최소 우선순위 큐
EXTRACT-MIN : 큐에서 가장 최솟값 추출

n = |C|
Q = C
for i = 1 to n - 1
   z.left = x = EXTRACT-MIN(Q)
   z.right = y = EXTRACT-MIN(Q) 
   z.freq = x.freq + y.freq
   INSERT(Q, z)
return EXTRACT-MIN(Q) 
```

<br/>

### 1-3. Huffman Coding 시간복잡도

문자를 탐색할 때 트리의 높이만큼 $O(\log n)$ 시간이 소요되고, 최악의 경우 모든 문자를 탐색해야 하므로 문자의 개수인 $O(n)$ 시간이 소요된다. 따라서 최종 시간복잡도는 이들의 곱인 $O(n\log n)$이다.

<br/>

### 2-1. Set Cover(집합덮개 문제)

전체 집합 $U$와 부분집합 $S$가 주어졌을 때, 부분집합 $S$ 중 가장 적은 집합을 골라서 그들의 합집합이 전체 집합 $U$가 되도록 부분집합 $S$를 선택하는 문제.

<br/>

### 2-2. Set Cover 시간복잡도

전체집합 $U$의 원소 개수가 $n$개일 때, 이들의 부분집합을 각각 $U$와 비교해 일치하는지 확인해야 한다.  
따라서 부분집합 $n^2$개를 각각 $n$번 반복하여 비교하므로 시간복잡도는 $O(n^3)$이다.

<br/>