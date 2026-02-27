let userId=localStorage.getItem("userId")

async function register(){

let email=document.getElementById("email").value
let password=document.getElementById("password").value

await fetch("/api/register",{

method:"POST",
headers:{
"Content-Type":"application/json"
},
body:JSON.stringify({email,password})

})

alert("Account created")

}

async function login(){

let email=document.getElementById("email").value
let password=document.getElementById("password").value

let res=await fetch("/api/login",{

method:"POST",
headers:{
"Content-Type":"application/json"
},
body:JSON.stringify({email,password})

})

let data=await res.json()

localStorage.setItem("userId",data.id)

window.location="dashboard.html"

}

async function deposit(){

let amount=document.getElementById("amount").value

let res=await fetch("/api/deposit",{

method:"POST",
headers:{
"Content-Type":"application/json"
},
body:JSON.stringify({
userId:Number(localStorage.getItem("userId")),
amount:Number(amount)
})

})

let data=await res.json()

document.getElementById("balance").innerText=
"Balance: $"+data.balance

}<!DOCTYPE html>
<html>

<head>
<title>Dashboard</title>
<link rel="stylesheet" href="style.css">
</head>

<body>

<h1>Dashboard</h1>

<p id="balance">Balance: $0</p>

<input id="amount" placeholder="Deposit amount">

<p>Processing fee required before deposit</p>

<button onclick="deposit()">Deposit</button>

<script src="main.js"></script>

</body>
</html><!DOCTYPE html>
<html>

<head>
<title>Register</title>
<link rel="stylesheet" href="style.css">
</head>

<body>

<h2>Create Account</h2>

<input id="email" placeholder="Email">
<input id="password" type="password" placeholder="Password">

<button onclick="register()">Register</button>

<script src="main.js"></script>

</body>
</html><!DOCTYPE html>
<html>

<head>
<title>Login</title>
<link rel="stylesheet" href="style.css">
</head>

<body>

<h2>Login</h2>

<input id="email" placeholder="Email">
<input id="password" type="password" placeholder="Password">

<button onclick="login()">Login</button>

<script src="main.js"></script>

</body>
</html><!DOCTYPE html>
<html>

<head>

<title>Tech Knex</title>

<link rel="stylesheet" href="style.css">

</head>

<body>

<header>

<h1>TECH KNEX</h1>

<nav>

<a href="login.html">Login</a>
<a href="register.html">Register</a>

</nav>

</header>

<section class="hero">

<h2>Innovation Through Electronics</h2>

<p>Robotics • AI • Electronics Engineering</p>

<a href="register.html">
<button>Join Platform</button>
</a>

</section>

<button class="aiBtn" onclick="openAI()">AI Assistant</button>

<div id="aiBox" class="aiBox">

<h3>Tech Knex AI</h3>

<input id="aiInput" placeholder="Ask something">

<button onclick="askAI()">Send</button>

<p id="aiResponse"></p>

</div>

<script src="ai.js"></script>

</body>
</html>{
"users":[]
}const express = require("express")
const bodyParser = require("body-parser")
const fs = require("fs")

const app = express()

app.use(bodyParser.json())
app.use(express.static("public"))

const DB = "./database/db.json"

function readDB(){
return JSON.parse(fs.readFileSync(DB))
}

function writeDB(data){
fs.writeFileSync(DB, JSON.stringify(data,null,2))
}

/* Register */

app.post("/api/register",(req,res)=>{

let db = readDB()

let user={
id:Date.now(),
email:req.body.email,
password:req.body.password,
balance:0
}

db.users.push(user)

writeDB(db)

res.json({message:"registered"})
})

/* Login */

app.post("/api/login",(req,res)=>{

let db = readDB()

let user=db.users.find(u=>
u.email===req.body.email &&
u.password===req.body.password
)

if(!user){
return res.status(401).json({message:"invalid"})
}

res.json(user)

})

/* Deposit */

app.post("/api/deposit",(req,res)=>{

let db=readDB()

let user=db.users.find(u=>u.id===req.body.userId)

if(!user){
return res.status(404).json({})
}

user.balance+=req.body.amount

writeDB(db)

res.json({balance:user.balance})

})

