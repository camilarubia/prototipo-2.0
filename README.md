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

/* MODAL & FLUJO */
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

/* PANTALLA PAGO */
.f-lbl{font-size:10px;text-transform:uppercase;letter-spacing:.07em;color:var(--text2);font-weight:600;display:block;margin-bottom:5px}
.f-inp{width:100%;padding:10px 12px;border-radius:var(--radius);border:1.5px solid var(--soft2);background:var(--white);color:var(--navy);font-size:13px;font-weight:500;margin-bottom:1rem;transition:border-color .15s}
.btn-confirm{width:100%;padding:12px;border-radius:var(--radius);background:var(--navy);color:var(--gold-lt);border:none;font-size:14px;font-weight:800;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:7px}

/* PROCESANDO */
.proc-wrap{padding:3rem 1.25rem;text-align:center}
.spinner{width:46px;height:46px;border:3.5px solid var(--soft2);border-top-color:var(--navy);border-radius:50%;margin:0 auto 1.4rem;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}

/* ÉXITO & PDF */
.ok-wrap{padding:2.5rem 1.5rem;text-align:center}
.ok-circle{width:62px;height:62px;border-radius:50%;background:var(--green-bg);border:2px solid var(--green-border);margin:0 auto 1.25rem;display:flex;align-items:center;justify-content:center}
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
      <a href="#demo" class="nav-cta">Ver prototipo</a>
    </nav>
  </div>
</header>

<section class="hero" id="inicio">
  <div class="hero-eyebrow"><div class="hero-dot"></div>Innovacion · Design Thinking · Transformacion Digital</div>
  <h1>Cada moneda tiene historia.<br><em>Ahora tambien tiene futuro.</em></h1>
  <p class="hero-sub">MonedaViva convierte cada pieza de Casa Moneda en un activo verificable con certificado PDF oficial.</p>
  <div class="hero-actions">
    <button class="btn-primary" onclick="openModal()">Ver prototipo en vivo</button>
  </div>
</section>

<section class="demo-sec" id="demo">
  <div class="demo-inner">
    <div class="demo-text">
      <p class="demo-eyebrow">Prototipo en vivo</p>
      <h2 class="demo-title">Vende tu moneda. Recibe el PDF al final.</h2>
      <p class="demo-sub">El certificado oficial se genera tras confirmar la venta simulada.</p>
      <button class="btn-demo" onclick="openModal()">Abrir prototipo interactivo &rarr;</button>
    </div>
  </div>
</section>

<div class="modal-overlay" id="modalPrototype">
  <div class="modal-box">
    
    <div class="proto-screen active" id="screenDetail">
      <div class="m-head">
        <div class="m-badge"><div class="live-dot"></div> MonedaViva Certificados</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="cert-body">
        <div class="coin-row">
          <div class="cert-vis">Chile<br>$200<br>2010</div>
          <div class="cert-info">
            <h2>Moneda Bicentenario 2010</h2>
            <p>ID Pieza: #MV-2010-8841X</p>
            <span class="tag-auth">✓ Original Casa Moneda</span>
          </div>
        </div>
        <div class="divider"></div>
        <div class="dgrid">
          <div class="dcell"><div class="l">Metal</div><div class="v">Cobre-Níquel</div></div>
          <div class="dcell"><div class="l">Año Emisión</div><div class="v">2010</div></div>
          <div class="dcell"><div class="l">Propietario Actual</div><div class="v">Carlos Mendoza</div></div>
          <div class="dcell"><div class="l">Estado Reg.</div><div class="v">Listo para Transferir</div></div>
        </div>
      </div>
      <div class="cert-foot">
        <button class="btn-sm" onclick="closeModal()">Cerrar</button>
        <button class="btn-navy" onclick="changeScreen('screenPayment')">Iniciar Venta ($38.500)</button>
      </div>
    </div>

    <div class="proto-screen" id="screenPayment">
      <div class="m-head">
        <div class="m-badge">Datos de Transferencia</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="cert-body">
        <label class="f-lbl">Nombre del Nuevo Propietario</label>
        <input type="text" id="buyerName" class="f-inp" value="Ana María Prado" placeholder="Ej: Juan Pérez">
        
        <label class="f-lbl">RUT Nuevo Propietario</label>
        <input type="text" id="buyerRut" class="f-inp" value="15.662.341-K" placeholder="12.345.678-9">

        <label class="f-lbl">Email de Notificación</label>
        <input type="email" id="buyerEmail" class="f-inp" value="ana.prado@email.cl" placeholder="correo@dominio.com">
        
        <div class="divider"></div>
        <p style="font-size: 12px; color: var(--text2); margin-bottom: 10px;">Al confirmar, se simulará una transacción segura via Transbank Webpay.</p>
        <button class="btn-confirm" onclick="processPayment()">Confirmar y Simular Pago</button>
      </div>
    </div>

    <div class="proto-screen" id="screenProcessing">
      <div class="proc-wrap">
        <div class="spinner"></div>
        <h3>Procesando Pago Seguro...</h3>
        <p style="font-size:13px; color:var(--text3); margin-top:5px;">Verificando firmas y registrando transferencia...</p>
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
        <p style="font-size:13px; color:var(--text2); margin-top:5px;">La moneda ha sido asignada legalmente al nuevo titular.</p>
        <div class="ok-folio">Folio Oficial Transacción:<br><strong id="folioCode">CMMC-9923-2026-X</strong></div>
        
        <button class="btn-pdf" onclick="generateOfficialPDF()">
          <span class="btn-pdf-icon">📄</span> Descargar Certificado PDF
        </button>
      </div>
    </div>

  </div>
</div>

