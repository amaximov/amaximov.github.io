{% assign files = site.static_files | where: "/files/" %}
{% for f in files %}
  {{ f.path }}
{% endfor %}
