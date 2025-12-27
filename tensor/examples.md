---
layout: article
title: "연습문제"
permalink: /tensor/index-notation-examples/
sidebar:
  nav: subjects
mathjax: true
mathjax_autoNumber: true
---

공대 유체/연속체역학에서 **아인슈타인 표기법(Einstein summation convention)**을 쓰면  
벡터·텐서 항등식들을 아주 짧고 정확하게 정리할 수 있습니다.

이 글은 **index notation**을 연습할 수 있는 예제입니다. 
---

##  벡터 항등식을 index notation으로 증명

\(\mathbf{a}(\mathbf{x}), \mathbf{b}(\mathbf{x})\): vector fields, \(\phi(\mathbf{x})\): scalar field.

---

### (1) \(\nabla\cdot(\phi\mathbf{a})=(\nabla\phi)\cdot\mathbf{a}+\phi(\nabla\cdot\mathbf{a})\)

$$
\partial_i(\phi a_i)=(\partial_i\phi)a_i+\phi(\partial_i a_i)
$$

---

### (2) \(\nabla\times(\phi\mathbf{a})=(\nabla\phi)\times\mathbf{a}+\phi(\nabla\times\mathbf{a})\)

좌변 \(i\)-성분:

$$
(\nabla\times(\phi\mathbf{a}))_i=\varepsilon_{ijk}\partial_j(\phi a_k)
=\varepsilon_{ijk}(\partial_j\phi)a_k+\phi\,\varepsilon_{ijk}\partial_j a_k
$$

---

### (3) \(\nabla\cdot(\nabla\times\mathbf{a})=0\)

$$
\nabla\cdot(\nabla\times\mathbf{a})
=\partial_i(\varepsilon_{ijk}\partial_j a_k)
=\varepsilon_{ijk}\partial_i\partial_j a_k=0
$$

(혼합편미분 대칭 텐서 × \(\varepsilon_{ijk}\) 반대칭 텐서)

---

### (4) \(\nabla\times(\nabla\phi)=0\)

$$
(\nabla\times\nabla\phi)_i=\varepsilon_{ijk}\partial_j\partial_k\phi=0
$$

---

### (5) \(\nabla\times(\mathbf{a}\times\mathbf{b})\)

$$
\nabla\times(\mathbf{a}\times\mathbf{b})
=(\mathbf{b}\cdot\nabla)\mathbf{a}-(\mathbf{a}\cdot\nabla)\mathbf{b}
+\mathbf{a}(\nabla\cdot\mathbf{b})-\mathbf{b}(\nabla\cdot\mathbf{a})
$$

---

### (6) \(\nabla\cdot(\mathbf{a}\times\mathbf{b})\)

$$
\nabla\cdot(\mathbf{a}\times\mathbf{b})
=(\nabla\times\mathbf{a})\cdot\mathbf{b}-(\nabla\times\mathbf{b})\cdot\mathbf{a}
$$

---

### (7) \(\nabla\cdot(\mathbf{a}\mathbf{b})\) (dyadic)

$$
\nabla\cdot(\mathbf{a}\mathbf{b})
=(\nabla\cdot\mathbf{a})\,\mathbf{b}+(\mathbf{a}\cdot\nabla)\mathbf{b}
$$

---

### (8) \(\nabla\times(\nabla\times\mathbf{a})=\nabla(\nabla\cdot\mathbf{a})-\nabla^2\mathbf{a}\)

$$
\nabla\times(\nabla\times\mathbf{a})
=\nabla(\nabla\cdot\mathbf{a})-\nabla^2\mathbf{a}
$$

---
