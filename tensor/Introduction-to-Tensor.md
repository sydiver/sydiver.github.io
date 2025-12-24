---
layout: article
title: "Introduction to Tensor"
permalink: /tensor/introduction-to-tensor/
sidebar:
  nav: subjects
mathjax: true
mathjax_autoNumber: true
---

공대생이라면 언젠가 **“텐서(tensor)”**라는 말을 듣게 됩니다.  
저는 고체역학이나 유체역학에서 **응력 텐서(stress tensor)**를 다룰 때 처음 들었던 것 같습니다.  
그런데 처음엔 정말 애매하기 짝이 없죠.  
텐서가 도대체 뭔지도, 왜 알아야 하는지도 잘 이해가 되지 않았습니다.

앞으로는 텐서에 대해서 알아본 후에,  
텐서를 사용하면 유체역학이 얼마나 간단해(?)지는지 조금씩 체감하게 되실 겁니다.

그럼 텐서가 도대체 뭔지 알아봅시다.

---

## 텐서란 무엇인가

결론부터 말합니다. **텐서는 물리 현상을 좌표계에 관계없이 표현하기 위한 수학적 도구**입니다.  
텐서(그리고 지표 표기법)를 사용하면 방정식을 더 **compact**하게 쓸 수 있고,  
복잡한 계산을 좀 더 **체계적으로** 정리할 수 있습니다.

예를 들어 이런 식으로 생긴(보기만 해도 머리 아픈) 표현들 말이죠:

$$
(\vec A \times \vec B)\cdot(\nabla \times \vec C)
$$

지금은 정확히 이해가 안 돼도 괜찮습니다.  
“이런 연산이 나중에 나온다” 정도만 기억하고 일단 넘어가 봅시다.

---

## Index

텐서(지표) 표기법에서 인덱스는 크게 **free index(자유 인덱스)**와 **dummy index(더미 인덱스)**로 나뉩니다.

### 1) Free index (자유 인덱스)

**free index n차원 텐서의 변수를 모두 함축하고 있는, 즉 변수 그 자체의 역할을 하는 인덱스**입니다.  


예를 들어 3차원 공간에서 $x_i$라고 쓰면, 여기서 $i$는 free index입니다.  
이 표현은 “$i=1,2,3$에 따라 $x_1, x_2, x_3$ 성분을 뜻한다”는 의미로 읽으면 됩니다.
$x_i$는 벡터라고 이해하면 되겠죠?



---

### 2) Dummy index (더미 인덱스)

**dummy index는 한 항(term) 안에서 두 번 등장하는 인덱스**이고,  
이 경우에는 **합($\sum$)을 생략한 표기**로 해석합니다. (Einstein summation convention)

예를 들어

$$
a_i b_i c_j
$$

에서 $i$는 두 번 등장하므로 dummy index이고, $j$는 한 번만 등장하므로 free index입니다.  
위 식은 실제로 다음을 의미합니다:

$$
a_i b_i c_j
= a_1 b_1 c_j + a_2 b_2 c_j + a_3 b_3 c_j.
$$

여기서 중요한 점은, dummy index는 **합을 위한 ‘이름표’**라서  
$i$ 대신 $k$라고 써도 의미가 바뀌지 않는다는 것입니다. (어차피 더해질 인덱스라서)

---

### 3) 표기 규칙에서 자주 하는 실수

**(규칙 A)** 같은 항(term) 안에서 인덱스는 보통 **최대 두 번만** 등장하게 씁니다.  
두 번 등장하면 합을 뜻하기 때문에, 세 번 이상 나오면 의미가 애매해지거나 규칙 위반이 됩니다.

**(규칙 B)** 등식이나 덧셈에서 **free index의 패턴은 모든 항에서 동일해야 합니다.**  
즉, 한 식에서 “남는 free index”가 무엇인지가 일관되어야 해요.

예를 들어

$$
a_i = b_j + c_i
$$

