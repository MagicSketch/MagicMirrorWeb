---
layout: flex
title: Learn
weight: 2
permalink: /learn/
redirect_from: /how-to/
---

# Learn

<div class="flex flex-wrap p1">

  {% for item in site.learn %}
    <div class="flex sm-col-6 md-col-4 border-box p1 template price" style="order:{{ item.weight }}">

      <div class="">
        <a href="{{ item.url }}">
          <img src="{{ item.image }}" height="auto" class="border" />
        </a>
        <div class="mx-auto">
          <span class="flex">
  	        <span class="flex-auto">
  		        <h4 class="title mt1 mb1 bold">{{ item.title }}</h4>
  		        <i class="meta m0">{{ item.description }}</i>
  		      </span>

          </span>
    		</div>
      </div>
    </div>
  {% endfor %}

</div>


# Advanced Techniques


<div class="flex flex-wrap p1">

  {% for item in site.data.advanced %}
    <div class="flex sm-col-6 md-col-4 border-box p1 template price" style="order:{{ item.weight }}">

      <div class="border p1">
        <a href="{{ item.link }}">
          {% if item.yt_id %}
            <img src="/images/showcase-placeholder.png" style="background-image:url('http://img.youtube.com/vi/{{ item.yt_id }}/0.jpg');background-position: center; background-size: 100% auto;
      background-repeat: no-repeat;"/>
          {% else %}
          <img src="{{ item.featured }}" height="auto" class="border" />
          {% endif %}
        </a>
        <div class="mx-auto">
          <span class="flex">
            <span class="flex-auto">
              <h4 class="title mt1 mb1 bold">{{ item.title }}</h4>
              <i class="meta m0">{{ item.description }}</i>
            </span>

          </span>
        </div>
      </div>
    </div>
  {% endfor %}

</div>