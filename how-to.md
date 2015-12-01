---
layout: flex
title: How-to
permalink: /how-to/
weight: 2
redirect_from: /videos/
description: All video tutorials and articles for Sketch and Magic Mirror Plugin. Be more productive with these tips and tricks!
---

<h1>Videos</h1>
<section class="my2 py2 clearfix" style='background-color:transparent'>
<div class="flex-wrap">
{% for video in site.data.videos %}

{% if video.link %}
{% assign link = video.link %}
{% else %}
{% capture link %}https://youtube.com/watch?v={{ video.yt_id }}&list=PLXM9Shjg7jenAH19HHSWYPJ4EtB4RNDc1{% endcapture %}
{% endif %}

<div class="sm-col sm-col-4 showcase">
	<img src="/images/video-placeholder.png" style="background-image:url('http://img.youtube.com/vi/{{ video.yt_id }}/0.jpg');background-position: center; background-size: 100% auto;
	    background-repeat: no-repeat;"/>
	<a href="{{ link }}" identifier="{{ video.identifier }}" class="overlay">
		<div class="overlay flex flex-end">
			<div class="flex flex-end m2">
				<div class="flex-none mr2">
					<img src="{{ video.avatar }}" class="avatar">
				</div>
				<div class="flex flex-column">
					<div class="flex-auto liner videotitle">{{ video.title }}</div>
					<div class="flex-auto author">- {{ video.author }}</div>
				</div>
			</div>
		</div>
	</a>
</div>
{% endfor %}
</div>

</section>
<br />
<h1>Articles</h1>
<section class="my2 py2 clearfix">
<div class="flex-wrap">
{% for article in site.data.articles %}
<div class="sm-col sm-col-4 showcase fixing">
	<img src="/images/showcase-placeholder.png" style="background-image:url('{{ article.featured }}');background-position: center; background-size: 100% auto;
    background-repeat: no-repeat; background-color: black;"/>
	<a href="{{ article.link }}" identifier="{{ article.identifier }}" class="overlay">
		<div class="overlay flex flex-end">
			<div class="flex flex-end m2">
				<div class="flex-none mr2">
					<img src="{{ article.avatar }}" class="avatar">
				</div>
				<div class="flex flex-column">
					<div class="flex-auto liner videotitle">{{ article.title }}</div>
					<div class="flex-auto author">- {{ article.author }}</div>
				</div>
			</div>
		</div>
	</a>
</div>
{% endfor %}
</div>

</section>
