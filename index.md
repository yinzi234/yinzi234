---
layout: index
title: 阿虚的二次元空间
---

<center><h1 id="section"><strong>阿虚的二次元空间</strong></h1></center>

<center><h3 id="section">weakyon / 弱爆的阿虚</h3></center>

<center><h3 id="section"><a href="http://dota.weakyon.com">弱虚同样弱爆的DotaTeamPicker</a></h3></center>

<center><p><img src="log.jpg" alt="阿虚logo" /></p></center>

<ul>
　　{% for post in site.posts %}
	<center><li>{{ post.date | date_to_string }} <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li></center>
　　{% endfor %}
</ul>

