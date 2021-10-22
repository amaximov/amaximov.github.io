{% assign files = site.static_files %}
{% for f in files %}
  {{ f.path }}
{% endfor %}
