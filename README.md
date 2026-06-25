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

/* ── PRODUCTOS ── */
.prod-sec{background:var(--off-white); padding: 3rem 1.5rem; max-width: 1140px; margin: 0 auto;}
.prod-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(320px,1fr));gap:2rem;margin-top:2.5rem}
.prod-card{background:var(--white);border:1.5px solid var(--soft2);border-radius:var(--radius-lg);overflow:hidden;transition:transform .2s,box-shadow .2s;cursor:pointer;display:flex;flex-direction:column;justify-content:space-between}
.prod-card:hover{transform:translateY(-4px);box-shadow:0 12px 32px rgba(11,31,58,0.12)}
.prod-img{height:200px;background:var(--soft);display:flex;align-items:center;justify-content:center;position:relative;overflow:hidden}
.prod-img img{width:100%;height:100%;object-fit:cover}
.prod-coin{border-radius:50%;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800);border:2px solid var(--gold-lt);display:flex;align-items:center;justify-content:center;font-weight:800;color:#3A2800;text-align:center;line-height:1.3}
.prod-tag{position:absolute;top:12px;right:12px;font-size:10px;padding:4px 10px;border-radius:20px;font-weight:700;z-index:10}
.tag-cert{background:var(--green-bg);color:var(--green-text);border:1px solid var(--green-border)}
.tag-new{background:#E6F1FB;color:#0C447C;border:1px solid #85B7EB}
.prod-info{padding:1.5rem;flex-grow:1}
.prod-info h3{font-size:17px;font-weight:700;color:var(--navy);margin-bottom:6px}
.prod-info p{font-size:13px;color:var(--text2);margin-bottom:1rem;height:45px;overflow:hidden}
.prod-qr-status{font-size:11px;font-weight:700;color:var(--green-text);background:var(--green-bg);padding:5px 10px;border-radius:6px;display:inline-flex;align-items:center;gap:6px;margin-bottom:1rem}
.prod-footer{display:flex;align-items:center;justify-content:space-between;border-top:1px solid var(--soft);padding-top:1rem}
.prod-price{font-size:20px;font-weight:800;color:var(--navy)}
.prod-price span{font-size:12px;color:var(--text3);font-weight:400}
.btn-ver{font-size:13px;font-weight:700;color:var(--navy-light);border:1.5px solid var(--soft2);background:transparent;border-radius:var(--radius);padding:8px 16px;cursor:pointer;transition:all .15s}
.btn-ver:hover{background:var(--navy);color:var(--white);border-color:var(--navy)}

/* ── MODAL DE PROTOTIPO COMPLETAMENTE INTERACTIVO ── */
.modal-overlay{display:none;position:fixed;inset:0;z-index:200;background:rgba(5,15,30,0.88);align-items:flex-start;justify-content:center;padding:2rem 1rem;overflow-y:auto}
.modal-overlay.open{display:flex}
.modal-box{background:var(--white);border-radius:var(--radius-lg);width:100%;max-width:520px;max-height:92vh;overflow-y:auto;border:1.5px solid var(--soft2);margin:auto;box-shadow:0 24px 80px rgba(0,0,0,0.3)}

.proto-screen{display:none}
.proto-screen.active{display:block;animation:fadeUp .2s ease}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}