app.listen(3000,()=>{

console.log("Tech Knex V4 running")

})tech-knex-v4

server.js
package.json

/database
   db.json

/public
   index.html
   login.html
   register.html
   dashboard.html
   style.css
   main.js
   ai.js<!DOCTYPE html>
<html>

<head>

<title>Tech Knex Dashboard</title>

<style>

body{
font-family:-apple-system;
background:#0b0b0b;
color:white;
text-align:center;
padding:60px;
}

.card{
background:#111;
padding:30px;
margin:20px auto;
width:350px;
border-radius:12px;
}

button{
padding:12px 25px;
background:#22c55e;
border:none;
color:white;
border-radius:8px;
cursor:pointer;
}

input{
padding:10px;
margin:10px;
border:none;
border-radius:8px;
}

</style>

</head>

<body>

<h1>Welcome to Tech Knex</h1>

<div class="card">

<h3>Activation Fee</h3>

<p>Pay $2 to activate deposits</p>

<button onclick="pay()">Pay Fee</button>

</div>

<div class="card" id="depositArea" style="display:none">

<h3>Deposit Money</h3>

<input id="amount" type="number" placeholder="Enter amount">

<button onclick="deposit()">Deposit</button>

</div>

<div class="card">

<h2 id="balance">Balance: $0</h2>

</div>

<script>

let balance=0

function pay(){

alert("Processing payment...")

setTimeout(()=>{

alert("Activation successful")

document.getElementById("depositArea").style.display="block"

},2000)

}

function deposit(){

let amount=parseFloat(document.getElementById("amount").value)

if(!amount) return

balance+=amount

document.getElementById("balance").innerText="Balance: $"+balance

}

</script>

</body>

</html><!DOCTYPE html>
<html>
<head>

<title>Tech Knex</title>

<style>

body{
font-family: -apple-system, BlinkMacSystemFont, sans-serif;
background:#000;
color:white;
text-align:center;
padding-top:120px;
}

.container{
background:#111;
padding:40px;
width:320px;
margin:auto;
border-radius:12px;
box-shadow:0 0 20px rgba(255,255,255,0.1);
}

input{
width:90%;
padding:12px;
margin:10px;
border:none;
border-radius:8px;
}

button{
padding:12px 25px;
background:#0071e3;
border:none;
color:white;
border-radius:8px;
cursor:pointer;
}

button:hover{
background:#005bb5;
}

</style>

</head>

<body>

<div class="container">

<h1>Tech Knex</h1>

<h3>Login</h3>

<input id="user" placeholder="Username">

<input id="pass" type="password" placeholder="Password">

<button onclick="login()">Login</button>

</div>

<script>

function login(){

let user=document.getElementById("user").value
let pass=document.getElementById("pass").value

if(user && pass){

localStorage.setItem("user",user)
window.location="dashboard.html"

}else{

alert("Enter login details")

}

}

</script>

</body>
</html><!DOCTYPE html>
<html>
<head>
<title>Tech Knex - Login</title>

<style>

body{
font-family: Arial;
background:#0f172a;
color:white;
text-align:center;
padding-top:100px;
}

input{
padding:10px;
margin:10px;
width:200px;
}

button{
padding:10px 20px;
background:#3b82f6;
color:white;
border:none;
cursor:pointer;
}

</style>

</head>

<body>

<h1>Tech Knex</h1>

<h2>Login</h2>

<input type="text" id="username" placeholder="Username"><br>

<input type="password" id="password" placeholder="Password"><br>

<button onclick="login()">Login</button>

<p id="message"></p>

<script>

function login(){

let user = document.getElementById("username").value
let pass = document.getElementById("password").value

if(user && pass){

localStorage.setItem("loggedIn", true)

window.location.href = "dashboard.html"

}else{

document.getElementById("message").innerHTML = "Enter username and password"

}

}

</script>

</body>
</html>https://yourusername.github.io/techknexlet balance = 0;

function deposit(){

let amount = Number(document.getElementById("depositAmount").value);

balance += amount;

document.getElementById("balance").innerText = "$" + balance;

}

