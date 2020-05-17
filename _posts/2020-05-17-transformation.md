---
layout : post
title : "4. Linear Transformation, Image, Kernel"
description :
date : 2020-05-17
category : Linear Algebra
tags : [Linear Transformation, Image, Kernel]
use_math: true
comments : true
share : true
---

<br/>
Marc Peter Deisenroth외 2인이 저술한 책인 Mathematics for Machine Learning과 Gilbert Strang이 저술한 책인 Introduction to Linear Algebra, 그리고 카이스트 주재걸 교수님의 [인공지능을 위한 선형대수](https://www.edwith.org/linearalgebra4ai) 강의를 참고하였다.

<br/>

### 1. Linear Transformation(선형 변환) = Linear Mapping

 Vector space $V, W$에 대해 $\phi : V \rightarrow W$를 아래 조건을 만족하며 수행하는 것

[선형변환의 조건]

벡터의 합 조건 : $\phi(x+y) = \phi(x) + \phi(y)$

스칼라 곱 조건 : $\phi(\lambda x) = \lambda\phi(x)$

즉, vector space $V$로부터 $W$의 함수 $T$가 벡터의 합 조건과 스칼라 곱 조건을 만족한다면, 함수 $T$를 $V$로부터 $W$로의 linear transformation이라고 한다.

선형변환의 예를 들면 다음과 같다.

$$T\begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} = \begin{bmatrix} 1 \\ 2 \end{bmatrix}, T\begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} = \begin{bmatrix} 4 \\ 3 \end{bmatrix}, T\begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} = \begin{bmatrix} 5 \\ 6 \end{bmatrix}$$

$$x = \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = x_1\begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} + x_2\begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} + x_3\begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}$$

$$\rightarrow 　T(x) = T(x_1\begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} + x_2\begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} + x_3\begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix})$$

$$\rightarrow 　x_1T\begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} + x_2T\begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} + x_3T\begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}$$

$$\rightarrow 　x_1\begin{bmatrix} 1 \\ 2 \end{bmatrix} + x_2\begin{bmatrix} 4 \\ 3 \end{bmatrix} + x_3\begin{bmatrix} 5 \\ 6 \end{bmatrix} = \begin{bmatrix} 1 & 4 & 5 \\ 2 & 3 & 6 \end{bmatrix}\begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = Ax$$

<br/>

### 2. ONTO and ONE-TO-ONE

선형변환을 제대로 이해하기 위해서는 함수의 특징에 대해 면밀히 알아야 한다.

| 특징       |                  | 설명                                                         |
| ---------- | ---------------- | ------------------------------------------------------------ |
| Injective  | 단사(ONE-TO-ONE) | $\forall x, y \in V : \phi(x) = \phi(y) \rightarrow x = y$<br />일대일 대응. 정의역의 한 원소는 공역의 단 하나의 값에 대응된다.<br />선형독립일때(해가 단 하나 일때) ONE-TO-ONE이다. |
| Surjective | 전사(ONTO)       | $\phi(V) = W$<br />공역의 값($W$)을 만족하는 정의역의 원소($V$)가 하나라도 존재한다. |
| Bijective  | 전단사           | Injective and Surjective. 일대일 대응                        |

정의역의 원소 개수를 $n$, 공역의 개수를 $m$이라 할 때
$n < m$ 이면 Surjective할 수 없고, $n > m$이면 Injective할 수 없다.

다음으로 함수의 사상에 대해 알아보자.

| 사상         |                    | 설명                                                         |
| ------------ | ------------------ | ------------------------------------------------------------ |
| Isomorphism  | 동형               | $\phi : V \rightarrow W$가 linear, bijective한 경우          |
| Endomorphism | 준동형             | $\phi : V \rightarrow V$가 linear(정의역과 공역이 같은)한 경우 |
| Automorphism | 자기동형(자기대칭) | $\phi : V \rightarrow V$가 linear, bijective한 경우          |

