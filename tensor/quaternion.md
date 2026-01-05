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

## 1. Quaternion (사원수) 정의

실수 -> 복소수 -> 사원수 순으로 확장된다고 생각하면 됩니다.
실수축은 직선입니다.
복소수는 실수에 허수 한 개를 더한 것입니다. 즉, 복소 공간은 2차원입니다. (실수축을 한 평면에 대해 회전시키는 것)
사원수는 실수에 허수 세 개를 더한 것입니다. (실수축을 세 평면에 대해 회전시키는 것)

Quaternion은 **실수 하나 + 벡터 하나**라고 생각하면 편합니다.

$$
q = q_0 + q_1\mathbf{i} + q_2\mathbf{j} + q_3\mathbf{k}
$$

혹은

$$
q = (q_0,\mathbf{q}), \qquad \mathbf{q}=(q_1,q_2,q_3).
$$

다른 quaternion $p$도 똑같이

$$
p=(p_0,\mathbf{p})
$$

라고 씁니다.

덧셈은 그냥 성분끼리 더하면 됩니다.

---

## 2. 곱셈 규칙 

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

그래서 quaternion 곱은 **교환법칙이 안 됩니다.** \\
(이거 꼭 기억해야 합니다.)

이걸 매번 i,j,k로 전개하기 싫으니까, 벡터식으로 외워버리면 됩니다.

$$
p=(p_0,\mathbf{p}),\quad q=(q_0,\mathbf{q})
$$

이면

$$
pq=
\Big(
p_0q_0-\mathbf{p}\cdot\mathbf{q},\ 
p_0\mathbf{q}+q_0\mathbf{p}+\mathbf{p}\times\mathbf{q}
\Big).
$$

헷갈리면 직접 전개해보면 됩니다. (근데 귀찮으니까 보통 이걸 외웁니다)

---

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
qq^* = q_0^2+q_1^2+q_2^2+q_3^2.
$$

따라서 inverse는

$$
q^{-1}=\frac{q^*}{|q|^2}.
$$

특히 $|q|=1$ (unit quaternion)이면

$$
q^{-1}=q^*
$$

로 끝납니다.

또 자주 쓰는 성질 몇 개만 적어두면

$$
(pq)^* = q^*p^*,\qquad |pq|=|p||q|.
$$

---

## 4. Rotation operator : $L_q(v)=qvq^*$

이제 진짜 하고 싶은 말을 합시다. Quaternion은 **3차원 회전**을 아주 우아하게 표현하는 방법입니다.

3D 벡터 $\mathbf{v}\in\mathbb{R}^3$를 quaternion으로 올릴 때는 \\
실수부를 0으로 만들어서

$$
v=(0,\mathbf{v})
$$

라고 둡니다. (pure quaternion)

그리고 unit quaternion $q$에 대해

$$
L_q(v) := qvq^*
$$

라고 정의합니다.

처음 보면 “왜 하필 $qvq^*$냐?” 싶은데, \\
일단 이걸 받아들이고 계산을 해보면 **회전이다**는 걸 보게 됩니다.

---

## 5. $qvq^*$ 전개하면 무슨 꼴이 나오나

$q=(q_0,\mathbf{q})$, $v=(0,\mathbf{v})$라고 하고 \\
아까 곱셈 공식으로 전개하면 (중간 과정은 길어서 생략)

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

여기서 확인해야 할 포인트는 딱 두 개입니다.

1) 길이가 보존됩니다.

$$
|L_q(v)| = |qvq^*| = |q||v||q^*| = |v|
$$

(특히 $|q|=1$이면 바로 보입니다)

2) $\mathbf{v}$가 $\mathbf{q}$와 평행한 경우는 그대로입니다. \\
즉 회전축 방향이 생깁니다.

예를 들어 $\mathbf{w}=k\mathbf{q}$라 두면

$$
q(kw)q^* = kq
$$

꼴로 남아서 축이 고정되는 걸 볼 수 있습니다. \\
(헷갈리면 직접 위 전개식에 $\mathbf{v}\parallel\mathbf{q}$ 넣어보면 됩니다)

또 선형성도 있습니다.

$$
L_q(\alpha_1 v_1+\alpha_2 v_2)=\alpha_1 L_q(v_1)+\alpha_2 L_q(v_2).
$$

---

## 6. unit quaternion은 결국 axis-angle이다

unit quaternion이면

$$
q_0^2+\|\mathbf{q}\|^2=1
$$

이니까, 어떤 각 $\theta$가 있어서

$$
q_0=\cos\frac{\theta}{2},\qquad \|\mathbf{q}\|=\sin\frac{\theta}{2}
$$

로 쓸 수 있습니다.

그리고 회전축 단위벡터를

$$
\hat{\mathbf{u}}=\frac{\mathbf{q}}{\|\mathbf{q}\|}
$$

라 두면

$$
q=\left(\cos\frac{\theta}{2},\ \hat{\mathbf{u}}\sin\frac{\theta}{2}\right)
$$

가 됩니다.

이 상태에서 $qvq^*$를 정리하면 결국 우리가 아는 Rodrigues 공식이 나옵니다.

$$
\mathbf{v}'
=
\cos\theta\,\mathbf{v}
+(1-\cos\theta)(\hat{\mathbf{u}}\cdot\mathbf{v})\hat{\mathbf{u}}
+\sin\theta(\hat{\mathbf{u}}\times\mathbf{v}).
$$

즉 결론은 이겁니다.

**unit quaternion $q$는 “축 $\hat{\mathbf{u}}$로 각 $\theta$만큼 회전”을 표현한다.** \\
그리고 실제 회전 적용은 $qvq^*$로 한다.

---

## 7. Example : 축 $(1,1,1)$, 각도 $2\pi/3$

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



{% include comments.html %}
