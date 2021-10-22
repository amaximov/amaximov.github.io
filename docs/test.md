{% assign files = site.static_files | where_exp: "item", "item.path contains '/files/'" %}
{% for f in files %}
  {{ f.path }}
  {{ f | inspect }}
{% endfor %}
