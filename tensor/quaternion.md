---
layout: article
title: "Quaternion (사원수)"
permalink: /tensor/quaternion/
sidebar:
  nav: subjects
mathjax: true
mathjax_autoNumber: true
---

## 주의
아래 개념이 익숙하지 않으면 읽다가 헷갈릴 수 있습니다.

선형대수학 - 직교행렬, 역행렬, 내적/외적, 회전행렬 \\
기하학 - 회전축(axis), 회전각(angle)  \\
벡터해석 - dot product, cross product

이 글의 목표는 간단합니다. \\
**회전행렬을 곱해서 벡터를 회전시킬 수도 있지만(Euler Rotation) 복소수의 확장판(?) 
격인 quaternion (사원수)로도 똑같이 할 수 있다**는 걸 확인하는 겁니다.

---

## 0. Quaternion (사원수) 정의

실수 -> 복소수 -> 사원수 순으로 확장된다고 생각하면 됩니다.\\
실수축은 직선입니다.\\
복소수는 실수에 허수 한 개를 더한 것입니다. 즉, 복소 공간은 2차원입니다. (실수축을 한 평면에 대해 회전시키는 것)\\
사원수는 실수에 허수 세 개를 더한 것입니다. (실수축을 세 평면에 대해 회전시키는 것)

Quaternion은 **실수 하나 + 벡터 하나**라고 생각하면 편합니다.

$$
q = q_0 + q_1\mathbf{i} + q_2\mathbf{j} + q_3\mathbf{k}
$$

혹은

$$
q = (q_0,\mathbf{q}), \qquad \mathbf{q}=(q_1,q_2,q_3).
$$

라고 씁니다.

## 1. 사원수의 더하기

덧셈은 복소수를 더하듯이 실수는 실수끼리 허수는 허수끼리 더하면 됩니다.
가령 새로운 사원수 $\mathbf{p}$를

$$
\mathbf{p} = p_0 + p_1\mathbf{i} + p_2\mathbf{j} + p_3 \mathbf{k}
$$

와같이 정의했을 때,
두 사원수를 더하면 

$$
\mathbf{p+q} = (p_0 + q_0) + (p_1 + q_1)\mathbf{i} + (p_2 + q_2)\mathbf{j} + (p_3 + q_3)\mathbf{k}
$$

처럼 새로운 사원수가 됩니다.

--

## 2. 사원수의 곱

기본 규칙은 이겁니다.

$$
\mathbf{i}^2=\mathbf{j}^2=\mathbf{k}^2=-1
$$

그리고

$$
\mathbf{i}\mathbf{j}=\mathbf{k},\quad
\mathbf{j}\mathbf{k}=\mathbf{i},\quad
\mathbf{k}\mathbf{i}=\mathbf{j}
$$


반대로 순서 바꾸면 부호가 바뀝니다.

$$
\mathbf{j}\mathbf{i}=-\mathbf{k},\quad
\mathbf{k}\mathbf{j}=-\mathbf{i},\quad
\mathbf{i}\mathbf{k}=-\mathbf{j}.
$$

이를 조합하면 
$$
ijk = k^2 = -1
$$

이 된다는 것도 생각할 수 있겠네요.

Quaternion 곱은 **교환법칙이 성립하지 않습니다.** \\
(이거 꼭 기억해야 합니다.)

이걸 매번 i,j,k로 전개하기 싫으니까, 벡터식으로 외워버리면 됩니다.

$$
p=(p_0,\mathbf{p}),\quad q=(q_0,\mathbf{q})
$$

이면

$$
\mathbf{pq}=
\Big(
p_0q_0-\mathbf{p}\cdot\mathbf{q},\ 
p_0\mathbf{q}+q_0\mathbf{p}+\mathbf{p}\times\mathbf{q}
\Big).
$$

증명해보죠.

$$
\mathbf{p} = (p_1,p_2,p_3) , \mathbf{q} = (q_1,q_2,q_3) 
$$

라고 정의합시다. (각각 세 개의 성분을 가진 벡터입니다)

$$
\mathbf{pq} = (p_0 + p_1\mathbf{i} + p_2\mathbf{j} + p_3 \mathbf{k}) (q_0 + q_1\mathbf{i} + q_2\mathbf{j} + q_3\mathbf{k})
= p_0q_0 + p_0(q_1\mathbf{i} + q_2\mathbf{j} + q_3\mathbf{k}) + q_0(p_1\mathbf{i}+p_2\mathbf{j}+p_3\mathbf{k})
+ \mathbf{p} \times \mathbf{q} - \mathbf{p} \cdot \mathbf{q}

= p_0q_0 - \mathbf{p}\cdot\mathbf{q} + \mathbf{p} \times \mathbf{q} + p_0\mathbf{q} + q_0\mathbf{p}

