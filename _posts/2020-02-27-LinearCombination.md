---
layout : post
title : "2. Linear Combination, Vector Space, Span"
description :
date : 2020-02-27
category : Linear Algebra
tags : [Linear Algebra, Linear Combination, Vector Space, Span]
use_math: true
comments : true
share : true
---

<br/>
Marc Peter Deisenroth외 2인이 저술한 책인 Mathematics for Machine Learning과 Gilbert Strang이 저술한 책인 Introduction to Linear Algebra, 그리고 카이스트 주재걸 교수님의 [인공지능을 위한 선형대수](https://www.edwith.org/linearalgebra4ai) 강의를 참고하였다.

<br/>

### 1. Linear Combinations(선형 결합)

스칼라 곱과 벡터의 덧셈을 조합하여 새로운 벡터를 얻는 연산. 간단히 말하면 벡터의 상수배들의 연산이다. 예를 들어 벡터가 $v_1, v_2, \dots, v_p$이고 스칼라가 $c_1, c_2, \dots, c_p$일 때, $c_1v_1 + \dots + c_pv_p$를 벡터와 스칼라의 Linear Combination이라고 한다. (*참고 : Zero Vector는 항상 선형 결합이다.*)

앞서 연립일차방정식(System of Linear Equation)을 공부하였다. 이 연립일차방정식이 $Ax = b$ 꼴이 되어 행렬 방정식(Matrix Equation)이 되고, 이들이 다시 $a_1x_2 + \dots + a_nx_n = b$ 꼴이 되어 벡터 방정식(Vector Equation)이 되는 것이다. 예를 들면 아래와 같다.

$$60x_1 + 5.5x_2 + x_3 = 66 \\ 65 x_1 + 5.0x_2 = 74 \\ 55x_1 + 6.0x_2 + x_3 = 78$$

$$\begin{bmatrix} 60 & 5.5 & 1 \\ 65 & 5.0 & 0 \\ 55 & 6.0 & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} 66 \\ 74 \\ 78 \end{bmatrix}$$

$$a_1 = \begin{bmatrix} 60 \\ 65 \\ 55 \end{bmatrix}, a_2 = \begin{bmatrix} 5.5 \\ 5.0 \\ 6.0 \end{bmatrix}, a_3 = \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}$$

$$\begin{bmatrix} a_1 & a_2 & a_3 \end{bmatrix}\begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} 66 \\ 74 \\ 78 \end{bmatrix}$$

$$a_1x_1 + a_2x_2 + a_3x_3 = b$$

<br/>

$$\begin{bmatrix} 1 & 1 & 0 \\ 1 & 0 & 1 \\ 1 & -1 & 1 \end{bmatrix}\begin{bmatrix} 1 & -1 \\ 2 & 0 \\ 3 & 1 \end{bmatrix} = \begin{bmatrix} x_1 & y_1 \\ x_2 & y_2 \\ x_3 & y_3 \end{bmatrix} = \begin{bmatrix} x & y \end{bmatrix}$$

$$x = \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix}1 + \begin{bmatrix} 1 \\ 0 \\ -1 \end{bmatrix}2 + \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix}3$$

$$y = \begin{bmatrix} y_1 \\ y_2 \\ y_3 \end{bmatrix} = \begin{bmatrix} 1 \\ 1\\ 1 \end{bmatrix}(-1) + \begin{bmatrix} 1 \\ 0 \\ -1 \end{bmatrix}0 + \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix}1$$

<br/>

$$\begin{bmatrix} 1 & 2 & 3 \end{bmatrix}\begin{bmatrix} 1 & 1 & 0 \\ 1 & 0 & 1 \\ 1 & -1 & 1 \end{bmatrix}$$

$$= 1 \times \begin{bmatrix} 1 & 1 & 0 \end{bmatrix} + 2 \times \begin{bmatrix} 1 & 0 & 1 \end{bmatrix} + 3 \times \begin{bmatrix} 1 & -1 & 1 \end{bmatrix}$$

