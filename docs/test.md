{% assign files = site.static_files | where_exp: "item", "item.path contains '/files/'" | sort: 'modified_time' | reverse %}
<table>
{% for f in files %}
  <tr>
    <td>`{{ f.modified_time }}`</td>
    <td>`[{{ f.path }}]({{ f.path }})`</td>
  </tr>
{% endfor %}
</table>