.m-head{background:var(--navy);padding:1.25rem;display:flex;align-items:center;justify-content:space-between;border-radius:var(--radius-lg) var(--radius-lg) 0 0}
.m-badge{display:flex;align-items:center;gap:7px;font-size:11px;color:var(--gold-lt);text-transform:uppercase;letter-spacing:.09em;font-weight:700}
.live-dot{width:7px;height:7px;border-radius:50%;background:#4CAF50;animation:pulse 1.6s infinite}
.m-close{background:none;border:none;color:rgba(255,255,255,0.45);font-size:24px;cursor:pointer}

.cert-body{padding:1.5rem}
.coin-row{display:flex;gap:1.2rem;align-items:center;margin-bottom:1.2rem}
.cert-vis-img{width:80px;height:55px;border-radius:4px;overflow:hidden;border:1px solid var(--soft2)}
.cert-vis-img img{width:100%;height:100%;object-fit:cover}
.cert-vis{width:64px;height:64px;border-radius:50%;flex-shrink:0;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800);border:2px solid var(--gold-lt);display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:800;color:#3A2800;text-align:center}
.cert-info h2{font-size:16px;font-weight:700;color:var(--navy);margin-bottom:4px}
.cert-info p{font-size:12.5px;color:var(--text2);margin-bottom:6px}
.tag-auth{display:inline-flex;align-items:center;gap:4px;font-size:11px;font-weight:700;padding:4px 10px;border-radius:20px;background:var(--green-bg);color:var(--green-text);border:1px solid var(--green-border)}
.divider{border:none;border-top:1.5px solid var(--soft);margin:1rem 0}
.dgrid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:1.2rem}
.dcell{background:var(--off-white);border-radius:var(--radius);padding:10px 12px;border:1px solid var(--soft2)}
.dcell .l{font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.07em;margin-bottom:3px;font-weight:600}
.dcell .v{font-size:13px;font-weight:600;color:var(--navy)}

.cert-foot{display:flex;gap:10px;padding:1.25rem;background:var(--off-white);border-top:1.5px solid var(--soft2);flex-wrap:wrap;border-radius:0 0 var(--radius-lg) var(--radius-lg)}
.btn-sm{flex:1;min-width:100px;padding:11px;border-radius:var(--radius);border:1.5px solid var(--soft2);background:var(--white);font-size:13px;font-weight:600;cursor:pointer}
.btn-navy{flex:1;min-width:140px;padding:11px;border-radius:var(--radius);border:none;background:var(--navy);font-size:13px;font-weight:700;cursor:pointer;color:var(--gold-lt);text-align:center}

/* FORMULARIO PAGO Y DESPACHO VOLUNTARIO */
.f-lbl{font-size:11.5px;text-transform:uppercase;letter-spacing:.07em;color:var(--navy);font-weight:700;display:block;margin-bottom:6px}
.f-inp{width:100%;padding:11px 13px;border-radius:var(--radius);border:1.5px solid var(--soft2);background:var(--white);color:var(--navy);font-size:13.5px;margin-bottom:1rem}

.radio-group{display:flex;flex-direction:column;gap:10px;margin-bottom:1.5rem}
.radio-box{border:1.5px solid var(--soft2);border-radius:var(--radius);padding:12px;display:flex;align-items:flex-start;gap:12px;cursor:pointer;background:var(--off-white);transition:all .15s}
.radio-box.active{border-color:var(--navy);background:var(--white);box-shadow:0 3px 10px rgba(11,31,58,0.06)}
.radio-box input{margin-top:4px}
.radio-txt h4{font-size:13px;font-weight:700;color:var(--navy)}
.radio-txt p{font-size:11.5px;color:var(--text3);line-height:1.45}

.mtabs{display:flex;gap:6px;margin-bottom:1.2rem}
.mtab{flex:1;padding:11px 6px;border-radius:var(--radius);border:1.5px solid var(--soft2);background:var(--off-white);font-size:12px;font-weight:700;cursor:pointer;color:var(--text2);text-align:center}
.mtab.active{border-color:var(--navy);background:var(--navy);color:var(--gold-lt)}