<div class="pdf-toast" id="toast">Certificado generado correctamente</div>

<script>
  function openModal() {
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

  function processPayment() {
    changeScreen('screenProcessing');
    // Simula 2 segundos de carga/procesamiento de Transbank
    setTimeout(() => {
      // Generar un código de folio dinámico para el prototipo
      const randomFolio = 'CMMC-' + Math.floor(1000 + Math.random() * 9000) + '-2026-X';
      document.getElementById('folioCode').innerText = randomFolio;
      changeScreen('screenSuccess');
    }, 2000);
  }

  // FUNCIÓN CORREGIDA Y MEJORADA PARA JSPDF v2.5.1
  function generateOfficialPDF() {
    // 1. Acceder correctamente a jsPDF en modo UMD
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();

    // 2. Rescatar los datos dinámicos capturados en el formulario
    const nuevoPropietario = document.getElementById('buyerName').value || 'Ana María Prado';
    const rutPropietario = document.getElementById('buyerRut').value || '15.662.341-K';
    const emailPropietario = document.getElementById('buyerEmail').value || 'ana.prado@email.cl';
    const folioTransaccion = document.getElementById('folioCode').innerText;
    const fechaEmision = new Date().toLocaleDateString('es-CL');

    // 3. Estructuración Estética y Corporativa del Documento PDF
    // Fondo de Cabecera (Azul Marino Corporativo)
    doc.setFillColor(11, 31, 58); // --navy
    doc.rect(0, 0, 210, 40, 'F');

    // Texto de Cabecera
    doc.setTextColor(255, 255, 255);
    doc.setFont("Helvetica", "bold");
    doc.setFontSize(22);
    doc.text("MONEDA VIVA", 20, 25);

    doc.setFont("Helvetica", "normal");
    doc.setFontSize(10);
    doc.setTextColor(201, 168, 76); // --gold-lt
    doc.text("CASA MONEDA DE CHILE · REGISTRO DIGITAL", 20, 32);

    // Título Principal
    doc.setTextColor(11, 31, 58);
    doc.setFont("Helvetica", "bold");
    doc.setFontSize(16);
    doc.text("CERTIFICADO DE AUTENTICIDAD Y TRANSFERENCIA", 20, 60);

    // Línea Dorada Divisoria
    doc.setDrawColor(201, 168, 76);
    doc.setLineWidth(1);
    doc.line(20, 65, 190, 65);

    // Detalles de la Pieza Histórica
    doc.setFontSize(12);
    doc.setTextColor(58, 80, 112); // --text2
    doc.text("Detalles del Acto Numismático:", 20, 75);

    doc.setFont("Helvetica", "normal");
    doc.setFontSize(10);
    doc.setTextColor(11, 31, 58);
    doc.text("• Pieza Original:", 25, 85); doc.setFont("Helvetica", "bold"); doc.text("Moneda Bicentenario $200 (Año 2010)", 60, 85);
    doc.setFont("Helvetica", "normal");
    doc.text("• ID de Registro Único:", 25, 93); doc.setFont("Helvetica", "bold"); doc.text("#MV-2010-8841X", 60, 93);
    doc.setFont("Helvetica", "normal");
    doc.text("• Composición Metálica:", 25, 101); doc.text("Cobre-Níquel (Edición Especial)", 60, 101);

    // Cuadro de Propiedad con Fondo Suave
    doc.setFillColor(244, 247, 251); // --off-white
    doc.rect(20, 112, 170, 45, 'F');
    doc.setDrawColor(212, 225, 240); // --soft2
    doc.rect(20, 112, 170, 45, 'S');

    doc.setTextColor(11, 31, 58);
    doc.setFont("Helvetica", "bold");
    doc.setFontSize(11);
    doc.text("DATOS LEGALES DEL NUEVO PROPIETARIO", 25, 120);

    doc.setFont("Helvetica", "normal");
    doc.setFontSize(10);
    doc.text(`Titular Registrado: ${nuevoPropietario}`, 25, 129);
    doc.text(`RUT Documentado:  ${rutPropietario}`, 25, 136);
    doc.text(`Email Vinculado:   ${emailPropietario}`, 25, 143);

    // Información de Validación de la Transacción
    doc.setFont("Helvetica", "normal");
    doc.setTextColor(107, 135, 168); // --text3
    doc.text(`Folio Transacción: ${folioTransaccion}`, 20, 175);
    doc.text(`Fecha de Liquidación: ${fechaEmision}`, 20, 182);
    doc.text("Medio de Pago Verificado: Transbank Webpay Plus Oficial", 20, 189);

    // Bloque de Firma / Pie de Página Simulado
    doc.setDrawColor(212, 225, 240);
    doc.line(20, 235, 90, 235);
    doc.setFontSize(9);
    doc.text("Firma Encargado de Registro", 20, 242);
    doc.setFont("Helvetica", "bold");
    doc.text("Casa Moneda de Chile S.A.", 20, 247);

    // Glosa Legal Pequeña
    doc.setFont("Helvetica", "italic");
    doc.setFontSize(8);
    doc.setTextColor(150, 150, 150);
    doc.text("Este documento sirve como representación gráfica e interactiva de un activo verificado.", 20, 275);
    doc.text("Casa Moneda de Chile - Prototipo de Innovación Digital 2026.", 20, 280);

    // 4. Salida del documento (Descarga automática en el navegador)
    doc.save(`Certificado-${folioTransaccion}.pdf`);

    // Feedback visual (Toast)
    const toast = document.getElementById('toast');
    toast.classList.add('show');
    setTimeout(() => toast.classList.remove('show'), 3000);
  }
</script>

</body>
</html>
