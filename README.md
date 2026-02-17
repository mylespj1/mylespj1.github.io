<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>sam.paints</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Lato:wght@300;400;700&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --clay:    #f5d55a;
      --sage:    #5a9bbf;
      --cream:   #fefaed;
      --bark:    #7a4f3a;
      --stone:   #8a7060;
      --warm-white: #fffdf5;
      --yellow:  #f5d55a;
      --sky:     #5a9bbf;
      --petal:   #e8a0b0;
      --earth:   #7a4f3a;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Lato', sans-serif;
      background: var(--warm-white);
      color: var(--bark);
      font-weight: 300;
    }

    /* ── NAV ── */
    nav {
      position: fixed; top: 0; width: 100%; z-index: 100;
      background: rgba(250,247,242,0.92);
      backdrop-filter: blur(8px);
      border-bottom: 1px solid rgba(46,31,18,0.1);
      display: flex; align-items: center; justify-content: space-between;
      padding: 1rem 3rem;
    }
    .nav-logo {
      font-family: 'Playfair Display', serif;
      font-size: 1.5rem; letter-spacing: 0.03em;
      color: var(--bark); text-decoration: none;
    }
    .nav-links { display: flex; gap: 2.5rem; list-style: none; }
    .nav-links a {
      text-decoration: none; color: var(--stone);
      font-size: 0.85rem; letter-spacing: 0.12em; text-transform: uppercase;
      transition: color 0.3s;
    }
    .nav-links a:hover { color: var(--earth); }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      text-align: center;
      padding: 8rem 2rem 4rem;
      background: 
        radial-gradient(ellipse at 15% 85%, rgba(245,213,90,0.25) 0%, transparent 55%),
        radial-gradient(ellipse at 85% 15%, rgba(90,155,191,0.2) 0%, transparent 55%),
        radial-gradient(ellipse at 60% 60%, rgba(232,160,176,0.12) 0%, transparent 50%),
        var(--warm-white);
    }
    .hero-eyebrow {
      font-size: 0.75rem; letter-spacing: 0.25em; text-transform: uppercase;
      color: var(--sky); margin-bottom: 1.2rem; font-weight: 400;
    }
    .hero-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(3rem, 8vw, 6rem);
      line-height: 1.1;
      color: var(--bark);
      margin-bottom: 1.5rem;
    }
    .hero-title em { color: var(--yellow); font-style: italic; text-shadow: 0 2px 20px rgba(245,213,90,0.3); }
    .hero-sub {
      max-width: 480px; font-size: 1.05rem; line-height: 1.7;
      color: var(--stone); margin-bottom: 2.5rem;
    }
    .btn {
      display: inline-block;
      padding: 0.85rem 2.5rem;
      background: var(--yellow); color: var(--earth);
      font-family: 'Lato', sans-serif;
      font-size: 0.8rem; letter-spacing: 0.15em; text-transform: uppercase;
      text-decoration: none; border: none; cursor: pointer;
      transition: background 0.3s, transform 0.2s;
    }
    .btn:hover { background: var(--earth); color: #fff; transform: translateY(-2px); }
    .btn-outline {
      background: transparent; color: var(--sky);
      border: 1.5px solid var(--sky); margin-left: 1rem;
    }
    .btn-outline:hover { background: var(--sky); color: #fff; }

    .scroll-hint {
      margin-top: 4rem; font-size: 0.75rem; letter-spacing: 0.15em;
      text-transform: uppercase; color: var(--stone); opacity: 0.6;
    }

    /* ── SECTIONS ── */
    section { padding: 6rem 3rem; }
    .section-label {
      font-size: 0.7rem; letter-spacing: 0.25em; text-transform: uppercase;
      color: var(--sky); margin-bottom: 0.75rem;
    }
    .section-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2rem, 4vw, 3rem);
      color: var(--bark); margin-bottom: 1rem;
    }
    .section-desc {
      max-width: 520px; color: var(--stone);
      line-height: 1.75; margin-bottom: 3rem;
    }

    /* ── GALLERY ── */
    #gallery { background: linear-gradient(180deg, #fefaed 0%, #fdf5d0 100%); }
    .gallery-header { text-align: center; margin-bottom: 3rem; }
    .gallery-header .section-desc { margin: 0 auto 3rem; }

    .gallery-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
      gap: 1.2rem;
      max-width: 1200px; margin: 0 auto;
    }
    .gallery-item {
      position: relative; overflow: hidden;
      aspect-ratio: 4/3;
      background: #d9cfc4;
      cursor: pointer;
    }
    .gallery-item img {
      width: 100%; height: 100%; object-fit: cover;
      transition: transform 0.5s ease;
    }
    .gallery-item:hover img { transform: scale(1.06); }
    .gallery-overlay {
      position: absolute; inset: 0;
      background: rgba(46,31,18,0.55);
      display: flex; align-items: flex-end;
      padding: 1.2rem;
      opacity: 0; transition: opacity 0.35s;
    }
    .gallery-item:hover .gallery-overlay { opacity: 1; }
    .gallery-overlay span {
      font-family: 'Playfair Display', serif;
      font-style: italic; color: #fff; font-size: 1.05rem;
    }

    /* Placeholder art tiles */
    .placeholder-art {
      width: 100%; height: 100%;
      display: flex; align-items: center; justify-content: center;
      font-family: 'Playfair Display', serif;
      font-style: italic; color: rgba(46,31,18,0.3);
      font-size: 0.9rem;
    }
    .p1 { background: linear-gradient(135deg, #fae87a 0%, #f0cc30 100%); }
    .p2 { background: linear-gradient(135deg, #7ec0dc 0%, #4a8eb0 100%); }
    .p3 { background: linear-gradient(135deg, #f0c0cc 0%, #d88098 100%); }
    .p4 { background: linear-gradient(135deg, #c8844e 0%, #9a5c30 100%); }
    .p5 { background: linear-gradient(135deg, #fde980 0%, #f0c820 100%); }
    .p6 { background: linear-gradient(135deg, #90c8e8 0%, #5aaac8 100%); }
    .p7 { background: linear-gradient(135deg, #e8b0bc 0%, #cc7888 100%); }
    .p8 { background: linear-gradient(135deg, #b07850 0%, #7a4830 100%); }

    /* ── SCHEDULE ── */
    #schedule { background: linear-gradient(180deg, #eef6fc 0%, #ddeef8 100%); }
    .schedule-container { max-width: 860px; margin: 0 auto; }
    .schedule-grid { display: grid; gap: 1.2rem; }
    .market-card {
      display: grid; grid-template-columns: 80px 1fr auto;
      align-items: center; gap: 1.5rem;
      background: var(--cream);
      padding: 1.5rem 2rem;
      border-left: 3px solid var(--yellow);
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .market-card:hover {
      transform: translateX(4px);
      box-shadow: -4px 0 0 var(--petal), 4px 8px 24px rgba(122,79,58,0.1);
    }
    .market-date {
      text-align: center;
      font-family: 'Playfair Display', serif;
    }
    .market-date .day { font-size: 2rem; font-weight: 700; color: var(--yellow); line-height: 1; }
    .market-date .month { font-size: 0.7rem; letter-spacing: 0.12em; text-transform: uppercase; color: var(--stone); }
    .market-info h3 { font-family: 'Playfair Display', serif; font-size: 1.15rem; margin-bottom: 0.25rem; }
    .market-info p { color: var(--stone); font-size: 0.88rem; }
    .market-time {
      font-size: 0.8rem; letter-spacing: 0.08em;
      color: var(--sky); font-weight: 700; text-align: right;
      white-space: nowrap; background: rgba(90,155,191,0.15); padding: 0.3rem 0.7rem; border-radius: 2px;
    }

    /* ── ABOUT ── */
    #about {
      background: #5a3520;
      color: var(--cream);
    }
    .about-grid {
      max-width: 1000px; margin: 0 auto;
      display: grid; grid-template-columns: 1fr 1fr;
      gap: 5rem; align-items: center;
    }
    .about-image {
      aspect-ratio: 3/4;
      background: linear-gradient(160deg, #f5d55a 0%, #5a9bbf 100%);
      display: flex; align-items: center; justify-content: center;
      font-family: 'Playfair Display', serif;
      font-style: italic; color: rgba(255,255,255,0.4); font-size: 0.9rem;
    }
    #about .section-label { color: var(--yellow); }
    #about .section-title { color: var(--cream); }
    #about .section-desc { color: rgba(246,240,232,0.65); max-width: 100%; margin-bottom: 1.5rem; }
    .about-quote {
      font-family: 'Playfair Display', serif;
      font-style: italic; font-size: 1.2rem;
      color: #e8a0b0; border-left: 3px solid #e8a0b0;
      padding-left: 1.2rem; margin: 1.5rem 0;
      line-height: 1.6;
    }

    /* ── CONTACT ── */
    #contact { background: linear-gradient(180deg, #fffdf0 0%, #fef8d5 100%); }
    .contact-container { max-width: 800px; margin: 0 auto; text-align: center; }
    .social-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 1.2rem; margin: 3rem 0;
    }
    .social-card {
      padding: 2rem 1.5rem;
      border: 1.5px solid rgba(46,31,18,0.12);
      background: var(--warm-white);
      text-decoration: none; color: var(--bark);
      display: flex; flex-direction: column;
      align-items: center; gap: 0.75rem;
      transition: border-color 0.3s, transform 0.2s, box-shadow 0.2s;
    }
    .social-card:hover {
      border-color: var(--sky);
      transform: translateY(-4px);
      box-shadow: 0 8px 28px rgba(46,31,18,0.1);
    }
    .social-icon { font-size: 2rem; }
    .social-card h3 { font-family: 'Playfair Display', serif; font-size: 1.1rem; }
    .social-card p { font-size: 0.82rem; color: var(--stone); }

    .contact-email {
      display: inline-flex; align-items: center; gap: 0.6rem;
      font-size: 1rem; color: var(--earth); text-decoration: none;
      border-bottom: 1px solid var(--petal);
      padding-bottom: 2px;
      transition: color 0.3s;
    }
    .contact-email:hover { color: var(--sky); border-color: var(--sky); }

    /* ── FOOTER ── */
    footer {
      background: #3a2010; color: #a09080;
      text-align: center; padding: 2.5rem;
      font-size: 0.8rem; letter-spacing: 0.06em;
    }
    footer span { color: var(--yellow); text-shadow: 0 0 20px rgba(245,213,90,0.4); }

    /* ── LIGHTBOX ── */
    .lightbox {
      display: none; position: fixed; inset: 0;
      background: rgba(0,0,0,0.88); z-index: 999;
      align-items: center; justify-content: center;
    }
    .lightbox.active { display: flex; }
    .lightbox img { max-width: 90vw; max-height: 85vh; object-fit: contain; }
    .lightbox-close {
      position: absolute; top: 1.5rem; right: 2rem;
      font-size: 2rem; color: #fff; cursor: pointer; line-height: 1;
    }

    /* ── MOBILE ── */
    @media (max-width: 768px) {
      nav { padding: 1rem 1.5rem; }
      .nav-links { gap: 1.2rem; }
      section { padding: 4rem 1.5rem; }
      .about-grid { grid-template-columns: 1fr; gap: 2.5rem; }
      .about-image { display: none; }
      .market-card { grid-template-columns: 60px 1fr; }
      .market-time { grid-column: 2; }
    }

    /* ── ANIMATIONS ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    .hero-eyebrow { animation: fadeUp 0.7s ease both; }
    .hero-title   { animation: fadeUp 0.7s 0.15s ease both; }
    .hero-sub     { animation: fadeUp 0.7s 0.3s ease both; }
    .hero-ctas    { animation: fadeUp 0.7s 0.45s ease both; }
  </style>
</head>
<body>

<!-- NAV -->
<nav>
  <a class="nav-logo" href="#hero">sam.paints</a>
  <ul class="nav-links">
    <li><a href="#gallery">Gallery</a></li>
    <li><a href="#schedule">Markets</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <p class="hero-eyebrow">sam.paints · Handmade Art · Farm Fresh</p>
  <h1 class="hero-title">Made with<br><em>roots & heart</em></h1>
  <p class="hero-sub">Original paintings, prints, and handcrafted pieces inspired by the natural world — found at farmers markets near you.</p>
  <div class="hero-ctas">
    <a class="btn" href="#gallery">View Gallery</a>
    <a class="btn btn-outline" href="#schedule">Find Me This Weekend</a>
  </div>
  <p class="scroll-hint">↓ Scroll to explore</p>
</section>

<!-- GALLERY -->
<section id="gallery">
  <div class="gallery-header">
    <p class="section-label">Portfolio</p>
    <h2 class="section-title">Original Works</h2>
    <p class="section-desc">Each piece is one-of-a-kind, made in my home studio. Click any image to view it larger.</p>
  </div>
  <div class="gallery-grid" id="galleryGrid">
    <!-- Replace src values with your own image paths, e.g. src="images/painting1.jpg" -->
    <div class="gallery-item" onclick="openLightbox(this)">
      <div class="placeholder-art p1">Your Photo Here</div>
      <div class="gallery-overlay"><span>Morning Meadow</span></div>
    </div>
    <div class="gallery-item" onclick="openLightbox(this)">
      <div class="placeholder-art p2">Your Photo Here</div>
      <div class="gallery-overlay"><span>Forest Study No. 3</span></div>
    </div>
    <div class="gallery-item" onclick="openLightbox(this)">
      <div class="placeholder-art p3">Your Photo Here</div>
      <div class="gallery-overlay"><span>Golden Hour</span></div>
    </div>
    <div class="gallery-item" onclick="openLightbox(this)">
      <div class="placeholder-art p4">Your Photo Here</div>
      <div class="gallery-overlay"><span>Wild Herbs</span></div>
    </div>
    <div class="gallery-item" onclick="openLightbox(this)">
      <div class="placeholder-art p5">Your Photo Here</div>
      <div class="gallery-overlay"><span>Harvest Still Life</span></div>
    </div>
    <div class="gallery-item" onclick="openLightbox(this)">
      <div class="placeholder-art p6">Your Photo Here</div>
      <div class="gallery-overlay"><span>Birch & Lichen</span></div>
    </div>
    <div class="gallery-item" onclick="openLightbox(this)">
      <div class="placeholder-art p7">Your Photo Here</div>
      <div class="gallery-overlay"><span>Late Summer</span></div>
    </div>
    <div class="gallery-item" onclick="openLightbox(this)">
      <div class="placeholder-art p8">Your Photo Here</div>
      <div class="gallery-overlay"><span>Tidal Pool</span></div>
    </div>
  </div>
</section>

<!-- SCHEDULE -->
<section id="schedule">
  <div class="schedule-container">
    <p class="section-label">Find Me</p>
    <h2 class="section-title">Farmers Market Schedule</h2>
    <p class="section-desc">Come say hello! I set up my booth at local markets throughout the season. Check back often — I update this regularly.</p>

    <div class="schedule-grid">
      <div class="market-card">
        <div class="market-date"><div class="day">15</div><div class="month">Mar</div></div>
        <div class="market-info">
          <h3>Downtown Provo Market</h3>
          <p>100 N University Ave, Provo, UT · Booth #12</p>
        </div>
        <div class="market-time">8 AM – 1 PM</div>
      </div>
      <div class="market-card">
        <div class="market-date"><div class="day">22</div><div class="month">Mar</div></div>
        <div class="market-info">
          <h3>Springville Art Market</h3>
          <p>200 S Main St, Springville, UT</p>
        </div>
        <div class="market-time">9 AM – 2 PM</div>
      </div>
      <div class="market-card">
        <div class="market-date"><div class="day">5</div><div class="month">Apr</div></div>
        <div class="market-info">
          <h3>Thanksgiving Point Market</h3>
          <p>3003 N Thanksgiving Way, Lehi, UT</p>
        </div>
        <div class="market-time">8 AM – 12 PM</div>
      </div>
      <div class="market-card">
        <div class="market-date"><div class="day">19</div><div class="month">Apr</div></div>
        <div class="market-info">
          <h3>Orem Farmers Market</h3>
          <p>Center St & State St, Orem, UT · Near the fountain</p>
        </div>
        <div class="market-time">7 AM – 1 PM</div>
      </div>
      <div class="market-card">
        <div class="market-date"><div class="day">3</div><div class="month">May</div></div>
        <div class="market-info">
          <h3>Spanish Fork Market Days</h3>
          <p>80 N Main St, Spanish Fork, UT</p>
        </div>
        <div class="market-time">9 AM – 2 PM</div>
      </div>
    </div>

    <p style="margin-top:2rem; color:var(--stone); font-size:0.85rem;">
      ✦ Follow on Instagram for last-minute pop-ups and schedule changes.
    </p>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-grid">
    <div class="about-image">Your Photo Here</div>
    <div>
      <p class="section-label">The Artist</p>
      <h2 class="section-title">Hi, I'm [Your Name]</h2>
      <p class="section-desc">I'm a self-taught artist based in Utah, creating work that celebrates the quiet beauty of the natural world — weathered wood, wildflowers, and the colors of the changing seasons.</p>
      <blockquote class="about-quote">"Every piece I make starts with a long walk and ends with paint-stained hands."</blockquote>
      <p class="section-desc">My work is sold exclusively at farmers markets and through commissions. I love connecting with people in person — come find me at a market and let's talk art!</p>
      <a class="btn" href="#contact" style="margin-top:0.5rem;">Get In Touch</a>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-container">
    <p class="section-label">Stay Connected</p>
    <h2 class="section-title">Find Me Online</h2>
    <p class="section-desc" style="margin:0 auto 0.5rem;">Follow along for new work, market updates, and behind-the-scenes from the studio.</p>

    <div class="social-grid">
      <a class="social-card" href="https://instagram.com/sam.paints" target="_blank">
        <div class="social-icon">📸</div>
        <h3>Instagram</h3>
        <p>@sam.paints</p>
      </a>
      <a class="social-card" href="https://facebook.com/sampaints" target="_blank">
        <div class="social-icon">📘</div>
        <h3>Facebook</h3>
        <p>/sampaints</p>
      </a>
      <a class="social-card" href="https://etsy.com/shop/sampaints" target="_blank">
        <div class="social-icon">🛍</div>
        <h3>Etsy Shop</h3>
        <p>Shop prints & cards</p>
      </a>
      <a class="social-card" href="/cdn-cgi/l/email-protection#3c54595050537c56594f4f534c4c5d5552484f125f5351" < div>
        <h3>Email</h3>
        <p>For commissions & questions</p>
      </a>
    </div>

    <p style="color:var(--stone); margin-top:1rem; font-size:0.9rem;">
      Or reach me directly: <a class="contact-email" href="/cdn-cgi/l/email-protection#b9d1dcd5d5d6f9d3dccacad6c9c9d8d0d7cdca97dad6d4"><span class="__cf_email__" data-cfemail="d5bdb0b9b9ba95bfb0a6a6baa5a5b4bcbba1a6fbb6bab8">[email&#160;protected]</span></a>
    </p>
  </div>
</section>

<!-- FOOTER -->
<footer>
  © 2026 <span>sam.paints</span> · Handmade with love · All rights reserved
</footer>

<!-- LIGHTBOX -->
<div class="lightbox" id="lightbox" onclick="closeLightbox()">
  <span class="lightbox-close">✕</span>
  <img id="lightboxImg" src="" alt=""/>
</div>

<script data-cfasync="false" src="/cdn-cgi/scripts/5c5dd728/cloudflare-static/email-decode.min.js"></script><script>
  function openLightbox(el) {
    const img = el.querySelector('img');
    if (img) {
      document.getElementById('lightboxImg').src = img.src;
      document.getElementById('lightbox').classList.add('active');
    }
    // If using placeholder divs (no <img>), lightbox won't open — that's fine
  }
  function closeLightbox() {
    document.getElementById('lightbox').class
