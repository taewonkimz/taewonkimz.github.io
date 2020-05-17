---
layout : post
title : "3. Linear Independence, Subspace, Basis, Rank"
description :
date : 2020-05-17
category : Linear Algebra
tags : [Linear Independence, Subspace, Basis, Rank]
use_math: true
comments : true
share : true

---

<br/>
Marc Peter Deisenroth외 2인이 저술한 책인 Mathematics for Machine Learning과 Gilbert Strang이 저술한 책인 Introduction to Linear Algebra, 그리고 카이스트 주재걸 교수님의 [인공지능을 위한 선형대수](https://www.edwith.org/linearalgebra4ai) 강의를 참고하였다.

<br/>

### 1. Linear Independence

벡터 $x_1, x_2, \cdots, x_n$이 있을 때 **모든 계수가 0인 경우를 제외하고** 어떠한 선형결합으로도 0을 만들 수 없을 때

$\lambda x_1 + \cdots + \lambda x_n = 0$의 solution이 $\lambda_1 = \cdots = \lambda_k = 0$ 밖에 없을 때

행렬 $A$의 nullspace가 오직 zero vector만 존재할 때

어떤 벡터가 다른 벡터들의 선형결합으로 표현되지 않을 때(Span에 없을 때) Linear Independece하다고 한다.

cf) 종속(Dependence) : 선형결합을 취할 때, $\lambda_1 = \cdots = \lambda_k = 0$인 경우를 제외하고도 결과값이 0인 경우

- 벡터는 Lineary Dependent 하거나 Independent 하다(둘중 하나)
- 벡터 $x_1, \cdots, x_n$ 중 하나라도 0이면 dependent(0인 벡터에 아무거나 곱해도 0이 되므로)
- 벡터들이 수직이면 dependent
- 하나의 벡터가 다른 벡터의 선형결합이면 dependent
- Gaussian Elimination을 했을 때
  - basic variable만 존재 : independent
  - free variable만 존재 : dependent

| Dependent                                      | Independent                                  |
| ---------------------------------------------- | -------------------------------------------- |
| 어떤 column을 다른 column으로 나타낼 수 있다   | 어떤 column을 다른 Column으로 나타낼 수 없다 |
| Nullspace가 zero vector말고 다른 것도 존재한다 | Nullspace가 zero vector밖에 없다             |
| Free column이 있다                             | Free column이 없다                           |
| Special Solution이 있다                        | Special Solution이 없다                      |
| 방정식의 개수 > 벡터의 개수                    | Full column rank이다                         |

dependenct한 vector들은 당연히 span을 팽창하지 않는다. 또, dependent하면 당연히 해가 무수히 많다.

<br/>

### 2. Subspace

vector space의 부분집합. 임의의 $n$차원 공간에 대해 $n$차원 공간에 포함되면서 $n$차원 벡터들에 대해 선형결합이 성립하는(선형결합에 닫혀있는) 작은 공간.

| Subspace     | 설명                                                         |
| ------------ | :----------------------------------------------------------- |
| Column space | Column들의 linear combination으로 형성된 subspace.<br />$Ax = b$에서 $b$가 $A$의 columns space에 존재해야 해를 구할 수 있다.<br />즉, 벡터 $b$가 $A$의 column의 linear combination으로 표현이 가능해야 해를 구할 수 있다. |
| row space    | row들의 linear combination으로 형성된 subspace               |
| null space   | $Ax = 0$이 되는 벡터 $x$의 집합($x$들의 linear combination으로 형성되는 공간)<br />special solution들의 linear combination이며 zero vector를 반드시 포함한다.<br />A를 Elimination해서 $Ax = 0$을 만족시키는 $x$를 구함으로써 null space를 구할 수 있다.<br />만약 free variable의 개수가 0개라면 모두 선형 독립이므로 이때 null space는 zero vector가 된다. |

추가로, 아래의 Basis에 대한 설명을 보고 와서 다음 표를 보도록 하자.

[표 : Four Subspaces의 basis와 차원 (A = m x n matrix)]

| 종류             | 이름            | 식           | Basis                          | 차원  |
| ---------------- | --------------- | ------------ | ------------------------------ | ----- |
| $C(A) \in R^m$   | Column space    | $ y = Ax$    | $A$의 pivot columns 개수       | $r$   |
| $N(A) \in R^n$   | Null space      | $Ax = 0$     | $A$의 free columns 개수        | $n-r$ |
| $C(A^T) \in R^n$ | Row space       | $y = A^Tx$   | $A^T$의 pivot columns 개수     | $r$   |
| $N(A^T) \in R^m$ | Left null space | $y^TA = 0^T$ | $A^Tx = 0$의 free columns 개수 | $m-r$ |

<br/>

### 3. Basis(기저)

Subspace를 span하는 선형독립인 벡터를 말한다. 더 쉽게 말하면, 서로 선형 독립이면서 vector space를 span하는 minimal한 벡터들의 집합이다.

- 모든 벡터들은 basis vector들의 유일한 선형결합이다.(모든 선형결합은 unique)하다.
- 모든 vector space는 기저를 갖는다.
- 모든 기저는 같은 수의 element를 갖는다
- **vector space의 차원 = 해당 vector space의 basis vector의 수**
- invertible한 모든 n x n matrix의 column들은 $R^n$에 대한 basis이다.
- Basis는 unique하지 않다.

Basis는 Gaussian Elimination으로 확인 가능하다. pivot columns가 independent하기 때문이다.

$$\begin{bmatrix} 1 & 2 & 3 & -1 \\ 2 & -1 & -4 & 8 \\ -1 & 1 & 3 & -5 \\ -1 & 2 & 5 & -6 \\ -1 & -2 & -3 & 1 \end{bmatrix} 　\rightarrow 　\begin{bmatrix} 1 & 2 & 3 & -1 \\ 0 & 1 & 2 & -2 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0\end{bmatrix} $$

여기서 pivot columns가 independent하므로 $x_1, x_2, x_4$는 linearly independent하다. 따라서 이들은 Basis이다.

<br/>

### 4. Rank

선형독립인 column들의 개수 = column space의 차원 = column space의 기저벡터 개수 = pivot column의 개수

- If $rk(A) = rk(A^T)$ : column rank = row rank
- $A$의 column들이 subspace $U$를 span하면 $rk(A) = dim(U)$
- n x n matrix $A$가 역행렬을 가지면 $rk(A) = n$
- m x n matrix $A$에 대해 $Ax = 0$의 solution들의 subspace의 차원은 $n - rk(A)$이다.
- If $rk(A) = A$의 차원이라면 이는 full rank임을 의미한다.
- $Ax = b$가 해를 가지기 위해서는 $rk(A) = rk(A | b)$이여야 한다.



| Full column rank                             | Full row rank                    |
| -------------------------------------------- | -------------------------------- |
| m x n matrix에서 $r = n$일 때                | m x n matrix에서 $r = m$일 때    |
| free column이 없음                           | free column은 $n - m$개          |
| column들이 서로 independent                  | column들이 서로 dependent        |
| null space는 오직 zero vector 뿐             | nullspace 존재                   |
| unique한 해를 가지며 $rk(A) = A$의 차원이다. | 해의 개수가 1개 또는 무수히 많다 |

<br/>
