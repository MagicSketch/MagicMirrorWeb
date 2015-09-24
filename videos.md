---
layout: flex
title: Videos
permalink: /videos/
weight: 1
---

<h1>Videos</h1>
<section class="my2 py2 border-top clearfix" style='background-color:transparent'>
<div class="flex-wrap">
{% for video in site.data.videos %}
<div class="sm-col sm-col-4 showcase">
	<img src="http://img.youtube.com/vi/{{ video.yt_id }}/0.jpg" class='fixing'/>
	<a href="https://youtube.com/watch?v={{ video.yt_id }}&list=PLXM9Shjg7jenAH19HHSWYPJ4EtB4RNDc1" identifier="{{ video.title }}" class="overlay">
		<img src="http://magicmirror.design/images/showcase-placeholder.png" />
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
<section class="my2 py2 border-top clearfix" style='background-color:black'>
<div class="flex-wrap">
{% for article in site.data.articles %}
<div class="sm-col sm-col-4 showcase fixing">
	<img src="{{ article.featured }}" class='fixing' />
	<a href="{{ article.link }}" identifier="{{ article.author }}" class="overlay">
		<img src="http://magicmirror.design/images/showcase-placeholder.png" />
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
