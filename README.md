<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>ShopNova — Premium Store</title>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600;700&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #0c0c0e;
      --surface: #141416;
      --card: #1a1a1e;
      --border: #2a2a30;
      --gold: #c9a84c;
      --gold-light: #e8c97a;
      --text: #f0ece4;
      --muted: #888890;
      --white: #ffffff;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'DM Sans', sans-serif;
      font-weight: 300;
      overflow-x: hidden;
    }

    /* ── SCROLLBAR ── */
    ::-webkit-scrollbar { width: 6px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--gold); border-radius: 3px; }

    /* ── NAVBAR ── */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 20px 60px;
      background: rgba(12,12,14,0.85);
      backdrop-filter: blur(20px);
      border-bottom: 1px solid var(--border);
      animation: slideDown 0.6s ease;
    }
    @keyframes slideDown { from { transform: translateY(-100%); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

    .logo {
      font-family: 'Cormorant Garamond', serif;
      font-size: 28px; font-weight: 700; letter-spacing: 2px;
      color: var(--gold);
      text-decoration: none;
    }
    .logo span { color: var(--text); }

    .nav-links { display: flex; gap: 36px; list-style: none; }
    .nav-links a {
      color: var(--muted); text-decoration: none;
      font-size: 13px; letter-spacing: 1.5px; text-transform: uppercase;
      transition: color 0.3s;
      position: relative;
    }
    .nav-links a::after {
      content: ''; position: absolute; bottom: -4px; left: 0;
      width: 0; height: 1px; background: var(--gold);
      transition: width 0.3s;
    }
    .nav-links a:hover { color: var(--gold); }
    .nav-links a:hover::after { width: 100%; }

    .nav-actions { display: flex; align-items: center; gap: 20px; }

    .search-box {
      display: flex; align-items: center; gap: 8px;
      background: var(--surface); border: 1px solid var(--border);
      padding: 8px 14px; border-radius: 6px;
    }
    .search-box input {
      background: none; border: none; outline: none;
      color: var(--text); font-family: 'DM Sans', sans-serif;
      font-size: 13px; width: 160px;
    }
    .search-box input::placeholder { color: var(--muted); }
    .search-box svg { color: var(--muted); flex-shrink: 0; }

    .cart-btn {
      position: relative; background: none; border: none; cursor: pointer;
      color: var(--text); padding: 6px; transition: color 0.3s;
    }
    .cart-btn:hover { color: var(--gold); }
    .cart-count {
      position: absolute; top: -4px; right: -4px;
      background: var(--gold); color: #000;
      width: 18px; height: 18px; border-radius: 50%;
      font-size: 10px; font-weight: 700;
      display: flex; align-items: center; justify-content: center;
    }

    /* ── HERO ── */
    .hero {
      min-height: 100vh;
      display: flex; align-items: center;
      padding: 120px 60px 80px;
      position: relative; overflow: hidden;
    }
    .hero-bg {
      position: absolute; inset: 0; z-index: 0;
      background: radial-gradient(ellipse 60% 80% at 70% 50%, rgba(201,168,76,0.08) 0%, transparent 70%),
                  radial-gradient(ellipse 40% 40% at 20% 80%, rgba(201,168,76,0.05) 0%, transparent 60%);
    }
    .hero-grid {
      position: absolute; inset: 0; z-index: 0; opacity: 0.04;
      background-image: linear-gradient(var(--border) 1px, transparent 1px),
                        linear-gradient(90deg, var(--border) 1px, transparent 1px);
      background-size: 60px 60px;
    }
    .hero-content { position: relative; z-index: 1; max-width: 600px; }
    .hero-tag {
      display: inline-flex; align-items: center; gap: 8px;
      background: rgba(201,168,76,0.12); border: 1px solid rgba(201,168,76,0.3);
      padding: 6px 14px; border-radius: 20px;
      font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--gold);
      margin-bottom: 28px;
      animation: fadeUp 0.8s ease 0.2s both;
    }
    .hero-tag::before { content: '◆'; font-size: 8px; }
    .hero h1 {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(52px, 7vw, 88px); font-weight: 600; line-height: 1.05;
      margin-bottom: 24px;
      animation: fadeUp 0.8s ease 0.35s both;
    }
    .hero h1 em { color: var(--gold); font-style: italic; }
    .hero p {
      font-size: 16px; line-height: 1.8; color: var(--muted);
      max-width: 420px; margin-bottom: 40px;
      animation: fadeUp 0.8s ease 0.5s both;
    }
    .hero-btns { display: flex; gap: 16px; animation: fadeUp 0.8s ease 0.65s both; }

    .btn-primary {
      padding: 14px 32px; background: var(--gold); color: #000;
      border: none; border-radius: 4px; cursor: pointer;
      font-family: 'DM Sans', sans-serif; font-size: 13px;
      font-weight: 500; letter-spacing: 1px; text-transform: uppercase;
      transition: all 0.3s;
    }
    .btn-primary:hover { background: var(--gold-light); transform: translateY(-2px); box-shadow: 0 8px 24px rgba(201,168,76,0.3); }

    .btn-outline {
      padding: 14px 32px; background: transparent; color: var(--text);
      border: 1px solid var(--border); border-radius: 4px; cursor: pointer;
      font-family: 'DM Sans', sans-serif; font-size: 13px;
      font-weight: 400; letter-spacing: 1px; text-transform: uppercase;
      transition: all 0.3s; text-decoration: none; display: inline-flex; align-items: center;
    }
    .btn-outline:hover { border-color: var(--gold); color: var(--gold); }

    .hero-stats {
      position: absolute; right: 60px; bottom: 80px; z-index: 1;
      display: flex; gap: 48px;
      animation: fadeUp 0.8s ease 0.8s both;
    }
    .stat { text-align: center; }
    .stat-num {
      font-family: 'Cormorant Garamond', serif;
      font-size: 36px; font-weight: 700; color: var(--gold);
    }
    .stat-label { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--muted); }

    @keyframes fadeUp { from { transform: translateY(30px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

    /* ── SECTION ── */
    section { padding: 100px 60px; }

    .section-header { text-align: center; margin-bottom: 60px; }
    .section-tag {
      font-size: 11px; letter-spacing: 3px; text-transform: uppercase;
      color: var(--gold); margin-bottom: 12px;
    }
    .section-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(32px, 4vw, 52px); font-weight: 600; line-height: 1.1;
    }
    .section-title em { color: var(--gold); font-style: italic; }

    /* ── CATEGORIES ── */
    .categories { background: var(--surface); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
    .cat-grid {
      display: grid; grid-template-columns: repeat(4, 1fr); gap: 1px;
      background: var(--border);
    }
    .cat-item {
      background: var(--surface); padding: 36px 28px;
      display: flex; flex-direction: column; align-items: center; gap: 12px;
      cursor: pointer; transition: background 0.3s;
      text-align: center;
    }
    .cat-item:hover { background: var(--card); }
    .cat-item:hover .cat-icon { color: var(--gold); transform: scale(1.15); }
    .cat-icon { font-size: 32px; transition: all 0.3s; }
    .cat-name { font-size: 13px; letter-spacing: 1.5px; text-transform: uppercase; font-weight: 500; }
    .cat-count { font-size: 12px; color: var(--muted); }

    /* ── PRODUCTS ── */
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 24px;
    }

    .product-card {
      background: var(--card); border: 1px solid var(--border);
      border-radius: 8px; overflow: hidden;
      transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
      animation: fadeUp 0.6s ease both;
    }
    .product-card:hover {
      transform: translateY(-6px);
      border-color: rgba(201,168,76,0.3);
      box-shadow: 0 20px 40px rgba(0,0,0,0.4);
    }
    .product-card:nth-child(1) { animation-delay: 0.1s; }
    .product-card:nth-child(2) { animation-delay: 0.2s; }
    .product-card:nth-child(3) { animation-delay: 0.3s; }
    .product-card:nth-child(4) { animation-delay: 0.4s; }
    .product-card:nth-child(5) { animation-delay: 0.5s; }
    .product-card:nth-child(6) { animation-delay: 0.6s; }

    .product-img {
      width: 100%; height: 220px; object-fit: cover;
      background: var(--surface);
      display: flex; align-items: center; justify-content: center;
      font-size: 64px; position: relative; overflow: hidden;
    }
    .product-img::after {
      content: ''; position: absolute; inset: 0;
      background: linear-gradient(to bottom, transparent 50%, rgba(0,0,0,0.4));
    }
    .badge {
      position: absolute; top: 12px; left: 12px; z-index: 1;
      background: var(--gold); color: #000;
      font-size: 10px; font-weight: 700; letter-spacing: 1px; text-transform: uppercase;
      padding: 4px 10px; border-radius: 2px;
    }
    .badge.new { background: #3a7d44; color: #fff; }
    .badge.hot { background: #b83232; color: #fff; }

    .wishlist-btn {
      position: absolute; top: 12px; right: 12px; z-index: 1;
      background: rgba(0,0,0,0.5); border: 1px solid var(--border);
      width: 34px; height: 34px; border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      cursor: pointer; color: var(--muted); transition: all 0.3s; font-size: 16px;
    }
    .wishlist-btn:hover { background: rgba(201,168,76,0.2); color: var(--gold); border-color: var(--gold); }
    .wishlist-btn.active { color: #e74c3c; }

    .product-info { padding: 20px; }
    .product-category { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--muted); margin-bottom: 6px; }
    .product-name { font-family: 'Cormorant Garamond', serif; font-size: 20px; font-weight: 600; margin-bottom: 8px; line-height: 1.2; }
    .product-rating { display: flex; align-items: center; gap: 6px; margin-bottom: 14px; }
    .stars { color: var(--gold); font-size: 13px; letter-spacing: 2px; }
    .rating-count { font-size: 12px; color: var(--muted); }

    .product-footer { display: flex; align-items: center; justify-content: space-between; }
    .price { font-family: 'Cormorant Garamond', serif; font-size: 24px; font-weight: 700; color: var(--gold); }
    .old-price { font-size: 14px; color: var(--muted); text-decoration: line-through; margin-left: 6px; font-family: 'DM Sans', sans-serif; font-weight: 300; }

    .add-cart-btn {
      background: transparent; border: 1px solid var(--gold); color: var(--gold);
      padding: 8px 18px; border-radius: 4px; cursor: pointer;
      font-family: 'DM Sans', sans-serif; font-size: 12px;
      font-weight: 500; letter-spacing: 1px; text-transform: uppercase;
      transition: all 0.3s;
    }
    .add-cart-btn:hover { background: var(--gold); color: #000; }
    .add-cart-btn.added { background: var(--gold); color: #000; }

    /* ── BANNER ── */
    .banner {
      background: var(--surface); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
      padding: 80px 60px;
    }
    .banner-inner {
      background: linear-gradient(135deg, rgba(201,168,76,0.08) 0%, transparent 60%);
      border: 1px solid rgba(201,168,76,0.2);
      border-radius: 12px; padding: 60px;
      display: flex; align-items: center; justify-content: space-between; gap: 40px;
    }
    .banner-text h2 { font-family: 'Cormorant Garamond', serif; font-size: 42px; font-weight: 600; margin-bottom: 12px; }
    .banner-text h2 em { color: var(--gold); font-style: italic; }
    .banner-text p { color: var(--muted); font-size: 15px; max-width: 400px; line-height: 1.7; }
    .banner-offer {
      text-align: center; flex-shrink: 0;
      background: rgba(201,168,76,0.1); border: 1px solid rgba(201,168,76,0.3);
      padding: 30px 40px; border-radius: 8px;
    }
    .offer-pct {
      font-family: 'Cormorant Garamond', serif;
      font-size: 64px; font-weight: 700; color: var(--gold); line-height: 1;
    }
    .offer-label { font-size: 11px; letter-spacing: 3px; text-transform: uppercase; color: var(--muted); }
    .offer-code {
      margin-top: 12px; background: var(--bg); border: 1px dashed var(--gold);
      padding: 6px 16px; border-radius: 4px; font-size: 13px;
      letter-spacing: 3px; color: var(--gold); font-weight: 500;
    }

    /* ── FEATURES ── */
    .features { background: var(--surface); border-top: 1px solid var(--border); }
    .features-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1px; background: var(--border); }
    .feature {
      background: var(--surface); padding: 36px 28px; text-align: center;
      transition: background 0.3s;
    }
    .feature:hover { background: var(--card); }
    .feature-icon { font-size: 28px; margin-bottom: 12px; }
    .feature-name { font-size: 14px; font-weight: 500; margin-bottom: 6px; }
    .feature-desc { font-size: 12px; color: var(--muted); line-height: 1.6; }

    /* ── FOOTER ── */
    footer {
      background: var(--surface); border-top: 1px solid var(--border);
      padding: 60px 60px 30px;
    }
    .footer-top { display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 60px; margin-bottom: 40px; }
    .footer-brand .logo { display: block; margin-bottom: 16px; }
    .footer-brand p { color: var(--muted); font-size: 13px; line-height: 1.8; max-width: 260px; }
    .footer-col h4 { font-size: 11px; letter-spacing: 2.5px; text-transform: uppercase; color: var(--gold); margin-bottom: 16px; }
    .footer-col ul { list-style: none; }
    .footer-col ul li { margin-bottom: 10px; }
    .footer-col ul a { color: var(--muted); text-decoration: none; font-size: 13px; transition: color 0.3s; }
    .footer-col ul a:hover { color: var(--text); }
    .footer-bottom { border-top: 1px solid var(--border); padding-top: 24px; display: flex; justify-content: space-between; align-items: center; }
    .footer-bottom p { font-size: 12px; color: var(--muted); }
    .footer-socials { display: flex; gap: 16px; }
    .social-link {
      width: 34px; height: 34px; background: var(--card); border: 1px solid var(--border);
      border-radius: 50%; display: flex; align-items: center; justify-content: center;
      color: var(--muted); font-size: 14px; text-decoration: none;
      transition: all 0.3s; cursor: pointer;
    }
    .social-link:hover { border-color: var(--gold); color: var(--gold); }

    /* ── CART SIDEBAR ── */
    .overlay {
      position: fixed; inset: 0; background: rgba(0,0,0,0.7);
      z-index: 200; opacity: 0; pointer-events: none; transition: opacity 0.3s;
    }
    .overlay.open { opacity: 1; pointer-events: all; }

    .cart-sidebar {
      position: fixed; top: 0; right: -420px; bottom: 0;
      width: 420px; background: var(--surface);
      border-left: 1px solid var(--border);
      z-index: 201; padding: 0; display: flex; flex-direction: column;
      transition: right 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .cart-sidebar.open { right: 0; }

    .cart-header {
      padding: 24px 28px; border-bottom: 1px solid var(--border);
      display: flex; align-items: center; justify-content: space-between;
    }
    .cart-header h3 { font-family: 'Cormorant Garamond', serif; font-size: 22px; font-weight: 600; }
    .close-btn {
      background: none; border: 1px solid var(--border); color: var(--muted);
      width: 34px; height: 34px; border-radius: 50%; cursor: pointer;
      font-size: 18px; display: flex; align-items: center; justify-content: center;
      transition: all 0.3s;
    }
    .close-btn:hover { border-color: var(--gold); color: var(--gold); }

    .cart-items { flex: 1; overflow-y: auto; padding: 20px 28px; }

    .cart-item {
      display: flex; align-items: center; gap: 16px;
      padding: 16px 0; border-bottom: 1px solid var(--border);
      animation: fadeUp 0.3s ease;
    }
    .cart-item-icon { font-size: 36px; flex-shrink: 0; }
    .cart-item-info { flex: 1; }
    .cart-item-name { font-size: 14px; font-weight: 500; margin-bottom: 4px; }
    .cart-item-price { font-size: 13px; color: var(--gold); }
    .cart-item-qty {
      display: flex; align-items: center; gap: 10px; margin-top: 8px;
    }
    .qty-btn {
      width: 26px; height: 26px; background: var(--card); border: 1px solid var(--border);
      color: var(--text); border-radius: 4px; cursor: pointer; font-size: 14px;
      display: flex; align-items: center; justify-content: center;
      transition: all 0.2s;
    }
    .qty-btn:hover { border-color: var(--gold); color: var(--gold); }
    .qty-num { font-size: 14px; min-width: 20px; text-align: center; }
    .remove-item { background: none; border: none; color: var(--muted); cursor: pointer; font-size: 18px; padding: 4px; transition: color 0.2s; margin-left: auto; }
    .remove-item:hover { color: #e74c3c; }

    .cart-empty {
      text-align: center; padding: 60px 20px; color: var(--muted);
    }
    .cart-empty .empty-icon { font-size: 48px; margin-bottom: 16px; }
    .cart-empty p { font-size: 14px; }

    .cart-footer {
      padding: 20px 28px; border-top: 1px solid var(--border);
      background: var(--surface);
    }
    .cart-subtotal {
      display: flex; justify-content: space-between; align-items: center;
      margin-bottom: 6px;
    }
    .cart-subtotal span { font-size: 13px; color: var(--muted); }
    .cart-subtotal strong { font-family: 'Cormorant Garamond', serif; font-size: 22px; color: var(--gold); }
    .cart-note { font-size: 11px; color: var(--muted); margin-bottom: 16px; }
    .checkout-btn {
      width: 100%; padding: 16px; background: var(--gold); color: #000;
      border: none; border-radius: 4px; cursor: pointer;
      font-family: 'DM Sans', sans-serif; font-size: 13px;
      font-weight: 500; letter-spacing: 2px; text-transform: uppercase;
      transition: all 0.3s;
    }
    .checkout-btn:hover { background: var(--gold-light); }

    /* ── TOAST ── */
    .toast {
      position: fixed; bottom: 30px; left: 50%; transform: translateX(-50%) translateY(80px);
      background: var(--card); border: 1px solid var(--gold);
      padding: 12px 24px; border-radius: 6px;
      font-size: 13px; letter-spacing: 0.5px; color: var(--text);
      z-index: 300; transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
      white-space: nowrap;
    }
    .toast.show { transform: translateX(-50%) translateY(0); }

    /* ── FILTER BAR ── */
    .filter-bar {
      display: flex; align-items: center; justify-content: space-between;
      margin-bottom: 40px; flex-wrap: wrap; gap: 16px;
    }
    .filter-tabs { display: flex; gap: 8px; flex-wrap: wrap; }
    .filter-tab {
      padding: 8px 18px; background: var(--card); border: 1px solid var(--border);
      border-radius: 20px; cursor: pointer; font-size: 12px;
      letter-spacing: 1px; text-transform: uppercase; color: var(--muted);
      transition: all 0.3s;
    }
    .filter-tab:hover, .filter-tab.active {
      background: rgba(201,168,76,0.12); border-color: var(--gold); color: var(--gold);
    }
    .sort-select {
      background: var(--card); border: 1px solid var(--border);
      color: var(--text); padding: 8px 14px; border-radius: 6px;
      font-family: 'DM Sans', sans-serif; font-size: 12px; cursor: pointer; outline: none;
    }
    .sort-select option { background: var(--card); }

    @media (max-width: 900px) {
      nav { padding: 16px 20px; }
      .nav-l