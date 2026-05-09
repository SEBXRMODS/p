<html lang="es">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Panel Secreto</title>

<style>

body{
background:#000;
color:#00ff88;
font-family:Consolas;
padding:20px;
}

h1{
text-align:center;
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

</style>

</head>
<body>

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

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

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

const db = getFirestore(app);

async function cargar(){

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

document.getElementById("tabla").innerHTML = html;

}

cargar();

</script>

</body>
</html>