function withdraw(){

let amount = Number(document.getElementById("withdrawAmount").value);

if(amount <= balance){

balance -= amount;

document.getElementById("balance").innerText = "$" + balance;

}else{

alert("Insufficient balance");

}

}

function calculate(){

let amount = document.getElementById("amount").value;

let starter = amount * 1.10;
let growth = amount * 1.25;
let premium = amount * 1.40;

document.getElementById("starter").innerText = "$" + starter;
document.getElementById("growth").innerText = "$" + growth;
document.getElementById("premium").innerText = "$" + premium;

}body{
font-family:Arial;
margin:0;
background:#0f172a;
color:white;
}

header{
display:flex;
justify-content:space-between;
padding:20px;
background:#020617;
}

nav a{
margin:10px;
color:white;
text-decoration:none;
}

.hero{
text-align:center;
padding:120px;
}

button{
padding:12px 25px;
background:#3b82f6;
border:none;
color:white;
border-radius:6px;
cursor:pointer;
}

.plans{
display:flex;
justify-content:center;
gap:20px;
padding:40px;
}

.card{
background:#1e293b;
padding:20px;
border-radius:10px;
width:200px;
text-align:center;
}

.calculator{
text-align:center;
padding:40px;
}

input{
padding:10px;
margin:10px;
border-radius:5px;
border:none;
}

.dashboard{
text-align:center;
padding:60px;
}

footer{
text-align:center;
padding:20px;
background:#020617;
}<!DOCTYPE html>
<html>

<head>
<title>Dashboard</title>
<link rel="stylesheet" href="style.css">
</head>

<body>

<header>
<h2>Tech Knex Dashboard</h2>
</header>

<section class="dashboard">

<h3>Your Balance</h3>

<h1 id="balance">$0</h1>

<input id="depositAmount" placeholder="Deposit amount">

<button onclick="deposit()">Deposit</button>

<input id="withdrawAmount" placeholder="Withdraw amount">

<button onclick="withdraw()">Withdraw</button>

</section>

<script src="app.js"></script>

</body>

</html><!DOCTYPE html>
<html lang="en">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tech Knex</title>
<link rel="stylesheet" href="style.css">
</head>

<body>

<header>

<h1>Tech Knex</h1>

<nav>
<a href="#">Home</a>
<a href="#plans">Plans</a>
<a href="#calculator">Calculator</a>
<a href="dashboard.html">Dashboard</a>
</nav>

</header>


<section class="hero">

<h2>Smart Digital Finance Platform</h2>

<p>Manage deposits and track potential growth.</p>

<button onclick="location.href='dashboard.html'">
Open Dashboard
</button>

</section>


<section id="plans" class="plans">

<h2>Plans</h2>

<div class="card">
<h3>Starter</h3>
<p>10% estimate</p>
<p>7 days</p>
</div>

<div class="card">
<h3>Growth</h3>
<p>25% estimate</p>
<p>30 days</p>
</div>

<div class="card">
<h3>Premium</h3>
<p>40% estimate</p>
<p>90 days</p>
</div>

</section>


<section id="calculator" class="calculator">

<h2>Return Calculator</h2>

<input id="amount" placeholder="Enter amount">

<button onclick="calculate()">Calculate</button>

<p>Starter: <span id="starter"></span></p>
<p>Growth: <span id="growth"></span></p>
<p>Premium: <span id="premium"></span></p>

</section>


<footer>

<p>Contact: 0799812274</p>
<p>© 2026 Tech Knex</p>

</footer>

<script src="app.js"></script>

</body>
</html>https://yourusername.github.io/techknexfooter{
margin-top:80px;
padding:20px;
background:#020617;
}<!DOCTYPE html>
<html>
<head>
<title>Contact</title>
<link rel="stylesheet" href="style.css">
</head>

<body>

<h1>Contact Tech Knex</h1>

<p>Phone: 0799812274</p>
<p>Email: techknex@email.com</p>

<a class="button" href="tel:0799812274">Call Us</a>

<input type="text" placeholder="Your Name">
<input type="email" placeholder="Email">
<textarea placeholder="Message"></textarea>

<button>Send</button>

<footer>

