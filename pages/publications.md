---
layout: page
title: Publications
permalink: /publications/
---

<table>
{% for paper in site.data.publications %}
<tr>
  <td> {{paper.number}}. </td>
  <td style="padding-left: 22px ; text-indent: -22px ;"> {{paper.text}}</td>
</tr>
{% endfor %}
</table>
