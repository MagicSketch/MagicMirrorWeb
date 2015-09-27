---
layout: flex
title: Create Perspective Mockups in Sketch
subscribe: true
share:
  title: Magic Mirror Sketch 3 Plugin
  description: Create Perspective Mockups in Sketch
---

# Create Perspective Mockups in Sketch

<div class="wrapper">
<div class="flex flex-wrap mxn1 px1 py2 flex-center flex-start nav">
<div class="flex-auto border-box center btn orange">
	<a href="/beta/v1.3" identifier="Beta-2-v1.3" class="clearfix">v1.3 Beta 2 + Corner Radius</a>
	<sup class="red">UPDATED (05/09)</sup>
</div>
<!-- <div class="flex-auto center btn orange border-box none" id="get-license-free">
	<a href="/madewithmagicmirror" identifier="Get-License-Free" class="clearfix">Get a license for free</a>
	<sup class="gray">ENDED (20/8-24/8)</sup>
</div> -->
<div class="flex-auto center btn orange border-box" id="see-templates">
	<a href="/templates" identifier="See-Templates" class="clearfix">New iPhone6s Template</a>
	<sup class="red">UPDATED (11/9)</sup>
</div>
<!-- <div class="flex-auto center btn orange border-box" id="server-maintenance">
	<a href="/2015/09/21/server-maintenance.html" identifier="See-Templates" class="clearfix">Server Maintenance</a>
	<sup class="red">NEW (21/9)</sup>
</div> -->
<div class="flex-auto center">
	<a href="{{ site.downloadurl }}/latest" identifier="Free-Download" class="flex-auto border-box center btn btn-outline orange"><i class="fa fa-arrow-circle-o-down"></i>    Try</a>
	<a href="/purchase" identifier="Get-Full-License-Top" class="flex-auto border-box center btn btn-outline orange strong">Get License 50% off</a>
</div>
</div>
</div>



<div class="flex container">
	<div id="computer" class="flex-stretch col-12 m2">
		<img src="/images/computer.png" class="flow flex-stretch col-12"/>

		<div class="videodom flex">

		<!-- <div class="left"> </div> -->

		<div class="screen flex flex-center">

			<div class="videoWrapper">
			    <!-- Copy & Pasted from YouTube -->
			    <iframe width="560" height="349" src="https://www.youtube.com/embed/b2bwysoKWgU?rel=0&hd=1" frameborder="0" allowfullscreen></iframe>
			</div>

		</div>

		<!-- <div class="right"></div> -->


		</div>
	</div>
</div>

{% include showstart.html class="wrapper" %}

Magic Mirror for Sketch 3 is a Sketch Plugin that can create perspective transformed image from an artboard and apply to corresponding shape.

You can consider it a simple version of Photoshop’s [Embeded Smart Objects](https://helpx.adobe.com/photoshop/using/create-smart-objects.html) for Sketch.

{% include showhidden.html %}

## What's different?

Unlike [Symbols](http://bohemiancoding.com/sketch/support/documentation/07-symbols/), Magic Mirror uses [Pattern Fill](http://bohemiancoding.com/sketch/support/documentation/08-styling/1-fills.html) to preform the mirroring. It can mirror any number of Artboards to any number of shape layers in any size, any angle, but <em>also</em> responds to the shape’s distortion (perspective transformation).

Unlike when editing Bitmaps in Sketch, Magic Mirror does not modify the original bitmap in a destructive way (since we’re sourcing from an Artboard). Using Shape layers instead of Bitmap layers, editable paths are preserved and can be easily updated.


## So how does it work?

In short, Magic Mirror iterates through all the “Shape” layers (MSShapeGroup) in the current page, and finds all the Artboard-Layer pairs that share the exact same name.

Then it looks into the path (NSBezierPath) and extracts the 4 corner points.

It then hands the content over to [Core Image](https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/CoreImaging/ci_intro/ci_intro.html) to do Perspective Transformation, and apply the transformed image using Pattern Fill.

{% include showend.html %}

<section class="my2 py2 border-top clearfix" style='background-color:black'>
<h1>Showcase</h1>

<div class="flex-wrap">
{% for showcase in site.data.showcases %}
<div class="sm-col sm-col-4 showcase" style="order: {{ showcase.order }}">
	<img src="{{ showcase.image }}" />
	<a href="{{ showcase.link }}" identifier="{{ showcase.author }}" class="overlay">
		<img src="/images/showcase-placeholder.png" />
		<div class="overlay flex flex-end">
			<div class="flex flex-end m2">
				<div class="flex-none mr2">
					<img src="{{ showcase.avatar }}" class="avatar">
				</div>
				<div class="flex flex-column">
					<div class="flex-auto liner">“{{ showcase.liner }}” </div>
					<div class="flex-auto author">- {{ showcase.author }}</div>
				</div>
			</div>
		</div>
	</a>
</div>
{% endfor %}
</div>

</section>

{% include features.html %}
{% include featured.html %}
{% include purchase.html %}
{% include community.html %}
