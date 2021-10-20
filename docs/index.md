{% for post in site.posts %}
* `{{ post.date | date_to_string }}` [{{ post.title | truncate: 52 }}]({{ post.url }})
{% endfor %}
