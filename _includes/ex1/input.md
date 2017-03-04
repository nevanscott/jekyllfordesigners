{% raw %}
<h1>{{ page.title }}</h1>
<h2>{{ page.subtitle }}</h2>
<p>by {{ page.author }}</p>
<p>Published by <a href="{{ page.publisher.url }}">{{ page.publisher.name }}</a></p>
{% endraw %}