/* FORMULARIO DE TARJETA REALISTA */
.card-wrapper{background:#F0F4F9;border:1.5px solid var(--soft2);border-radius:var(--radius);padding:1.25rem;margin-bottom:1.2rem}
.card-row{display:grid;grid-template-columns:1fr 1fr;gap:12px}

.method-desc{font-size:12px;color:var(--text3);margin-top:-6px;margin-bottom:15px;display:none}
.method-desc.active{display:block}
.btn-confirm{width:100%;padding:13px;border-radius:var(--radius);background:var(--navy);color:var(--gold-lt);border:none;font-size:14.5px;font-weight:800;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px}

/* PROCESANDO / ÉXITO */
.proc-wrap{padding:4rem 1.5rem;text-align:center}
.spinner{width:48px;height:48px;border:4px solid var(--soft2);border-top-color:var(--navy);border-radius:50%;margin:0 auto 1.5rem;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.ok-wrap{padding:3rem 1.5rem;text-align:center}
.ok-circle{width:64px;height:64px;border-radius:50%;background:var(--green-bg);border:2px solid var(--green-border);margin:0 auto 1.5rem;display:flex;align-items:center;justify-content:center}
.ok-circle svg{width:30px;height:30px;stroke:var(--green-text);fill:none;stroke-width:2.5}
.ok-folio{font-family:monospace;font-size:12px;color:var(--text3);background:var(--off-white);padding:10px 14px;border-radius:var(--radius);border:1.5px solid var(--soft2);margin:1rem auto;max-width:320px}
.btn-pdf{display:inline-flex;align-items:center;gap:8px;padding:13px 26px;border-radius:var(--radius);border:2px solid var(--navy);background:var(--navy);font-size:14.5px;font-weight:800;cursor:pointer;color:var(--gold-lt);margin-top:1.5rem}

.pdf-toast{position:fixed;bottom:2rem;left:50%;transform:translateX(-50%);background:var(--navy);color:var(--gold-lt);border:1.5px solid var(--navy3);padding:11px 22px;border-radius:var(--radius);font-size:13px;font-weight:600;z-index:999;opacity:0;transition:opacity .3s;pointer-events:none}
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
  </div>
</header>

<section class="hero" id="inicio">
  <div class="hero-eyebrow"><div class="hero-dot"></div>Trazabilidad Numismática Garantizada con QR Oficial</div>
  <h1>Catálogo e Historial de Activos</h1>
  <p class="hero-sub">Escanea, verifica la procedencia institucional mediante QR y adquiere coleccionables con transferencia de dominio instantánea.</p>
</section>

<section class="prod-sec" id="productos">
  <div class="prod-grid">
    
    <div class="prod-card" onclick="openPrototype('Impreso Conmemorativo: Margot Duhalde', '$12.990', '#SKU-90005045', 'Papel de Seguridad', true)">
      <div class="prod-img">
        <img src="data:image/jpeg;base64,` + b64_data + `" alt="Margot Duhalde">
        <span class="prod-tag tag-new">Especial 280 Años</span>
      </div>
      <div class="prod-info">
        <h3>Impreso Conmemorativo: Margot Duhalde</h3>
        <p>Papel de seguridad con ilustraciones de alta calidad y elementos de resguardo oficial.</p>
        <div class="prod-qr-status"><span>📱</span> QR Escaneado: Auténtico Casa Moneda</div>
        <div class="prod-footer">
          <div class="prod-price">$12.990 <span>CLP</span></div>
          <button class="btn-ver">Ver y Comprar</button>
        </div>
      </div>
    </div>

    <div class="prod-card" onclick="openPrototype('Moneda Bicentenario 2010', '$38.500', '#MV-2010-8841X', 'Cobre-Níquel', false)">
      <div class="prod-img">
        <div class="prod-coin" style="width:90px;height:90px;font-size:11px">Chile<br>$200<br>2010</div>
        <span class="prod-tag tag-cert">Certificada</span>
      </div>
      <div class="prod-info">
        <h3>Moneda Bicentenario 2010</h3>
        <p>Edición conmemorativa acuñada en metal noble. Registro histórico intachable.</p>
        <div class="prod-qr-status"><span>📱</span> QR Escaneado: Auténtico Casa Moneda</div>
        <div class="prod-footer">
          <div class="prod-price">$38.500 <span>CLP</span></div>
          <button class="btn-ver">Ver y Comprar</button>
        </div>
      </div>
    </div>

  </div>
</section>

<div class="modal-overlay" id="modalPrototype">
  <div class="modal-box">
    
    <div class="proto-screen active" id="screenDetail">
      <div class="m-head">
        <div class="m-badge"><div class="live-dot"></div> MonedaViva Blockchain QR</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="cert-body">
        <div class="coin-row">
          <div id="modalAssetVisualContainer"></div>
          <div class="cert-info">
            <h2 id="modalAssetName">Impreso Conmemorativo: Margot Duhalde</h2>
            <p>Identificador Único: <span id="modalAssetId" style="font-weight:bold;">#SKU-90005045</span></p>
            <span class="tag-auth">✓ QR Verificado: 100% Original Casa Moneda</span>
          </div>
        </div>
        <div class="divider"></div>
        <div class="dgrid">
          <div class="dcell"><div class="l">Material Base</div><div class="v" id="modalAssetMaterial">Papel de seguridad</div></div>
          <div class="dcell"><div class="l">Propietario Origen</div><div class="v">Coleccionista Particular</div></div>
          <div class="dcell"><div class="l">Estado QR</div><div class="v" style="color:var(--green-text)">Firma Digital Válida</div></div>
          <div class="dcell"><div class="l">Disponibilidad</div><div class="v">Traspaso Inmediato</div></div>
        </div>
      </div>
      <div class="cert-foot">
        <button class="btn-sm" onclick="closeModal()">Cerrar</button>
        <button class="btn-navy" onclick="changeScreen('screenPayment')">Adquirir Activo (<span id="modalAssetPrice">$12.990</span>)</button>
      </div>
    </div>

    <div class="proto-screen" id="screenPayment">
      <div class="m-head">
        <div class="m-badge">Formulario de Transmisión legal</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="cert-body">
        <label class="f-lbl">Nombre del Nuevo Propietario</label>
        <input type="text" id="buyerName" class="f-inp" value="Ana María Prado">
        
        <label class="f-lbl">RUT Nuevo Propietario</label>
        <input type="text" id="buyerRut" class="f-inp" value="15.662.341-K">

        <label class="f-lbl">Logística y Custodia Física (Voluntario)</label>
        <div class="radio-group">
          <div class="radio-box active" id="rBox1" onclick="setShipping('owner')">
            <input type="radio" id="shipOwner" name="shippingMethod" value="owner" checked>
            <div class="radio-txt">
              <h4>El dueño anterior realiza el envío</h4>
              <p>El vendedor gestiona el despacho de la pieza física de forma directa y privada bajo mutuo acuerdo.</p>
            </div>
          </div>
          <div class="radio-box" id="rBox2" onclick="setShipping('casamoneda')">
            <input type="radio" id="shipCasa" name="shippingMethod" value="casamoneda">
            <div class="radio-txt">
              <h4>Delegar despacho a Casa de Moneda</h4>
              <p>La institución actúa como intermediario seguro: retira, audita la autenticidad física y despacha al domicilio.</p>
            </div>
          </div>
        </div>

        <label class="f-lbl">Pasarela Bancaria Integrada</label>
        <div class="mtabs">
          <div class="mtab active" id="tab-tbk" onclick="selectMethod('tbk')">Transbank</div>
          <div class="mtab" id="tab-transfer" onclick="selectMethod('transfer')">Transferencia</div>
          <div class="mtab" id="tab-mach" onclick="selectMethod('mach')">MACH</div>
        </div>

        <div id="panel-tbk" class="card-wrapper">
          <label class="f-lbl" style="font-size:10px; color:var(--text2)">Número de la Tarjeta</label>
          <input type="text" class="f-inp" value="5412 7511 9042 8815" placeholder="4320 5571 8842 9012" style="letter-spacing:1px; margin-bottom: 0.8rem;">
          <div class="card-row">
            <div>
              <label class="f-lbl" style="font-size:10px; color:var(--text2)">Expiración</label>
              <input type="text" class="f-inp" value="11/29" placeholder="MM/AA" style="margin-bottom: 0;">
            </div>
            <div>
              <label class="f-lbl" style="font-size:10px; color:var(--text2)">CVV / CVC</label>
              <input type="password" class="f-inp" value="382" placeholder="3 dígitos" style="margin-bottom: 0;">
            </div>
          </div>
        </div>

        <div class="method-desc" id="desc-transfer">ℹ️ Transferencia directa a la cuenta corriente institucional de resguardo de Casa de Moneda de Chile.</div>
        <div class="method-desc" id="desc-mach">ℹ️ Liquidación instantánea escaneando el código push en tu cuenta digital MACH Bci.</div>

        <div class="divider"></div>
        <button class="btn-confirm" onclick="processPayment()">Pagar y Validar Certificado</button>
      </div>
    </div>

    <div class="proto-screen" id="screenProcessing">
      <div class="proc-wrap">
        <div class="spinner"></div>
        <h3 id="processingTitle">Conectando con Transbank...</h3>
        <p style="font-size:13px; color:var(--text3); margin-top:5px;">Acuñando datos del propietario y logística...</p>
      </div>
    </div>

    <div class="proto-screen" id="screenSuccess">
      <div class="m-head">
        <div class="m-badge">✓ Proceso Finalizado</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="ok-wrap">
        <div class="ok-circle">
          <svg viewBox="0 0 24 24"><path d="M5 13l4 4L19 7"/></svg>
        </div>
        <h2>¡Transferencia Completa!</h2>
        <p style="font-size:13px; color:var(--text2); margin-top:5px;">El dominio digital ha cambiado y la orden de entrega fue emitida.</p>
        <div class="ok-folio">Folio Registro:<br><strong id="folioCode">CMMC-8841-2026</strong></div>
        
        <button class="btn-pdf" onclick="generateOfficialPDF()">
          <span>📄</span> Descargar PDF Oficial con Datos de Envío
        </button>
      </div>
    </div>

  </div>
</div>

<div class="pdf-toast" id="toast">Certificado PDF emitido con éxito</div>

<script>
  let currentAssetName = "";
  let currentAssetPrice = "";
  let currentAssetId = "";
  let currentAssetMaterial = "";
  let selectedMethodName = "Transbank Webpay Plus (Tarjeta Crédito/Débito)";
  let selectedShippingLabel = "El dueño anterior realiza el envío de forma directa (Acuerdo privado)";
  const realB64 = "data:image/jpeg;base64,` + b64_data + `";

  function openPrototype(name, price, id, material, isDuhalde) {
    currentAssetName = name;
    currentAssetPrice = price;
    currentAssetId = id;
    currentAssetMaterial = material;

    document.getElementById('modalAssetName').innerText = name;
    document.getElementById('modalAssetPrice').innerText = price;
    document.getElementById('modalAssetId').innerText = id;
    document.getElementById('modalAssetMaterial').innerText = material;

    const container = document.getElementById('modalAssetVisualContainer');
    if(isDuhalde) {
      container.innerHTML = `<div class="cert-vis-img"><img src="${realB64}" alt="Duhalde"></div>`;
    } else {
      container.innerHTML = `<div class="cert-vis">Chile<br>$200</div>`;
    }

    document.getElementById('modalPrototype').classList.add('open');
    changeScreen('screenDetail');
  }

  function closeModal() {
    document.getElementById('modalPrototype').classList.remove('open');
  }

  function changeScreen(screenId) {
    document.querySelectorAll('.proto-screen').forEach(s => s.classList.remove('active'));
    document.getElementById(screenId).classList.add('active');
  }

  function setShipping(type) {
    document.getElementById('rBox1').classList.remove('active');
    document.getElementById('rBox2').classList.remove('active');
    
    if(type === 'owner') {
      document.getElementById('rBox1').classList.add('active');
      document.getElementById('shipOwner').checked = true;
      selectedShippingLabel = "El dueño anterior realiza el envío de forma directa (Acuerdo privado)";
    } else {
      document.getElementById('rBox2').classList.add('active');
      document.getElementById('shipCasa').checked = true;
      selectedShippingLabel = "Delegado a Casa de Moneda de Chile (Logística Centralizada)";
    }
  }

  function selectMethod(method) {
    document.querySelectorAll('.mtab').forEach(t => t.classList.remove('active'));
    document.querySelectorAll('.method-desc').forEach(d => d.classList.remove('active'));
    document.getElementById('panel-tbk').style.display = 'none';

    document.getElementById(`tab-${method}`).classList.add('active');

    if(method === 'tbk') {
      document.getElementById('panel-tbk').style.display = 'block';
      selectedMethodName = "Transbank Webpay Plus (Tarjeta Crédito/Débito)";
    } else if(method === 'transfer') {
      document.getElementById('desc-transfer').classList.add('active');
      selectedMethodName = "Transferencia Bancaria";
    } else if(method === 'mach') {
      document.getElementById('desc-mach').classList.add('active');
      selectedMethodName = "MACH Digital Bci";
    }
  }

  function processPayment() {
    document.getElementById('processingTitle').innerText = `Conectando con ${selectedMethodName}...`;
    changeScreen('screenProcessing');
    setTimeout(() => {
      document.getElementById('folioCode').innerText = 'CMMC-' + Math.floor(1000 + Math.random() * 9000) + '-2026';
      changeScreen('screenSuccess');
    }, 1500);
  }

  function generateOfficialPDF() {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();

    const buyer = document.getElementById('buyerName').value || 'Ana María Prado';
    const rut = document.getElementById('buyerRut').value || '15.662.341-K';
    const folio = document.getElementById('folioCode').innerText;
    const dateStr = new Date().toLocaleDateString('es-CL');

    // Cabecera institucional
    doc.setFillColor(11, 31, 58);
    doc.rect(0, 0, 210, 40, 'F');
    doc.text("CASA MONEDA DE CHILE", 20, 25);
    doc.setFontSize(10);
    doc.setTextColor(201, 168, 76);
    doc.text("SISTEMA DE VERIFICACIÓN QR Y TRAZABILIDAD MONEDAVIVA", 20, 32);

    doc.setTextColor(11, 31, 58);
    doc.setFontSize(14);
    doc.text("CERTIFICADO DE AUTENTICIDAD Y PROPIEDAD DIGITAL", 20, 58);
    doc.setDrawColor(201, 168, 76);
    doc.line(20, 62, 190, 62);

    doc.setFontSize(11);
    doc.setTextColor(58, 80, 112);
    doc.text("Detalle del Activo Validado por Código QR:", 20, 72);

    doc.setFont("Helvetica", "normal");
    doc.setFontSize(10);
    doc.setTextColor(11, 31, 58);
    doc.text(`• Nombre de la Pieza:   ${currentAssetName}`, 24, 82);
    doc.text(`• Código de Identificación QR: ${currentAssetId}`, 24, 89);
    doc.text(`• Material Evaluado:     ${currentAssetMaterial}`, 24, 96);
    doc.text(`• Estado de Validación:  Auténtico Garantizado bajo Auditoría Institucional`, 24, 103);

    doc.setFillColor(244, 247, 251); 
    doc.rect(20, 112, 170, 45, 'F');
    doc.text("DATOS LEGALES DEL ADQUIRENTE", 25, 122);
    doc.text(`Nuevo Propietario Registrado: ${buyer}`, 25, 131);
    doc.text(`Cédula de Identidad / RUT:      ${rut}`, 25, 138);

    doc.text("Modalidad de Envío Solicitada:", 20, 175);
    doc.text(selectedShippingLabel, 20, 182);

    doc.text(`• Código de Operación Interna: ${folio}`, 20, 206);
    doc.text(`• Fecha de Timbrado Digital:     ${dateStr}`, 20, 213);
    doc.text(`• Pasarela Transaccional:       ${selectedMethodName}`, 20, 220);

    doc.save(`Certificado-QR-${currentAssetId}.pdf`);

    const toast = document.getElementById('toast');
    toast.classList.add('show');
    setTimeout(() => toast.classList.remove('show'), 3000);
  }
</script>

</body>
</html>
