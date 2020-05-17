---
layout : post
title : "1. Introduction, Linear Equation"
description :
date : 2020-02-26
category : Linear Algebra
tags : [Linear Algebra, Linear Equation]
use_math: true
comments : true
share : true
---

<br/>
Marc Peter Deisenroth외 2인이 저술한 책인 Mathematics for Machine Learning과 Gilbert Strang이 저술한 책인 Introduction to Linear Algebra, 그리고 카이스트 주재걸 교수님의 [인공지능을 위한 선형대수](https://www.edwith.org/linearalgebra4ai) 강의를 참고하였다.

<br/>

이제 알고리즘 다음으로 선형대수학을 공부할 차례이다. 근데 이게 지금...노트에 적혀있는게 빼곡한데 이걸 일일이 마크다운으로 행렬 만들고 표 만들고 그래프 그리고...하다보면 시간이 너무 오래 걸릴 것 같아 어떻게 공부해야할지 고민이 되었다. 그래서 한참 고민하다가, 정말 쉬운 내용은 생략하기로 하였고 중요한 내용 중에서도 최대한 개념만을 위주로 포스팅하기로 마음 먹었다.

<br/>

### 1. Introduction of Linear Algebra

- **Linear** : 선형성. 직선 그래프로 표현될 수 있는 수학적 성질

　　　　　*선형성의 조건 : $f(x+y) = f(x) + f(y), f(ax) = af(x)$*

- **Linear Algebra** : 선형성을 가지는 대수로 이루어진 방정식들의 해를 구하는 방법론
- **Scalar** : a single number, e.g. 4
- **Vector** : an orderd list of numbers
- **Matrix** : $m$과 $n$이 실수일 때, $m$개의 row와 $n$개의 column으로 구성된 rectangular scheme 안에 원소들이 들어선 형태
- **Column Vector** : 한 개의 열을 갖는 matrix. 즉, 임의의 $n$개의 원소를 갖는 $n \times 1$ matrix
- **Row Vector** : 한 개의 행을 갖는 matrix. 즉, 임의의 $n$개의 원소를 갖는 $1 \times n$ matrix
- **Properties of Matrix**
  - Distributive : $A(B + C) = AB + AC$
  - Associative : $A(BC) = (AB)C$
  - Transpose : $(AB)^T = B^TA^T$

- $A \in R^{m \times n}, B \in R^{n \times k} 　\rightarrow 　AB = C \in R^{m \times k}$

- Matrices can only be multiplied if their "neighboring" dimensions match.

  *아다마르(Hadamard) 곱 : 위 조건을 만족하지 않는, 예를 들어 $(m, n), (m, n)$ 행렬 간의 곱*

- $AB \neq BA$ : 값이 달라지고, 차원도 달라질 수 있다

- **Identity Matrix(단위 행렬)** : $I_n \in R^{n \times n}, 　IA = AI = A$

- 행렬간의 곱셈 성질 : Associativity, Distributivity

- $A \in R^{n \times n}$이고, $B \in R^{n \times n}$ 일때, $AB = I_n = BA$인 $B$를 *$A$의 Inverse* = $A^{-1}$라고 한다.

  $A$의 Inverse가 있다면 $A$는 *regular / invertible / nonsingular* 하다고 하며,  
  $A$의 Inverse가 없다면 $A$는 *singular / noninvertible* 하다고 한다.

- **Symetric Marix** : $A \in R^{n \times n}$이고, $A = A^T$인 $A$. 　Only $n \times n$ matrices can by symmetric.
- $(A^{-1})^T = (A^T)^{-1} = A^{-T}$
- $A, B$가 Symmetric 하다면 $A + B = C$도 Symmetric 하다. 하지만 $AB$는 보장할 수 없다.

<br/>

### 2-1. Systems of Linear Equations(연립일차방정식)

같은 변수를 갖는 두 개 이상의 선형 방정식들의 모임. 

$$a_{11}x_1 + a_{12}x_2 + \dots a_{1n}x_n = b_1$$

$$ \vdots $$

$$a_{11}x_1 + a_{12}x_2 + \dots a_{1n}x_n = b_1$$

위 식들은 다음과 같이 표현할 수 있다.

$$x_1\begin{bmatrix} a_{11} \\ \vdots \\ a_{m1} \end{bmatrix} + x_2\begin{bmatrix} a_{12} \\ \vdots \\ a_{m2} \end{bmatrix} + \dots + x_n\begin{bmatrix} a_{1n} \\ \vdots \\ a_{mn} \end{bmatrix} = x_n\begin{bmatrix} b_1 \\ \vdots \\ b_m \end{bmatrix}$$

$$\begin{bmatrix} a_{11} & a_{12} & \dots & a_{1n} \\ a_{21} & a_{22} & \dots & a_{2n} \\ \vdots & \vdots & \vdots & \vdots \\ a_{m1} & a_{m2} & \dots & a_{mn}\end{bmatrix}\begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix} = \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_m \end{bmatrix}$$

