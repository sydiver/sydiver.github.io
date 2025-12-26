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

참고로 텐서 노테이션 = 인덱스 노테이션 = 아인슈타인 노테이션 모두 같은 말입니다.

그럼 텐서가 도대체 뭔지 알아봅시다.

---

## 0. 텐서란 무엇인가

결론부터 말합니다. **텐서는 물리 현상을 좌표계에 관계없이 표현하기 위한 수학적 도구**입니다.  
텐서(그리고 지표 표기법)를 사용하면 방정식을 더 **compact**하게 쓸 수 있고,  
복잡한 계산을 좀 더 **체계적으로** 정리할 수 있습니다.

예를 들어 이런 식으로 생긴(보기만 해도 머리 아픈) 표현들 말이죠:

$$
(\vec A \times \vec B)\times (\nabla \vec C)
$$

지금은 정확히 이해가 안 돼도 괜찮습니다.  
“이런 연산이 나중에 나온다” 정도만 기억하고 일단 넘어가 봅시다.

---

## 1. Index
텐서 표기법(노테이션)은 인덱스 노테이션이라고도 불립니다.
인덱스는 어떤 개념의 순서나 목차를 알려주는 숫자를 말하죠?
텐서 표기법에서 인덱스는 크게 **free index(자유 인덱스)**와 **dummy index(더미 인덱스)**로 나뉩니다.

### 1.1) Free index (자유 인덱스)

**free index n차원 텐서의 변수를 모두 함축하고 있는, 즉 변수 그 자체의 역할을 하는 인덱스**입니다.  


예를 들어 3차원 공간에서 $x_i$라고 쓰면, 여기서 $i$는 free index입니다.  
이 표현은 “$i=1,2,3$에 따라 $x_1, x_2, x_3$ 성분을 뜻한다”는 의미로 읽으면 됩니다.
$x_i$는 벡터라고 이해하면 되겠죠?

즉, 모든 차원의 변수를 하나의 표기로 대체하겠다는 겁니다.
그럼 3차원에서 방정식을 세 개 써야할 것을, 하나만 써도 됩니다.
하지만 텐서 표기법의 장점은 이것만이 아닙니다. (뒤에 나옵니다)

---

### 1.2) Dummy index (더미 인덱스)

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

더미 인덱스가 여러개 일 수도 있겠죠?
그런 경우 우선 더미 인덱스 하나를 먼저 풀어쓰고, 나머지를 풀어쓴다고 생각하면 쉽습니다.
아래에서는 i,j 모두 더미 인덱스입니다.

$$A_{ij}B_{ij} = A_{1j}B_{1j} + A_{2j}B_{2j} + A_{3j}B_{3j} $$

먼저 더미 인덱스 i,j 중 i를 풀어서 썼습니다.

그 다음은 더미인덱스 j를 풀어쓰면 되겠죠?

$$
= A_{1j}B_{1j} + A_{2j}B_{2j} + A_{3j}B_{3j}
=  ( A_{11}B_{11} + + A_{12}B_{12} + A_{13}B_{13}  )
+ ( A_{21}B_{21} + + A_{22}B_{22} + A_{23}B_{23}  )
+ ( A_{31}B_{31} + + A_{32}B_{32} + A_{33}B_{33}  )
$$


---

### 1.3) 표기 규칙에서 자주 하는 실수

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

## 2. Order (Rank)

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

이라고 우선 생각하셔도 좋습니다. 3차텐서 이상은 우선 생각하지 맙시다.

> 주의: 이 $n^r$은 “모든 성분을 독립적으로 셌을 때”의 개수입니다.  
> 대칭/반대칭 같은 제약이 있으면 독립 성분 수는 더 줄어듭니다.

예를 들어 3차원에서 $\mathbf{y}=\mathbf{A}\mathbf{x}$를 생각해 봅시다.
여기서 $\mathbf{A}$는 2차텐서 $A_{ij}$이고 $\mathbf{x}$는 1차텐서(벡터)인 $x_j$입니다.
텐서 표기법에서는 벡터표기법에서 흔히 쓰는 bold체를 쓰지 않고도 벡터와 행렬을 표기함에 주의하시기 바랍니다!!

$$
\mathbf{x}=
\begin{bmatrix}
x_1\\x_2\\x_3
\end{bmatrix},\qquad
\mathbf{A}=
\begin{bmatrix}
A_{11}&A_{12}&A_{13}\\
A_{21}&A_{22}&A_{23}\\
A_{31}&A_{32}&A_{33}
\end{bmatrix},\qquad
\mathbf{y}=
\begin{bmatrix}
y_1\\y_2\\y_3
\end{bmatrix}.
$$

