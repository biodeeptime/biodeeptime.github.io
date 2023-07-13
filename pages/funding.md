---
layout: page
title: Funding history
permalink: team/funding/
---

{% for funder in site.data.funders %}
<section>
<a href="{{funder.webpage}}">
<div class="box">
<div class="columns" style="padding:15px">
	<div class="column-is-four-fifths">
		<h2> {{funder.name}}</h2>
			<hr>
		<p>{{funder.text}}</p>
		<p>{{funder.what}}</p>
		<img src="{{site.url}}{{site.baseurl}}/{{funder.funder_logo}}" style="max-height: 100px"> 
<p><em>{{funder.webpage}}</em></p>
	</div>
	<div class="column-is-one-fifth">
	<img src="{{site.url}}{{site.baseurl}}/{{funder.logo}}" style="max-width: 300px;margin:10px">
	</div>
</div>
</div>
</a>
<br>
{%endfor %}
