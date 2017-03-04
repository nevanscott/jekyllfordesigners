---
title: Getting Started
permalink: /getting-started/
---

Assuming you're running a relatively recent version of Mac OS X, you should be able to get up and running with just the following command in the Terminal:

```bash
$ gem install jekyll
```

From here, we're going to start from scratch[^quickstart] making a new little Jekyll website. In it's simplest form, Jekyll will just take the files that you write and copy the into your generated site.

1. Make a directory for your Jekyll project, and start the Jekyll server.
  
    ```bash
    ~ $ mkdir mysite
    ~ $ cd mysite
    ~/mysite $ jekyll serve
    ```
    
    You should see something like the following, which means everything is working:
    
    ```bash
    Configuration file: none
                Source: /Users/nevan/mysite
           Destination: /Users/nevan/mysite/_site
          Generating... 
                        done.
     Auto-regeneration: enabled for '/Users/nevan/mysite'
    Configuration file: none
        Server address: http://127.0.0.1:4000/
      Server running... press ctrl-c to stop.
    ```

2. Let's add a simple file. Make a file in the `mysite` folder called `index.html` and put in the following:
    
    ```html
    <h1>Hello World!</h1>
    ```

3. Make sure the server is still running in the Terminal, and then browse to the address listed there -- most likely `http://127.0.0.1:4000/`, as above.
    
    Not very interesting, I admit, but it's a start!

[^quickstart]: Jekyll's documentation includes a [Quick-start guide](http://jekyllrb.com/docs/quickstart/), which includes a number of built-in templates and styles, all of which are geared primarily toward using Jekyll as a blog. For our purposes, I don't recommend starting this way as it simply gives you too much out of the box.