- 유한한 차원의 vector space $V, W$에 대하여 dim($V$) = dim($W$)이면 $V$와 $W$는 isomorphic하다.
- Linear mapping $\phi : V \rightarrow W$ and $\theta : W \rightarrow X$일 때 $\phi$ o $\theta$ : $V \rightarrow X$는 linear하다.
- 어떠한 함수가 Isomorphism하다면, 그 역도 lsomorphism하다.
- 두 함수가 linear하다면 함수들의 합과, 스칼라 곱의 합도 linear하다.

<br/>

### 3. Matrix Representation of Linear Transformation

Linear Transformation을 하게 되면 이전 vector space의 basis는 이후 vector space의 basis의 선형결합으로 표현 가능하다.

다시 말해, vector space $V, W$의 basis를 각각 $B = (b_1, \cdots, b_n), C = (c_1, \cdots, c_n)$이라고 할 때, Linear mapping $\phi : V \rightarrow W$가 있으면 $j \in$ {$1, \cdots, n$}에 대하여 $\phi(b_j) = \alpha_{1j}c_1 + \cdots + \alpha_{mj}c_m = \sum_{i=1}^m\alpha_{ij}c_i$로 나타낼 수 있다.

이때, $\phi$의 transformation matrix = $A_\phi(i, j) = \alpha_{ij}$이다.
또, vector를 기저들을 전개할 때의 계수를 표현한 것을 알 수 있는데 여기서는 $\alpha$가 이에 해당되며, 이를  coordinate vector라고 한다.

위 표현 방식에 대하여 예를 들면 다음과 같다.

$$\phi : V \rightarrow W, B = (b_1, b_2, b_3), C = (c_1, c_2, c_3, c_4)$$

$$\phi(b_1) = c_1 - c_2 + 3c_3 - c_4$$

$$\phi(b_2) = 2c_1 + c_2 + 7c_3 + 2c_4$$

$$\phi(b_3) = 3c_2 + c_3 + 4c_4$$

$$\rightarrow 　A_\phi = \begin{bmatrix} \alpha_1, \alpha_2, \alpha_3 \end{bmatrix} = \begin{bmatrix} 1 & 2 & 0 \\ -1 & 1 & 3 \\ 3 & 7 & 1 \\ -1 & 2 & 4 \end{bmatrix}$$

<br/>

### 4. Image and Kernel

Image(range) : $V$에서 $W$로 mapping될 때 **reached**될 수 있는 벡터 = $Im(\phi)$

Kernel(null space) : $V$에서 $W$로 mapping될 때 0이 되는 벡터 = $Ker(\phi)$



- null space는 empty하지 않다
- $Ker(\phi)$은 $V$의 subspace, $Im(\phi)$는 $W$의 subspace이다.
- $Ker(\phi)$ = {0}이면 일대일 대응(Injective)
- vector space $A$에 대하여$(A \in R^{m \times n})$ $Im(\phi)$ = span$[a_1, \cdots, a_n]$
- $A$의 column들의 span의 image는 마찬가지로 $A$의 column space
- Column space(Image)는 $R^m$의 subspace이며, 이때 $m$을 "height"라고 한다.
- $rk(A) = dim(Im(\phi))$
- Kernel, null space는 $Ax = 0$의 general solution
- $A \in R^{m \times n}$일 때, Kernel은 $R^n$의 subspace이며 $n$은 "Width"이다. Image는 $R^m$의 subspace이며 $m$은 "height"이다.

※ 참고 : rank - nullity theorem(계수-퇴화차수 정리). $\phi : V \rightarrow W$ 일때

- $dim(Ker(\phi)) + dim(Im(\phi)) = dim(V)$
- $dim(Im(\phi))$ = pivot column의 수
- $dim(Ker(\phi))$ = non-pivot column(free column)의 수
- If $dim(Im(\phi)) < dim(V) 　\rightarrow 　dim(Ker(\phi)) \geq 1$
- If $dim(V) = dim(W) 　\rightarrow 　Im(\phi) \in W 　\rightarrow 　$ 　$\phi$는 injective, surjective, bejective