그러면

$$
\mathbf{y}=\mathbf{A}\mathbf{x}
\quad\Longleftrightarrow\quad
\begin{bmatrix}
y_1\\y_2\\y_3
\end{bmatrix}
=
\begin{bmatrix}
A_{11}&A_{12}&A_{13}\\
A_{21}&A_{22}&A_{23}\\
A_{31}&A_{32}&A_{33}
\end{bmatrix}
\begin{bmatrix}
x_1\\x_2\\x_3
\end{bmatrix}.
$$

성분으로 풀어 쓰면
$y_1=A_{11}x_1+A_{12}x_2+A_{13}x_3$,
$y_2=A_{21}x_1+A_{22}x_2+A_{23}x_3$,
$y_3=A_{31}x_1+A_{32}x_2+A_{33}x_3$이며,
이를 인덱스 노테이션으로 압축해서 쓰면 $y_i=A_{ij}x_j$입니다.


인덱스 노테이션이 벡터표현이나 행렬표현보다 꽤 간단하죠?

또 여기서 주목할 점은, x라는 1차텐서의 인덱스는 원래 j였는데, 거기에 인덱스 i,j를 가지는 2차텐서를 곱했더니,
결과는 i라는 인덱스를 가지는 1차텐서 y가 되었습니다.

$$j -> i $$ 와 같이 인덱스가 **변환된** 것이죠.
이것은 좌표축이 변하는 원리와 같습니다. 

!(_/assets/images/tensor1.png)

위의 그림에서 기존의 인덱스 j는 $x_1, x_2, x_3좌표계였다면$
i인덱스는 새로운 $x_1', x_2', x_3'$ 좌표계를 뜻합니다.
하지만 좌표계를 변환했더라도, $\mathbf{V}$는 변하지 않았죠?

이제 우리는 **물리량을 좌표에 무관하게 표현하기 위함** 이었음을 확인했습니다.

---

## 3. Tensor Algebra

텐서는 스칼라, 벡터등을 포함하는 물리량의 일반적인 개념이라고 했습니다.
당연히 텐서도 물리량이므로 연산할 수 있습니다.

상식적으로 스칼라 + 스칼라는 스칼라가 되겠죠?
벡터 + 벡터는 벡터가 될 겁니다.

당연히 스칼라 + 벡터는 정의되지 않습니다.

### 3.1) Addition (덧셈)

**같은 차수(같은 rank)**의 텐서끼리만 더할 수 있고, 결과도 같은 차수의 텐서가 됩니다.  
예를 들어

$$
A_{ijk} + B_{ijk} = C_{ijk}
$$

와 같이 씁니다.

---

### 3.2) Multiplication (곱)

곱은 종류가 여러 가지가 있는데, 가장 단순한 형태는 **텐서곱**입니다.  
예를 들어 2차 텐서 $A_{ij}$와 3차 텐서 $B_{rst}$의 외적은

$$
C_{ijrst} = A_{ij}\,B_{rst}
$$

처럼 쓰며, 결과는 5차 텐서가 됩니다.

> 행렬곱처럼 “인덱스를 하나 이상 합쳐서 줄이는 곱(수축, contraction)”도 아주 중요하지만,  
> 그건 다음에 따로 정리하겠습니다.

---

## 4. Symmetry / Skew-symmetry

텐서에서는 인덱스의 위치를 바꿨을 때 성질이 유지되는 경우가 많습니다.

### 4.1) Symmetry (대칭)

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

### 4.2) Skew-symmetry (반대칭)

반대로, 인덱스 두 개를 바꾸면 부호가 바뀌는 경우도 있습니다. 예를 들어

$$
A_{ij} = -A_{ji}
$$

이면 **반대칭(skew-symmetric, antisymmetric)** 텐서라고 합니다.

이 성질은 나중에 텐서 연산(특히 수축, 내적, 에너지 형태 등)에서  
불필요한 항을 날려서 계산을 크게 단순화해 줍니다.

> 반대칭 텐서의 대각성분은 0이 될 수밖에 없다는 것을 생각해보시기 바랍니다.

### 4.3) 대칭텐서와 반대칭텐서의 텐서곱은 0이 된다.

매우 중요한 성질입니다.
증명도 매우 쉽습니다.

대칭텐서 $A_{ij}$, 반대칭텐서 $B_{ij}$이 있습니다.

텐서곱 $$A_{ij}B_{ij} $$을 생각해봅시다. 
반대칭텐서의 정의에 따라 $$B_{ij} = - B_{ji}$$
따라서 $$A_{ij}B_{ij} = - A_{ij}B_{ji}  $$