즉, 다시 말해 두 개 이상의 선형방정식들의 모임을 $Ax = b$의 형태로 표현할 수 있는 것이다. 여기서 $A$를 계수 행렬, $x$를 미지수 벡터, $b$를 우변 벡터라고 하며 Solution set은 일차 방정식들의 교차점(점, 선, 평면)이다.

그렇다면 위 과정을 통해 $x$를 어떻게 구하는가? 당연히 $A$의 Inverse matrix를 구하면 된다. 하지만 $A$가 너무 커서 Inverse matrix를 구하기 어려운 경우에는 어떻게 할 것인가? 이 경우에는 Gaussian Elimination을 이용해준다.

*Elimination(Factorization) : 소거법. 해의 존재 여부를 판별하는 기법*

또 만약 $A^{-1}$이 존재하지 않는다면 $x$는 존재하지 않거나, 혹은 무수히 많을 것이다. 이제 Gaussian Elimination을 공부해보자.

<br/>

### 2-2. Solving Systems of Linear Equations

연립일차방정식을 풀기 위한 대표적인 방법은 **Gaussian Elimination**이다.

**Gaussian Elimination** : 연립일차방정식을 reduced row-echelon form(REF : 기약 사다리꼴 행렬)로 바꾸는 알고리즘

가우시안 소거법을 이용해 REF를 만들게 되면 맨 밑의 row가 모두 0이 되는데 행렬 $A$의 row의 어떤 결합이 zero row를 만든다면 $b$에 대한 똑같은 선형 결합도 0이 되어야하기 때문에 해를 구할 수 있는 것이다. 이를 **가해 조건**이라고 한다.

$$-2x_1 + 4x_2 - 2x_3 - x_4 + 4x_5 = -3$$

$$4x_1 - 8x_2 + 3x_3 - 3x_4 + x_5 = 2$$

$$x_1 - 2x_2 +　x_3 - x_4 + x_5 = 0$$

$$x_1 - 2x_2　　　　- 3x_4 + 4x_5 = a$$

이 연립일차방정식을 대상으로 가우시안 소거법을 적용해보자.

#### 1. $Ax = b$형태로 만들기

$$\begin{bmatrix} -2 & 4 & -2 & -1 & 4 \\ 4 & -8 & 3 & -3 & 1 \\ 1 & -2 & 1 & -1 & 1 \\ 1 & -2 & 0 & -3 & 4 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \\ x_4 \end{bmatrix} = \begin{bmatrix} -3 \\ 2 \\ 0 \\ a \end{bmatrix}$$

#### 2. $A$와 $b$를 대상으로 Augmented matrix(첨가행렬. $[A　|　B]$의 형태)로 만들기

$$ \left[
\begin{array}{ccccc|c}
  -2&4&-2&-1&4&-3\\
  4&-8&3&-3&1&-2\\
  1&-2&1&-1&1&0\\
  1&-2&0&-3&4&a
\end{array}
\right] $$

#### 3. row의 pivot을 주인공으로 하여 모든 row에 빼주기

먼저, 계산시간을 줄이기 위해 3rd row와 1st row의 순서를 바꿔주자

$$ \left[
\begin{array}{ccccc|c}
  1&-2&1&-1&1&0\\
  4&-8&3&-3&1&-2\\
  -2&4&-2&-1&4&-3\\
  1&-2&0&-3&4&a
\end{array}
\right] $$

first pivot = 1이다. 이를 주인공으로 하여 1st column에 1st row의 1을 제외하고 나머지 값이 소거되도록 빼준다. 즉, 1st row에 4를 곱하여 2nd row에 빼주고, 다시 1st row에 -2를 곱하여 3rd row에 빼주고, 원본을 4th row에 빼주는 것이다. 1st row는 그대로 유지된다. 결과는 다음과 같다.

