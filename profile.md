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

		function logout(){
			var param = {
				email: Cookies.get('userEmail'),
			};

			// Perform Login
			$.ajax({
				url: '{{ site.apigateway[jekyll.environment].url }}/logout',
				data: param,
				headers: {
					'X-Access-Token': Cookies.get('t'),
					'X-Refresh-Token': Cookies.get('rt'),
				},
				method: 'DELETE',
				complete: function(json){
				},
				success: function(json){
					console.log(json);
					Cookies.remove('t');
					Cookies.remove('rt');
					Cookies.remove('userEmail');

					window.location = '/';
				},
				error: function(json){
					console.log(json);
				}
			});
		}

		function setupProfile(user){
			var basicHandler = StripeCheckout.configure({
			    key: '{{ site.stripe[jekyll.environment].key }}',
			    image: '/images/profile.png',
			    locale: 'auto',
			    token: function(token) {
			      // You can access the token ID with `token.id`.
			      // Get the token ID to your server-side code for use.

					// Perform subscribe
					$.ajax({
						url: '{{ site.apigateway[jekyll.environment].url }}/subscribe/MG01',
						data: token,
						method: 'POST',
						complete: function(json){
						},
						success: function(json){
							console.log(json);
						},
						error: function(json){
							console.log(json);
						}
					});
			    },
			    email: user.email

			  });

			var premiumHandler = StripeCheckout.configure({
			    key: '{{ site.stripe[jekyll.environment].key }}',
			    image: '/images/profile.png',
			    locale: 'auto',
			    token: function(token) {
			      // You can access the token ID with `token.id`.
			      // Get the token ID to your server-side code for use.

					// Perform subscribe
					$.ajax({
						url: '{{ site.apigateway[jekyll.environment].url }}/subscribe/MG02',
						data: token,
						method: 'POST',
						complete: function(json){
						},
						success: function(json){
							console.log(json);
						},
						error: function(json){
							console.log(json);
						}
					});
			    },
			    email: user.email

			  });

			var proHandler = StripeCheckout.configure({
			    key: '{{ site.stripe[jekyll.environment].key }}',
			    image: '/images/profile.png',
			    locale: 'auto',
			    token: function(token) {
			      // You can access the token ID with `token.id`.
			      // Get the token ID to your server-side code for use.

					// Perform subscribe
					$.ajax({
						url: '{{ site.apigateway[jekyll.environment].url }}/subscribe/MG03',
						data: token,
						method: 'POST',
						complete: function(json){
						},
						success: function(json){
							console.log(json);
						},
						error: function(json){
							console.log(json);
						}
					});
			    },
			    email: user.email

			  });

		  $('#customButton').removeAttr('disabled');
		  $('#customButton').on('click', function(e) {
		    // Open Checkout with further options:
		    basicHandler.open({
		      name: 'Basic plan',
		      description: '5GB cloud storage',
		      amount: 999,
		    });
		    e.preventDefault();
		  });

		  $('#customButton2').removeAttr('disabled');
		  $('#customButton2').on('click', function(e) {
		    // Open Checkout with further options:
		    premiumHandler.open({
		      name: 'Premium plan',
		      description: '10GB cloud storage + access to premium content',
		      amount: 2999,
		    });
		    e.preventDefault();
		  });

		  $('#customButton3').removeAttr('disabled');
		  $('#customButton3').on('click', function(e) {
		    // Open Checkout with further options:
		    proHandler.open({
		      name: 'Pro Plan',
		      description: '50GB cloud storage + access to premium content',
		      amount: 5999,
		    });
		    e.preventDefault();
		  });

		  $('#accountInfo').html('Logged in as: '+ user.email);
		}

		if(getParameterByName('inapp') != null){
			$('.flex-center.mb2').hide();
			$('.site-header').hide();
			$('.site-footer').hide();

			inapp = true;
		}

		$('#logoutButton').click(function(e){
			logout();

			$(this).attr('disabled', 'disabled');
		});

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
				console.log(json);
			}
		});

	  });

</script>

<!-- <script src="https://checkout.stripe.com/checkout.js"></script> -->

<!-- <button id="customButton" disabled="disabled">Subscribe magic sketch personal cloud (5GB)</button>
<button id="customButton2" disabled="disabled">Subscribe magic sketch premium plan (10GB + download premium content)</button>
<button id="customButton3" disabled="disabled">Subscribe magic sketch pro plan (50GB + download premium content)</button>

<button id="logoutButton">logout</button>

<div id="accountInfo"></div>
 -->
<div class="profile-content">
	<div class="profile-row flex">
		<div class="col-4 col info-content">
			<div class="profile-pic-info col"><img src="/images/profile.png" /></div>
			<div class="user-info col">
				<div class="user-info-content thin-text">
					<a href="/plan">James Tang</a>
					<div class="plan-info"><a href="/plan">BASIC PLAN</a></div>
				</div>
			</div>
		</div>
		<div class="col-4 col usage-field info-content">
			<div class="info-content-wrap thin-text">
				<div class="col">Traffic</div><div class="col-right">7 / 10 GB</div>
				<div class="clear"></div>
				<div class="bar"><div class="usage-bar traffic" style="width:33%"></div></div>
			</div>
		</div>
		<div class="col-4 col usage-field info-content">
			<div class="info-content-wrap thin-text">
				<div class="col">Storage</div><div class="col-right">7 / 1000 MB</div>
				<div class="clear"></div>
				<div class="bar"><div class="usage-bar storage" style="width:77%"></div></div>
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
