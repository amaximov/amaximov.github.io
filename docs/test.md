{% assign files = site.static_files | where_exp: "item", "item.path contains '/files/'" | sort: 'modified_time' | reverse %}
<table>
{% for f in files %}
  <tr>
    <td><dd>{{ f.modified_time }}</dd></td>
    <td><a href="{{ f.path }}">{{ f.path }})</a></td>
  </tr>
{% endfor %}
</table>
