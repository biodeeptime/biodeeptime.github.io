---
layout: page
title: BioDeepTime
subtitle: Assemblage time series across scales
hero_link: /database/access/
hero_link_text: Download
show_sidebar: true
---

<div class="columns">
  <div class="column">
	<h1>Welcome</h1>
<p>The presence of humanity on the planet has been having a profound impact on life, which needs to be assessed in a broad temporal context. The BioDeepTime project aims to unravel how processes that change biological assemblages scale across historical and geological timescales.To achieve our goal, we have compiled biogeographic records of both modern and fossil organisms from various sources that include assemblage time series information over time.</p> 
  </div>
  <div class="column">
{% for row in site.data.summary %}
  <table class="summary">
	<tr>
		<th>Records:</th>
		<td>{{row.records | format_number: "N"}}</td>
	</tr>
	<tr  style="background-color: #fafafa">
		<th>Sources:</th>
		<td>{{row.db | format_number: "N"}}</td>
	</tr>
	<tr>
		<th>Time Series:</th>
		<td>{{row.series}}</td>
	</tr>
	<tr  style="background-color: #fafafa">
		<th>Samples:</th>
		<td>{{row.samples}}</td>
	</tr>
	<tr>
		<th>Taxon entries:</th>
		<td>{{row.taxa}}</td>
	</tr>
	<tr  style="background-color: #fafafa">
		<th>Oldest sample:</th>
		<td>{{row.from_ma}} Ma</td>
	</tr>
	<tr>
		<th>Youngest sample:</th>
		<td>{{row.to_year}}</td>
	</tr>
  </table>
{% endfor %}
<br>
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
  </div>

</div>

- repeating basic links - most importantly: [ACCESS]({{site.url}}{{site.baseurl}}/database/access/). 
