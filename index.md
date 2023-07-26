---
layout: page
title: BioDeepTime
subtitle: Assemblage time series across scales
show_sidebar: true
hero_image: "/images/bg/ocean.jpg"
---

<h1>BioDeepTime</h1>
<div class="columns">
  <div class="column">
<p style="text-align:justify">Humans have profoundly modified ecosystems and planetary processes across the globe.  Yet it remains difficult to quantify humanity's impact because doing so requires disentangling human and natural drivers of change.
The BioDeepTime Project aims to unravel the drivers of biodiversity dynamics by leveraging the combined power of ecological and fossil timeseries and by advancing broadly integrative theories of biodiversity change and scaling in time.</p> 
	<div class="buttons">
		<a class="button is-info" href="{{site.url}}{{site.basurl}}/database/access/">Access database</a>
		<a class="button is-primary" href="https://doi.org/10.1111/geb.13735">Database paper</a>
	</div>
  </div>
  <div class="column">
{% for row in site.data.summary %}
  <table class="summary">
	<tr  style="background-color: #fafafa">
		<th>Records:</th>
		<td>{{row.records | intcomma: ',' }}</td>
	</tr>
	<tr>
		<th>References: </th>
		<td>{{row.refs | intcomma: ',' }}</td>
	</tr>
	<tr  style="background-color: #fafafa">
		<th>Source databases: </th>
		<td>{{row.db}}</td>
	</tr>
	<tr>
		<th>Time Series:</th>
		<td>{{row.series | intcomma: ',' }}</td>
	</tr>
	<tr  style="background-color: #fafafa">
		<th>Samples:</th>
		<td>{{row.samples | intcomma: ',' }}</td>
	</tr>
	<tr>
		<th>Taxon entries:</th>
		<td>{{row.taxa  | intcomma: ',' }}</td>
	</tr>
	<tr style="background-color: #fafafa">
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
