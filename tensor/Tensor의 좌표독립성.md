---
layout: article
title: "왜 아인슈타인 표기법은 좌표독립적인가"
permalink: /tensor/why-einstein-notation-is-coordinate-free/
sidebar:
  nav: subjects
mathjax: true
mathjax_autoNumber: true
---

\text{공대 수업이나 물리학 책을 보면 이런 말을 자주 접합니다.}

\[
\text{``아인슈타인 표기법은 좌표계에 무관하다.''}
\]

\text{그런데 처음 이 말을 들으면 보통 이런 생각이 듭니다.}

\[
\text{``}x_i, A_{ij}\text{ 처럼 좌표를 잔뜩 쓰는데, 대체 어디가 좌표독립적이라는 거지?''}
\]

\text{이번 글에서는 이 질문에 대해,}
\text{수학적으로는 엄밀하지만 최대한 직관적으로 설명해 보겠습니다.}

---

\section*{1. 좌표독립적이라는 말의 정확한 의미}

\text{먼저 오해부터 하나 정리합시다.}

\[
\text{좌표독립적이라는 말은 ``좌표가 안 나온다''는 뜻이 아닙니다.}
\]

\text{정확히는 다음을 의미합니다.}

\[
\text{좌표계를 바꾸어도 같은 물리량을 표현한다.}
\]

\text{즉,}
\begin{itemize}
  \item \text{성분(숫자)은 바뀔 수 있지만}
  \item \text{그 성분들이 나타내는 대상은 같다}
\end{itemize}

\text{는 뜻입니다.}

---

\section*{2. 벡터는 숫자가 아니라 기하학적 대상이다}

\text{공간에 벡터 } \mathbf{v} \text{가 하나 있다고 합시다.}

\text{이 벡터는 좌표계를 잡기 전부터}
\text{공간에 그대로 존재하는 대상입니다.}

\text{다만 계산을 하려면 좌표계를 하나 정하고}
\text{성분으로 표현해야 합니다.}

\[
\mathbf{v} = v_i \hat e_i
\]

\text{여기서}
\begin{itemize}
  \item \hat e_i \text{ 는 좌표축 방향의 단위벡터}
  \item v_i \text{ 는 해당 좌표계에서의 성분}
\end{itemize}

\text{입니다.}

---

\section*{3. 좌표계를 바꾸면 무엇이 바뀌는가}

\text{이제 좌표계를 회전시켜 보겠습니다.}

\text{새 좌표계의 기저를 } \hat e'_i \text{ 라고 하면,}
\text{기저 벡터는 다음과 같이 변합니다.}

\[
\hat e'_i = Q_{ij} \hat e_j
\]

\text{여기서 } Q_{ij} \text{ 는 좌표 변환 행렬입니다.}

\text{벡터 } \mathbf{v} \text{ 는 같은 대상이므로}

\[
\mathbf{v} = v_i \hat e_i = v'_j \hat e'_j
\]

\text{가 성립합니다. 이를 대입하면}

\[
v'_j Q_{jk} \hat e_k = v_i \hat e_i
\]

\text{기저 } \hat e_k \text{ 들은 서로 독립이므로}

\[
v_i = Q_{ij} v'_j
\quad\Longrightarrow\quad
v'_j = Q_{ji} v_i
\]

\text{즉,}

\[
\text{좌표계를 바꾸면 벡터의 성분은 반드시 바뀝니다.}
\]

---

\section*{4. 텐서의 정의는 변환 법칙이다}

\text{여기서 매우 중요한 사실이 하나 나옵니다.}

\[
\text{텐서는 ``이렇게 변환된다''로 정의된다.}
\]

\text{예를 들어 2차 텐서 } A_{ij} \text{ 는}
\text{좌표 변환에 대해 다음을 만족해야 합니다.}

\[
A'_{ij} = Q_{ik} Q_{jl} A_{kl}
\]

\text{이 변환 법칙을 만족하는 대상만}
\text{우리는 **2차 텐서**라고 부릅니다.}

\[
\text{즉, 텐서란 **좌표 변환에 대해 정해진 규칙으로 변하는 물리량**입니다.}
\]

---

\section*{5. 아인슈타인 표기의 핵심 구조}

\text{이제 우리가 자주 보는 식을 하나 봅시다. 기초적인 대수식입니다.}

\[
y_i = A_{ij} x_j
\]

\text{여기서}
\begin{itemize}
  \item i \text{ 는 free index (결과의 방향)}
  \item j \text{ 는 dummy index (합을 위한 인덱스)}
\end{itemize}

\text{입니다.}

---

\section*{6. 좌표 변환을 대입해 보자}

\text{좌표계를 바꾸면 성분들은 다음과 같이 변합니다.}

\[
x'_j = Q_{jk} x_k, \qquad
A'_{ij} = Q_{ip} Q_{jq} A_{pq}
\]

\text{이를 그대로 대입하면}

\[
y'_i
= A'_{ij} x'_j
= (Q_{ip} Q_{jq} A_{pq})(Q_{jr} x_r)
\]

---

\section*{7. 더미 인덱스는 자동 소거 장치다}

\text{위 식에서 } j \text{ 는 dummy index입니다.}

\text{즉, 이름은 중요하지 않고}
\text{합만 의미합니다. 인덱스가 무엇이든 어차피 합쳐질 것이기 때문이죠.}

\text{따라서 다음이 성립합니다.}

\[
Q_{jq} Q_{jr} = \delta_{qr}
\]

\text{이를 적용하면}

\[
y'_i = Q_{ip} A_{pq} x_q
\]

\text{즉}

\[
y'_i = Q_{ip} y_p
\]

\text{가 됩니다.}

\text{이는 정확히 벡터의 좌표 변환 법칙입니다.}

---

\section*{8. 그래서 무엇이 좌표독립적인가}

\text{정리하면}

\begin{itemize}
  \item x_i, A_{ij}, y_i \text{ 는 좌표계에 따라 바뀐다}
  \item 그러나 }
  \[
  y_i = A_{ij} x_j
  \]
  \text{라는 관계식의 구조는 변하지 않는다}
\end{itemize}

\text{즉,}

\[
\text{좌표계를 어떻게 바꿔도 같은 물리적 관계를 표현한다}
\]

\text{이것이 좌표독립성입니다.}

---

\section*{9. 결론}

\[
\text{아인슈타인 표기법이 좌표독립적인 이유는}
\]

\[
\text{텐서를 변환 법칙으로 정의했고,}
\]

\[
\text{더미 인덱스의 수축이 그 변환을 정확히 상쇄하도록}
\]

\[
\text{정의하였기 때문입니다. }
\]

\[
\text{그래서 텐서 물리량이 좌표계에 무관하다는 것입니다. }
\]

{% include comments.html %}