$$$



여기서 중요한 점은, 서로다른 사원수를 곱하여 얻은 $증명해보죠.

$$
\vec{p} = (p_1,p_2,p_3) , \vec{q} = (q_1,q_2,q_3) 
$$

라고 정의합시다. (각각 세 개의 성분을 가진 벡터입니다)
즉, 사원수 $\mathbf{p}$와 $\mathbf{q}$는 각각 

$$
\mathbf{p} = p_0 + \vec{p}, \mathbf{q} = q_0 + \vec{q}
$$

그러면 사원수의 곱 $\mathbf{pq}$는



$$
\mathbf{pq} = (p_0 + p_1\mathbf{i} + p_2\mathbf{j} + p_3 \mathbf{k}) (q_0 + q_1\mathbf{i} + q_2\mathbf{j} + q_3\mathbf{k})
= p_0q_0 + p_0(q_1\mathbf{i} + q_2\mathbf{j} + q_3\mathbf{k}) + q_0(p_1\mathbf{i}+p_2\mathbf{j}+p_3\mathbf{k})
+ \vec{p} \vec{q}
$$

여기서 마지막 항인 $\vec{p}\vec{q}$ 부분을 생각해봅시다. 같은 단위벡터끼리 곱해지면 음수가 된다고 했습니다.
그럼 음수가 붙은 내적이 하나 나오겠네요. 그리고 단위벡터의 곱은 오른손법칙을 따르는 외적과 같습니다.
그러면 양수가 붙은 외적이 하나 나오겠네요.
따라서

$$
\vec{p} \vec{q} = -\vec{p} \cdo \vec{q} + \vec{p} \times \vec{q}
$$




$$
= p_0q_0 - \vec{p}\cdot\vec{q} + \vec{p} \times \vec{q} + p_0\vec{q} + q_0\vec{p}
$$



여기서 중요한 점은, 서로다른 사원수를 곱하여 얻은 $\mathbf{p}\mathbf{q}$는 여전히 사원수라는 것입니다.



--

## 3. Conjugate / norm / inverse
사원수는 복소수의 확장판(?) 이므로 복소수와 유사하게 conjugate, norm, inverse를 정의할 수 있습니다.

켤레(conjugate)는 벡터부분의 부호를 바꾸는 겁니다.

$$
q^*=(q_0,-\mathbf{q})
= q_0 - q_1\mathbf{i} - q_2\mathbf{j} - q_3\mathbf{k}.
$$

당연히

$$
(q^*)^* = q
$$

입니다.

그리고 norm은

$$
|q| = \sqrt{q^*q}=\sqrt{qq^*}
$$

이며 실제로 계산하면

$$
q^*q = (q_0 - \vec{q})(q_0 + \vec{q}) = q_0^2 + q_0\vec{q} - q_0\vec{q} - \vec{q}\vec{q}
$$

아까 연산을 떠올려보면 음수가 붙은 내적, 양수가 붙은 외적이 하나 나왔었죠?
$$
\vec{q} \vec{q} = -\vec{q} \cdot \vec{q} + \vec{q} \times \vec{q}
$$

따라서

$$
q^*q = (q_0 - \vec{q})(q_0 + \vec{q}) = q_0^2 + q_0\vec{q} - q_0\vec{q} - \vec{q}\vec{q}
= q_0^2 + q_0 \vec{q} - q_0 \vec{q} + \vec{q} \cdot \vec{q} - \vec{q} \times \vec{q}
$$

서로 상쇄하여 없어지는 항이 있고, 또 같은 벡터의 외적은 0입니다. 따라서

$$
q^*q = q_0^2 + \vec{q} \cdot \vec{q} 
= q_0^2 + q_1^2 + q_2^2 + q_3^2
$$

여기서 루트를 취해주면 norm이 되겠네요. 그런데, 어차피 크기라는 것은 스칼라 아닙니까?
따라서 

$$
q^*q = qq^*
$$
라는 것도 알 수 있습니다.

inverse는

$$
q^{-1}=\frac{q^*}{|q|^2}.
$$

conjugate, norm, inverse를 조합하여 사원수의 몇가지 성질을 적어보자면,
$$
(pq)^* = q^*p^* \\
|q| = \sqrt{q^*q} \\
|pq|^2 = |p|^2 |q|^2 \\ 
q^-1 = \frac{q^*} {|q|^2}    \because q^-1q = qq^-1 = 1,   q \frac{q^*} {|q|^2} = \frac{ |q|^2}{|q|^2} = 1
$$

뭔가 벡터 같기도 하고, 행렬 같기도 하고, 그렇죠?

---