는 틀린 표현입니다.  
좌변은 $i$ 성분에 대한 식인데, 우변에는 $j$가 free로 남아서 성분이 맞지 않기 때문입니다.

반면에

$$
a_i + b_{ij}c_j + d_{kl} f_{kli} = 0
$$

는 맞는 표현입니다.  
각 항을 보면 $j,k,l$은 두 번씩 등장하므로 dummy index(합)이고,  
결국 식 전체에서 남는 free index는 $i$ 하나로 통일되기 때문입니다.

---

## Order (Rank)

텐서의 **차수(order)** 혹은 **랭크(rank)**에 대해 설명하겠습니다.  
$n$차원 공간에서 **rank $r$ 텐서**는 보통 $n^r$개의 성분(component)을 가집니다.

예를 들어 3차원($n=3$)에서

$$
3^0=1,\qquad 3^1=3,\qquad 3^2=9
$$

이므로,

- 0차 텐서: 성분 1개 (스칼라)
- 1차 텐서: 성분 3개 (벡터)
- 2차 텐서: 성분 9개 (행렬)

이라고 우선 생각하셔도 좋습니다.

> 주의: 이 $n^r$은 “모든 성분을 독립적으로 셌을 때”의 개수입니다.  
> 대칭/반대칭 같은 제약이 있으면 독립 성분 수는 더 줄어듭니다.

예를 들어 3차원에서 $\mathbf{x}=\begin{bmatrix}x_1\\x_2\\x_3\end{bmatrix}$, $\mathbf{A}=\begin{bmatrix}A_{11}&A_{12}&A_{13}\\A_{21}&A_{22}&A_{23}\\A_{31}&A_{32}&A_{33}\end{bmatrix}$라 두면,
$\mathbf{y}=\mathbf{A}\mathbf{x}$는
$\begin{bmatrix}y_1\\y_2\\y_3\end{bmatrix}
=
\begin{bmatrix}A_{11}&A_{12}&A_{13}\\A_{21}&A_{22}&A_{23}\\A_{31}&A_{32}&A_{33}\end{bmatrix}
\begin{bmatrix}x_1\\x_2\\x_3\end{bmatrix}$
이고, 성분으로 쓰면
$y_1=A_{11}x_1+A_{12}x_2+A_{13}x_3$, $y_2=A_{21}x_1+A_{22}x_2+A_{23}x_3$, $y_3=A_{31}x_1+A_{32}x_2+A_{33}x_3$이며,
이를 인덱스 노테이션으로 쓰면 $y_i=A_{ij}x_j$입니다.

---

## Tensor Algebra

텐서도 물리량이므로 연산할 수 있습니다.

### 1) Addition (덧셈)

**같은 차수(같은 rank)**의 텐서끼리만 더할 수 있고, 결과도 같은 차수의 텐서가 됩니다.  
예를 들어

$$
A_{ijk} + B_{ijk} = C_{ijk}
$$

와 같이 씁니다.

---

### 2) Multiplication (곱)

곱은 종류가 여러 가지가 있는데, 가장 단순한 형태는 **외적(outer product)**입니다.  
예를 들어 2차 텐서 $A_{ij}$와 3차 텐서 $B_{rst}$의 외적은

$$
C_{ijrst} = A_{ij}\,B_{rst}
$$

처럼 쓰며, 결과는 5차 텐서가 됩니다.

> 행렬곱처럼 “인덱스를 하나 이상 합쳐서 줄이는 곱(수축, contraction)”도 아주 중요하지만,  
> 그건 다음에 따로 정리하겠습니다.

---

## Symmetry / Skew-symmetry

텐서에서는 인덱스의 위치를 바꿨을 때 성질이 유지되는 경우가 많습니다.

### 1) Symmetry (대칭)

예를 들어 4차 텐서 $A_{ijkl}$에 대해

$$
A_{ijkl} = A_{ikjl}
$$

