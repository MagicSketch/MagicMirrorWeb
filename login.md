---
layout: flex
title: Gallery
permalink: /login/
banner: true
share:
  title: Sign up For Magic Sketch
  description: Checkout the new Magic Templates Gallery
---

# Login Magic Sketch

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

		// $.ajax({
		//   url: 'https://api.fieldbook.com/v1/572f1172158f420300f5211b/template',
		//   method: 'GET',
		//   success: function (data) {
		//     $.each(data, function(index, item){
		//     	$('#galleryContainer').append(new createGalleryGrid(item));
		//     });
		//   },
		//   error: function (error) {
		//     console.log('error', error);
		//   }
		// });

		function login(email, password){
			var errorOutput = $('#errorMsg');
			var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

			if(!re.test(email)){
				errorOutput.html('Email address is invalid');
				return false;
			}

			var param = {
				email: email,
				password: password
			};

			// Perform Login
			$.ajax({
				url: 'http://localhost:3000/login',
				data: param,
				method: 'POST',
				complete: function(json){
				},
				success: function(json){
					Cookies.set('t', json.access_token); //{domain: 'config.domain'});
					Cookies.set('rt', json.refresh_token);
					console.log(json);
				},
				error: function(json){
					console.log(json);
				}
			});
		}

		$('#loginButton').click(function(e){
			var email = $('#emailInput').val();
			var password = $('#passwordInput').val();

			login(email, password);
		});

		$('#localMsg').html(Cookies.get('t') + ':' + Cookies.get('rt'));

	  });

</script>

<div class="">
	<div>
		<label for="emailInput">Email:</label>
		<input type="text" id="emailInput" />
	</div>
	<div>
		<label for="passwordInput">Password:</label>
		<input type="password" id="passwordInput" />
	</div>
	<div id="errorMsg"></div>
	<div>
		<button id="loginButton">Login</button>
	</div>
	<div id="localMsg"></div>
</div>
<div class="center wrapper mt4" markdown="1">

Magic Mirror Gallery is still in beta. If you want to help or want to have your own templates show up please read the <a href="/template-guideline">templates contribution guideline</a> :)

</div>
