{% assign files = site.static_files | where: "path", "files" %}
{% for f in files %}
  {{ f.path }}
{% endfor %}
