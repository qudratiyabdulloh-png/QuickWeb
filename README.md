<!DOCTYPE html>
<html lang="uz" data-theme="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>QuickWeb — Professional Sayt Yaratish</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --acid: #c8ff00;
    --acid-fg: #c8ff00;
    --acid-tint: rgba(200,255,0,0.05);
    --acid-tint-strong: rgba(200,255,0,0.12);
    --acid-border: rgba(200,255,0,0.3);
    --acid-border-soft: rgba(200,255,0,0.18);

    /* DARK THEME (default) */
    --bg: #080808;
    --bg-alt: #111111;
    --bg-card: #0d0d0d;
    --bg-card-hover: #111111;
    --bg-marquee: #0d0d0d;
    --text: #f5f5f0;
    --text-muted: #777;
    --text-soft: #bbb;
    --border: rgba(255,255,255,0.05);
    --border-strong: rgba(255,255,255,0.12);
    --tint: rgba(255,255,255,0.025);
    --tint-strong: rgba(255,255,255,0.04);
    --noise-opacity: 0.5;
    --nav-bg: rgba(8,8,8,0.8);
    --preview-bar: #1a1a1a;
    --preview-card: #1a1a1a;
    --plan-featured: linear-gradient(160deg, #0e1500 0%, #0a0a0a 100%);
    --pline: rgba(255,255,255,0.07);
    --cursor-blend: exclusion;
  }

  [data-theme="light"] {
    --acid-fg: #4d6800;
    --acid-tint: rgba(77,104,0,0.08);
    --acid-tint-strong: rgba(77,104,0,0.18);
    --acid-border: rgba(77,104,0,0.5);
    --acid-border-soft: rgba(77,104,0,0.35);
    --bg: #f5f5f0;
    --bg-alt: #ebebe5;
    --bg-card: #ffffff;
    --bg-card-hover: #fafaf3;
    --bg-marquee: #ebebe5;
    --text: #0a0a0a;
    --text-muted: #6a6a6a;
    --text-soft: #333;
    --border: rgba(0,0,0,0.07);
    --border-strong: rgba(0,0,0,0.14);
    --tint: rgba(0,0,0,0.025);
    --tint-strong: rgba(0,0,0,0.04);
    --noise-opacity: 0.25;
    --nav-bg: rgba(245,245,240,0.85);
    --preview-bar: #e8e8e0;
    --preview-card: #fafaf3;
    --plan-featured: linear-gradient(160deg, #f0f8d8 0%, #fafaf3 100%);
    --pline: rgba(0,0,0,0.08);
    --cursor-blend: difference;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }
  body { background: var(--bg); color: var(--text); font-family: 'Inter', sans-serif; overflow-x: hidden; cursor: none; transition: background 0.3s, color 0.3s; }
  body.no-scroll { overflow: hidden; }

  /* CURSOR */
  .cursor { width: 10px; height: 10px; background: var(--acid); border-radius: 50%; position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9999; mix-blend-mode: var(--cursor-blend); transition: transform 0.15s ease; }
  .cursor.big { transform: scale(4.5); }
  .cursor-canvas { position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9997; }

  /* NOISE */
  body::before { content: ''; position: fixed; inset: 0; background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E"); pointer-events: none; z-index: 200; opacity: var(--noise-opacity); }

  /* NAV */
  nav { position: fixed; top: 0; left: 0; right: 0; z-index: 500; display: flex; justify-content: space-between; align-items: center; padding: 1rem 4rem; border-bottom: 1px solid var(--border); backdrop-filter: blur(16px); background: var(--nav-bg); gap: 1rem; transition: background 0.3s, border-color 0.3s; }
  .logo { display: inline-flex; align-items: center; gap: 0.55rem; font-family: 'Syne', sans-serif; font-weight: 800; font-size: 1.2rem; letter-spacing: -0.03em; color: var(--text); text-decoration: none; flex-shrink: 0; }
  .logo-mark { width: 30px; height: 30px; color: var(--acid-fg); flex-shrink: 0; }
  .logo span { color: var(--acid-fg); }
  nav ul { list-style: none; display: flex; gap: 2.2rem; }
  nav ul a { font-family: 'Space Mono', monospace; font-size: 0.68rem; color: var(--text-muted); text-decoration: none; letter-spacing: 0.1em; text-transform: uppercase; transition: color 0.2s; }
  nav ul a:hover { color: var(--acid-fg); }

  .nav-tools { display: flex; align-items: center; gap: 0.6rem; flex-shrink: 0; }

  /* THEME TOGGLE */
  .theme-toggle { background: transparent; border: 1px solid var(--border-strong); color: var(--text); width: 36px; height: 36px; border-radius: 50%; cursor: none; display: inline-flex; align-items: center; justify-content: center; font-size: 0.9rem; transition: border-color 0.2s, color 0.2s, background 0.2s; }
  .theme-toggle:hover { border-color: var(--acid-fg); color: var(--acid-fg); }

  /* LANG SWITCHER */
  .lang-switcher { display: inline-flex; border: 1px solid var(--border-strong); border-radius: 999px; padding: 2px; }
  .lang-btn { background: transparent; border: none; color: var(--text-muted); font-family: 'Space Mono', monospace; font-size: 0.62rem; letter-spacing: 0.08em; text-transform: uppercase; padding: 0.32rem 0.6rem; cursor: none; border-radius: 999px; transition: color 0.2s, background 0.2s; }
  .lang-btn:hover { color: var(--text); }
  .lang-btn.active { background: var(--acid); color: #080808; font-weight: 700; }

  /* NAV CTA — Buyurtma qilish */
  .nav-cta { background: var(--acid); color: #080808; padding: 0.55rem 1.2rem; border-radius: 2px; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.78rem; text-decoration: none; cursor: none; border: none; transition: transform 0.2s, box-shadow 0.2s; letter-spacing: -0.01em; white-space: nowrap; }
  .nav-cta:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(200,255,0,0.35); }

  /* HERO */
  .hero { min-height: 100vh; display: flex; flex-direction: column; justify-content: center; padding: 8rem 4rem 4rem; position: relative; overflow: hidden; }
  .hero-grid { position: absolute; inset: 0; background-image: linear-gradient(rgba(200,255,0,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(200,255,0,0.03) 1px, transparent 1px); background-size: 56px 56px; mask-image: radial-gradient(ellipse 80% 80% at 40% 50%, black 0%, transparent 75%); animation: gridShift 25s linear infinite; }
  [data-theme="light"] .hero-grid { background-image: linear-gradient(rgba(0,0,0,0.04) 1px, transparent 1px), linear-gradient(90deg, rgba(0,0,0,0.04) 1px, transparent 1px); }
  @keyframes gridShift { from{background-position:0 0} to{background-position:56px 56px} }
  .particles { position: absolute; inset: 0; pointer-events: none; overflow: hidden; }
  .particle { position: absolute; background: var(--acid); border-radius: 50%; animation: particleUp linear infinite; }
  @keyframes particleUp { 0%{transform:translateY(100vh);opacity:0} 5%{opacity:0.8} 90%{opacity:0.3} 100%{transform:translateY(-50px);opacity:0} }

  .hero-badge { display: inline-flex; align-items: center; gap: 0.5rem; font-family: 'Space Mono', monospace; font-size: 0.68rem; letter-spacing: 0.14em; color: var(--acid-fg); text-transform: uppercase; border: 1px solid rgba(200,255,0,0.3); padding: 0.4rem 0.9rem; border-radius: 2px; margin-bottom: 2rem; width: fit-content; animation: fadeUp 0.8s ease both; background: rgba(200,255,0,0.05); }
  .hero-badge::before { content: ''; width: 6px; height: 6px; background: var(--acid); border-radius: 50%; animation: ripplePulse 1.8s ease-in-out infinite; }
  @keyframes ripplePulse { 0%,100%{opacity:1;transform:scale(1);box-shadow:0 0 0 0 rgba(200,255,0,0.5)} 50%{opacity:0.5;transform:scale(1.4);box-shadow:0 0 0 8px rgba(200,255,0,0)} }

  .hero h1 { font-family: 'Syne', sans-serif; font-size: clamp(3.5rem, 9vw, 9rem); font-weight: 800; line-height: 0.9; letter-spacing: -0.04em; max-width: 950px; animation: fadeUp 0.9s 0.1s ease both; }
  .line-accent { color: var(--acid-fg); }
  .line-outline { -webkit-text-stroke: 1.5px var(--border-strong); color: transparent; }
  .typewriter-wrap { display: inline-block; position: relative; }
  .tw-word { border-right: 3px solid var(--acid-fg); display: inline; animation: blinkCaret 0.9s step-end infinite; }
  @keyframes blinkCaret { 0%,100%{border-color:var(--acid-fg)} 50%{border-color:transparent} }

  .hero-sub { max-width: 460px; font-size: 1rem; color: var(--text-muted); line-height: 1.75; margin-top: 2.5rem; font-weight: 300; animation: fadeUp 1s 0.2s ease both; }
  .hero-actions { display: flex; gap: 1rem; margin-top: 3rem; animation: fadeUp 1s 0.3s ease both; flex-wrap: wrap; }

  .btn-primary { background: var(--acid); color: #080808; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; padding: 1rem 2.2rem; border: none; border-radius: 2px; cursor: none; text-decoration: none; display: inline-flex; align-items: center; gap: 0.5rem; transition: transform 0.2s, box-shadow 0.2s; letter-spacing: -0.01em; position: relative; overflow: hidden; }
  .btn-primary::after { content: ''; position: absolute; inset: 0; background: linear-gradient(90deg, transparent, rgba(255,255,255,0.25), transparent); transform: translateX(-100%); transition: transform 0.45s ease; }
  .btn-primary:hover::after { transform: translateX(100%); }
  .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 12px 40px rgba(200,255,0,0.35); }

  .btn-outline { background: transparent; color: var(--text); font-family: 'Space Mono', monospace; font-size: 0.72rem; letter-spacing: 0.1em; text-transform: uppercase; padding: 1rem 2rem; border: 1px solid var(--border-strong); border-radius: 2px; cursor: none; text-decoration: none; transition: border-color 0.2s, color 0.2s, background 0.2s; }
  .btn-outline:hover { border-color: var(--acid-fg); color: var(--acid-fg); background: rgba(200,255,0,0.04); }

  .btn-tg { background: #0088cc; color: #fff; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; padding: 1rem 2rem; border-radius: 2px; cursor: none; text-decoration: none; display: inline-flex; align-items: center; gap: 0.6rem; transition: transform 0.2s, box-shadow 0.2s; }
  .btn-tg:hover { transform: translateY(-3px); box-shadow: 0 12px 40px rgba(0,136,204,0.35); }

  .hero-stats { display: flex; gap: 4rem; margin-top: 5rem; padding-top: 3rem; border-top: 1px solid var(--border); animation: fadeUp 1s 0.4s ease both; flex-wrap: wrap; }
  .stat-num { font-family: 'Syne', sans-serif; font-size: 2.4rem; font-weight: 800; color: var(--acid-fg); line-height: 1; }
  .stat-label { font-family: 'Space Mono', monospace; font-size: 0.62rem; color: var(--text-muted); margin-top: 0.35rem; letter-spacing: 0.06em; }

  /* MARQUEE */
  .marquee-wrap { overflow: hidden; padding: 0.9rem 0; border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); background: var(--bg-marquee); }
  .marquee-track { display: flex; gap: 2.5rem; animation: marqueeScroll 18s linear infinite; width: max-content; }
  .marquee-item { font-family: 'Space Mono', monospace; font-size: 0.68rem; letter-spacing: 0.15em; text-transform: uppercase; color: var(--text-muted); white-space: nowrap; display: flex; align-items: center; gap: 0.8rem; }
  .dot-sep { color: var(--acid-fg); }
  @keyframes marqueeScroll { from{transform:translateX(0)} to{transform:translateX(-50%)} }

  /* PAIN SECTION */
  .pain-section { padding: 8rem 4rem; background: var(--bg-alt); position: relative; overflow: hidden; }
  .pain-section::before { content: ''; position: absolute; left: 0; top: 0; bottom: 0; width: 2px; background: linear-gradient(to bottom, transparent, rgba(255,59,59,0.6), transparent); }

  .section-tag { font-family: 'Space Mono', monospace; font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--acid-fg); margin-bottom: 1rem; }
  .section-title { font-family: 'Syne', sans-serif; font-size: clamp(2rem, 4vw, 3.2rem); font-weight: 800; letter-spacing: -0.03em; line-height: 1.05; max-width: 600px; }

  .pain-subtitle { font-size: 1rem; color: var(--text-muted); max-width: 500px; line-height: 1.7; margin-top: 1rem; }
  .pain-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1px; background: var(--border); border-radius: 4px; overflow: hidden; margin-top: 3rem; }
  .pain-card { background: var(--bg-card); padding: 2.5rem 2rem; position: relative; overflow: hidden; transition: background 0.3s; opacity: 0; transform: translateY(30px); }
  .pain-card.visible { opacity: 1; transform: translateY(0); transition: opacity 0.6s ease, transform 0.6s ease, background 0.3s; }
  .pain-card:hover { background: var(--bg-card-hover); }
  .pain-top-line { position: absolute; top: 0; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, rgba(255,59,59,0.7), transparent); transform: scaleX(0); transform-origin: left; transition: transform 0.4s ease; }
  .pain-card:hover .pain-top-line { transform: scaleX(1); }
  .pain-emoji { font-size: 2rem; margin-bottom: 1.2rem; display: block; }
  .pain-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; margin-bottom: 0.5rem; color: var(--text); }
  .pain-desc { font-size: 0.8rem; color: var(--text-muted); line-height: 1.65; }
  .pain-solution { display: flex; align-items: center; gap: 0.5rem; margin-top: 1.2rem; font-size: 0.75rem; color: var(--acid-fg); font-family: 'Space Mono', monospace; }
  .pain-solution::before { content: '✓ '; font-weight: 700; }

  .arrow-pill-wrap { text-align: center; padding: 2.5rem 4rem; background: var(--bg-alt); }
  .arrow-pill { display: inline-flex; align-items: center; gap: 1rem; background: rgba(200,255,0,0.05); border: 1px solid rgba(200,255,0,0.2); padding: 0.8rem 2rem; border-radius: 100px; font-family: 'Space Mono', monospace; font-size: 0.7rem; letter-spacing: 0.1em; color: var(--acid-fg); text-transform: uppercase; }

  /* FEATURES */
  #features { padding: 8rem 4rem; }
  .features-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 5rem; align-items: center; margin-top: 4rem; }
  .feature-card { display: flex; gap: 1.2rem; padding: 1.5rem; border: 1px solid var(--border); border-radius: 4px; margin-bottom: 0.8rem; background: var(--tint); transition: border-color 0.3s, background 0.3s, transform 0.3s; opacity: 0; transform: translateX(-20px); }
  .feature-card.visible { opacity: 1; transform: translateX(0); }
  .feature-card:hover { border-color: rgba(200,255,0,0.25); background: rgba(200,255,0,0.03); transform: translateX(6px); }
  .feat-icon { font-size: 1.4rem; flex-shrink: 0; width: 40px; height: 40px; display: flex; align-items: center; justify-content: center; background: rgba(200,255,0,0.07); border-radius: 4px; }
  .feat-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.9rem; margin-bottom: 0.3rem; }
  .feat-desc { font-size: 0.8rem; color: var(--text-muted); line-height: 1.6; }

  /* BROWSER */
  .preview-block { background: var(--bg-card); border: 1px solid var(--border); border-radius: 10px; overflow: hidden; box-shadow: 0 40px 100px rgba(0,0,0,0.3); opacity: 0; transform: translateY(30px); transition: opacity 0.8s ease, transform 0.8s ease; }
  .preview-block.visible { opacity: 1; transform: translateY(0); }
  .preview-bar { background: var(--preview-bar); padding: 0.65rem 1rem; display: flex; align-items: center; gap: 0.4rem; }
  .dot { width: 9px; height: 9px; border-radius: 50%; }
  .dot-r { background: #ff5f57; } .dot-y { background: #febc2e; } .dot-g { background: #28c840; }
  .preview-url { margin-left: 0.8rem; background: var(--bg-alt); border-radius: 4px; padding: 0.22rem 0.8rem; font-family: 'Space Mono', monospace; font-size: 0.6rem; color: var(--text-muted); flex: 1; max-width: 180px; }
  .preview-content { padding: 1.5rem; }
  .preview-hero-block { background: linear-gradient(135deg, var(--bg-alt) 0%, rgba(200,255,0,0.05) 100%); border-radius: 6px; padding: 1.8rem; margin-bottom: 1rem; position: relative; overflow: hidden; }
  .preview-hero-block::after { content: ''; position: absolute; top: -30px; right: -30px; width: 120px; height: 120px; background: var(--acid); border-radius: 50%; opacity: 0.08; animation: orbBreath 3s ease-in-out infinite; }
  @keyframes orbBreath { 0%,100%{transform:scale(1)} 50%{transform:scale(1.25)} }
  .preview-h1 { font-family: 'Syne', sans-serif; font-size: 1.1rem; font-weight: 800; margin-bottom: 0.3rem; }
  .preview-p { font-size: 0.6rem; color: var(--text-muted); line-height: 1.5; max-width: 180px; margin-bottom: 0.8rem; }
  .preview-btn-sm { background: var(--acid); color: #080808; font-family: 'Syne', sans-serif; font-size: 0.58rem; font-weight: 700; padding: 0.3rem 0.7rem; border-radius: 2px; display: inline-block; }
  .preview-cards { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0.5rem; }
  .preview-card-sm { background: var(--preview-card); border-radius: 4px; padding: 0.7rem; border: 1px solid var(--border); }
  .pbar { height: 4px; border-radius: 2px; margin-bottom: 0.35rem; background: var(--acid); }
  .pline { height: 2px; background: var(--pline); border-radius: 2px; margin-bottom: 0.25rem; }

  /* PROCESS */
  #process { background: var(--bg-alt); padding: 8rem 4rem; }
  .steps-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1px; background: var(--border); margin-top: 4rem; border-radius: 4px; overflow: hidden; }
  .step { background: var(--bg-card); padding: 2.5rem 1.8rem; position: relative; opacity: 0; transform: translateY(20px); }
  .step.visible { opacity: 1; transform: translateY(0); transition: opacity 0.5s ease, transform 0.5s ease, background 0.3s; }
  .step:hover { background: var(--bg-card-hover); }
  .step-top-line { position: absolute; top: 0; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, var(--acid), transparent); transform: scaleX(0); transform-origin: left; transition: transform 0.4s ease; }
  .step:hover .step-top-line { transform: scaleX(1); }
  .step-num { font-family: 'Space Mono', monospace; font-size: 0.62rem; color: var(--acid-fg); letter-spacing: 0.15em; margin-bottom: 1.5rem; opacity: 0.7; }
  .step-icon { font-size: 1.7rem; margin-bottom: 0.8rem; }
  .step-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; margin-bottom: 0.5rem; }
  .step-desc { font-size: 0.78rem; color: var(--text-muted); line-height: 1.6; }

  /* PRICING */
  #pricing { padding: 8rem 4rem; }
  .pricing-header { text-align: center; margin-bottom: 4rem; }
  .pricing-grid { display: grid; grid-template-columns: 1fr 1fr; max-width: 880px; margin: 0 auto; border: 1px solid var(--border-strong); border-radius: 6px; overflow: hidden; }
  .plan { background: var(--bg-card); padding: 3rem; transition: background 0.3s; }
  .plan:hover { background: var(--bg-card-hover); }
  .plan.featured { background: var(--plan-featured); border-left: 1px solid rgba(200,255,0,0.18); position: relative; }
  .plan.featured::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, var(--acid), rgba(200,255,0,0.2)); }
  .plan-tag { font-family: 'Space Mono', monospace; font-size: 0.62rem; letter-spacing: 0.15em; text-transform: uppercase; color: var(--acid-fg); background: rgba(200,255,0,0.1); padding: 0.25rem 0.65rem; border-radius: 2px; display: inline-block; margin-bottom: 1.5rem; }
  .plan-icon { font-size: 1.8rem; margin-bottom: 0.8rem; display: block; }
  .plan-name { font-family: 'Syne', sans-serif; font-size: 1.4rem; font-weight: 800; margin-bottom: 0.4rem; }
  .plan-desc { font-size: 0.82rem; color: var(--text-muted); line-height: 1.6; margin-bottom: 2rem; }
  .plan-price { font-family: 'Syne', sans-serif; font-size: 3.8rem; font-weight: 800; letter-spacing: -0.04em; color: var(--acid-fg); line-height: 1; margin-bottom: 0.3rem; }
  .plan-price sup { font-size: 1.5rem; font-weight: 400; vertical-align: super; }
  .plan-per { font-family: 'Space Mono', monospace; font-size: 0.65rem; color: var(--text-muted); letter-spacing: 0.08em; margin-bottom: 2.5rem; }
  .plan-features { list-style: none; margin-bottom: 2.5rem; display: flex; flex-direction: column; gap: 0.75rem; }
  .plan-features li { display: flex; align-items: flex-start; gap: 0.8rem; font-size: 0.83rem; color: var(--text-soft); line-height: 1.5; }
  .plan-features li::before { content: '→'; color: var(--acid-fg); font-family: 'Space Mono', monospace; font-size: 0.72rem; flex-shrink: 0; margin-top: 0.1rem; }
  .plan-btn { display: block; text-align: center; padding: 0.9rem; border-radius: 2px; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.88rem; text-decoration: none; cursor: none; transition: all 0.2s; border: none; width: 100%; }
  .plan-btn-outline { border: 1px solid var(--border-strong); color: var(--text); background: transparent; }
  .plan-btn-outline:hover { border-color: var(--acid-fg); color: var(--acid-fg); }
  .plan-btn-fill { background: var(--acid); color: #080808; }
  .plan-btn-fill:hover { box-shadow: 0 6px 30px rgba(200,255,0,0.4); transform: translateY(-2px); }

  /* CTA */
  .cta-section { text-align: center; padding: 8rem 4rem; position: relative; overflow: hidden; background: var(--bg-alt); }
  .cta-bg { position: absolute; inset: 0; background: radial-gradient(ellipse 700px 500px at 50% 50%, rgba(200,255,0,0.06) 0%, transparent 70%); animation: ctaPulse 5s ease-in-out infinite; }
  @keyframes ctaPulse { 0%,100%{opacity:0.5} 50%{opacity:1} }
  .cta-section h2 { font-family: 'Syne', sans-serif; font-size: clamp(2.5rem, 6vw, 5rem); font-weight: 800; letter-spacing: -0.04em; line-height: 1; margin-bottom: 1.5rem; position: relative; }
  .cta-section p { color: var(--text-muted); font-size: 1rem; max-width: 440px; margin: 0 auto 3rem; line-height: 1.7; position: relative; }
  .cta-buttons { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; position: relative; }

  /* SCROLL PROGRESS */
  .progress-bar { position: fixed; top: 0; left: 0; height: 2px; background: var(--acid); z-index: 1000; box-shadow: 0 0 8px rgba(200,255,0,0.5); pointer-events: none; }

  /* FOOTER */
  footer { border-top: 1px solid var(--border); padding: 2.5rem 4rem; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem; }
  footer p { font-family: 'Space Mono', monospace; font-size: 0.62rem; color: var(--text-muted); letter-spacing: 0.06em; }

  @keyframes fadeUp { from{opacity:0;transform:translateY(28px)} to{opacity:1;transform:translateY(0)} }

  .reveal { opacity: 0; transform: translateY(28px); transition: opacity 0.7s ease, transform 0.7s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* ============= ORDER OVERLAY ============= */
  .order-overlay { position: fixed; inset: 0; z-index: 2000; background: rgba(0,0,0,0.92); backdrop-filter: blur(20px); display: flex; align-items: flex-start; justify-content: center; overflow-y: auto; opacity: 0; pointer-events: none; transition: opacity 0.35s ease; padding: 5rem 1.5rem 3rem; }
  [data-theme="light"] .order-overlay { background: rgba(245,245,240,0.96); }
  .order-overlay.open { opacity: 1; pointer-events: auto; }
  .order-panel { background: var(--bg-card); border: 1px solid var(--border-strong); border-radius: 8px; max-width: 720px; width: 100%; padding: 3rem; position: relative; transform: translateY(20px); transition: transform 0.35s ease; box-shadow: 0 40px 120px rgba(0,0,0,0.5); }
  .order-overlay.open .order-panel { transform: translateY(0); }
  .order-close { position: absolute; top: 1.1rem; right: 1.1rem; width: 38px; height: 38px; background: transparent; border: 1px solid var(--border-strong); color: var(--text); font-size: 1.3rem; line-height: 1; border-radius: 50%; cursor: none; transition: border-color 0.2s, color 0.2s, transform 0.2s; }
  .order-close:hover { border-color: var(--acid-fg); color: var(--acid-fg); transform: rotate(90deg); }
  .order-header { margin-bottom: 2.2rem; }
  .order-header .section-tag { margin-bottom: 0.7rem; }
  .order-header h2 { font-family: 'Syne', sans-serif; font-size: clamp(1.7rem, 3.5vw, 2.4rem); font-weight: 800; letter-spacing: -0.03em; line-height: 1.05; margin-bottom: 0.7rem; }
  .order-header p { color: var(--text-muted); font-size: 0.92rem; line-height: 1.6; max-width: 480px; }

  .order-form { display: flex; flex-direction: column; gap: 0.9rem; }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 0.9rem; }
  .order-form input, .order-form select, .order-form textarea {
    width: 100%; background: var(--tint); border: 1px solid var(--border-strong); border-radius: 4px;
    padding: 0.85rem 1rem; color: var(--text); font-family: 'Inter', sans-serif; font-size: 0.92rem;
    transition: border-color 0.2s, background 0.2s; cursor: none; outline: none;
  }
  .order-form textarea { resize: vertical; min-height: 110px; font-family: 'Inter', sans-serif; }
  .order-form input::placeholder, .order-form textarea::placeholder { color: var(--text-muted); }
  .order-form input:focus, .order-form select:focus, .order-form textarea:focus { border-color: var(--acid-fg); background: rgba(200,255,0,0.04); }
  .order-form select { appearance: none; background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 12 8'%3E%3Cpath fill='%23c8ff00' d='M6 8L0 0h12z'/%3E%3C/svg%3E"); background-repeat: no-repeat; background-position: right 1rem center; background-size: 10px; padding-right: 2.5rem; }
  /* Native dropdown options — explicit colors so they're readable regardless of OS theme */
  .order-form select option { background: #ffffff; color: #0a0a0a; padding: 0.5rem; }
  .order-form select option:disabled { color: #888; }
  .form-submit { background: var(--acid); color: #080808; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; padding: 1rem 2rem; border: none; border-radius: 2px; cursor: none; margin-top: 0.5rem; transition: transform 0.2s, box-shadow 0.2s; letter-spacing: -0.01em; }
  .form-submit:hover { transform: translateY(-2px); box-shadow: 0 12px 40px rgba(200,255,0,0.4); }

  .order-divider { display: flex; align-items: center; gap: 1rem; margin: 2rem 0 1.5rem; color: var(--text-muted); font-family: 'Space Mono', monospace; font-size: 0.65rem; letter-spacing: 0.15em; text-transform: uppercase; }
  .order-divider::before, .order-divider::after { content: ''; flex: 1; height: 1px; background: var(--border-strong); }

  .order-contacts { display: flex; flex-direction: column; gap: 0.7rem; }
  .order-contacts a { display: flex; align-items: center; gap: 0.8rem; padding: 0.95rem 1.2rem; background: var(--tint); border: 1px solid var(--border-strong); border-radius: 4px; color: var(--text); text-decoration: none; font-family: 'Syne', sans-serif; font-weight: 600; font-size: 0.92rem; transition: border-color 0.2s, background 0.2s, transform 0.2s; cursor: none; }
  .order-contacts a:hover { border-color: var(--acid-fg); background: rgba(200,255,0,0.05); transform: translateX(4px); }
  .order-contacts a .ic { width: 28px; height: 28px; display: inline-flex; align-items: center; justify-content: center; flex-shrink: 0; }
  .order-contacts .ic.tg { color: #2ca5e0; }
  .order-contacts .ic.tel { color: var(--acid-fg); }

  /* MOBILE */
  @media (max-width: 768px) {
    nav { padding: 0.9rem 1rem; gap: 0.5rem; }
    nav ul { display: none; }
    .nav-tools { gap: 0.4rem; }
    .nav-cta { padding: 0.45rem 0.8rem; font-size: 0.7rem; }
    .lang-switcher { padding: 1px; }
    .lang-btn { padding: 0.25rem 0.45rem; font-size: 0.58rem; }
    .theme-toggle { width: 32px; height: 32px; font-size: 0.85rem; }
    .logo { font-size: 1rem; }
    .logo-mark { width: 26px; height: 26px; }

    .hero, .pain-section, #features, #process, #pricing, .cta-section { padding: 5rem 1.5rem; }
    .pain-grid, .pricing-grid { grid-template-columns: 1fr; }
    .features-layout { grid-template-columns: 1fr; gap: 3rem; }
    .steps-grid { grid-template-columns: 1fr 1fr; }
    .hero-stats { gap: 2rem; }
    footer { flex-direction: column; text-align: center; }
    .arrow-pill-wrap { padding: 2rem 1.5rem; }
    .order-panel { padding: 2rem 1.3rem; }
    .form-row { grid-template-columns: 1fr; }
    .order-overlay { padding: 4rem 1rem 2rem; }

    body { cursor: auto; }
    .cursor, .cursor-canvas { display: none; }
    .btn-primary, .btn-outline, .btn-tg, .nav-cta, .plan-btn,
    .lang-btn, .theme-toggle, .order-close, .form-submit,
    .order-form input, .order-form select, .order-form textarea,
    .order-contacts a { cursor: pointer; }
  }

  /* ============= LIGHT MODE — readable acid accents ============= */
  [data-theme="light"] .hero-badge {
    border-color: var(--acid-border);
    background: var(--acid-tint);
  }
  [data-theme="light"] .arrow-pill {
    border-color: var(--acid-border-soft);
    background: var(--acid-tint);
  }
  [data-theme="light"] .feature-card:hover {
    border-color: var(--acid-border-soft);
    background: var(--acid-tint);
  }
  [data-theme="light"] .btn-outline:hover {
    background: var(--acid-tint);
  }
  [data-theme="light"] .plan.featured {
    border-left-color: var(--acid-border-soft);
  }
  [data-theme="light"] .plan.featured::before {
    background: linear-gradient(90deg, var(--acid-fg), var(--acid-tint-strong));
  }
  [data-theme="light"] .plan-tag {
    background: var(--acid-tint-strong);
  }
  [data-theme="light"] .step-top-line {
    background: linear-gradient(90deg, var(--acid-fg), transparent);
  }
  [data-theme="light"] .feat-icon {
    background: var(--acid-tint-strong);
  }
  [data-theme="light"] .order-form input:focus,
  [data-theme="light"] .order-form select:focus,
  [data-theme="light"] .order-form textarea:focus {
    background: var(--acid-tint);
  }
  [data-theme="light"] .order-contacts a:hover {
    background: var(--acid-tint);
  }
  [data-theme="light"] .progress-bar {
    background: var(--acid-fg);
    box-shadow: 0 0 8px rgba(77,104,0,0.4);
  }
  [data-theme="light"] .tw-word { border-right-color: var(--acid-fg); }
  [data-theme="light"] .order-form select {
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 12 8'%3E%3Cpath fill='%234d6800' d='M6 8L0 0h12z'/%3E%3C/svg%3E");
  }
  /* Buttons that have acid background + dark text: keep bright in light too — already readable */
  /* But hover shadow should match the new accent for light */
  [data-theme="light"] .btn-primary:hover { box-shadow: 0 12px 40px rgba(77,104,0,0.35); }
  [data-theme="light"] .nav-cta:hover { box-shadow: 0 8px 24px rgba(77,104,0,0.35); }
  [data-theme="light"] .plan-btn-fill:hover { box-shadow: 0 6px 30px rgba(77,104,0,0.4); }
  [data-theme="light"] .form-submit:hover { box-shadow: 0 12px 40px rgba(77,104,0,0.4); }
</style>
</head>
<body>

<div class="progress-bar" id="progressBar"></div>
<div class="cursor" id="cursor"></div>
<canvas class="cursor-canvas" id="cursorCanvas"></canvas>

<!-- LOGO SVG (referenced by <use>) -->
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <symbol id="qw-logo" viewBox="0 0 64 64">
      <!-- Globe -->
      <circle cx="40" cy="32" r="18" fill="none" stroke="currentColor" stroke-width="2"/>
      <ellipse cx="40" cy="32" rx="18" ry="7" fill="none" stroke="currentColor" stroke-width="1.4"/>
      <ellipse cx="40" cy="32" rx="7" ry="18" fill="none" stroke="currentColor" stroke-width="1.4"/>
      <line x1="22" y1="32" x2="58" y2="32" stroke="currentColor" stroke-width="1.4"/>
      <!-- Globe nodes -->
      <circle cx="22" cy="32" r="2" fill="currentColor"/>
      <circle cx="58" cy="32" r="2" fill="currentColor"/>
      <circle cx="40" cy="14" r="2" fill="currentColor"/>
      <circle cx="40" cy="50" r="2" fill="currentColor"/>
      <circle cx="50" cy="20" r="1.6" fill="currentColor"/>
      <circle cx="30" cy="44" r="1.6" fill="currentColor"/>
      <!-- Lightning bolt (overlapping) -->
      <path d="M34 12 L20 34 L29 34 L24 52 L42 28 L33 28 L38 12 Z" fill="currentColor" stroke="var(--bg)" stroke-width="1"/>
      <!-- Speed lines -->
      <line x1="18" y1="20" x2="6" y2="20" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <line x1="14" y1="26" x2="2" y2="26" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <line x1="16" y1="32" x2="4" y2="32" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <line x1="12" y1="38" x2="2" y2="38" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
    </symbol>
  </defs>
</svg>

<!-- NAV -->
<nav>
  <a href="#" class="logo">
    <svg class="logo-mark"><use href="#qw-logo"/></svg>
    <span style="color:var(--text)">Quick</span><span>Web</span>
  </a>
  <ul>
    <li><a href="#pain" data-i18n="nav.problems">Muammolar</a></li>
    <li><a href="#features" data-i18n="nav.features">Imkoniyatlar</a></li>
    <li><a href="#pricing" data-i18n="nav.pricing">Narxlar</a></li>
    <li><a href="#contact" data-i18n="nav.contact">Bog'lanish</a></li>
  </ul>
  <div class="nav-tools">
    <button class="theme-toggle" id="themeToggle" aria-label="Toggle theme" title="Theme">☀</button>
    <div class="lang-switcher" role="tablist" aria-label="Language">
      <button class="lang-btn" data-lang="uz">UZ</button>
      <button class="lang-btn" data-lang="ru">RU</button>
      <button class="lang-btn" data-lang="en">EN</button>
    </div>
    <button class="nav-cta" id="orderBtn" data-open-order data-i18n="nav.order">Buyurtma qilish</button>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-grid"></div>
  <div class="particles" id="particles"></div>

  <div class="hero-badge" data-i18n="hero.badge">⚡ Sayt yaratishda yangi standart</div>

  <h1>
    <span data-i18n="hero.h1_line1">Biznesingiz</span><br>
    <span class="line-accent typewriter-wrap"><span class="tw-word" id="tw"></span></span><br>
    <span class="line-outline" data-i18n="hero.h1_line3">kuchli.</span>
  </h1>

  <p class="hero-sub" data-i18n="hero.sub">
    Tez, zamonaviy va mijozlarni qozonuvchi saytlar.
    Faqat natijaga yo'naltirilgan yondashuv — chiroyli emas, <em>ishlaydi</em>.
  </p>

  <div class="hero-actions">
    <a href="#" class="btn-primary" data-open-order data-i18n="hero.cta_consult">Bepul maslahat →</a>
    <a href="#pricing" class="btn-outline" data-i18n="hero.cta_pricing">Narxlarni ko'rish</a>
  </div>

  <div class="hero-stats">
    <div><div class="stat-num" data-count="48" data-suffix="h">48h</div><div class="stat-label" data-i18n="hero.stat1">O'rtacha topshirish</div></div>
    <div><div class="stat-num" data-count="100" data-suffix="%">100%</div><div class="stat-label" data-i18n="hero.stat2">Mobil optimallashtirish</div></div>
    <div><div class="stat-num" data-count="50" data-suffix="+">50+</div><div class="stat-label" data-i18n="hero.stat3">Topshirilgan saytlar</div></div>
    <div><div class="stat-num">SSL</div><div class="stat-label" data-i18n="hero.stat4">Xavfsizlik bepul</div></div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-wrap">
  <div class="marquee-track" id="marqueeTrack"></div>
</div>

<!-- PAIN SECTION -->
<section class="pain-section" id="pain">
  <div class="section-tag" data-i18n="pain.tag">// odamlar duch keladigan muammolar</div>
  <div class="section-title reveal" data-i18n="pain.title">Saytingiz yo'qmi?<br>Bu sizga qancha turadi.</div>
  <p class="pain-subtitle reveal" data-i18n="pain.subtitle">Har kuni saytisiz bizneslar minglab mijozlarni yo'qotmoqda. Siz qaysi muammoni his qilyapsiz?</p>

  <div class="pain-grid">
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">😤</span>
      <div class="pain-title" data-i18n="pain.c1.title">"Sayt yo'q — mijozlar topilmaydi"</div>
      <div class="pain-desc" data-i18n="pain.c1.desc">Google'da qidirishadi — siz topilmaysiz. Raqibingiz topiladi. Mijoz unikiga boradi. Har kuni shunday.</div>
      <div class="pain-solution" data-i18n="pain.c1.sol">Sayt = 24/7 ishlaydigan sotuvchi</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">🐌</span>
      <div class="pain-title" data-i18n="pain.c2.title">"Sayt bor, lekin juda sekin"</div>
      <div class="pain-desc" data-i18n="pain.c2.desc">3 soniyadan ko'p kutgan foydalanuvchilarning 53% sahifani tark etadi. Sekin sayt = yo'qolgan sotuvlar.</div>
      <div class="pain-solution" data-i18n="pain.c2.sol">1 soniyadan tez yuklanishni kafolatlaymiz</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">📵</span>
      <div class="pain-title" data-i18n="pain.c3.title">"Telefonda ko'rinmaydi"</div>
      <div class="pain-desc" data-i18n="pain.c3.desc">Bugungi kunda 78% tashrif mobil qurilmadan. Agar sayt mobil optimallashtirilmagan bo'lsa — chiqib ketishadi.</div>
      <div class="pain-solution" data-i18n="pain.c3.sol">Har qanday qurilmada mukammal</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">💸</span>
      <div class="pain-title" data-i18n="pain.c4.title">"Dasturchi juda qimmat so'radi"</div>
      <div class="pain-desc" data-i18n="pain.c4.desc">Ko'pchilik oddiy sayt uchun $500–$2000 so'raydi va oylar ketadi. Biznes esa kutib turolmaydi.</div>
      <div class="pain-solution" data-i18n="pain.c4.sol">$99 dan — 48 soatda tayyor</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">😰</span>
      <div class="pain-title" data-i18n="pain.c6.title">"O'zim o'zgarta olmayman"</div>
      <div class="pain-desc" data-i18n="pain.c6.desc">Narx o'zgartirmoqchi — dasturchi kerak. Rasm qo'shmoqchi — dasturchi kerak. Bu biznesni to'xtatadi.</div>
      <div class="pain-solution" data-i18n="pain.c6.sol">Admin panel — o'zingiz boshqarasiz</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">🛠️</span>
      <div class="pain-title" data-i18n="pain.c5.title">"Ertaga bitadi" sindromi</div>
      <div class="pain-desc" data-i18n="pain.c5.desc">Dasturchi bilan kelishasiz, lekin ish haftalab, oylab cho'ziladi. Vaqt o'tgani sari g'oyangiz "sovub" boradi. Biznesda vaqt — bu boy berilgan foyda.</div>
      <div class="pain-solution" data-i18n="pain.c5.sol">Aniq muddat: 48 soat ichida ishga tushiramiz</div>
    </div>
  </div>
</section>

<div class="arrow-pill-wrap">
  <div class="arrow-pill" data-i18n="arrow_pill">⚡ QuickWeb bu muammolarni hal qildi →</div>
</div>

<!-- FEATURES -->
<section id="features">
  <div class="section-tag" data-i18n="features.tag">// nima beramiz</div>
  <div class="section-title reveal" data-i18n="features.title">Har bir piksel — maqsadli.</div>
  <div class="features-layout">
    <div>
      <div class="feature-card reveal">
        <div class="feat-icon">⚡</div>
        <div><div class="feat-title" data-i18n="feat.f1.title">Ultra tezkor ishlash</div><div class="feat-desc" data-i18n="feat.f1.desc">Barcha qurilmalarda 1 soniyadan tez yuklanish. Foydalanuvchi kutmaydi — sotib oladi.</div></div>
      </div>
      <div class="feature-card reveal">
        <div class="feat-icon">📱</div>
        <div><div class="feat-title" data-i18n="feat.f2.title">Mobil birinchi yondashuv</div><div class="feat-desc" data-i18n="feat.f2.desc">Har qanday smartfon, planshet va kompyuterda mukammal ko'rinish.</div></div>
      </div>
      <div class="feature-card reveal">
        <div class="feat-icon">🔒</div>
        <div><div class="feat-title" data-i18n="feat.f3.title">SSL + Xavfsizlik</div><div class="feat-desc" data-i18n="feat.f3.desc">Bepul SSL sertifikati, ma'lumotlar shifrlangan — mijozlaringiz ishonadi.</div></div>
      </div>
      <div class="feature-card reveal">
        <div class="feat-icon">📬</div>
        <div><div class="feat-title" data-i18n="feat.f4.title">Telegram integratsiya</div><div class="feat-desc" data-i18n="feat.f4.desc">Saytdan kelgan har bir so'rov darhol Telegramingizga tushadi. Hech narsa o'tkazib yuborilmaydi.</div></div>
      </div>
    </div>
    <div>
      <div class="preview-block reveal">
        <div class="preview-bar">
          <div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div>
          <div class="preview-url">quickweb.uz</div>
        </div>
        <div class="preview-content">
          <div class="preview-hero-block">
            <div class="preview-h1" data-i18n="preview.h1">Sizning Biznesingiz ⚡</div>
            <p class="preview-p" data-i18n="preview.p">Professional va tez sayt — mijozlar sizni taniydi</p>
            <div class="preview-btn-sm" data-i18n="preview.btn">Buyurtma berish →</div>
          </div>
          <div class="preview-cards">
            <div class="preview-card-sm"><div class="pbar"></div><div class="pline"></div><div class="pline" style="width:60%"></div></div>
            <div class="preview-card-sm"><div class="pbar" style="opacity:.3;width:70%"></div><div class="pline"></div><div class="pline" style="width:80%"></div></div>
            <div class="preview-card-sm"><div class="pbar" style="opacity:.15;width:50%"></div><div class="pline"></div><div class="pline" style="width:45%"></div></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PROCESS -->
<section id="process">
  <div class="section-tag" data-i18n="process.tag">// qanday ishlaydi</div>
  <div class="section-title reveal" data-i18n="process.title">4 qadamda — saytingiz tayyor.</div>
  <div class="steps-grid">
    <div class="step reveal"><div class="step-top-line"></div><div class="step-num">01 —</div><div class="step-icon">💬</div><div class="step-title" data-i18n="proc.s1.title">Muloqot</div><div class="step-desc" data-i18n="proc.s1.desc">Biznes haqida gaplashamiz, maqsadlarni aniqlaymiz.</div></div>
    <div class="step reveal"><div class="step-top-line"></div><div class="step-num">02 —</div><div class="step-icon">🎨</div><div class="step-title" data-i18n="proc.s2.title">Dizayn</div><div class="step-desc" data-i18n="proc.s2.desc">Brendingizga mos eksklyuziv dizayn tayyorlanadi.</div></div>
    <div class="step reveal"><div class="step-top-line"></div><div class="step-num">03 —</div><div class="step-icon">⚙️</div><div class="step-title" data-i18n="proc.s3.title">Ishlab chiqish</div><div class="step-desc" data-i18n="proc.s3.desc">48 soat ichida to'liq ishlayotgan sayt serverga joylashtiriladi.</div></div>
    <div class="step reveal"><div class="step-top-line"></div><div class="step-num">04 —</div><div class="step-icon">🚀</div><div class="step-title" data-i18n="proc.s4.title">Topshirish</div><div class="step-desc" data-i18n="proc.s4.desc">Domenga ulanadi, testdan o'tkaziladi. Biznes ishlaydi.</div></div>
  </div>
</section>

<!-- PRICING -->
<section id="pricing">
  <div class="pricing-header">
    <div class="section-tag" data-i18n="pricing.tag">// tariflar</div>
    <div class="section-title reveal" style="margin:0 auto" data-i18n="pricing.title">O'zingizga mos tanlang.</div>
  </div>
  <div class="pricing-grid">
    <div class="plan reveal">
      <div class="plan-tag" data-i18n="plan1.tag">⚡ START</div>
      <div class="plan-icon">🚀</div>
      <div class="plan-name">START</div>
      <div class="plan-desc" data-i18n="plan1.desc">Biznesini internetda tez va sifatli ko'rsatishni xohlovchi tadbirkorlar uchun.</div>
      <div class="plan-price"><sup>$</sup>99</div>
      <div class="plan-per" data-i18n="plan1.per">bir martalik to'lov</div>
      <ul class="plan-features">
        <li data-i18n="plan1.f1">Ko'p sahifali sayt (Bosh, Menyu, Haqimizda, Aloqa)</li>
        <li data-i18n="plan1.f2">Onlayn savatcha va buyurtma tizimi</li>
        <li data-i18n="plan1.f3">Serverga joylashtirish + domenga ulash</li>
        <li data-i18n="plan1.f4">Barcha smartfonlarda mobil optimizatsiya</li>
        <li data-i18n="plan1.f5">SSL sertifikati — bepul</li>
      </ul>
      <button class="plan-btn plan-btn-outline" data-open-order data-plan="START $99" data-i18n="plan1.btn">Buyurtma berish</button>
    </div>
    <div class="plan featured reveal">
      <div class="plan-tag" data-i18n="plan2.tag">🏢 BIZNES — Eng mashhur</div>
      <div class="plan-icon">💎</div>
      <div class="plan-name">BIZNES</div>
      <div class="plan-desc" data-i18n="plan2.desc">To'liq avtomatlashtirilgan, yuqori nufuzga ega professional platforma.</div>
      <div class="plan-price"><sup>$</sup>199</div>
      <div class="plan-per" data-i18n="plan2.per">bir martalik to'lov</div>
      <ul class="plan-features">
        <li data-i18n="plan2.f1">Eksklyuziv dizayn — logotip va brendingizga mos</li>
        <li data-i18n="plan2.f2">Kengaytirilgan katalog — filtrlash, tavsiflar</li>
        <li data-i18n="plan2.f3">SEO tayyorgarlik — Google va Yandexda yuqori o'rin</li>
        <li data-i18n="plan2.f4">Ko'p tilli qo'llab-quvvatlash</li>
      </ul>
      <button class="plan-btn plan-btn-fill" data-open-order data-plan="BIZNES $199" data-i18n="plan2.btn">Hoziroq boshlash →</button>
    </div>
  </div>
</section>

<!-- CTA -->
<section class="cta-section" id="contact">
  <div class="cta-bg"></div>
  <div class="section-tag" style="display:inline-block;position:relative" data-i18n="cta.tag">// bog'laning</div>
  <h2 style="margin-top:1rem"><span data-i18n="cta.h2_a">Saytingiz</span><br><span style="color:var(--acid)" data-i18n="cta.h2_b">bugun</span> <span data-i18n="cta.h2_c">tayyor.</span></h2>
  <p data-i18n="cta.sub">Savollaringiz bormi? Yoki darhol boshlashni xohlaysizmi? Biz doim shu yerda.</p>
  <div class="cta-buttons">
    <a href="https://t.me/QuickWweb" target="_blank" rel="noopener" class="btn-tg">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm5.562 8.069l-2.07 9.754c-.155.697-.567.867-1.148.538l-3.185-2.347-1.537 1.479c-.17.17-.312.312-.64.312l.228-3.237 5.894-5.322c.256-.228-.056-.355-.397-.127L6.43 14.47l-3.138-.979c-.68-.213-.694-.68.143-.997l12.26-4.73c.566-.21 1.063.127.867.305z"/></svg>
      Telegram: @QuickWweb
    </a>
    <a href="tel:+998903497778" class="btn-primary">📞 +998 90 349 77 78</a>
  </div>
</section>

<!-- ============= ORDER OVERLAY ============= -->
<div class="order-overlay" id="orderOverlay" role="dialog" aria-modal="true" aria-labelledby="orderTitle">
  <div class="order-panel">
    <button class="order-close" id="orderClose" aria-label="Close">×</button>

    <div class="order-header">
      <div class="section-tag" data-i18n="order.tag">// buyurtma berish</div>
      <h2 id="orderTitle" data-i18n="order.title">Saytingizni yaratamiz.</h2>
      <p data-i18n="order.subtitle">Ma'lumotlarni qoldiring — 1 soat ichida bog'lanamiz.</p>
    </div>

    <form class="order-form" id="orderForm" action="https://formsubmit.co/Kudratiys@gmail.com" method="POST">
      <input type="hidden" name="_subject" value="QuickWeb — Yangi buyurtma">
      <input type="hidden" name="_captcha" value="false">
      <input type="hidden" name="_template" value="table">
      <input type="hidden" name="_next" id="formNext" value="">

      <div class="form-row">
        <input type="text" name="Ism" required data-i18n-ph="order.ph.name" placeholder="Ismingiz">
        <input type="tel" name="Telefon" required data-i18n-ph="order.ph.phone" placeholder="+998 XX XXX XX XX">
      </div>
      <input type="email" name="Email" data-i18n-ph="order.ph.email" placeholder="email@example.com (ixtiyoriy)">
      <select name="Tarif" id="orderPlan" required>
        <option value="" data-i18n="order.plan.default">Tarifni tanlang</option>
        <option value="START $99" data-i18n="order.plan.start">START — $99</option>
        <option value="BIZNES $199" data-i18n="order.plan.biznes">BIZNES — $199</option>
        <option value="Maslahat" data-i18n="order.plan.consult">Maslahat kerak</option>
      </select>
      <textarea name="Xabar" rows="4" data-i18n-ph="order.ph.message" placeholder="Loyihangiz haqida qisqacha..."></textarea>
      <button type="submit" class="form-submit" data-i18n="order.submit">Buyurtma yuborish →</button>
    </form>

    <div class="order-divider" data-i18n="order.divider">yoki to'g'ridan-to'g'ri</div>

    <div class="order-contacts">
      <a href="https://t.me/QuickWweb" target="_blank" rel="noopener">
        <span class="ic tg">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm5.562 8.069l-2.07 9.754c-.155.697-.567.867-1.148.538l-3.185-2.347-1.537 1.479c-.17.17-.312.312-.64.312l.228-3.237 5.894-5.322c.256-.228-.056-.355-.397-.127L6.43 14.47l-3.138-.979c-.68-.213-.694-.68.143-.997l12.26-4.73c.566-.21 1.063.127.867.305z"/></svg>
        </span>
        Telegram: @QuickWweb
      </a>
      <a href="tel:+998903497778">
        <span class="ic tel">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72c.13.96.36 1.9.7 2.81a2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.91.34 1.85.57 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
        </span>
        +998 90 349 77 78
      </a>
    </div>
  </div>
</div>

<!-- FOOTER -->
<footer>
  <a href="#" class="logo" style="font-size:0.95rem">
    <svg class="logo-mark" style="width:24px;height:24px"><use href="#qw-logo"/></svg>
    <span style="color:var(--text)">Quick</span><span>Web</span>
  </a>
  <p data-i18n="footer.copy">© 2025 QuickWeb — Professional sayt yaratish xizmati</p>
  <p style="color:rgba(200,255,0,0.5)" data-i18n="footer.loc">Toshkent, O'zbekiston</p>
</footer>

<script>
/* ============================================================
   I18N
============================================================ */
const I18N = {
  uz: {
    'nav.problems':'Muammolar','nav.features':'Imkoniyatlar','nav.pricing':'Narxlar','nav.contact':"Bog'lanish",'nav.order':'Buyurtma qilish',
    'hero.badge':'⚡ Sayt yaratishda yangi standart',
    'hero.h1_line1':'Biznesingiz','hero.h1_line3':'kuchli.',
    'hero.sub':"Tez, zamonaviy va mijozlarni qozonuvchi saytlar. Faqat natijaga yo'naltirilgan yondashuv — chiroyli emas, <em>ishlaydi</em>.",
    'hero.cta_consult':'Bepul maslahat →','hero.cta_pricing':"Narxlarni ko'rish",
    'hero.stat1':"O'rtacha topshirish",'hero.stat2':'Mobil optimallashtirish','hero.stat3':'Topshirilgan saytlar','hero.stat4':'Xavfsizlik bepul',
    'pain.tag':'// odamlar duch keladigan muammolar',
    'pain.title':"Saytingiz yo'qmi?<br>Bu sizga qancha turadi.",
    'pain.subtitle':"Har kuni saytisiz bizneslar minglab mijozlarni yo'qotmoqda. Siz qaysi muammoni his qilyapsiz?",
    'pain.c1.title':'"Sayt yo\'q — mijozlar topilmaydi"',
    'pain.c1.desc':"Google'da qidirishadi — siz topilmaysiz. Raqibingiz topiladi. Mijoz unikiga boradi. Har kuni shunday.",
    'pain.c1.sol':'Sayt = 24/7 ishlaydigan sotuvchi',
    'pain.c2.title':'"Sayt bor, lekin juda sekin"',
    'pain.c2.desc':"3 soniyadan ko'p kutgan foydalanuvchilarning 53% sahifani tark etadi. Sekin sayt = yo'qolgan sotuvlar.",
    'pain.c2.sol':'1 soniyadan tez yuklanishni kafolatlaymiz',
    'pain.c3.title':'"Telefonda ko\'rinmaydi"',
    'pain.c3.desc':"Bugungi kunda 78% tashrif mobil qurilmadan. Agar sayt mobil optimallashtirilmagan bo'lsa — chiqib ketishadi.",
    'pain.c3.sol':'Har qanday qurilmada mukammal',
    'pain.c4.title':'"Dasturchi juda qimmat so\'radi"',
    'pain.c4.desc':"Ko'pchilik oddiy sayt uchun $500–$2000 so'raydi va oylar ketadi. Biznes esa kutib turolmaydi.",
    'pain.c4.sol':'$99 dan — 48 soatda tayyor',
    'pain.c5.title':'"Ertaga bitadi" sindromi',
    'pain.c5.desc':'Dasturchi bilan kelishasiz, lekin ish haftalab, oylab cho\'ziladi. Vaqt o\'tgani sari g\'oyangiz "sovub" boradi. Biznesda vaqt — bu boy berilgan foyda.',
    'pain.c5.sol':'Aniq muddat: 48 soat ichida ishga tushiramiz',
    'pain.c6.title':'"O\'zim o\'zgarta olmayman"',
    'pain.c6.desc':'Narx o\'zgartirmoqchi — dasturchi kerak. Rasm qo\'shmoqchi — dasturchi kerak. Bu biznesni to\'xtatadi.',
    'pain.c6.sol':"Admin panel — o'zingiz boshqarasiz",
    'arrow_pill':'⚡ QuickWeb bu muammolarni hal qildi →',
    'features.tag':'// nima beramiz','features.title':'Har bir piksel — maqsadli.',
    'feat.f1.title':'Ultra tezkor ishlash','feat.f1.desc':'Barcha qurilmalarda 1 soniyadan tez yuklanish. Foydalanuvchi kutmaydi — sotib oladi.',
    'feat.f2.title':'Mobil birinchi yondashuv','feat.f2.desc':'Har qanday smartfon, planshet va kompyuterda mukammal ko\'rinish.',
    'feat.f3.title':'SSL + Xavfsizlik','feat.f3.desc':'Bepul SSL sertifikati, ma\'lumotlar shifrlangan — mijozlaringiz ishonadi.',
    'feat.f4.title':'Telegram integratsiya','feat.f4.desc':"Saytdan kelgan har bir so'rov darhol Telegramingizga tushadi. Hech narsa o'tkazib yuborilmaydi.",
    'preview.h1':'Sizning Biznesingiz ⚡','preview.p':'Professional va tez sayt — mijozlar sizni taniydi','preview.btn':'Buyurtma berish →',
    'process.tag':'// qanday ishlaydi','process.title':'4 qadamda — saytingiz tayyor.',
    'proc.s1.title':'Muloqot','proc.s1.desc':'Biznes haqida gaplashamiz, maqsadlarni aniqlaymiz.',
    'proc.s2.title':'Dizayn','proc.s2.desc':'Brendingizga mos eksklyuziv dizayn tayyorlanadi.',
    'proc.s3.title':'Ishlab chiqish','proc.s3.desc':"48 soat ichida to'liq ishlayotgan sayt serverga joylashtiriladi.",
    'proc.s4.title':'Topshirish','proc.s4.desc':"Domenga ulanadi, testdan o'tkaziladi. Biznes ishlaydi.",
    'pricing.tag':'// tariflar','pricing.title':"O'zingizga mos tanlang.",
    'plan1.tag':'⚡ START',
    'plan1.desc':"Biznesini internetda tez va sifatli ko'rsatishni xohlovchi tadbirkorlar uchun.",
    'plan1.per':'bir martalik to\'lov',
    'plan1.f1':"Ko'p sahifali sayt (Bosh, Menyu, Haqimizda, Aloqa)",
    'plan1.f2':'Onlayn savatcha va buyurtma tizimi',
    'plan1.f3':'Serverga joylashtirish + domenga ulash',
    'plan1.f4':'Barcha smartfonlarda mobil optimizatsiya',
    'plan1.f5':'SSL sertifikati — bepul',
    'plan1.btn':'Buyurtma berish',
    'plan2.tag':'🏢 BIZNES — Eng mashhur',
    'plan2.desc':"To'liq avtomatlashtirilgan, yuqori nufuzga ega professional platforma.",
    'plan2.per':'bir martalik to\'lov',
    'plan2.f1':'Eksklyuziv dizayn — logotip va brendingizga mos',
    'plan2.f2':'Kengaytirilgan katalog — filtrlash, tavsiflar',
    'plan2.f3':'SEO tayyorgarlik — Google va Yandexda yuqori o\'rin',
    'plan2.f4':"Ko'p tilli qo'llab-quvvatlash",
    'plan2.btn':'Hoziroq boshlash →',
    'cta.tag':'// bog\'laning','cta.h2_a':'Saytingiz','cta.h2_b':'bugun','cta.h2_c':'tayyor.',
    'cta.sub':'Savollaringiz bormi? Yoki darhol boshlashni xohlaysizmi? Biz doim shu yerda.',
    'order.tag':'// buyurtma berish','order.title':'Saytingizni yaratamiz.','order.subtitle':"Ma'lumotlarni qoldiring — 1 soat ichida bog'lanamiz.",
    'order.ph.name':'Ismingiz','order.ph.phone':'+998 XX XXX XX XX','order.ph.email':'email@example.com (ixtiyoriy)','order.ph.message':'Loyihangiz haqida qisqacha...',
    'order.plan.default':'Tarifni tanlang','order.plan.start':'START — $99','order.plan.biznes':'BIZNES — $199','order.plan.consult':'Maslahat kerak',
    'order.submit':'Buyurtma yuborish →','order.divider':"yoki to'g'ridan-to'g'ri",
    'footer.copy':'© 2025 QuickWeb — Professional sayt yaratish xizmati','footer.loc':"Toshkent, O'zbekiston"
  },
  ru: {
    'nav.problems':'Проблемы','nav.features':'Возможности','nav.pricing':'Цены','nav.contact':'Контакты','nav.order':'Заказать',
    'hero.badge':'⚡ Новый стандарт создания сайтов',
    'hero.h1_line1':'Ваш бизнес','hero.h1_line3':'мощный.',
    'hero.sub':'Быстрые, современные сайты, которые приводят клиентов. Подход, ориентированный на результат — не просто красиво, а <em>работает</em>.',
    'hero.cta_consult':'Бесплатная консультация →','hero.cta_pricing':'Посмотреть цены',
    'hero.stat1':'Среднее время сдачи','hero.stat2':'Мобильная оптимизация','hero.stat3':'Сданных сайтов','hero.stat4':'Безопасность бесплатно',
    'pain.tag':'// проблемы, с которыми сталкиваются',
    'pain.title':'Нет сайта?<br>Это вам дорого обходится.',
    'pain.subtitle':'Каждый день бизнес без сайта теряет тысячи клиентов. Какую проблему ощущаете вы?',
    'pain.c1.title':'«Нет сайта — клиенты не находят»',
    'pain.c1.desc':'Они ищут в Google — вас не находят. Находят конкурента. Клиент уходит к нему. Так каждый день.',
    'pain.c1.sol':'Сайт = продавец, работающий 24/7',
    'pain.c2.title':'«Сайт есть, но очень медленный»',
    'pain.c2.desc':'53% пользователей покидают страницу, ждущую более 3 секунд. Медленный сайт = потерянные продажи.',
    'pain.c2.sol':'Гарантируем загрузку быстрее 1 секунды',
    'pain.c3.title':'«На телефоне не отображается»',
    'pain.c3.desc':'Сегодня 78% посещений с мобильных. Если сайт не оптимизирован — уходят сразу.',
    'pain.c3.sol':'Идеально на любом устройстве',
    'pain.c4.title':'«Разработчик запросил очень дорого»',
    'pain.c4.desc':'Многие просят $500–$2000 за обычный сайт и тратят месяцы. Бизнес не может ждать.',
    'pain.c4.sol':'От $99 — готов за 48 часов',
    'pain.c5.title':'Синдром «Завтра будет готово»',
    'pain.c5.desc':'Договариваетесь с разработчиком, но работа растягивается на недели и месяцы. Ваша идея «остывает». В бизнесе время — это упущенная прибыль.',
    'pain.c5.sol':'Чёткий срок: запуск за 48 часов',
    'pain.c6.title':'«Сам ничего изменить не могу»',
    'pain.c6.desc':'Хочешь изменить цену — нужен разработчик. Добавить фото — нужен разработчик. Это тормозит бизнес.',
    'pain.c6.sol':'Админ-панель — управляете сами',
    'arrow_pill':'⚡ QuickWeb решил эти проблемы →',
    'features.tag':'// что мы даём','features.title':'Каждый пиксель — с целью.',
    'feat.f1.title':'Ультра-быстрая работа','feat.f1.desc':'Загрузка быстрее 1 секунды на любых устройствах. Пользователь не ждёт — покупает.',
    'feat.f2.title':'Mobile-first подход','feat.f2.desc':'Идеальный вид на любом смартфоне, планшете и компьютере.',
    'feat.f3.title':'SSL + Безопасность','feat.f3.desc':'Бесплатный SSL-сертификат, шифрование данных — клиенты доверяют.',
    'feat.f4.title':'Интеграция с Telegram','feat.f4.desc':'Каждая заявка с сайта мгновенно приходит в Telegram. Ничего не пропустите.',
    'preview.h1':'Ваш бизнес ⚡','preview.p':'Профессиональный быстрый сайт — клиенты вас узнают','preview.btn':'Заказать →',
    'process.tag':'// как это работает','process.title':'4 шага — и сайт готов.',
    'proc.s1.title':'Общение','proc.s1.desc':'Обсуждаем бизнес, определяем цели.',
    'proc.s2.title':'Дизайн','proc.s2.desc':'Готовим эксклюзивный дизайн под ваш бренд.',
    'proc.s3.title':'Разработка','proc.s3.desc':'За 48 часов полностью рабочий сайт размещаем на сервере.',
    'proc.s4.title':'Сдача','proc.s4.desc':'Подключаем к домену, тестируем. Бизнес работает.',
    'pricing.tag':'// тарифы','pricing.title':'Выберите подходящий.',
    'plan1.tag':'⚡ START','plan1.desc':'Для предпринимателей, желающих быстро и качественно показать бизнес в интернете.',
    'plan1.per':'разовая оплата',
    'plan1.f1':'Многостраничный сайт (Главная, Меню, О нас, Контакты)',
    'plan1.f2':'Онлайн-корзина и система заказов',
    'plan1.f3':'Размещение на сервере + подключение к домену',
    'plan1.f4':'Мобильная оптимизация для всех смартфонов',
    'plan1.f5':'SSL-сертификат — бесплатно',
    'plan1.btn':'Заказать',
    'plan2.tag':'🏢 BIZNES — Самый популярный',
    'plan2.desc':'Полностью автоматизированная, престижная профессиональная платформа.',
    'plan2.per':'разовая оплата',
    'plan2.f1':'Эксклюзивный дизайн — под логотип и бренд',
    'plan2.f2':'Расширенный каталог — фильтры, описания',
    'plan2.f3':'SEO-подготовка — высокие позиции в Google и Яндекс',
    'plan2.f4':'Многоязычная поддержка',
    'plan2.btn':'Начать сейчас →',
    'cta.tag':'// связаться','cta.h2_a':'Ваш сайт','cta.h2_b':'сегодня','cta.h2_c':'готов.',
    'cta.sub':'Есть вопросы? Или хотите начать прямо сейчас? Мы всегда здесь.',
    'order.tag':'// оформить заказ','order.title':'Создадим ваш сайт.','order.subtitle':'Оставьте данные — свяжемся в течение часа.',
    'order.ph.name':'Ваше имя','order.ph.phone':'+998 XX XXX XX XX','order.ph.email':'email@example.com (необязательно)','order.ph.message':'Кратко о вашем проекте...',
    'order.plan.default':'Выберите тариф','order.plan.start':'START — $99','order.plan.biznes':'BIZNES — $199','order.plan.consult':'Нужна консультация',
    'order.submit':'Отправить заявку →','order.divider':'или напрямую',
    'footer.copy':'© 2025 QuickWeb — Услуги профессиональной разработки сайтов','footer.loc':'Ташкент, Узбекистан'
  },
  en: {
    'nav.problems':'Problems','nav.features':'Features','nav.pricing':'Pricing','nav.contact':'Contact','nav.order':'Order Now',
    'hero.badge':'⚡ The new standard in web creation',
    'hero.h1_line1':'Your business','hero.h1_line3':'powerful.',
    'hero.sub':'Fast, modern websites that win customers. A results-driven approach — not just pretty, but <em>it works</em>.',
    'hero.cta_consult':'Free consultation →','hero.cta_pricing':'View pricing',
    'hero.stat1':'Average delivery','hero.stat2':'Mobile optimization','hero.stat3':'Sites delivered','hero.stat4':'Security included',
    'pain.tag':'// problems people face',
    'pain.title':"Don't have a website?<br>Here's what it costs you.",
    'pain.subtitle':'Every day, businesses without a website lose thousands of customers. Which problem do you feel?',
    'pain.c1.title':'"No site — customers can\'t find me"',
    'pain.c1.desc':'They search on Google — you\'re not there. Your competitor is. The customer goes to them. Every day.',
    'pain.c1.sol':'A website = a 24/7 salesperson',
    'pain.c2.title':'"Site exists, but it\'s too slow"',
    'pain.c2.desc':'53% of users abandon a page that takes more than 3 seconds. Slow site = lost sales.',
    'pain.c2.sol':'We guarantee sub-1-second loading',
    'pain.c3.title':'"It looks broken on mobile"',
    'pain.c3.desc':'Today 78% of visits come from mobile. If your site isn\'t optimized — they leave.',
    'pain.c3.sol':'Perfect on every device',
    'pain.c4.title':'"The developer asked way too much"',
    'pain.c4.desc':'Most ask $500–$2000 for a basic site and take months. Business can\'t wait.',
    'pain.c4.sol':'From $99 — ready in 48 hours',
    'pain.c5.title':'"It\'ll be done tomorrow" syndrome',
    'pain.c5.desc':'You agree with a developer, but the work drags on for weeks or months. Your idea cools off. In business, time means lost profit.',
    'pain.c5.sol':'A real deadline: live in 48 hours',
    'pain.c6.title':'"I can\'t change anything myself"',
    'pain.c6.desc':'Want to change a price — need a developer. Add a photo — need a developer. It paralyzes business.',
    'pain.c6.sol':'Admin panel — you\'re in control',
    'arrow_pill':'⚡ QuickWeb solved these problems →',
    'features.tag':'// what we deliver','features.title':'Every pixel — with purpose.',
    'feat.f1.title':'Ultra-fast performance','feat.f1.desc':'Sub-1-second loading on every device. Users don\'t wait — they buy.',
    'feat.f2.title':'Mobile-first approach','feat.f2.desc':'Looks perfect on any smartphone, tablet, or desktop.',
    'feat.f3.title':'SSL + Security','feat.f3.desc':'Free SSL certificate, encrypted data — your customers trust you.',
    'feat.f4.title':'Telegram integration','feat.f4.desc':'Every request from the site goes straight to your Telegram. Nothing missed.',
    'preview.h1':'Your Business ⚡','preview.p':'Professional fast site — customers will know you','preview.btn':'Order now →',
    'process.tag':'// how it works','process.title':'4 steps — your site is ready.',
    'proc.s1.title':'Discussion','proc.s1.desc':'We talk about your business and pin down the goals.',
    'proc.s2.title':'Design','proc.s2.desc':'An exclusive design tailored to your brand is prepared.',
    'proc.s3.title':'Development','proc.s3.desc':'Within 48 hours a fully working site is deployed to the server.',
    'proc.s4.title':'Delivery','proc.s4.desc':'Connected to the domain, tested, live. Business runs.',
    'pricing.tag':'// pricing','pricing.title':'Pick what fits you.',
    'plan1.tag':'⚡ START','plan1.desc':'For entrepreneurs who want to quickly and professionally appear online.',
    'plan1.per':'one-time payment',
    'plan1.f1':'Multi-page site (Home, Menu, About, Contact)',
    'plan1.f2':'Online cart and order system',
    'plan1.f3':'Server hosting + domain connection',
    'plan1.f4':'Mobile optimization for all smartphones',
    'plan1.f5':'SSL certificate — free',
    'plan1.btn':'Order',
    'plan2.tag':'🏢 BIZNES — Most popular',
    'plan2.desc':'A fully automated, prestigious, professional platform.',
    'plan2.per':'one-time payment',
    'plan2.f1':'Exclusive design — matched to your logo and brand',
    'plan2.f2':'Extended catalog — filters, descriptions',
    'plan2.f3':'SEO-ready — high rankings on Google and Yandex',
    'plan2.f4':'Multi-language support',
    'plan2.btn':'Start now →',
    'cta.tag':'// get in touch','cta.h2_a':'Your site','cta.h2_b':'today','cta.h2_c':'is ready.',
    'cta.sub':'Got questions? Or want to start right now? We\'re here.',
    'order.tag':'// place an order','order.title':'Let\'s build your site.','order.subtitle':'Leave your details — we\'ll get back within an hour.',
    'order.ph.name':'Your name','order.ph.phone':'+998 XX XXX XX XX','order.ph.email':'email@example.com (optional)','order.ph.message':'Briefly about your project...',
    'order.plan.default':'Choose a plan','order.plan.start':'START — $99','order.plan.biznes':'BIZNES — $199','order.plan.consult':'Need consultation',
    'order.submit':'Send request →','order.divider':'or directly',
    'footer.copy':'© 2025 QuickWeb — Professional website creation','footer.loc':'Tashkent, Uzbekistan'
  }
};

const TW_WORDS = {
  uz: ['raqamda','onlaynda','Googleda','kuchli'],
  ru: ['в цифре','онлайн','в Google','мощный'],
  en: ['digital','online','on Google','powerful']
};

const MARQUEE_ITEMS = {
  uz: ['Mobil Dizayn','SEO Optimizatsiya','Tezkor Topshirish','SSL Sertifikat','Admin Panel','Telegram Bot','Eksklyuziv Dizayn','Domenga Ulash'],
  ru: ['Мобильный дизайн','SEO-оптимизация','Быстрая сдача','SSL-сертификат','Админ-панель','Telegram-бот','Эксклюзивный дизайн','Подключение домена'],
  en: ['Mobile Design','SEO Optimization','Fast Delivery','SSL Certificate','Admin Panel','Telegram Bot','Exclusive Design','Domain Connection']
};

/* ============================================================
   THEME
============================================================ */
const themeBtn = document.getElementById('themeToggle');
function applyTheme(t) {
  document.documentElement.setAttribute('data-theme', t);
  themeBtn.textContent = t === 'dark' ? '☀' : '☾';
  themeBtn.setAttribute('aria-label', t === 'dark' ? 'Switch to light' : 'Switch to dark');
}
applyTheme(localStorage.getItem('qw-theme') || 'dark');
themeBtn.addEventListener('click', () => {
  const next = document.documentElement.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
  applyTheme(next);
  try { localStorage.setItem('qw-theme', next); } catch(e) {}
});

/* ============================================================
   I18N RUNTIME
============================================================ */
let currentLang = localStorage.getItem('qw-lang') || 'uz';
function setLang(lang) {
  if (!I18N[lang]) lang = 'uz';
  currentLang = lang;
  const dict = I18N[lang];

  document.querySelectorAll('[data-i18n]').forEach(el => {
    const key = el.dataset.i18n;
    if (dict[key] !== undefined) el.innerHTML = dict[key];
  });
  document.querySelectorAll('[data-i18n-ph]').forEach(el => {
    const key = el.dataset.i18nPh;
    if (dict[key] !== undefined) el.placeholder = dict[key];
  });

  document.documentElement.lang = lang;
  document.querySelectorAll('.lang-btn').forEach(b => b.classList.toggle('active', b.dataset.lang === lang));

  // Rebuild marquee
  buildMarquee(lang);
  // Reset typewriter
  resetTypewriter();

  try { localStorage.setItem('qw-lang', lang); } catch(e) {}
}
document.querySelectorAll('.lang-btn').forEach(btn => {
  btn.addEventListener('click', () => setLang(btn.dataset.lang));
});

/* ============================================================
   MARQUEE BUILD
============================================================ */
function buildMarquee(lang) {
  const track = document.getElementById('marqueeTrack');
  const items = MARQUEE_ITEMS[lang] || MARQUEE_ITEMS.uz;
  // duplicate twice for seamless scroll
  const seq = [...items, ...items];
  track.innerHTML = seq.map(t =>
    `<span class="marquee-item">${t} <span class="dot-sep">✦</span></span>`
  ).join('');
}

/* ============================================================
   ORDER OVERLAY
============================================================ */
const overlay = document.getElementById('orderOverlay');
const closeBtn = document.getElementById('orderClose');
const planSelect = document.getElementById('orderPlan');
const formNext = document.getElementById('formNext');
formNext.value = window.location.href.split('#')[0] + '?sent=1';

function openOrder(plan) {
  if (plan && planSelect) planSelect.value = plan;
  overlay.classList.add('open');
  document.body.classList.add('no-scroll');
}
function closeOrder() {
  overlay.classList.remove('open');
  document.body.classList.remove('no-scroll');
}

document.querySelectorAll('[data-open-order]').forEach(el => {
  el.addEventListener('click', e => {
    e.preventDefault();
    openOrder(el.dataset.plan || '');
  });
});
closeBtn.addEventListener('click', closeOrder);
overlay.addEventListener('click', e => { if (e.target === overlay) closeOrder(); });
document.addEventListener('keydown', e => { if (e.key === 'Escape' && overlay.classList.contains('open')) closeOrder(); });

// Show success banner if redirected back
if (new URLSearchParams(window.location.search).get('sent') === '1') {
  const msg = document.createElement('div');
  msg.style.cssText = 'position:fixed;top:80px;left:50%;transform:translateX(-50%);background:var(--acid);color:#080808;padding:0.9rem 1.5rem;border-radius:4px;font-family:Syne,sans-serif;font-weight:700;z-index:3000;box-shadow:0 12px 40px rgba(200,255,0,0.4)';
  const successMsg = { uz:'✓ Buyurtma yuborildi! Tez orada bog\'lanamiz.', ru:'✓ Заявка отправлена! Скоро свяжемся.', en:'✓ Request sent! We\'ll be in touch soon.' };
  msg.textContent = successMsg[currentLang] || successMsg.uz;
  document.body.appendChild(msg);
  setTimeout(() => msg.style.opacity = '0', 5000);
  setTimeout(() => msg.remove(), 5500);
}

/* ============================================================
   SCROLL PROGRESS
============================================================ */
const pb = document.getElementById('progressBar');
window.addEventListener('scroll', () => {
  pb.style.width = (window.scrollY / (document.body.scrollHeight - window.innerHeight) * 100) + '%';
});

/* ============================================================
   CURSOR + TRAIL (desktop only)
============================================================ */
const cursor = document.getElementById('cursor');
const canvas = document.getElementById('cursorCanvas');
const isDesktop = window.matchMedia('(min-width: 769px)').matches;

if (isDesktop) {
  const ctx = canvas.getContext('2d');
  let W = canvas.width = window.innerWidth, H = canvas.height = window.innerHeight;
  window.addEventListener('resize', () => { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight; });

  let mx = W/2, my = H/2;
  const pts = [];
  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx - 5 + 'px';
    cursor.style.top = my - 5 + 'px';
    pts.push({ x: mx, y: my, t: Date.now() });
    if (pts.length > 24) pts.shift();
  });
  document.addEventListener('mouseover', e => {
    if (e.target.closest('a,button,input,select,textarea')) cursor.classList.add('big');
  });
  document.addEventListener('mouseout', e => {
    if (e.target.closest('a,button,input,select,textarea')) cursor.classList.remove('big');
  });
  (function loop() {
    ctx.clearRect(0, 0, W, H);
    const now = Date.now();
    for (let i = 1; i < pts.length; i++) {
      const age = (now - pts[i].t) / 400;
      if (age > 1) continue;
      const alpha = (1 - age) * 0.22 * (i / pts.length);
      const r = (i / pts.length) * 5;
      ctx.beginPath();
      ctx.arc(pts[i].x, pts[i].y, r, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(200,255,0,${alpha})`;
      ctx.fill();
    }
    requestAnimationFrame(loop);
  })();
} else {
  cursor.style.display = 'none';
  canvas.style.display = 'none';
}

/* ============================================================
   PARTICLES
============================================================ */
const pc = document.getElementById('particles');
for (let i = 0; i < 14; i++) {
  const p = document.createElement('div');
  p.className = 'particle';
  const s = Math.random() * 2.5 + 1;
  p.style.cssText = `width:${s}px;height:${s}px;left:${Math.random()*100}%;animation-duration:${7+Math.random()*10}s;animation-delay:${Math.random()*10}s;opacity:0;`;
  pc.appendChild(p);
}

/* ============================================================
   TYPEWRITER
============================================================ */
const twEl = document.getElementById('tw');
let twWi = 0, twCi = 0, twDeleting = false, twTimer = null;
function tw() {
  const words = TW_WORDS[currentLang] || TW_WORDS.uz;
  const w = words[twWi % words.length];
  if (!twDeleting) {
    twEl.textContent = w.slice(0, ++twCi);
    if (twCi === w.length) { twDeleting = true; twTimer = setTimeout(tw, 1800); return; }
    twTimer = setTimeout(tw, 90);
  } else {
    twEl.textContent = w.slice(0, --twCi);
    if (twCi === 0) { twDeleting = false; twWi = (twWi + 1) % words.length; twTimer = setTimeout(tw, 300); return; }
    twTimer = setTimeout(tw, 45);
  }
}
function resetTypewriter() {
  if (twTimer) clearTimeout(twTimer);
  twWi = 0; twCi = 0; twDeleting = false;
  twEl.textContent = '';
  tw();
}

/* ============================================================
   COUNTERS + INTERSECTION OBSERVER
============================================================ */
function runCounter(el) {
  const target = parseInt(el.dataset.count);
  const suffix = el.dataset.suffix || '';
  if (!target) return;
  let cur = 0; const step = target / 45;
  const t = setInterval(() => {
    cur = Math.min(cur + step, target);
    el.textContent = Math.round(cur) + suffix;
    if (cur >= target) clearInterval(t);
  }, 28);
}

const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      if (e.target.dataset.count) runCounter(e.target);
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.reveal, .feature-card, .pain-card, .step, .preview-block').forEach((el, i) => {
  el.style.transitionDelay = (i % 4 * 0.1) + 's';
  obs.observe(el);
});
document.querySelectorAll('.stat-num[data-count]').forEach(el => obs.observe(el));

/* ============================================================
   PARALLAX
============================================================ */
window.addEventListener('scroll', () => {
  const g = document.querySelector('.hero-grid');
  if (g) g.style.transform = `translateY(${window.scrollY * 0.12}px)`;
});

/* ============================================================
   INIT
============================================================ */
setLang(currentLang); // builds marquee + starts typewriter
</script>
</body>
</html><!DOCTYPE html>
<html lang="uz" data-theme="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>QuickWeb — Professional Sayt Yaratish</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --acid: #c8ff00;
    --acid-fg: #c8ff00;
    --acid-tint: rgba(200,255,0,0.05);
    --acid-tint-strong: rgba(200,255,0,0.12);
    --acid-border: rgba(200,255,0,0.3);
    --acid-border-soft: rgba(200,255,0,0.18);

    /* DARK THEME (default) */
    --bg: #080808;
    --bg-alt: #111111;
    --bg-card: #0d0d0d;
    --bg-card-hover: #111111;
    --bg-marquee: #0d0d0d;
    --text: #f5f5f0;
    --text-muted: #777;
    --text-soft: #bbb;
    --border: rgba(255,255,255,0.05);
    --border-strong: rgba(255,255,255,0.12);
    --tint: rgba(255,255,255,0.025);
    --tint-strong: rgba(255,255,255,0.04);
    --noise-opacity: 0.5;
    --nav-bg: rgba(8,8,8,0.8);
    --preview-bar: #1a1a1a;
    --preview-card: #1a1a1a;
    --plan-featured: linear-gradient(160deg, #0e1500 0%, #0a0a0a 100%);
    --pline: rgba(255,255,255,0.07);
    --cursor-blend: exclusion;
  }

  [data-theme="light"] {
    --acid-fg: #4d6800;
    --acid-tint: rgba(77,104,0,0.08);
    --acid-tint-strong: rgba(77,104,0,0.18);
    --acid-border: rgba(77,104,0,0.5);
    --acid-border-soft: rgba(77,104,0,0.35);
    --bg: #f5f5f0;
    --bg-alt: #ebebe5;
    --bg-card: #ffffff;
    --bg-card-hover: #fafaf3;
    --bg-marquee: #ebebe5;
    --text: #0a0a0a;
    --text-muted: #6a6a6a;
    --text-soft: #333;
    --border: rgba(0,0,0,0.07);
    --border-strong: rgba(0,0,0,0.14);
    --tint: rgba(0,0,0,0.025);
    --tint-strong: rgba(0,0,0,0.04);
    --noise-opacity: 0.25;
    --nav-bg: rgba(245,245,240,0.85);
    --preview-bar: #e8e8e0;
    --preview-card: #fafaf3;
    --plan-featured: linear-gradient(160deg, #f0f8d8 0%, #fafaf3 100%);
    --pline: rgba(0,0,0,0.08);
    --cursor-blend: difference;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }
  body { background: var(--bg); color: var(--text); font-family: 'Inter', sans-serif; overflow-x: hidden; cursor: none; transition: background 0.3s, color 0.3s; }
  body.no-scroll { overflow: hidden; }

  /* CURSOR */
  .cursor { width: 10px; height: 10px; background: var(--acid); border-radius: 50%; position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9999; mix-blend-mode: var(--cursor-blend); transition: transform 0.15s ease; }
  .cursor.big { transform: scale(4.5); }
  .cursor-canvas { position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9997; }

  /* NOISE */
  body::before { content: ''; position: fixed; inset: 0; background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E"); pointer-events: none; z-index: 200; opacity: var(--noise-opacity); }

  /* NAV */
  nav { position: fixed; top: 0; left: 0; right: 0; z-index: 500; display: flex; justify-content: space-between; align-items: center; padding: 1rem 4rem; border-bottom: 1px solid var(--border); backdrop-filter: blur(16px); background: var(--nav-bg); gap: 1rem; transition: background 0.3s, border-color 0.3s; }
  .logo { display: inline-flex; align-items: center; gap: 0.55rem; font-family: 'Syne', sans-serif; font-weight: 800; font-size: 1.2rem; letter-spacing: -0.03em; color: var(--text); text-decoration: none; flex-shrink: 0; }
  .logo-mark { width: 30px; height: 30px; color: var(--acid-fg); flex-shrink: 0; }
  .logo span { color: var(--acid-fg); }
  nav ul { list-style: none; display: flex; gap: 2.2rem; }
  nav ul a { font-family: 'Space Mono', monospace; font-size: 0.68rem; color: var(--text-muted); text-decoration: none; letter-spacing: 0.1em; text-transform: uppercase; transition: color 0.2s; }
  nav ul a:hover { color: var(--acid-fg); }

  .nav-tools { display: flex; align-items: center; gap: 0.6rem; flex-shrink: 0; }

  /* THEME TOGGLE */
  .theme-toggle { background: transparent; border: 1px solid var(--border-strong); color: var(--text); width: 36px; height: 36px; border-radius: 50%; cursor: none; display: inline-flex; align-items: center; justify-content: center; font-size: 0.9rem; transition: border-color 0.2s, color 0.2s, background 0.2s; }
  .theme-toggle:hover { border-color: var(--acid-fg); color: var(--acid-fg); }

  /* LANG SWITCHER */
  .lang-switcher { display: inline-flex; border: 1px solid var(--border-strong); border-radius: 999px; padding: 2px; }
  .lang-btn { background: transparent; border: none; color: var(--text-muted); font-family: 'Space Mono', monospace; font-size: 0.62rem; letter-spacing: 0.08em; text-transform: uppercase; padding: 0.32rem 0.6rem; cursor: none; border-radius: 999px; transition: color 0.2s, background 0.2s; }
  .lang-btn:hover { color: var(--text); }
  .lang-btn.active { background: var(--acid); color: #080808; font-weight: 700; }

  /* NAV CTA — Buyurtma qilish */
  .nav-cta { background: var(--acid); color: #080808; padding: 0.55rem 1.2rem; border-radius: 2px; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.78rem; text-decoration: none; cursor: none; border: none; transition: transform 0.2s, box-shadow 0.2s; letter-spacing: -0.01em; white-space: nowrap; }
  .nav-cta:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(200,255,0,0.35); }

  /* HERO */
  .hero { min-height: 100vh; display: flex; flex-direction: column; justify-content: center; padding: 8rem 4rem 4rem; position: relative; overflow: hidden; }
  .hero-grid { position: absolute; inset: 0; background-image: linear-gradient(rgba(200,255,0,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(200,255,0,0.03) 1px, transparent 1px); background-size: 56px 56px; mask-image: radial-gradient(ellipse 80% 80% at 40% 50%, black 0%, transparent 75%); animation: gridShift 25s linear infinite; }
  [data-theme="light"] .hero-grid { background-image: linear-gradient(rgba(0,0,0,0.04) 1px, transparent 1px), linear-gradient(90deg, rgba(0,0,0,0.04) 1px, transparent 1px); }
  @keyframes gridShift { from{background-position:0 0} to{background-position:56px 56px} }
  .particles { position: absolute; inset: 0; pointer-events: none; overflow: hidden; }
  .particle { position: absolute; background: var(--acid); border-radius: 50%; animation: particleUp linear infinite; }
  @keyframes particleUp { 0%{transform:translateY(100vh);opacity:0} 5%{opacity:0.8} 90%{opacity:0.3} 100%{transform:translateY(-50px);opacity:0} }

  .hero-badge { display: inline-flex; align-items: center; gap: 0.5rem; font-family: 'Space Mono', monospace; font-size: 0.68rem; letter-spacing: 0.14em; color: var(--acid-fg); text-transform: uppercase; border: 1px solid rgba(200,255,0,0.3); padding: 0.4rem 0.9rem; border-radius: 2px; margin-bottom: 2rem; width: fit-content; animation: fadeUp 0.8s ease both; background: rgba(200,255,0,0.05); }
  .hero-badge::before { content: ''; width: 6px; height: 6px; background: var(--acid); border-radius: 50%; animation: ripplePulse 1.8s ease-in-out infinite; }
  @keyframes ripplePulse { 0%,100%{opacity:1;transform:scale(1);box-shadow:0 0 0 0 rgba(200,255,0,0.5)} 50%{opacity:0.5;transform:scale(1.4);box-shadow:0 0 0 8px rgba(200,255,0,0)} }

  .hero h1 { font-family: 'Syne', sans-serif; font-size: clamp(3.5rem, 9vw, 9rem); font-weight: 800; line-height: 0.9; letter-spacing: -0.04em; max-width: 950px; animation: fadeUp 0.9s 0.1s ease both; }
  .line-accent { color: var(--acid-fg); }
  .line-outline { -webkit-text-stroke: 1.5px var(--border-strong); color: transparent; }
  .typewriter-wrap { display: inline-block; position: relative; }
  .tw-word { border-right: 3px solid var(--acid-fg); display: inline; animation: blinkCaret 0.9s step-end infinite; }
  @keyframes blinkCaret { 0%,100%{border-color:var(--acid-fg)} 50%{border-color:transparent} }

  .hero-sub { max-width: 460px; font-size: 1rem; color: var(--text-muted); line-height: 1.75; margin-top: 2.5rem; font-weight: 300; animation: fadeUp 1s 0.2s ease both; }
  .hero-actions { display: flex; gap: 1rem; margin-top: 3rem; animation: fadeUp 1s 0.3s ease both; flex-wrap: wrap; }

  .btn-primary { background: var(--acid); color: #080808; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; padding: 1rem 2.2rem; border: none; border-radius: 2px; cursor: none; text-decoration: none; display: inline-flex; align-items: center; gap: 0.5rem; transition: transform 0.2s, box-shadow 0.2s; letter-spacing: -0.01em; position: relative; overflow: hidden; }
  .btn-primary::after { content: ''; position: absolute; inset: 0; background: linear-gradient(90deg, transparent, rgba(255,255,255,0.25), transparent); transform: translateX(-100%); transition: transform 0.45s ease; }
  .btn-primary:hover::after { transform: translateX(100%); }
  .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 12px 40px rgba(200,255,0,0.35); }

  .btn-outline { background: transparent; color: var(--text); font-family: 'Space Mono', monospace; font-size: 0.72rem; letter-spacing: 0.1em; text-transform: uppercase; padding: 1rem 2rem; border: 1px solid var(--border-strong); border-radius: 2px; cursor: none; text-decoration: none; transition: border-color 0.2s, color 0.2s, background 0.2s; }
  .btn-outline:hover { border-color: var(--acid-fg); color: var(--acid-fg); background: rgba(200,255,0,0.04); }

  .btn-tg { background: #0088cc; color: #fff; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; padding: 1rem 2rem; border-radius: 2px; cursor: none; text-decoration: none; display: inline-flex; align-items: center; gap: 0.6rem; transition: transform 0.2s, box-shadow 0.2s; }
  .btn-tg:hover { transform: translateY(-3px); box-shadow: 0 12px 40px rgba(0,136,204,0.35); }

  .hero-stats { display: flex; gap: 4rem; margin-top: 5rem; padding-top: 3rem; border-top: 1px solid var(--border); animation: fadeUp 1s 0.4s ease both; flex-wrap: wrap; }
  .stat-num { font-family: 'Syne', sans-serif; font-size: 2.4rem; font-weight: 800; color: var(--acid-fg); line-height: 1; }
  .stat-label { font-family: 'Space Mono', monospace; font-size: 0.62rem; color: var(--text-muted); margin-top: 0.35rem; letter-spacing: 0.06em; }

  /* MARQUEE */
  .marquee-wrap { overflow: hidden; padding: 0.9rem 0; border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); background: var(--bg-marquee); }
  .marquee-track { display: flex; gap: 2.5rem; animation: marqueeScroll 18s linear infinite; width: max-content; }
  .marquee-item { font-family: 'Space Mono', monospace; font-size: 0.68rem; letter-spacing: 0.15em; text-transform: uppercase; color: var(--text-muted); white-space: nowrap; display: flex; align-items: center; gap: 0.8rem; }
  .dot-sep { color: var(--acid-fg); }
  @keyframes marqueeScroll { from{transform:translateX(0)} to{transform:translateX(-50%)} }

  /* PAIN SECTION */
  .pain-section { padding: 8rem 4rem; background: var(--bg-alt); position: relative; overflow: hidden; }
  .pain-section::before { content: ''; position: absolute; left: 0; top: 0; bottom: 0; width: 2px; background: linear-gradient(to bottom, transparent, rgba(255,59,59,0.6), transparent); }

  .section-tag { font-family: 'Space Mono', monospace; font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--acid-fg); margin-bottom: 1rem; }
  .section-title { font-family: 'Syne', sans-serif; font-size: clamp(2rem, 4vw, 3.2rem); font-weight: 800; letter-spacing: -0.03em; line-height: 1.05; max-width: 600px; }

  .pain-subtitle { font-size: 1rem; color: var(--text-muted); max-width: 500px; line-height: 1.7; margin-top: 1rem; }
  .pain-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1px; background: var(--border); border-radius: 4px; overflow: hidden; margin-top: 3rem; }
  .pain-card { background: var(--bg-card); padding: 2.5rem 2rem; position: relative; overflow: hidden; transition: background 0.3s; opacity: 0; transform: translateY(30px); }
  .pain-card.visible { opacity: 1; transform: translateY(0); transition: opacity 0.6s ease, transform 0.6s ease, background 0.3s; }
  .pain-card:hover { background: var(--bg-card-hover); }
  .pain-top-line { position: absolute; top: 0; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, rgba(255,59,59,0.7), transparent); transform: scaleX(0); transform-origin: left; transition: transform 0.4s ease; }
  .pain-card:hover .pain-top-line { transform: scaleX(1); }
  .pain-emoji { font-size: 2rem; margin-bottom: 1.2rem; display: block; }
  .pain-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; margin-bottom: 0.5rem; color: var(--text); }
  .pain-desc { font-size: 0.8rem; color: var(--text-muted); line-height: 1.65; }
  .pain-solution { display: flex; align-items: center; gap: 0.5rem; margin-top: 1.2rem; font-size: 0.75rem; color: var(--acid-fg); font-family: 'Space Mono', monospace; }
  .pain-solution::before { content: '✓ '; font-weight: 700; }

  .arrow-pill-wrap { text-align: center; padding: 2.5rem 4rem; background: var(--bg-alt); }
  .arrow-pill { display: inline-flex; align-items: center; gap: 1rem; background: rgba(200,255,0,0.05); border: 1px solid rgba(200,255,0,0.2); padding: 0.8rem 2rem; border-radius: 100px; font-family: 'Space Mono', monospace; font-size: 0.7rem; letter-spacing: 0.1em; color: var(--acid-fg); text-transform: uppercase; }

  /* FEATURES */
  #features { padding: 8rem 4rem; }
  .features-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 5rem; align-items: center; margin-top: 4rem; }
  .feature-card { display: flex; gap: 1.2rem; padding: 1.5rem; border: 1px solid var(--border); border-radius: 4px; margin-bottom: 0.8rem; background: var(--tint); transition: border-color 0.3s, background 0.3s, transform 0.3s; opacity: 0; transform: translateX(-20px); }
  .feature-card.visible { opacity: 1; transform: translateX(0); }
  .feature-card:hover { border-color: rgba(200,255,0,0.25); background: rgba(200,255,0,0.03); transform: translateX(6px); }
  .feat-icon { font-size: 1.4rem; flex-shrink: 0; width: 40px; height: 40px; display: flex; align-items: center; justify-content: center; background: rgba(200,255,0,0.07); border-radius: 4px; }
  .feat-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.9rem; margin-bottom: 0.3rem; }
  .feat-desc { font-size: 0.8rem; color: var(--text-muted); line-height: 1.6; }

  /* BROWSER */
  .preview-block { background: var(--bg-card); border: 1px solid var(--border); border-radius: 10px; overflow: hidden; box-shadow: 0 40px 100px rgba(0,0,0,0.3); opacity: 0; transform: translateY(30px); transition: opacity 0.8s ease, transform 0.8s ease; }
  .preview-block.visible { opacity: 1; transform: translateY(0); }
  .preview-bar { background: var(--preview-bar); padding: 0.65rem 1rem; display: flex; align-items: center; gap: 0.4rem; }
  .dot { width: 9px; height: 9px; border-radius: 50%; }
  .dot-r { background: #ff5f57; } .dot-y { background: #febc2e; } .dot-g { background: #28c840; }
  .preview-url { margin-left: 0.8rem; background: var(--bg-alt); border-radius: 4px; padding: 0.22rem 0.8rem; font-family: 'Space Mono', monospace; font-size: 0.6rem; color: var(--text-muted); flex: 1; max-width: 180px; }
  .preview-content { padding: 1.5rem; }
  .preview-hero-block { background: linear-gradient(135deg, var(--bg-alt) 0%, rgba(200,255,0,0.05) 100%); border-radius: 6px; padding: 1.8rem; margin-bottom: 1rem; position: relative; overflow: hidden; }
  .preview-hero-block::after { content: ''; position: absolute; top: -30px; right: -30px; width: 120px; height: 120px; background: var(--acid); border-radius: 50%; opacity: 0.08; animation: orbBreath 3s ease-in-out infinite; }
  @keyframes orbBreath { 0%,100%{transform:scale(1)} 50%{transform:scale(1.25)} }
  .preview-h1 { font-family: 'Syne', sans-serif; font-size: 1.1rem; font-weight: 800; margin-bottom: 0.3rem; }
  .preview-p { font-size: 0.6rem; color: var(--text-muted); line-height: 1.5; max-width: 180px; margin-bottom: 0.8rem; }
  .preview-btn-sm { background: var(--acid); color: #080808; font-family: 'Syne', sans-serif; font-size: 0.58rem; font-weight: 700; padding: 0.3rem 0.7rem; border-radius: 2px; display: inline-block; }
  .preview-cards { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0.5rem; }
  .preview-card-sm { background: var(--preview-card); border-radius: 4px; padding: 0.7rem; border: 1px solid var(--border); }
  .pbar { height: 4px; border-radius: 2px; margin-bottom: 0.35rem; background: var(--acid); }
  .pline { height: 2px; background: var(--pline); border-radius: 2px; margin-bottom: 0.25rem; }

  /* PROCESS */
  #process { background: var(--bg-alt); padding: 8rem 4rem; }
  .steps-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1px; background: var(--border); margin-top: 4rem; border-radius: 4px; overflow: hidden; }
  .step { background: var(--bg-card); padding: 2.5rem 1.8rem; position: relative; opacity: 0; transform: translateY(20px); }
  .step.visible { opacity: 1; transform: translateY(0); transition: opacity 0.5s ease, transform 0.5s ease, background 0.3s; }
  .step:hover { background: var(--bg-card-hover); }
  .step-top-line { position: absolute; top: 0; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, var(--acid), transparent); transform: scaleX(0); transform-origin: left; transition: transform 0.4s ease; }
  .step:hover .step-top-line { transform: scaleX(1); }
  .step-num { font-family: 'Space Mono', monospace; font-size: 0.62rem; color: var(--acid-fg); letter-spacing: 0.15em; margin-bottom: 1.5rem; opacity: 0.7; }
  .step-icon { font-size: 1.7rem; margin-bottom: 0.8rem; }
  .step-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; margin-bottom: 0.5rem; }
  .step-desc { font-size: 0.78rem; color: var(--text-muted); line-height: 1.6; }

  /* PRICING */
  #pricing { padding: 8rem 4rem; }
  .pricing-header { text-align: center; margin-bottom: 4rem; }
  .pricing-grid { display: grid; grid-template-columns: 1fr 1fr; max-width: 880px; margin: 0 auto; border: 1px solid var(--border-strong); border-radius: 6px; overflow: hidden; }
  .plan { background: var(--bg-card); padding: 3rem; transition: background 0.3s; }
  .plan:hover { background: var(--bg-card-hover); }
  .plan.featured { background: var(--plan-featured); border-left: 1px solid rgba(200,255,0,0.18); position: relative; }
  .plan.featured::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, var(--acid), rgba(200,255,0,0.2)); }
  .plan-tag { font-family: 'Space Mono', monospace; font-size: 0.62rem; letter-spacing: 0.15em; text-transform: uppercase; color: var(--acid-fg); background: rgba(200,255,0,0.1); padding: 0.25rem 0.65rem; border-radius: 2px; display: inline-block; margin-bottom: 1.5rem; }
  .plan-icon { font-size: 1.8rem; margin-bottom: 0.8rem; display: block; }
  .plan-name { font-family: 'Syne', sans-serif; font-size: 1.4rem; font-weight: 800; margin-bottom: 0.4rem; }
  .plan-desc { font-size: 0.82rem; color: var(--text-muted); line-height: 1.6; margin-bottom: 2rem; }
  .plan-price { font-family: 'Syne', sans-serif; font-size: 3.8rem; font-weight: 800; letter-spacing: -0.04em; color: var(--acid-fg); line-height: 1; margin-bottom: 0.3rem; }
  .plan-price sup { font-size: 1.5rem; font-weight: 400; vertical-align: super; }
  .plan-per { font-family: 'Space Mono', monospace; font-size: 0.65rem; color: var(--text-muted); letter-spacing: 0.08em; margin-bottom: 2.5rem; }
  .plan-features { list-style: none; margin-bottom: 2.5rem; display: flex; flex-direction: column; gap: 0.75rem; }
  .plan-features li { display: flex; align-items: flex-start; gap: 0.8rem; font-size: 0.83rem; color: var(--text-soft); line-height: 1.5; }
  .plan-features li::before { content: '→'; color: var(--acid-fg); font-family: 'Space Mono', monospace; font-size: 0.72rem; flex-shrink: 0; margin-top: 0.1rem; }
  .plan-btn { display: block; text-align: center; padding: 0.9rem; border-radius: 2px; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.88rem; text-decoration: none; cursor: none; transition: all 0.2s; border: none; width: 100%; }
  .plan-btn-outline { border: 1px solid var(--border-strong); color: var(--text); background: transparent; }
  .plan-btn-outline:hover { border-color: var(--acid-fg); color: var(--acid-fg); }
  .plan-btn-fill { background: var(--acid); color: #080808; }
  .plan-btn-fill:hover { box-shadow: 0 6px 30px rgba(200,255,0,0.4); transform: translateY(-2px); }

  /* CTA */
  .cta-section { text-align: center; padding: 8rem 4rem; position: relative; overflow: hidden; background: var(--bg-alt); }
  .cta-bg { position: absolute; inset: 0; background: radial-gradient(ellipse 700px 500px at 50% 50%, rgba(200,255,0,0.06) 0%, transparent 70%); animation: ctaPulse 5s ease-in-out infinite; }
  @keyframes ctaPulse { 0%,100%{opacity:0.5} 50%{opacity:1} }
  .cta-section h2 { font-family: 'Syne', sans-serif; font-size: clamp(2.5rem, 6vw, 5rem); font-weight: 800; letter-spacing: -0.04em; line-height: 1; margin-bottom: 1.5rem; position: relative; }
  .cta-section p { color: var(--text-muted); font-size: 1rem; max-width: 440px; margin: 0 auto 3rem; line-height: 1.7; position: relative; }
  .cta-buttons { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; position: relative; }

  /* SCROLL PROGRESS */
  .progress-bar { position: fixed; top: 0; left: 0; height: 2px; background: var(--acid); z-index: 1000; box-shadow: 0 0 8px rgba(200,255,0,0.5); pointer-events: none; }

  /* FOOTER */
  footer { border-top: 1px solid var(--border); padding: 2.5rem 4rem; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem; }
  footer p { font-family: 'Space Mono', monospace; font-size: 0.62rem; color: var(--text-muted); letter-spacing: 0.06em; }

  @keyframes fadeUp { from{opacity:0;transform:translateY(28px)} to{opacity:1;transform:translateY(0)} }

  .reveal { opacity: 0; transform: translateY(28px); transition: opacity 0.7s ease, transform 0.7s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* ============= ORDER OVERLAY ============= */
  .order-overlay { position: fixed; inset: 0; z-index: 2000; background: rgba(0,0,0,0.92); backdrop-filter: blur(20px); display: flex; align-items: flex-start; justify-content: center; overflow-y: auto; opacity: 0; pointer-events: none; transition: opacity 0.35s ease; padding: 5rem 1.5rem 3rem; }
  [data-theme="light"] .order-overlay { background: rgba(245,245,240,0.96); }
  .order-overlay.open { opacity: 1; pointer-events: auto; }
  .order-panel { background: var(--bg-card); border: 1px solid var(--border-strong); border-radius: 8px; max-width: 720px; width: 100%; padding: 3rem; position: relative; transform: translateY(20px); transition: transform 0.35s ease; box-shadow: 0 40px 120px rgba(0,0,0,0.5); }
  .order-overlay.open .order-panel { transform: translateY(0); }
  .order-close { position: absolute; top: 1.1rem; right: 1.1rem; width: 38px; height: 38px; background: transparent; border: 1px solid var(--border-strong); color: var(--text); font-size: 1.3rem; line-height: 1; border-radius: 50%; cursor: none; transition: border-color 0.2s, color 0.2s, transform 0.2s; }
  .order-close:hover { border-color: var(--acid-fg); color: var(--acid-fg); transform: rotate(90deg); }
  .order-header { margin-bottom: 2.2rem; }
  .order-header .section-tag { margin-bottom: 0.7rem; }
  .order-header h2 { font-family: 'Syne', sans-serif; font-size: clamp(1.7rem, 3.5vw, 2.4rem); font-weight: 800; letter-spacing: -0.03em; line-height: 1.05; margin-bottom: 0.7rem; }
  .order-header p { color: var(--text-muted); font-size: 0.92rem; line-height: 1.6; max-width: 480px; }

  .order-form { display: flex; flex-direction: column; gap: 0.9rem; }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 0.9rem; }
  .order-form input, .order-form select, .order-form textarea {
    width: 100%; background: var(--tint); border: 1px solid var(--border-strong); border-radius: 4px;
    padding: 0.85rem 1rem; color: var(--text); font-family: 'Inter', sans-serif; font-size: 0.92rem;
    transition: border-color 0.2s, background 0.2s; cursor: none; outline: none;
  }
  .order-form textarea { resize: vertical; min-height: 110px; font-family: 'Inter', sans-serif; }
  .order-form input::placeholder, .order-form textarea::placeholder { color: var(--text-muted); }
  .order-form input:focus, .order-form select:focus, .order-form textarea:focus { border-color: var(--acid-fg); background: rgba(200,255,0,0.04); }
  .order-form select { appearance: none; background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 12 8'%3E%3Cpath fill='%23c8ff00' d='M6 8L0 0h12z'/%3E%3C/svg%3E"); background-repeat: no-repeat; background-position: right 1rem center; background-size: 10px; padding-right: 2.5rem; }
  /* Native dropdown options — explicit colors so they're readable regardless of OS theme */
  .order-form select option { background: #ffffff; color: #0a0a0a; padding: 0.5rem; }
  .order-form select option:disabled { color: #888; }
  .form-submit { background: var(--acid); color: #080808; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.95rem; padding: 1rem 2rem; border: none; border-radius: 2px; cursor: none; margin-top: 0.5rem; transition: transform 0.2s, box-shadow 0.2s; letter-spacing: -0.01em; }
  .form-submit:hover { transform: translateY(-2px); box-shadow: 0 12px 40px rgba(200,255,0,0.4); }

  .order-divider { display: flex; align-items: center; gap: 1rem; margin: 2rem 0 1.5rem; color: var(--text-muted); font-family: 'Space Mono', monospace; font-size: 0.65rem; letter-spacing: 0.15em; text-transform: uppercase; }
  .order-divider::before, .order-divider::after { content: ''; flex: 1; height: 1px; background: var(--border-strong); }

  .order-contacts { display: flex; flex-direction: column; gap: 0.7rem; }
  .order-contacts a { display: flex; align-items: center; gap: 0.8rem; padding: 0.95rem 1.2rem; background: var(--tint); border: 1px solid var(--border-strong); border-radius: 4px; color: var(--text); text-decoration: none; font-family: 'Syne', sans-serif; font-weight: 600; font-size: 0.92rem; transition: border-color 0.2s, background 0.2s, transform 0.2s; cursor: none; }
  .order-contacts a:hover { border-color: var(--acid-fg); background: rgba(200,255,0,0.05); transform: translateX(4px); }
  .order-contacts a .ic { width: 28px; height: 28px; display: inline-flex; align-items: center; justify-content: center; flex-shrink: 0; }
  .order-contacts .ic.tg { color: #2ca5e0; }
  .order-contacts .ic.tel { color: var(--acid-fg); }

  /* MOBILE */
  @media (max-width: 768px) {
    nav { padding: 0.9rem 1rem; gap: 0.5rem; }
    nav ul { display: none; }
    .nav-tools { gap: 0.4rem; }
    .nav-cta { padding: 0.45rem 0.8rem; font-size: 0.7rem; }
    .lang-switcher { padding: 1px; }
    .lang-btn { padding: 0.25rem 0.45rem; font-size: 0.58rem; }
    .theme-toggle { width: 32px; height: 32px; font-size: 0.85rem; }
    .logo { font-size: 1rem; }
    .logo-mark { width: 26px; height: 26px; }

    .hero, .pain-section, #features, #process, #pricing, .cta-section { padding: 5rem 1.5rem; }
    .pain-grid, .pricing-grid { grid-template-columns: 1fr; }
    .features-layout { grid-template-columns: 1fr; gap: 3rem; }
    .steps-grid { grid-template-columns: 1fr 1fr; }
    .hero-stats { gap: 2rem; }
    footer { flex-direction: column; text-align: center; }
    .arrow-pill-wrap { padding: 2rem 1.5rem; }
    .order-panel { padding: 2rem 1.3rem; }
    .form-row { grid-template-columns: 1fr; }
    .order-overlay { padding: 4rem 1rem 2rem; }

    body { cursor: auto; }
    .cursor, .cursor-canvas { display: none; }
    .btn-primary, .btn-outline, .btn-tg, .nav-cta, .plan-btn,
    .lang-btn, .theme-toggle, .order-close, .form-submit,
    .order-form input, .order-form select, .order-form textarea,
    .order-contacts a { cursor: pointer; }
  }

  /* ============= LIGHT MODE — readable acid accents ============= */
  [data-theme="light"] .hero-badge {
    border-color: var(--acid-border);
    background: var(--acid-tint);
  }
  [data-theme="light"] .arrow-pill {
    border-color: var(--acid-border-soft);
    background: var(--acid-tint);
  }
  [data-theme="light"] .feature-card:hover {
    border-color: var(--acid-border-soft);
    background: var(--acid-tint);
  }
  [data-theme="light"] .btn-outline:hover {
    background: var(--acid-tint);
  }
  [data-theme="light"] .plan.featured {
    border-left-color: var(--acid-border-soft);
  }
  [data-theme="light"] .plan.featured::before {
    background: linear-gradient(90deg, var(--acid-fg), var(--acid-tint-strong));
  }
  [data-theme="light"] .plan-tag {
    background: var(--acid-tint-strong);
  }
  [data-theme="light"] .step-top-line {
    background: linear-gradient(90deg, var(--acid-fg), transparent);
  }
  [data-theme="light"] .feat-icon {
    background: var(--acid-tint-strong);
  }
  [data-theme="light"] .order-form input:focus,
  [data-theme="light"] .order-form select:focus,
  [data-theme="light"] .order-form textarea:focus {
    background: var(--acid-tint);
  }
  [data-theme="light"] .order-contacts a:hover {
    background: var(--acid-tint);
  }
  [data-theme="light"] .progress-bar {
    background: var(--acid-fg);
    box-shadow: 0 0 8px rgba(77,104,0,0.4);
  }
  [data-theme="light"] .tw-word { border-right-color: var(--acid-fg); }
  [data-theme="light"] .order-form select {
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 12 8'%3E%3Cpath fill='%234d6800' d='M6 8L0 0h12z'/%3E%3C/svg%3E");
  }
  /* Buttons that have acid background + dark text: keep bright in light too — already readable */
  /* But hover shadow should match the new accent for light */
  [data-theme="light"] .btn-primary:hover { box-shadow: 0 12px 40px rgba(77,104,0,0.35); }
  [data-theme="light"] .nav-cta:hover { box-shadow: 0 8px 24px rgba(77,104,0,0.35); }
  [data-theme="light"] .plan-btn-fill:hover { box-shadow: 0 6px 30px rgba(77,104,0,0.4); }
  [data-theme="light"] .form-submit:hover { box-shadow: 0 12px 40px rgba(77,104,0,0.4); }
</style>
</head>
<body>

<div class="progress-bar" id="progressBar"></div>
<div class="cursor" id="cursor"></div>
<canvas class="cursor-canvas" id="cursorCanvas"></canvas>

<!-- LOGO SVG (referenced by <use>) -->
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <symbol id="qw-logo" viewBox="0 0 64 64">
      <!-- Globe -->
      <circle cx="40" cy="32" r="18" fill="none" stroke="currentColor" stroke-width="2"/>
      <ellipse cx="40" cy="32" rx="18" ry="7" fill="none" stroke="currentColor" stroke-width="1.4"/>
      <ellipse cx="40" cy="32" rx="7" ry="18" fill="none" stroke="currentColor" stroke-width="1.4"/>
      <line x1="22" y1="32" x2="58" y2="32" stroke="currentColor" stroke-width="1.4"/>
      <!-- Globe nodes -->
      <circle cx="22" cy="32" r="2" fill="currentColor"/>
      <circle cx="58" cy="32" r="2" fill="currentColor"/>
      <circle cx="40" cy="14" r="2" fill="currentColor"/>
      <circle cx="40" cy="50" r="2" fill="currentColor"/>
      <circle cx="50" cy="20" r="1.6" fill="currentColor"/>
      <circle cx="30" cy="44" r="1.6" fill="currentColor"/>
      <!-- Lightning bolt (overlapping) -->
      <path d="M34 12 L20 34 L29 34 L24 52 L42 28 L33 28 L38 12 Z" fill="currentColor" stroke="var(--bg)" stroke-width="1"/>
      <!-- Speed lines -->
      <line x1="18" y1="20" x2="6" y2="20" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <line x1="14" y1="26" x2="2" y2="26" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <line x1="16" y1="32" x2="4" y2="32" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <line x1="12" y1="38" x2="2" y2="38" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
    </symbol>
  </defs>
</svg>

<!-- NAV -->
<nav>
  <a href="#" class="logo">
    <svg class="logo-mark"><use href="#qw-logo"/></svg>
    <span style="color:var(--text)">Quick</span><span>Web</span>
  </a>
  <ul>
    <li><a href="#pain" data-i18n="nav.problems">Muammolar</a></li>
    <li><a href="#features" data-i18n="nav.features">Imkoniyatlar</a></li>
    <li><a href="#pricing" data-i18n="nav.pricing">Narxlar</a></li>
    <li><a href="#contact" data-i18n="nav.contact">Bog'lanish</a></li>
  </ul>
  <div class="nav-tools">
    <button class="theme-toggle" id="themeToggle" aria-label="Toggle theme" title="Theme">☀</button>
    <div class="lang-switcher" role="tablist" aria-label="Language">
      <button class="lang-btn" data-lang="uz">UZ</button>
      <button class="lang-btn" data-lang="ru">RU</button>
      <button class="lang-btn" data-lang="en">EN</button>
    </div>
    <button class="nav-cta" id="orderBtn" data-open-order data-i18n="nav.order">Buyurtma qilish</button>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-grid"></div>
  <div class="particles" id="particles"></div>

  <div class="hero-badge" data-i18n="hero.badge">⚡ Sayt yaratishda yangi standart</div>

  <h1>
    <span data-i18n="hero.h1_line1">Biznesingiz</span><br>
    <span class="line-accent typewriter-wrap"><span class="tw-word" id="tw"></span></span><br>
    <span class="line-outline" data-i18n="hero.h1_line3">kuchli.</span>
  </h1>

  <p class="hero-sub" data-i18n="hero.sub">
    Tez, zamonaviy va mijozlarni qozonuvchi saytlar.
    Faqat natijaga yo'naltirilgan yondashuv — chiroyli emas, <em>ishlaydi</em>.
  </p>

  <div class="hero-actions">
    <a href="#" class="btn-primary" data-open-order data-i18n="hero.cta_consult">Bepul maslahat →</a>
    <a href="#pricing" class="btn-outline" data-i18n="hero.cta_pricing">Narxlarni ko'rish</a>
  </div>

  <div class="hero-stats">
    <div><div class="stat-num" data-count="48" data-suffix="h">48h</div><div class="stat-label" data-i18n="hero.stat1">O'rtacha topshirish</div></div>
    <div><div class="stat-num" data-count="100" data-suffix="%">100%</div><div class="stat-label" data-i18n="hero.stat2">Mobil optimallashtirish</div></div>
    <div><div class="stat-num" data-count="50" data-suffix="+">50+</div><div class="stat-label" data-i18n="hero.stat3">Topshirilgan saytlar</div></div>
    <div><div class="stat-num">SSL</div><div class="stat-label" data-i18n="hero.stat4">Xavfsizlik bepul</div></div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-wrap">
  <div class="marquee-track" id="marqueeTrack"></div>
</div>

<!-- PAIN SECTION -->
<section class="pain-section" id="pain">
  <div class="section-tag" data-i18n="pain.tag">// odamlar duch keladigan muammolar</div>
  <div class="section-title reveal" data-i18n="pain.title">Saytingiz yo'qmi?<br>Bu sizga qancha turadi.</div>
  <p class="pain-subtitle reveal" data-i18n="pain.subtitle">Har kuni saytisiz bizneslar minglab mijozlarni yo'qotmoqda. Siz qaysi muammoni his qilyapsiz?</p>

  <div class="pain-grid">
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">😤</span>
      <div class="pain-title" data-i18n="pain.c1.title">"Sayt yo'q — mijozlar topilmaydi"</div>
      <div class="pain-desc" data-i18n="pain.c1.desc">Google'da qidirishadi — siz topilmaysiz. Raqibingiz topiladi. Mijoz unikiga boradi. Har kuni shunday.</div>
      <div class="pain-solution" data-i18n="pain.c1.sol">Sayt = 24/7 ishlaydigan sotuvchi</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">🐌</span>
      <div class="pain-title" data-i18n="pain.c2.title">"Sayt bor, lekin juda sekin"</div>
      <div class="pain-desc" data-i18n="pain.c2.desc">3 soniyadan ko'p kutgan foydalanuvchilarning 53% sahifani tark etadi. Sekin sayt = yo'qolgan sotuvlar.</div>
      <div class="pain-solution" data-i18n="pain.c2.sol">1 soniyadan tez yuklanishni kafolatlaymiz</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">📵</span>
      <div class="pain-title" data-i18n="pain.c3.title">"Telefonda ko'rinmaydi"</div>
      <div class="pain-desc" data-i18n="pain.c3.desc">Bugungi kunda 78% tashrif mobil qurilmadan. Agar sayt mobil optimallashtirilmagan bo'lsa — chiqib ketishadi.</div>
      <div class="pain-solution" data-i18n="pain.c3.sol">Har qanday qurilmada mukammal</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">💸</span>
      <div class="pain-title" data-i18n="pain.c4.title">"Dasturchi juda qimmat so'radi"</div>
      <div class="pain-desc" data-i18n="pain.c4.desc">Ko'pchilik oddiy sayt uchun $500–$2000 so'raydi va oylar ketadi. Biznes esa kutib turolmaydi.</div>
      <div class="pain-solution" data-i18n="pain.c4.sol">$99 dan — 48 soatda tayyor</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">😰</span>
      <div class="pain-title" data-i18n="pain.c6.title">"O'zim o'zgarta olmayman"</div>
      <div class="pain-desc" data-i18n="pain.c6.desc">Narx o'zgartirmoqchi — dasturchi kerak. Rasm qo'shmoqchi — dasturchi kerak. Bu biznesni to'xtatadi.</div>
      <div class="pain-solution" data-i18n="pain.c6.sol">Admin panel — o'zingiz boshqarasiz</div>
    </div>
    <div class="pain-card">
      <div class="pain-top-line"></div>
      <span class="pain-emoji">🛠️</span>
      <div class="pain-title" data-i18n="pain.c5.title">"Ertaga bitadi" sindromi</div>
      <div class="pain-desc" data-i18n="pain.c5.desc">Dasturchi bilan kelishasiz, lekin ish haftalab, oylab cho'ziladi. Vaqt o'tgani sari g'oyangiz "sovub" boradi. Biznesda vaqt — bu boy berilgan foyda.</div>
      <div class="pain-solution" data-i18n="pain.c5.sol">Aniq muddat: 48 soat ichida ishga tushiramiz</div>
    </div>
  </div>
</section>

<div class="arrow-pill-wrap">
  <div class="arrow-pill" data-i18n="arrow_pill">⚡ QuickWeb bu muammolarni hal qildi →</div>
</div>

<!-- FEATURES -->
<section id="features">
  <div class="section-tag" data-i18n="features.tag">// nima beramiz</div>
  <div class="section-title reveal" data-i18n="features.title">Har bir piksel — maqsadli.</div>
  <div class="features-layout">
    <div>
      <div class="feature-card reveal">
        <div class="feat-icon">⚡</div>
        <div><div class="feat-title" data-i18n="feat.f1.title">Ultra tezkor ishlash</div><div class="feat-desc" data-i18n="feat.f1.desc">Barcha qurilmalarda 1 soniyadan tez yuklanish. Foydalanuvchi kutmaydi — sotib oladi.</div></div>
      </div>
      <div class="feature-card reveal">
        <div class="feat-icon">📱</div>
        <div><div class="feat-title" data-i18n="feat.f2.title">Mobil birinchi yondashuv</div><div class="feat-desc" data-i18n="feat.f2.desc">Har qanday smartfon, planshet va kompyuterda mukammal ko'rinish.</div></div>
      </div>
      <div class="feature-card reveal">
        <div class="feat-icon">🔒</div>
        <div><div class="feat-title" data-i18n="feat.f3.title">SSL + Xavfsizlik</div><div class="feat-desc" data-i18n="feat.f3.desc">Bepul SSL sertifikati, ma'lumotlar shifrlangan — mijozlaringiz ishonadi.</div></div>
      </div>
      <div class="feature-card reveal">
        <div class="feat-icon">📬</div>
        <div><div class="feat-title" data-i18n="feat.f4.title">Telegram integratsiya</div><div class="feat-desc" data-i18n="feat.f4.desc">Saytdan kelgan har bir so'rov darhol Telegramingizga tushadi. Hech narsa o'tkazib yuborilmaydi.</div></div>
      </div>
    </div>
    <div>
      <div class="preview-block reveal">
        <div class="preview-bar">
          <div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div>
          <div class="preview-url">quickweb.uz</div>
        </div>
        <div class="preview-content">
          <div class="preview-hero-block">
            <div class="preview-h1" data-i18n="preview.h1">Sizning Biznesingiz ⚡</div>
            <p class="preview-p" data-i18n="preview.p">Professional va tez sayt — mijozlar sizni taniydi</p>
            <div class="preview-btn-sm" data-i18n="preview.btn">Buyurtma berish →</div>
          </div>
          <div class="preview-cards">
            <div class="preview-card-sm"><div class="pbar"></div><div class="pline"></div><div class="pline" style="width:60%"></div></div>
            <div class="preview-card-sm"><div class="pbar" style="opacity:.3;width:70%"></div><div class="pline"></div><div class="pline" style="width:80%"></div></div>
            <div class="preview-card-sm"><div class="pbar" style="opacity:.15;width:50%"></div><div class="pline"></div><div class="pline" style="width:45%"></div></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PROCESS -->
<section id="process">
  <div class="section-tag" data-i18n="process.tag">// qanday ishlaydi</div>
  <div class="section-title reveal" data-i18n="process.title">4 qadamda — saytingiz tayyor.</div>
  <div class="steps-grid">
    <div class="step reveal"><div class="step-top-line"></div><div class="step-num">01 —</div><div class="step-icon">💬</div><div class="step-title" data-i18n="proc.s1.title">Muloqot</div><div class="step-desc" data-i18n="proc.s1.desc">Biznes haqida gaplashamiz, maqsadlarni aniqlaymiz.</div></div>
    <div class="step reveal"><div class="step-top-line"></div><div class="step-num">02 —</div><div class="step-icon">🎨</div><div class="step-title" data-i18n="proc.s2.title">Dizayn</div><div class="step-desc" data-i18n="proc.s2.desc">Brendingizga mos eksklyuziv dizayn tayyorlanadi.</div></div>
    <div class="step reveal"><div class="step-top-line"></div><div class="step-num">03 —</div><div class="step-icon">⚙️</div><div class="step-title" data-i18n="proc.s3.title">Ishlab chiqish</div><div class="step-desc" data-i18n="proc.s3.desc">48 soat ichida to'liq ishlayotgan sayt serverga joylashtiriladi.</div></div>
    <div class="step reveal"><div class="step-top-line"></div><div class="step-num">04 —</div><div class="step-icon">🚀</div><div class="step-title" data-i18n="proc.s4.title">Topshirish</div><div class="step-desc" data-i18n="proc.s4.desc">Domenga ulanadi, testdan o'tkaziladi. Biznes ishlaydi.</div></div>
  </div>
</section>

<!-- PRICING -->
<section id="pricing">
  <div class="pricing-header">
    <div class="section-tag" data-i18n="pricing.tag">// tariflar</div>
    <div class="section-title reveal" style="margin:0 auto" data-i18n="pricing.title">O'zingizga mos tanlang.</div>
  </div>
  <div class="pricing-grid">
    <div class="plan reveal">
      <div class="plan-tag" data-i18n="plan1.tag">⚡ START</div>
      <div class="plan-icon">🚀</div>
      <div class="plan-name">START</div>
      <div class="plan-desc" data-i18n="plan1.desc">Biznesini internetda tez va sifatli ko'rsatishni xohlovchi tadbirkorlar uchun.</div>
      <div class="plan-price"><sup>$</sup>99</div>
      <div class="plan-per" data-i18n="plan1.per">bir martalik to'lov</div>
      <ul class="plan-features">
        <li data-i18n="plan1.f1">Ko'p sahifali sayt (Bosh, Menyu, Haqimizda, Aloqa)</li>
        <li data-i18n="plan1.f2">Onlayn savatcha va buyurtma tizimi</li>
        <li data-i18n="plan1.f3">Serverga joylashtirish + domenga ulash</li>
        <li data-i18n="plan1.f4">Barcha smartfonlarda mobil optimizatsiya</li>
        <li data-i18n="plan1.f5">SSL sertifikati — bepul</li>
      </ul>
      <button class="plan-btn plan-btn-outline" data-open-order data-plan="START $99" data-i18n="plan1.btn">Buyurtma berish</button>
    </div>
    <div class="plan featured reveal">
      <div class="plan-tag" data-i18n="plan2.tag">🏢 BIZNES — Eng mashhur</div>
      <div class="plan-icon">💎</div>
      <div class="plan-name">BIZNES</div>
      <div class="plan-desc" data-i18n="plan2.desc">To'liq avtomatlashtirilgan, yuqori nufuzga ega professional platforma.</div>
      <div class="plan-price"><sup>$</sup>199</div>
      <div class="plan-per" data-i18n="plan2.per">bir martalik to'lov</div>
      <ul class="plan-features">
        <li data-i18n="plan2.f1">Eksklyuziv dizayn — logotip va brendingizga mos</li>
        <li data-i18n="plan2.f2">Kengaytirilgan katalog — filtrlash, tavsiflar</li>
        <li data-i18n="plan2.f3">SEO tayyorgarlik — Google va Yandexda yuqori o'rin</li>
        <li data-i18n="plan2.f4">Ko'p tilli qo'llab-quvvatlash</li>
      </ul>
      <button class="plan-btn plan-btn-fill" data-open-order data-plan="BIZNES $199" data-i18n="plan2.btn">Hoziroq boshlash →</button>
    </div>
  </div>
</section>

<!-- CTA -->
<section class="cta-section" id="contact">
  <div class="cta-bg"></div>
  <div class="section-tag" style="display:inline-block;position:relative" data-i18n="cta.tag">// bog'laning</div>
  <h2 style="margin-top:1rem"><span data-i18n="cta.h2_a">Saytingiz</span><br><span style="color:var(--acid)" data-i18n="cta.h2_b">bugun</span> <span data-i18n="cta.h2_c">tayyor.</span></h2>
  <p data-i18n="cta.sub">Savollaringiz bormi? Yoki darhol boshlashni xohlaysizmi? Biz doim shu yerda.</p>
  <div class="cta-buttons">
    <a href="https://t.me/QuickWweb" target="_blank" rel="noopener" class="btn-tg">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm5.562 8.069l-2.07 9.754c-.155.697-.567.867-1.148.538l-3.185-2.347-1.537 1.479c-.17.17-.312.312-.64.312l.228-3.237 5.894-5.322c.256-.228-.056-.355-.397-.127L6.43 14.47l-3.138-.979c-.68-.213-.694-.68.143-.997l12.26-4.73c.566-.21 1.063.127.867.305z"/></svg>
      Telegram: @QuickWweb
    </a>
    <a href="tel:+998903497778" class="btn-primary">📞 +998 90 349 77 78</a>
  </div>
</section>

<!-- ============= ORDER OVERLAY ============= -->
<div class="order-overlay" id="orderOverlay" role="dialog" aria-modal="true" aria-labelledby="orderTitle">
  <div class="order-panel">
    <button class="order-close" id="orderClose" aria-label="Close">×</button>

    <div class="order-header">
      <div class="section-tag" data-i18n="order.tag">// buyurtma berish</div>
      <h2 id="orderTitle" data-i18n="order.title">Saytingizni yaratamiz.</h2>
      <p data-i18n="order.subtitle">Ma'lumotlarni qoldiring — 1 soat ichida bog'lanamiz.</p>
    </div>

    <form class="order-form" id="orderForm" action="https://formsubmit.co/Kudratiys@gmail.com" method="POST">
      <input type="hidden" name="_subject" value="QuickWeb — Yangi buyurtma">
      <input type="hidden" name="_captcha" value="false">
      <input type="hidden" name="_template" value="table">
      <input type="hidden" name="_next" id="formNext" value="">

      <div class="form-row">
        <input type="text" name="Ism" required data-i18n-ph="order.ph.name" placeholder="Ismingiz">
        <input type="tel" name="Telefon" required data-i18n-ph="order.ph.phone" placeholder="+998 XX XXX XX XX">
      </div>
      <input type="email" name="Email" data-i18n-ph="order.ph.email" placeholder="email@example.com (ixtiyoriy)">
      <select name="Tarif" id="orderPlan" required>
        <option value="" data-i18n="order.plan.default">Tarifni tanlang</option>
        <option value="START $99" data-i18n="order.plan.start">START — $99</option>
        <option value="BIZNES $199" data-i18n="order.plan.biznes">BIZNES — $199</option>
        <option value="Maslahat" data-i18n="order.plan.consult">Maslahat kerak</option>
      </select>
      <textarea name="Xabar" rows="4" data-i18n-ph="order.ph.message" placeholder="Loyihangiz haqida qisqacha..."></textarea>
      <button type="submit" class="form-submit" data-i18n="order.submit">Buyurtma yuborish →</button>
    </form>

    <div class="order-divider" data-i18n="order.divider">yoki to'g'ridan-to'g'ri</div>

    <div class="order-contacts">
      <a href="https://t.me/QuickWweb" target="_blank" rel="noopener">
        <span class="ic tg">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm5.562 8.069l-2.07 9.754c-.155.697-.567.867-1.148.538l-3.185-2.347-1.537 1.479c-.17.17-.312.312-.64.312l.228-3.237 5.894-5.322c.256-.228-.056-.355-.397-.127L6.43 14.47l-3.138-.979c-.68-.213-.694-.68.143-.997l12.26-4.73c.566-.21 1.063.127.867.305z"/></svg>
        </span>
        Telegram: @QuickWweb
      </a>
      <a href="tel:+998903497778">
        <span class="ic tel">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72c.13.96.36 1.9.7 2.81a2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.91.34 1.85.57 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
        </span>
        +998 90 349 77 78
      </a>
    </div>
  </div>
</div>

<!-- FOOTER -->
<footer>
  <a href="#" class="logo" style="font-size:0.95rem">
    <svg class="logo-mark" style="width:24px;height:24px"><use href="#qw-logo"/></svg>
    <span style="color:var(--text)">Quick</span><span>Web</span>
  </a>
  <p data-i18n="footer.copy">© 2025 QuickWeb — Professional sayt yaratish xizmati</p>
  <p style="color:rgba(200,255,0,0.5)" data-i18n="footer.loc">Toshkent, O'zbekiston</p>
</footer>

<script>
/* ============================================================
   I18N
============================================================ */
const I18N = {
  uz: {
    'nav.problems':'Muammolar','nav.features':'Imkoniyatlar','nav.pricing':'Narxlar','nav.contact':"Bog'lanish",'nav.order':'Buyurtma qilish',
    'hero.badge':'⚡ Sayt yaratishda yangi standart',
    'hero.h1_line1':'Biznesingiz','hero.h1_line3':'kuchli.',
    'hero.sub':"Tez, zamonaviy va mijozlarni qozonuvchi saytlar. Faqat natijaga yo'naltirilgan yondashuv — chiroyli emas, <em>ishlaydi</em>.",
    'hero.cta_consult':'Bepul maslahat →','hero.cta_pricing':"Narxlarni ko'rish",
    'hero.stat1':"O'rtacha topshirish",'hero.stat2':'Mobil optimallashtirish','hero.stat3':'Topshirilgan saytlar','hero.stat4':'Xavfsizlik bepul',
    'pain.tag':'// odamlar duch keladigan muammolar',
    'pain.title':"Saytingiz yo'qmi?<br>Bu sizga qancha turadi.",
    'pain.subtitle':"Har kuni saytisiz bizneslar minglab mijozlarni yo'qotmoqda. Siz qaysi muammoni his qilyapsiz?",
    'pain.c1.title':'"Sayt yo\'q — mijozlar topilmaydi"',
    'pain.c1.desc':"Google'da qidirishadi — siz topilmaysiz. Raqibingiz topiladi. Mijoz unikiga boradi. Har kuni shunday.",
    'pain.c1.sol':'Sayt = 24/7 ishlaydigan sotuvchi',
    'pain.c2.title':'"Sayt bor, lekin juda sekin"',
    'pain.c2.desc':"3 soniyadan ko'p kutgan foydalanuvchilarning 53% sahifani tark etadi. Sekin sayt = yo'qolgan sotuvlar.",
    'pain.c2.sol':'1 soniyadan tez yuklanishni kafolatlaymiz',
    'pain.c3.title':'"Telefonda ko\'rinmaydi"',
    'pain.c3.desc':"Bugungi kunda 78% tashrif mobil qurilmadan. Agar sayt mobil optimallashtirilmagan bo'lsa — chiqib ketishadi.",
    'pain.c3.sol':'Har qanday qurilmada mukammal',
    'pain.c4.title':'"Dasturchi juda qimmat so\'radi"',
    'pain.c4.desc':"Ko'pchilik oddiy sayt uchun $500–$2000 so'raydi va oylar ketadi. Biznes esa kutib turolmaydi.",
    'pain.c4.sol':'$99 dan — 48 soatda tayyor',
    'pain.c5.title':'"Ertaga bitadi" sindromi',
    'pain.c5.desc':'Dasturchi bilan kelishasiz, lekin ish haftalab, oylab cho\'ziladi. Vaqt o\'tgani sari g\'oyangiz "sovub" boradi. Biznesda vaqt — bu boy berilgan foyda.',
    'pain.c5.sol':'Aniq muddat: 48 soat ichida ishga tushiramiz',
    'pain.c6.title':'"O\'zim o\'zgarta olmayman"',
    'pain.c6.desc':'Narx o\'zgartirmoqchi — dasturchi kerak. Rasm qo\'shmoqchi — dasturchi kerak. Bu biznesni to\'xtatadi.',
    'pain.c6.sol':"Admin panel — o'zingiz boshqarasiz",
    'arrow_pill':'⚡ QuickWeb bu muammolarni hal qildi →',
    'features.tag':'// nima beramiz','features.title':'Har bir piksel — maqsadli.',
    'feat.f1.title':'Ultra tezkor ishlash','feat.f1.desc':'Barcha qurilmalarda 1 soniyadan tez yuklanish. Foydalanuvchi kutmaydi — sotib oladi.',
    'feat.f2.title':'Mobil birinchi yondashuv','feat.f2.desc':'Har qanday smartfon, planshet va kompyuterda mukammal ko\'rinish.',
    'feat.f3.title':'SSL + Xavfsizlik','feat.f3.desc':'Bepul SSL sertifikati, ma\'lumotlar shifrlangan — mijozlaringiz ishonadi.',
    'feat.f4.title':'Telegram integratsiya','feat.f4.desc':"Saytdan kelgan har bir so'rov darhol Telegramingizga tushadi. Hech narsa o'tkazib yuborilmaydi.",
    'preview.h1':'Sizning Biznesingiz ⚡','preview.p':'Professional va tez sayt — mijozlar sizni taniydi','preview.btn':'Buyurtma berish →',
    'process.tag':'// qanday ishlaydi','process.title':'4 qadamda — saytingiz tayyor.',
    'proc.s1.title':'Muloqot','proc.s1.desc':'Biznes haqida gaplashamiz, maqsadlarni aniqlaymiz.',
    'proc.s2.title':'Dizayn','proc.s2.desc':'Brendingizga mos eksklyuziv dizayn tayyorlanadi.',
    'proc.s3.title':'Ishlab chiqish','proc.s3.desc':"48 soat ichida to'liq ishlayotgan sayt serverga joylashtiriladi.",
    'proc.s4.title':'Topshirish','proc.s4.desc':"Domenga ulanadi, testdan o'tkaziladi. Biznes ishlaydi.",
    'pricing.tag':'// tariflar','pricing.title':"O'zingizga mos tanlang.",
    'plan1.tag':'⚡ START',
    'plan1.desc':"Biznesini internetda tez va sifatli ko'rsatishni xohlovchi tadbirkorlar uchun.",
    'plan1.per':'bir martalik to\'lov',
    'plan1.f1':"Ko'p sahifali sayt (Bosh, Menyu, Haqimizda, Aloqa)",
    'plan1.f2':'Onlayn savatcha va buyurtma tizimi',
    'plan1.f3':'Serverga joylashtirish + domenga ulash',
    'plan1.f4':'Barcha smartfonlarda mobil optimizatsiya',
    'plan1.f5':'SSL sertifikati — bepul',
    'plan1.btn':'Buyurtma berish',
    'plan2.tag':'🏢 BIZNES — Eng mashhur',
    'plan2.desc':"To'liq avtomatlashtirilgan, yuqori nufuzga ega professional platforma.",
    'plan2.per':'bir martalik to\'lov',
    'plan2.f1':'Eksklyuziv dizayn — logotip va brendingizga mos',
    'plan2.f2':'Kengaytirilgan katalog — filtrlash, tavsiflar',
    'plan2.f3':'SEO tayyorgarlik — Google va Yandexda yuqori o\'rin',
    'plan2.f4':"Ko'p tilli qo'llab-quvvatlash",
    'plan2.btn':'Hoziroq boshlash →',
    'cta.tag':'// bog\'laning','cta.h2_a':'Saytingiz','cta.h2_b':'bugun','cta.h2_c':'tayyor.',
    'cta.sub':'Savollaringiz bormi? Yoki darhol boshlashni xohlaysizmi? Biz doim shu yerda.',
    'order.tag':'// buyurtma berish','order.title':'Saytingizni yaratamiz.','order.subtitle':"Ma'lumotlarni qoldiring — 1 soat ichida bog'lanamiz.",
    'order.ph.name':'Ismingiz','order.ph.phone':'+998 XX XXX XX XX','order.ph.email':'email@example.com (ixtiyoriy)','order.ph.message':'Loyihangiz haqida qisqacha...',
    'order.plan.default':'Tarifni tanlang','order.plan.start':'START — $99','order.plan.biznes':'BIZNES — $199','order.plan.consult':'Maslahat kerak',
    'order.submit':'Buyurtma yuborish →','order.divider':"yoki to'g'ridan-to'g'ri",
    'footer.copy':'© 2025 QuickWeb — Professional sayt yaratish xizmati','footer.loc':"Toshkent, O'zbekiston"
  },
  ru: {
    'nav.problems':'Проблемы','nav.features':'Возможности','nav.pricing':'Цены','nav.contact':'Контакты','nav.order':'Заказать',
    'hero.badge':'⚡ Новый стандарт создания сайтов',
    'hero.h1_line1':'Ваш бизнес','hero.h1_line3':'мощный.',
    'hero.sub':'Быстрые, современные сайты, которые приводят клиентов. Подход, ориентированный на результат — не просто красиво, а <em>работает</em>.',
    'hero.cta_consult':'Бесплатная консультация →','hero.cta_pricing':'Посмотреть цены',
    'hero.stat1':'Среднее время сдачи','hero.stat2':'Мобильная оптимизация','hero.stat3':'Сданных сайтов','hero.stat4':'Безопасность бесплатно',
    'pain.tag':'// проблемы, с которыми сталкиваются',
    'pain.title':'Нет сайта?<br>Это вам дорого обходится.',
    'pain.subtitle':'Каждый день бизнес без сайта теряет тысячи клиентов. Какую проблему ощущаете вы?',
    'pain.c1.title':'«Нет сайта — клиенты не находят»',
    'pain.c1.desc':'Они ищут в Google — вас не находят. Находят конкурента. Клиент уходит к нему. Так каждый день.',
    'pain.c1.sol':'Сайт = продавец, работающий 24/7',
    'pain.c2.title':'«Сайт есть, но очень медленный»',
    'pain.c2.desc':'53% пользователей покидают страницу, ждущую более 3 секунд. Медленный сайт = потерянные продажи.',
    'pain.c2.sol':'Гарантируем загрузку быстрее 1 секунды',
    'pain.c3.title':'«На телефоне не отображается»',
    'pain.c3.desc':'Сегодня 78% посещений с мобильных. Если сайт не оптимизирован — уходят сразу.',
    'pain.c3.sol':'Идеально на любом устройстве',
    'pain.c4.title':'«Разработчик запросил очень дорого»',
    'pain.c4.desc':'Многие просят $500–$2000 за обычный сайт и тратят месяцы. Бизнес не может ждать.',
    'pain.c4.sol':'От $99 — готов за 48 часов',
    'pain.c5.title':'Синдром «Завтра будет готово»',
    'pain.c5.desc':'Договариваетесь с разработчиком, но работа растягивается на недели и месяцы. Ваша идея «остывает». В бизнесе время — это упущенная прибыль.',
    'pain.c5.sol':'Чёткий срок: запуск за 48 часов',
    'pain.c6.title':'«Сам ничего изменить не могу»',
    'pain.c6.desc':'Хочешь изменить цену — нужен разработчик. Добавить фото — нужен разработчик. Это тормозит бизнес.',
    'pain.c6.sol':'Админ-панель — управляете сами',
    'arrow_pill':'⚡ QuickWeb решил эти проблемы →',
    'features.tag':'// что мы даём','features.title':'Каждый пиксель — с целью.',
    'feat.f1.title':'Ультра-быстрая работа','feat.f1.desc':'Загрузка быстрее 1 секунды на любых устройствах. Пользователь не ждёт — покупает.',
    'feat.f2.title':'Mobile-first подход','feat.f2.desc':'Идеальный вид на любом смартфоне, планшете и компьютере.',
    'feat.f3.title':'SSL + Безопасность','feat.f3.desc':'Бесплатный SSL-сертификат, шифрование данных — клиенты доверяют.',
    'feat.f4.title':'Интеграция с Telegram','feat.f4.desc':'Каждая заявка с сайта мгновенно приходит в Telegram. Ничего не пропустите.',
    'preview.h1':'Ваш бизнес ⚡','preview.p':'Профессиональный быстрый сайт — клиенты вас узнают','preview.btn':'Заказать →',
    'process.tag':'// как это работает','process.title':'4 шага — и сайт готов.',
    'proc.s1.title':'Общение','proc.s1.desc':'Обсуждаем бизнес, определяем цели.',
    'proc.s2.title':'Дизайн','proc.s2.desc':'Готовим эксклюзивный дизайн под ваш бренд.',
    'proc.s3.title':'Разработка','proc.s3.desc':'За 48 часов полностью рабочий сайт размещаем на сервере.',
    'proc.s4.title':'Сдача','proc.s4.desc':'Подключаем к домену, тестируем. Бизнес работает.',
    'pricing.tag':'// тарифы','pricing.title':'Выберите подходящий.',
    'plan1.tag':'⚡ START','plan1.desc':'Для предпринимателей, желающих быстро и качественно показать бизнес в интернете.',
    'plan1.per':'разовая оплата',
    'plan1.f1':'Многостраничный сайт (Главная, Меню, О нас, Контакты)',
    'plan1.f2':'Онлайн-корзина и система заказов',
    'plan1.f3':'Размещение на сервере + подключение к домену',
    'plan1.f4':'Мобильная оптимизация для всех смартфонов',
    'plan1.f5':'SSL-сертификат — бесплатно',
    'plan1.btn':'Заказать',
    'plan2.tag':'🏢 BIZNES — Самый популярный',
    'plan2.desc':'Полностью автоматизированная, престижная профессиональная платформа.',
    'plan2.per':'разовая оплата',
    'plan2.f1':'Эксклюзивный дизайн — под логотип и бренд',
    'plan2.f2':'Расширенный каталог — фильтры, описания',
    'plan2.f3':'SEO-подготовка — высокие позиции в Google и Яндекс',
    'plan2.f4':'Многоязычная поддержка',
    'plan2.btn':'Начать сейчас →',
    'cta.tag':'// связаться','cta.h2_a':'Ваш сайт','cta.h2_b':'сегодня','cta.h2_c':'готов.',
    'cta.sub':'Есть вопросы? Или хотите начать прямо сейчас? Мы всегда здесь.',
    'order.tag':'// оформить заказ','order.title':'Создадим ваш сайт.','order.subtitle':'Оставьте данные — свяжемся в течение часа.',
    'order.ph.name':'Ваше имя','order.ph.phone':'+998 XX XXX XX XX','order.ph.email':'email@example.com (необязательно)','order.ph.message':'Кратко о вашем проекте...',
    'order.plan.default':'Выберите тариф','order.plan.start':'START — $99','order.plan.biznes':'BIZNES — $199','order.plan.consult':'Нужна консультация',
    'order.submit':'Отправить заявку →','order.divider':'или напрямую',
    'footer.copy':'© 2025 QuickWeb — Услуги профессиональной разработки сайтов','footer.loc':'Ташкент, Узбекистан'
  },
  en: {
    'nav.problems':'Problems','nav.features':'Features','nav.pricing':'Pricing','nav.contact':'Contact','nav.order':'Order Now',
    'hero.badge':'⚡ The new standard in web creation',
    'hero.h1_line1':'Your business','hero.h1_line3':'powerful.',
    'hero.sub':'Fast, modern websites that win customers. A results-driven approach — not just pretty, but <em>it works</em>.',
    'hero.cta_consult':'Free consultation →','hero.cta_pricing':'View pricing',
    'hero.stat1':'Average delivery','hero.stat2':'Mobile optimization','hero.stat3':'Sites delivered','hero.stat4':'Security included',
    'pain.tag':'// problems people face',
    'pain.title':"Don't have a website?<br>Here's what it costs you.",
    'pain.subtitle':'Every day, businesses without a website lose thousands of customers. Which problem do you feel?',
    'pain.c1.title':'"No site — customers can\'t find me"',
    'pain.c1.desc':'They search on Google — you\'re not there. Your competitor is. The customer goes to them. Every day.',
    'pain.c1.sol':'A website = a 24/7 salesperson',
    'pain.c2.title':'"Site exists, but it\'s too slow"',
    'pain.c2.desc':'53% of users abandon a page that takes more than 3 seconds. Slow site = lost sales.',
    'pain.c2.sol':'We guarantee sub-1-second loading',
    'pain.c3.title':'"It looks broken on mobile"',
    'pain.c3.desc':'Today 78% of visits come from mobile. If your site isn\'t optimized — they leave.',
    'pain.c3.sol':'Perfect on every device',
    'pain.c4.title':'"The developer asked way too much"',
    'pain.c4.desc':'Most ask $500–$2000 for a basic site and take months. Business can\'t wait.',
    'pain.c4.sol':'From $99 — ready in 48 hours',
    'pain.c5.title':'"It\'ll be done tomorrow" syndrome',
    'pain.c5.desc':'You agree with a developer, but the work drags on for weeks or months. Your idea cools off. In business, time means lost profit.',
    'pain.c5.sol':'A real deadline: live in 48 hours',
    'pain.c6.title':'"I can\'t change anything myself"',
    'pain.c6.desc':'Want to change a price — need a developer. Add a photo — need a developer. It paralyzes business.',
    'pain.c6.sol':'Admin panel — you\'re in control',
    'arrow_pill':'⚡ QuickWeb solved these problems →',
    'features.tag':'// what we deliver','features.title':'Every pixel — with purpose.',
    'feat.f1.title':'Ultra-fast performance','feat.f1.desc':'Sub-1-second loading on every device. Users don\'t wait — they buy.',
    'feat.f2.title':'Mobile-first approach','feat.f2.desc':'Looks perfect on any smartphone, tablet, or desktop.',
    'feat.f3.title':'SSL + Security','feat.f3.desc':'Free SSL certificate, encrypted data — your customers trust you.',
    'feat.f4.title':'Telegram integration','feat.f4.desc':'Every request from the site goes straight to your Telegram. Nothing missed.',
    'preview.h1':'Your Business ⚡','preview.p':'Professional fast site — customers will know you','preview.btn':'Order now →',
    'process.tag':'// how it works','process.title':'4 steps — your site is ready.',
    'proc.s1.title':'Discussion','proc.s1.desc':'We talk about your business and pin down the goals.',
    'proc.s2.title':'Design','proc.s2.desc':'An exclusive design tailored to your brand is prepared.',
    'proc.s3.title':'Development','proc.s3.desc':'Within 48 hours a fully working site is deployed to the server.',
    'proc.s4.title':'Delivery','proc.s4.desc':'Connected to the domain, tested, live. Business runs.',
    'pricing.tag':'// pricing','pricing.title':'Pick what fits you.',
    'plan1.tag':'⚡ START','plan1.desc':'For entrepreneurs who want to quickly and professionally appear online.',
    'plan1.per':'one-time payment',
    'plan1.f1':'Multi-page site (Home, Menu, About, Contact)',
    'plan1.f2':'Online cart and order system',
    'plan1.f3':'Server hosting + domain connection',
    'plan1.f4':'Mobile optimization for all smartphones',
    'plan1.f5':'SSL certificate — free',
    'plan1.btn':'Order',
    'plan2.tag':'🏢 BIZNES — Most popular',
    'plan2.desc':'A fully automated, prestigious, professional platform.',
    'plan2.per':'one-time payment',
    'plan2.f1':'Exclusive design — matched to your logo and brand',
    'plan2.f2':'Extended catalog — filters, descriptions',
    'plan2.f3':'SEO-ready — high rankings on Google and Yandex',
    'plan2.f4':'Multi-language support',
    'plan2.btn':'Start now →',
    'cta.tag':'// get in touch','cta.h2_a':'Your site','cta.h2_b':'today','cta.h2_c':'is ready.',
    'cta.sub':'Got questions? Or want to start right now? We\'re here.',
    'order.tag':'// place an order','order.title':'Let\'s build your site.','order.subtitle':'Leave your details — we\'ll get back within an hour.',
    'order.ph.name':'Your name','order.ph.phone':'+998 XX XXX XX XX','order.ph.email':'email@example.com (optional)','order.ph.message':'Briefly about your project...',
    'order.plan.default':'Choose a plan','order.plan.start':'START — $99','order.plan.biznes':'BIZNES — $199','order.plan.consult':'Need consultation',
    'order.submit':'Send request →','order.divider':'or directly',
    'footer.copy':'© 2025 QuickWeb — Professional website creation','footer.loc':'Tashkent, Uzbekistan'
  }
};

const TW_WORDS = {
  uz: ['raqamda','onlaynda','Googleda','kuchli'],
  ru: ['в цифре','онлайн','в Google','мощный'],
  en: ['digital','online','on Google','powerful']
};

const MARQUEE_ITEMS = {
  uz: ['Mobil Dizayn','SEO Optimizatsiya','Tezkor Topshirish','SSL Sertifikat','Admin Panel','Telegram Bot','Eksklyuziv Dizayn','Domenga Ulash'],
  ru: ['Мобильный дизайн','SEO-оптимизация','Быстрая сдача','SSL-сертификат','Админ-панель','Telegram-бот','Эксклюзивный дизайн','Подключение домена'],
  en: ['Mobile Design','SEO Optimization','Fast Delivery','SSL Certificate','Admin Panel','Telegram Bot','Exclusive Design','Domain Connection']
};

/* ============================================================
   THEME
============================================================ */
const themeBtn = document.getElementById('themeToggle');
function applyTheme(t) {
  document.documentElement.setAttribute('data-theme', t);
  themeBtn.textContent = t === 'dark' ? '☀' : '☾';
  themeBtn.setAttribute('aria-label', t === 'dark' ? 'Switch to light' : 'Switch to dark');
}
applyTheme(localStorage.getItem('qw-theme') || 'dark');
themeBtn.addEventListener('click', () => {
  const next = document.documentElement.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
  applyTheme(next);
  try { localStorage.setItem('qw-theme', next); } catch(e) {}
});

/* ============================================================
   I18N RUNTIME
============================================================ */
let currentLang = localStorage.getItem('qw-lang') || 'uz';
function setLang(lang) {
  if (!I18N[lang]) lang = 'uz';
  currentLang = lang;
  const dict = I18N[lang];

  document.querySelectorAll('[data-i18n]').forEach(el => {
    const key = el.dataset.i18n;
    if (dict[key] !== undefined) el.innerHTML = dict[key];
  });
  document.querySelectorAll('[data-i18n-ph]').forEach(el => {
    const key = el.dataset.i18nPh;
    if (dict[key] !== undefined) el.placeholder = dict[key];
  });

  document.documentElement.lang = lang;
  document.querySelectorAll('.lang-btn').forEach(b => b.classList.toggle('active', b.dataset.lang === lang));

  // Rebuild marquee
  buildMarquee(lang);
  // Reset typewriter
  resetTypewriter();

  try { localStorage.setItem('qw-lang', lang); } catch(e) {}
}
document.querySelectorAll('.lang-btn').forEach(btn => {
  btn.addEventListener('click', () => setLang(btn.dataset.lang));
});

/* ============================================================
   MARQUEE BUILD
============================================================ */
function buildMarquee(lang) {
  const track = document.getElementById('marqueeTrack');
  const items = MARQUEE_ITEMS[lang] || MARQUEE_ITEMS.uz;
  // duplicate twice for seamless scroll
  const seq = [...items, ...items];
  track.innerHTML = seq.map(t =>
    `<span class="marquee-item">${t} <span class="dot-sep">✦</span></span>`
  ).join('');
}

/* ============================================================
   ORDER OVERLAY
============================================================ */
const overlay = document.getElementById('orderOverlay');
const closeBtn = document.getElementById('orderClose');
const planSelect = document.getElementById('orderPlan');
const formNext = document.getElementById('formNext');
formNext.value = window.location.href.split('#')[0] + '?sent=1';

function openOrder(plan) {
  if (plan && planSelect) planSelect.value = plan;
  overlay.classList.add('open');
  document.body.classList.add('no-scroll');
}
function closeOrder() {
  overlay.classList.remove('open');
  document.body.classList.remove('no-scroll');
}

document.querySelectorAll('[data-open-order]').forEach(el => {
  el.addEventListener('click', e => {
    e.preventDefault();
    openOrder(el.dataset.plan || '');
  });
});
closeBtn.addEventListener('click', closeOrder);
overlay.addEventListener('click', e => { if (e.target === overlay) closeOrder(); });
document.addEventListener('keydown', e => { if (e.key === 'Escape' && overlay.classList.contains('open')) closeOrder(); });

// Show success banner if redirected back
if (new URLSearchParams(window.location.search).get('sent') === '1') {
  const msg = document.createElement('div');
  msg.style.cssText = 'position:fixed;top:80px;left:50%;transform:translateX(-50%);background:var(--acid);color:#080808;padding:0.9rem 1.5rem;border-radius:4px;font-family:Syne,sans-serif;font-weight:700;z-index:3000;box-shadow:0 12px 40px rgba(200,255,0,0.4)';
  const successMsg = { uz:'✓ Buyurtma yuborildi! Tez orada bog\'lanamiz.', ru:'✓ Заявка отправлена! Скоро свяжемся.', en:'✓ Request sent! We\'ll be in touch soon.' };
  msg.textContent = successMsg[currentLang] || successMsg.uz;
  document.body.appendChild(msg);
  setTimeout(() => msg.style.opacity = '0', 5000);
  setTimeout(() => msg.remove(), 5500);
}

/* ============================================================
   SCROLL PROGRESS
============================================================ */
const pb = document.getElementById('progressBar');
window.addEventListener('scroll', () => {
  pb.style.width = (window.scrollY / (document.body.scrollHeight - window.innerHeight) * 100) + '%';
});

/* ============================================================
   CURSOR + TRAIL (desktop only)
============================================================ */
const cursor = document.getElementById('cursor');
const canvas = document.getElementById('cursorCanvas');
const isDesktop = window.matchMedia('(min-width: 769px)').matches;

if (isDesktop) {
  const ctx = canvas.getContext('2d');
  let W = canvas.width = window.innerWidth, H = canvas.height = window.innerHeight;
  window.addEventListener('resize', () => { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight; });

  let mx = W/2, my = H/2;
  const pts = [];
  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx - 5 + 'px';
    cursor.style.top = my - 5 + 'px';
    pts.push({ x: mx, y: my, t: Date.now() });
    if (pts.length > 24) pts.shift();
  });
  document.addEventListener('mouseover', e => {
    if (e.target.closest('a,button,input,select,textarea')) cursor.classList.add('big');
  });
  document.addEventListener('mouseout', e => {
    if (e.target.closest('a,button,input,select,textarea')) cursor.classList.remove('big');
  });
  (function loop() {
    ctx.clearRect(0, 0, W, H);
    const now = Date.now();
    for (let i = 1; i < pts.length; i++) {
      const age = (now - pts[i].t) / 400;
      if (age > 1) continue;
      const alpha = (1 - age) * 0.22 * (i / pts.length);
      const r = (i / pts.length) * 5;
      ctx.beginPath();
      ctx.arc(pts[i].x, pts[i].y, r, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(200,255,0,${alpha})`;
      ctx.fill();
    }
    requestAnimationFrame(loop);
  })();
} else {
  cursor.style.display = 'none';
  canvas.style.display = 'none';
}

/* ============================================================
   PARTICLES
============================================================ */
const pc = document.getElementById('particles');
for (let i = 0; i < 14; i++) {
  const p = document.createElement('div');
  p.className = 'particle';
  const s = Math.random() * 2.5 + 1;
  p.style.cssText = `width:${s}px;height:${s}px;left:${Math.random()*100}%;animation-duration:${7+Math.random()*10}s;animation-delay:${Math.random()*10}s;opacity:0;`;
  pc.appendChild(p);
}

/* ============================================================
   TYPEWRITER
============================================================ */
const twEl = document.getElementById('tw');
let twWi = 0, twCi = 0, twDeleting = false, twTimer = null;
function tw() {
  const words = TW_WORDS[currentLang] || TW_WORDS.uz;
  const w = words[twWi % words.length];
  if (!twDeleting) {
    twEl.textContent = w.slice(0, ++twCi);
    if (twCi === w.length) { twDeleting = true; twTimer = setTimeout(tw, 1800); return; }
    twTimer = setTimeout(tw, 90);
  } else {
    twEl.textContent = w.slice(0, --twCi);
    if (twCi === 0) { twDeleting = false; twWi = (twWi + 1) % words.length; twTimer = setTimeout(tw, 300); return; }
    twTimer = setTimeout(tw, 45);
  }
}
function resetTypewriter() {
  if (twTimer) clearTimeout(twTimer);
  twWi = 0; twCi = 0; twDeleting = false;
  twEl.textContent = '';
  tw();
}

/* ============================================================
   COUNTERS + INTERSECTION OBSERVER
============================================================ */
function runCounter(el) {
  const target = parseInt(el.dataset.count);
  const suffix = el.dataset.suffix || '';
  if (!target) return;
  let cur = 0; const step = target / 45;
  const t = setInterval(() => {
    cur = Math.min(cur + step, target);
    el.textContent = Math.round(cur) + suffix;
    if (cur >= target) clearInterval(t);
  }, 28);
}

const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      if (e.target.dataset.count) runCounter(e.target);
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.reveal, .feature-card, .pain-card, .step, .preview-block').forEach((el, i) => {
  el.style.transitionDelay = (i % 4 * 0.1) + 's';
  obs.observe(el);
});
document.querySelectorAll('.stat-num[data-count]').forEach(el => obs.observe(el));

/* ============================================================
   PARALLAX
============================================================ */
window.addEventListener('scroll', () => {
  const g = document.querySelector('.hero-grid');
  if (g) g.style.transform = `translateY(${window.scrollY * 0.12}px)`;
});

/* ============================================================
   INIT
============================================================ */
setLang(currentLang); // builds marquee + starts typewriter
</script>
</body>
</html>
