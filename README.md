<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MonedaViva · Casa Moneda de Chile</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  /* Paleta azul marino + blanco + dorado acento */
  --navy:       #0B1F3A;
  --navy2:      #122847;
  --navy3:      #1A3A5C;
  --navy4:      #234E75;
  --navy-light: #2E6DA4;
  --white:      #FFFFFF;
  --off-white:  #F4F7FB;
  --soft:       #E8EEF6;
  --soft2:      #D4E1F0;
  --gold:       #C9A84C;
  --gold-lt:    #E2C06A;
  --gold-dk:    #9A7530;
  --text:       #0B1F3A;
  --text2:      #3A5070;
  --text3:      #6B87A8;
  --border:      rgba(11,31,58,0.10);
  --border2:     rgba(11,31,58,0.20);
  --radius:      10px;
  --radius-lg:  16px;
  --green-bg:#EAF3DE;--green-text:#2E6B0F;--green-border:#8CBF50;
  --amber-bg:#FEF3DC;--amber-text:#7A5200;--amber-border:#E8B84B;
  --red-bg:#FDECEA;  --red-text:#9B2020;  --red-border:#E57373;
}
html{scroll-behavior:smooth}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Helvetica,sans-serif;background:var(--off-white);color:var(--text);line-height:1.65}
a{color:inherit;text-decoration:none}

/* ── NAV ── */
.site-header{background:var(--navy);position:sticky;top:0;z-index:100;border-bottom:3px solid var(--gold)}
.nav-inner{max-width:1140px;margin:0 auto;padding:0 1.5rem;display:flex;align-items:center;justify-content:space-between;height:66px}
.logo-wrap{display:flex;align-items:center;gap:13px}
.logo-coin{width:40px;height:40px;border-radius:50%;background:radial-gradient(circle at 35% 35%,#F7E48A,var(--gold) 55%,#7A5800);border:2px solid var(--gold-lt);flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:800;color:#3A2800;text-align:center;line-height:1.2}
.logo-text strong{display:block;font-size:18px;font-weight:800;color:var(--white);letter-spacing:-.01em}
.logo-text span{font-size:10px;color:var(--gold-lt);letter-spacing:.1em;text-transform:uppercase}
.nav-links{display:flex;align-items:center;gap:2rem}
.nav-links a{font-size:13px;color:rgba(255,255,255,0.65);transition:color .15s;font-weight:500}
.nav-links a:hover{color:var(--gold-lt)}
.nav-cta{background:var(--gold);color:var(--navy)!important;font-weight:700!important;padding:8px 18px;border-radius:var(--radius);font-size:13px!important;transition:background .15s!important;border:none}
.nav-cta:hover{background:var(--gold-lt)!important}
@media(max-width:720px){.nav-links{display:none}}

/* ── HERO ── */
.hero{background:var(--navy);padding:5rem 1.5rem 0;text-align:center;position:relative;overflow:hidden}
.hero::after{content:'';display:block;height:60px;background:linear-gradient(to bottom right,var(--navy) 50%,var(--off-white) 50%)}
.hero-eyebrow{display:inline-flex;align-items:center;gap:7px;font-size:11px;color:var(--gold-lt);text-transform:uppercase;letter-spacing:.14em;border:1px solid rgba(201,168,76,0.35);border-radius:20px;padding:5px 14px;margin-bottom:1.75rem}
.hero-dot{width:7px;height:7px;border-radius:50%;background:#4CAF50;animation:pulse 1.6s infinite}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(.85)}}
.hero h1{font-size:clamp(2.2rem,5vw,3.8rem);font-weight:800;color:var(--white);line-height:1.1;margin-bottom:1.1rem;letter-spacing:-.02em}
.hero h1 em{color:var(--gold-lt);font-style:normal}
.hero-sub{font-size:18px;color:rgba(255,255,255,0.58);max-width:560px;margin:0 auto 2.5rem;line-height:1.75}
.hero-actions{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;margin-bottom:4rem}
.btn-primary{background:var(--gold);color:var(--navy);font-weight:800;padding:14px 30px;border-radius:var(--radius);font-size:15px;border:none;cursor:pointer;transition:background .15s;display:inline-block}
.btn-primary:hover{background:var(--gold-lt)}
.btn-ghost{background:transparent;color:rgba(255,255,255,0.7);font-weight:500;padding:14px 30px;border-radius:var(--radius);font-size:15px;border:1.5px solid rgba(255,255,255,0.2);cursor:pointer;transition:all .15s;display:inline-block}
.btn-ghost:hover{border-color:var(--gold-lt);color:var(--gold-lt)}

/* Monedas hero */
.hero-coins{display:flex;align-items:flex-end;justify-content:center;gap:1.5rem;margin-bottom:0}
.hcoin{border-radius:50%;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800);border:2.5px solid var(--gold-lt);display:flex;align-items:center;justify-content:center;font-weight:800;color:#3A2800;text-align:center;line-height:1.3;flex-shrink:0;box-shadow:0 4px 20px rgba(0,0,0,0.3)}
.hcoin-lg{width:120px;height:120px;font-size:12px;animation:float 3.2s ease-in-out infinite}
.hcoin-md{width:84px;height:84px;font-size:10px;animation:float 3.6s ease-in-out infinite .5s;opacity:.9}
.hcoin-sm{width:62px;height:62px;font-size:9px;animation:float 2.9s ease-in-out infinite 1s;opacity:.75}
@keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-10px)}}

