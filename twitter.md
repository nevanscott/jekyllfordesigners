---
title: Twitter
scss: |
  $brand: hsl(180, 15%, 95%);
  $sans: 'Whitney SSm A', 'Whitney SSm B', -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue", Avenir, Noto, sans-serif;
  article.tweet {
    background: $brand;
    border: 2px solid darken($brand, 30%);
    border-radius: .25em;
    padding: 1.5em;
    h1 {
      border: none;
      font-size: 1em;
    }
    p {
      margin: 1em 0 0;
    }
  }
  .markup [title] {
    outline: 1px solid red;
    position: relative;
    z-index: 1;
    &:after {
      background: red;
      border-radius: 0 0 0 3px;
      color: white;
      content: attr(title);
      font-family: $sans;
      font-size: .5em;
      font-weight: bold;
      padding: .25em .5em .4em;
      position: absolute;
      right: 0;
      top: 0;
      z-index: 2;
    }
  }
tweets:
  -
    username: Nevan Scott
    message: This is a statement that I just made.
  -
    username: Roxane Gay
    message: WELCOME TO JURASSIC PARK
---

Have a look at the following:

<figure>
  <article class="tweet" title="Tweet">
    <h1 title="User Name">Nevan Scott</h1>
    <p title="Message">This is a statement that I just made.</p>
  </article>
</figure>

Let's take a closer look at the content elements in play here:

<figure class="markup">
  <article class="tweet" title="Tweet">
    <h1 title="User Name">Nevan Scott</h1>
    <p title="Message">This is a statement that I just made.</p>
  </article>
</figure>

With this structure in mind, I might develop a basic model for tweets that I could use in my YAML frontmatter or in a data YAML file, like so:

```yaml
tweets:
  -
    username: Nevan Scott
    message: This is a statement that I just made.
  -
    username: Roxane Gay
    message: WELCOME TO JURASSIC PARK
```

Let's say this is the HTML that I ultimately what to hit (for each tweet):

```html
<article class="tweet">
  <h1>USER NAME HERE</h1>
  <p>MESSAGE HERE</p>
</article>
```

We can stitch the two together like so:

```liquid
---
tweets:
  -
    username: Nevan Scott
    message: This is a statement that I just made.
  -
    username: Roxane Gay
    message: WELCOME TO JURASSIC PARK
---

{% raw %}{% for tweet in page.tweets %}{% endraw %}
<article class="tweet">
  <h1>{% raw %}{{ tweet.username }}{% endraw %}</h1>
  <p>{% raw %}{{ tweet.message }}{% endraw %}</p>
</article>
{% raw %}{% endfor %}{% endraw %}
```

Then we can have some fun playing around with different options for how to present the information:

{% capture scss %}
$sans: 'Whitney SSm A', 'Whitney SSm B', -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue", Avenir, Noto, sans-serif;
.twitter_examples {
  height: 60vh;
}
.twitter_example {
  background: white;
  box-shadow: 0 0 .25em rgba(0,0,0,.5);
  font-size: smaller;
  height: 60vh;
  margin: 0 -6.25% 0 0;
  overflow: hidden;
  padding: .5em;
  position: relative;
  width: 25%;
  float: left;
  box-sizing: border-box;
  .tweet {
    margin-bottom: .5em;
  }
  h1, p {
    font-family: $sans;
  }
}
.twitter_example_2, .twitter_example_4 { top: -4px; }
.twitter_example_3 { top: -8px; }
.twitter_example_1 {
  .tweet {
    h1 {
      margin: 0;
    }
    p {
      margin: 0;
    }
  }
}
.twitter_example_2 {
  .tweet {
    background: hsl(180, 15%, 45%);
    border: none;
    color: white;
    h1 {
      margin: 0;
    }
    p {
      margin: 0;
    }
  }
}
.twitter_example_3 {
  padding: 0;
  .tweet {
    background: transparent;
    border: none;
    border-bottom: 1px solid #CCC;
    border-radius: 0;
    color: black;
    h1 {
      margin: 0;
    }
    p {
      margin: 0;
    }
  }
}
.twitter_example_4 {
  padding: 0;
  .tweet {
    background: transparent;
    border: none;
    border-bottom: 1px solid #CCC;
    border-radius: 0;
    color: black;
    margin: 0;
    padding: .75em 1em;
    h1 {
      color: hsl(180, 15%, 40%);
      margin: 0;
    }
    p {
      margin: 0;
    }
  }
}
.twitter_example_5 {
  padding: 0;
  .tweet {
    background: transparent;
    background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#FFF), to(hsl(180, 15%, 95%)));
    background: -webkit-linear-gradient(top, #FFF, hsl(180, 15%, 95%));
    background: -moz-linear-gradient(top, #FFF, hsl(180, 15%, 95%));
    background: -ms-linear-gradient(top, #FFF, hsl(180, 15%, 95%));
    background: -o-linear-gradient(top, #FFF, hsl(180, 15%, 95%));
    border: none;
    border-bottom: 1px solid hsl(180, 15%, 80%);
    border-radius: 0;
    color: black;
    margin: 0;
    padding: .75em 1em;
    h1 {
      color: hsl(180, 15%, 40%);
      margin: 0;
    }
    p {
      margin: 0;
    }
  }
}
{% endcapture %}
<style>{{ scss | scssify }}</style>

<figure class="full twitter_examples">
{% for i in (1..5) %}
  <figure class="twitter_example twitter_example_{{i}}">
    {% for i in (1..5) %}
    {% for tweet in page.tweets %}
    <article class="tweet">
      <h1>{{ tweet.username }}</h1>
      <p>{{ tweet.message }}</p>
    </article>
    {% endfor %}
    {% endfor %}
  </figure>
{% endfor %}
</figure>

Isn't that fun?