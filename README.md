# threadswap
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ThreadSwap — Buy & Sell Pre-Loved Clothes</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --cream: #f5f0e8;
    --warm-white: #faf8f4;
    --charcoal: #1a1714;
    --brown: #6b4f3a;
    --rust: #c4622d;
    --sage: #7a8c6e;
    --gold: #d4a843;
    --light-brown: #e8d5c4;
    --text-muted: #8a7968;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--warm-white);
    color: var(--charcoal);
    overflow-x: hidden;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.2rem 3rem;
    background: rgba(245,240,232,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(107,79,58,0.15);
  }
  .logo {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem; font-weight: 900; letter-spacing: -0.5px;
    color: var(--charcoal);
  }
  .logo span { color: var(--rust); }
  .nav-links { display: flex; gap: 2rem; align-items: center; }
  .nav-links a {
    text-decoration: none; color: var(--charcoal);
    font-size: 0.9rem; font-weight: 500; letter-spacing: 0.3px;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--rust); }
  .nav-actions { display: flex; gap: 1rem; align-items: center; }
  .btn {
    padding: 0.6rem 1.4rem; border-radius: 50px; border: none;
    font-family: 'DM Sans', sans-serif; font-weight: 600;
    font-size: 0.88rem; cursor: pointer; transition: all 0.25s;
    text-decoration: none; display: inline-flex; align-items: center; gap: 0.4rem;
  }
  .btn-outline {
    background: transparent; color: var(--charcoal);
    border: 1.5px solid var(--charcoal);
  }
  .btn-outline:hover { background: var(--charcoal); color: var(--cream); }
  .btn-primary {
    background: var(--rust); color: #fff;
    box-shadow: 0 4px 14px rgba(196,98,45,0.35);
  }
  .btn-primary:hover { background: #a84f22; transform: translateY(-1px); }
  .cart-btn {
    position: relative; background: none; border: none; cursor: pointer;
    font-size: 1.3rem; color: var(--charcoal); padding: 0.3rem;
  }
  .cart-badge {
    position: absolute; top: -4px; right: -4px;
    background: var(--rust); color: #fff;
    font-size: 0.65rem; font-weight: 700;
    width: 18px; height: 18px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
  }

  /* ── HERO ── */
  .hero {
    min-height: 100vh; display: flex; align-items: center;
    padding: 6rem 3rem 3rem;
    background: var(--cream);
    position: relative; overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute; top: -100px; right: -100px;
    width: 600px; height: 600px; border-radius: 50%;
    background: radial-gradient(circle, rgba(212,168,67,0.18) 0%, transparent 70%);
  }
  .hero::after {
    content: '';
    position: absolute; bottom: -50px; left: 40%;
    width: 300px; height: 300px; border-radius: 50%;
    background: radial-gradient(circle, rgba(196,98,45,0.12) 0%, transparent 70%);
  }
  .hero-content { max-width: 580px; z-index: 1; }
  .hero-tag {
    display: inline-block;
    background: var(--light-brown); color: var(--brown);
    font-size: 0.78rem; font-weight: 600; letter-spacing: 1.5px;
    text-transform: uppercase; padding: 0.35rem 1rem; border-radius: 50px;
    margin-bottom: 1.5rem;
    animation: fadeUp 0.6s ease both;
  }
  .hero h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.8rem, 5vw, 4.5rem);
    font-weight: 900; line-height: 1.05;
    margin-bottom: 1.5rem;
    animation: fadeUp 0.6s 0.1s ease both;
  }
  .hero h1 em { color: var(--rust); font-style: italic; }
  .hero p {
    font-size: 1.05rem; color: var(--text-muted); line-height: 1.7;
    margin-bottom: 2.5rem;
    animation: fadeUp 0.6s 0.2s ease both;
  }
  .hero-actions {
    display: flex; gap: 1rem; flex-wrap: wrap;
    animation: fadeUp 0.6s 0.3s ease both;
  }
  .hero-actions .btn { padding: 0.85rem 2rem; font-size: 0.95rem; }
  .hero-stats {
    display: flex; gap: 2.5rem; margin-top: 3.5rem;
    animation: fadeUp 0.6s 0.4s ease both;
  }
  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 2rem; font-weight: 700; color: var(--charcoal);
    display: block;
  }
  .stat-label { font-size: 0.82rem; color: var(--text-muted); font-weight: 500; }

  .hero-visual {
    position: absolute; right: 0; top: 0; bottom: 0;
    width: 45%; z-index: 0;
    display: flex; align-items: center; justify-content: center;
  }
  .clothes-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 1rem;
    transform: rotate(3deg); margin-right: -2rem;
  }
  .clothes-card {
    background: #fff; border-radius: 16px;
    padding: 1rem; box-shadow: 0 8px 30px rgba(0,0,0,0.08);
    animation: float 4s ease-in-out infinite;
  }
  .clothes-card:nth-child(2) { animation-delay: 1s; margin-top: 2rem; }
  .clothes-card:nth-child(3) { animation-delay: 2s; }
  .clothes-card:nth-child(4) { animation-delay: 0.5s; margin-top: 2rem; }
  .clothes-emoji { font-size: 3rem; display: block; text-align: center; margin-bottom: 0.5rem; }
  .clothes-price {
    font-weight: 700; font-size: 0.85rem; color: var(--rust);
    text-align: center;
  }
  .clothes-name { font-size: 0.75rem; color: var(--text-muted); text-align: center; }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-10px); }
  }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── SECTIONS ── */
  section { padding: 5rem 3rem; }
  .section-label {
    font-size: 0.78rem; font-weight: 600; letter-spacing: 2px;
    text-transform: uppercase; color: var(--rust); margin-bottom: 0.6rem;
  }
  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.8rem, 3vw, 2.8rem); font-weight: 700;
    line-height: 1.2; margin-bottom: 1rem;
  }
  .section-sub { color: var(--text-muted); font-size: 1rem; line-height: 1.6; max-width: 480px; }

  /* ── HOW IT WORKS ── */
  .how-it-works { background: var(--charcoal); color: #fff; }
  .how-it-works .section-label { color: var(--gold); }
  .how-it-works .section-title { color: #fff; }
  .steps {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 2rem; margin-top: 3rem;
  }
  .step {
    background: rgba(255,255,255,0.05); border-radius: 16px;
    padding: 2rem; border: 1px solid rgba(255,255,255,0.08);
    transition: all 0.3s;
  }
  .step:hover { background: rgba(255,255,255,0.1); transform: translateY(-4px); }
  .step-num {
    font-family: 'Playfair Display', serif;
    font-size: 3rem; font-weight: 900; color: var(--gold);
    opacity: 0.5; display: block; margin-bottom: 0.5rem;
  }
  .step h3 { font-size: 1.05rem; font-weight: 600; margin-bottom: 0.5rem; }
  .step p { font-size: 0.88rem; color: rgba(255,255,255,0.55); line-height: 1.6; }

  /* ── SEARCH / FILTER BAR ── */
  .browse-section { background: var(--warm-white); }
  .search-bar {
    display: flex; gap: 1rem; align-items: center; flex-wrap: wrap;
    background: var(--cream); border-radius: 16px;
    padding: 1.2rem 1.5rem; margin: 2.5rem 0;
    border: 1px solid var(--light-brown);
  }
  .search-input {
    flex: 1; min-width: 200px; border: none; background: transparent;
    font-family: 'DM Sans', sans-serif; font-size: 0.95rem;
    color: var(--charcoal); outline: none;
  }
  .search-input::placeholder { color: var(--text-muted); }
  .filter-select {
    border: 1px solid var(--light-brown); border-radius: 8px;
    padding: 0.5rem 1rem; background: #fff;
    font-family: 'DM Sans', sans-serif; font-size: 0.88rem;
    color: var(--charcoal); cursor: pointer; outline: none;
  }
  .search-btn {
    background: var(--charcoal); color: #fff; border: none;
    padding: 0.6rem 1.4rem; border-radius: 10px;
    font-family: 'DM Sans', sans-serif; font-weight: 600;
    font-size: 0.88rem; cursor: pointer; transition: all 0.2s;
  }
  .search-btn:hover { background: var(--rust); }

  /* ── PRODUCT GRID ── */
  .categories {
    display: flex; gap: 0.8rem; flex-wrap: wrap; margin-bottom: 2rem;
  }
  .cat-btn {
    padding: 0.45rem 1.1rem; border-radius: 50px;
    border: 1.5px solid var(--light-brown);
    background: transparent; color: var(--charcoal);
    font-family: 'DM Sans', sans-serif; font-weight: 500;
    font-size: 0.85rem; cursor: pointer; transition: all 0.2s;
  }
  .cat-btn.active, .cat-btn:hover {
    background: var(--charcoal); color: #fff; border-color: var(--charcoal);
  }

  .products-grid {
    display: grid; grid-template-columns: repeat(auto-fill, minmax(230px, 1fr));
    gap: 1.5rem;
  }
  .product-card {
    background: #fff; border-radius: 20px;
    overflow: hidden; transition: all 0.3s;
    border: 1px solid rgba(0,0,0,0.05);
    cursor: pointer;
  }
  .product-card:hover { transform: translateY(-6px); box-shadow: 0 20px 40px rgba(0,0,0,0.1); }
  .product-img {
    height: 200px; background: var(--cream);
    display: flex; align-items: center; justify-content: center;
    font-size: 5rem; position: relative; overflow: hidden;
  }
  .product-badge {
    position: absolute; top: 12px; left: 12px;
    background: var(--rust); color: #fff;
    font-size: 0.7rem; font-weight: 700; letter-spacing: 0.5px;
    padding: 0.25rem 0.6rem; border-radius: 6px;
    text-transform: uppercase;
  }
  .badge-new { background: var(--sage); }
  .badge-hot { background: var(--gold); color: var(--charcoal); }
  .wishlist-btn {
    position: absolute; top: 12px; right: 12px;
    background: rgba(255,255,255,0.9); border: none;
    width: 32px; height: 32px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; font-size: 1rem; transition: all 0.2s;
  }
  .wishlist-btn:hover { background: #fff; transform: scale(1.1); }
  .product-info { padding: 1.2rem; }
  .product-brand { font-size: 0.72rem; font-weight: 600; color: var(--rust); letter-spacing: 0.5px; text-transform: uppercase; }
  .product-name { font-weight: 600; font-size: 0.95rem; margin: 0.2rem 0; }
  .product-size { font-size: 0.78rem; color: var(--text-muted); margin-bottom: 0.6rem; }
  .product-footer { display: flex; align-items: center; justify-content: space-between; margin-top: 0.8rem; }
  .product-price { font-family: 'Playfair Display', serif; font-size: 1.2rem; font-weight: 700; }
  .original-price { font-size: 0.78rem; color: var(--text-muted); text-decoration: line-through; margin-left: 0.3rem; font-family: 'DM Sans', sans-serif; font-weight: 400; }
  .add-cart-btn {
    background: var(--charcoal); color: #fff; border: none;
    padding: 0.45rem 1rem; border-radius: 8px; font-size: 0.8rem;
    font-family: 'DM Sans', sans-serif; font-weight: 600;
    cursor: pointer; transition: all 0.2s;
  }
  .add-cart-btn:hover { background: var(--rust); }
  .condition-dot {
    display: inline-block; width: 8px; height: 8px; border-radius: 50%;
    margin-right: 4px;
  }
  .cond-excellent { background: var(--sage); }
  .cond-good { background: var(--gold); }
  .cond-fair { background: #e0956a; }
  .condition-label { font-size: 0.75rem; color: var(--text-muted); display: flex; align-items: center; }

  /* ── SELL SECTION ── */
  .sell-section {
    background: linear-gradient(135deg, var(--rust) 0%, #8b3a1a 100%);
    color: #fff; border-radius: 24px; margin: 0 3rem 3rem;
    padding: 4rem; display: flex; align-items: center; gap: 3rem;
    flex-wrap: wrap;
  }
  .sell-content { flex: 1; min-width: 280px; }
  .sell-content .section-label { color: rgba(255,255,255,0.6); }
  .sell-content .section-title { color: #fff; }
  .sell-content p { color: rgba(255,255,255,0.75); line-height: 1.7; margin-bottom: 2rem; }
  .sell-form { flex: 1; min-width: 300px; }
  .sell-form-inner {
    background: rgba(255,255,255,0.12); border-radius: 20px;
    padding: 2rem; backdrop-filter: blur(10px);
    border: 1px solid rgba(255,255,255,0.2);
  }
  .form-group { margin-bottom: 1rem; }
  .form-label { display: block; font-size: 0.82rem; font-weight: 600; margin-bottom: 0.4rem; color: rgba(255,255,255,0.8); }
  .form-input, .form-select, .form-textarea {
    width: 100%; padding: 0.7rem 1rem;
    border: 1px solid rgba(255,255,255,0.2); border-radius: 10px;
    background: rgba(255,255,255,0.1); color: #fff;
    font-family: 'DM Sans', sans-serif; font-size: 0.9rem; outline: none;
    transition: border-color 0.2s;
  }
  .form-input::placeholder, .form-textarea::placeholder { color: rgba(255,255,255,0.45); }
  .form-input:focus, .form-select:focus, .form-textarea:focus {
    border-color: rgba(255,255,255,0.6);
  }
  .form-select option { background: var(--rust); color: #fff; }
  .form-textarea { resize: none; height: 80px; }
  .form-row { display: flex; gap: 1rem; }
  .form-row .form-group { flex: 1; }
  .upload-area {
    border: 2px dashed rgba(255,255,255,0.35); border-radius: 12px;
    padding: 1.5rem; text-align: center; cursor: pointer;
    transition: all 0.2s; margin-bottom: 1rem;
  }
  .upload-area:hover { border-color: rgba(255,255,255,0.7); background: rgba(255,255,255,0.05); }
  .upload-icon { font-size: 2rem; display: block; margin-bottom: 0.4rem; }
  .upload-text { font-size: 0.82rem; color: rgba(255,255,255,0.6); }
  .btn-white {
    width: 100%; background: #fff; color: var(--rust);
    font-family: 'DM Sans', sans-serif; font-weight: 700;
    font-size: 0.95rem; padding: 0.85rem; border-radius: 12px;
    border: none; cursor: pointer; transition: all 0.2s;
    letter-spacing: 0.2px;
  }
  .btn-white:hover { background: var(--cream); transform: translateY(-1px); }

  /* ── TESTIMONIALS ── */
  .testimonials { background: var(--cream); }
  .testimonials-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 1.5rem; margin-top: 3rem; }
  .testimonial-card {
    background: #fff; border-radius: 20px; padding: 1.8rem;
    border: 1px solid var(--light-brown);
    transition: box-shadow 0.3s;
  }
  .testimonial-card:hover { box-shadow: 0 10px 30px rgba(0,0,0,0.08); }
  .stars { color: var(--gold); font-size: 1rem; margin-bottom: 0.8rem; }
  .testimonial-text { font-size: 0.92rem; line-height: 1.65; color: var(--charcoal); margin-bottom: 1.2rem; font-style: italic; }
  .reviewer { display: flex; align-items: center; gap: 0.8rem; }
  .reviewer-avatar {
    width: 38px; height: 38px; border-radius: 50%;
    background: var(--light-brown); display: flex; align-items: center;
    justify-content: center; font-size: 1.2rem;
  }
  .reviewer-name { font-weight: 600; font-size: 0.88rem; }
  .reviewer-loc { font-size: 0.75rem; color: var(--text-muted); }

  /* ── FOOTER ── */
  footer {
    background: var(--charcoal); color: rgba(255,255,255,0.65);
    padding: 3rem; text-align: center;
  }
  .footer-logo {
    font-family: 'Playfair Display', serif;
    font-size: 1.8rem; font-weight: 900; color: #fff; margin-bottom: 0.5rem;
  }
  .footer-logo span { color: var(--rust); }
  .footer-tagline { font-size: 0.88rem; margin-bottom: 2rem; }
  .footer-links { display: flex; gap: 2rem; justify-content: center; flex-wrap: wrap; margin-bottom: 1.5rem; }
  .footer-links a { color: rgba(255,255,255,0.5); text-decoration: none; font-size: 0.85rem; transition: color 0.2s; }
  .footer-links a:hover { color: var(--gold); }
  .footer-copy { font-size: 0.78rem; color: rgba(255,255,255,0.3); }

  /* ── MODAL ── */
  .modal-overlay {
    position: fixed; inset: 0; background: rgba(0,0,0,0.5);
    z-index: 200; display: none; align-items: center; justify-content: center;
    backdrop-filter: blur(4px);
  }
  .modal-overlay.active { display: flex; }
  .modal {
    background: #fff; border-radius: 24px; padding: 2.5rem;
    max-width: 480px; width: 90%; max-height: 85vh; overflow-y: auto;
    animation: slideUp 0.3s ease;
    position: relative;
  }
  @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
  .modal-close {
    position: absolute; top: 1.2rem; right: 1.2rem;
    background: var(--cream); border: none; border-radius: 50%;
    width: 32px; height: 32px; font-size: 1rem; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    color: var(--charcoal); transition: all 0.2s;
  }
  .modal-close:hover { background: var(--light-brown); }
  .modal-title { font-family: 'Playfair Display', serif; font-size: 1.5rem; font-weight: 700; margin-bottom: 1.5rem; }

  /* ── TOAST ── */
  .toast {
    position: fixed; bottom: 2rem; right: 2rem; z-index: 300;
    background: var(--charcoal); color: #fff;
    padding: 0.9rem 1.5rem; border-radius: 12px;
    font-size: 0.9rem; font-weight: 500;
    display: flex; align-items: center; gap: 0.5rem;
    transform: translateY(100px); opacity: 0;
    transition: all 0.35s cubic-bezier(0.34,1.56,0.64,1);
    box-shadow: 0 8px 24px rgba(0,0,0,0.2);
  }
  .toast.show { transform: translateY(0); opacity: 1; }

  /* ── RESPONSIVE ── */
  @media(max-width: 768px) {
    nav { padding: 1rem 1.5rem; }
    .nav-links { display: none; }
    .hero { padding: 5rem 1.5rem 3rem; min-height: auto; }
    .hero-visual { display: none; }
    section { padding: 3.5rem 1.5rem; }
    .sell-section { margin: 0 1.5rem 2rem; padding: 2.5rem 1.5rem; }
    .hero-stats { gap: 1.5rem; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="logo">Thread<span>Swap</span></div>
  <div class="nav-links">
    <a href="#browse">Browse</a>
    <a href="#sell">Sell</a>
    <a href="#how">How it Works</a>
    <a href="#reviews">Reviews</a>
  </div>
  <div class="nav-actions">
    <button class="cart-btn" onclick="openCart()">🛒<span class="cart-badge" id="cartBadge">0</span></button>
    <button class="btn btn-outline" onclick="openLogin()">Log in</button>
    <button class="btn btn-primary" onclick="openSignup()">Sign up</button>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-content">
    <div class="hero-tag">🌿 Sustainable Fashion Marketplace</div>
    <h1>Give Clothes a<br><em>Second Life</em></h1>
    <p>Buy and sell pre-loved fashion at unbeatable prices. Every purchase reduces textile waste — look good, feel good, do good.</p>
    <div class="hero-actions">
      <a href="#browse" class="btn btn-primary">🔍 Shop Now</a>
      <a href="#sell" class="btn btn-outline">📦 Start Selling</a>
    </div>
    <div class="hero-stats">
      <div>
        <span class="stat-num">12K+</span>
        <span class="stat-label">Items Listed</span>
      </div>
      <div>
        <span class="stat-num">5K+</span>
        <span class="stat-label">Happy Buyers</span>
      </div>
      <div>
        <span class="stat-num">40%</span>
        <span class="stat-label">Avg. Savings</span>
      </div>
    </div>
  </div>
  <div class="hero-visual">
    <div class="clothes-grid">
      <div class="clothes-card"><span class="clothes-emoji">👗</span><div class="clothes-price">₹450</div><div class="clothes-name">Summer Dress</div></div>
      <div class="clothes-card"><span class="clothes-emoji">🧥</span><div class="clothes-price">₹1,200</div><div class="clothes-name">Denim Jacket</div></div>
      <div class="clothes-card"><span class="clothes-emoji">👟</span><div class="clothes-price">₹650</div><div class="clothes-name">Sneakers</div></div>
      <div class="clothes-card"><span class="clothes-emoji">👕</span><div class="clothes-price">₹200</div><div class="clothes-name">Vintage Tee</div></div>
    </div>
  </div>
</section>

<!-- HOW IT WORKS -->
<section class="how-it-works" id="how">
  <div class="section-label">Simple Process</div>
  <div class="section-title">How ThreadSwap Works</div>
  <div class="steps">
    <div class="step">
      <span class="step-num">01</span>
      <h3>📸 List Your Item</h3>
      <p>Upload photos, set your price, add a description. It takes less than 3 minutes.</p>
    </div>
    <div class="step">
      <span class="step-num">02</span>
      <h3>💬 Connect & Negotiate</h3>
      <p>Chat with buyers, answer questions, and agree on a fair deal.</p>
    </div>
    <div class="step">
      <span class="step-num">03</span>
      <h3>📦 Ship or Meet Up</h3>
      <p>Choose home delivery or a local meetup — whatever suits both parties.</p>
    </div>
    <div class="step">
      <span class="step-num">04</span>
      <h3>💸 Get Paid</h3>
      <p>Funds released securely once the buyer confirms receipt. Simple and safe.</p>
    </div>
  </div>
</section>

<!-- BROWSE -->
<section class="browse-section" id="browse">
  <div class="section-label">Marketplace</div>
  <div class="section-title">Browse Listings</div>
  <p class="section-sub">Thousands of pre-loved pieces from real people near you.</p>

  <div class="search-bar">
    <span style="font-size:1.1rem">🔍</span>
    <input class="search-input" type="text" placeholder="Search for jeans, tops, shoes..." id="searchInput" oninput="filterProducts()">
    <select class="filter-select" id="sizeFilter" onchange="filterProducts()">
      <option value="">All Sizes</option>
      <option>XS</option><option>S</option><option>M</option><option>L</option><option>XL</option><option>XXL</option>
    </select>
    <select class="filter-select" id="condFilter" onchange="filterProducts()">
      <option value="">All Conditions</option>
      <option>Excellent</option><option>Good</option><option>Fair</option>
    </select>
    <select class="filter-select" id="priceFilter" onchange="filterProducts()">
      <option value="">Any Price</option>
      <option value="low">Under ₹500</option>
      <option value="mid">₹500–₹1500</option>
      <option value="high">Over ₹1500</option>
    </select>
    <button class="search-btn" onclick="filterProducts()">Search</button>
  </div>

  <div class="categories">
    <button class="cat-btn active" onclick="setCategory(this, 'all')">All</button>
    <button class="cat-btn" onclick="setCategory(this, 'tops')">👕 Tops</button>
    <button class="cat-btn" onclick="setCategory(this, 'bottoms')">👖 Bottoms</button>
    <button class="cat-btn" onclick="setCategory(this, 'dresses')">👗 Dresses</button>
    <button class="cat-btn" onclick="setCategory(this, 'jackets')">🧥 Jackets</button>
    <button class="cat-btn" onclick="setCategory(this, 'shoes')">👟 Shoes</button>
    <button class="cat-btn" onclick="setCategory(this, 'accessories')">👜 Accessories</button>
  </div>

  <div class="products-grid" id="productsGrid"></div>
</section>

<!-- SELL SECTION -->
<div class="sell-section" id="sell">
  <div class="sell-content">
    <div class="section-label">Earn Money</div>
    <div class="section-title">Sell Your Clothes</div>
    <p>Clear out your wardrobe and earn cash. List in minutes, sell to thousands of shoppers looking for exactly what you have.</p>
    <div style="display:flex;gap:1.5rem;flex-wrap:wrap">
      <div>
        <div style="font-family:'Playfair Display',serif;font-size:1.8rem;font-weight:700;color:#fff">₹0</div>
        <div style="font-size:0.8rem;color:rgba(255,255,255,0.6)">Listing Fee</div>
      </div>
      <div>
        <div style="font-family:'Playfair Display',serif;font-size:1.8rem;font-weight:700;color:#fff">5%</div>
        <div style="font-size:0.8rem;color:rgba(255,255,255,0.6)">Commission Only</div>
      </div>
      <div>
        <div style="font-family:'Playfair Display',serif;font-size:1.8rem;font-weight:700;color:#fff">24h</div>
        <div style="font-size:0.8rem;color:rgba(255,255,255,0.6)">Avg. Time to Sell</div>
      </div>
    </div>
  </div>
  <div class="sell-form">
    <div class="sell-form-inner">
      <div style="font-weight:700;font-size:1.1rem;color:#fff;margin-bottom:1.2rem">📦 List an Item</div>
      <div class="upload-area" onclick="showToast('📸 Photo upload feature available after sign-up!')">
        <span class="upload-icon">📷</span>
        <div class="upload-text">Click to upload photos</div>
      </div>
      <div class="form-group">
        <label class="form-label">Item Name</label>
        <input class="form-input" placeholder="e.g. Zara floral midi dress" id="itemName">
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Category</label>
          <select class="form-select">
            <option>Tops</option><option>Bottoms</option><option>Dresses</option>
            <option>Jackets</option><option>Shoes</option><option>Accessories</option>
          </select>
        </div>
        <div class="form-group">
          <label class="form-label">Size</label>
          <select class="form-select">
            <option>XS</option><option>S</option><option>M</option><option>L</option><option>XL</option><option>XXL</option>
          </select>
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Price (₹)</label>
          <input class="form-input" placeholder="500" type="number" id="itemPrice">
        </div>
        <div class="form-group">
          <label class="form-label">Condition</label>
          <select class="form-select">
            <option>Excellent</option><option>Good</option><option>Fair</option>
          </select>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Description</label>
        <textarea class="form-textarea" placeholder="Describe the item, any flaws, brand, etc."></textarea>
      </div>
      <button class="btn-white" onclick="handleListItem()">🚀 List My Item</button>
    </div>
  </div>
</div>

<!-- TESTIMONIALS -->
<section class="testimonials" id="reviews">
  <div class="section-label">Community Love</div>
  <div class="section-title">What Our Users Say</div>
  <div class="testimonials-grid">
    <div class="testimonial-card">
      <div class="stars">★★★★★</div>
      <div class="testimonial-text">"Sold 15 items in my first month and made over ₹8,000! The process is super smooth and buyers are genuinely nice."</div>
      <div class="reviewer">
        <div class="reviewer-avatar">👩</div>
        <div><div class="reviewer-name">Priya S.</div><div class="reviewer-loc">Mumbai, MH</div></div>
      </div>
    </div>
    <div class="testimonial-card">
      <div class="stars">★★★★★</div>
      <div class="testimonial-text">"Found a barely-used Levi's jacket for just ₹600. Would've paid ₹3,000 new. ThreadSwap is honestly a goldmine."</div>
      <div class="reviewer">
        <div class="reviewer-avatar">👨</div>
        <div><div class="reviewer-name">Rohan K.</div><div class="reviewer-loc">Nagpur, MH</div></div>
      </div>
    </div>
    <div class="testimonial-card">
      <div class="stars">★★★★☆</div>
      <div class="testimonial-text">"Love that I'm reducing waste while refreshing my wardrobe. Payments are fast and secure. Highly recommend!"</div>
      <div class="reviewer">
        <div class="reviewer-avatar">👩</div>
        <div><div class="reviewer-name">Ayesha M.</div><div class="reviewer-loc">Pune, MH</div></div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">Thread<span>Swap</span></div>
  <div class="footer-tagline">Fashion's second chance — and yours to grab.</div>
  <div class="footer-links">
    <a href="#">About</a><a href="#">How it Works</a><a href="#">Safety</a>
    <a href="#">Blog</a><a href="#">Help</a><a href="#">Contact</a>
  </div>
  <div class="footer-copy">© 2026 ThreadSwap. All rights reserved. Built with ♻️ and ❤️</div>
</footer>

<!-- CART MODAL -->
<div class="modal-overlay" id="cartModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('cartModal')">✕</button>
    <div class="modal-title">🛒 Your Cart</div>
    <div id="cartItems" style="min-height:80px"></div>
    <div id="cartTotal" style="margin-top:1rem;font-weight:700;font-size:1.1rem;border-top:1px solid #eee;padding-top:1rem"></div>
    <button class="btn btn-primary" style="width:100%;margin-top:1.2rem;padding:0.9rem;font-size:1rem" onclick="checkout()">Proceed to Checkout →</button>
  </div>
</div>

<!-- LOGIN MODAL -->
<div class="modal-overlay" id="loginModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('loginModal')">✕</button>
    <div class="modal-title">Welcome Back 👋</div>
    <div class="form-group" style="margin-bottom:1rem">
      <label style="display:block;font-size:0.85rem;font-weight:600;margin-bottom:0.4rem">Email</label>
      <input style="width:100%;padding:0.75rem;border:1.5px solid #e0d5c4;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.9rem;outline:none" placeholder="you@email.com" type="email">
    </div>
    <div class="form-group" style="margin-bottom:1.5rem">
      <label style="display:block;font-size:0.85rem;font-weight:600;margin-bottom:0.4rem">Password</label>
      <input style="width:100%;padding:0.75rem;border:1.5px solid #e0d5c4;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.9rem;outline:none" placeholder="••••••••" type="password">
    </div>
    <button class="btn btn-primary" style="width:100%;padding:0.9rem;font-size:1rem" onclick="showToast('✅ Logged in successfully!');closeModal('loginModal')">Log In</button>
    <p style="text-align:center;margin-top:1rem;font-size:0.85rem;color:#8a7968">Don't have an account? <a href="#" onclick="closeModal('loginModal');openSignup()" style="color:var(--rust);font-weight:600">Sign up</a></p>
  </div>
</div>

<!-- SIGNUP MODAL -->
<div class="modal-overlay" id="signupModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('signupModal')">✕</button>
    <div class="modal-title">Join ThreadSwap 🌿</div>
    <div style="display:flex;gap:1rem">
      <div class="form-group" style="flex:1;margin-bottom:1rem">
        <label style="display:block;font-size:0.85rem;font-weight:600;margin-bottom:0.4rem">First Name</label>
        <input style="width:100%;padding:0.75rem;border:1.5px solid #e0d5c4;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.9rem;outline:none" placeholder="Priya">
      </div>
      <div class="form-group" style="flex:1;margin-bottom:1rem">
        <label style="display:block;font-size:0.85rem;font-weight:600;margin-bottom:0.4rem">Last Name</label>
        <input style="width:100%;padding:0.75rem;border:1.5px solid #e0d5c4;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.9rem;outline:none" placeholder="Sharma">
      </div>
    </div>
    <div class="form-group" style="margin-bottom:1rem">
      <label style="display:block;font-size:0.85rem;font-weight:600;margin-bottom:0.4rem">Email</label>
      <input style="width:100%;padding:0.75rem;border:1.5px solid #e0d5c4;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.9rem;outline:none" placeholder="you@email.com" type="email">
    </div>
    <div class="form-group" style="margin-bottom:1.5rem">
      <label style="display:block;font-size:0.85rem;font-weight:600;margin-bottom:0.4rem">Password</label>
      <input style="width:100%;padding:0.75rem;border:1.5px solid #e0d5c4;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.9rem;outline:none" placeholder="••••••••" type="password">
    </div>
    <button class="btn btn-primary" style="width:100%;padding:0.9rem;font-size:1rem" onclick="showToast('🎉 Account created! Welcome to ThreadSwap!');closeModal('signupModal')">Create Account</button>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<script>
  // ─── DATA ───
  const products = [
    { id:1, name:'Floral Midi Dress', brand:'Zara', emoji:'👗', size:'M', price:650, orig:2200, condition:'Excellent', category:'dresses', badge:'Hot' },
    { id:2, name:'Classic Denim Jacket', brand:'Levi\'s', emoji:'🧥', size:'L', price:950, orig:3500, condition:'Good', category:'jackets', badge:'New' },
    { id:3, name:'White Linen Shirt', brand:'H&M', emoji:'👕', size:'S', price:280, orig:900, condition:'Excellent', category:'tops', badge:'' },
    { id:4, name:'High-Waist Jeans', brand:'Mango', emoji:'👖', size:'M', price:750, orig:2800, condition:'Good', category:'bottoms', badge:'Hot' },
    { id:5, name:'Nike Air Sneakers', brand:'Nike', emoji:'👟', size:'42', price:1200, orig:4500, condition:'Good', category:'shoes', badge:'' },
    { id:6, name:'Boho Maxi Skirt', brand:'FabIndia', emoji:'🩱', size:'XL', price:420, orig:1400, condition:'Excellent', category:'bottoms', badge:'New' },
    { id:7, name:'Leather Tote Bag', brand:'Coach', emoji:'👜', size:'One Size', price:1800, orig:7000, condition:'Good', category:'accessories', badge:'' },
    { id:8, name:'Vintage Band Tee', brand:'Unbranded', emoji:'👕', size:'L', price:190, orig:600, condition:'Fair', category:'tops', badge:'' },
    { id:9, name:'Trench Coat', brand:'Marks & Spencer', emoji:'🧥', size:'M', price:1500, orig:5500, condition:'Excellent', category:'jackets', badge:'New' },
    { id:10, name:'Silk Blouse', brand:'Tommy Hilfiger', emoji:'👚', size:'S', price:560, orig:2000, condition:'Good', category:'tops', badge:'' },
    { id:11, name:'Formal Oxford Shoes', brand:'Clarks', emoji:'👞', size:'43', price:1100, orig:4200, condition:'Good', category:'shoes', badge:'Hot' },
    { id:12, name:'Floral Scrunchie Set', brand:'Various', emoji:'🎀', size:'One Size', price:99, orig:350, condition:'Excellent', category:'accessories', badge:'' },
  ];

  let cart = [];
  let activeCategory = 'all';

  // ─── RENDER PRODUCTS ───
  function conditionColor(c) {
    if(c==='Excellent') return 'cond-excellent';
    if(c==='Good') return 'cond-good';
    return 'cond-fair';
  }

  function renderProducts(list) {
    const grid = document.getElementById('productsGrid');
    if(!list.length) { grid.innerHTML = '<p style="color:var(--text-muted);grid-column:1/-1">No items found. Try adjusting your filters.</p>'; return; }
    grid.innerHTML = list.map(p => `
      <div class="product-card">
        <div class="product-img">
          ${p.badge ? `<div class="product-badge ${p.badge==='New'?'badge-new':p.badge==='Hot'?'badge-hot':''}">${p.badge}</div>` : ''}
          <button class="wishlist-btn" onclick="toggleWishlist(this)">🤍</button>
          ${p.emoji}
        </div>
        <div class="product-info">
          <div class="product-brand">${p.brand}</div>
          <div class="product-name">${p.name}</div>
          <div class="condition-label"><span class="condition-dot ${conditionColor(p.condition)}"></span>${p.condition} · Size ${p.size}</div>
          <div class="product-footer">
            <div><span class="product-price">₹${p.price.toLocaleString()}</span><span class="original-price">₹${p.orig.toLocaleString()}</span></div>
            <button class="add-cart-btn" onclick="addToCart(${p.id})">+ Cart</button>
          </div>
        </div>
      </div>
    `).join('');
  }

  function setCategory(btn, cat) {
    document.querySelectorAll('.cat-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    activeCategory = cat;
    filterProducts();
  }

  function filterProducts() {
    const q = document.getElementById('searchInput').value.toLowerCase();
    const size = document.getElementById('sizeFilter').value;
    const cond = document.getElementById('condFilter').value;
    const priceRange = document.getElementById('priceFilter').value;

    let filtered = products.filter(p => {
      const matchCat = activeCategory === 'all' || p.category === activeCategory;
      const matchQ = !q || p.name.toLowerCase().includes(q) || p.brand.toLowerCase().includes(q);
      const matchSize = !size || p.size === size;
      const matchCond = !cond || p.condition === cond;
      const matchPrice = !priceRange ||
        (priceRange==='low' && p.price < 500) ||
        (priceRange==='mid' && p.price >= 500 && p.price <= 1500) ||
        (priceRange==='high' && p.price > 1500);
      return matchCat && matchQ && matchSize && matchCond && matchPrice;
    });
    renderProducts(filtered);
  }

  // ─── CART ───
  function addToCart(id) {
    const p = products.find(x => x.id === id);
    const existing = cart.find(x => x.id === id);
    if(existing) existing.qty++;
    else cart.push({...p, qty: 1});
    updateCartBadge();
    showToast(`✅ ${p.name} added to cart!`);
  }

  function updateCartBadge() {
    const total = cart.reduce((s,i) => s + i.qty, 0);
    document.getElementById('cartBadge').textContent = total;
  }

  function openCart() {
    const cartItems = document.getElementById('cartItems');
    const cartTotal = document.getElementById('cartTotal');
    if(!cart.length) {
      cartItems.innerHTML = '<p style="color:var(--text-muted);text-align:center;padding:1.5rem 0">Your cart is empty 🛒<br><small>Browse listings to add items!</small></p>';
      cartTotal.innerHTML = '';
    } else {
      cartItems.innerHTML = cart.map(i => `
        <div style="display:flex;align-items:center;gap:1rem;padding:0.8rem 0;border-bottom:1px solid #f0ece4">
          <div style="font-size:2rem">${i.emoji}</div>
          <div style="flex:1">
            <div style="font-weight:600;font-size:0.9rem">${i.name}</div>
            <div style="font-size:0.78rem;color:var(--text-muted)">${i.brand} · Size ${i.size}</div>
          </div>
          <div style="font-weight:700">₹${(i.price*i.qty).toLocaleString()}</div>
          <button onclick="removeFromCart(${i.id})" style="background:none;border:none;color:var(--text-muted);cursor:pointer;font-size:1.1rem">✕</button>
        </div>
      `).join('');
      const total = cart.reduce((s,i) => s + i.price*i.qty, 0);
      cartTotal.innerHTML = `Total: ₹${total.toLocaleString()} <span style="font-size:0.8rem;color:var(--text-muted);font-weight:400">(incl. all taxes)</span>`;
    }
    document.getElementById('cartModal').classList.add('active');
  }

  function removeFromCart(id) {
    cart = cart.filter(i => i.id !== id);
    updateCartBadge();
    openCart();
  }

  function checkout() {
    if(!cart.length) { showToast('🛒 Your cart is empty!'); return; }
    cart = [];
    updateCartBadge();
    closeModal('cartModal');
    showToast('🎉 Order placed! Check your email for confirmation.');
  }

  // ─── SELL ───
  function handleListItem() {
    const name = document.getElementById('itemName').value;
    const price = document.getElementById('itemPrice').value;
    if(!name || !price) { showToast('⚠️ Please fill in item name and price.'); return; }
    showToast(`✅ "${name}" listed for ₹${price}!`);
    document.getElementById('itemName').value = '';
    document.getElementById('itemPrice').value = '';
  }

  // ─── WISHLIST ───
  function toggleWishlist(btn) {
    if(btn.textContent === '🤍') { btn.textContent = '❤️'; showToast('❤️ Added to wishlist!'); }
    else { btn.textContent = '🤍'; showToast('Removed from wishlist.'); }
  }

  // ─── MODALS ───
  function openLogin() { document.getElementById('loginModal').classList.add('active'); }
  function openSignup() { document.getElementById('signupModal').classList.add('active'); }
  function closeModal(id) { document.getElementById(id).classList.remove('active'); }

  document.querySelectorAll('.modal-overlay').forEach(o => {
    o.addEventListener('click', e => { if(e.target === o) o.classList.remove('active'); });
  });

  // ─── TOAST ───
  function showToast(msg) {
    const t = document.getElementById('toast');
    t.textContent = msg;
    t.classList.add('show');
    clearTimeout(t._timer);
    t._timer = setTimeout(() => t.classList.remove('show'), 3000);
  }

  // ─── INIT ───
  renderProducts(products);
</script>
</body>
</html>
