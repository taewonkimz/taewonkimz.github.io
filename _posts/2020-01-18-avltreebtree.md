---
layout : post
title : "참고 3. AVL Tree, B-Tree"
description :
date : 2020-01-18
category : Algorithms
tags : [Data Structure, AVL Tree, B-Tree]
use_math: true
comments : true
share : true

---

<br/>
Sanjoy Dasgupta가 저술한 책인 Algorithms과 [이기창님의 블로그](https://ratsgo.github.io/), [JLog](https://hyungjoon6876.github.io/jlog/2018/07/20/btree.html)를 참고하였다.

<br/>

앞서 BST를 공부했을 때, 높이가 $n$이 되는 최악의 BST는 다음과 같았다.

<a href="https://imgur.com/XR4fujQ"><img src="https://i.imgur.com/XR4fujQ.png" width="150px" title="source: imgur.com" /></a>

따라서 트리의 Balance를 맞춰주기 위해 AVL Tree와 B-Tree가 이용된다고 하였다.

<br/>

### 1-1. AVL Tree

**서브트리의 높이를 적절하게 제어해 전체 트리의 Balance를 맞춘 BST**. 왼쪽 서브트리와 오른쪽 서브트리의 높이 차이가 최대 1이다.

AVL Tree를 재귀적으로 정의하면 다음과 같다.

*어떤 노드의 왼쪽 서브트리의 높이와 오른쪽 서브트리의 높이의 차이의 절댓값이 1 이하인 성질이 리프노드로부터 루트노드로 갈수록 유지되는 트리*

AVL Tree의 핵심 개념 중 하나는 Balance Factor(BF)이다.

**BF** : 왼쪽 서브트리의 높이 - 오른쪽 서브트리의 높이

<a href="https://imgur.com/JxjSEnO"><img src="https://i.imgur.com/JxjSEnO.png" width="200px" title="source: imgur.com" /></a>

위 트리의 노드별로 BF를 구하면 다음과 같다. AVL Tree에서 가장 중요한 것은 트리의 균형을 맞춰주기 위해, 각 노드의 BF $\leq$ $\left\vert 1 \right\vert $이 되어야 한다는 것이다.

따라서 AVL Tree를 구현하기 위해서는, 요소를 삽입하거나 삭제하는 과정에서 서브트리를 재구성해 트리 전체의 균형을 맞춰주어야 한다. 이를 위해 시행되는 연산이 **rotation**이다.

<br/>

### 1-2. AVL Tree의 구현(삽입, 삭제)

- Single rotation

  <a href="https://imgur.com/q3VrlhW"><img src="https://i.imgur.com/q3VrlhW.png" width="400px" title="source: imgur.com" /></a>

  위 트리를 보자. U와 V는 노드이며 X, Y, Z는 서브트리이다. 이때, X의 자식노드가 생겨 U의 BF가 2가 된다고 하자. 이 경우 BF가 1을 넘으므로 rotation을 진행한다. 어떻게 하냐면, **비어있는 서브트리의 뒤꽁무니를 아래로 잡아당기는 것**이다. 여기서는 Z 쪽이 비어있으므로 Z를 잡고 아래로 당긴다. 그렇게 하여 V를 새로운 루트노드로 만드는 것이다. 동시에, **반대편의 서브트리 중 가까운 서브트리를 내려온 노드(U)의 서브트리로 가져온다**. 이 과정을 거치면, 오른쪽의 After Rotation 트리를 얻을 수 있다.

  1. 높이가 더 낮은 서브트리의 뒤꽁무니를 아래로 당긴다
  2. 기존 루트노드를 아래로 가져오고, 당겨지는 방향의 반대편에 있는 자식노드를 루트노드로 만든다. 
  3. 당겨지는 방향의 반대편에 있는 서브트리 중, 가까운 서브트리를 내려온 루트노드의 서브트리로 붙여준다.

  이렇게 복잡한 과정을 거치는 이유는 BST의 특징인 왼쪽 자식노드 $\leq$ 부모노드 $\leq$ 오른쪽 자식노드의 특징을 유지해야하기 때문이다. 저 방식대로만 rotation을 해준다면 위 규칙을 깨트릴 위험 없이 AVL Tree를 만들 수 있다. 예를 하나 보자.

  <a href="https://imgur.com/etDYy8r"><img src="https://i.imgur.com/etDYy8r.png" width="400px" title="source: imgur.com" /></a>

  rotation 과정을 거친 뒤에도 위의 대소 특성을 만족하며, BST의 트리 순회방식인 Inorder(왼 - 노 - 오) 방식대로 읽어보아도 0.8, 1, 3, 4, 5, 8 처럼 그 성질을 만족하는 것을 알 수 있다.

  더 명확한 정의를 하자면, single rotation은 left rotation과 right rotation으로 구분된다.

  <a href="https://imgur.com/ifikmO7"><img src="https://i.imgur.com/ifikmO7.png" width="400px" title="source: imgur.com" /></a>

  right rotation : 왼쪽 서브트리에 새 노드가 삽입되어 오른쪽 아래로 잡아당기는 경우

  left rotation : 오른쪽 서브트리에 새 노드가 삽입되어 왼쪽 아래로 잡아당기는 경우

  애니메이션으로 이 과정을 보면 다음과 같다.

  <a href="https://imgur.com/UdJtIAZ"><img src="https://i.imgur.com/UdJtIAZ.gif" title="source: imgur.com" /></a>

- Double rotation

  rotation을 2회 이상 시행해야 하는 경우를 Double rotation이라고 한다. 예를 보자.

  <a href="https://imgur.com/qCsLMlQ"><img src="https://i.imgur.com/qCsLMlQ.png" title="source: imgur.com" /></a>

  이 경우, U의 BF가 1을 초과하는 것을 알 수 있다.

  우선 V를 기준으로 left rotation을 해준다. 그러면 비어있는 서브트리인 A의 꽁무니를 잡고 아래로 당기게 되고, W가 루트노드가 된다. 그리고, 반대편 서브트리 중 가장 가까운 B가 내려온 V의 서브트리가 된다.

  이 과정을 거쳐도 U의 BF가 여전히 1을 초과한다. 따라서 rotation을 한번 더 진행한다.

  U를 기준으로 right rotation을 해준다. 그러면 비어있는 서브트리인 D의 꽁무니를 잡고 아래로 당기게 되고, W가 루트노드가 된다. 그리고, 반대편 서브트리 중 가장 가까운 C가 내려온 U의 서브트리가 된다.

  그 결과, 매우매우 균형적인 Tree가 완성된 것을 볼 수 있다.


<br/>

위 방식을 유념하여, AVL Tree를 구축해보자. 다음 숫자들을 순서대로 넣는다.

> 3, 2, 1, 4, 5, 6, 7, 16, 15, 14

<a href="https://imgur.com/wdJh60D"><img src="https://i.imgur.com/wdJh60D.png" width="150px" title="source: imgur.com" /></a>

트리의 속성(Inorder)대로 3, 2, 1을 넣어주었다. 이때 3의 BF가 1을 넘으므로 바로 rotation을 진행해준다. 이처럼, 숫자들을 넣어 트리를 구축하는 과정에서 어떤 노드의 BF가 1을 넘으면 곧바로 rotation을 해주는 것이다. 결과는 다음과 같다.(내려온 노드에 붙여줄 서브트리가 없으면 안붙여줘도 된다.)

<a href="https://imgur.com/KBkWut8"><img src="https://i.imgur.com/KBkWut8.png" width="170px" title="source: imgur.com" /></a>

이어서 4, 5를 넣어준다.

<a href="https://imgur.com/AXR4xZx"><img src="https://i.imgur.com/AXR4xZx.png" width="250px" title="source: imgur.com" /></a>

3의 BF가 1을 넘어버렸다. rotation을 해주면 다음과 같다.

<a href="https://imgur.com/MlraT9I"><img src="https://i.imgur.com/MlraT9I.png" width="200px" title="source: imgur.com" /></a>

이처럼 숫자를 넣는 과정에서 BF가 1을 넘으면 곧바로 rotation을 진행해주면서 트리를 구축하면 최종적으로 예쁜 AVL Tree를 만들 수 있다. 결과는 생략하겠다.

<br/>

### 1-3. AVL Tree의 시간복잡도

BST의 경우, 탐색과 삽입, 삭제를 하는 데 시간복잡도는 $O(\log_2n)$이었고, 최악의 경우 $O(n)$까지 높아진다고 하였다. 이때, 불균형 트리에 대해 AVL Tree를 구축한다고 하자.

먼저, 삽입을 보자. AVL Tree는 BST의 일종이므로 삽입을 하는데 $O(h)$ 시간이 소요된다. 이후, BF를 계산한다. BF 계산 대상이 되는 노드는 잎새노드 ~ 루트노드에 이르는 경로의 모든 노드이므로 $O(h)$만큼의 시간이 걸린다. 이후, rotation을 할 때는 그냥 부모-자식 위치만 변경해주면 되므로 $O(1)$만큼의 시간이 걸린다. 따라서 총 시간복잡도는 $O(h)$이다.

삭제할 때의 시간복잡도도 위와 동일하다. 이때, 노드 수가 $n$개이면 높이 $h$의 하한은 $2\log_2n$이라고 한다. 따라서 $O(h) = O(\log_2n)$이므로 AVL Tree의 시간복잡도는 $O(\log_2n)$이다.

<br/>

### 2-1. B-Tree

자식 노드의 개수가 2개 이상이며, 한 노드 내의 데이터가 1개 이상인 트리. 노드 내의 데이터 수가 $n$개이면 $n$차 B-Tree라고 명명한다.

<a href = "https://hyungjoon6876.github.io/jlog/2018/07/20/btree.html"><img src = "https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_3.png" width = "400px" title = "source : hyungjoon6876.github.io/"></a>

Binary Tree는 부모가 자식을 2개밖에 갖지 못하고, 균형이 맞지 않을 경우 시간복잡도가 $O(n)$으로 안 좋아진다. 이를 보완하기 위해, 이진트리를 확장해서 더 많은 수의 자식을 가질 수 있게 일반화 시킨 것이 B-Tree이다. 따라서 노드에 데이터를 추가로 넣음으로써 균형을 맞출 수 있다. 삭제 시에도 leaf로부터 root로 tree를 재구성하기 때문에 항상 균형을 유지할 수 있다.

AVL Tree가 BST를 아래로 잡아당기고, 자식노드와 부모노드를 바꾸는 과정을 통해 균형을 맞춰주었다면, B-Tree는 노드 내에 데이터를 더 넣고, 자식 노드를 2개 이상으로 허가해줌으로써 균형을 맞춰주는 것이다.

<br/>

### 2-2. B-Tree의 특징

- 노드의 데이터 수가 $n$개라면 자식 노드의 개수는 $n + 1$개이다.
- 노드의 데이터는 정렬되어 있어야한다.
- 노드의 데이터를 기준으로 왼쪽 자식노드는 작은 값, 가운데 자식노드는 사잇값, 오른쪽 자식노드는 큰 값이 위치해야한다.
- 4차 B-Tree부터 모든 노드는 적어도 $n/2$개의 데이터를 가져야한다.
- 잎새노드는 모두 같은 레벨에 존재해야한다.
- 입력자료는 중복될 수 없다.

<br/>

### 2-3. B-Tree의 구현

- 삽입

  3차 B-Tree를 이용해 다음의 데이터를 넣는 과정은 다음과 같다.

  > 5, 1, 7, 9, 12

  <a href = "https://hyungjoon6876.github.io/jlog/2018/07/20/btree.html"><img src = "https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_6.png" width = "600px" title = "source : hyungjoon.github.io"></a>

  1. 루트노드를 생성해 데이터를 삽입한다.

  2. 노드에 데이터가 꽉 차면, 노드를 분리한다.

  3. 분리된 노드에 B-Tree의 특성을 만족하도록 데이터를 삽입한다.

  4. 1 ~ 3을 반복한다.

- 삭제

  삭제는 삭제되는 노드가 리프노드인 경우와 그렇지 않은 경우로 나뉜다. BST를 삭제할 때 리프노드인지, 하나의 서브트리를 갖는지 두개의 서브트리를 갖는지로 나뉘었던 것을 비교한다면 꽤나 간단한 것을 알 수 있다.

  B-Tree의 삭제연산은 여러 경우가 있는데 그림으로 설명을 대체한다.

  예시 (1) 리프노드이고 삭제해도 다른 데이터가 남아있는 경우

  <a href = "https://hyungjoon6876.github.io/jlog/2018/07/20/btree.html"><img src = "https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_7.png" width = "450px" title = "source : hyungjoon6876.github.io/"></a>

  예시 (2) 리프노드이고 삭제되면 B-Tree 구조가 깨지는 경우

  <a href = "https://hyungjoon6876.github.io/jlog/2018/07/20/btree.html"><img src = "https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_8.png" width = "600px" title = "source : hyungjoon6876.github.io/"></a>

  예시 (3) 리프노드가 아닌 경우

  <a href = "https://hyungjoon6876.github.io/jlog/2018/07/20/btree.html"><img src = "https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_9.png" width = "400px" title = "source : hyungjoon6876.github.io/"></a>

  예시 (4)

  <a href = "https://hyungjoon6876.github.io/jlog/2018/07/20/btree.html"><img src = "https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_10.png" width = "600px" title = "source : hyungjoon6876.github.io/"></a>

<br/>

### 2-4. B-Tree의 시간복잡도

삭제, 삽입 모두 시간복잡도가 $O(\log_2n)$이다.

탐색, 삽입, 삭제 시에 BST와 AVL Tree, B-Tree의 시간복잡도를 비교하면 다음과 같다.

| BST  | Best, Average-Case | Worst-Case |
| :--: | :----------------: | :--------: |
| 탐색 |    $O(\log_2n)$    |   $O(n)$   |
| 삽입 |    $O(\log_2n)$    |   $O(n)$   |
| 삭제 |    $O(\log_2n)$    |   $O(n)$   |

| AVL Tree, B-Tree | Best, Average-Case |  Worst-Case  |
| :--------------: | :----------------: | :----------: |
|       탐색       |    $O(\log_2n)$    | $O(\log_2n)$ |
|       삽입       |    $O(\log_2n)$    | $O(\log_2n)$ |
|       삭제       |    $O(\log_2n)$    | $O(\log_2n)$ |

<br/>