/* ── STATS ── */
.stats-bar{background:var(--navy2);border-bottom:1px solid var(--navy3);padding:1.5rem}
.stats-inner{max-width:1140px;margin:0 auto;display:flex;align-items:center;justify-content:space-around;gap:1rem;flex-wrap:wrap}
.stat-item{text-align:center}
.stat-num{font-size:24px;font-weight:800;color:var(--gold-lt)}
.stat-lbl{font-size:10px;color:rgba(255,255,255,0.45);text-transform:uppercase;letter-spacing:.08em;margin-top:3px}

/* ── SECCIONES ── */
section{padding:5.5rem 1.5rem}
.sec-inner{max-width:1140px;margin:0 auto}
.eyebrow{font-size:11px;text-transform:uppercase;letter-spacing:.12em;color:var(--navy-light);font-weight:700;margin-bottom:.6rem}
.sec-title{font-size:clamp(1.7rem,3vw,2.5rem);font-weight:800;color:var(--navy);margin-bottom:1rem;line-height:1.15;letter-spacing:-.02em}
.sec-sub{font-size:16px;color:var(--text2);max-width:580px;line-height:1.75}

/* ── CÓMO FUNCIONA ── */
.how-sec{background:var(--white)}
.steps-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:1.5rem;margin-top:3rem}
.step-card{background:var(--off-white);border:1.5px solid var(--soft2);border-radius:var(--radius-lg);padding:1.75rem;position:relative}
.step-num{width:38px;height:38px;border-radius:50%;background:var(--navy);color:var(--gold-lt);font-size:15px;font-weight:800;display:flex;align-items:center;justify-content:center;margin-bottom:1.1rem}
.step-card h3{font-size:15px;font-weight:700;color:var(--navy);margin-bottom:.5rem}
.step-card p{font-size:13px;color:var(--text2);line-height:1.65}

/* ── PRODUCTOS ── */
.prod-sec{background:var(--off-white)}
.prod-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:1.25rem;margin-top:2.5rem}
.prod-card{background:var(--white);border:1.5px solid var(--soft2);border-radius:var(--radius-lg);overflow:hidden;transition:transform .2s,box-shadow .2s;cursor:pointer}
.prod-card:hover{transform:translateY(-4px);box-shadow:0 12px 32px rgba(11,31,58,0.12)}
.prod-img{height:165px;background:var(--soft);display:flex;align-items:center;justify-content:center;position:relative}
.prod-coin{border-radius:50%;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800);border:2px solid var(--gold-lt);display:flex;align-items:center;justify-content:center;font-weight:800;color:#3A2800;text-align:center;line-height:1.3}
.prod-tag{position:absolute;top:10px;right:10px;font-size:10px;padding:3px 9px;border-radius:20px;font-weight:700}
.tag-cert{background:var(--green-bg);color:var(--green-text);border:1px solid var(--green-border)}
.tag-new{background:#E6F1FB;color:#0C447C;border:1px solid #85B7EB}
.tag-hot{background:var(--amber-bg);color:var(--amber-text);border:1px solid var(--amber-border)}
.prod-info{padding:1.1rem}
.prod-info h3{font-size:14px;font-weight:700;color:var(--navy);margin-bottom:4px}
.prod-info p{font-size:12px;color:var(--text3);margin-bottom:.8rem}
.prod-footer{display:flex;align-items:center;justify-content:space-between}
.prod-price{font-size:17px;font-weight:800;color:var(--navy)}
.prod-price span{font-size:11px;color:var(--text3);font-weight:400}
.btn-ver{font-size:12px;font-weight:700;color:var(--navy-light);border:1.5px solid var(--soft2);background:transparent;border-radius:var(--radius);padding:6px 13px;cursor:pointer;transition:all .15s}
.btn-ver:hover{background:var(--navy);color:var(--white);border-color:var(--navy)}

/* ── DEMO ── */
.demo-sec{background:var(--navy);padding:5.5rem 1.5rem}
.demo-inner{max-width:1140px;margin:0 auto;display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:center}
@media(max-width:760px){.demo-inner{grid-template-columns:1fr}}
.demo-eyebrow{font-size:11px;text-transform:uppercase;letter-spacing:.12em;color:var(--gold-lt);font-weight:700;margin-bottom:.6rem}
.demo-title{font-size:clamp(1.7rem,3vw,2.5rem);font-weight:800;color:var(--white);line-height:1.15;letter-spacing:-.02em;margin-bottom:1rem}
.demo-sub{font-size:16px;color:rgba(255,255,255,0.55);line-height:1.75;margin-bottom:2rem}
.demo-bullets{display:flex;flex-direction:column;gap:.85rem;margin-bottom:2rem}
.demo-bullet{display:flex;align-items:flex-start;gap:10px;font-size:14px;color:rgba(255,255,255,0.7)}
.bicon{width:22px;height:22px;border-radius:50%;background:rgba(201,168,76,0.18);border:1.5px solid rgba(201,168,76,0.4);flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:11px;color:var(--gold-lt);margin-top:1px}
.btn-demo{background:var(--gold);color:var(--navy);font-weight:800;padding:13px 26px;border-radius:var(--radius);font-size:14px;border:none;cursor:pointer;transition:background .15s}
.btn-demo:hover{background:var(--gold-lt)}

/* ── BENEFICIOS ── */
.ben-sec{background:var(--off-white)}
.ben-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:1.25rem;margin-top:2.5rem}
.ben-card{background:var(--white);border:1.5px solid var(--soft2);border-radius:var(--radius-lg);padding:1.6rem}
.ben-icon{width:46px;height:46px;border-radius:12px;background:var(--navy);display:flex;align-items:center;justify-content:center;font-size:22px;margin-bottom:1.1rem}
.ben-card h3{font-size:15px;font-weight:700;color:var(--navy);margin-bottom:.5rem}
.ben-card p{font-size:13px;color:var(--text2);line-height:1.65}
.ben-num{font-size:24px;font-weight:900;color:var(--navy);margin-top:.85rem}
.ben-num-lbl{font-size:11px;color:var(--text3)}

