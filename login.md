---
layout: flex
title: Gallery
permalink: /login/
banner: true
share:
  title: Login For Magic Sketch
  description: Checkout the new Magic Templates Gallery
---

<link rel="stylesheet" type="text/css" href="/css/gallery.css" media="screen" />

# Login Magic Gallery

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

		if(getParameterByName('inapp') != null){
			$('.flex-center.mb2').hide();
			$('.site-header').hide();
			$('.site-footer').hide();

			inapp = true;
		}

		function login(email, password){
			var errorOutput = $('#errorMsg');
			var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

			if(!re.test(email)){
				errorOutput.html('Email address is invalid');
				$('#loginButton').removeAttr('disabled');
				return false;
			}

			var param = {
				email: email,
				password: password
			};

			// Perform Login
			$.ajax({
				url: '{{ site.apigateway[jekyll.environment].url }}/login',
				data: param,
				method: 'POST',
				complete: function(json){
				},
				success: function(json){
					Cookies.set('t', json.access_token); //{domain: 'config.domain'});
					Cookies.set('rt', json.refresh_token);
					Cookies.set('userEmail', email);

					window.location = '/profile'+(inapp?'?inapp':'');
				},
				error: function(json){
					console.log(json);

					errorOutput.html('There is problem on logging in.');
					$('#loginButton').removeAttr('disabled');
				}
			});
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

		$('#signupButton').click(function(e){
			window.location = '/signup' + (inapp?'?inapp':'');
		});

	  });

</script>

<div class="login-form-container">
	<div class="field-area">
		<div class="form-field">
			<i class="fa fa-envelope-o" aria-hidden="true"></i>
			<input type="text" id="emailInput" placeholder="Email" />
		</div>

		<div class="form-field">
			<i class="fa fa-key" aria-hidden="true"></i>
			<input type="password" id="passwordInput" placeholder="Password" />
		</div>
		<div class="form-field no-border">
			<div id="errorMsg"></div>
		</div>
	</div>

	<div class="account-control">
		<div class="col-right col-6"><button class="button-action" id="signupButton">Sign up</button></div>
		<div class="col-right col-6"><button class="button-action" id="loginButton">Login</button></div>
	</div>

</div>