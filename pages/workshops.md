---
layout: page
title: Workshops
permalink: team/workshops/
---

{% assign wsord = site.data.workshops | sort: 'year' | reverse %}
{% for ws in wsord %}
<section>
<div class="box">
<div class="columns">
	<div class="column is-three-fifths">
		<h2> {{ws.year}} - <em>{{ws.name}}</em></h2>
		<hr>
		<div class="columns">
			<div class="column is-two-thirds">
			<table>
				<tr> 
				<th style="text-align: left">Date: </th>
				<td>{{ws.date}} </td>
				</tr>
				<tr> 
				<th style="text-align: left">Location: </th>
				<td>{{ws.where}} </td>
				</tr>
				<tr> 
				<th style="text-align: left">Funding: </th>
				{%assign lastFunder = ''%}
				{%for funds in site.data.funders %}
				{% if ws.funder contains funds.ref %}
				<td><a href="{{site.url}}{{site.baseurl}}/team/funding/#{{funds.name | slugify}}">{{funds.name}}</a></td>
				{%assign lastFunder = funds.name%}
				{% endif %}
				{% endfor %}
				</tr>
			</table>
			</div>
			<div class="column is-one-third">
			<a href="{{site.url}}{{site.baseurl}}/team/funding/#{{lastFunder | slugify}}"><img src="{{site.url}}{{site.baseurl}}/{{ws.logo}}" width="150px"></a>
			</div>
		</div>
		<br>
		<h4>Participants (in-person)</h4>
		{% assign everyone = site.data.people | sort: 'last'%}
		{% assign groupsize = ws.onsite | size %}
		{% assign i = 1 %}
		{% for person in everyone %}
			{% if ws.onsite contains person.ref%}
		<a href="{{site.url}}{{site.baseurl}}/team/people/#{{ person.first | append: " " | append: person.last | slugify }}">{{person.first}} {{person.last}}</a> 
			{% unless groupsize == i %} | {% endunless %}
			{% assign i = i | plus:1 %}
			{% endif %}
		{% endfor %}
	</div>
	<div class="column is-two-fifth">
		<img src="{{site.url}}{{site.baseurl}}/{{ws.groupPhoto}}">
	</div>
</div>
</div>
</section>
<br>
{% endfor %}
