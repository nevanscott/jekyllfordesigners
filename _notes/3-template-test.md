---
title: Template Test
permalink: /testing/
published: false
ex:
  title: Excavation
  subtitle: A Memoir
  author: Wendy C. Ortiz
  publisher:
    name: Future Tense Books
    url: http://www.futuretensebooks.com
  tags:
    - memoir
    - literary

---


<figure class="krazy">
<div class="input">
```liquid
{% include ex1/input.md %}
```
</div>
{% include code/output.html output=include.output %}
<div class="browser">
{{ include.output }}
</div>
</figure>


## THIS IS A TEST

{% capture yaml %}
title: {{ page.ex.title }}
subtitle: {{ page.ex.subtitle }}
author: {{ page.ex.author }}
publisher:{% for item in page.ex.publisher %}
  {{ item[0] }}: {{ item[1] }}{% endfor %}
{% endcapture %}

{% capture input %}{% raw %}
<h1>{{ page.title }}</h1>
<h2>{{ page.subtitle }}</h2>
<p>by {{ page.author }}</p>
<p>Published by <a href="{{ page.publisher.url }}">{{ page.publisher.name }}</a></p>
{% endraw %}{% endcapture %}

{% capture output %}
<h1>{{ page.ex.title }}</h1>
<h2>{{ page.ex.subtitle }}</h2>
<p>by {{ page.ex.author }}</p>
<p>Published by <a href="{{ page.ex.publisher.url }}">{{ page.ex.publisher.name }}</a></p>
{% endcapture %}

{% include example.html yaml=yaml input=input output=output %}







## END TEST!!!