---
layout: flex
title: Gallery
permalink: /profile/
banner: true
share:
  title: Subscribe for Magic Sketch
  description: Checkout the new Magic Templates Gallery
---

# Subscribe Magic Sketch

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
					window.location = '/login';
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

<script src="https://checkout.stripe.com/checkout.js"></script>

<button id="customButton" disabled="disabled">Subscribe magic sketch personal cloud (5GB)</button>
<button id="customButton2" disabled="disabled">Subscribe magic sketch premium plan (10GB + download premium content)</button>
<button id="customButton3" disabled="disabled">Subscribe magic sketch pro plan (50GB + download premium content)</button>

<button id="logoutButton">logout</button>

<div id="accountInfo"></div>

<div class="center wrapper mt4" markdown="1">

Magic Mirror Gallery is still in beta. If you want to help or want to have your own templates show up please read the <a href="/template-guideline">templates contribution guideline</a> :)

</div>