/* ── CTA ── */
.cta-sec{background:var(--navy2);border-top:3px solid var(--gold);padding:5rem 1.5rem;text-align:center}
.cta-sec h2{font-size:clamp(1.7rem,3vw,2.5rem);font-weight:800;color:var(--white);margin-bottom:1rem;letter-spacing:-.02em}
.cta-sec p{font-size:16px;color:rgba(255,255,255,0.55);max-width:500px;margin:0 auto 2rem}
.cta-actions{display:flex;gap:12px;justify-content:center;flex-wrap:wrap}

/* ── FOOTER ── */
.site-footer{background:var(--navy);border-top:1px solid var(--navy3);padding:2.5rem 1.5rem}
.footer-inner{max-width:1140px;margin:0 auto;display:flex;align-items:center;justify-content:space-between;gap:1rem;flex-wrap:wrap}
.footer-logo{font-size:19px;font-weight:800;color:var(--gold-lt)}
.footer-copy{font-size:11px;color:rgba(255,255,255,0.3);margin-top:.3rem}
.footer-links{display:flex;gap:1.5rem;flex-wrap:wrap}
.footer-links a{font-size:12px;color:rgba(255,255,255,0.4);transition:color .15s}
.footer-links a:hover{color:var(--gold-lt)}

/* ── MODAL DE PROTOTIPO ── */
.modal-overlay{display:none;position:fixed;inset:0;z-index:200;background:rgba(5,15,30,0.88);align-items:flex-start;justify-content:center;padding:2rem 1rem;overflow-y:auto}
.modal-overlay.open{display:flex}
.modal-box{background:var(--white);border-radius:var(--radius-lg);width:100%;max-width:500px;max-height:92vh;overflow-y:auto;border:1.5px solid var(--soft2);margin:auto;box-shadow:0 24px 80px rgba(0,0,0,0.3)}

.proto-screen{display:none}
.proto-screen.active{display:block;animation:fadeUp .2s ease}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}

