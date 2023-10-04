<script>
    import { redirect } from "@sveltejs/kit";
	import { sha256, sha224 } from "js-sha256";
	import { onMount } from "svelte";
    import { object_without_properties } from "svelte/internal";

	const User = {
		firstName: "",
		lastName: "",
		email: "",
		password: "",
	};

	onMount(() => {
		document
			.getElementById("signin")
			.addEventListener("submit", function (e) {
				e.preventDefault();

				getData(e.target);
				e.target.reset();
			});
	});

	function getData(form) {
		var formData = new FormData(form);

		console.log(formData.entries());
		for (var [key, value] of formData.entries()) {
			if (User.hasOwnProperty(key)) {
				User[key] = encryptValues(value);
			}
		}

		console.log(User);
	}

	function encryptValues(value) {
		return value != undefined ? sha256(value) : value;
	}
</script>

<html lang="en">
	<body>
		<div>
			<form class="form-style-7" name="signin" id="signin" method="post">
				<ul>
					<li>
						<label for="firstName">First name </label>
						<input
							required
							name="firstName"
							value=""
							id="firstName"
							type="text"
							maxlength="100"
						/>
						<span>Enter your first name here</span>
					</li>
					<li>
						<label for="lastName">Last name </label>
						<input
							required
							name="lastName"
							value=""
							id="lastName"
							type="text"
							maxlength="100"
						/>
						<span>Enter your last name here</span>
					</li>
					<li>
						<label for="email">Email </label>
						<input
							required
							name="email"
							value=""
							id="email"
							type="email"
							maxlength="100"
						/>
						<span>Enter a valid email</span>
					</li>
					<li>
						<label for="password">Password </label>
						<input
							required
							name="password"
							value=""
							id="password"
							type="password"
							maxlength="100"
						/>
						<span>Enter password </span>
					</li>
					<li>
						<input type="submit" value="Sign up">
					</li>
				</ul>	
			</form>

			<div class="redirect-button">
				<span>Already have an account?</span>
				<br>
				<a style="text-decoration: aqua;" href="/login">Log in</a>
			</div>
			
		</div>
	</body>

	<link
		href="http://fonts.googleapis.com/css?family=Open+Sans+Condensed:300"
		rel="stylesheet"
		type="text/css"
	/>
	<style type="text/css">
		.form-style-7 {
			display: grid;
			width: 60vw;
			max-width: 400px;
			min-width: 300px;
			margin: 50px auto;
			padding: 20px;
			font-family: Georgia, "Times New Roman", Times, serif;
			border-radius: 2px;
			background: #fff;
		}

		.form-style-7 h1 {
			display: block;
			text-align: center;
			padding: 0;
			margin: 0px 0px 20px 0px;
			color: #5c5c5c;
			font-size: x-large;
		}
		.form-style-7 ul{
			list-style: none;
			padding: 0;
			margin: 0;
		}

		.form-style-7 li{
			display: block;
			padding: 9px;
			border:1.5px solid #DDDDDD;
			margin-bottom: 30px;
			border-radius: 3px;
		}

		.form-style-7 li:last-child{
			border: none;
			height: 100%;
			margin-bottom:0px;
			text-align: center;

		}

		.form-style-7 li > label{
			display: block;
			float: left;
			margin-top: -15px;
			background: #FFFFFF;
			height: 14px;
			padding: 2px 5px 2px 5px;
			color: #B9B9B9;
			font-size: 13px;
			overflow: hidden;
			font-family: Arial, Helvetica, sans-serif;
		}
		.form-style-7 input[type="text"],
		.form-style-7 input[type="date"],
		.form-style-7 input[type="datetime"],
		.form-style-7 input[type="email"],
		.form-style-7 input[type="number"],
		.form-style-7 input[type="search"],
		.form-style-7 input[type="time"],
		.form-style-7 input[type="url"],
		.form-style-7 input[type="password"],
		.form-style-7 textarea,
		.form-style-7 select 
		{
			background: white;
			box-sizing: border-box;
			-webkit-box-sizing: border-box;
			-moz-box-sizing: border-box;
			width: 100%;
			display: block;
			outline: none;
			border: none;
			height: 25px;
			line-height: 25px;
			font-size: 15px;
			padding: 0;
			color: #6b6964;
			font-family: Arial, Helvetica, sans-serif;
		}
		.form-style-7 input[type="text"]:focus,
		.form-style-7 input[type="date"]:focus,
		.form-style-7 input[type="datetime"]:focus,
		.form-style-7 input[type="email"]:focus,
		.form-style-7 input[type="number"]:focus,
		.form-style-7 input[type="search"]:focus,
		.form-style-7 input[type="time"]:focus,
		.form-style-7 input[type="url"]:focus,
		.form-style-7 input[type="password"]:focus,
		.form-style-7 textarea:focus,
		.form-style-7 select:focus 
		{
		}
		.form-style-7 li > span{
			background-image: linear-gradient(white,#F3F3F3) ;
			display: block;
			padding: 4px;
			margin: 0 -9px -10px -9px;
			text-align: center;
			color: #C0C0C0;
			font-family: Arial, Helvetica, sans-serif;
			font-size: 11px;
		}

		.form-style-7 input[type="submit"],
		.form-style-7 input[type="button"]{
			background: #2471FF;
			/* margin: 0px 150px auto; */
			border: none;
			padding: 10px 20px 10px 20px;
			border-bottom: 3px solid #5994FF;
			border-radius: 3px;

			color: #D2E2FF;
		}
		.form-style-7 input[type="submit"]:hover,
		.form-style-7 input[type="button"]:hover{
			background: #6B9FFF;
			color:#fff;
		}

		.redirect-button{
			font-family: Arial, Helvetica, sans-serif;
			font-size: 15px;
			display: block;
			background-color: transparent;
			text-align: center;
			margin: auto ;
			border:none;
			outline:none;
			width: 300px;
			position: relative;
			top: -50px;


			
		}

		
	</style>
</html>