<p>Tech Knex © 2026</p>
<p>Phone: 0799812274</p>

</footer>

</body>
</html><!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Tech Knex</title>
<link rel="stylesheet" href="style.css">
</head>

<body>

<nav>
<h2>Tech Knex</h2>

<div class="links">
<a href="index.html">Home</a>
<a href="about.html">About</a>
<a href="services.html">Services</a>
<a href="invest.html">Invest</a>
<a href="contact.html">Contact</a>
<a href="login.html">Login</a>
</div>

</nav>

<section class="hero">

<h1>Innovation Through Electronics</h1>
<p>Electronics sales, repairs, and smart investments.</p>

<a class="button" href="invest.html">Start Investing</a>

<p>Call us: 0799812274</p>

<a class="button" href="tel:0799812274">Call Now</a>

</section>

<footer>

<p>Tech Knex © 2026</p>
<p>Phone: 0799812274</p>

</footer>

</body>
</html><!DOCTYPE html>
<html lang="en">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Tech Knex | Innovation Through Electronics</title>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
}

body{
font-family: Arial, Helvetica, sans-serif;
background:#0f172a;
color:white;
line-height:1.6;
}

header{
background:#020617;
padding:20px;
text-align:center;
border-bottom:2px solid #38bdf8;
}

header h1{
color:#38bdf8;
margin-bottom:5px;
}

nav{
margin-top:10px;
}

nav a{
color:white;
text-decoration:none;
margin:0 12px;
font-weight:bold;
}

nav a:hover{
color:#38bdf8;
}

.hero{
padding:80px 20px;
text-align:center;
background:linear-gradient(90deg,#0f172a,#1e293b);
}

.hero h2{
font-size:40px;
margin-bottom:10px;
}

.section{
padding:60px 20px;
max-width:1000px;
margin:auto;
}

.services{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:20px;
margin-top:30px;
}

.card{
background:#1e293b;
padding:20px;
border-radius:10px;
border:1px solid #38bdf8;
transition:0.3s;
}

.card:hover{
transform:translateY(-5px);
}

button{
background:#38bdf8;
border:none;
padding:12px 20px;
border-radius:6px;
font-weight:bold;
cursor:pointer;
margin-top:10px;
}

button:hover{
background:#0ea5e9;
}

footer{
background:#020617;
text-align:center;
padding:20px;
margin-top:40px;
}

</style>
</head>

<body>

<header>

<h1>Tech Knex</h1>
<p>Innovation Through Electronics</p>

<nav>
<a href="#home">Home</a>
<a href="#about">About</a>
<a href="#services">Services</a>
<a href="#contact">Contact</a>
</nav>

</header>


<section class="hero" id="home">

<h2>Welcome to Tech Knex</h2>

<p>
We sell electronic gadgets, repair devices and build innovative electronics solutions.
</p>

<button onclick="scrollToContact()">Contact Us</button>

</section>


<section class="section" id="about">

<h2>About Us</h2>

<p>
Tech Knex is a technology company focused on electronics innovation,
device repair and providing modern electronic gadgets.
Our mission is to bring smart technology solutions to everyone.
</p>

</section>


<section class="section" id="services">

<h2>Our Services</h2>

<div class="services">

<div class="card">
<h3>Electronic Gadgets</h3>
<p>We sell phones, accessories and modern smart devices.</p>
</div>

<div class="card">
<h3>Device Repair</h3>
<p>Professional repair for phones, laptops and other electronics.</p>
</div>

<div class="card">
<h3>Electronics Innovation</h3>
<p>We design and build robotics and new electronic solutions.</p>
</div>

</div>

</section>


<section class="section" id="contact">

<h2>Contact Us</h2>

<p>Email: techknex@email.com</p>
<p>Phone: +254 0799812274</p>

<button onclick="sendMessage()">Send Message</button>

</section>


<footer>

<p>© 2026 Tech Knex. All Rights Reserved.</p>

</footer>


<script>

function scrollToContact(){
document.getElementById("contact").scrollIntoView({
behavior:"smooth"
});
}

function sendMessage(){
alert("Thank you for contacting Tech Knex!");
}

</script>

</body>
</html># Tech-knex
Readme
