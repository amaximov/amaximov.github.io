{% assign files = site.static_files | where_exp: "item", "item.path contains '/files/'" | sort: 'modified_time' | reverse %}
| timestamp   | path        |
| :---------- | :---------- |
{% for f in files %}
| {{ f.modified_time }} | [{{ f.path }}]({{ f.path }}) |  
{% endfor %}
