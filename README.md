<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
  <meta name="theme-color" content="#ffffff">
  <meta name="description" content="Kall helps travelers in Korea book tickets, reservations, and local services through Korean-speaking assistance.">
  <title>Kall | Korea Ticket Booking Assistant</title>
  <style>
    :root {
      color-scheme: light;
      --bg: #f7fbff;
      --paper: #ffffff;
      --paper-soft: rgba(255, 255, 255, .92);
      --ink: #111827;
      --ink-2: #334155;
      --muted: #718096;
      --line: rgba(17, 24, 39, .09);
      --blue: #2563ff;
      --blue-2: #174bd7;
      --blue-soft: #eaf1ff;
      --teal: #13b8a6;
      --green: #13b981;
      --amber: #f59e0b;
      --rose: #f43f5e;
      --violet: #7457f5;
      --shadow: 0 24px 60px rgba(15, 23, 42, .14);
      --shadow-soft: 0 12px 30px rgba(15, 23, 42, .09);
      --max: 560px;
      --safe-top: env(safe-area-inset-top, 0px);
      --safe-bottom: env(safe-area-inset-bottom, 0px);
    }

    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; background: var(--bg); }
    body {
      margin: 0;
      min-height: 100vh;
      color: var(--ink);
      background:
        linear-gradient(180deg, rgba(255, 255, 255, .8), rgba(247, 251, 255, 1) 560px),
        var(--bg);
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Apple SD Gothic Neo", "Noto Sans KR", "Noto Sans JP", "Noto Sans SC", Arial, sans-serif;
      letter-spacing: 0;
    }

    body.locked { overflow: hidden; }
    a { color: inherit; text-decoration: none; }
    button, input, textarea, select { font: inherit; }
    button { border: 0; cursor: pointer; -webkit-tap-highlight-color: transparent; }
    img, svg { display: block; }

    .app {
      width: min(100%, var(--max));
      min-height: 100vh;
      margin: 0 auto;
      padding: calc(12px + var(--safe-top)) 16px calc(98px + var(--safe-bottom));
      position: relative;
    }

    .topbar {
      position: sticky;
      top: 0;
      z-index: 40;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      margin: calc(-12px - var(--safe-top)) -16px 12px;
      padding: calc(12px + var(--safe-top)) 16px 11px;
      background: rgba(255, 255, 255, .94);
      border-bottom: 1px solid rgba(17, 24, 39, .06);
      backdrop-filter: blur(18px);
    }

    .brand {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      min-width: 0;
    }

    .brand-logo {
      width: 42px;
      height: 42px;
      flex: 0 0 auto;
      display: grid;
      place-items: center;
      overflow: hidden;
      border-radius: 14px;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .07);
      box-shadow: 0 12px 26px rgba(37, 99, 255, .16);
    }

    .brand-logo img {
      width: 34px;
      height: 34px;
      object-fit: contain;
      transform: scale(2.4);
    }

    .brand-copy { display: grid; gap: 2px; min-width: 0; }
    .brand-name { font-size: 18px; line-height: 1; font-weight: 950; }
    .brand-sub {
      color: var(--muted);
      font-size: 11px;
      line-height: 1.15;
      font-weight: 780;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .icon-btn {
      width: 44px;
      height: 44px;
      display: grid;
      place-items: center;
      border-radius: 16px;
      color: #0f172a;
      background: rgba(255, 255, 255, .95);
      border: 1px solid rgba(17, 24, 39, .07);
      box-shadow: 0 10px 24px rgba(15, 23, 42, .08);
      position: relative;
      transition: transform .18s ease;
    }

    .icon-btn:active,
    .btn:active,
    .nav-btn:active,
    .choice:active,
    .timeline-item:active,
    .plan-option:active {
      transform: translateY(1px) scale(.99);
    }

    .lang-icon { width: 23px; height: 23px; }
    .lang-code {
      position: absolute;
      right: -2px;
      bottom: -4px;
      min-width: 23px;
      height: 23px;
      display: grid;
      place-items: center;
      padding: 0 5px;
      border-radius: 99px;
      color: #fff;
      background: var(--blue);
      border: 2px solid #fff;
      font-size: 10px;
      font-weight: 950;
    }

    .view { display: none; animation: rise .24s ease both; }
    .view.active { display: block; }
    @keyframes rise {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    h1, h2, h3 { margin: 0; letter-spacing: 0; }
    h1 {
      color: var(--ink);
      font-size: 38px;
      line-height: 1.04;
      font-weight: 950;
    }
    h2 {
      color: var(--ink);
      font-size: 25px;
      line-height: 1.18;
      font-weight: 940;
    }
    h3 {
      color: var(--ink);
      font-size: 17px;
      line-height: 1.2;
      font-weight: 930;
    }

    .lead {
      margin: 14px 0 20px;
      color: var(--ink-2);
      font-size: 15px;
      line-height: 1.58;
      font-weight: 650;
    }
    .copy {
      margin: 8px 0 0;
      color: var(--ink-2);
      font-size: 13px;
      line-height: 1.55;
      font-weight: 650;
    }
    .kicker {
      margin-bottom: 6px;
      color: var(--blue);
      font-size: 12px;
      font-weight: 930;
    }

    .hero { padding: 12px 0 0; }
    .hero-actions {
      display: grid;
      grid-template-columns: 1fr;
      gap: 10px;
      margin: 18px 0 20px;
    }

    .btn {
      width: 100%;
      min-height: 54px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 9px;
      padding: 0 18px;
      border-radius: 16px;
      color: #fff;
      background: linear-gradient(180deg, #3375ff 0%, #1d55ef 100%);
      box-shadow: 0 16px 34px rgba(37, 99, 255, .30), inset 0 1px 0 rgba(255, 255, 255, .28);
      font-size: 15px;
      line-height: 1.2;
      font-weight: 920;
      transition: transform .18s ease, box-shadow .18s ease;
    }
    .btn.secondary {
      color: #1f2937;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .08);
      box-shadow: 0 12px 28px rgba(15, 23, 42, .08);
    }
    .btn.dark {
      background: linear-gradient(180deg, #202938 0%, #111827 100%);
      box-shadow: 0 16px 34px rgba(17, 24, 39, .24);
    }
    .btn.small {
      min-height: 44px;
      border-radius: 14px;
      padding: 0 13px;
      font-size: 13px;
    }
    .btn:disabled {
      opacity: .5;
      cursor: not-allowed;
      box-shadow: none;
    }
    .icon { width: 21px; height: 21px; flex: 0 0 auto; }

    .phone-scene {
      min-height: 330px;
      display: grid;
      place-items: center;
      position: relative;
      perspective: 1200px;
      margin: 2px -2px 4px;
    }

    .phone {
      width: min(100%, 324px);
      min-height: 316px;
      border-radius: 39px;
      padding: 13px;
      background: linear-gradient(145deg, rgba(255, 255, 255, .98), rgba(230, 238, 250, .94));
      border: 1px solid rgba(255, 255, 255, .92);
      box-shadow: 0 34px 70px rgba(37, 99, 255, .16), 0 18px 42px rgba(15, 23, 42, .14), inset 0 1px 0 rgba(255, 255, 255, .9);
      transform: rotateX(9deg) rotateY(-8deg) rotateZ(1deg);
      transform-style: preserve-3d;
      animation: floatPhone 5s ease-in-out infinite;
    }
    @keyframes floatPhone {
      0%, 100% { transform: rotateX(9deg) rotateY(-8deg) rotateZ(1deg) translateY(0); }
      50% { transform: rotateX(7deg) rotateY(-6deg) rotateZ(-1deg) translateY(-8px); }
    }

    .screen {
      min-height: 290px;
      border-radius: 29px;
      padding: 16px;
      overflow: hidden;
      background: linear-gradient(180deg, #fff 0%, #f7fbff 100%);
      box-shadow: inset 0 0 0 1px rgba(17, 24, 39, .05);
    }
    .screen-head {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      margin-bottom: 13px;
    }
    .screen-head b { font-size: 13px; font-weight: 920; }
    .screen-badge {
      min-height: 28px;
      display: inline-flex;
      align-items: center;
      border-radius: 999px;
      padding: 0 9px;
      color: #05704a;
      background: rgba(19, 185, 129, .12);
      font-size: 11px;
      font-weight: 930;
      white-space: nowrap;
    }

    .mini-card {
      border-radius: 22px;
      padding: 15px;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .06);
      box-shadow: var(--shadow-soft);
    }
    .mini-card h3 { font-size: 20px; line-height: 1.15; }
    .mini-card p {
      margin: 8px 0 14px;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.45;
      font-weight: 730;
    }
    .mini-row {
      min-height: 38px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
      margin-top: 8px;
      padding: 0 11px;
      border-radius: 14px;
      background: #f2f6ff;
      font-size: 12px;
      font-weight: 850;
    }
    .mini-row span:last-child { color: var(--blue); font-weight: 950; }

    .float-chip {
      position: absolute;
      z-index: 2;
      display: flex;
      align-items: center;
      gap: 6px;
      padding: 7px 9px;
      border-radius: 999px;
      background: rgba(255, 255, 255, .95);
      border: 1px solid rgba(255, 255, 255, .85);
      box-shadow: 0 10px 22px rgba(15, 23, 42, .11);
      backdrop-filter: blur(12px);
      font-size: 10.5px;
      font-weight: 920;
      transform: translateZ(60px);
    }
    .float-left { left: 10px; top: 78px; }
    .float-right { right: 10px; bottom: 54px; }
    .chip-symbol {
      width: 22px;
      height: 22px;
      display: grid;
      place-items: center;
      border-radius: 8px;
      color: #fff;
      background: var(--green);
      font-size: 11px;
      font-weight: 950;
    }
    .chip-symbol.blue { background: var(--blue); }
    .chip-symbol.rose { background: var(--rose); }

    .section { margin: 25px 0; }
    .section-head {
      display: flex;
      align-items: flex-end;
      justify-content: space-between;
      gap: 12px;
      margin-bottom: 13px;
    }
    .glass {
      border-radius: 22px;
      background: var(--paper-soft);
      border: 1px solid rgba(255, 255, 255, .84);
      box-shadow: var(--shadow-soft);
      backdrop-filter: blur(18px);
      overflow: hidden;
    }

    .ticket-strip {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 9px;
    }
    .ticket-chip {
      min-height: 70px;
      display: grid;
      grid-template-columns: 36px 1fr;
      align-items: center;
      gap: 10px;
      padding: 12px;
      border-radius: 18px;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .06);
      box-shadow: 0 10px 24px rgba(15, 23, 42, .06);
    }
    .ticket-icon {
      width: 36px;
      height: 36px;
      display: grid;
      place-items: center;
      border-radius: 13px;
      color: #fff;
      background: linear-gradient(135deg, var(--blue), var(--teal));
      font-size: 15px;
      font-weight: 950;
    }
    .ticket-chip:nth-child(2) .ticket-icon { background: linear-gradient(135deg, var(--rose), var(--amber)); }
    .ticket-chip:nth-child(3) .ticket-icon { background: linear-gradient(135deg, var(--violet), var(--blue)); }
    .ticket-chip:nth-child(4) .ticket-icon { background: linear-gradient(135deg, var(--teal), var(--green)); }
    .ticket-chip b {
      display: block;
      font-size: 12px;
      line-height: 1.2;
      font-weight: 920;
    }
    .ticket-chip span {
      display: block;
      margin-top: 4px;
      color: var(--muted);
      font-size: 10.5px;
      line-height: 1.25;
      font-weight: 760;
    }

    .pricing-frame {
      border: 1px solid rgba(37, 99, 255, .10);
      border-radius: 22px;
      padding: 11px 10px;
      background: linear-gradient(180deg, #f8fbff 0%, #fff 100%);
      overflow: visible;
      box-shadow: 0 14px 32px rgba(37, 99, 255, .07);
    }
    .pricing-section .section-head { margin-bottom: 9px; }
    .pricing-section .section-head h2 { font-size: 21px; line-height: 1.14; }
    .pricing-section .kicker { font-size: 11px; margin-bottom: 4px; }
    .plan-board-title {
      margin: 0 0 9px;
      text-align: center;
      color: #0f172a;
      font-size: 17px;
      line-height: 1.12;
      font-weight: 950;
    }
    .pricing {
      display: grid;
      grid-template-columns: 1fr;
      align-items: stretch;
      gap: 9px;
      min-width: 0;
    }
    .price-card {
      --plan-accent: #2563ff;
      --plan-accent-dark: #1d4ed8;
      --plan-tint: #eff6ff;
      position: relative;
      overflow: hidden;
      display: grid;
      grid-template-columns: minmax(94px, 112px) 1fr;
      grid-auto-rows: auto;
      gap: 6px 11px;
      min-height: 0;
      border-radius: 18px;
      padding: 12px 12px 12px 14px;
      background: linear-gradient(135deg, #fff 0%, #fbfdff 100%);
      border: 1px solid rgba(15, 23, 42, .07);
      box-shadow: 0 8px 18px rgba(37, 99, 255, .055);
      cursor: pointer;
      transition: transform .18s ease, border-color .18s ease, box-shadow .18s ease;
    }
    .price-card::before {
      content: "";
      position: absolute;
      inset: 0 auto 0 0;
      width: 4px;
      background: var(--plan-accent, var(--blue));
    }
    .price-card.lite { --plan-accent: #2563ff; --plan-accent-dark: #1d4ed8; --plan-tint: #eff6ff; }
    .price-card.wonderful { --plan-accent: #0ea5e9; --plan-accent-dark: #0284c7; --plan-tint: #f0f9ff; }
    .price-card.super { --plan-accent: #7457f5; --plan-accent-dark: #5b3de6; --plan-tint: #f5f3ff; }
    .price-card.selected,
    .price-card.featured {
      color: var(--ink);
      background: linear-gradient(180deg, #f8fcff 0%, #fff 54%);
      border-color: rgba(0, 150, 255, .42);
      box-shadow: 0 14px 30px rgba(0, 150, 255, .16), 0 0 0 1px rgba(0, 150, 255, .08);
    }
    .price-card:hover { transform: translateY(-2px); box-shadow: 0 16px 32px rgba(15, 23, 42, .10); }
    .price-card:focus-visible { outline: 3px solid rgba(37, 99, 255, .25); outline-offset: 3px; }

    .price-top {
      grid-column: 1;
      grid-row: 1 / span 3;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: flex-start;
      gap: 7px;
      min-width: 0;
      margin: 0;
      text-align: left;
    }
    .price-top h3 {
      min-height: 0;
      display: inline-flex;
      align-items: center;
      width: fit-content;
      max-width: 100%;
      padding: 5px 8px;
      border-radius: 999px;
      color: var(--plan-accent-dark);
      background: var(--plan-tint);
      font-size: 12px;
      line-height: 1;
      font-weight: 930;
    }
    .price {
      margin: 0;
      color: #0f172a;
      font-size: 21px;
      line-height: .98;
      font-weight: 950;
      white-space: nowrap;
      word-break: keep-all;
    }
    .price small {
      display: block;
      margin-top: 4px;
      color: var(--muted);
      font-size: 8.5px;
      line-height: 1.2;
      font-weight: 820;
    }
    .plan-purpose {
      grid-column: 2;
      grid-row: 1;
      color: #1f2937;
      font-size: 9.8px;
      line-height: 1.26;
      font-weight: 820;
      padding-right: 36px;
    }
    .plan-feature-list {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 4px 7px;
      margin: 0;
      padding: 0;
      list-style: none;
    }
    .plan-feature-list li {
      position: relative;
      padding-left: 13px;
      color: #172033;
      font-size: 8.4px;
      line-height: 1.18;
      font-weight: 730;
    }
    .plan-feature-list li::before {
      content: "";
      position: absolute;
      top: .45em;
      left: 0;
      width: 6px;
      height: 6px;
      border-radius: 999px;
      background: #475569;
    }
    .plan-feature-list li.plan-diff {
      color: var(--plan-accent-dark);
      font-weight: 900;
    }
    .plan-feature-list li.plan-diff::before { background: var(--plan-accent); }
    .popular-ribbon {
      position: absolute;
      top: 5px;
      right: 6px;
      min-width: 72px;
      height: 18px;
      padding: 0 7px;
      display: grid;
      place-items: center;
      border-radius: 999px;
      color: #fff;
      background: linear-gradient(120deg, #ff3b5c 0%, #ff7a45 42%, #ff3b5c 72%);
      background-size: 220% 100%;
      font-size: 7px;
      line-height: 1;
      font-weight: 950;
      box-shadow: 0 6px 14px rgba(255, 59, 92, .24);
    }
    .plan-example {
      grid-column: 2;
      display: block;
      border-radius: 10px;
      padding: 6px 8px;
      color: #334155;
      background: #f8fafc;
      border: 1px solid rgba(15, 23, 42, .07);
      font-size: 8.6px;
      line-height: 1.25;
      font-weight: 760;
    }
    .fee-note {
      margin-top: 10px;
      padding: 11px 12px;
      border-radius: 16px;
      color: #334155;
      background: #fff;
      border: 1px dashed rgba(37, 99, 255, .22);
      font-size: 11px;
      line-height: 1.45;
      font-weight: 760;
    }
    .fee-note b { color: #0f172a; font-weight: 950; }
    .fee-note a {
      color: var(--blue);
      font-weight: 900;
      text-decoration: underline;
      text-decoration-thickness: 1px;
      text-underline-offset: 2px;
    }

    .steps { display: grid; gap: 10px; }
    .step-card {
      position: relative;
      isolation: isolate;
      overflow: hidden;
      min-height: 82px;
      display: grid;
      grid-template-columns: 44px 1fr;
      align-items: center;
      gap: 12px;
      border-radius: 20px;
      padding: 13px;
      background: linear-gradient(135deg, #fff 0%, #f8fbff 100%);
      border: 1px solid rgba(17, 24, 39, .06);
      box-shadow: 0 10px 24px rgba(15, 23, 42, .07);
    }
    .step-card::before {
      content: "";
      position: absolute;
      inset: 0;
      z-index: -1;
      background: radial-gradient(circle at 26px 28px, rgba(37, 99, 255, .14), transparent 44%);
      opacity: .42;
    }
    .step-no {
      width: 44px;
      height: 44px;
      display: grid;
      place-items: center;
      border-radius: 16px;
      color: #fff;
      background: var(--blue);
      font-weight: 950;
      box-shadow: 0 12px 26px rgba(37, 99, 255, .24);
    }
    .step-card b {
      display: block;
      font-size: 14px;
      line-height: 1.2;
      font-weight: 930;
    }
    .step-card span {
      display: block;
      margin-top: 4px;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.35;
      font-weight: 720;
    }

    .estimate-grid,
    .notice-grid {
      display: grid;
      gap: 10px;
    }
    .estimate-card,
    .notice-card {
      border-radius: 20px;
      padding: 14px;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .06);
      box-shadow: 0 10px 24px rgba(15, 23, 42, .07);
    }
    .estimate-card {
      display: grid;
      grid-template-columns: 44px 1fr auto;
      align-items: center;
      gap: 10px;
    }
    .estimate-icon {
      width: 44px;
      height: 44px;
      display: grid;
      place-items: center;
      border-radius: 16px;
      color: #fff;
      background: linear-gradient(135deg, var(--blue), var(--teal));
      font-size: 14px;
      font-weight: 950;
    }
    .estimate-card:nth-child(2) .estimate-icon { background: linear-gradient(135deg, var(--rose), var(--amber)); }
    .estimate-card:nth-child(3) .estimate-icon { background: linear-gradient(135deg, var(--violet), var(--blue)); }
    .estimate-card:nth-child(4) .estimate-icon { background: linear-gradient(135deg, var(--teal), var(--green)); }
    .estimate-card b {
      display: block;
      font-size: 13px;
      font-weight: 930;
    }
    .estimate-card span {
      display: block;
      margin-top: 4px;
      color: var(--muted);
      font-size: 11px;
      font-weight: 760;
    }
    .estimate-time {
      color: var(--blue);
      font-size: 13px;
      font-weight: 950;
      white-space: nowrap;
    }

    .notice-card { position: relative; overflow: hidden; }
    .notice-card h3 {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 16px;
    }
    .notice-card h3 img {
      width: 30px;
      height: 30px;
      object-fit: contain;
    }
    .notice-card ul {
      display: grid;
      gap: 8px;
      margin: 12px 0 0;
      padding: 0;
      list-style: none;
    }
    .notice-card li {
      position: relative;
      padding-left: 16px;
      color: var(--ink-2);
      font-size: 12px;
      line-height: 1.45;
      font-weight: 700;
    }
    .notice-card li::before {
      content: "";
      position: absolute;
      top: .55em;
      left: 1px;
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: var(--blue);
    }
    .notice-card.refund li::before { background: var(--rose); }
    .notice-card.time li::before { background: var(--teal); }

    .book-shell { display: grid; gap: 14px; }
    .progress-card {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      padding: 9px;
      border-radius: 22px;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .06);
      box-shadow: var(--shadow-soft);
    }
    .progress-step {
      min-height: 50px;
      display: grid;
      place-items: center;
      align-content: center;
      gap: 2px;
      border-radius: 16px;
      color: var(--muted);
      background: #f8fafc;
      font-size: 11px;
      font-weight: 900;
    }
    .progress-step b {
      color: inherit;
      font-size: 15px;
      line-height: 1;
      font-weight: 950;
    }
    .progress-step.active {
      color: var(--blue);
      background: var(--blue-soft);
    }

    .form-card {
      padding: 17px;
      border-radius: 24px;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .06);
      box-shadow: var(--shadow-soft);
    }
    .form-step { display: none; }
    .form-step.active { display: block; animation: rise .2s ease both; }
    .form-step h2 { font-size: 22px; }
    .field-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 12px;
      margin-top: 15px;
    }
    .field {
      display: grid;
      gap: 7px;
    }
    .field label {
      color: #1f2937;
      font-size: 12px;
      font-weight: 900;
    }
    .field input,
    .field select,
    .field textarea {
      width: 100%;
      min-height: 48px;
      border: 1px solid rgba(17, 24, 39, .09);
      border-radius: 15px;
      padding: 0 13px;
      color: var(--ink);
      background: #f8fafc;
      outline: none;
      font-size: 14px;
      font-weight: 720;
      transition: border-color .18s ease, box-shadow .18s ease, background .18s ease;
    }
    .field textarea {
      min-height: 96px;
      padding-top: 12px;
      resize: vertical;
      line-height: 1.45;
    }
    .field input:focus,
    .field select:focus,
    .field textarea:focus {
      border-color: rgba(37, 99, 255, .48);
      background: #fff;
      box-shadow: 0 0 0 4px rgba(37, 99, 255, .10);
    }
    .field.invalid input,
    .field.invalid select,
    .field.invalid textarea {
      border-color: rgba(244, 63, 94, .72);
      box-shadow: 0 0 0 4px rgba(244, 63, 94, .09);
    }
    .field-help {
      display: none;
      color: var(--rose);
      font-size: 11px;
      font-weight: 800;
    }
    .field.invalid .field-help { display: block; }

    .plan-options,
    .choice-grid {
      display: grid;
      gap: 9px;
      margin-top: 15px;
    }
    .plan-option,
    .choice {
      min-height: 66px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      padding: 12px;
      border-radius: 18px;
      color: #1f2937;
      background: #f8fafc;
      border: 1px solid rgba(17, 24, 39, .07);
      transition: transform .18s ease, border-color .18s ease, background .18s ease;
      text-align: left;
    }
    .plan-option input { display: none; }
    .plan-option:has(input:checked),
    .choice.selected {
      background: #fff;
      border-color: rgba(37, 99, 255, .48);
      box-shadow: 0 12px 26px rgba(37, 99, 255, .10);
    }
    .plan-option b,
    .choice b {
      display: block;
      font-size: 14px;
      font-weight: 930;
    }
    .plan-option span span,
    .choice span {
      display: block;
      margin-top: 5px;
      color: var(--muted);
      font-size: 11px;
      line-height: 1.35;
      font-weight: 760;
    }
    .plan-price-pill {
      min-height: 32px;
      display: inline-flex;
      align-items: center;
      border-radius: 999px;
      padding: 0 10px;
      color: var(--blue);
      background: var(--blue-soft);
      font-size: 12px;
      font-weight: 950;
      white-space: nowrap;
    }

    .summary-card {
      display: grid;
      gap: 10px;
      padding: 14px;
      border-radius: 20px;
      background: #f8fafc;
      border: 1px solid rgba(17, 24, 39, .06);
      margin-top: 15px;
    }
    .summary-row {
      display: flex;
      justify-content: space-between;
      gap: 12px;
      padding: 9px 0;
      border-bottom: 1px dashed #d7dee9;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.3;
      font-weight: 800;
    }
    .summary-row:last-child { border-bottom: 0; }
    .summary-row b {
      color: #172033;
      font-weight: 950;
      text-align: right;
      overflow-wrap: anywhere;
    }
    .summary-total {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      gap: 12px;
      padding-top: 12px;
      border-top: 1px solid rgba(17, 24, 39, .08);
      color: #0f172a;
      font-size: 14px;
      font-weight: 920;
    }
    .summary-total b {
      font-size: 25px;
      line-height: 1;
      font-weight: 950;
    }
    .estimate-footnote {
      margin: 2px 0 0;
      color: var(--muted);
      font-size: 11px;
      line-height: 1.45;
      font-weight: 720;
    }

    .form-actions {
      display: grid;
      grid-template-columns: 1fr;
      gap: 10px;
      margin-top: 15px;
    }
    .form-actions.two { grid-template-columns: .8fr 1fr; }

    .status-card {
      border-radius: 24px;
      padding: 17px;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .06);
      box-shadow: var(--shadow-soft);
    }
    .status-top {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 10px;
      margin-bottom: 14px;
    }
    .status-no {
      color: var(--muted);
      font-size: 12px;
      font-weight: 920;
    }
    .status-pill {
      min-height: 28px;
      display: inline-flex;
      align-items: center;
      gap: 7px;
      border-radius: 999px;
      padding: 0 10px;
      color: #05704a;
      background: rgba(19, 185, 129, .12);
      font-size: 11px;
      font-weight: 930;
      white-space: nowrap;
    }
    .live-dot {
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: var(--green);
      box-shadow: 0 0 0 5px rgba(19, 185, 129, .13);
    }
    .status-card h2 { font-size: 24px; line-height: 1.18; }
    .status-card p {
      margin: 9px 0 0;
      color: var(--ink-2);
      font-size: 14px;
      line-height: 1.56;
      font-weight: 650;
    }
    .empty-state {
      min-height: 240px;
      display: grid;
      align-content: center;
      justify-items: center;
      gap: 14px;
      padding: 25px;
      border-radius: 25px;
      text-align: center;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .06);
      box-shadow: var(--shadow-soft);
    }
    .empty-icon {
      width: 80px;
      height: 80px;
      display: grid;
      place-items: center;
      border-radius: 27px;
      color: #fff;
      background: linear-gradient(135deg, #2563ff, #1fb6a5);
      box-shadow: 0 16px 36px rgba(37, 99, 255, .24);
    }
    .empty-icon img {
      width: 48px;
      height: 48px;
      object-fit: contain;
    }
    .timeline {
      display: grid;
      gap: 10px;
      margin-top: 14px;
    }
    .timeline-item {
      width: 100%;
      min-height: 72px;
      display: grid;
      grid-template-columns: 42px 1fr auto;
      align-items: center;
      gap: 10px;
      padding: 12px;
      border-radius: 18px;
      background: #f8fafc;
      border: 1px solid rgba(17, 24, 39, .06);
      text-align: left;
    }
    .stage-icon {
      width: 42px;
      height: 42px;
      display: grid;
      place-items: center;
      border-radius: 15px;
      color: #fff;
      background: var(--blue);
      font-size: 12px;
      font-weight: 950;
    }
    .timeline-item.done .stage-icon { background: var(--green); }
    .timeline-item.active .stage-icon { background: var(--blue); }
    .timeline-item.todo .stage-icon { background: #94a3b8; }
    .timeline-item b {
      display: block;
      font-size: 13px;
      line-height: 1.2;
      font-weight: 920;
    }
    .timeline-item span {
      display: block;
      margin-top: 4px;
      color: var(--muted);
      font-size: 11px;
      line-height: 1.3;
      font-weight: 760;
    }
    .timeline-time {
      color: var(--muted);
      font-size: 11px;
      font-weight: 920;
      white-space: nowrap;
    }

    .bottom-nav {
      position: fixed;
      z-index: 50;
      left: 50%;
      bottom: 0;
      width: min(100%, var(--max));
      transform: translateX(-50%);
      padding: 8px 14px calc(10px + var(--safe-bottom));
      background: rgba(255, 255, 255, .96);
      backdrop-filter: blur(14px);
    }
    .nav-inner {
      min-height: 64px;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 6px;
      padding: 7px;
      border-radius: 23px;
      background: #fff;
      border: 1px solid rgba(17, 24, 39, .07);
      box-shadow: 0 16px 36px rgba(15, 23, 42, .14);
    }
    .nav-btn {
      min-width: 0;
      display: grid;
      place-items: center;
      align-content: center;
      gap: 4px;
      border-radius: 17px;
      color: var(--muted);
      background: transparent;
      font-size: 11px;
      font-weight: 920;
    }
    .nav-btn.active {
      color: var(--blue);
      background: var(--blue-soft);
    }
    .nav-btn svg { width: 21px; height: 21px; }

    .toast {
      position: fixed;
      z-index: 120;
      left: 50%;
      bottom: calc(96px + var(--safe-bottom));
      width: min(calc(100% - 32px), 430px);
      min-height: 54px;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 12px 16px;
      border-radius: 18px;
      color: #fff;
      background: rgba(17, 24, 39, .94);
      box-shadow: 0 18px 42px rgba(15, 23, 42, .24);
      font-size: 13px;
      font-weight: 850;
      text-align: center;
      transform: translate(-50%, 18px);
      opacity: 0;
      pointer-events: none;
      transition: transform .2s ease, opacity .2s ease;
    }
    .toast.show {
      opacity: 1;
      transform: translate(-50%, 0);
    }

    @media (max-width: 370px) {
      h1 { font-size: 34px; }
      h2 { font-size: 22px; }
      .lead { font-size: 14px; }
      .ticket-strip { grid-template-columns: 1fr; }
      .price-card {
        grid-template-columns: 88px 1fr;
        gap: 6px 8px;
        padding: 10px 10px 10px 13px;
      }
      .price { font-size: 18px; }
      .price-top h3 { font-size: 11px; padding: 5px 7px; }
      .plan-purpose { padding-right: 28px; font-size: 8.8px; }
      .plan-feature-list { grid-template-columns: 1fr; gap: 3px; }
      .plan-feature-list li { font-size: 8px; }
      .popular-ribbon { right: 4px; font-size: 6px; padding: 0 4px; min-width: 60px; }
      .phone { width: 292px; min-height: 300px; }
      .phone-scene { min-height: 312px; }
      .screen { min-height: 274px; }
    }

    @media (min-width: 430px) {
      .hero-actions { grid-template-columns: 1fr .82fr; }
      .form-actions { grid-template-columns: 1fr .82fr; }
    }

    @media (min-width: 560px) {
      :root { --max: 680px; }
      .app { padding-left: 24px; padding-right: 24px; }
      .topbar { margin-left: -24px; margin-right: -24px; padding-left: 24px; padding-right: 24px; }
      .hero {
        display: grid;
        grid-template-columns: 1fr minmax(280px, 334px);
        align-items: center;
        gap: 22px;
      }
      .ticket-strip { grid-template-columns: repeat(4, minmax(0, 1fr)); }
      .estimate-grid { grid-template-columns: 1fr 1fr; }
      .notice-grid { grid-template-columns: 1fr 1fr; }
      .choice-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
      .field-grid.two { grid-template-columns: repeat(2, minmax(0, 1fr)); }
    }

    @media (min-width: 920px) {
      body { display: grid; justify-items: center; }
      :root { --max: 720px; }
      .app {
        margin-top: 26px;
        margin-bottom: 26px;
        min-height: calc(100vh - 52px);
        border-radius: 38px;
        background: #fff;
        box-shadow: 0 0 0 1px rgba(17, 24, 39, .06), 0 32px 80px rgba(15, 23, 42, .13);
      }
      .bottom-nav { border-radius: 0 0 38px 38px; }
    }

    @media (prefers-reduced-motion: reduce) {
      html { scroll-behavior: auto; }
      *, *::before, *::after {
        animation-duration: .01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: .01ms !important;
        scroll-behavior: auto !important;
      }
    }
  </style>
</head>
<body>
  <main class="app">
    <header class="topbar">
      <a class="brand" href="#" data-nav="intro" aria-label="Kall home">
        <div class="brand-logo" aria-hidden="true"><img src="./logo.png" alt=""></div>
        <div class="brand-copy">
          <div class="brand-name">Kall</div>
          <div class="brand-sub">Korea ticket booking help</div>
        </div>
      </a>
      <button class="icon-btn" type="button" aria-label="Language is English">
        <svg class="lang-icon" viewBox="0 0 24 24" fill="none" aria-hidden="true">
          <path d="M12 21a9 9 0 1 0 0-18 9 9 0 0 0 0 18Z" stroke="currentColor" stroke-width="2"/>
          <path d="M3.7 9h16.6M3.7 15h16.6M12 3c2 2.2 3 5.2 3 9s-1 6.8-3 9c-2-2.2-3-5.2-3-9s1-6.8 3-9Z" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
        </svg>
        <span class="lang-code">EN</span>
      </button>
    </header>

    <section class="view active" id="view-intro">
      <div class="hero">
        <div>
          <div class="kicker">Ticket-first concierge</div>
          <h1>Korea tickets, booked through a local voice.</h1>
          <p class="lead">Send us the event, ticket link, date, seats, and payment limits. Kall handles Korean calls, site checks, and booking coordination, then sends the result to your messenger.</p>
          <div class="hero-actions">
            <button class="btn" type="button" data-nav="book">
              <svg class="icon" viewBox="0 0 24 24" fill="none"><path d="M5 5h14v14H5z" stroke="currentColor" stroke-width="2.2"/><path d="M8 9h8M8 13h5" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"/></svg>
              <span>Request tickets</span>
            </button>
            <button class="btn secondary" type="button" data-nav="status">Track request</button>
          </div>
        </div>
        <div class="phone-scene" aria-label="Kall booking preview">
          <div class="float-chip float-left"><span class="chip-symbol">KR</span><span>Korean call ready</span></div>
          <div class="phone">
            <div class="screen">
              <div class="screen-head"><b>Kall</b><span class="screen-badge">Checking seats</span></div>
              <div class="mini-card">
                <h3>Baseball in Seoul</h3>
                <p>Jamsil Stadium, 2 seats, Saturday night, backup section included.</p>
                <div class="mini-row"><span>Ticket request</span><span>Received</span></div>
                <div class="mini-row"><span>Venue/account check</span><span>Live</span></div>
                <div class="mini-row"><span>Result to messenger</span><span>Next</span></div>
              </div>
            </div>
          </div>
          <div class="float-chip float-right"><span class="chip-symbol blue">W</span><span id="chipPrice">From 1,250 KRW/min</span></div>
        </div>
      </div>

      <section class="section">
        <div class="section-head"><div><div class="kicker">Most requested by travelers</div><h2>Built around Korean ticket friction.</h2></div></div>
        <div class="ticket-strip">
          <article class="ticket-chip"><div class="ticket-icon">BB</div><div><b>Baseball tickets</b><span>KBO games, seat sections, same-day checks</span></div></article>
          <article class="ticket-chip"><div class="ticket-icon">CV</div><div><b>Concerts and festivals</b><span>Availability, Korean-only notices, purchase help</span></div></article>
          <article class="ticket-chip"><div class="ticket-icon">SH</div><div><b>Shows and musicals</b><span>Dates, cast schedule, seat alternatives</span></div></article>
          <article class="ticket-chip"><div class="ticket-icon">TR</div><div><b>Trip bookings</b><span>Train, theme park, pickup, restaurant backups</span></div></article>
        </div>
      </section>

      <section class="section pricing-section">
        <div class="section-head">
          <div>
            <div class="kicker">Pricing policy</div>
            <h2>Time-based support, inspired by Wonderful.</h2>
          </div>
        </div>
        <div class="pricing-frame" aria-label="Service plans">
          <div class="plan-board-title">Choose the time bank that fits your trip</div>
          <div class="pricing">
            <article class="price-card lite" data-plan-card="lite" role="button" tabindex="0">
              <div class="price-top"><div><h3>Travel Lite</h3></div><div class="price">2,000<small>KRW / min</small></div></div>
              <p class="plan-purpose">Best for one short ticket check or a single reservation task.</p>
              <div><ul class="plan-feature-list"><li>Minimum deposit: 180,000 KRW</li><li>Includes 1.5 hours</li><li>Refund scheduled after 1 month</li><li>No package discount</li></ul></div>
              <div class="plan-example">Example: one baseball ticket purchase or one restaurant booking with a clear backup.</div>
            </article>

            <article class="price-card wonderful featured selected" data-plan-card="wonderful" role="button" tabindex="0">
              <span class="popular-ribbon">Recommended</span>
              <div class="price-top"><div><h3>Wonderful</h3></div><div class="price">1,500<small>KRW / min</small></div></div>
              <p class="plan-purpose">Recommended for most visitors booking tickets, restaurants, and itinerary items.</p>
              <div><ul class="plan-feature-list"><li>Minimum deposit: 360,000 KRW</li><li>Includes 4 hours</li><li>5% first-time discount</li><li class="plan-diff">Refund scheduled after 3 months</li></ul></div>
              <div class="plan-example">Example: concert ticket check plus restaurant and transportation coordination.</div>
            </article>

            <article class="price-card super" data-plan-card="super" role="button" tabindex="0">
              <div class="price-top"><div><h3>Super</h3></div><div class="price">1,250<small>KRW / min</small></div></div>
              <p class="plan-purpose">For heavy users or groups with many requests during a Korea trip.</p>
              <div><ul class="plan-feature-list"><li>Minimum deposit: 900,000 KRW</li><li>Includes 12 hours</li><li>Lowest per-minute rate</li><li class="plan-diff">Non-refundable; forfeited after 3 months</li></ul></div>
              <div class="plan-example">Example: group itinerary with multiple ticket, venue, delivery, and booking tasks.</div>
            </article>
          </div>
          <div class="fee-note">
            <b>Payment note:</b> foreign card and PayPal payments may include an 8.5% processing and currency-exchange fee. On-site payment, Korean bank transfer, or Wise may reduce the fee when available.
            <a href="https://www.gowonderfully.com/pricing" target="_blank" rel="noopener">Reference</a>
          </div>
        </div>
      </section>

      <section class="section">
        <div class="section-head"><div><div class="kicker">How long does it take?</div><h2>Ticket work is usually measured in minutes.</h2></div></div>
        <div class="estimate-grid">
          <article class="estimate-card"><div class="estimate-icon">BB</div><div><b>Buy baseball tickets</b><span>Seat checks, account friction, payment coordination</span></div><div class="estimate-time">15-30 min</div></article>
          <article class="estimate-card"><div class="estimate-icon">CV</div><div><b>Buy concert tickets</b><span>Availability, purchase flow, troubleshooting</span></div><div class="estimate-time">15-45 min</div></article>
          <article class="estimate-card"><div class="estimate-icon">MV</div><div><b>Buy movie tickets</b><span>Fastest ticket flow when details are clear</span></div><div class="estimate-time">10-20 min</div></article>
          <article class="estimate-card"><div class="estimate-icon">RS</div><div><b>Dinner reservation</b><span>Call the venue and confirm details</span></div><div class="estimate-time">3-8 min</div></article>
        </div>
        <p class="copy">These are rough processing estimates. Sold-out events, vendor holds, payment issues, and changed preferences can add time.</p>
      </section>

      <section class="section">
        <div class="section-head"><div><div class="kicker">Refunds and work rules</div><h2>Clear before the request starts.</h2></div></div>
        <div class="notice-grid">
          <article class="notice-card refund">
            <h3><img src="./pay.png" alt="">Refund policy</h3>
            <ul>
              <li>Used assistant time, completed work, and third-party ticket fees are not refundable through Kall.</li>
              <li>For Travel Lite and Wonderful, unused remaining balance can be requested for refund and is typically processed within 1 week.</li>
              <li>Travel Lite unused balance is scheduled for refund after 1 month unless you top up to extend.</li>
              <li>Wonderful unused balance is scheduled for refund after 3 months unless you top up to extend.</li>
              <li>Super time is non-refundable and is forfeited after 3 months.</li>
              <li>Ticket provider cancellation rules are separate from Kall service time.</li>
            </ul>
          </article>
          <article class="notice-card time">
            <h3><img src="./call.png" alt="">Time charged</h3>
            <ul>
              <li>Charged time includes chat clarification, research, phone calls, messaging, reports, and request troubleshooting.</li>
              <li>Not charged: idle waiting, explaining how the service works, Kall-side mistakes, lunch breaks, or closed hours.</li>
              <li>Business hours are 10 a.m. to 8 p.m. KST, Monday to Saturday.</li>
              <li>Accepted work outside regular hours may be charged at 2x the regular rate; otherwise it starts next business day.</li>
            </ul>
          </article>
        </div>
      </section>

      <section class="section">
        <div class="section-head"><div><div class="kicker">How it works</div><h2>Three steps, no Korean phone needed.</h2></div></div>
        <div class="steps">
          <article class="step-card"><div class="step-no">1</div><div><b>Send ticket details</b><span>Event name, link, date, seats, budget, and backup options.</span></div></article>
          <article class="step-card"><div class="step-no">2</div><div><b>Kall works in Korean</b><span>We check the local site, call if needed, and clarify purchase rules.</span></div></article>
          <article class="step-card"><div class="step-no">3</div><div><b>Get a result</b><span>Receive booking status, remaining time, and next steps through messenger.</span></div></article>
        </div>
      </section>
    </section>

    <section class="view" id="view-book">
      <section class="section" style="margin-top:16px;">
        <div class="section-head">
          <div>
            <div class="kicker">Ticket request</div>
            <h2>Plan first, then details.</h2>
            <p class="copy">This prototype saves the request in your browser only. Connect payment and backend later.</p>
          </div>
        </div>
        <div class="book-shell">
          <div class="progress-card" aria-label="Request progress">
            <div class="progress-step active" data-progress="1"><b>1</b><span>Plan</span></div>
            <div class="progress-step" data-progress="2"><b>2</b><span>Details</span></div>
            <div class="progress-step" data-progress="3"><b>3</b><span>Review</span></div>
          </div>

          <form class="form-card" id="bookingForm" novalidate>
            <section class="form-step active" data-step="1">
              <h2>Choose plan and ticket type</h2>
              <div class="plan-options">
                <label class="plan-option"><span><b>Travel Lite</b><span>2,000 KRW/min, 1.5 hour minimum deposit</span></span><span class="plan-price-pill">180,000 KRW</span><input type="radio" name="plan" value="lite"></label>
                <label class="plan-option"><span><b>Wonderful</b><span>1,500 KRW/min, recommended 4 hour time bank</span></span><span class="plan-price-pill">360,000 KRW</span><input type="radio" name="plan" value="wonderful" checked></label>
                <label class="plan-option"><span><b>Super</b><span>1,250 KRW/min, heavy-user 12 hour time bank</span></span><span class="plan-price-pill">900,000 KRW</span><input type="radio" name="plan" value="super"></label>
              </div>

              <div class="choice-grid" aria-label="Ticket type">
                <button class="choice selected" type="button" data-type="Baseball tickets"><b>Baseball</b><span>15-30 min estimate</span></button>
                <button class="choice" type="button" data-type="Concert tickets"><b>Concert</b><span>15-45 min estimate</span></button>
                <button class="choice" type="button" data-type="Movie tickets"><b>Movie</b><span>10-20 min estimate</span></button>
                <button class="choice" type="button" data-type="Other booking"><b>Other</b><span>Custom request</span></button>
              </div>
              <div class="form-actions">
                <button class="btn" type="button" data-next>Continue</button>
              </div>
            </section>

            <section class="form-step" data-step="2">
              <h2>Add the details we need</h2>
              <div class="field-grid">
                <div class="field"><label for="eventName">Event, venue, or business name</label><input id="eventName" name="eventName" autocomplete="off" placeholder="LG Twins vs Doosan, Jamsil Stadium" required><span class="field-help">Required</span></div>
                <div class="field"><label for="ticketLink">Ticket link or map link</label><input id="ticketLink" name="ticketLink" inputmode="url" placeholder="https://..."></div>
              </div>
              <div class="field-grid two">
                <div class="field"><label for="targetDate">Preferred date</label><input id="targetDate" name="targetDate" type="date" required><span class="field-help">Required</span></div>
                <div class="field"><label for="ticketCount">Tickets / guests</label><input id="ticketCount" name="ticketCount" type="number" min="1" max="20" value="2" required><span class="field-help">Required</span></div>
              </div>
              <div class="field-grid">
                <div class="field"><label for="seatRequest">Seat, budget, and backup options</label><textarea id="seatRequest" name="seatRequest" placeholder="2 adjacent seats. Prefer 1st base side, max 120,000 KRW total. Backup: any lower section."></textarea></div>
                <div class="field"><label for="travelerName">Name for booking</label><input id="travelerName" name="travelerName" autocomplete="name" placeholder="Alex Kim" required><span class="field-help">Required</span></div>
              </div>
              <div class="form-actions two">
                <button class="btn secondary" type="button" data-prev>Back</button>
                <button class="btn" type="button" data-next>Review</button>
              </div>
            </section>

            <section class="form-step" data-step="3">
              <h2>Review request</h2>
              <div class="field-grid two">
                <div class="field"><label for="messenger">Messenger</label><select id="messenger" name="messenger"><option>WhatsApp</option><option>KakaoTalk</option><option>LINE</option><option>WeChat</option><option>Email</option></select></div>
                <div class="field"><label for="messengerId">Messenger ID</label><input id="messengerId" name="messengerId" placeholder="+1 555 0100" required><span class="field-help">Required</span></div>
              </div>
              <div class="summary-card" aria-live="polite">
                <div class="summary-row"><span>Plan</span><b id="sumPlan">Wonderful</b></div>
                <div class="summary-row"><span>Request type</span><b id="sumType">Baseball tickets</b></div>
                <div class="summary-row"><span>Estimated working time</span><b id="sumTime">15-30 min</b></div>
                <div class="summary-row"><span>Estimated service time cost</span><b id="sumCost">22,500-45,000 KRW</b></div>
                <div class="summary-row"><span>Minimum deposit</span><b id="sumDeposit">360,000 KRW</b></div>
                <div class="summary-row"><span>Card/PayPal fee estimate</span><b id="sumFee">30,600 KRW</b></div>
                <div class="summary-total"><span>Deposit due</span><b id="sumTotal">390,600 KRW</b></div>
                <p class="estimate-footnote">Unused balance follows the selected package refund rules. Ticket vendor charges are separate.</p>
              </div>
              <div class="form-actions two">
                <button class="btn secondary" type="button" data-prev>Back</button>
                <button class="btn dark" type="button" id="createRequestBtn">Create request number</button>
              </div>
            </section>
          </form>
        </div>
      </section>
    </section>

    <section class="view" id="view-status">
      <section class="section" style="margin-top:16px;">
        <div class="section-head"><div><div class="kicker">My request</div><h2>Check your Kall ticket request.</h2></div></div>
        <div class="empty-state" id="emptyStatus">
          <div class="empty-icon"><img src="./result.png" alt=""></div>
          <h2>No request yet</h2>
          <p class="copy">Create a ticket request first. Your Kall request number will appear here.</p>
          <button class="btn" type="button" data-nav="book">Start request</button>
        </div>

        <div class="status-card" id="activeStatus" hidden>
          <div class="status-top">
            <span class="status-no" id="bookingNo">Kall #KA-0000</span>
            <span class="status-pill"><span class="live-dot"></span><span>Received</span></span>
          </div>
          <h2 id="statusMain">Your ticket request is ready for Kall.</h2>
          <p id="statusDesc">We will work in Korean and update your selected messenger.</p>
          <div class="summary-card">
            <div class="summary-row"><span>Type</span><b id="statusType">-</b></div>
            <div class="summary-row"><span>Event</span><b id="statusEvent">-</b></div>
            <div class="summary-row"><span>Date</span><b id="statusDate">-</b></div>
            <div class="summary-row"><span>Messenger</span><b id="statusMessenger">-</b></div>
            <div class="summary-row"><span>Plan</span><b id="statusPlan">-</b></div>
          </div>

          <div class="timeline">
            <div class="timeline-item done"><div class="stage-icon">1</div><div><b>Request received</b><span>Ticket details and messenger are saved locally.</span></div><div class="timeline-time">Done</div></div>
            <div class="timeline-item active"><div class="stage-icon">2</div><div><b>Korean check queued</b><span>Assistant will review the link, call, or message the venue.</span></div><div class="timeline-time">Next</div></div>
            <div class="timeline-item todo"><div class="stage-icon">3</div><div><b>Result update</b><span>Confirmation, sold-out notice, or backup options.</span></div><div class="timeline-time">Pending</div></div>
          </div>
        </div>
      </section>
    </section>
  </main>

  <nav class="bottom-nav" aria-label="Main navigation">
    <div class="nav-inner">
      <button class="nav-btn active" type="button" data-nav="intro"><svg viewBox="0 0 24 24" fill="none"><path d="M4 11.5 12 4l8 7.5V20H5v-8.5Z" stroke="currentColor" stroke-width="2.1" stroke-linejoin="round"/><path d="M10 20v-5h4v5" stroke="currentColor" stroke-width="2.1" stroke-linejoin="round"/></svg><span>Home</span></button>
      <button class="nav-btn" type="button" data-nav="book"><svg viewBox="0 0 24 24" fill="none"><path d="M6 4h12v16H6z" stroke="currentColor" stroke-width="2.1"/><path d="M9 8h6M9 12h6M9 16h4" stroke="currentColor" stroke-width="2.1" stroke-linecap="round"/></svg><span>Request</span></button>
      <button class="nav-btn" type="button" data-nav="status"><svg viewBox="0 0 24 24" fill="none"><path d="M5 12.5 10 17 19 7" stroke="currentColor" stroke-width="2.5" stroke-linecap="round"/><path d="M21 12a9 9 0 1 1-4.1-7.6" stroke="currentColor" stroke-width="2.1" stroke-linecap="round"/></svg><span>Status</span></button>
    </div>
  </nav>

  <div class="toast" id="toast" role="status" aria-live="polite"></div>

  <script>
    const plans = {
      lite: { name: "Travel Lite", rate: 2000, deposit: 180000, refund: "1 month" },
      wonderful: { name: "Wonderful", rate: 1500, deposit: 360000, refund: "3 months" },
      super: { name: "Super", rate: 1250, deposit: 900000, refund: "non-refundable" }
    };

    const timeRanges = {
      "Baseball tickets": [15, 30],
      "Concert tickets": [15, 45],
      "Movie tickets": [10, 20],
      "Other booking": [15, 35]
    };

    const $ = (selector, root = document) => root.querySelector(selector);
    const $$ = (selector, root = document) => [...root.querySelectorAll(selector)];

    const state = {
      view: "intro",
      step: 1,
      type: "Baseball tickets",
      booking: JSON.parse(localStorage.getItem("kallTicketRequest") || "null")
    };

    function money(value) {
      return `${Math.round(value).toLocaleString("en-US")} KRW`;
    }

    function selectedPlan() {
      return $("input[name='plan']:checked")?.value || "wonderful";
    }

    function selectedPlanData() {
      return plans[selectedPlan()];
    }

    function selectedRange() {
      return timeRanges[state.type] || timeRanges["Other booking"];
    }

    function showToast(message) {
      const toast = $("#toast");
      toast.textContent = message;
      toast.classList.add("show");
      clearTimeout(showToast.timer);
      showToast.timer = setTimeout(() => toast.classList.remove("show"), 2200);
    }

    function navigate(view) {
      state.view = view;
      $$(".view").forEach((item) => item.classList.toggle("active", item.id === `view-${view}`));
      $$("[data-nav]").forEach((item) => {
        if (item.classList.contains("nav-btn")) item.classList.toggle("active", item.dataset.nav === view);
      });
      window.scrollTo({ top: 0, behavior: "smooth" });
      renderStatus();
    }

    function setStep(step) {
      state.step = Math.max(1, Math.min(3, step));
      $$(".form-step").forEach((item) => item.classList.toggle("active", Number(item.dataset.step) === state.step));
      $$("[data-progress]").forEach((item) => item.classList.toggle("active", Number(item.dataset.progress) === state.step));
      updateSummary();
    }

    function markField(field, invalid) {
      field.closest(".field")?.classList.toggle("invalid", invalid);
    }

    function validateStep() {
      let valid = true;
      $$(`.form-step[data-step="${state.step}"] [required]`).forEach((field) => {
        const invalid = !String(field.value || "").trim();
        markField(field, invalid);
        if (invalid) valid = false;
      });
      if (!valid) showToast("Please complete the required fields.");
      return valid;
    }

    function updatePlanCards() {
      const plan = selectedPlan();
      $$(".price-card[data-plan-card]").forEach((card) => card.classList.toggle("selected", card.dataset.planCard === plan));
    }

    function updateSummary() {
      const plan = selectedPlanData();
      const [min, max] = selectedRange();
      const minCost = min * plan.rate;
      const maxCost = max * plan.rate;
      const fee = plan.deposit * 0.085;
      const total = plan.deposit + fee;

      $("#sumPlan").textContent = plan.name;
      $("#sumType").textContent = state.type;
      $("#sumTime").textContent = `${min}-${max} min`;
      $("#sumCost").textContent = `${money(minCost)}-${money(maxCost)}`;
      $("#sumDeposit").textContent = money(plan.deposit);
      $("#sumFee").textContent = money(fee);
      $("#sumTotal").textContent = money(total);
      $("#chipPrice").textContent = `From ${money(plans.super.rate).replace(" KRW", "")} KRW/min`;
      updatePlanCards();
    }

    function generateBookingNumber() {
      const now = new Date();
      const yy = String(now.getFullYear()).slice(-2);
      const mm = String(now.getMonth() + 1).padStart(2, "0");
      const dd = String(now.getDate()).padStart(2, "0");
      const rand = Math.floor(1000 + Math.random() * 9000);
      return `KA-${yy}${mm}${dd}-${rand}`;
    }

    function formData() {
      const plan = selectedPlanData();
      const eventName = $("#eventName").value.trim();
      const targetDate = $("#targetDate").value;
      const messenger = $("#messenger").value;
      const messengerId = $("#messengerId").value.trim();
      return {
        bookingNo: generateBookingNumber(),
        type: state.type,
        plan: plan.name,
        deposit: plan.deposit,
        eventName,
        targetDate,
        messenger,
        messengerId,
        createdAt: new Date().toISOString()
      };
    }

    function createRequest() {
      if (!validateStep()) return;
      state.booking = formData();
      localStorage.setItem("kallTicketRequest", JSON.stringify(state.booking));
      renderStatus();
      navigate("status");
      showToast(`Request created: ${state.booking.bookingNo}`);
    }

    function renderStatus() {
      const booking = state.booking;
      $("#emptyStatus").hidden = Boolean(booking);
      $("#activeStatus").hidden = !booking;
      if (!booking) return;
      $("#bookingNo").textContent = `Kall #${booking.bookingNo}`;
      $("#statusMain").textContent = `${booking.eventName || "Ticket request"} - ${booking.plan}`;
      $("#statusDesc").textContent = `We will update ${booking.messenger} at ${booking.messengerId}.`;
      $("#statusType").textContent = booking.type;
      $("#statusEvent").textContent = booking.eventName || "-";
      $("#statusDate").textContent = booking.targetDate || "-";
      $("#statusMessenger").textContent = `${booking.messenger} - ${booking.messengerId}`;
      $("#statusPlan").textContent = `${booking.plan} - ${money(booking.deposit)} deposit`;
    }

    $$("[data-nav]").forEach((button) => button.addEventListener("click", (event) => {
      event.preventDefault();
      navigate(button.dataset.nav);
    }));

    $$("[data-next]").forEach((button) => button.addEventListener("click", () => {
      if (validateStep()) setStep(state.step + 1);
    }));
    $$("[data-prev]").forEach((button) => button.addEventListener("click", () => setStep(state.step - 1)));

    $$(".choice").forEach((button) => button.addEventListener("click", () => {
      state.type = button.dataset.type;
      $$(".choice").forEach((item) => item.classList.remove("selected"));
      button.classList.add("selected");
      updateSummary();
    }));

    $$("input[name='plan']").forEach((input) => input.addEventListener("change", updateSummary));
    $$("[data-plan-card]").forEach((card) => {
      card.addEventListener("click", () => {
        const input = $(`input[name='plan'][value='${card.dataset.planCard}']`);
        if (input) {
          input.checked = true;
          updateSummary();
          navigate("book");
        }
      });
      card.addEventListener("keydown", (event) => {
        if (event.key === "Enter" || event.key === " ") {
          event.preventDefault();
          card.click();
        }
      });
    });

    $$("input, select, textarea").forEach((field) => {
      field.addEventListener("input", () => {
        markField(field, false);
        updateSummary();
      });
      field.addEventListener("change", () => {
        markField(field, false);
        updateSummary();
      });
    });

    $("#createRequestBtn").addEventListener("click", createRequest);

    const today = new Date();
    today.setHours(0, 0, 0, 0);
    $("#targetDate").min = today.toISOString().slice(0, 10);

    updateSummary();
    renderStatus();
  </script>
</body>
</html>