이제 대칭텐서는 정의에 따라 $A_{ij} = A_{ji}$였으니
$$ - A_{ij}B_{ji}  =  - A_{ji}B_{ji}  $$

여기서 i와 j는 모두 dummy index이죠?
dummy index는 **합을 위한 ‘이름표’**라서  
$i$ 대신 $k$라고 써도 의미가 바뀌지 않는다는 것입니다. (어차피 summation할 인덱스라서 알파벳을 아무거나 써도 된다고 했습니다)

그러면 결국 i와 j를 바꿔서 써도 같은 표현이라는 말입니다.
$ - A_{ji}B_{ji} = - A_{ij}B_{ij}$가 된다는 거죠.
(헷갈리면 직접 풀어서 써보시길 바랍니다)

그럼 결국 $$
A_{ij}B_{ij} = - A_{ij}B_{ij}
$$
라는 결론을 얻게 됩니다. 

$$
2 A_{ij}B_{ij} = 0 
$$
이므로 **대칭텐서와 반대칭텐서의 곱은 0이다**는 것을 증명했습니다.

---

## 5. Kronecker delta (크로네커 델타)

지표 표기법에서 가장 자주 등장하는 “기본 부품” 중 하나가 **Kronecker delta**입니다.  
기호는 $\delta_{ij}$로 쓰고, 정의는 다음과 같습니다.

$$
\delta_{ij} =
\begin{cases}
1, & i=j,\\
0, & i\neq j.
\end{cases}
$$

직관적으로는 “인덱스를 바꾸는 역할” 정도로 생각해 둡시다.

### 5.1) Identity tensor (단위 텐서)

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

### 5.2) 벡터/텐서에 작용: "substitution property”

Kronecker delta는 i와 j인덱스가 같을 때만 1이 되고,
다르면 0이 된다고 했습니다.
즉, 두개의 인덱스 중 **겹치는 것**만 남기고 나머지는 지운다는 말입니다.
따라서 kronecker delta는 **substituting property**를 갖는다고 할 수 있습니다.
예를 들면,
$$
\delta_{ij} a_j = a_i
$$
와 같이 인덱스 j를 지울 수 있습니다.

왜냐하면 $j$에 대해 합이 일어나면서, $i=j$인 성분만 남기 때문입니다.  
(인덱스를 하나 “바꿔 끼우는” 느낌이라고 보면 됩니다.)

직관적으로 이해가 되지 않는다면 풀어서 증명해보면 됩니다.
j는 두 번 등장했으니 dummy index이죠?

$$
\delta_{ij} a_j = \delta_{i1} a_1 + \delta_{i2} a_2 + \delta _ {i3} a_3 
$$
여기서 우변의 첫 번째 항을 성분으로 풀어서 써 보겠습니다.
i는 free index이니 3차원에서의 방향(기저)를 의미한다고 했죠? 따라서 성분은 i = 1,2,3의 세 가지를 가질 겁니다.
$$
\delta_{i1} a_1 =  ( \delta_{11} a_1 ,  \delta_{21} a_1 , \delta_{31} a_1) 
$$
그럼 kroncecker delta의 정의에 따라, 위의 세 성분 중 $\delta_{11} a_1 $만 살아남겠죠.
그것은 곧 $a_1$과 같습니다.
따라서 $\delta_{ij} a_j = a_i$가 되는 것이죠. 


더 일반적으로,

$$
\delta_{ij} A_{jk} = A_{ik}, \qquad
A_{ij}\delta_{jk} = A_{ik}.
$$

### 5.3) 편미분 표현

$$\frac {\partial x_i} {\partial x_j}  = \delta_{ij}$$ 입니다.

$i=j$이면 1,
$i \neq j$이면 0이니까 그렇습니다.

이런 스킬은 복잡한 계산에서 매우 유용하게 사용되니 그냥 '이런 게 있구나'하고 넘어갑니다.


---

## 6. Permutation tensor (Levi-Civita symbol, 순열 텐서)

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

### 6.1) levi-civita 텐서는 반대칭이다 

$\varepsilon_{ijk}$는 어떤 두 인덱스를 서로 바꾸면 부호가 바뀝니다.

$$
\varepsilon_{ijk} = -\varepsilon_{jik} = -\varepsilon_{ikj} = \cdots
$$

그래서 “순열 텐서 = 반대칭 텐서”라고 이해할 수 있습니다.

---

## 7. 외적/컬/스칼라 삼중곱을 텐서 표기법으로 쓰기

먼저 Del operator $\nabla$ Operator를 정의하면, vector caculus가 매우 쉬워집니다.