## 4. Rotation operator : $L_q(v)=qvq^*$
이제 진짜 하고 싶은 말을 합시다. Quaternion은 **3차원 회전**을 아주 우아하게 표현하는 방법입니다.

사원수는 \mathbb{R}^4에 속하는 수입니다. 4차원을 가지고 어떻게 벡터 (\mathbb{R}^3)을 회전시킨다는 걸까요?
여기서 **pure quaternion**을 정의합시다.
pure quaternion $\mathbf{v}$는 실수부가 0인 사원수입니다.

$$
\mathbf{v} = (0, \vec{v})
$$


그리고 unit quaternion (norm이 1인 사원수) $q$에 대해

$$
|q| = \sqrt{q_0^2 + q_1^2 + q_2^2 + q_3^2} = 1
$$ 이므로

$$
q_0^2 + |\vec{q}|^2 = 1 
$$

이 되네요? (벡터 $\vec{q}$의 norm $|\vec{q}| = \sqrt{q_1^2 + q_2^2 + q_3^2$ 이니까요)

여기서 어떤 각도 $\theta$가 존재하여, $\cos^2\theta = q_0^2$, $\sin^2\theta = |\vec{q}|^2$를 만족한다고 둡시다.
그러면 unit quaternion은 아래와 같이 쓸 수 있습니다.

$$
q = cos \theta + \vec{u} sin\theta,  \vec{u} = \frac{\vec{q}} { |\vec{q}|}
$$

여기서 $\vec{u}$는 unit quaternion을 자신의 크기로 나눈 단위 quaternion입니다.
unit quaternion $\mathbf{q}$를 이용하여, 우리는 이제 벡터 $\vec{v} \in \mathbb{R}^3$의 회전을 아래와 같이 정의할 겁니다.

$$
L_q(\vec{v}) := q\vec{v}q^*
$$


처음 보면 “왜 하필 $qvq^*$냐?” 싶은데, \\
일단 이걸 받아들이고 계산을 해보면 **회전이다**는 걸 보게 됩니다.

---

## 5. $qvq^*$ 전개하면 무슨 꼴이 나오나

$q=(q_0,\mathbf{q})$, $v=(0,\mathbf{v})$라고 하고 \\
아까 곱셈 공식으로 전개하면 

$$
L_q(\vec{v}) = q\vec{v}q^*
             = (q_0 + \vec{q})( 0 +  \vec{v}) q^*
             = ( - \vec{q} \cdot \vec{v} + \vec{q} \times \vec{v} + q_0 \vec{v}) (q_0 - \vec{q})
$$


$$
= (\vec{q} \cdot \vec{v})q_0 - (\vec{q} \times \vec{v} + q_0\vec{v}) \cdot (-\vec{q})
 + (\vec{q} \times \vec{v}) \times (-\vec{q}) + q_0(\vec{q} \times \vec{v} + q_0\vec{v})
 + (\vec{q} \cdot \vec{v}) \vec{q}
= q_0^2 \vec{v} + q_0(\vec{q} \times \vec{v}) - q_0(\vec{v} \times \vec{q}) + (\vec{q} \cdot \vec{v}) \vec{q}
= q_0^2\vec{v} - |\vec{q}|^2\vec{v} + 2q_0(\vec{q} \times \vec{v} + 2(\vec{q} \cdot \vec{v} vec{q}
= (q_0^2 - |\vec{q}|^2) \vec{v} + 2(\vec{q}\cdot\vec{v})\vec{q} + 2q_0 (\vec{q} \times \vec{v})

$$

(솔직히 이부분은 그냥 받아들이고 넘기셔도 이해하는 데 문제 없습니다...)

결론만 말하자면 quaternion과 그 conjugate를 양 옆에 곱해서
새로 얻은 벡터 $\vec{v}'$는

$$
\mathbf{v}'
=
(q_0^2-\|\mathbf{q}\|^2)\mathbf{v}
+2(\mathbf{q}\cdot\mathbf{v})\,\mathbf{q}
+2q_0(\mathbf{q}\times\mathbf{v})
$$

가 됩니다. 즉,

$$
L_q(v) = (0,\mathbf{v}')
$$

로 다시 pure quaternion이 됩니다.

여기서 중요한 성질이 나옵니다.

1) 길이가 보존됩니다.

$$
|L_q(v)| = |qvq^*| = |q||v||q^*| = |v|
$$


2) $\mathbf{v}$가 $\mathbf{q}$와 평행한 경우는 그대로입니다. \\
즉 회전축 방향이 생깁니다.

예를 들어 $\vec{v}=k\vec{q}$라 두면 $q(자기자신)q^*$을 해도 방향이 변하지 않습니다.

$$
q\vec{v}q^* = q(k\vec{q})q^*
            = (q_0^2 - |\vec{q}|^2(k\vec{q}) + 2(\vec{q} \cdot k\vec{q})\vec{q} + 2q_0(\vec{q} \times \vec{q})
            = kq_0^2\vec{q} + k|\vec{q}|^2\vec{q}
            = k(q_0^2 + |\vec{q}|^2)\vec{q} = k\vec{q}

$$

꼴로 남아서 축이 고정되는 걸 볼 수 있습니다. \\


또 선형성도 있습니다.

$$
L_q(\alpha_1 \vec{v_1}+\alpha_2 \vec{v_2})=\alpha_1 L_q(\vec{v_1})+\alpha_2 L_q(\vec{v_2}).
$$



### THM 1
For any unit quaternion $q$, $q = cos \frac{\theta}{2} + \vec{u} sin \frac{\theta}{2}$ ,
and any $\vec{v} \in \mathbb{R}^3$, the action $q\vec{v}q*$ is a rotation of $\vec{v}$ by angle $\theta$
about axis $\vec{u}$.

<img width="601" height="607" alt="화면 캡처 2026-01-06 041301" src="https://github.com/user-attachments/assets/c86030c1-11d0-499f-8dbd-a5a691af152f" />





---


## Example : 축 $(1,1,1)$, 각도 $2\pi/3$

예시 하나 보겠습니다.

회전축이 $(1,1,1)$이면 단위벡터는

$$
\hat{\mathbf{u}}=\frac{1}{\sqrt{3}}(1,1,1).
$$

회전각이

$$
\theta=\frac{2\pi}{3}
$$

이면

$$
q=\cos\frac{\theta}{2}+\hat{\mathbf{u}}\sin\frac{\theta}{2}
=\cos\frac{\pi}{3}+\hat{\mathbf{u}}\sin\frac{\pi}{3}
=\frac12+\frac{\sqrt{3}}{2}\hat{\mathbf{u}}
=\frac12+\frac12(\mathbf{i}+\mathbf{j}+\mathbf{k}).
$$

이제 basis vector $\hat{\mathbf{i}}=(1,0,0)$이 어떻게 가는지 보겠습니다. \\
Rodrigues 공식 그대로 대입하면 됩니다.

$$
\mathbf{v}=\hat{\mathbf{i}},\quad
\cos\theta=\cos\frac{2\pi}{3}=-\frac12,\quad
\sin\theta=\sin\frac{2\pi}{3}=\frac{\sqrt{3}}{2}.
$$

또

$$
\hat{\mathbf{u}}\cdot\hat{\mathbf{i}}=\frac{1}{\sqrt{3}}.
$$

그리고

$$
\hat{\mathbf{u}}\times\hat{\mathbf{i}}
=
\frac{1}{\sqrt{3}}(1,1,1)\times(1,0,0)
=
\frac{1}{\sqrt{3}}(0,1,-1).
$$

따라서

$$
\mathbf{v}'
=
\cos\theta\,\hat{\mathbf{i}}
+(1-\cos\theta)(\hat{\mathbf{u}}\cdot\hat{\mathbf{i}})\hat{\mathbf{u}}
+\sin\theta(\hat{\mathbf{u}}\times\hat{\mathbf{i}})
$$

를 계산하면

$$
\mathbf{v}'=(0,1,0)=\hat{\mathbf{j}}
$$

가 됩니다.

즉,

$$
\hat{\mathbf{i}}\to \hat{\mathbf{j}}
$$

이고 마찬가지로 계산하면

$$
\hat{\mathbf{j}}\to \hat{\mathbf{k}},\qquad
\hat{\mathbf{k}}\to \hat{\mathbf{i}}
$$

처럼 순환합니다.

---

## 결론


Quaternion은 3차원 회전을 표현합니다. \\
벡터의 크기를 보존하며, 방향만 회전시킵니다. \\

또 Euler angle처럼 “회전을 세 번 나눠서 순서대로 곱하는 방식”이 아니라, \\
**한 번의 회전을 하나의 quaternion으로** 표현할 수 있습니다. \\

그래서 Euler angle에서 자주 생기는 문제들(순서에 따른 결과 변화, gimbal lock 등)에서 자유롭습니다. \\

따라서 게임(3D 그래픽), 유체역학 시뮬레이션(CFD) 등에서 물체나 벡터를 회전시킬 때 사용합니다.

$$
(0,\mathbf{v}') = q(0,\mathbf{v})q^*
$$

입니다.

[quarternion.pdf](https://github.com/user-attachments/files/24426729/quarternion.pdf)

<embed src="quarternion.pdf" type="application/pdf" width="100%" height="900px">

2026.01.05

{% include comments.html %}
