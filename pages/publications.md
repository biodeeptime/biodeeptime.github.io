---
layout: page
title: Publications
permalink: /publications/
hero_image: "/../images/bg/ocean.jpg"
---

<table>
{% for paper in site.data.publications %}
<tr>
  <td> {{paper.number}}. </td>
  <td style="padding-left: 22px ; text-indent: -22px ;text-align:left">{{paper.text}}</td>
</tr>
{% endfor %}
</table>
