https://yourusername.github.io/techknexfooter{
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
