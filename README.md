# Pentagram-website
Our website 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>PENTAGRAM DESIGN — We Build Brands That Sell</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet"/>
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --black: #0B0B0B;
    --red: #FF2A2A;
    --red-dim: rgba(255,42,42,0.15);
    --red-glow: rgba(255,42,42,0.35);
    --white: #FFFFFF;
    --gray: #1A1A1A;
    --gray-mid: #2A2A2A;
    --gray-text: #888888;
    --font-display: 'Bebas Neue', sans-serif;
    --font-body: 'DM Sans', sans-serif;
    --font-mono: 'Space Mono', monospace;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: var(--font-body);
    overflow-x: hidden;
    cursor: default;
  }

  /* Custom scrollbar */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--black); }
  ::-webkit-scrollbar-thumb { background: var(--red); border-radius: 2px; }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 9999;
    opacity: 0.4;
  }

  /* ── NAV ── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 1000;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 24px 60px;
    backdrop-filter: blur(20px);
    background: rgba(11,11,11,0.7);
    border-bottom: 1px solid rgba(255,255,255,0.04);
    transition: padding 0.3s;
  }
  nav.scrolled { padding: 16px 60px; }

  .nav-logo {
    font-family: var(--font-display);
    font-size: 22px;
    letter-spacing: 4px;
    color: var(--white);
    text-decoration: none;
  }
  .nav-logo span { color: var(--red); }

  .nav-links {
    display: flex;
    gap: 40px;
    list-style: none;
  }
  .nav-links a {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--gray-text);
    text-decoration: none;
    transition: color 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -4px; left: 0;
    width: 0; height: 1px;
    background: var(--red);
    transition: width 0.3s;
  }
  .nav-links a:hover { color: var(--white); }
  .nav-links a:hover::after { width: 100%; }

  .nav-cta {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 2px;
    padding: 10px 22px;
    border: 1px solid var(--red);
    color: var(--red);
    text-decoration: none;
    text-transform: uppercase;
    transition: all 0.3s;
  }
  .nav-cta:hover {
    background: var(--red);
    color: var(--white);
    box-shadow: 0 0 20px var(--red-glow);
  }

  /* Hamburger */
  .hamburger { display: none; flex-direction: column; gap: 5px; cursor: pointer; }
  .hamburger span {
    width: 24px; height: 1px;
    background: var(--white);
    transition: all 0.3s;
    display: block;
  }
  .hamburger.open span:nth-child(1) { transform: translateY(6px) rotate(45deg); }
  .hamburger.open span:nth-child(2) { opacity: 0; }
  .hamburger.open span:nth-child(3) { transform: translateY(-6px) rotate(-45deg); }

  .mobile-menu {
    display: none;
    position: fixed;
    inset: 0;
    background: var(--black);
    z-index: 999;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 40px;
  }
  .mobile-menu.open { display: flex; }
  .mobile-menu a {
    font-family: var(--font-display);
    font-size: 48px;
    letter-spacing: 4px;
    color: var(--white);
    text-decoration: none;
    transition: color 0.3s;
  }
  .mobile-menu a:hover { color: var(--red); }

  /* ── HERO ── */
  #hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    overflow: hidden;
    padding: 120px 60px 80px;
  }

  /* Red glow blob */
  #hero::before {
    content: '';
    position: absolute;
    width: 700px; height: 700px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(255,42,42,0.18) 0%, transparent 70%);
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    animation: pulse 4s ease-in-out infinite;
  }
  /* Grid lines */
  #hero::after {
    content: '';
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(255,255,255,0.025) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,255,255,0.025) 1px, transparent 1px);
    background-size: 60px 60px;
    mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black 40%, transparent 100%);
  }

  @keyframes pulse {
    0%, 100% { transform: translate(-50%,-50%) scale(1); opacity: 0.8; }
    50% { transform: translate(-50%,-50%) scale(1.15); opacity: 1; }
  }

  .hero-inner {
    position: relative;
    z-index: 2;
    text-align: center;
    max-width: 1000px;
  }

  .hero-eyebrow {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: var(--red);
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 0.8s 0.2s forwards;
  }

  .hero-title {
    font-family: var(--font-display);
    font-size: clamp(64px, 10vw, 140px);
    line-height: 0.9;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--white);
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 0.8s 0.4s forwards;
  }
  .hero-title span { color: var(--red); }

  .hero-subtitle {
    font-family: var(--font-body);
    font-size: clamp(14px, 2vw, 18px);
    color: var(--gray-text);
    letter-spacing: 3px;
    font-weight: 300;
    text-transform: uppercase;
    margin-bottom: 56px;
    opacity: 0;
    animation: fadeUp 0.8s 0.6s forwards;
  }

  .hero-buttons {
    display: flex;
    gap: 16px;
    justify-content: center;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.8s 0.8s forwards;
  }

  .btn-primary {
    font-family: var(--font-mono);
    font-size: 13px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 18px 48px;
    background: var(--red);
    color: var(--white);
    text-decoration: none;
    border: none;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition: box-shadow 0.3s, transform 0.3s;
    display: inline-block;
  }
  .btn-primary::before {
    content: '';
    position: absolute;
    inset: 0;
    background: rgba(255,255,255,0.1);
    transform: translateX(-100%);
    transition: transform 0.4s;
  }
  .btn-primary:hover::before { transform: translateX(0); }
  .btn-primary:hover {
    box-shadow: 0 0 40px var(--red-glow), 0 0 80px rgba(255,42,42,0.15);
    transform: translateY(-2px);
  }

  .btn-secondary {
    font-family: var(--font-mono);
    font-size: 13px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 18px 48px;
    background: transparent;
    color: var(--white);
    text-decoration: none;
    border: 1px solid rgba(255,255,255,0.2);
    cursor: pointer;
    transition: all 0.3s;
    display: inline-block;
  }
  .btn-secondary:hover {
    border-color: var(--white);
    background: rgba(255,255,255,0.05);
  }

  /* Scroll indicator */
  .scroll-indicator {
    position: absolute;
    bottom: 40px; left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    opacity: 0;
    animation: fadeUp 0.8s 1.2s forwards;
  }
  .scroll-indicator span {
    font-family: var(--font-mono);
    font-size: 9px;
    letter-spacing: 3px;
    color: var(--gray-text);
    text-transform: uppercase;
  }
  .scroll-line {
    width: 1px; height: 48px;
    background: linear-gradient(var(--red), transparent);
    animation: scrollAnim 2s 1.5s ease-in-out infinite;
  }
  @keyframes scrollAnim {
    0% { transform: scaleY(0); transform-origin: top; }
    50% { transform: scaleY(1); transform-origin: top; }
    50.01% { transform: scaleY(1); transform-origin: bottom; }
    100% { transform: scaleY(0); transform-origin: bottom; }
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── MARQUEE ── */
  .marquee-wrap {
    background: var(--red);
    padding: 14px 0;
    overflow: hidden;
    white-space: nowrap;
  }
  .marquee-track {
    display: inline-flex;
    animation: marquee 18s linear infinite;
  }
  .marquee-track span {
    font-family: var(--font-display);
    font-size: 18px;
    letter-spacing: 4px;
    color: var(--white);
    padding: 0 32px;
  }
  .marquee-track span.dot { color: rgba(255,255,255,0.5); padding: 0; }
  @keyframes marquee {
    0% { transform: translateX(0); }
    100% { transform: translateX(-50%); }
  }

  /* ── SECTIONS COMMON ── */
  section { padding: 120px 60px; }

  .section-label {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: var(--red);
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .section-label::before {
    content: '';
    display: inline-block;
    width: 24px; height: 1px;
    background: var(--red);
  }

  .section-title {
    font-family: var(--font-display);
    font-size: clamp(40px, 6vw, 80px);
    letter-spacing: 2px;
    line-height: 1;
    text-transform: uppercase;
    margin-bottom: 64px;
  }

  /* Fade-in on scroll */
  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* ── SERVICES ── */
  #services { background: var(--gray); }

  .services-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
  }

  .service-card {
    background: var(--black);
    padding: 56px 40px;
    position: relative;
    overflow: hidden;
    transition: background 0.4s;
    cursor: default;
  }
  .service-card::before {
    content: '';
    position: absolute;
    bottom: 0; left: 0;
    width: 0; height: 2px;
    background: var(--red);
    transition: width 0.5s ease;
  }
  .service-card:hover::before { width: 100%; }
  .service-card:hover { background: #111111; }

  .service-icon {
    width: 56px; height: 56px;
    margin-bottom: 32px;
    position: relative;
  }
  .service-icon svg { width: 100%; height: 100%; }

  .service-num {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 3px;
    color: var(--red);
    margin-bottom: 16px;
    display: block;
  }

  .service-name {
    font-family: var(--font-display);
    font-size: 32px;
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 16px;
    color: var(--white);
  }

  .service-desc {
    font-size: 14px;
    line-height: 1.7;
    color: var(--gray-text);
    font-weight: 300;
  }

  .service-arrow {
    margin-top: 32px;
    font-family: var(--font-mono);
    font-size: 20px;
    color: var(--red);
    display: inline-block;
    transition: transform 0.3s;
  }
  .service-card:hover .service-arrow { transform: translateX(8px); }

  /* ── PORTFOLIO ── */
  #portfolio { background: var(--black); }

  .portfolio-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
  }

  .portfolio-item {
    aspect-ratio: 4/3;
    position: relative;
    overflow: hidden;
    cursor: pointer;
  }

  .portfolio-bg {
    width: 100%; height: 100%;
    transition: transform 0.6s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: var(--font-display);
    font-size: 48px;
    letter-spacing: 4px;
  }

  /* Each card unique style */
  .p1 .portfolio-bg { background: #0f0f0f; color: var(--red); }
  .p2 .portfolio-bg { background: #140a0a; color: #fff; }
  .p3 .portfolio-bg { background: #0a0a14; color: var(--red); }
  .p4 .portfolio-bg { background: #0a140a; color: #fff; }
  .p5 .portfolio-bg { background: #14140a; color: var(--red); }
  .p6 .portfolio-bg { background: #0f0f0f; color: #fff; }

  .portfolio-item:hover .portfolio-bg { transform: scale(1.06); }

  .portfolio-overlay {
    position: absolute;
    inset: 0;
    background: rgba(255,42,42,0.88);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.4s;
  }
  .portfolio-item:hover .portfolio-overlay { opacity: 1; }

  .portfolio-overlay h3 {
    font-family: var(--font-display);
    font-size: 28px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--white);
    margin-bottom: 8px;
  }
  .portfolio-overlay p {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 2px;
    color: rgba(255,255,255,0.7);
    text-transform: uppercase;
  }

  /* Portfolio visual elements */
  .p1 .portfolio-bg::before { content: '◆'; font-size: 56px; }
  .p2 .portfolio-bg::before { content: '⬡'; font-size: 64px; }
  .p3 .portfolio-bg::before { content: '△'; font-size: 60px; }
  .p4 .portfolio-bg::before { content: '○'; font-size: 68px; }
  .p5 .portfolio-bg::before { content: '★'; font-size: 56px; }
  .p6 .portfolio-bg::before { content: '⬟'; font-size: 60px; }

  /* ── PRICING ── */
  #pricing { background: var(--gray); }

  .pricing-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    margin-bottom: 64px;
  }

  .pricing-card {
    background: var(--black);
    padding: 56px 40px;
    position: relative;
    transition: transform 0.3s;
  }
  .pricing-card:hover { transform: translateY(-6px); }

  .pricing-card.popular {
    background: var(--red);
    transform: translateY(-12px);
  }
  .pricing-card.popular:hover { transform: translateY(-18px); }

  .popular-badge {
    position: absolute;
    top: -1px; right: 32px;
    background: var(--white);
    color: var(--red);
    font-family: var(--font-mono);
    font-size: 9px;
    letter-spacing: 2px;
    padding: 6px 14px;
    text-transform: uppercase;
    font-weight: 700;
  }

  .pricing-tier {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--gray-text);
    margin-bottom: 24px;
  }
  .pricing-card.popular .pricing-tier { color: rgba(255,255,255,0.7); }

  .pricing-price {
    font-family: var(--font-display);
    font-size: 80px;
    line-height: 1;
    color: var(--white);
    margin-bottom: 32px;
    letter-spacing: 2px;
  }
  .pricing-price sup {
    font-family: var(--font-body);
    font-size: 24px;
    font-weight: 300;
    vertical-align: top;
    margin-top: 14px;
    display: inline-block;
  }

  .pricing-features {
    list-style: none;
    margin-bottom: 48px;
    display: flex;
    flex-direction: column;
    gap: 14px;
  }
  .pricing-features li {
    font-size: 14px;
    color: rgba(255,255,255,0.7);
    display: flex;
    align-items: center;
    gap: 12px;
    font-weight: 300;
  }
  .pricing-card.popular .pricing-features li { color: rgba(255,255,255,0.85); }
  .pricing-features li::before {
    content: '→';
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--red);
  }
  .pricing-card.popular .pricing-features li::before { color: var(--white); }

  .btn-pricing {
    display: block;
    text-align: center;
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 16px;
    border: 1px solid rgba(255,255,255,0.2);
    color: var(--white);
    text-decoration: none;
    transition: all 0.3s;
    cursor: pointer;
  }
  .btn-pricing:hover {
    border-color: var(--red);
    background: var(--red);
    box-shadow: 0 0 20px var(--red-glow);
  }
  .pricing-card.popular .btn-pricing {
    background: var(--white);
    color: var(--red);
    border-color: var(--white);
  }
  .pricing-card.popular .btn-pricing:hover {
    background: var(--black);
    color: var(--white);
    border-color: var(--black);
  }

  .pricing-cta {
    text-align: center;
    padding: 64px;
    background: var(--black);
    border: 1px solid rgba(255,42,42,0.2);
    position: relative;
    overflow: hidden;
  }
  .pricing-cta::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse 60% 60% at 50% 50%, rgba(255,42,42,0.08) 0%, transparent 100%);
  }
  .pricing-cta h3 {
    font-family: var(--font-display);
    font-size: clamp(28px, 4vw, 48px);
    letter-spacing: 4px;
    text-transform: uppercase;
    margin-bottom: 24px;
    position: relative;
  }
  .pricing-cta p {
    font-size: 14px;
    color: var(--gray-text);
    margin-bottom: 40px;
    position: relative;
    font-weight: 300;
  }
  .pricing-cta .btn-primary { position: relative; font-size: 14px; }

  /* ── ABOUT ── */
  #about {
    background: var(--black);
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
  }

  .about-left { position: relative; }

  .about-visual {
    aspect-ratio: 1;
    background: var(--gray);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: var(--font-display);
    font-size: clamp(60px, 8vw, 100px);
    letter-spacing: 4px;
    color: var(--red);
    position: relative;
    overflow: hidden;
  }
  .about-visual::before {
    content: '';
    position: absolute;
    inset: 12px;
    border: 1px solid rgba(255,42,42,0.3);
    animation: rotateSquare 20s linear infinite;
  }
  .about-visual::after {
    content: '';
    position: absolute;
    inset: 24px;
    border: 1px solid rgba(255,42,42,0.15);
    animation: rotateSquare 20s linear infinite reverse;
  }
  @keyframes rotateSquare {
    from { transform: rotate(0); }
    to { transform: rotate(360deg); }
  }

  .about-text { }

  .about-title {
    font-family: var(--font-display);
    font-size: clamp(36px, 5vw, 64px);
    letter-spacing: 2px;
    text-transform: uppercase;
    line-height: 1.05;
    margin-bottom: 32px;
  }

  .about-body {
    font-size: 17px;
    line-height: 1.8;
    color: var(--gray-text);
    font-weight: 300;
    margin-bottom: 48px;
  }
  .about-body strong { color: var(--white); font-weight: 500; }

  .about-stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 32px;
    padding-top: 48px;
    border-top: 1px solid rgba(255,255,255,0.06);
  }

  .stat-num {
    font-family: var(--font-display);
    font-size: 48px;
    color: var(--red);
    letter-spacing: 2px;
    line-height: 1;
  }
  .stat-label {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--gray-text);
    margin-top: 4px;
  }

  /* ── CONTACT ── */
  #contact {
    background: var(--gray);
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  #contact::before {
    content: '';
    position: absolute;
    width: 600px; height: 600px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(255,42,42,0.12) 0%, transparent 70%);
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
  }

  .contact-inner { position: relative; z-index: 2; max-width: 700px; margin: 0 auto; }

  .contact-title {
    font-family: var(--font-display);
    font-size: clamp(48px, 8vw, 100px);
    letter-spacing: 4px;
    text-transform: uppercase;
    line-height: 0.95;
    margin-bottom: 32px;
  }
  .contact-title span { color: var(--red); }

  .contact-sub {
    font-size: 15px;
    color: var(--gray-text);
    margin-bottom: 56px;

    
