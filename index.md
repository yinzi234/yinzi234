---
layout: index
title: 阿虚的二次元空间
---

<center><h1 id="section"><strong>二次元空间</strong></h1></center>


<center><h3 id="section"><a href="http://dota.weakyon.com">弱虚同样弱爆的DotaTeamPicker</a></h3></center>

<center><div class="logo-image"><img src="log.jpg" alt="阿虚logo" /></div></center>

<table id="list">
	{% for post in site.posts %}
 	 <tr>
    	<td class="list-title"><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></td>
    	<td class="list-span"><p><span></span></p></td>
    	<td class="list-date"><p>{{ post.date | date_to_string }}</p></td>
 	 </tr>
  	{% endfor %}
</table>