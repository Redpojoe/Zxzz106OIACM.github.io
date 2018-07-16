---
layout: default
---

# Articles

{% for category in site.categories %}
<h2>{{ category | first }}</h2>
<ul class="arc-list">
    {% for post in category.last %}
        <li><font size="4">{{ post.date | date:"%d/%m/%Y"}}<a href="{{ post.url }}">{{ post.title }}</a></font></li>
    {% endfor %}
</ul>
{% endfor %}