<br/>

$$\begin{bmatrix} 1 & 2 & 3 \\ 1 & 0 & -1 \end{bmatrix}\begin{bmatrix} 1 & 1 & 0 \\ 1 & 0 & 1 \\ 1 & -1 & 1 \end{bmatrix} = \begin{bmatrix} x_1 & x_2 & x_3 \\ y_1 & y_2 & y_3 \end{bmatrix} = \begin{bmatrix} x^T \\ y^T \end{bmatrix}$$

$$x^T = \begin{bmatrix} x_1 & x_2 & x_3 \end{bmatrix} = 1 \times \begin{bmatrix} 1 & 1 & 0 \end{bmatrix} + 2 \times \begin{bmatrix} 1 & 0 & 1 \end{bmatrix} + 3 \times \begin{bmatrix} 1 & -1 & 1 \end{bmatrix}$$

$$y^T = \begin{bmatrix} y_1 & y_2 & y_3 \end{bmatrix} = 1 \times \begin{bmatrix} 1 & 1 & 0 \end{bmatrix} + 0 \times \begin{bmatrix} 1 & 0 & 1 \end{bmatrix} + (-1) \times \begin{bmatrix} 1 & -1 & 1 \end{bmatrix}$$

<br/>

### 2. Vector Space

원소를 서로 더하거나 주어진 배수로 늘이고, 줄일 수 있는 공간

만약 벡터 $v, w$가 vector space 내에 존재한다면 다음을 만족한다.

1. $v + w$가 같은 벡터 공간 안에 존재
2. $cv, cw$가 같은 벡터 공간안에 존재
3. 선형결합 $cv + dw$가 같은 벡터 공간안에 존재

*참고 : 벡터의 내적 (Inner / Scalar / dot Product)과 외적 (Outer Product)*  
$a$와 $b$가 다음과 같을 때, 내적과 외적을 순서대로 나타내면 다음과 같다.

$$a = \begin{bmatrix} 　 \\ 　\\ 　 \end{bmatrix}, b = \begin{bmatrix} 　& 　& 　 \end{bmatrix}$$

$$a^Tb = \begin{bmatrix} 　 & 　 & 　 \end{bmatrix}\begin{bmatrix} 　 \\ 　 \\ 　 \end{bmatrix}$$

$$ab^T = \begin{bmatrix} 　 \\ 　 \\ 　 \end{bmatrix}\begin{bmatrix} 　 & 　 & 　 \end{bmatrix}$$

이때, [　　　]와 같이 모든 행렬들의 기본적인 행렬 단위를 **Rank 1**이라고 하며, 이는 공분산 매트릭스(Covariance matrix), Gram matrix 등 머신러닝에서 광범위하게 사용된다.

벡터가 vector space 내에 존재하기 위해서는 1) 두 벡터의 합이 같은 vector space에 존재해야 하고, 2)상수배가 같은 vector space에 존재해야 하고, 3) 선형 결합이 같은 vector space에 존재해야 한다.

Vector Subspace : Vector Space의 부분집합. 임의의 n차원 공간에 대해, n차원 공간에 포함되면서 n차원 벡터들에 대해 선형결합연산이 성립하는 작은 공간. 반드시 zero vector를 포함해야 한다

<br/>

### 3. Span

벡터들의 가능한 모든 Linear Combination으로 만들어진 집합 혹은 공간. Generating set(선형 결합되어 모든 벡터를 나타낼 수 있는 벡터들의 집합)의 벡터들이 Linear Combination된 결과의 집합

즉, 벡터들이 Linear Combination 한다는 것은 Span한다는 것과 똑같은 말이다.

　$\rightarrow$　Span {$v_1, \dots, v_p$} = $c_1v_2 + \dots + c_pv_p$

　$\rightarrow$　If $a_1x_1 + a_2x_2 + a_3x_3 = b$일 때, $b$가 선형결합의 Span에 포함되야 해가 존재한다.

<br/>