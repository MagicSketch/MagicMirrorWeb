---
layout: flex
title: Gallery
permalink: /gallery/
weight: 1
banner: true
share:
  title: Sketch Template Gallery
  description: Checkout the new Magic Templates Gallery
---

# Gallery

<script>

	$( document ).ready(function() {

		function getParameterByName(name, url) {
		    if (!url) url = window.location.href;
		    name = name.replace(/[\[\]]/g, "\\$&");
		    var regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"),
		        results = regex.exec(url);
		    if (!results) return null;
		    if (!results[2]) return '';
		    return decodeURIComponent(results[2].replace(/\+/g, " "));
		}

		function createGalleryGrid(galleryItem){
			var result = $('<div>').addClass("flex sm-col-6 md-col-4 border-box p1 template free");
			var body = $('<div>').addClass('p1 border rounded').appendTo(result);

			var previewLink = $('<a>').attr({href: galleryItem.data}).append($('<img>').attr({'src': galleryItem.preview, 'height': 'auto'})).appendTo(body);

			var info = $('<div>').addClass('mx-auto').appendTo(body);
			var bigSpan = $('<span>').addClass('flex').appendTo(info);
			var infoSpan = $('<span>').addClass('flex-auto').appendTo(bigSpan);
			$('<h4>').addClass('title mt1 mb1 bold').html(galleryItem.name).appendTo(infoSpan);
			$('<i>').addClass('meta m0').html('description').appendTo(infoSpan);
			// $('author').append?
			$('<p>').addClass('author').append($('<a>').attr({href: 'http://twitter.com/jamztang', identifier: 'author'}).addClass('name').append($('<img>').attr({src: 'https://avatars2.githubusercontent.com/u/852375?v=3&s=460'}).addClass('avatar')).append(' James Tang')).appendTo(infoSpan);

			var priceDiv = $('<div>').addClass('flex-none p1 right-align').appendTo(bigSpan);
			$('<p>').addClass('status').append('FREE').appendTo(priceDiv);

			return result;
		}

		if(getParameterByName('inapp') != null){
			$('.flex-center.mb2').hide();
			$('.site-header').hide();
			$('.site-footer').hide();
		}

		$.ajax({
		  url: 'https://api.fieldbook.com/v1/572f1172158f420300f5211b/template',
		  method: 'GET',
		  success: function (data) {
		    $.each(data, function(index, item){
		    	$('#galleryContainer').append(new createGalleryGrid(item));
		    });
		  },
		  error: function (error) {
		    console.log('error', error);
		  }
		});

	  });

</script>

<div class="flex flex-wrap p1 templates" id="galleryContainer">

</div>
<div class="center wrapper mt4" markdown="1">

Magic Mirror Gallery is still in beta. If you want to help or want to have your own templates show up please read the <a href="/template-guideline">templates contribution guideline</a> :)

</div>
