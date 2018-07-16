---
layout: default
---

# Articles

<style type="text/css">
	a{text-decoration: none; padding: 10PX; color:#000;}
	a:hover{ color:silver;}
	li{list-style:none}
</style>

{% for category in site.categories %}
<h2>{{ category | first }}</h2>
<ul class="arc-list">
    {% for post in category.last %}
        <li>{{ post.date | date:"%m/%d/%Y"}}<a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>
{% endfor %}