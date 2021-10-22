{% assign files = site.static_files | where_exp: "item", "item.path contains '/files/'" | sort: 'path' | reverse %}
<table>
{% for f in files %}
  <tr>
    <td><a href="{{ f.path }}">{{ f.path }}</a></td>
  </tr>
{% endfor %}
</table>
