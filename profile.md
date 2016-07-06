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

		if(getParameterByName('inapp') != null){
			$('.flex-center.mb2').hide();
			$('.site-header').hide();
			$('.site-footer').hide();
		}

	  });

</script>

<div class="">

<script src="https://checkout.stripe.com/checkout.js"></script>

<button id="customButton">Purchase</button>

<script>
  var handler = StripeCheckout.configure({
    key: 'pk_test_nF0KASSRwbKt0dujnXAyxwpW',
    image: '/img/documentation/checkout/marketplace.png',
    locale: 'auto',
    token: function(token) {
      // You can access the token ID with `token.id`.
      // Get the token ID to your server-side code for use.

		// Perform subscribe
		$.ajax({
			url: 'http://localhost:3000/subscribe',
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
    email: 'hihi11@hihi.com'

  });

  $('#customButton').on('click', function(e) {
    // Open Checkout with further options:
    handler.open({
      name: 'Demo Site',
      description: '2 widgets',
      amount: 2000,
    });
    e.preventDefault();
  });

  // Close Checkout on page navigation:
  // $(window).on('popstate', function() {
  //   handler.close();
  // });
</script>

<div class="center wrapper mt4" markdown="1">

Magic Mirror Gallery is still in beta. If you want to help or want to have your own templates show up please read the <a href="/template-guideline">templates contribution guideline</a> :)

</div>
