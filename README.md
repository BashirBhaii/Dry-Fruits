<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>DryFruits – Premium Store</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root{
      --brand:#131921;      /* Amazon-like dark */
      --brand-2:#232f3e;    /* secondary header */
      --accent:#ffd814;     /* yellow button */
      --accent-2:#fcd200;   /* hover */
      --text:#111827;
      --muted:#6b7280;
      --card:#ffffff;
      --bg:#f3f4f6;
      --green:#059669;
      --red:#ef4444;
      --chip:#ecfeff;
      --chip-text:#065f46;
      --shadow:0 6px 20px rgba(0,0,0,.08);
      --radius:16px;
    }
    *{box-sizing:border-box}
    html,body{margin:0;padding:0;font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial,"Noto Sans",sans-serif;background:var(--bg);color:var(--text)}
    a{color:inherit;text-decoration:none}
    /* Top Nav */
    .topbar{background:var(--brand);color:#fff;display:flex;align-items:center;gap:16px;padding:10px 16px;position:sticky;top:0;z-index:50}
    .logo{font-weight:800;font-size:22px;letter-spacing:.5px}
    .logo span{color:var(--accent)}
    .search{flex:1;display:flex;align-items:center}
    .search input{flex:1;padding:12px 14px;border:1px solid #e5e7eb;border-right:none;border-radius:8px 0 0 8px;font-size:15px}
    .search button{background:var(--accent);border:none;padding:12px 16px;border-radius:0 8px 8px 0;font-weight:600;cursor:pointer}
    .search button:hover{background:var(--accent-2)}
    .nav-actions{display:flex;align-items:center;gap:14px}
    .nav-link{font-size:14px;opacity:.95}
    .cart-btn{position:relative;cursor:pointer;padding:8px 12px;border-radius:8px;background:#0b1320}
    .cart-count{position:absolute;top:-6px;right:-6px;background:#f43f5e;color:#fff;font-size:12px;padding:2px 6px;border-radius:999px;font-weight:700}

    /* Subnav */
    .subnav{background:var(--brand-2);color:#e5e7eb;display:flex;gap:18px;padding:10px 16px;font-size:14px;flex-wrap:wrap}
    .chip{background:#374151;color:#e5e7eb;padding:6px 10px;border-radius:999px;cursor:pointer;transition:.2s}
    .chip.active,.chip:hover{background:#111827}

    /* Hero */
    .hero{background:linear-gradient(135deg,#fff,#eef2ff);border-radius:var(--radius);padding:24px;margin:16px;display:grid;grid-template-columns:1.2fr .8fr;gap:18px;align-items:center;box-shadow:var(--shadow)}
    .hero h1{margin:0;font-size:36px;line-height:1.1}
    .hero p{margin:10px 0 16px;color:var(--muted)}
    .hero img{width:100%;border-radius:14px}
    .hero .cta{display:flex;gap:12px}
    .btn{display:inline-flex;align-items:center;gap:8px;padding:12px 16px;border-radius:12px;border:1px solid #d1d5db;background:#fff;cursor:pointer;font-weight:600}
    .btn.primary{background:var(--accent);border-color:#eab308}
    .btn.primary:hover{background:var(--accent-2)}

    /* Toolbar */
    .toolbar{display:flex;gap:12px;align-items:center;flex-wrap:wrap;margin:0 16px 8px 16px}
    .select, .input{padding:10px 12px;border:1px solid #e5e7eb;border-radius:10px;background:#fff}
    .badge{background:var(--chip);color:var(--chip-text);padding:6px 10px;border-radius:12px;font-weight:600;font-size:12px;border:1px solid #a7f3d0}

    /* Grid */
    .container{padding:8px 16px 40px}
    .grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:16px}
    @media (max-width:1100px){.grid{grid-template-columns:repeat(3,1fr)}}
    @media (max-width:800px){
      .hero{grid-template-columns:1fr}
      .grid{grid-template-columns:repeat(2,1fr)}
      .search{order:2}
    }
    @media (max-width:520px){.grid{grid-template-columns:1fr}}

    .card{background:var(--card);border-radius:var(--radius);box-shadow:var(--shadow);overflow:hidden;display:flex;flex-direction:column}
    .thumb{height:180px;background:#f8fafc;display:flex;align-items:center;justify-content:center}
    .thumb img{max-height:100%;width:auto}
    .content{padding:12px 14px;display:flex;flex-direction:column;gap:8px}
    .title{font-weight:700;font-size:16px}
    .muted{color:var(--muted);font-size:13px}
    .row{display:flex;align-items:center;justify-content:space-between;gap:10px}
    .price{font-size:18px;font-weight:800}
    .cut{color:#9ca3af;text-decoration:line-through;font-weight:500;font-size:13px}
    .rating{font-size:13px;color:#f59e0b}
    .pill{background:#f1f5f9;border:1px solid #e5e7eb;padding:4px 8px;border-radius:999px;font-size:12px}
    .add{margin-top:6px}

    /* Cart Drawer */
    .drawer{position:fixed;top:0;right:-420px;width:380px;max-width:95vw;height:100vh;background:#fff;box-shadow:-8px 0 24px rgba(0,0,0,.15);transition:right .25s ease;z-index:60;display:flex;flex-direction:column}
    .drawer.open{right:0}
    .drawer header{padding:16px;border-bottom:1px solid #e5e7eb;display:flex;align-items:center;justify-content:space-between}
    .drawer .items{flex:1;overflow:auto}
    .cart-item{display:flex;gap:12px;padding:12px 16px;border-bottom:1px solid #f3f4f6}
    .cart-item img{width:56px;height:56px;object-fit:cover;border-radius:8px}
    .cart-item .ci-title{font-weight:600;font-size:14px}
    .drawer footer{padding:16px;border-top:1px solid #e5e7eb;display:grid;gap:10px}
    .total-row{display:flex;align-items:center;justify-content:space-between;font-weight:800}
    .checkout{background:var(--green);color:#fff;font-weight:700;border:none;padding:12px 16px;border-radius:10px;cursor:pointer}

    /* Footer */
    footer.site{margin-top:24px;background:#111827;color:#e5e7eb;padding:20px 16px;text-align:center}
  </style>
</head>
<body>
  <!-- Top bar -->
  <div class="topbar">
    <div class="logo">Dry<span>Fruits</span>.pk</div>
    <div class="search">
      <input id="search" type="search" placeholder="Search almonds, pistachios, dates…" />
      <button id="searchBtn">Search</button>
    </div>
    <div class="nav-actions">
      <a class="nav-link" href="#">Sign In</a>
      <a class="nav-link" href="#">Orders</a>
      <div class="cart-btn" id="openCart" aria-label="Open cart">🛒<span class="cart-count" id="cartCount">0</span></div>
    </div>
  </div>
  
  <!-- Subnav categories -->
  <div class="subnav" id="categoryChips"></div>

  <!-- Hero -->
  <section class="hero">
    <div>
      <h1>Premium Dry Fruits, Fast Delivery</h1>
      <p>Pakistan-wide shipping. Fresh stock, airtight packing, and easy returns. Prices shown include a <b>30% markup</b> as requested.</p>
      <div class="cta">
        <button class="btn primary" id="shopNow">Shop bestsellers</button>
        <button class="btn" id="toggleView">Grid View</button>
      </div>
    </div>
    <img src="https://images.unsplash.com/photo-1600959907703-125ba1374a12?q=80&w=1400&auto=format&fit=crop" alt="Assorted dry fruits"/>
  </section>

  <!-- Toolbar -->
  <div class="toolbar">
    <select class="select" id="sort">
      <option value="featured">Sort: Featured</option>
      <option value="priceAsc">Price: Low to High</option>
      <option value="priceDesc">Price: High to Low</option>
      <option value="rating">Customer Rating</option>
    </select>
    <span class="badge" id="countBadge">0 items</span>
  </div>

  <!-- Products -->
  <main class="container">
    <div class="grid" id="grid"></div>
  </main>

  <!-- Cart Drawer -->
  <aside class="drawer" id="drawer">
    <header>
      <strong>Your Cart</strong>
      <button class="btn" id="closeCart">Close</button>
    </header>
    <div class="items" id="cartItems"></div>
    <footer>
      <div class="total-row"><span>Subtotal</span><span id="subtotal">Rs 0</span></div>
      <button class="checkout">Proceed to Checkout</button>
      <small class="muted">Note: Displayed prices include a 30% markup over base market prices.</small>
    </footer>
  </aside>

  <footer class="site">
    © <span id="year"></span> DryFruits.pk — Freshness Guaranteed • Customer Care: 0300‑0000000
  </footer>

  <script>
    const PKR = n => `Rs ${n.toLocaleString('en-PK')}`;
    const MARKUP = 1.30; // 30% higher rates

    const products = [
      {id:1,name:'Kaghan Almonds (Badam) 1kg',cat:'Almonds',base:2300,img:'https://cdn.pixabay.com/photo/2022/10/21/14/54/nuts-7537290_640.jpg',rating:4.7,fast:true},
      {id:2,name:'Iranian Pistachios (Pista) 1kg',cat:'Pistachios',base:4200,img:'https://cdn.pixabay.com/photo/2018/06/03/14/32/pistachios-3450670_640.jpg',rating:4.8,fast:true},
      {id:3,name:'Chilgoza Pine Nuts 1kg',cat:'Pine Nuts',base:7800,img:'https://cdn.pixabay.com/photo/2015/12/18/02/57/pine-nuts-1098175_640.jpg',rating:4.6,fast:false},
      {id:4,name:'Kashmiri Walnuts (Akhrot) 1kg',cat:'Walnuts',base:2600,img:'https://cdn.pixabay.com/photo/2013/03/02/01/25/walnut-89019_1280.jpg',rating:4.5,fast:true},
      {id:5,name:'Cashews W320 (Kaju) 1kg',cat:'Cashews',base:3600,img:'https://cdn.pixabay.com/photo/2025/03/18/03/51/kaju-sweets-9477189_640.jpg',rating:4.6,fast:true},
      {id:6,name:'Ajwa Dates (Khajoor) 1kg',cat:'Dates',base:3800,img:'https://cdn.pixabay.com/photo/2015/09/09/14/22/jujube-931587_640.jpg',rating:4.9,fast:true},
      {id:7,name:'Dried Figs (Anjeer) 1kg',cat:'Figs',base:3400,img:'https://cdn.pixabay.com/photo/2018/10/27/08/46/fig-jam-3776038_640.jpg',rating:4.4,fast:false},
      {id:8,name:'Raisins Golden (Kishmish) 1kg',cat:'Raisins',base:1200,img:'https://cdn.pixabay.com/photo/2015/02/05/05/58/food-624603_1280.jpg',rating:4.3,fast:true},
      {id:9,name:'Apricots Dried (Khubani) 1kg',cat:'Apricots',base:1500,img:'https://cdn.pixabay.com/photo/2015/06/28/15/53/peaches-824624_640.jpg',rating:4.2,fast:false},
      {id:10,name:'Hazelnuts 1kg',cat:'Hazelnuts',base:5200,img:'https://cdn.pixabay.com/photo/2016/10/01/14/00/hazelnuts-1707601_640.jpg',rating:4.5,fast:false},
      {id:11,name:'Pecans 1kg',cat:'Pecans',base:5600,img:'https://cdn.pixabay.com/photo/2023/04/20/09/54/pecan-nuts-7939326_640.jpg',rating:4.4,fast:false},
      {id:12,name:'Brazil Nuts 1kg',cat:'Brazil Nuts',base:6100,img:'https://cdn.pixabay.com/photo/2021/01/10/18/44/nuts-5906063_1280.jpg',rating:4.3,fast:false},
      {id:13,name:'Macadamia 1kg',cat:'Macadamia',base:7500,img:'https://cdn.pixabay.com/photo/2012/10/15/20/29/macadamia-61634_640.jpg',rating:4.7,fast:false},
      {id:14,name:'Peanuts Roasted 1kg',cat:'Peanuts',base:700,img:'https://cdn.pixabay.com/photo/2015/01/31/14/40/peanuts-618547_640.jpg',rating:4.0,fast:true},
      {id:15,name:'Chironji (Charoli) 1kg',cat:'Chironji',base:6400,img:'https://cdn.pixabay.com/photo/2017/01/24/07/36/suzuki-2004732_1280.jpg',rating:4.1,fast:false},
      {id:16,name:'Trail Mix Supreme 1kg',cat:'Mixes',base:3000,img:'https://cdn.pixabay.com/photo/2017/04/04/17/37/food-2202384_1280.jpg',rating:4.6,fast:true},
    ];

    const state = { 
      q: '',
      cat: 'All',
      sort: 'featured',
      cart: [] // {id, qty}
    };

    const cats = ['All', ...Array.from(new Set(products.map(p=>p.cat)))];

    const grid = document.getElementById('grid');
    const countBadge = document.getElementById('countBadge');
    const chips = document.getElementById('categoryChips');

    function renderChips(){
      chips.innerHTML = cats.map(c=>`<div class="chip ${state.cat===c?'active':''}" data-cat="${c}">${c}</div>`).join('');
      chips.querySelectorAll('.chip').forEach(el=>{
        el.addEventListener('click',()=>{state.cat = el.dataset.cat; render(); window.scrollTo({top:0,behavior:'smooth'});});
      });
    }

    function priceWithMarkup(base){
      return Math.round(base * MARKUP);
    }

    function filtered(){
      let list = products.filter(p=> p.name.toLowerCase().includes(state.q.toLowerCase()));
      if(state.cat !== 'All') list = list.filter(p=> p.cat === state.cat);
      switch(state.sort){
        case 'priceAsc': list.sort((a,b)=> priceWithMarkup(a.base) - priceWithMarkup(b.base)); break;
        case 'priceDesc': list.sort((a,b)=> priceWithMarkup(b.base) - priceWithMarkup(a.base)); break;
        case 'rating': list.sort((a,b)=> b.rating - a.rating); break;
        default: break; // featured
      }
      return list;
    }

    function starRow(r){
      const full = '★'.repeat(Math.floor(r));
      const half = (r%1>=0.5)?'½':''; // simple text half marker
      const empty = '☆'.repeat(5-Math.ceil(r));
      return `<span class="rating" aria-label="${r} out of 5">${full}${empty} <span class="muted">(${r.toFixed(1)})</span></span>`;
    }

    function addToCart(id){
      const found = state.cart.find(ci=>ci.id===id);
      if(found) found.qty += 1; else state.cart.push({id,qty:1});
      updateCartUI();
    }

    function removeFromCart(id){
      state.cart = state.cart.filter(ci=>ci.id!==id);
      updateCartUI();
    }

    function changeQty(id, delta){
      const item = state.cart.find(ci=>ci.id===id); if(!item) return;
      item.qty = Math.max(1, item.qty + delta);
      updateCartUI();
    }

    function updateCartUI(){
      const cartCount = document.getElementById('cartCount');
      const cartItems = document.getElementById('cartItems');
      const subtotalEl = document.getElementById('subtotal');
      const entries = state.cart.map(ci=>{
        const p = products.find(p=>p.id===ci.id);
        const price = priceWithMarkup(p.base);
        return { ...p, qty: ci.qty, price, total: price*ci.qty };
      });
      cartCount.textContent = entries.reduce((a,b)=>a+b.qty,0);
      cartItems.innerHTML = entries.map(e=>`
        <div class="cart-item">
          <img src="${e.img}" alt="${e.name}"/>
          <div style="flex:1">
            <div class="ci-title">${e.name}</div>
            <div class="muted">${PKR(e.price)} × ${e.qty}</div>
            <div class="row" style="margin-top:6px">
              <div class="pill">${e.cat}</div>
              <div>
                <button class="btn" onclick="changeQty(${e.id},-1)">−</button>
                <button class="btn" onclick="changeQty(${e.id},+1)">+</button>
                <button class="btn" onclick="removeFromCart(${e.id})">Remove</button>
              </div>
            </div>
          </div>
        </div>`).join('');
      const subtotal = entries.reduce((sum,e)=>sum+e.total,0);
      subtotalEl.textContent = PKR(subtotal);
    }

    function render(){
      const list = filtered();
      countBadge.textContent = `${list.length} items`;
      grid.innerHTML = list.map(p=>{
        const price = priceWithMarkup(p.base);
        const cut = Math.round(p.base*1.45); // fake crossed MRP for look
        return `
          <article class="card">
            <div class="thumb"><img loading="lazy" src="${p.img}" alt="${p.name}"/></div>
            <div class="content">
              <div class="title">${p.name}</div>
              <div class="row">
                <span class="pill">${p.cat}</span>
                ${p.fast?'<span class="pill">Fast Delivery</span>':''}
              </div>
              ${starRow(p.rating)}
              <div class="row">
                <div>
                  <div class="price">${PKR(price)}</div>
                  <div class="cut">${PKR(cut)}</div>
                </div>
                <button class="btn primary add" onclick="addToCart(${p.id})">Add to Cart</button>
              </div>
              <div class="muted">Price includes 30% markup</div>
            </div>
          </article>`;
      }).join('');
    }

    // Event wiring
    document.getElementById('search').addEventListener('input', (e)=>{state.q=e.target.value; render();});
    document.getElementById('searchBtn').addEventListener('click', ()=> render());
    document.getElementById('sort').addEventListener('change', (e)=>{state.sort=e.target.value; render();});

    // Drawer control
    const drawer = document.getElementById('drawer');
    document.getElementById('openCart').addEventListener('click', ()=> drawer.classList.add('open'));
    document.getElementById('closeCart').addEventListener('click', ()=> drawer.classList.remove('open'));

    // Hero buttons
    document.getElementById('shopNow').addEventListener('click', ()=>{
      window.scrollTo({top: document.querySelector('.container').offsetTop-20, behavior:'smooth'});
    });
    document.getElementById('toggleView').addEventListener('click', ()=>{
      const g = document.querySelector('.grid');
      const cols = getComputedStyle(g).gridTemplateColumns.split(' ').length;
      if(cols>=3){ g.style.gridTemplateColumns = 'repeat(2, minmax(0,1fr))'; }
      else { g.style.gridTemplateColumns = 'repeat(4, minmax(0,1fr))'; }
    });

    // Init
    renderChips();
    render();
    updateCartUI();
    document.getElementById('year').textContent = new Date().getFullYear();
  </script>
</body>
</html>
