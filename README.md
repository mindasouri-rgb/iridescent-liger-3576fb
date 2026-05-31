HTML
<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>السلة</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<header>
🛒 سلة التسوق
<a href="index.html">🏠 العودة</a>
</header>

<div id="cart"></div>

<script src="app.js"></script>
</body>
</html>
🎨 4) style.css (التصميم)
CSS
body {
margin: 0;
font-family: Arial;
background: #f5f5f5;
}

header {
background: #111;
color: white;
padding: 15px;
display: flex;
justify-content: space-between;
align-items: center;
}

a {
color: white;
text-decoration: none;
}

.hero {
text-align: center;
padding: 20px;
}

.grid {
display: grid;
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
gap: 15px;
padding: 20px;
}

.card {
background: white;
padding: 10px;
border-radius: 10px;
text-align: center;
}

button {
width: 100%;
padding: 10px;
background: #ffcc00;
border: none;
border-radius: 8px;
cursor: pointer;
}

img {
width: 100%;
border-radius: 10px;
}
⚙️ 5) app.js (المنطق + السلة)
JavaScript
const products = [
{
id: 1,
title: "نظارات شمسية أسود",
price: 2500,
image: "https://images.unsplash.com/photo-1511499767150-a48a237f0083"
},
{
id: 2,
title: "نظارات رياضية",
price: 3000,
image: "https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f"
},
{
id: 3,
title: "نظارات فخمة",
price: 4500,
image: "https://images.unsplash.com/photo-1518709268805-4e9042af9f23"
}
];

// إضافة للسلة
function addToCart(id) {
let cart = JSON.parse(localStorage.getItem("cart")) || [];
cart.push(id);
localStorage.setItem("cart", JSON.stringify(cart));
alert("تمت الإضافة 🛒");
}

// عرض المنتجات
if (document.getElementById("products")) {
const container = document.getElementById("products");

products.forEach(p => {
container.innerHTML += &lt;div class="card"&gt; &lt;img src="${p.image}">
<h3>${p.title}&lt;/h3&gt; &lt;p&gt;${p.price} دج</p>
<button onclick="addToCart(${p.id})"&gt;أضف للسلة&lt;/button&gt; &lt;/div&gt;;
});
}

// عرض السلة
if (document.getElementById("cart")) {
const container = document.getElementById("cart");
let cart = JSON.parse(localStorage.getItem("cart")) || [];

let total = 0;

cart.forEach(id => {
const p = products.find(x => x.id === id);
if (!p) return;

total += p.price;

container.innerHTML += &lt;div class="card"&gt; &lt;h3&gt;${p.title}</h3>
<p>${p.price} دج&lt;/p&gt; &lt;/div&gt;;
});

container.innerHTML += &lt;h2&gt;المجموع: ${total} دج&lt;/h2&gt; &lt;button onclick="alert('سيتم تأكيد الطلب (COD)')"&gt;إتمام الطلب&lt;/button&gt;;
}
