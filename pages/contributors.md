---
layout: page
title: Contributing databases
permalink: database/contributing/
hero_image: "/../../images/bg/ocean.jpg"
---

BioDeepTime compiles assemblage time series data from a number of databases - all of which are publicly available. 

{% for db in site.data.databases %}

<div class="box">
  <div class="columns is-vcentered">
	<div class="column is-2">
	<a  href="{{db['link']}}">
	<img src="{{site.baseurl}}{{site.url}}/images/logos/{{db['logo']}}" width="200" alt="{{db['name']}} logo" style="margin-left:20px;margin-right:20px">
	</a>
	</div>
	<div class="column is-1">
	</div>
	<div class="column">
	<a  href="{{db['link']}}">
	<h2>{{db['name']}}</h2>
	</a>
	<p> {{db['text']}}</p>
	<p> <strong>Representative(s): </strong> 
	{% assign i = 0 %}
	{% for person in site.data.people %}
		{% if db['representatives'] contains person.ref %}
		  {% if i == 0 %}	
			<a href="{{site.url}}{{site.baseurl}}/team/people/#{{ person.first | append: " " | append: person.last | slugify }}">{{person.first}} {{person.last}}</a>
			{% endif %}
			{% if i != 0 %}	
			- <a href="{{site.url}}{{site.baseurl}}/team/people/#{{ person.first | append: " " | append: person.last | slugify }}">{{person.first}} {{person.last}}</a>
			{% endif %}
		  {% assign i = i | plus:1 %}
		{% endif %}
	{% endfor %}
	</p>
	</div>
  </div>
</div>


{% endfor %}


## Direct uploads 

BioDeepTime also aggregates data from time series that are not part of any of the formal entities above. These are categorized as **Direct uploads**.
