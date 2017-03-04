---
title: Structured Content
permalink: /structured-content/
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

"YAML[^yaml] Frontmatter" is the name for structured content placed at the top of a document, which can be accessed within that document, as well as by its layout documents.

Here is a very basic example:

```yaml
---
title: {{ page.ex.title }}
---

This is the content of the document.
```

Note two things:

* The frontmatter is separated out at the top of the file and delineated by the `---` above and below it. These markers need to be present and must be at the top of the file.
* The frontmatter is stripped out of the rendered page. It is best to think of this block as metadata for the page, which can, if desired, be placed onto the rendered page itself.


Basic Content
-------------

In its simplest use, YAML gives us a way to store simple pieces of text content, like so:

```yaml
---
title: {{ page.ex.title }}
subtitle: {{ page.ex.subtitle }}
author: {{ page.ex.author }}
---
```

[^yaml]: [YAML](http://www.yaml.org), short for "YAML Ain't Markup Language" is a simple and very human-readable syntax for structuring content/data. It's really the heart of what makes Jekyll such a useful tool.


If you've got data in the frontmatter of a document. Odds are pretty good that you're going to want to use it in the document itself, like so:

```liquid
---
title: {{ page.ex.title }}
---

<h1>{% raw %}{{ page.title }}{% endraw %}</h1>
```

Anything that is in the page's frontmatter is accessible in the same way:

```liquid
---
title: {{ page.ex.title }}
subtitle: {{ page.ex.subtitle }}
author: {{ page.ex.author }}
---

<h1>{% raw %}{{ page.title }}{% endraw %}</h1>
<h2>{% raw %}{{ page.subtitle }}{% endraw %}</h2>
<p>{% raw %}{{ page.author }}{% endraw %}</p>
```

That will output:

```html
<h1>{{ page.ex.title }}</h1>
<h2>{{ page.ex.subtitle }}</h2>
<p>by {{ page.ex.author }}</p>
```


Nested Content
--------------

We can also easily access nested information:

```liquid
---
title: {{ page.ex.title }}
subtitle: {{ page.ex.subtitle }}
author: {{ page.ex.author }}
publisher:{% for item in page.ex.publisher %}
  {{ item[0] }}: {{ item[1] }}{% endfor %}
---

<h1>{% raw %}{{ page.title }}{% endraw %}</h1>
<h2>{% raw %}{{ page.subtitle }}{% endraw %}</h2>
<p>{% raw %}by {{ page.author }}{% endraw %}</p>
<p>Published by <a href="{% raw %}{{ page.publisher.url }}{% endraw %}">{% raw %}{{ page.publisher.name }}{% endraw %}</a></p>
```

That will output:

```html
<h1>{{ page.ex.title }}</h1>
<h2>{{ page.ex.subtitle }}</h2>
<p>by {{ page.ex.author }}</p>
<p>Published by <a href="{{ page.ex.publisher.url }}">{{ page.ex.publisher.name }}</a></p>
```




Looping Through Content
-----------------------

```liquid
---
title: {{ page.ex.title }}
subtitle: {{ page.ex.subtitle }}
author: {{ page.ex.author }}
publisher:{% for item in page.ex.publisher %}
  {{ item[0] }}: {{ item[1] }}{% endfor %}
tags:{% for tag in page.ex.tags %}
  - {{ tag }}{% endfor %}
---

<h1>{% raw %}{{ page.title }}{% endraw %}</h1>
<h2>{% raw %}{{ page.subtitle }}{% endraw %}</h2>
<p>{% raw %}{{ page.author }}{% endraw %}</p>
<p>Filed under: {% raw %}{{ page.tags | join:', ' }}{% endraw %}</p>
```

That will output:

```html
<h1>{{ page.ex.title }}</h1>
<h2>{{ page.ex.subtitle }}</h2>
<p>{{ page.ex.author }}</p>
<p>Filed under: {{ page.ex.tags | join:', ' }}</p>
```
