---
layout: flex
title: Templates
permalink: /templates/
weight: 1
banner: true
share:
  title: Sketch Perspective Mockups and Templates
  description: Checkout the new Magic Mirror Templates for iPhone 6S
---

# Templates

<div class="flex flex-wrap p1 templates">

  {% for item in site.templates %}

    {% if item.hidden %}

    {% else %}

    {% if item.price %}
    <div class="flex sm-col-6 md-col-4 border-box p1 template price" style="order:{{ item.weight }}">
    {% elsif item.members %}
    <div class="flex sm-col-6 md-col-4 border-box p1 template members" style="order:{{ item.weight }}">
    {% else %}
    <div class="flex sm-col-6 md-col-4 border-box p1 template free" style="order:{{ item.weight }}">
    {% endif %}


      <div class="p1 border rounded">
        <a href="{{ item.url }}">
          <img src="/images/templates/{{ item.image }}" height="auto" />
        </a>
        <div class="mx-auto">
          <span class="flex">
  	        <span class="flex-auto">
  		        <h4 class="title mt1 mb1 bold">{{ item.title }}</h4>
  		        <i class="meta m0">{{ item.description }}</i>
              {% assign author = site.data.authors[item.author] %}
              <p class="author"><a href="{{ author.link }}" identifier="{{ item.author }}" class="name"><img src="{{ author.avatar }}" class="avatar"/> {{ item.author }}</a></p>
  		      </span>

        <!--
          {% if item.members %}
          <a href="{{ item.download_link }}" class="members-btn border-box center btn btn-outline gray flex-none" width="100px" max-width="100px">MEMBERS</a>
          {% else %}
          <a href="{{ item.download_link }}" class="border-box center btn btn-outline green flex-none" width="100px" max-width="100px">FREE</a>
          {% endif %}
        -->

            <div class="flex-none p1 right-align">

              <p class="status">
              {% if item.price %}
                ${{ item.price }}
              {% elsif item.members %}
                MEMBERS
              {% else %}
                FREE
              {% endif %}
              </p>
            </div>
          </span>
    		</div>
      </div>
    </div>
    {% endif %}
  {% endfor %}


</div>
<div class="center wrapper mt4" markdown="1">

Magic Mirror Templates is still in beta. If you want to help or want to have your own templates show up please read the <a href="/template-guideline">templates contribution guideline</a> :)

</div>