처럼 특정 인덱스 두 개를 바꿔도 값이 같으면, 해당 인덱스 쌍에 대해 **대칭(symmetry)**이라고 합니다.

(특히 2차 텐서에서는 보통

$$
A_{ij}=A_{ji}
$$

를 “대칭 텐서”라고 많이 부릅니다.)

---

### 2) Skew-symmetry (반대칭)

반대로, 인덱스 두 개를 바꾸면 부호가 바뀌는 경우도 있습니다. 예를 들어

$$
A_{ij} = -A_{ji}
$$

이면 **반대칭(skew-symmetric, antisymmetric)** 텐서라고 합니다.

이 성질은 나중에 텐서 연산(특히 수축, 내적, 에너지 형태 등)에서  
불필요한 항을 날려서 계산을 크게 단순화해 줍니다.

---

## Kronecker delta (크로네커 델타)

지표 표기법에서 가장 자주 등장하는 “기본 부품” 중 하나가 **Kronecker delta**입니다.  
기호는 $\delta_{ij}$로 쓰고, 정의는 다음과 같습니다.

$$
\delta_{ij} =
\begin{cases}
1, & i=j,\\
0, & i\neq j.
\end{cases}
$$

직관적으로는 “인덱스를 서로 같게 맞춰주는 스위치”라고 생각하면 됩니다.

### 1) Identity tensor (단위 텐서)

3차원에서 $\delta_{ij}$는 2차 텐서(행렬)로 보면 곧바로 단위행렬과 같습니다.

$$
\delta_{ij} \;\longleftrightarrow\;
\mathbf I=
\begin{bmatrix}
1&0&0\\
0&1&0\\
0&0&1
\end{bmatrix}.
$$

즉, $\delta_{ij}$는 흔히 **2차 단위 텐서(identity tensor)**라고도 부릅니다.

### 2) 벡터/텐서에 작용: “그대로 돌려준다”

$$
\delta_{ij} a_j = a_i
$$

왜냐하면 $j$에 대해 합이 일어나면서, $i=j$인 성분만 남기 때문입니다.  
(인덱스를 하나 “바꿔 끼우는” 느낌이라고 보면 됩니다.)

더 일반적으로,

$$
\delta_{ij} A_{jk} = A_{ik}, \qquad
A_{ij}\delta_{jk} = A_{ik}.
$$

### 3) Trace(대각합)와의 관계

$$
\delta_{ii} = n
$$

여기서 $n$은 공간 차원입니다. (3차원이라면 $\delta_{ii}=3$)

또한 2차 텐서 $A_{ij}$의 trace는

$$
\mathrm{tr}(\mathbf A)=A_{ii}
$$

처럼 인덱스를 수축(contraction)해서 얻습니다.

---

## Permutation tensor (Levi--Civita symbol, 순열 텐서)

외적(cross product), 컬(curl) 같은 3차원 벡터 연산은 지표 표기법으로 쓰면 깔끔해지는데,  
그 핵심이 바로 **permutation tensor**입니다. 보통 $\varepsilon_{ijk}$로 씁니다.

정의는 다음과 같습니다.

$$
\varepsilon_{ijk} =
\begin{cases}
+1, & (i,j,k)\ \text{가 }(1,2,3)\text{의 짝순열(even permutation)}\\
-1, & (i,j,k)\ \text{가 }(1,2,3)\text{의 홀순열(odd permutation)}\\
0, & \text{그 외 (즉, 인덱스 중 중복이 있을 때)}
\end{cases}
$$

예를 들면

$$
\varepsilon_{123}=+1,\qquad
\varepsilon_{231}=+1,\qquad
\varepsilon_{312}=+1
$$

은 짝순열이라 $+1$이고,

$$
\varepsilon_{132}=-1,\qquad
\varepsilon_{213}=-1,\qquad
\varepsilon_{321}=-1
$$

