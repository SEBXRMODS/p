<html lang="es">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Panel de Visitas</title>

<style>

body{
background:black;
color:#00ff88;
font-family:Consolas;
padding:20px;
}

h1{
text-align:center;
font-size:40px;
text-shadow:0 0 15px #00ff88;
}

table{
width:100%;
border-collapse:collapse;
margin-top:20px;
}

th,td{
border:1px solid #00ff88;
padding:10px;
text-align:center;
}

tr:hover{
background:#001a11;
}

.login{
max-width:400px;
margin:auto;
border:2px solid #00ff88;
padding:25px;
border-radius:15px;
box-shadow:0 0 20px #00ff88;
margin-top:100px;
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
color:red;
text-align:center;
margin-top:10px;
}

#panel{
display:none;
}

</style>

</head>
<body>

<!-- LOGIN -->

<div class="login" id="loginBox">

<h1>LOGIN ADMIN</h1>

<input type="email" id="email" placeholder="Correo">

<input type="password" id="password" placeholder="Contraseña">

<button onclick="login()">ENTRAR</button>

<p id="error"></p>

</div>

<!-- PANEL -->

<div id="panel">

<h1>PANEL DE VISITAS</h1>

<table>

<thead>

<tr>
<th>IP</th>
<th>País</th>
<th>Ciudad</th>
<th>Dispositivo</th>
<th>Hora</th>
</tr>

</thead>

<tbody id="tabla"></tbody>

</table>

</div>

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

import {
getAuth,
signInWithEmailAndPassword,
onAuthStateChanged
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

import {
getFirestore,
collection,
getDocs
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

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

const db = getFirestore(app);

// LOGIN

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

}catch(err){

document.getElementById("error").innerHTML =
"Correo o contraseña incorrectos";

}

}

// VERIFICAR LOGIN

onAuthStateChanged(auth, (user)=>{

if(user){

document.getElementById("loginBox").style.display =
"none";

document.getElementById("panel").style.display =
"block";

cargarVisitas();

}

});

// CARGAR VISITAS

async function cargarVisitas(){

const querySnapshot =
await getDocs(collection(db,"visitas"));

let html = "";

querySnapshot.forEach((doc)=>{

const d = doc.data();

html += `

<tr>
<td>${d.ip}</td>
<td>${d.pais}</td>
<td>${d.ciudad}</td>
<td>${d.device}</td>
<td>${d.hora}</td>
</tr>

`;

});

document.getElementById("tabla").innerHTML =
html;

}

</script>

</body>
</html>