$$\nabla  := \hat{e_i} \frac {\partial } {\partial x_i} = \hat{e_1} \frac {\partial } {\partial x_1} + \hat{e_2} \frac {\partial } {\partial x_2} + \hat{e_3} \frac {\partial } {\partial x_3} $$

 입니다.  


### 7.1) Divergence

$u_j = (u_1, u_2, u_3)$인 벡터가 있다고 합시다.
그리고 각 좌표의 단위벡터를 $\hat{e_j}$라고 합시다.

그러면 1차텐서 $u_j$는 아래와 같이 쓸 수 있겠죠?
$$u_j = u_1 \hat {e_1} + u_2 \hat {e_2} + u_3 \hat {e_3} = u_j \hat {e_j} $$

> 헷갈린다면 dummy index가 j라는 것을 상기해 보시기 바랍니다.

벡터 u_j의 divergence는 벡터 표기법으로 쓰면 $\nabla \cdot \mathbf{u} $입니다.
이것을 텐서 표기법으로 써봅시다.

별 것 없습니다. 그냥 정의를 그대로 쓰면 됩니다.

$$
\hat{e_i} \frac {\partial } {\partial x_i} \cdot u_j \hat{e_j}
$$

여기서 벡터는 $\hat{e_i}$와 $\hat{e_j}$ 밖에 없습니다. $u_j$는 성분이고, $\partial x_i$는 편미분 기호이니까요.

내적연산자 " $\cdot$ " 는 벡터에만 적용되는 것이죠? 
따라서 아래와 같이 다시 쓸 수 있습니다.

$$
\hat{e_i} \frac {\partial } {\partial x_i} \cdot u_j \hat{e_j} = \frac{\partial u_j} {\partial x_i} \hat{e_i} \cdot \hat{e_j}
$$

$\hat{e_i} \cdot \hat{e_j}$ 부분이 좀 찝집합니다. 
i = 1,2,3이며 마찬가지로 j = 1,2,3 일 때 
$$
\hat{e_1} \cdot \hat{e_2} = 0 
$$


이죠? 반면에 

$$
\hat{e_1} \cdot \hat{e_1} = 1 
$$
입니다.

즉, $i=j$이면 1이고 $i \neq j$이면 0입니다.
$\delta_{ij}$의 정의와 **정확히 같습니다**.

내적은 기하학적으로 **얼마나 같은 방향을 향하고 있는가**를 따지는 것이기 때문입니다.

따라서 
$$\hat{e_i} \cdot \hat{e_j} = \delta_{ij}$$ 입니다.

결국 우리의 목적이었던 divergence 연산은


$$
 \frac{\partial u_j} {\partial x_i} \hat{e_i} \cdot \hat{e_j}
 = \frac{\partial u_j} {\partial x_i} \delta_{ij}
$$가 됩니다. kronecker delta의 역할(subsituting property)을 상기하여 인덱스를 바꿔봅시다.

 
 $$

\frac{\partial u_j} {\partial x_i} \delta_{ij}  = \frac{\partial u_j} {\partial x_j}

$$

우리가 기존에 알고 있던 divergence와 일치합니다.

$$\nabla \cdot \mathbf{u} = \frac {\partial u_j} {\partial x_j}$$

헷갈린다면 dummy index를 직접 전개해 보시길 바랍니다.

편미분 기호를 계속 쓰기 귀찮으니까 $$ \frac {\partial u_j} {\partial x_j} = x_{j,j} $$ 와 같이 쉼표를 찍고 표기하기도 합니다.

### 7.2) Cross product 

이제 자세한 계산과정은 생략하겠습니다. 

벡터 $\vec a,\vec b$에 대해 외적 $\vec c=\vec a\times \vec b$의 성분은

외적, 내적은 **벡터**에 적용하는 것이지 **성분**에 정의되는 연산이 아니라고 했습니다!

$$

a_j\hat{e_j} \times b_k \hat{e_k}
= a_jb_k \hat{e_j} \times \hat{e_k}
= a_jb_k \varepsilon_{ijk} \hat{e_i} 

$$ 


> 여기서 $ \hat{e_j} \times \hat{e_k} = \varepsilon_{ijk} \hat{e_i}  $가 헷갈리신다면, 외적의 기하학적 정의와 오른손 법칙을 떠올려보시길 바랍니다. 



### 7.3) Curl
이번에도 그냥 정의대로 쭉 붙여서 쓰면 됩니다.

$$
\nabla \times \vec{u} 
=  (\hat{e_j} \frac{\partial } {\partial x_j})   \times  (u_k \hat{e_k})
$$

