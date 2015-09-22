---
layout: flex
title: Videos
permalink: /videos/
weight: 1
---

<h1 stlye='text-align:center;'>Videos</h1>
<div class="flex flex-wrap p1 templates">
{% for video in site.data.videos %}
      <div class="lg lg-col-4 md-col-4 sm-col-2">
        <a href="https://youtube.com/watch?v={{ video.yt_id }}&list=PLXM9Shjg7jenAH19HHSWYPJ4EtB4RNDc1">
        <img src="http://img.youtube.com/vi/{{ video.yt_id }}/0.jpg" alt="{{ video.title }}"/>
        </a>
        <p><a href="https://youtube.com/watch?v={{ video.yt_id }}&list=PLXM9Shjg7jenAH19HHSWYPJ4EtB4RNDc1">{{ video.title }}</a></p><p class="author"><img src="https://avatars.githubusercontent.com/{{ video.github }}" class="avatar"/><a href="https://github.com/{{ video.github }}" class="name">{{ video.github }}</a></p>
        </div>
{% endfor %}
</div>
<h1 style='text-align:center;'>Articles</h1>
<div class="flex flex-wrap p1 templates">
{% for article in site.data.articles %}
<div class='lg lg-col-3 md-col-3 sm-col-2 px3'>
<img src="{{ article.featured}}" alt="{{ article.title }}"  />
<p><a href="{{ article.link }}" alt="{{ article.title }}">{{ article.title }} </a></p>
<p class="author"><img src="https://avatars.githubusercontent.com/{{ article.github }}" class="avatar"/><a href="https://github.com/{{ article.github }}" class="name">{{ article.github }}</a></p>
</div>
{% endfor %}
</div>

<div class="center wrapper mt4" markdown="1">
Magic Mirror Templates is still in beta. If you want to help or want to have your own templates show up please read the <a href="/template-guideline">templates contribution guideline</a> :)
</div>
