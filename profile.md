---
layout: flex
title: Gallery
permalink: /profile/
banner: true
share:
  title: Subscribe for Magic Sketch
  description: Checkout the new Magic Templates Gallery
---

<link rel="stylesheet" type="text/css" href="/css/gallery.css" media="screen" />

<script>
	var inapp = false;
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

		function createGalleryGrid(item){
			var row = $('<div>').addClass('col-4 col gallery-preview');
			var loader = $('<div>').addClass('loader').append($('<div>').addClass('spin').append($('<i>').addClass('fa fa-spinner fa-spin fa-3x fa-fw'))).hide().appendTo(row);
			var image = $('<img>').appendTo(row);

			console.log(item);

			if(item === undefined){
				row.addClass('nothing');
			}else{
				image.attr('src', item.preview);

				row.click(function(e){
					loader.show();

					window.location.href = item.data;
					// console.log('download ' + item.data);

					setTimeout(function(){
						loader.hide();
					}, 5000);
				});
			}

			return row;
		}

		function createTemplatesDisplay(list){
			var container = $('#galleryContainer');
			var index = 0;

			while(index < list.length){
				var row = $('<div>').addClass('gallery-row flex').appendTo(container);
				for(;;index++){
					row.append(createGalleryGrid(list[index]));
					if((index+1)%3 == 0 && index != 0){
						break;
					}
				}
				$('<div>').addClass('clear').appendTo(row);

				index++;
			}

			$('.global-loader').remove();
		}

		function getTemplates(){
			$.ajax({
				url: '{{ site.apigateway[jekyll.environment].url }}/mytemplate',
				method: 'GET',
				headers: {
					'X-Access-Token': Cookies.get('t'),
					'X-Refresh-Token': Cookies.get('rt'),
				},
				success: function (data) {
					createTemplatesDisplay(data);
				},
				error: function (error) {
					console.log('error', error);
				}
			});
		}

		function setupProfile(user){
			var totalStorage = user.customData.freeStorage + user.customData.cloudStorage;
			var storagePercent = user.customData.cloudUsage / totalStorage * 100;
			var trafficPercent = user.customData.trafficUsage / user.customData.trafficLimit * 100;

			var storageUsage = "";
			var storageTotal = "";
			var trafficUsage = "";
			var trafficTotal = "";

			if(user.customData.trafficLimit > 1000000000){
				trafficTotal = (user.customData.trafficLimit/1000000000)+" GB";
				trafficUsage = (user.customData.trafficUsage/1000000000);
			}else{
				trafficTotal = (user.customData.trafficLimit/1000000)+" MB";
				trafficUsage = (user.customData.trafficUsage/1000000);
			}

			if(totalStorage > 1000000000){
				storageTotal = (totalStorage/1000000000)+" GB";
				storageUsage = Math.round(user.customData.cloudUsage/1000000000 * 100) / 100;
			}else{
				storageTotal = (totalStorage/1000000)+" MB";
				storageUsage = Math.round(user.customData.cloudUsage/1000000 * 100) / 100;
			}

			if(trafficPercent > 100){
				trafficPercent = 100;
				trafficFull = true;
				$("#trafficUsageBar").addClass('full');
			}
			if(storagePercent > 100){
				storagePercent = 100;
				$("#storageUsageBar").addClass('full');
			}


			$('#nameDisplay').html(user.fullName);
			$('#planDisplay').html(user.customData.userType);

			$("#trafficUsageDisplay").html(trafficUsage);
			$("#trafficLimitDisplay").html(trafficTotal);
			$("#trafficUsageBar").attr('style', 'width:'+trafficPercent+'%');
			$("#storageUsageDisplay").html(storageUsage);
			$("#storageLimitDisplay").html(storageTotal);
			$("#storageUsageBar").attr('style', 'width:'+storagePercent+'%');

			if(inapp){
				$('#nameDisplay').attr('href', $('#nameDisplay').attr('href')+'?inapp');
				$('#planDisplay').attr('href', $('#planDisplay').attr('href')+'?inapp');
			}

			getTemplates();
		}

		if(getParameterByName('inapp') != null){
			$('.flex-center.mb2').hide();
			$('.site-header').hide();
			$('.site-footer').hide();

			inapp = true;
		}

		console.log(Cookies.get('t'));
		console.log(Cookies.get('rt'));

		$.ajax({
			url: '{{ site.apigateway[jekyll.environment].url }}/user',
			data: {
				email: Cookies.get('userEmail')
			},
			headers: {
				'X-Access-Token': Cookies.get('t'),
				'X-Refresh-Token': Cookies.get('rt'),
			},
			method: 'GET',
			complete: function(json){
			},
			success: function(json){
				console.log(json);

				if(json.email === undefined){
					window.location = '/login' + (inapp?'?inapp':'');
				}else{
					setupProfile(json);
				}
			},
			error: function(json){
				window.location = '/login' + (inapp?'?inapp':'');
			}
		});

	  });

</script>

<div class="loader global-loader">
	<div class="spin">
		<i class="fa fa-spinner fa-spin fa-3x fa-fw"></i>
	</div>
</div>
<div class="profile-content">
	<div class="profile-row flex">
		<div class="col-4 col info-content">
			<div class="profile-pic-info col"><img src="/images/arjen.jpg" /></div>
			<div class="user-info col">
				<div class="user-info-content thin-text">
					<a href="/plan" id="nameDisplay"></a>
					<div class="plan-info"><a href="/plan" id="planDisplay">FREE USER</a></div>
				</div>
			</div>
		</div>
		<div class="col-4 col usage-field info-content">
			<div class="info-content-wrap thin-text">
				<div class="col">Traffic</div><div class="col-right"><span id="trafficUsageDisplay">0</span> / <span id="trafficLimitDisplay">0 MB</span></div>
				<div class="clear"></div>
				<div class="bar"><div class="usage-bar traffic" style="width:0" id="trafficUsageBar"></div></div>
			</div>
		</div>
		<div class="col-4 col usage-field info-content">
			<div class="info-content-wrap thin-text">
				<div class="col">Storage</div><div class="col-right"><span id="storageUsageDisplay">0</span> / <span id="storageLimitDisplay">0 MB</span></div>
				<div class="clear"></div>
				<div class="bar"><div class="usage-bar storage" style="width:0" id="storageUsageBar"></div></div>
			</div>
		</div>
		<div class="clear"></div>
	</div>

	<div id="galleryContainer">
	</div>

</div>
