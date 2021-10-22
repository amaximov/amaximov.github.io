| timestamp      | path |
{% assign files = site.static_files | where_exp: "item", "item.path contains '/files/'" | sort: 'modified_time' | reverse %}
{% for f in files %}
| ----------- | ----------- |
| {{ f.modified_time }} | [{{ f.path }}]({{ f.path }}) |  
{% endfor %}
