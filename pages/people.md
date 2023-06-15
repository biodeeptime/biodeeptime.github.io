---
layout: page
title: People
permalink: team/people/
---

# Project Coordination (PIs)

{% assign i = 0 %}
{% assign basic = site.data.people | where: 'special', 'pi' %}
{% assign basic = basic | sort: 'last' %}
{% for person in basic %}
{% assign i = i | plus:1 %}
{% assign something = i | modulo:2 %}
{% if something == 1 %}
<div class="columns is-vcentered">
{% endif %}

<div class="column">
	<div class="box">
	<div class="columns">
		<div class="column is-3">
		<a href="{{person.webpage}}"><img src="{{site.url}}{{site.baseurl}}/images/photos/{{person.image}}" style="border-radius:3%;border:1px solid #ddd"></a>
		</div>
		<div class="column">
		<h4 id="{{ person.first | append: " " | append: person.last | slugify }}"><a href="{{person.webpage}}">{{person.first}} {{person.last}}</a></h4>
		{{person.institute}}
		</div>
	</div>
	</div>
</div>

{% if something == 0 %}
</div>
{% endif %}
{% endfor %}

{% if something == 1 %}
<div class="column">
</div>
</div>
{% endif %}


# Database Development

{% assign i = 0 %}
{% assign basic = site.data.people | where: 'special', 'admin' %}
{% assign basic = basic | sort: 'last' %}
{% for person in basic %}
{% assign i = i | plus:1 %}
{% assign something = i | modulo:2 %}
{% if something == 1 %}
<div class="columns is-vcentered">
{% endif %}

<div class="column">
	<div class="box">
	<div class="columns">
		<div class="column is-3">
		<a href="{{person.webpage}}"><img src="{{site.url}}{{site.baseurl}}/images/photos/{{person.image}}" style="border-radius:3%;border:1px solid #ddd"></a>
		</div>
		<div class="column">
		<h4 id="{{ person.first | append: " " | append: person.last | slugify }}"><a href="{{person.webpage}}">{{person.first}} {{person.last}}</a></h4>
		{{person.institute}}
		</div>
	</div>
	</div>
</div>

{% if something == 0 %}
</div>
{% endif %}
{% endfor %}

{% if something == 1 %}
<div class="column">
</div>
</div>
{% endif %}

# Data contributors and Researchers

{% assign i = 0 %}
{% assign basic = site.data.people | where: 'special', null %}
{% assign basic = basic | sort: 'last' %}
{% for person in basic %}
{% assign i = i | plus:1 %}
{% assign something = i | modulo:2 %}
{% if something == 1 %}
<div class="columns is-vcentered">
{% endif %}

<div class="column">
	<div class="box">
	<div class="columns">
		<div class="column is-3">
		<a href="{{person.webpage}}"><img src="{{site.url}}{{site.baseurl}}/images/photos/{{person.image}}" style="border-radius:3%;border:1px solid #ddd"></a>
		</div>
		<div class="column">
		<h4 id="{{ person.first | append: " " | append: person.last | slugify }}"><a href="{{person.webpage}}">{{person.first}} {{person.last}}</a></h4>
		{{person.institute}}
		</div>
	</div>
	</div>
</div>

{% if something == 0 %}
</div>
{% endif %}
{% endfor %}

{% if something == 1 %}
<div class="column">
</div>
</div>
{% endif %}


- Open group.
- We are looking for collaborators.
- Please get in touch if you are would like to contribute data.
