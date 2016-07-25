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
<script src="https://checkout.stripe.com/checkout.js"></script>
<script>
	var inapp = false;
	$( document ).ready(function() {

		function blockPageLoading(){
			var loading = $('<div>').addClass('loader global-loader').prependTo($('body'));
			$('<div>').addClass('spin').append($('<i>').addClass("fa fa-spinner fa-spin fa-3x fa-fw")).appendTo(loading);
		}

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
					console.log(json);
					Cookies.remove('t');
					Cookies.remove('rt');
					Cookies.remove('userEmail');

					if(inapp){
						window.location = '/login?inapp';
					}else{
						window.location = '/';
					}
				},
				success: function(json){
				},
				error: function(json){
					console.log(json);
				}
			});
		}

		function getUserPlan(){
			// TODO: get all plan and display
		}

		function getUserPaymentLog(){

		}

		function setupProfile(user){
			$('.global-loader').remove();

			var basicHandler = StripeCheckout.configure({
			    key: '{{ site.stripe[jekyll.environment].key }}',
			    image: '/images/profile.png',
			    locale: 'auto',
			    token: function(token) {
			      // You can access the token ID with `token.id`.
			      // Get the token ID to your server-side code for use.

			      	$('.subscribe-button').attr('disabled', 'disabled');
			      	blockPageLoading();
					// Perform subscribe
					$.ajax({
						url: '{{ site.apigateway[jekyll.environment].url }}/subscribe/MG01',
						data: token,
						method: 'POST',
						complete: function(json){
						},
						success: function(json){
							window.location.reload();
						},
						error: function(json){
							$('.global-loader').remove();
							$('.subscribe-button:not(.current-plan)').removeAttr('disabled');
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

			      	$('.subscribe-button').attr('disabled', 'disabled');
			      	blockPageLoading();
					// Perform subscribe
					$.ajax({
						url: '{{ site.apigateway[jekyll.environment].url }}/subscribe/MG02',
						data: token,
						method: 'POST',
						complete: function(json){
						},
						success: function(json){
							window.location.reload();
						},
						error: function(json){
							$('.global-loader').remove();
							$('.subscribe-button:not(.current-plan)').removeAttr('disabled');
						}
					});
			    },
			    email: user.email

			  });

			var ultraHandler = StripeCheckout.configure({
			    key: '{{ site.stripe[jekyll.environment].key }}',
			    image: '/images/profile.png',
			    locale: 'auto',
			    token: function(token) {
			      // You can access the token ID with `token.id`.
			      // Get the token ID to your server-side code for use.

			      	$('.subscribe-button').attr('disabled', 'disabled');
			      	blockPageLoading();
					// Perform subscribe
					$.ajax({
						url: '{{ site.apigateway[jekyll.environment].url }}/subscribe/MG03',
						data: token,
						method: 'POST',
						complete: function(json){
						},
						success: function(json){
							window.location.reload();
						},
						error: function(json){
							$('.global-loader').remove();
							$('.subscribe-button:not(.current-plan)').removeAttr('disabled');
						}
					});
			    },
			    email: user.email

			  });

			if(user.customData.accessLevel == 0){
				$('#noPlanButton').addClass('current-plan').html('current plan');
			}else{
				$('#noPlanButton').removeAttr('disabled');
				$('#noPlanButton').html('back to Free plan');
				$('#noPlanButton').on('click', function(e){
					if(confirm('Are you sure to unsubscribe Magic Gallery service?')){
						$('.subscribe-button').attr('disabled', 'disabled');
						blockPageLoading();
						$.ajax({
							url: '{{ site.apigateway[jekyll.environment].url }}/unsubscribe',
							headers: {
								'X-Access-Token': Cookies.get('t'),
								'X-Refresh-Token': Cookies.get('rt'),
							},
							method: 'DELETE',
							complete: function(json){
							},
							success: function(json){
								window.location.reload();
							},
							error: function(json){
								$('.global-loader').remove();
								$('.subscribe-button:not(.current-plan)').removeAttr('disabled');
							}
						});
					}
				});
			}

			if(user.customData.accessLevel == 1){
				$('#basicButton').addClass('current-plan').html('current plan');
			}else{
				$('#basicButton').removeAttr('disabled');
				$('#basicButton').on('click', function(e) {
					// Open Checkout with further options:
					basicHandler.open({
					  name: 'Subscribe to Basic plan',
					  description: '',
					  amount: 500,
					});
					e.preventDefault();
				});
			}

			if(user.customData.accessLevel == 2){
				$('#proButton').addClass('current-plan').html('current plan');
			}else{
				$('#proButton').removeAttr('disabled');
				$('#proButton').on('click', function(e) {
					// Open Checkout with further options:
					proHandler.open({
					  name: 'Subscribe to Pro plan',
					  description: '',
					  amount: 1000,
					});
					e.preventDefault();
				});
			}

			if(user.customData.accessLevel == 3){
				$('#ultraButton').addClass('current-plan').html('current plan');
			}else{
				$('#ultraButton').removeAttr('disabled');
				$('#ultraButton').on('click', function(e) {
					// Open Checkout with further options:
					ultraHandler.open({
						name: 'Subscribe to Ultra Plan',
						description: '',
						amount: 2000,
					});
					e.preventDefault();
				});
			}

			$('#nameDisplay').html(user.fullName);
			$('#planDisplay').html(user.customData.userType);

			if(inapp){
				$('#nameDisplay').attr('href', $('#nameDisplay').attr('href')+'?inapp');
				$('#planDisplay').attr('href', $('#planDisplay').attr('href')+'?inapp');
			}

			// getUserPlan();
			getUserPaymentLog();
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
				window.location = '/login' + (inapp?'?inapp':'');
			}
		});

	  });

