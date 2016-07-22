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
					if(json.access_token !== undefined){
						Cookies.set('t', json.access_token); //{domain: 'config.domain'});
						Cookies.set('rt', json.refresh_token);
						Cookies.set('userEmail', email);

						window.location = '/profile'+(inapp?'?inapp':'');	
					}else{
						console.log(json);
						errorOutput.html('There is problem on logging in.');
						$('#loginButton').removeAttr('disabled');
					}
					
				},
				error: function(json){
					console.log(json);

					if(json.message === undefined){
						errorOutput.html('There is problem on logging in.');
					}else{
						errorOutput.html(json.message);
					}
					
					$('#loginButton').removeAttr('disabled');
				}
			});
		}

		$('#loginButton').click(function(e){
			var email = $('#emailInput').val();
			var password = $('#passwordInput').val();
			$(this).attr('disabled', 'disabled');

			login(email, password);
		});

		$('#passwordInput').keypress(function(e){
			if(e.which == 13) {
				$('#loginButton').click();
			}
		});

		$('#logoutButton').click(function(e){
			$(this).attr('disabled', 'disabled');
			logout();
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