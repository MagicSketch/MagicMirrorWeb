---
layout: flex
title: Gallery
permalink: /signup/
banner: true
share:
  title: Sign up For Magic Sketch
  description: Checkout the new Magic Templates Gallery
---

<link rel="stylesheet" type="text/css" href="/css/gallery.css" media="screen" />

# Sign up for Magic Gallery

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

		function signupUser(email, password, confirmPassword, firstName, lastName){
			var errorOutput = $('#errorMsg');
			var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

			if(password != confirmPassword){
				errorOutput.html('Confirm password does not match');
				return false;
			}
			if(!re.test(email)){
				errorOutput.html('Email address is invalid');
				return false;
			}

			var param = {
				'email': email,
				'password': password,
				'firstName': firstName,
				'lastName': lastName,
			};

			// create account
			$.ajax({
				url: '{{ site.apigateway[jekyll.environment].url }}/signup',
				data: param,
				method: 'POST',
				complete: function(json){
				},
				success: function(json){
					console.log(json);

					if(json.userType !== undefined){
						window.location = '/login' + (inapp?'inapp':'');
					}else{
						if(json.message !== undefined){
							errorOutput.html(json.message);
						}else{
							errorOutput.html('There is some error on signing up.');
						}
						$('#signupButton').removeAttr('disabled');
					}
				},
				error: function(json){
					console.log(json);

					$('#signupButton').removeAttr('disabled');
				}
			});
		}

		$('#signupButton').click(function(e){
			var email = $('#emailInput').val();
			var password = $('#passwordInput').val();
			var confirmPassword = $('#confirmPasswordInput').val();
			var firstName = $('#firstNameInput').val();
			var lastName = $('#lastNameInput').val();

			$(this).attr('disabled', 'disabled');

			signupUser(email, password, confirmPassword, firstName, lastName);
		});

		$('#loginButton').click(function(e){
			window.location = '/login' + (inapp?'?inapp':'');
		});

	  });

</script>


<div class="signup-form-container">
	<div class="field-area">
		<div class="form-field col-6 col first-input">
			<input type="text" id="firstNameInput" placeholder="First Name" />
		</div>

		<div class="form-field col-5 col">
			<input type="text" id="lastNameInput" placeholder="Last Name" />
		</div>

		<div class="clear"></div>

		<div class="form-field">
			<i class="fa fa-envelope-o" aria-hidden="true"></i>
			<input type="text" id="emailInput" placeholder="Email" />
		</div>

		<div class="form-field">
			<i class="fa fa-key" aria-hidden="true"></i>
			<input type="password" id="passwordInput" placeholder="Password" />
		</div>
		<div class="form-field">
			<i class="fa fa-key" aria-hidden="true"></i>
			<input type="password" id="confirmPasswordInput" placeholder="Confirm Password" />
		</div>
		<div class="form-field no-border">
			<div id="errorMsg"></div>
		</div>
	</div>

	<div class="account-control">
		<button class="button-action" id="signupButton">Sign up</button>
		<p>&nbsp;</p>
		<button class="button-action" id="loginButton">Have account? Login</button>
	</div>

</div>