</script>

<!-- <button id="customButton" disabled="disabled">Subscribe magic sketch personal cloud (5GB)</button>
<button id="customButton2" disabled="disabled">Subscribe magic sketch premium plan (10GB + download premium content)</button>
<button id="customButton3" disabled="disabled">Subscribe magic sketch pro plan (50GB + download premium content)</button>

<button id="logoutButton">logout</button>

<div id="accountInfo"></div>
 -->

<div class="loader global-loader">
	<div class="spin">
		<i class="fa fa-spinner fa-spin fa-3x fa-fw"></i>
	</div>
</div>

<div class="profile-content">
	<div class="profile-row flex">
		<div class="col-8 col info-content">
			<div class="profile-pic-info col"><img src="/images/arjen.jpg" /></div>
			<div class="user-info col">
				<div class="user-info-content thin-text">
					<a href="/profile" id="nameDisplay"></a>
					<div class="plan-info"><a href="/profile" id="planDisplay"></a></div>
				</div>
			</div>
		</div>
		<div class="col-2 col info-content">
			<div class="info-content-wrap thin-text">
				<a href="">edit your profile on gravtar</a>
			</div>
		</div>
		<div class="col-2 col info-content signout-field">
			<div class="info-content-wrap medium-text">
				<button id="logoutButton" class="signout-link">Sign out</button>
			</div>
		</div>
		<div class="clear"></div>
	</div>

	<div class="gallery-row flex">
		<div class="col-3 col plan-desc">
			<div class="plan-type">Free</div>
			<div class="plan-price medium-text">Free</div>
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
				<button class="subscribe-button no-plan" id="noPlanButton" disabled="disabled">current plan</button>
			</div>
		</div>
		<div class="col-3 col plan-desc">
			<div class="plan-type">Basic</div>
			<div class="plan-price medium-text">$5*</div>
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
				<button class="subscribe-button" id="basicButton" disabled="disabled">select plan</button>
			</div>
		</div>
		<div class="col-3 col plan-desc">
			<div class="plan-type">Pro</div>
			<div class="plan-price medium-text">$10*</div>
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
				<button class="subscribe-button" id="proButton" disabled="disabled">select plan</button>
			</div>
		</div>
		<div class="col-3 col plan-desc">
			<div class="plan-type">Ultra</div>
			<div class="plan-price medium-text">$20*</div>
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
				<button class="subscribe-button" id="ultraButton" disabled="disabled">select plan</button>
			</div>
		</div>
		<div class="clear"></div>
	</div>
	<div class="remarks thin-text">* price in USD.</div>

	<div class="log-content medium-text">
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
