---
layout: flex
title: Gallery
permalink: /login/
banner: true
share:
  title: Login For Magic Sketch
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
				url: '{{ site.apigateway_url }}/login',
				data: param,
				method: 'POST',
				complete: function(json){
				},
				success: function(json){
					Cookies.set('t', json.access_token); //{domain: 'config.domain'});
					Cookies.set('rt', json.refresh_token);
					Cookies.set('userEmail', email);
					console.log(json);

					window.location = '/profile';
				},
				error: function(json){
					console.log(json);
				}
			});
		}

		function logout(){
			var param = {
				email: Cookies.get('userEmail'),
			};

			// Perform Login
			$.ajax({
				url: '{{ site.apigateway_url }}/logout',
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

		$('#loginButton').click(function(e){
			var email = $('#emailInput').val();
			var password = $('#passwordInput').val();

			login(email, password);

			$(this).attr('disabled', 'disabled');
		});

		$('#logoutButton').click(function(e){
			logout();

			$(this).attr('disabled', 'disabled');
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
<button id="logoutButton">logout</button>
<div class="center wrapper mt4" markdown="1">

Magic Mirror Gallery is still in beta. If you want to help or want to have your own templates show up please read the <a href="/template-guideline">templates contribution guideline</a> :)

</div>