>> 여기서 j,k는 모두 dummy index입니다.

$$
 = \frac {\partial u_k} {\partial x_j} \hat{e_j} \times \hat{e_k}
 = \varepsilon_{ijk} u_{k,j} \hat{e_i}
 $$

 마찬가지로 헷갈리신다면 직접 전개해 보시길 추천드립니다.


### 7.4) Gradient

0차텐서(스칼라) $Phi$에 대하여
gradient $Phi$는


$$
\nabla \Phi = (\hat{e_j} \frac{\partial } {\partial x_j}) \Phi
=  \frac {\partial \Phi} {\partial x_j} \hat{e_j}
 = \Phi,j
$$

0차텐서를 편미분 했더니 1차텐서가 되었습니다.

**n차 텐서의 편미분은 (n+1)차 텐서가 된다**는 것을 증명없이 받아들입시다.












---

## 8. Kronecker delta와 permutation tensor의 핵심 항등식

이제 진짜 거의 다 왔습니다. 

아래 항등식은 외적을 단순화해 줍니다. 정신 건강상 외워두면 좋지만 그래도 증명은 한 번 하고 갑시다.

### 8.1) 한 번 수축한 항등식

$$
\varepsilon_{ijk}\varepsilon_{imn}
=
\delta_{jm}\delta_{kn}-\delta_{jn}\delta_{km}.
$$

우선 i는 dummy index이니 summation해서 없어질 겁니다.
그리고 $j=k$이거나 $m=n$이면 levi civita 텐서는 0이 됩니다.
그럼 $j \neq k$ , $m \neq n$의 경우만 보면 되겠네요.

$j \neq k$ 인 경우에, 세 인덱스 ijk는 모두 서로다른 값이어야 1또는 -1이 됩니다.
$(m,n) = (j,k)$와 같이 순서대로 인덱스가 배열되는 경우에는
$$
\varepsilon_{ijk} \varepsilon_{imn} = \varepsilon^2_{ijk} = 1 
$$
+1또는 -1의 제곱이니 무조건 1이 되겠죠.

$(m,n) = (k,j)$와 같이 반대 순서로 인덱스가 배열되는 경우에는
$$
\varepsilon_{ijk} \varepsilon_{imn} = \varepsilon_{ijk} (- \varepsilon_{ijk})  = -1  
$$

정리해보면,
$(m,n) = (j,k)$이면 +1
$(m,n) = (k,j)$ -1
그 외에는 $0$

이것을 kronecker delta로 표현하면
$$ \delta_{jm}\delta_{kn}-\delta_{jn}\delta_{km} $$
이 됩니다.


(가장 자주 쓰는 형태입니다. 외적-외적 전개할 때 거의 무조건 나옵니다.)

### 8.2) 두 번 수축한 항등식

$$
\varepsilon_{ijk}\varepsilon_{ijn}
=
2\,\delta_{kn}.
$$

이 식은 7.1에서 증명한 한 번 수축한 항등식의 인덱스 m에 j를 대입하면 됩니다.
인덱스 i,j 두 개가 겹치죠? 그래서 두 번 수축한 항등식입니다.
$$
\varepsilon_{ijk} \varepsilon_{ijn} = \delta_{jj} \delta_{kn} - \delta{jn} \delta_{kj} 
$$
여기서
$$
\delta_{jj} = \delta_{11} + \delta_{22} + \delta_{33} = 3
$$
따라서 
$$
\delta_{jj}\delta_{kn} - \delta_{jn} \delta_{kj}  = 3 \delta_{jn} - \delta_{jn} = 2 \delta_{jn}
$$

특히 3차원에서만 성립하는 **외적 특유의 단순화**가 여기서 나옵니다.

---

이제 텐서 노테이션을 이해하기위해서 더 필요한 것은 없습니다.
아직 찝찝한 분들을 위해서 하나의 예시를 보겠습니다.

## 예시: $\vec a \times (\vec b \times \vec c)$ 전개가 왜 쉬워지나

주로 물리학과나 공대에서 BAC CAB 공식이라고 외우는 삼중 외적 항등식

$$
\vec a \times (\vec b \times \vec c)
= \vec b(\vec a\cdot\vec c)-\vec c(\vec a\cdot\vec b)
$$

도 사실 $\varepsilon$와 $\delta$로 2~3줄이면 정리됩니다. 성분으로 쓰려면 적어도 20줄 넘게 써야할 겁니다.

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
> - 두 개를 같이 쓰면 외적/컬 같은 복잡한 벡터 연산을 쉽게 할 수 있습니다.

{% include comments.html %}

