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

		// function createGalleryGrid(galleryItem){
		// 	var result = $('<div>').addClass("flex sm-col-6 md-col-4 border-box p1 template free");
		// 	var body = $('<div>').addClass('p1 border rounded sm-col-12 md-col-12').appendTo(result);

		// 	var previewLink = $('<a>').attr({href: galleryItem.data}).append($('<img>').attr({'src': galleryItem.preview, 'height': 'auto'})).appendTo(body);

		// 	var info = $('<div>').addClass('mx-auto').appendTo(body);
		// 	var bigSpan = $('<span>').addClass('flex').appendTo(info);
		// 	var infoSpan = $('<span>').addClass('flex-auto').appendTo(bigSpan);
		// 	$('<h4>').addClass('title mt1 mb1 bold').html(galleryItem.name).appendTo(infoSpan);
		// 	$('<i>').addClass('meta m0').html('description').appendTo(infoSpan);
		// 	// $('author').append?
		// 	$('<p>').addClass('author').append($('<a>').attr({href: 'http://twitter.com/jamztang', identifier: 'author'}).addClass('name').append($('<img>').attr({src: 'https://avatars2.githubusercontent.com/u/852375?v=3&s=460'}).addClass('avatar')).append(' James Tang')).appendTo(infoSpan);

		// 	var priceDiv = $('<div>').addClass('flex-none p1 right-align').appendTo(bigSpan);
		// 	$('<p>').addClass('status').append('FREE').appendTo(priceDiv);

		// 	return result;
		// }

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

			// create stripe 
			$.ajax({
				url: '{{ site.apigateway[jekyll.environment].url }}/signup',
				data: param,
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
		}

		$('#signupButton').click(function(e){
			var email = $('#emailInput').val();
			var password = $('#passwordInput').val();
			var confirmPassword = $('#confirmPasswordInput').val();
			var firstName = $('#firstNameInput').val();
			var lastName = $('#lastNameInput').val();

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