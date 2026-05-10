<!DOCTYPE html>
<html lang="es">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Login Admin</title>

<style>

body{
background:black;
color:#00ff88;
font-family:Consolas;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
margin:0;
}

.login-box{

width:350px;
padding:30px;
border:2px solid #00ff88;
border-radius:15px;
box-shadow:0 0 25px #00ff88;

}

h1{
text-align:center;
margin-bottom:30px;
}

input{

width:100%;
padding:12px;
margin-bottom:15px;
background:black;
border:1px solid #00ff88;
color:#00ff88;
font-size:16px;

}

button{

width:100%;
padding:12px;
background:black;
border:2px solid #00ff88;
color:#00ff88;
font-size:18px;
cursor:pointer;

}

button:hover{

background:#00ff88;
color:black;

}

#error{

margin-top:15px;
color:red;
text-align:center;

}

</style>

</head>
<body>

<div class="login-box">

<h1>LOGIN ADMIN</h1>

<input type="email" id="email" placeholder="Correo">

<input type="password" id="password" placeholder="Contraseña">

<button onclick="login()">ENTRAR</button>

<p id="error"></p>

</div>

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

import {
getAuth,
signInWithEmailAndPassword
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

const firebaseConfig = {

apiKey: "AIzaSyC8cF8i86iqxCUIlOw1ykd_Civxl1qX2FM",
authDomain: "osting-1b3f6.firebaseapp.com",
projectId: "osting-1b3f6",
storageBucket: "osting-1b3f6.firebasestorage.app",
messagingSenderId: "1080144262727",
appId: "1:1080144262727:web:3f42a97c334adb826b2362"

};

const app = initializeApp(firebaseConfig);

const auth = getAuth(app);

window.login = async function(){

const email =
document.getElementById("email").value;

const password =
document.getElementById("password").value;

try{

await signInWithEmailAndPassword(
auth,
email,
password
);

// CAMBIA ESTA URL POR TU PANEL

window.location.href =
"https://TUUSUARIO.github.io/TUREPO/panel.html";

}catch(err){

document.getElementById("error").innerHTML =
"Correo o contraseña incorrectos";

}

}

</script>

</body>
</html>
