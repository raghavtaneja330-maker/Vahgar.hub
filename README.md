<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vahgar hub</title>

<style>
:root{
  --primary:#111;
  --accent:#ff4d4d;
  --light:#f4f4f4;
}

*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family: 'Segoe UI', sans-serif;
}

body{
  background:#fff;
  color:#222;
}

/* HERO SECTION */
.hero{
  height:100vh;
  background:url("https://images.unsplash.com/photo-1521334884684-d80222895322?q=80&w=1600&auto=format&fit=crop") center/cover no-repeat;
  display:flex;
  align-items:center;
  justify-content:center;
  text-align:center;
  color:#fff;
  position:relative;
}

.hero::after{
  content:"";
  position:absolute;
  inset:0;
  background:rgba(0,0,0,0.6);
}

.hero-content{
  position:relative;
  z-index:2;
}

.hero h1{
  font-size:2.8rem;
  letter-spacing:2px;
}

.hero p{
  margin:15px 0;
  font-size:1.1rem;
}

.btn{
  padding:12px 28px;
  background:var(--accent);
  color:#fff;
  border:none;
  border-radius:30px;
  cursor:pointer;
  transition:0.3s;
  font-weight:bold;
}

.btn:hover{
  background:#e60000;
}

/* PRODUCTS */
.products{
  padding:40px 20px;
  background:var(--light);
}

.products h2{
  text-align:center;
  margin-bottom:30px;
  font-size:2rem;
}

.product-card{
  background:#fff;
  border-radius:12px;
  padding:15px;
  margin-bottom:25px;
  box-shadow:0 10px 25px rgba(0,0,0,0.08);
}

.product-card img{
  width:100%;
  border-radius:10px;
}

.product-info{
  margin-top:15px;
}

.product-info h3{
  font-size:1.3rem;
}

.price{
  color:var(--accent);
  font-weight:bold;
  margin:10px 0;
  font-size:1.1rem;
}

.select-group{
  display:flex;
  gap:10px;
  margin-bottom:10px;
}

select, input[type="number"]{
  padding:8px;
  border:1px solid #ccc;
  border-radius:6px;
  width:100%;
}

/* FLOATING CART */
.cart-icon{
  position:fixed;
  bottom:20px;
  right:20px;
  background:var(--accent);
  color:#fff;
  padding:15px;
  border-radius:50%;
  cursor:pointer;
  font-weight:bold;
  box-shadow:0 5px 15px rgba(0,0,0,0.3);
}

/* CART PANEL */
.cart{
  position:fixed;
  right:-100%;
  top:0;
  height:100%;
  width:100%;
  max-width:400px;
  background:#fff;
  box-shadow:-5px 0 20px rgba(0,0,0,0.2);
  padding:20px;
  transition:0.4s;
  overflow-y:auto;
}

.cart.active{
  right:0;
}

.cart h3{
  margin-bottom:15px;
}

.cart-item{
  display:flex;
  justify-content:space-between;
  margin-bottom:8px;
}

.total{
  font-weight:bold;
  margin:15px 0;
}

form input{
  width:100%;
  padding:10px;
  margin-bottom:10px;
  border-radius:6px;
  border:1px solid #ddd;
}

footer{
  text-align:center;
  padding:15px;
  background:#111;
  color:#fff;
}
</style>
</head>

<body>

<!-- HERO -->
<section class="hero">
  <div class="hero-content">
    <h1>vahgar hub</h1>
    <p>fresh find, best prices, fashion</p>
    <button class="btn" onclick="scrollToProducts()">Shop Now</button>
  </div>
</section>

<!-- PRODUCTS -->
<section class="products" id="products">
  <h2>Japanese Pant Collection</h2>

  <div class="product-card">
    <img src="https://i.imgur.com/8Km9tLL.jpg" alt="Japanese Pant">
    <div class="product-info">
      <h3>Japanese Pant</h3>
      <p class="price">₹490</p>

      <div class="select-group">
        <select id="color">
          <option value="Black">Black</option>
          <option value="Brown">Brown</option>
          <option value="Beige">Beige</option>
          <option value="Grey">Grey</option>
        </select>

        <input type="number" id="qty" value="1" min="1">
      </div>

      <button class="btn" onclick="addToCart()">Add to Cart</button>
    </div>
  </div>
</section>

<!-- FLOATING CART -->
<div class="cart-icon" onclick="toggleCart()">
🛒
</div>

<!-- CART -->
<div class="cart" id="cartPanel">
  <h3>Your Cart</h3>
  <div id="cart-items"></div>
  <div class="total">Total: ₹<span id="total">0</span></div>

  <form onsubmit="placeOrder(event)">
    <input type="text" id="name" placeholder="Customer Name" required>
    <input type="tel" id="mobile" placeholder="Mobile Number" required>
    <button type="submit" class="btn">Order via Email</button>
  </form>

  <button class="btn" style="margin-top:10px;background:#25D366" onclick="orderWhatsApp()">Order via WhatsApp</button>
</div>

<footer>
Contact: raghav.taneja330@gmail.com
</footer>

<script>
let cart=[];

function scrollToProducts(){
  document.getElementById("products").scrollIntoView({behavior:"smooth"});
}

function toggleCart(){
  document.getElementById("cartPanel").classList.toggle("active");
}

function addToCart(){
  let color=document.getElementById("color").value;
  let qty=parseInt(document.getElementById("qty").value);
  let price=490;
  cart.push({name:"Japanese Pant",color,qty,price});
  renderCart();
  toggleCart();
}

function renderCart(){
  let div=document.getElementById("cart-items");
  div.innerHTML="";
  let total=0;

  cart.forEach(item=>{
    let itemTotal=item.price*item.qty;
    total+=itemTotal;
    div.innerHTML+=`
      <div class="cart-item">
        <span>${item.name} (${item.color}) x${item.qty}</span>
        <span>₹${itemTotal}</span>
      </div>
    `;
  });

  document.getElementById("total").innerText=total;
}

function placeOrder(e){
  e.preventDefault();
  let name=document.getElementById("name").value;
  let mobile=document.getElementById("mobile").value;
  let total=document.getElementById("total").innerText;

  if(cart.length===0){
    alert("Cart is empty!");
    return;
  }

  let items=cart.map(i=>`${i.name} (${i.color}) x${i.qty} - ₹${i.price*i.qty}`).join("%0D%0A");

  let mailto=`mailto:raghav.taneja330@gmail.com?subject=New Order from vahgar hub&body=Customer Name: ${name}%0D%0AMobile: ${mobile}%0D%0A%0AItems:%0D%0A${items}%0D%0A%0ATotal: ₹${total}`;
  window.location.href=mailto;
}

function orderWhatsApp(){
  let total=document.getElementById("total").innerText;
  if(cart.length===0){
    alert("Cart is empty!");
    return;
  }

  let items=cart.map(i=>`${i.name} (${i.color}) x${i.qty} - ₹${i.price*i.qty}`).join("%0A");

  let message=`New Order from vahgar hub%0A%0A${items}%0A%0ATotal: ₹${total}`;
  window.open(`https://wa.me/91YOURNUMBER?text=${message}`,"_blank");
}
</script>

</body>
</html># Vahgar.hub