$$ \left[
\begin{array}{ccccc|c}
  1&-2&1&-1&1&0\\
  0&0&-1&1&-3&2\\
  0&0&0&-3&6&-3\\
  0&0&-1&-2&3&a
\end{array}
\right] $$

그 다음, 2nd row의 3rd column 값인 -1을 pivot으로 하여 4th row에 빼준다. 결과는 다음과 같다.

$$ \left[
\begin{array}{ccccc|c}
  1&-2&1&-1&1&0\\
  0&0&-1&1&-3&2\\
  0&0&0&-3&6&-3\\
  0&0&0&-3&6&a-2
\end{array}
\right] $$

그 다음, 3rd row의 4th column 값인 -3을 pivot으로 하여 4th row에 빼준다. 결과는 다음과 같다.

$$ \left[
\begin{array}{ccccc|c}
  1&-2&1&-1&1&0\\
  0&0&-1&1&-3&2\\
  0&0&0&-3&6&-3\\
  0&0&0&0&0&a+1
\end{array}
\right] $$

그러면 최종적으로 왼쪽 $A$의 형태가 REF가 된 것을 알 수 있다. 위 식을 다시 $Ax = b$의 형태로 바꿔주면 다음과 같다.

$$x_1 -2x_2 + x_3 - x_4 + x_5 = 0$$

$$x_3 - x_4 + 3x_5 = -2$$

$$x_4 - 2x_5 = 1$$

$$0 = a+1$$

우선적으로 $a = -1$인 것을 알 수 있다. 원래대로라면 $x_5$가 남아있어서 아래에서부터 차근차근 $x_4, x_3, x_2, x_1$을 구할 수 있지만 위 식의 경우 $x_5$가 소거되는 바람에 정확한 $x$를 구할 수 없다. 이 경우에는 General Solution을 구해주어야 한다.

#### 4. General Solution 구하기

이를 위해서는 먼저 **basic variable**과 **free variable**이라는 개념을 알아야 한다.

- **basic variable** : pivot이 존재하는 $x$
- **free variable** : pivot이 존재하지 않는 $x$

즉, 위에서 pivot은 1st column과 3rd column, 4th column이었으므로 basic variable은 $x_1, x_3, x_4$이고, free variable은 $x_2, x_5$이다. *(참고 : A = m x n matrix일 때 (m < n), max(pivot) = m, min(free variable) = n - m)*

그 다음으로 **particular solution**과 **general solution**이라는 개념을 알아야 한다.

- **particular solution** : free variable 값이 모두 0일 때의 solution
- **general solution** : particular solution + $\mu \times $free variable의 값이 각각 1과 0일 때의 solution

위에서 구한 결과를 토대로 particular solution과 general solution을 각각 구하면 다음과 같다.

$$\begin{bmatrix} x_1 \\ x_2 \\ x_3 \\ x_4 \\ x_5 \end{bmatrix} = \begin{bmatrix} 2 \\ 0 \\ -1 \\ 1 \\ 0 \end{bmatrix}$$

$$\begin{bmatrix} x_1 \\ x_2 \\ x_3 \\ x_4 \\ x_5 \end{bmatrix} = \begin{bmatrix} 2 \\ 0 \\ -1 \\ 1 \\ 0 \end{bmatrix} + \mu_1\begin{bmatrix} 2 \\ 1 \\ 0 \\ 0 \\ 1 \end{bmatrix} + \mu_2\begin{bmatrix} 2 \\ 0 \\ -1 \\ 2 \\ 1 \end{bmatrix}$$

이 과정을 거쳐 general solution을 구했다면, 가우시안 소거법을 최종적으로 완료한 것이다.

<br/>

가우시안 소거법은 이밖에도 여러 경우에 사용되는데 그 경우는 다음과 같다.

- Determinants 구할 때
- 벡터 집합이 선형 독립인지 검사할 때
- 역행렬을 구할 때
- matrix의 rank를 구할 때
- basis of a vector space를 결정할 때

위 경우들 중에서 가우시안 소거법을 이용해 역행렬을 어떻게 구할 수 있을까?  
방법은 간단하다. $[A　|　I]$의 형태를 만들어 준 다음, 가우시안 소거법을 이용해 $A$를 $I$로 만들어주면 된다. 그러면 최종적으로 $[I　|　B]$ 형태가 만들어지는데, 이 때 $B$가 바로 $A^{-1}$이다. 자세한 과정은 생략한다.

<br/>