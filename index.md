---
layout: page
title: BioDeepTime
subtitle: Assemblage time series across scales
show_sidebar: true
hero_image: "/images/bg/ocean.jpg"
---

<h1>BioDeepTime (v1.0)</h1>
<div class="columns">
  <div class="column">
<p style="text-align:justify">The presence of humanity on the planet has been having a profound impact on life, which needs to be assessed in a broad temporal context. The BioDeepTime project aims to unravel how processes that change biological assemblages scale across historical and geological timescales. To achieve our goal, we have compiled biogeographic records of both modern and fossil organisms from various sources that include assemblage time series information over time.</p> 
	<div class="buttons">
		<a class="button is-info" href="{{site.url}}{{site.basurl}}/database/access/">Access database</a>
		<a class="button is-primary" style="text-decoration:line-through">Database paper</a>
	</div>
  </div>
  <div class="column">
{% for row in site.data.summary %}
  <table class="summary">
	<tr  style="background-color: #fafafa">
		<th>Records:</th>
		<td>{{row.records | format_number: "N"}}</td>
	</tr>
	<tr>
		<th>Sources:</th>
		<td>{{row.db | format_number: "N"}}</td>
	</tr>
	<tr  style="background-color: #fafafa">
		<th>Time Series:</th>
		<td>{{row.series}}</td>
	</tr>
	<tr>
		<th>Samples:</th>
		<td>{{row.samples}}</td>
	</tr>
	<tr  style="background-color: #fafafa">
		<th>Taxon entries:</th>
		<td>{{row.taxa}}</td>
	</tr>
	<tr>
		<th>Oldest sample:</th>
		<td>{{row.from_ma}} Ma</td>
	</tr>
	<tr style="background-color: #fafafa">
		<th>Youngest sample:</th>
		<td>{{row.to_year}}</td>
	</tr>
  </table>
{% endfor %}
<br>
  </div>

</div>

<div class="columns">
	<div class="column">
		<h5 style="text-align:center">Modern records</h5>
{% include image-modal.html ratio="is-16by9" link="/images/bdt/gridModernRobin.png" alt="Example image" large_link='/images/bdt/gridModernRobin.png' %} 
	</div>
	<div class="column">
		<h5  style="text-align:center">Fossil records</h5>
{% include image-modal.html ratio="is-16by9" link="/images/bdt/gridFossilRobin.png" alt="Example image" large_link='/images/bdt/gridFossilRobin.png' %} 
	</div>
</div>
