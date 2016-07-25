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

		function getTemplates(){
			// TODO: get this user uploaded template
		}

		function setupProfile(user){
			$('.global-loader').remove();

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
				storageUsage = (user.customData.cloudUsage/1000000000);
			}else{
				storageTotal = (totalStorage/1000000)+" MB";
				storageUsage = (user.customData.cloudUsage/1000000);
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

	<div class="gallery-row flex">
		<div class="col-4 col gallery-preview">
			<div class="loader">
				<div class="spin">
					<i class="fa fa-spinner fa-spin fa-3x fa-fw"></i>
				</div>
			</div>
			<img src="/images/templates/2015-11-03-ipad-mac.jpg" />
		</div>
		<div class="col-4 col gallery-preview"><img src="/images/templates/ipad-on-desk.jpg" /></div>
		<div class="col-4 col gallery-preview"><img src="/images/templates/iphone-6-and-6s.jpg" /></div>
		<div class="clear"></div>
	</div>

	<div class="gallery-row flex">
		<div class="col-4 col gallery-preview">
			<div class="loader">
				<div class="spin">
					<i class="fa fa-spinner fa-spin fa-3x fa-fw"></i>
				</div>
			</div>
			<img src="/images/templates/iphone-6-fingertip.jpg" />
		</div>
		<div class="col-4 col gallery-preview">
			<div class="loader">
				<div class="spin">
					<i class="fa fa-spinner fa-spin fa-3x fa-fw"></i>
				</div>
			</div>
			<img src="/images/templates/iphone-office-cover.jpg" />
		</div>
		<div class="col-4 col gallery-preview">
			<div class="loader">
				<div class="spin">
					<i class="fa fa-spinner fa-spin fa-3x fa-fw"></i>
				</div>
			</div>
			<img src="/images/templates/iphone-watch-cover.jpg" />
		</div>
		<div class="clear"></div>
	</div>

	<div class="gallery-row flex">
		<div class="col-4 col gallery-preview"><img src="/images/templates/iphone6-girls-hand.jpg" /></div>
		<div class="col-4 col gallery-preview"><img src="/images/templates/iphone6s-flowkit.jpg" /></div>
		<div class="col-4 col gallery-preview"><img src="/images/templates/iphone6s-hands.jpg" /></div>
		<div class="clear"></div>
	</div>

	<div class="gallery-row flex">
		<div class="col-4 col gallery-preview"><img src="/images/templates/iphone6s.jpg" /></div>
		<div class="col-4 col gallery-preview"><img src="/images/templates/macbook-air-desk.jpg" /></div>
		<div class="col-4 col gallery-preview nothing"></div>
		<div class="clear"></div>
	</div>

</div>
