{% assign files = site.static_files | where_exp: "item", "item.path contains '/files/'" | sort: 'path' | reverse %}
<table>
{% for f in files %}
  <tr>
    <td>{{ f.modified_time | date: "%Y-%m-%d %H:%M" }}</td>
    <td><a href="{{ f.path }}">{{ f.path }}</a></td>
  </tr>
{% endfor %}
</table>
