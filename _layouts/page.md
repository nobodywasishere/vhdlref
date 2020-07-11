---
layout: default
---

<title>{{ page.title }}</title>

<span>
    <h2 style="align-items: center;">
        <a href={{ "index.html" | proper_url }} class="text-norm">
            <img src="{{ 'assets/icon.svg' | baseurl }}" alt="logo" style="vertical-align:middle; margin: auto 2px 5px auto; width: 50px; height: 50px" />
            {{ site.name }}
        </a>
    </h2>
</span>

<hr>

<h1>{{ page.title }}</h1>

{{ content }}

<br>
<hr>
