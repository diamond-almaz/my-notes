---
layout: default
title: Главная страница
---

# Мои заметки

## JavaScript концепции

{% for doc in site.docs %}
  - [{{ doc.title | default: doc.name }}]({{ doc.url }})
{% endfor %}