.m-head{background:var(--navy);padding:1rem 1.25rem;display:flex;align-items:center;justify-content:space-between;border-radius:var(--radius-lg) var(--radius-lg) 0 0}
.m-badge{display:flex;align-items:center;gap:7px;font-size:11px;color:var(--gold-lt);text-transform:uppercase;letter-spacing:.09em;font-weight:700}
.live-dot{width:7px;height:7px;border-radius:50%;background:#4CAF50;animation:pulse 1.6s infinite}
.m-close{background:none;border:none;color:rgba(255,255,255,0.45);font-size:20px;cursor:pointer;line-height:1;transition:color .15s}
.m-close:hover{color:var(--white)}

.cert-body{padding:1.35rem}
.coin-row{display:flex;gap:1.1rem;align-items:flex-start;margin-bottom:1.2rem}
.cert-vis{width:72px;height:72px;border-radius:50%;flex-shrink:0;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800);border:2.5px solid var(--gold-lt);display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:800;color:#3A2800;text-align:center;line-height:1.3}
.cert-info h2{font-size:15px;font-weight:700;color:var(--navy);margin-bottom:4px}
.cert-info p{font-size:12px;color:var(--text2);margin-bottom:7px}
.tag-auth{display:inline-flex;align-items:center;gap:4px;font-size:10px;font-weight:700;padding:3px 10px;border-radius:20px;background:var(--green-bg);color:var(--green-text);border:1px solid var(--green-border)}
.divider{border:none;border-top:1.5px solid var(--soft);margin:.85rem 0}
.dgrid{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-bottom:1rem}
.dcell{background:var(--off-white);border-radius:var(--radius);padding:9px 11px;border:1px solid var(--soft2)}
.dcell .l{font-size:9px;color:var(--text3);text-transform:uppercase;letter-spacing:.07em;margin-bottom:3px;font-weight:600}
.dcell .v{font-size:12px;font-weight:600;color:var(--navy)}

.cert-foot{display:flex;gap:8px;padding:1rem 1.25rem;background:var(--off-white);border-top:1.5px solid var(--soft2);flex-wrap:wrap;border-radius:0 0 var(--radius-lg) var(--radius-lg)}
.btn-sm{flex:1;min-width:100px;padding:9px 10px;border-radius:var(--radius);border:1.5px solid var(--soft2);background:var(--white);font-size:12px;font-weight:600;cursor:pointer;color:var(--text2);text-align:center;transition:all .15s}
.btn-sm:hover{border-color:var(--navy);color:var(--navy)}
.btn-navy{flex:1;min-width:130px;padding:9px 10px;border-radius:var(--radius);border:none;background:var(--navy);font-size:12px;font-weight:700;cursor:pointer;color:var(--gold-lt);text-align:center;transition:opacity .15s}
.btn-navy:hover{opacity:.85}

/* PANTALLA PAGO & MÉTODOS */
.f-lbl{font-size:10px;text-transform:uppercase;letter-spacing:.07em;color:var(--text2);font-weight:600;display:block;margin-bottom:5px}
.f-inp{width:100%;padding:10px 12px;border-radius:var(--radius);border:1.5px solid var(--soft2);background:var(--white);color:var(--navy);font-size:13px;font-weight:500;margin-bottom:1rem;transition:border-color .15s}
.mtabs{display:flex;gap:6px;margin-bottom:1.25rem}
.mtab{flex:1;padding:10px 5px;border-radius:var(--radius);border:1.5px solid var(--soft2);background:var(--off-white);font-size:11px;font-weight:700;cursor:pointer;color:var(--text2);text-align:center;transition:all .15s}
.mtab.active{border-color:var(--navy);background:var(--navy);color:var(--gold-lt)}
.method-desc{font-size:11px;color:var(--text3);margin-top:-8px;margin-bottom:15px;display:none}
.method-desc.active{display:block}

.btn-confirm{width:100%;padding:12px;border-radius:var(--radius);background:var(--navy);color:var(--gold-lt);border:none;font-size:14px;font-weight:800;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:7px}

/* PROCESANDO */
.proc-wrap{padding:3rem 1.25rem;text-align:center}
.spinner{width:46px;height:46px;border:3.5px solid var(--soft2);border-top-color:var(--navy);border-radius:50%;margin:0 auto 1.4rem;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}

/* ÉXITO & PDF */
.ok-wrap{padding:2.5rem 1.5rem;text-align:center}
.ok-circle{width:62px;height:62px;border-radius:50%;background:var(--green-bg);border:2px solid var(--green-border);margin:0 auto 1.25rem;display:flex;align-items:center;justify-content:center}
.ok-circle svg{width:28px;height:28px;stroke:var(--green-text);fill:none;stroke-width:2.5}
.ok-folio{font-family:monospace;font-size:11px;color:var(--text3);background:var(--off-white);padding:8px 12px;border-radius:var(--radius);border:1.5px solid var(--soft2);margin:.9rem auto;max-width:310px}
.btn-pdf{display:inline-flex;align-items:center;gap:7px;padding:12px 24px;border-radius:var(--radius);border:2px solid var(--navy);background:var(--navy);font-size:14px;font-weight:800;cursor:pointer;color:var(--gold-lt);margin-top:1.5rem;transition:all .15s}
.btn-pdf:hover{background:var(--navy2)}

/* Toast */
.pdf-toast{position:fixed;bottom:2rem;left:50%;transform:translateX(-50%);background:var(--navy);color:var(--gold-lt);border:1.5px solid var(--navy3);padding:10px 20px;border-radius:var(--radius);font-size:13px;font-weight:600;z-index:999;opacity:0;transition:opacity .3s;pointer-events:none}
.pdf-toast.show{opacity:1}
</style>
</head>
<body>

<header class="site-header">
  <div class="nav-inner">
    <div class="logo-wrap">
      <div class="logo-coin">MV<br>&#x20B1;</div>
      <div class="logo-text">
        <strong>MonedaViva</strong>
        <span>Casa Moneda de Chile</span>
      </div>
    </div>
    <nav class="nav-links">
      <a href="#como-funciona">Como funciona</a>
      <a href="#productos">Coleccion</a>
      <a href="#beneficios">Beneficios</a>
      <a href="#demo" class="nav-cta">Ver prototipo</a>
    </nav>
  </div>
</header>

<section class="hero" id="inicio">
  <div class="hero-eyebrow"><div class="hero-dot"></div>Innovacion · Design Thinking · Transformacion Digital</div>
  <h1>Cada moneda tiene historia.<br><em>Ahora tambien tiene futuro.</em></h1>
  <p class="hero-sub">MonedaViva convierte cada pieza de Casa Moneda en un activo verificable con certificado PDF oficial y pagos integrados.</p>
  <div class="hero-actions">
    <button class="btn-primary" onclick="openPrototype('Moneda Bicentenario 2010', '$38.500', '#MV-2010-8841X')">Ver prototipo en vivo</button>
    <a href="#como-funciona" class="btn-ghost">Como funciona &darr;</a>
  </div>
  <div class="hero-coins" aria-hidden="true">
    <div class="hcoin hcoin-sm">$100<br>1998</div>
    <div class="hcoin hcoin-md">$200<br>2010</div>
    <div class="hcoin hcoin-lg">Bicentenario<br>$500<br>Chile</div>
    <div class="hcoin hcoin-md">Oro<br>999,9</div>
    <div class="hcoin hcoin-sm">Medalla<br>Bronce</div>
  </div>
</section>

<div class="stats-bar">
  <div class="stats-inner">
    <div class="stat-item"><div class="stat-num">+280</div><div class="stat-lbl">Anos de historia</div></div>
    <div class="stat-item"><div class="stat-num">50.000</div><div class="stat-lbl">Unidades por edicion</div></div>
    <div class="stat-item"><div class="stat-num">2%</div><div class="stat-lbl">Ingreso por reventa</div></div>
    <div class="stat-item"><div class="stat-num">PDF</div><div class="stat-lbl">Certificado oficial</div></div>
    <div class="stat-item"><div class="stat-num">24 hrs</div><div class="stat-lbl">Pago en tu cuenta</div></div>
  </div>
</div>

<section class="how-sec" id="como-funciona">
  <div class="sec-inner">
    <p class="eyebrow">El proceso</p>
    <h2 class="sec-title">Del QR al certificado PDF en cuatro pasos</h2>
    <p class="sec-sub">Cada pieza de Casa Moneda sale con un QR unico grabado. La venta genera el certificado oficial automaticamente.</p>
    <div class="steps-grid">
      <div class="step-card">
        <div class="step-num">1</div>
        <h3>Compra en tienda</h3>
        <p>Adquieres tu moneda o medalla en <strong>tienda.casamoneda.cl</strong>. El proceso de compra no cambia en absoluto.</p>
      </div>
      <div class="step-card">
        <div class="step-num">2</div>
        <h3>Escanea el QR</h3>
        <p>Cada pieza lleva un QR unico grabado. Lo escaneas con la camara del celular para ver el historial y autenticidad oficial.</p>
      </div>
      <div class="step-card">
        <div class="step-num">3</div>
        <h3>Vende Seguro</h3>
        <p>El cobro al comprador se procesa via <strong>Transbank / Transferencia / MACH</strong>. Todo integrado en la app.</p>
      </div>
      <div class="step-card">
        <div class="step-num">4</div>
        <h3>Descarga tu certificado PDF</h3>
        <p>Solo tras confirmar la venta, el sistema genera el <strong>certificado PDF oficial</strong> con el nuevo propietario registrado.</p>
      </div>
    </div>
  </div>
</section>

<section class="prod-sec" id="productos">
  <div class="sec-inner">
    <p class="eyebrow">Coleccion certificada</p>
    <h2 class="sec-title">Piezas con certificado MonedaViva</h2>
    <p class="sec-sub">Elige cualquiera de los siguientes activos reales para simular el proceso comercial y emitir su respectivo PDF.</p>
    <div class="prod-grid">
      
      <div class="prod-card" onclick="openPrototype('Moneda Bicentenario 2010', '$38.500', '#MV-2010-8841X')">
        <div class="prod-img">
          <div class="prod-coin" style="width:90px;height:90px;font-size:11px">Chile<br>$200<br>2010</div>
          <span class="prod-tag tag-cert">Certificada</span>
        </div>
        <div class="prod-info">
          <h3>Moneda Bicentenario 2010</h3>
          <p>Cobre-Niquel · Edicion limitada 50.000 uds.</p>
          <div class="prod-footer">
            <div class="prod-price">$38.500 <span>CLP</span></div>
            <button class="btn-ver">Ver y vender</button>
          </div>
        </div>
      </div>

      <div class="prod-card" onclick="openPrototype('Medalla Bronce Manuel Bulnes', '$33.990', '#MV-1841-B992')">
        <div class="prod-img">
          <div class="prod-coin" style="width:90px;height:90px;font-size:10px">Bulnes<br>Bronce<br>1841</div>
          <span class="prod-tag tag-new">Nuevo</span>
        </div>
        <div class="prod-info">
          <h3>Medalla Bronce · Manuel Bulnes</h3>
          <p>Serie Presidencial · Pieza historica coleccionable</p>
          <div class="prod-footer">
            <div class="prod-price">$33.990 <span>CLP</span></div>
            <button class="btn-ver">Ver y vender</button>
          </div>
        </div>
      </div>

      <div class="prod-card" onclick="openPrototype('Barra de Oro 1 oz 999,9', '$3.200.000', '#MV-ORO-7712')">
        <div class="prod-img" style="background:linear-gradient(135deg,#FEF9EC,#F0DC8A)">
          <div class="prod-coin" style="width:90px;height:90px;font-size:10px;background:radial-gradient(circle at 35% 35%,#FFF5CC,#D4A017 50%,#8A6700);border-color:#FFD700">Oro<br>999,9<br>1 oz</div>
          <span class="prod-tag tag-hot">Alta demanda</span>
        </div>
        <div class="prod-info">
          <h3>Barra de Oro 1 oz · 999,9</h3>
          <p>Oro fino certificado · Instrumento de inversion</p>
          <div class="prod-footer">
            <div class="prod-price">$3.200.000 <span>CLP</span></div>
            <button class="btn-ver">Ver y vender</button>
          </div>
        </div>
      </div>

      <div class="prod-card" onclick="openPrototype('Billete Conmemorativo Neruda 2026', '$42.980', '#MV-NERU-2026')">
        <div class="prod-img" style="background: #EAF2F8;">
          <div style="width:120px; height:70px; background:linear-gradient(to right, #A9DFBF, #AED6F1); border:1.5px solid #2E86C1; border-radius:4px; display:flex; flex-direction:column; justify-content:space-between; padding:5px; font-size:9px; color:#1B4F72; font-weight:bold;">
            <div style="display:flex; justify-content:space-between;"><span>2026</span><span>$5000</span></div>
            <div style="text-align:center; font-size:10px;">Neruda</div>
            <div style="font-size:7px; letter-spacing:1px">CASA MONEDA CHILE</div>
          </div>
          <span class="prod-tag tag-new">Nuevo</span>
        </div>
        <div class="prod-info">
          <h3>Billete Conmemorativo Neruda</h3>
          <p>Edicion especial 2026 · Polímero de Alta Seguridad</p>
          <div class="prod-footer">
            <div class="prod-price">$42.980 <span>CLP</span></div>
            <button class="btn-ver">Ver y vender</button>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>

<section class="demo-sec" id="demo">
  <div class="demo-inner">
    <div class="demo-text">
      <p class="demo-eyebrow">Prototipo en vivo</p>
      <h2 class="demo-title">Vende tu activo. Recibe el PDF oficial al final.</h2>
      <p class="demo-sub">El certificado de propiedad no se entrega al aire; se acuña digitalmente vinculando al nuevo comprador mediante pasarelas robustas chilenas.</p>
      <button class="btn-demo" onclick="openPrototype('Moneda Bicentenario 2010', '$38.500', '#MV-2010-8841X')">Abrir prototipo interactivo &rarr;</button>
    </div>
  </div>
</section>

<section class="ben-sec" id="beneficios">
  <div class="sec-inner">
    <p class="eyebrow">Por que elegirnos</p>
    <h2 class="sec-title">La evolucion de la seguridad numismatica</h2>
    <p class="sec-sub">Combinamos la centenaria tradición de acuñación física con la inmutabilidad de los registros digitales modernos.</p>
    <div class="ben-grid">
      <div class="ben-card">
        <div class="ben-icon">🔒</div>
        <h3>Autenticidad Criptográfica</h3>
        <p>Cada QR grabado es único e imposible de clonar. Vincula la pieza física directamente con la base de datos central de Casa Moneda.</p>
      </div>
      <div class="ben-card">
        <div class="ben-icon">📈</div>
        <h3>Mercado Secundario Líquido</h3>
        <p>Vende tus coleccionables desde cualquier lugar del país con liquidación inmediata directo a tus cuentas bancarias chilenas.</p>
      </div>
      <div class="ben-card">
        <div class="ben-icon">💰</div>
        <h3>Regalías de Reventa</h3>
        <p>Casa Moneda percibe un 2% de comisión automatizada por cada reventa, garantizando el financiamiento de futuros diseños artísticos.</p>
      </div>
    </div>
  </div>
</section>

<section class="cta-sec">
  <h2>¿Listo para digitalizar tu colección?</h2>
  <p>Accede de forma anticipada a la transformación del mercado numismático en Chile.</p>
  <button class="btn-primary" onclick="openPrototype('Moneda Bicentenario 2010', '$38.500', '#MV-2010-8841X')">Probar Sistema Ahora</button>
</section>

<footer class="site-footer">
  <div class="footer-inner">
    <div>
      <div class="footer-logo">MonedaViva</div>
      <div class="footer-copy">© 2026 Casa Moneda de Chile S.A. Todos los derechos reservados.</div>
    </div>
  </div>
</footer>

<div class="modal-overlay" id="modalPrototype">
  <div class="modal-box">
    
    <div class="proto-screen active" id="screenDetail">
      <div class="m-head">
        <div class="m-badge"><div class="live-dot"></div> MonedaViva Certificados</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="cert-body">
        <div class="coin-row">
          <div class="cert-vis" id="modalAssetVisual">Chile<br>$200<br>2010</div>
          <div class="cert-info">
            <h2 id="modalAssetName">Moneda Bicentenario 2010</h2>
            <p>ID Pieza: <span id="modalAssetId" style="font-weight:bold;">#MV-2010-8841X</span></p>
            <span class="tag-auth">✓ Original Casa Moneda</span>
          </div>
        </div>
        <div class="divider"></div>
        <div class="dgrid">
          <div class="dcell"><div class="l">Tipo Activo</div><div class="v" id="modalAssetType">Numismático Oficial</div></div>
          <div class="dcell"><div class="l">Custodia</div><div class="v">Titular Particular</div></div>
          <div class="dcell"><div class="l">Propietario Actual</div><div class="v">Carlos Mendoza</div></div>
          <div class="dcell"><div class="l">Estado Reg.</div><div class="v">Listo para Transferir</div></div>
        </div>
      </div>
      <div class="cert-foot">
        <button class="btn-sm" onclick="closeModal()">Cerrar</button>
        <button class="btn-navy" onclick="changeScreen('screenPayment')">Iniciar Venta (<span id="modalAssetPrice">$38.500</span>)</button>
      </div>
    </div>

    <div class="proto-screen" id="screenPayment">
      <div class="m-head">
        <div class="m-badge">Formulario de Transferencia</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="cert-body">
        <label class="f-lbl">Nombre del Nuevo Propietario</label>
        <input type="text" id="buyerName" class="f-inp" value="Ana María Prado">
        
        <label class="f-lbl">RUT Nuevo Propietario</label>
        <input type="text" id="buyerRut" class="f-inp" value="15.662.341-K">

        <label class="f-lbl">Email del Adquirente</label>
        <input type="email" id="buyerEmail" class="f-inp" value="ana.prado@email.cl">
        
        <label class="f-lbl">Seleccione Método de Pago</label>
        <div class="mtabs">
          <div class="mtab active" id="tab-tbk" onclick="selectMethod('tbk')">Transbank</div>
          <div class="mtab" id="tab-transfer" onclick="selectMethod('transfer')">Transferencia</div>
          <div class="mtab" id="tab-mach" onclick="selectMethod('mach')">MACH</div>
        </div>

        <div class="method-desc active" id="desc-tbk">ℹ️ Conexión simulada con Webpay Plus. Admite Crédito, Débito y Prepago.</div>
        <div class="method-desc" id="desc-transfer">ℹ️ Abono directo a Cuenta Corriente de Casa Moneda con validación automática de fondos.</div>
        <div class="method-desc" id="desc-mach">ℹ️ Pago inmediato mediante escaneo seguro desde tu billetera digital MACH Bci.</div>

        <div class="divider"></div>
        <button class="btn-confirm" onclick="processPayment()">Confirmar Transferencia Bancaria</button>
      </div>
    </div>

    <div class="proto-screen" id="screenProcessing">
      <div class="proc-wrap">
        <div class="spinner"></div>
        <h3 id="processingTitle">Procesando Transacción Segura...</h3>
        <p style="font-size:13px; color:var(--text3); margin-top:5px;">Inscribiendo propiedad en Casa Moneda de Chile...</p>
      </div>
    </div>

    <div class="proto-screen" id="screenSuccess">
      <div class="m-head">
        <div class="m-badge">✓ Transferencia Exitosa</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="ok-wrap">
        <div class="ok-circle">
          <svg viewBox="0 0 24 24"><path d="M5 13l4 4L19 7"/></svg>
        </div>
        <h2>¡Propiedad Transferida!</h2>
        <p style="font-size:13px; color:var(--text2); margin-top:5px;">El activo ha sido adjudicado legalmente al nuevo titular.</p>
        <div class="ok-folio">Folio Transacción:<br><strong id="folioCode">CMMC-9923-2026-X</strong></div>
        
        <button class="btn-pdf" onclick="generateOfficialPDF()">
          <span>📄</span> Descargar Certificado PDF Oficial
        </button>
      </div>
    </div>

  </div>
</div>

<div class="pdf-toast" id="toast">Certificado generado correctamente</div>

<script>
  // Variables globales del prototipo para capturar lo seleccionado en el catálogo
  let currentAssetName = "";
  let currentAssetPrice = "";
  let currentAssetId = "";
  let selectedMethodName = "Transbank Webpay Plus";

  function openPrototype(name, price, id) {
    currentAssetName = name;
    currentAssetPrice = price;
    currentAssetId = id;

    // Actualizar dinámicamente la UI del Modal
    document.getElementById('modalAssetName').innerText = name;
    document.getElementById('modalAssetPrice').innerText = price;
    document.getElementById('modalAssetId').innerText = id;

    // Generar una vista en miniatura simple según el tipo de producto
    const visual = document.getElementById('modalAssetVisual');
    if(name.includes('Barra')) {
      visual.style.background = 'radial-gradient(circle at 35% 35%,#FFF5CC,#D4A017 50%,#8A6700)';
      visual.innerText = "Oro\n1 oz";
    } else if(name.includes('Billete')) {
      visual.style.background = 'linear-gradient(to right, #A9DFBF, #AED6F1)';
      visual.innerText = "Billete\n2026";
    } else if(name.includes('Bronce')) {
      visual.style.background = '#CD7F32';
      visual.innerText = "Bronce\n1841";
    } else {
      visual.style.background = 'radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800)';
      visual.innerText = "Chile\n$200";
    }

    // Configurar tipo de activo en la grilla del modal
    document.getElementById('modalAssetType').innerText = name.includes('Billete') ? "Papel Moneda Oficial" : "Numismático Oficial";

    document.getElementById('modalPrototype').classList.add('open');
    changeScreen('screenDetail');
  }

  function closeModal() {
    document.getElementById('modalPrototype').classList.remove('open');
  }

  function changeScreen(screenId) {
    const screens = document.querySelectorAll('.proto-screen');
    screens.forEach(s => s.classList.remove('active'));
    document.getElementById(screenId).classList.add('active');
  }

  function selectMethod(method) {
    // Apagar todos los tabs y descripciones
    document.querySelectorAll('.mtab').forEach(t => t.classList.remove('active'));
    document.querySelectorAll('.method-desc').forEach(d => d.classList.remove('active'));

    // Encender el correspondiente
    document.getElementById(`tab-${method}`).classList.add('active');
    document.getElementById(`desc-${method}`).classList.add('active');

    // Mapear nombre del método para colocarlo en el PDF final
    if(method === 'tbk') selectedMethodName = "Transbank Webpay Plus";
    if(method === 'transfer') selectedMethodName = "Transferencia Bancaria Directa";
    if(method === 'mach') selectedMethodName = "MACH Digital Bci";
  }

  function processPayment() {
    // Actualizar el título de la carga según el método de pago elegido
    document.getElementById('processingTitle').innerText = `Conectando con ${selectedMethodName}...`;
    changeScreen('screenProcessing');
    
    setTimeout(() => {
      const randomFolio = 'CMMC-' + Math.floor(1000 + Math.random() * 9000) + '-2026-X';
      document.getElementById('folioCode').innerText = randomFolio;
      changeScreen('screenSuccess');
    }, 1800);
  }

  // GENERADOR DE PDF PROFESIONAL RESPONDIDAS LAS EXIGENCIAS
  function generateOfficialPDF() {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();

    const nuevoPropietario = document.getElementById('buyerName').value || 'Ana María Prado';
    const rutPropietario = document.getElementById('buyerRut').value || '15.662.341-K';
    const emailPropietario = document.getElementById('buyerEmail').value || 'ana.prado@email.cl';
    const folioTransaccion = document.getElementById('folioCode').innerText;
    const fechaEmision = new Date().toLocaleDateString('es-CL');

    // Estilo Visual del PDF Corporativo
    doc.setFillColor(11, 31, 58); // --navy
    doc.rect(0, 0, 210, 40, 'F');

    doc.setTextColor(255, 255, 255);
    doc.setFont("Helvetica", "bold");
    doc.setFontSize(22);
    doc.text("MONEDA VIVA", 20, 25);

    doc.setFont("Helvetica", "normal");
    doc.setFontSize(10);
    doc.setTextColor(201, 168, 76); // --gold-lt
    doc.text("CASA MONEDA DE CHILE · SOLUCIÓN INMUTABLE", 20, 32);

    doc.setTextColor(11, 31, 58);
    doc.setFont("Helvetica", "bold");
    doc.setFontSize(15);
    doc.text("CERTIFICADO OFICIAL DE TRANSMISIÓN DE DOMINIO", 20, 60);

    doc.setDrawColor(201, 168, 76);
    doc.setLineWidth(1);
    doc.line(20, 65, 190, 65);

    doc.setFontSize(11);
    doc.setTextColor(58, 80, 112);
    doc.text("Especificaciones técnicas del activo:", 20, 75);

    doc.setFont("Helvetica", "normal");
    doc.setFontSize(10);
    doc.setTextColor(11, 31, 58);
    doc.text("• Descripción de la Pieza:", 25, 85); doc.setFont("Helvetica", "bold"); doc.text(currentAssetName, 68, 85);
    doc.setFont("Helvetica", "normal");
    doc.text("• ID único del Registro:", 25, 93); doc.setFont("Helvetica", "bold"); doc.text(currentAssetId, 68, 93);
    doc.setFont("Helvetica", "normal");
    doc.text("• Valor de Adjudicación:", 25, 101); doc.text(`${currentAssetPrice} CLP`, 68, 101);

    // Cuadro con datos del Comprador
    doc.setFillColor(244, 247, 251); 
    doc.rect(20, 112, 170, 45, 'F');
    doc.setDrawColor(212, 225, 240); 
    doc.rect(20, 112, 170, 45, 'S');

    doc.setTextColor(11, 31, 58);
    doc.setFont("Helvetica", "bold");
    doc.setFontSize(11);
    doc.text("TITULAR LEGAL REGISTRADO", 25, 121);

    doc.setFont("Helvetica", "normal");
    doc.setFontSize(10);
    doc.text(`Nombre Completo: ${nuevoPropietario}`, 25, 130);
    doc.text(`RUT Identificador: ${rutPropietario}`, 25, 137);
    doc.text(`Email Registrado:  ${emailPropietario}`, 25, 144);

    // Liquidación
    doc.setFont("Helvetica", "normal");
    doc.setTextColor(107, 135, 168);
    doc.text(`Código Único Operacional: ${folioTransaccion}`, 20, 175);
    doc.text(`Fecha Timbrado Digital: ${fechaEmision}`, 20, 182);
    doc.text(`Canal Integrado de Pago: ${selectedMethodName}`, 20, 189);

    // Firmas fijas
    doc.setDrawColor(212, 225, 240);
    doc.line(20, 230, 90, 230);
    doc.setFontSize(9);
    doc.text("Firma de Validación Tecnológica", 20, 237);
    doc.setFont("Helvetica", "bold");
    doc.text("Casa Moneda de Chile S.A.", 20, 242);

    doc.setFont("Helvetica", "italic");
    doc.setFontSize(8);
    doc.setTextColor(160, 160, 160);
    doc.text("Este certificado emula las condiciones reales de auditoría numismática en la red MonedaViva.", 20, 275);

    // Guardado y descarga automatizada
    doc.save(`Certificado-${currentAssetId}.pdf`);

    // Mostrar Toast flotante informativo
    const toast = document.getElementById('toast');
    toast.classList.add('show');
    setTimeout(() => toast.classList.remove('show'), 3000);
  }
</script>

</body>
</html>
