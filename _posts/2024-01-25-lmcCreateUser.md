---
comments: True
layout: post
title: Create User
description: cooking
courses: { csp: {week: 20} }
type: hacks
permalink: /lmc-createUser
---
<style>

</style>
<!-- 
A simple HTML login form with a Login action when button is pressed.  

The form triggers the login_user function defined in the JavaScript below when the Login button is pressed.
-->
<link rel="stylesheet" href="/lmc-frontend/LMC/JS/SCSS/lmcLogin.css">
<div id="titleContainer">
    <h1 id="title">Let-M-Cook</h1>
</div>

<div class="background">

</div>

<div class="container">
    <form id="username" action="javascript:login_user()">
        <label>
            Name:
            <input class="userInput" type="text" name="name" id="name" required>
        </label>
        </p>
        <p><label>
            User ID:
            <input class="userInput" type="text" name="uid" id="uid" required>
        </label></p>
        <p ><label>
            Password:
            <input class="userInput" type="password" name="password" id="password" required>
        </label></p>
        <p><label>
            Date of Birth:
            <input class="userInput" type="text" id="dob" required>
        </label></p>
		<p><label>
			Favorite Food:
			<input class="userInput" type="text" id="food" required>
		</label></p>
        <p>
            <button onclick="login_user()">Submit</button>
        </p>
    </form>
</div>


<!-- 
Below JavaScript code is designed to handle user authentication in a web application. It's written to work with a backend server that uses JWT (JSON Web Tokens) for authentication.

The script defines a function when the page loads. This function is triggered when the Login button in the HTML form above is pressed. 
 -->
<script type="module">
    // uri variable and options object are obtained from config.js
    import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';
    const url = uri + '/api/users/authenticate';
    const body = {
            // name: document.getElementById("name").value,
            uid: "toby",
            password: "123toby"
            // dob: document.getElementById("dob").value
        };
    const authOptions = {
            ...options, // This will copy all properties from options
            method: 'POST', // Override the method property
            cache: 'no-cache', // Set the cache property
            body: JSON.stringify(body)
        };
    fetch(url, authOptions)
    function login_user(){
        // Set Authenticate endpoint
        const url = uri + '/api/users/';

        // Set the body of the request to include login data from the DOM
        const body = {
            name: document.getElementById("name").value,
            uid: document.getElementById("uid").value,
            password: document.getElementById("password").value,
            dob: document.getElementById("dob").value,
			fav_food: document.getElementById("food").value
        };

        // Change options according to Authentication requirements
        const authOptions = {
            ...options, // This will copy all properties from options
            method: 'POST', // Override the method property
            cache: 'no-cache', // Set the cache property
            body: JSON.stringify(body)
        };

        // Fetch JWT
        fetch(url, authOptions)
        .then(response => {
            // handle error response from Web API
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                return;
            }
            // Success!!!
            // Redirect to the database page
            window.location.href = "{{site.baseurl}}/data/database";
        })
        // catch fetch errors (ie ACCESS to server blocked)
        .catch(err => {
            console.error(err);
        });
    }

    // Attach login_user to the window object, allowing access to form action
    window.login_user = login_user;
</script>