---
comments: True
layout: post
toc: false
title: Login
permalink: /login
description: Login
type: hacks
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Form</title>
    <style>
        #login {
            margin-top: 10px;
            padding: 0.75rem;
            text-align: center;
            width: 100%;
        }
        .login-container {
            border: 3px solid #39FF14;
            background-color: #171515;
        }

        input[type=text], input[type=password] {
            width: 100%;
            padding: 12px 20px;
            margin: 8px 0;
            display: inline-block;
            border: 1px solid #39FF14;
            box-sizing: border-box;
            background-color: #171515;
            color: #39FF14;
        }

        button {
            background-color: #39FF14;
            color: #171515;
            padding: 14px 20px;
            margin: 8px 0;
            border: none;
            cursor: pointer;
            width: 50%;
            margin-left: 170px;
        }

        button:hover {
            opacity: 0.8;
        }

        .imgcontainer {
            text-align: center;
            margin: 24px 0 12px 0;
        }

        img.avatar {
            width: 40%;
            border-radius: 50%;
        }

        .container {
            padding: 16px;
        }

        span.psw {
            display: flex;
            justify-items: center;
            text-align: center;
            margin-left: 250px;
            padding-top: 16px;
            color: #39FF14;
        }

        @media screen and (max-width: 300px) {
            span.psw {
                display: block;
                float: none;
            }

            .cancelbtn {
                width: 100%;
            }
        }
    </style>
<div class="login-container">
  
<form action="javascript:login_user()">
    <label for="uid"><b>Username</b></label>
    <input type="text" id="uid" placeholder="Enter Username" name="uid" required>
    <label for="password"><b>Password</b></label>
    <input type="password" id="password" placeholder="Enter Password" name="password" required>
    <button class='button'>Log in</button>
    <div>
    <span class="psw">Need an account? <a href="{{site.baseurl}}/signup"> Sign Up</a></span>
    </div>

</form>
<script type="module">
    import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';
    function login_user() {
        var myHeaders = new Headers();
        myHeaders.append("Content-Type", "application/json");
        const url = uri + '/api/users/authenticate';
        const body = {
            uid: document.getElementById("uid").value,
            password: document.getElementById("password").value,
        };
        const authOptions = {
            method: 'POST',
            cache: 'no-cache',
            headers: myHeaders,
            body: JSON.stringify(body)
        };
        fetch(url, authOptions)
        .then(response => {
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                return null;
            }
            const contentType = response.headers.get('Content-Type');
            if (contentType && contentType.includes('application/json')) {
                return response.json();
            } else {
                return response.text();
            }
        })
        .then(data => {
            if (data !== null) {
                console.log('Response:', data);
            }
            // window.location.href = "{{site.baseurl}}/";
        })
        .catch(err => {
            console.error('Fetch error:', err);
        });
    }
    window.login_user = login_user;

</script>