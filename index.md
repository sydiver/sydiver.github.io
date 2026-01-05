---
layout: article
title: "유체노트"
permalink: /
sidebar:
  nav: subjects
---

유체/수학 정리 노트입니다. 실험 영상과 CFD 결과도 같이 올립니다.

---

{% for sec in site.data.navigation.subjects %}
## {{ sec.title }}

<ul>
  {% for item in sec.children %}
    {% if item.url and item.url != "" %}
      <li><a href="{{ item.url }}">{{ item.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>
{% endfor %}
