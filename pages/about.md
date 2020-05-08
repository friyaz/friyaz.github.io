---
layout: page
title: About Me
permalink: /about-me/
weight: 3
---

# **About Me**

Hi I am **{{ site.author.name }}** :wave:,<br>
This personal website is still under construction, stay tuned!

<div class="row">
{% include about/skills.html title="Programming Skills" source=site.data.programming-skills %}
</div>
**Programming languages**: 
- C/C++
- Python
- Java
- x86 Assembly
- RISC-V Assembly (Learning)
- Javascript

**Database** : 
- MySQL
- PostgreSQL

**Frameworks, Libraries and Programming Tools** :
- Git
- Tensorflow
- SymPy
- HTML/CSS	
- Flask

<div class="row">
{% include about/timeline.html title="Experiences" source=site.data.experiences-timeline %}
</div>

<div class="row">
{% include about/timeline.html title="Education" source=site.data.education-timeline %}
</div>
