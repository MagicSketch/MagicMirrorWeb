---
layout: page-without-title
title: Pro Version
permalink: /purchase/
weight: 4
banner: true
purchase-button: false
show-featured: true
share:
  title: Image Perspective Transform Plugin for Sketch 3
  url: http://magicmirror.design
  description: Create Professional Realistic Mockups with Magic Mirror 2
---

<style type="text/css">
  	h3 {
  		/* 1. Download the plug: */
  		font-family: Asap-Regular;
  		font-size: 32px;
  		color: #9B9B9B;
  		line-height: 42px;
  		margin-top: 60px;
  		text-align: center;
  	}
  	p {
		font-family: Asap-Regular;
		font-size: 18px;
		color: #B3B2B2;
		line-height: 32px;
		text-align: center;
  	}
	.purchase-button
	{
	    color: #fff !important;
		background-color: #F79403;
		padding: 10px 20px 10px 20px;
		border-radius: 20px;
		text-decoration: none !important;
	}

	.custom-button-nav
	{
		margin: 0 0px 0 10px;
	}

	.fourth-block
	{
		width: 100%;
		background-color: #E5E5E5;
		border-radius: 10px;
	}

	.fourth-block-center
	{
		padding: 10px 10px 10px 10px;
	}

	.fourth-block-center span
	{
		font-size: 13px;
	}

	.fourth-block-center span span
	{
		font-weight: bold;
	}

	.fifth-block
	{
		background-color: #FFF7D0;
		width:100%;
		border-radius: 10px;
	}

	.fifth-first
	{
		float: left;
		width: 30%;
		padding: 0 15px 0 15px;
		text-align: center;
	}

	.fifth-second
	{
		float: left;
		width: 30%;
		padding: 0 20px 0 0px;
	}

	.sixth-block
	{
		width: 100%;
		text-align: center;
	}

	.seventh-block
	{
		width: 100%;
		background-color: #FAFAFA;
	}

	.seventh-first
	{
		width: 23%;
		float: left;
	}

	.seventh-second
	{
		width: 23%;
		float: left;
		padding: 0 15px 0 0;
	}

	.seventh-third
	{
		width: 23%;
		float: left;
		padding: 0 0px 0 10px;
	}

	.seventh-fourth
	{
		width: 23%;
		float: right;
	}


</style>

# What's in the Pro version

## Magic Mirror 2 vs Magic Mirror 1

- Enhanced Image Quality
- Improved Performance (3x-5x better)
- New UI Toolbar
- Live Update (experiemental)

## The Story:

After two full months of working on this update, I've finally made its way to this major release. It's a free upgrade to all Magic Mirror 1 supporters, just download the latest version and enjoy the new features! Like the first version, number of features are locked until you've enter the license key.


### Enhanced Image Quality

![](/images/enhanced-image-quality.png)

All transformed image should look pixel perfect in 100% zoomed in even in @1x settings.
However, when you're looking to export images with @2x or above resolution, the source would have provide 4 times as much pixels.
Enhanced Image Quality is here to solve the issue.
@1x and @2x depends on the source of the artboard size, so the higher the source is, the clearer the rendered image. It's fast and works well with general UI perpective transform.

Max resolution depends on the shape, it looks into the target's shape size and find out the best resolution it can be rendered to make exporting in @3x as clear as possible. Works best for rendering small vector UI components into larger canvas.

*Free version will see a watermark in @2x and Max image quality setting.

<div class="fourth-block">
	<div class="fourth-block-center">
		Free version of Magic Mirror is licensed under the creative commons Attibution-NonCommercial 4.0 International License.
		<br>
		To use it for Commercial projects, you'll have to obtain commercial license through purchasing below.
		<br>
		<span>
			(Early doners in v1.1 before will <span>not</span> need to pay anything extra to continue to use the plugin for commercial purpose.)
		</span>
	</div>
</div>
<div class="py2 clear"></div>

{% include tips.html %}

<div class="py2 clear"></div>

<div class="sixth-block">
	<a href="/proceed-to-purchase/" id="proceed-to-purchase" identifier="proceed-to-purchase-tips" class="purchase-button">Upgrade for ${{ site.data.products.plugin.price }} <s>${{ site.data.products.plugin.original }}</s></a>
  <span id="tweet-text" class="px2">Tweet to get extra 25% off!</span>
</div>
<br>
<br><br>
