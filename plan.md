---
layout: flex
title: Gallery
permalink: /plan/
banner: true
share:
  title: Subscribe for Magic Sketch
  description: Checkout the new Magic Templates Gallery
---

<link rel="stylesheet" type="text/css" href="/css/gallery.css" media="screen" />

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
		}

		$('#logoutButton').click(function(e){
			logout();

			$(this).attr('disabled', 'disabled');
		});

		// $.ajax({
		// 	url: '{{ site.apigateway[jekyll.environment].url }}/user',
		// 	data: {
		// 		email: Cookies.get('userEmail')
		// 	},
		// 	headers: {
		// 		'X-Access-Token': Cookies.get('t'),
		// 		'X-Refresh-Token': Cookies.get('rt'),
		// 	},
		// 	method: 'GET',
		// 	complete: function(json){
		// 	},
		// 	success: function(json){
		// 		console.log(json);

		// 		if(json.email === undefined){
		// 			window.location = '/login';
		// 		}else{
		// 			setupProfile(json);
		// 		}
		// 	},
		// 	error: function(json){
		// 		console.log(json);
		// 	}
		// });

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
		<div class="col-8 col info-content">
			<div class="profile-pic-info col"><img src="/images/profile.png" /></div>
			<div class="user-info col">
				<div class="user-info-content">
					James Tang
					<div class="plan-info">james@magicsketch.io</div>
				</div>
			</div>
		</div>
		<div class="col-2 col info-content">
			<div class="info-content-wrap">
				<a href="">edit your profile on gravtar</a>
			</div>
		</div>
		<div class="col-2 col info-content signout-field">
			<div class="info-content-wrap">
				<button id="logoutButton" class="signout-link">Sign out</button>
			</div>
		</div>
		<div class="clear"></div>
	</div>

	<div class="gallery-row flex">
		<div class="col-3 col plan-desc">
			<div class="plan-type">Free</div>
			<div class="plan-price">Free</div>
			<div class="plan-duration">Monthly</div>
			<div class="plan-storage col-12">
				<div class="col-7 col category">Storage</div>
				<div class="col-5 col category-value">100MB</div>
				<div class="clear"></div>
			</div>
			<div class="plan-traffic col-12">
				<div class="col-7 col category">Traffic</div>
				<div class="col-5 col category-value">1GB</div>
				<div class="clear"></div>
			</div>
			<div class="plan-subscribe">
				<button class="subscribe-button" disabled="disabled">current plan</button>
			</div>
		</div>
		<div class="col-3 col plan-desc">
			<div class="plan-type">Basic</div>
			<div class="plan-price">$5*</div>
			<div class="plan-duration">Monthly</div>
			<div class="plan-storage col-12">
				<div class="col-7 col category">Storage</div>
				<div class="col-5 col category-value">1GB</div>
				<div class="clear"></div>
			</div>
			<div class="plan-traffic col-12">
				<div class="col-7 col category">Traffic</div>
				<div class="col-5 col category-value">10GB</div>
				<div class="clear"></div>
			</div>
			<div class="plan-subscribe">
				<button class="subscribe-button">select plan</button>
			</div>
		</div>
		<div class="col-3 col plan-desc">
			<div class="plan-type">Pro</div>
			<div class="plan-price">$10*</div>
			<div class="plan-duration">Monthly</div>
			<div class="plan-storage col-12">
				<div class="col-7 col category">Storage</div>
				<div class="col-5 col category-value">3GB</div>
				<div class="clear"></div>
			</div>
			<div class="plan-traffic col-12">
				<div class="col-7 col category">Traffic</div>
				<div class="col-5 col category-value">30GB</div>
				<div class="clear"></div>
			</div>
			<div class="plan-subscribe">
				<button class="subscribe-button">select plan</button>
			</div>
		</div>
		<div class="col-3 col plan-desc">
			<div class="plan-type">Ultra</div>
			<div class="plan-price">$20*</div>
			<div class="plan-duration">Monthly</div>
			<div class="plan-storage col-12">
				<div class="col-7 col category">Storage</div>
				<div class="col-5 col category-value">10GB</div>
				<div class="clear"></div>
			</div>
			<div class="plan-traffic col-12">
				<div class="col-7 col category">Traffic</div>
				<div class="col-5 col category-value">200GB</div>
				<div class="clear"></div>
			</div>
			<div class="plan-subscribe">
				<button class="subscribe-button">select plan</button>
			</div>
		</div>
		<div class="clear"></div>
	</div>
	<div class="remarks">* price in usd.</div>

	<div class="log-content">
		<div class="title">Transaction Log</div>
		<div class="log-record col-12">
			<div class="col-6 col log-time">2016-04-20</div>
			<div class="col-6 col log-plan">Pro $10</div>
			<div class="clear"></div>
		</div>
		<div class="log-record col-12">
			<div class="col-6 col log-time">2016-04-20</div>
			<div class="col-6 col log-plan">Pro $10</div>
			<div class="clear"></div>
		</div>
		<div class="log-record col-12">
			<div class="col-6 col log-time">2016-04-20</div>
			<div class="col-6 col log-plan">Pro $10</div>
			<div class="clear"></div>
		</div>
		<div class="log-record col-12">
			<div class="col-6 col log-time">2016-04-20</div>
			<div class="col-6 col log-plan">Pro $10</div>
			<div class="clear"></div>
		</div>
	</div>

</div>