은 홀순열이라 $-1$입니다.  
그리고 같은 숫자가 반복되면 0:

$$
\varepsilon_{113}=0,\quad \varepsilon_{222}=0.
$$

### 1) 완전 반대칭 (totally antisymmetric)

$\varepsilon_{ijk}$는 어떤 두 인덱스를 서로 바꾸면 부호가 바뀝니다.

$$
\varepsilon_{ijk} = -\varepsilon_{jik} = -\varepsilon_{ikj} = \cdots
$$

그래서 “순열 텐서 = 완전 반대칭 텐서”라고 이해해도 됩니다.

---

## 외적/컬/스칼라 삼중곱을 지표로 쓰기

### 1) Cross product (외적)

벡터 $\vec a,\vec b$에 대해 외적 $\vec c=\vec a\times \vec b$의 성분은

$$
c_i = (\vec a \times \vec b)_i = \varepsilon_{ijk} a_j b_k
$$

로 쓸 수 있습니다.

### 2) Curl (컬)

벡터장 $\vec v(\vec x)$에 대해

$$
(\nabla \times \vec v)_i = \varepsilon_{ijk}\,\partial_j v_k
$$

여기서 $\partial_j := \dfrac{\partial}{\partial x_j}$ 입니다.

### 3) Scalar triple product (스칼라 삼중곱)

$$
\vec a\cdot(\vec b\times \vec c)
= \varepsilon_{ijk} a_i b_j c_k.
$$

---

## Kronecker delta와 permutation tensor의 핵심 항등식

아래 항등식은 외적/컬 계산을 “마법처럼” 단순화해 줍니다.

### 1) 한 번 수축한 항등식

$$
\varepsilon_{ijk}\varepsilon_{imn}
=
\delta_{jm}\delta_{kn}-\delta_{jn}\delta_{km}.
$$

(가장 자주 쓰는 형태입니다. 외적-외적 전개할 때 거의 무조건 나옵니다.)

### 2) 두 번 수축한 항등식

$$
\varepsilon_{ijk}\varepsilon_{ijn}
=
2\,\delta_{kn}.
$$

특히 3차원에서만 성립하는 “외적 특유의 단순화”가 여기서 나옵니다.

---

## 예시: $\vec a \times (\vec b \times \vec c)$ 전개가 왜 쉬워지나

삼중 외적 항등식

$$
\vec a \times (\vec b \times \vec c)
= \vec b(\vec a\cdot\vec c)-\vec c(\vec a\cdot\vec b)
$$

도 사실 $\varepsilon$와 $\delta$로 2~3줄이면 정리됩니다.

$$
\bigl(\vec a \times (\vec b \times \vec c)\bigr)_i
=
\varepsilon_{ijk}a_j(\vec b\times \vec c)_k
=
\varepsilon_{ijk}a_j(\varepsilon_{kmn}b_m c_n).
$$

여기서 항등식

$$
\varepsilon_{ijk}\varepsilon_{kmn}
=
\delta_{im}\delta_{jn}-\delta_{in}\delta_{jm}
$$

을 적용하면,

$$
\bigl(\vec a \times (\vec b \times \vec c)\bigr)_i
=
(\delta_{im}\delta_{jn}-\delta_{in}\delta_{jm})a_j b_m c_n
=
b_i(a_j c_j) - c_i(a_j b_j).
$$

즉,

$$
\vec a \times (\vec b \times \vec c)
= \vec b(\vec a\cdot\vec c)-\vec c(\vec a\cdot\vec b).
$$

---

> 정리하자면,  
> - $\delta_{ij}$는 “인덱스를 그대로 통과시키는 단위 텐서”  
> - $\varepsilon_{ijk}$는 “3차원 외적/컬을 인덱스로 쓰게 해주는 완전 반대칭 텐서”  
> - 두 개를 같이 쓰면 외적/컬 같은 복잡한 벡터 연산이 기계적으로 정리됩니다.
