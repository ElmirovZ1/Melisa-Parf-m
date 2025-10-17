# Melisa-Parf-m
Parfüm satış mağazası.
<!DOCTYPE html>
<html lang="az">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Melisa Parfüm</title>
<style>
/* Ümumi stil */
body {
    margin:0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(to bottom, #fdfdfd, #e6e6e6);
    color: #333;
}
header {
    text-align:center;
    padding:50px 20px;
    background: linear-gradient(135deg, #f0f0f0, #dcdcdc);
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}
header h1 {
    font-size:3rem;
    color:#555;
    font-family:'Georgia', serif;
}
header p {
    font-size:1.5rem;
    color:#777;
    font-style:italic;
    margin-top:10px;
}
/* Yeni slogan */
header .slogan {
    font-size:1.3rem;
    color:#d35400; /* diqqət çəkən narıncı */
    font-weight:bold;
    margin-top:5px;
}

nav {
    display:flex;
    justify-content:center;
    gap:15px;
    flex-wrap:wrap;
    margin:20px 0;
}
nav button {
    padding:12px 25px;
    border:none;
    border-radius:25px;
    background:#cfcfcf;
    color:#333;
    font-weight:bold;
    cursor:pointer;
    transition:0.3s;
}
nav button:hover {
    background:#bfbfbf;
}
.search-box {
    text-align:center;
    margin:20px;
}
.search-box input {
    padding:12px 15px;
    width:250px;
    border-radius:25px;
    border:1px solid #ccc;
    font-size:1rem;
    outline:none;
}
.products {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
    gap:20px;
    padding:20px;
    max-width:1200px;
    margin:auto;
}
.product {
    background:white;
    border-radius:20px;
    box-shadow:0 4px 12px rgba(0,0,0,0.1);
    padding:15px;
    text-align:center;
    transition: transform 0.3s;
}
.product:hover {
    transform:translateY(-5px);
}
.product img {
    max-width:100%;
    border-radius:15px;
    margin-bottom:10px;
}
.product h3 {
    font-size:1.2rem;
    margin:5px 0;
}
.product p {
    font-size:1rem;
    margin:5px 0;
    color:#555;
}
/* WhatsApp butonu daha cazibədar */
.product button {
    margin-top:10px;
    padding:10px 15px;
    border:none;
    border-radius:25px;
    background: linear-gradient(90deg, #25D366, #128C7E); /* WhatsApp rəngləri */
    color:white;
    font-weight:bold;
    cursor:pointer;
    font-size:1rem;
    transition: all 0.3s ease;
}
.product button:hover {
    transform: scale(1.05);
    box-shadow: 0 4px 12px rgba(37,211,102,0.5);
}
</style>
</head>
<body>

<header>
    <h1>Melisa Parfüm</h1>
    <p>Ətir Dünyasının Möhtəşəm Təcrübəsi</p>
    <p class="slogan">Topdan Alişda Endirim</p>
</header>

<nav>
    <button onclick="filterCategory('all')">Hamısı</button>
    <button onclick="filterCategory('Kişi')">Kişi</button>
    <button onclick="filterCategory('Qadın')">Qadın</button>
    <button onclick="filterCategory('Unisex')">Unisex</button>
    <button onclick="filterCategory('Parfüm Qutusu')">Parfüm Qutusu</button>
</nav>

<div class="search-box">
    <input type="text" id="searchInput" placeholder="Məhsul axtar..." onkeyup="searchProduct()">
</div>

<div class="products" id="productContainer"></div>

<script>
const whatsappNumber = '+994553536017';
const products = [
{name:"Q4", category:"Unisex", image:"https://i.ibb.co/S4yMHLw7/MG-20251013-183252.jpg", price:"18 AZN"},
{name:"AVENTUS SAUVAGE", category:"Kişi", image:"https://i.ibb.co/d4jYN6Nk/MG-20251016-163305.jpg", price:"18 AZN"},
{name:"Q4", category:"Kişi", image:"https://i.ibb.co/S4yMHLw7/MG-20251013-183252.jpg", price:"18 AZN"},
{name:"CREED AVENTUS", category:"Kişi", image:"https://i.ibb.co/hFWy135g/MG-20251013-183020.jpg", price:"18 AZN"},
{name:"RICARDO VERON", category:"Kişi", image:"https://i.ibb.co/4qpqyMd/MG-20251013-182940.jpg", price:"18 AZN"},
{name:"DIOR SAUVAGE", category:"Kişi", image:"https://i.ibb.co/TDN0wfsm/MG-20251013-182849.jpg", price:"18 AZN"},
{name:"LV PACIHIL", category:"Kişi", image:"https://i.ibb.co/60XYkscB/MG-20251013-182742.jpg", price:"18 AZN"},
{name:"GENERAL", category:"Kişi", image:"https://i.ibb.co/x8J3sVPb/MG-20251013-182711.jpg", price:"18 AZN"},
{name:"GISADA", category:"Kişi", image:"https://i.ibb.co/gZTkQ3hz/MG-20251013-182637.jpg", price:"18 AZN"},
{name:"REISIN ETRI", category:"Kişi", image:"https://i.ibb.co/S4jssjwp/MG-20251013-182408.jpg", price:"18 AZN"},
{name:"GISADA SWITZERLAND", category:"Kişi", image:"https://i.ibb.co/YBM8kcnW/MG-20251013-182142.jpg", price:"18 AZN"},
{name:"YASƏMƏN", category:"Qadın", image:"https://i.ibb.co/4gfmpGmw/MG-20251013-181055.jpg", price:"18 AZN"},
{name:"V SECRET SO SEXY", category:"Qadın", image:"https://i.ibb.co/qYpkh0pR/MG-20251013-180848.jpg", price:"18 AZN"},
{name:"Q4", category:"Qadın", image:"https://i.ibb.co/S4yMHLw7/MG-20251013-183252.jpg", price:"18 AZN"},
{name:"SHISEIDO GINZA", category:"Qadın", image:"https://i.ibb.co/vvZ6D3XB/MG-20251013-180530.jpg", price:"18 AZN"},
{name:"PRADA PARDOXE INTENSE", category:"Qadın", image:"https://i.ibb.co/whr4Yk15/MG-20251013-180435.jpg", price:"18 AZN"},
{name:"MY WAY", category:"Qadın", image:"https://i.ibb.co/Kc8CQyQv/MG-20251013-180402.jpg", price:"18 AZN"},
{name:"LV SYMPHONY", category:"Qadın", image:"https://i.ibb.co/tPZh9b83/MG-20251013-180335.jpg", price:"18 AZN"},
{name:"KENZO WORLD", category:"Qadın", image:"https://i.ibb.co/5xvhLbWM/MG-20251013-180104.jpg", price:"18 AZN"},
{name:"LIBRE", category:"Qadın", image:"https://i.ibb.co/DgRTqxdm/MG-20251013-180017.jpg", price:"18 AZN"},
{name:"Parfüm Qutusu", category:"Parfüm Qutusu", image:"https://i.ibb.co/S4yMHLw7/MG-20251013-183252.jpg", price:"18 AZN"}
];

function displayProducts(list){
    const container = document.getElementById('productContainer');
    container.innerHTML = '';
    if(list.length===0){
        container.innerHTML=`<p style="text-align:center; font-size:1.2rem;">Məhsul tapılmadı. <button onclick="requestWhatsApp()" style="padding:10px 15px; border-radius:20px; background:#25D366; color:white; border:none; cursor:pointer;">WhatsApp vasitəsilə sorğu göndər</button></p>`;
        return;
    }
    list.forEach(p=>{
        const div=document.createElement('div');
        div.classList.add('product');
        div.innerHTML=`
        <img src="${p.image}" alt="${p.name}">
        <h3>${p.name}</h3>
        <p>${p.category}</p>
        <p>${p.price}</p>
        <button onclick="buyWhatsApp('${p.name}')">Alış üçün WhatsApp</button>
        `;
        container.appendChild(div);
    });
}

function filterCategory(cat){
    if(cat==='all') displayProducts(products);
    else displayProducts(products.filter(p=>p.category===cat));
}

function searchProduct(){
    const q=document.getElementById('searchInput').value.toLowerCase();
    displayProducts(products.filter(p=>p.name.toLowerCase().includes(q)));
}

function buyWhatsApp(name){
    const msg=encodeURIComponent(`Mən "${name}" məhsulunu almaq istəyirəm.`);
    window.open(`https://wa.me/${whatsappNumber}?text=${msg}`,'_blank');
}

function requestWhatsApp(){
    const query=document.getElementById('searchInput').value;
    const msg=encodeURIComponent(`Mən "${query}" məhsulunu sifariş vermək istəyirəm, amma saytınızda yoxdur.`);
    window.open(`https://wa.me/${whatsappNumber}?text=${msg}`,'_blank');
}

displayProducts(products);
</script>

</body>
</html>