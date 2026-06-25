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
  --radius:      10px;
  --radius-lg:  16px;
  --green-bg:#EAF3DE;--green-text:#2E6B0F;--green-border:#8CBF50;
}
html{scroll-behavior:smooth}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Helvetica,sans-serif;background:var(--off-white);color:var(--text);line-height:1.65}

/* ── NAV ── */
.site-header{background:var(--navy);position:sticky;top:0;z-index:100;border-bottom:3px solid var(--gold)}
.nav-inner{max-width:1140px;margin:0 auto;padding:0 1.5rem;display:flex;align-items:center;justify-content:between;height:66px}
.logo-wrap{display:flex;align-items:center;gap:13px}
.logo-coin{width:40px;height:40px;border-radius:50%;background:radial-gradient(circle at 35% 35%,#F7E48A,var(--gold) 55%,#7A5800);border:2px solid var(--gold-lt);display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:800;color:#3A2800;text-align:center;line-height:1.2}
.logo-text strong{display:block;font-size:18px;font-weight:800;color:var(--white)}
.logo-text span{font-size:10px;color:var(--gold-lt);text-transform:uppercase;letter-spacing:.1em}

/* ── HERO ── */
.hero{background:var(--navy);padding:4rem 1.5rem 2rem;text-align:center;color:var(--white)}
.hero h1{font-size:2.5rem;font-weight:800;margin-bottom:0.5rem}
.hero p{color:rgba(255,255,255,0.6);font-size:15px}

/* ── PRODUCTOS ── */
.prod-sec{padding:3rem 1.5rem;max-width:1140px;margin:0 auto}
.prod-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:1.5rem;margin-top:2rem}
.prod-card{background:var(--white);border:1.5px solid var(--soft2);border-radius:var(--radius-lg);overflow:hidden;cursor:pointer;display:flex;flex-direction:column}
.prod-img{height:160px;background:var(--soft);display:flex;align-items:center;justify-content:center;position:relative}
.prod-tag{position:absolute;top:10px;right:10px;font-size:10px;padding:3px 9px;border-radius:20px;font-weight:700;background:var(--gold);color:var(--navy)}
.prod-info{padding:1.25rem;flex-grow:1}
.prod-info h3{font-size:16px;font-weight:700;color:var(--navy);margin-bottom:6px}
.prod-info p{font-size:13px;color:var(--text2);margin-bottom:1rem;height:40px;overflow:hidden}
.prod-qr-status{font-size:11px;font-weight:700;color:var(--green-text);background:var(--green-bg);padding:5px 8px;border-radius:6px;display:inline-flex;align-items:center;gap:5px;margin-bottom:1rem}
.prod-footer{display:flex;align-items:center;justify-content:between;border-top:1px solid var(--soft);padding-top:0.75rem}
.prod-price{font-size:18px;font-weight:800;color:var(--navy)}
.btn-ver{font-size:12px;font-weight:700;color:var(--white);background:var(--navy);border:none;border-radius:var(--radius);padding:8px 14px;cursor:pointer}

/* ── MODAL INTERACTIVO ── */
.modal-overlay{display:none;position:fixed;inset:0;z-index:200;background:rgba(5,15,30,0.85);align-items:flex-start;justify-content:center;padding:1.5rem 1rem;overflow-y:auto}
.modal-overlay.open{display:flex}
.modal-box{background:var(--white);border-radius:var(--radius-lg);width:100%;max-width:520px;max-height:95vh;overflow-y:auto;border:1.5px solid var(--soft2);box-shadow:0 24px 80px rgba(0,0,0,0.3)}

.proto-screen{display:none}
.proto-screen.active{display:block}

.m-head{background:var(--navy);padding:1rem;display:flex;align-items:center;justify-content:between;border-radius:var(--radius-lg) var(--radius-lg) 0 0;color:var(--white)}
.m-badge{font-size:12px;color:var(--gold-lt);font-weight:700;display:flex;align-items:center;gap:6px}
.live-dot{width:8px;height:8px;border-radius:50%;background:#4CAF50}
.m-close{background:none;border:none;color:white;font-size:22px;cursor:pointer}

.cert-body{padding:1.25rem}
.coin-row{display:flex;gap:1rem;align-items:center;margin-bottom:1rem}
.cert-vis{width:64px;height:64px;border-radius:50%;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold));display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:800;color:#3A2800;text-align:center}
.cert-info h2{font-size:15px;font-weight:700}
.tag-auth{font-size:10px;background:var(--green-bg);color:var(--green-text);padding:2px 8px;border-radius:10px;font-weight:700}

.divider{border:none;border-top:1px solid var(--soft);margin:1rem 0}
.dgrid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:1rem}
.dcell{background:var(--off-white);padding:8px 12px;border-radius:var(--radius);font-size:12px}
.dcell .l{color:var(--text3);font-size:10px;text-transform:uppercase;font-weight:600}
.dcell .v{font-weight:700;color:var(--navy)}

/* FORMULARIOS */
.f-lbl{font-size:11px;text-transform:uppercase;color:var(--navy);font-weight:700;display:block;margin-bottom:4px}
.f-inp{width:100%;padding:9px 12px;border-radius:var(--radius);border:1.5px solid var(--soft2);font-size:13px;margin-bottom:0.85rem;color:var(--navy)}

/* Radio group envío */
.radio-group{display:flex;flex-direction:column;gap:8px;margin-bottom:1rem}
.radio-box{border:1.5px solid var(--soft2);border-radius:var(--radius);padding:10px;display:flex;gap:10px;cursor:pointer;background:var(--off-white)}
.radio-box.active{border-color:var(--navy);background:var(--white)}
.radio-box h4{font-size:12px;color:var(--navy);font-weight:700}
.radio-box p{font-size:11px;color:var(--text3)}

/* Pestañas de Pago */
.mtabs{display:flex;gap:6px;margin-bottom:1rem}
.mtab{flex:1;padding:9px 5px;border-radius:var(--radius);border:1.5px solid var(--soft2);background:var(--off-white);font-size:12px;font-weight:700;cursor:pointer;text-align:center}
.mtab.active{border-color:var(--navy);background:var(--navy);color:var(--gold-lt)}

/* CONTENEDOR DINÁMICO DE TARJETA / WEB PAY */
.card-form-container{background:#f1f4f8;border:1px solid var(--soft2);border-radius:var(--radius);padding:1rem;margin-bottom:1rem}
.card-row-inline{display:grid;grid-template-columns:1fr 1fr;gap:10px}

/* OTROS MÉTODOS */
.method-panel{display:none;background:#f1f4f8;border:1px solid var(--soft2);border-radius:var(--radius);padding:1rem;margin-bottom:1rem;font-size:12px;color:var(--text2)}
.method-panel.active{display:block}

.btn-confirm{width:100%;padding:12px;border-radius:var(--radius);background:var(--navy);color:var(--gold-lt);border:none;font-size:14px;font-weight:800;cursor:pointer}

/* PANTALLAS PROCESANDO / ÉXITO */
.proc-wrap{padding:3rem 1.25rem;text-align:center}
.spinner{width:40px;height:40px;border:3px solid var(--soft2);border-top-color:var(--navy);border-radius:50%;margin:0 auto 1rem;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}

.ok-wrap{padding:2rem 1.5rem;text-align:center}
.ok-circle{width:50px;height:50px;border-radius:50%;background:var(--green-bg);margin:0 auto 1rem;display:flex;align-items:center;justify-content:center;color:var(--green-text);font-size:22px;font-weight:bold}
.ok-folio{font-family:monospace;font-size:12px;background:var(--off-white);padding:8px;border-radius:var(--radius);margin:1rem 0}
.btn-pdf{padding:12px 24px;border-radius:var(--radius);background:var(--navy);color:var(--gold-lt);font-size:14px;font-weight:800;border:none;cursor:pointer}

.pdf-toast{position:fixed;bottom:2rem;left:50%;transform:translateX(-50%);background:var(--navy);color:var(--gold-lt);padding:10px 20px;border-radius:var(--radius);font-size:13px;z-index:999;opacity:0;transition:opacity .3s;pointer-events:none}
.pdf-toast.show{opacity:1}
</style>
</head>
<body>

<header class="site-header">
  <div class="nav-inner">
    <div class="logo-wrap">
      <div class="logo-coin">MV</div>
      <div class="logo-text"><strong>MonedaViva</strong><span>Casa Moneda de Chile</span></div>
    </div>
  </div>
</header>

<section class="hero">
  <h1>Portal de Certificación QR</h1>
  <p>Verifica la procedencia legítima e inicia la transferencia regulada de activos numismáticos.</p>
</section>

<section class="prod-sec">
  <div class="prod-grid">
    
    <div class="prod-card" onclick="openPrototype('Impreso Conmemorativo: Margot Duhalde', '$12.990', '#SKU-90005045', 'Papel de Seguridad')">
      <div class="prod-img">
        <div style="width:140px; height:85px; background:linear-gradient(135deg, #AED6F1, #D6EAF8); border:1.5px dashed #2E86C1; padding:8px; font-size:10px; color:#1B4F72; font-weight:bold; border-radius:4px; text-align:center;">
          <div style="font-size:7px; color:var(--gold-dk); text-align:right;">280 AÑOS</div>
          Margot Duhalde
          <div style="font-size:6px; font-weight:normal; margin-top:5px;">CASA MONEDA DE CHILE</div>
        </div>
        <span class="prod-tag">Edición 280 años</span>
      </div>
      <div class="prod-info">
        <h3>Impreso Conmemorativo: Margot Duhalde</h3>
        <p>Papel de resguardo con dístico oficial ilustrado en alta fidelidad patrimonial.</p>
        <div class="prod-qr-status">📱 QR Escaneado: Auténtico de Origen</div>
        <div class="prod-footer">
          <div class="prod-price">$12.990 <span>CLP</span></div>
          <button class="btn-ver">Comprar Activo</button>
        </div>
      </div>
    </div>

    <div class="prod-card" onclick="openPrototype('Moneda Bicentenario 2010', '$38.500', '#MV-2010-8841X', 'Cobre-Níquel')">
      <div class="prod-img">
        <div class="prod-coin" style="width:75px;height:75px;">$200<br>2010</div>
        <span class="prod-tag">Colección</span>
      </div>
      <div class="prod-info">
        <h3>Moneda Bicentenario 2010</h3>
        <p>Acuñación premium de circulación limitada para coleccionistas.</p>
        <div class="prod-qr-status">📱 QR Escaneado: Auténtico de Origen</div>
        <div class="prod-footer">
          <div class="prod-price">$38.500 <span>CLP</span></div>
          <button class="btn-ver">Comprar Activo</button>
        </div>
      </div>
    </div>

  </div>
</section>

<div class="modal-overlay" id="modalPrototype">
  <div class="modal-box">
    
    <div class="proto-screen active" id="screenDetail">
      <div class="m-head">
        <div class="m-badge"><div class="live-dot"></div> Auditoría QR MonedaViva</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="cert-body">
        <div class="coin-row">
          <div class="cert-vis" id="modalAssetVisual">MV</div>
          <div class="cert-info">
            <h2 id="modalAssetName">Impreso Conmemorativo: Margot Duhalde</h2>
            <p>ID Registro: <span id="modalAssetId" style="font-weight:bold;">#SKU-90005045</span></p>
            <span class="tag-auth">✓ Firma Criptográfica Verificada</span>
          </div>
        </div>
        <div class="divider"></div>
        <div class="dgrid">
          <div class="dcell"><div class="l">Soporte Material</div><div class="v" id="modalAssetMaterial">Papel de seguridad</div></div>
          <div class="dcell"><div class="l">Entidad Emisora</div><div class="v">Casa de Moneda S.A.</div></div>
        </div>
        <button class="btn-confirm" style="margin-top:0.5rem" onclick="changeScreen('screenPayment')">Iniciar Adquisición (<span id="modalAssetPrice">$12.990</span>)</button>
      </div>
    </div>

    <div class="proto-screen" id="screenPayment">
      <div class="m-head">
        <div class="m-badge">Formulario de Traspaso y Pago Seguro</div>
        <button class="m-close" onclick="closeModal()">&times;</button>
      </div>
      <div class="cert-body">
        
        <label class="f-lbl">Nombre Completo del Comprador</label>
        <input type="text" id="buyerName" class="f-inp" value="Ana María Prado">
        
        <label class="f-lbl">RUT Identificador</label>
        <input type="text" id="buyerRut" class="f-inp" value="15.662.341-K">

        <label class="f-lbl">Modalidad de Despacho Físico (Voluntario)</label>
        <div class="radio-group">
          <div class="radio-box active" id="rBox1" onclick="setShipping('owner')">
            <input type="radio" id="shipOwner" name="shippingMethod" checked>
            <div>
              <h4>El dueño anterior realiza el envío</h4>
              <p>Acuerdo de logística directo, privado y descentralizado entre usuarios.</p>
            </div>
          </div>
          <div class="radio-box" id="rBox2" onclick="setShipping('casamoneda')">
            <input type="radio" id="shipCasa" name="shippingMethod">
            <div>
              <h4>Delegar custodia y despacho a Casa de Moneda</h4>
              <p>La institución centraliza la entrega cobrando el coste base técnico.</p>
            </div>
          </div>
        </div>

        <label class="f-lbl">Seleccione Medio de Pago</label>
        <div class="mtabs">
          <div class="mtab active" id="tab-tbk" onclick="selectMethod('tbk')">Transbank</div>
          <div class="mtab" id="tab-transfer" onclick="selectMethod('transfer')">Transferencia</div>
          <div class="mtab" id="tab-mach" onclick="selectMethod('mach')">MACH</div>
        </div>

        <div id="panel-tbk" class="method-panel active" style="background:#FFF; padding:0; border:none;">
          <div class="card-form-container">
            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;">
              <span style="font-size:11px; font-weight:bold; color:var(--navy-light);">💳 WEBPAY PLUS (CRÉDITO / DÉBITO)</span>
              <span style="font-size:10px; color:#999;">Transacción Encriptada</span>
            </div>
            
            <label class="f-lbl" style="font-size:10px; color:var(--text2)">Número de Tarjeta</label>
            <input type="text" class="f-inp" placeholder="4320 5571 8842 9012" value="4513 9982 4115 6320" style="margin-bottom:0.6rem; letter-spacing:1px;">
            
            <div class="card-row-inline">
              <div>
                <label class="f-lbl" style="font-size:10px; color:var(--text2)">Vencimiento</label>
                <input type="text" class="f-inp" placeholder="MM/AA" value="08/29" style="margin-bottom:0;">
              </div>
              <div>
                <label class="f-lbl" style="font-size:10px; color:var(--text2)">CVV (Cod. Seguridad)</label>
                <input type="password" class="f-inp" placeholder="3 dígitos" value="441" style="margin-bottom:0;">
              </div>
            </div>
          </div>
        </div>

        <div id="panel-transfer" class="method-panel">
          🏛️ <strong>Cuenta Resguardo Casa de Moneda S.A.</strong><br>
          Banco de Chile · Cuenta Corriente Nº 99-1205-01<br>
          <span style="color:var(--text3)">Los fondos quedan retenidos hasta la aprobación del QR físico.</span>
        </div>

        <div id="panel-mach" class="method-panel">
          📱 <strong>Pago Inmediato con MACH</strong><br>
          Al presionar continuar, se generará la solicitud de cobro push directo en tu aplicación MACH Bci vinculada a tu RUT.
        </div>

        <button class="btn-confirm" onclick="processPayment()">Pagar y Confirmar Traspaso</button>
      </div>
    </div>

    <div class="proto-screen" id="screenProcessing">
      <div class="proc-wrap">
        <div class="spinner"></div>
        <h3 id="processingTitle">Autorizando Transacción...</h3>
        <p style="font-size:12px; color:var(--text3); margin-top:4px;">Validando firma bancaria y asignación de dominio...</p>
      </div>
    </div>

    <div class="proto-screen" id="screenSuccess">
      <div class="m-head"><div class="m-badge">✓ Operación Aprobada por Operador</div></div>
      <div class="ok-wrap">
        <div class="ok-circle">✓</div>
        <h2>¡Propiedad Registrada!</h2>
        <p style="font-size:13px; color:var(--text2)">El certificado amarra la numeración QR a tus credenciales.</p>
        <div class="ok-folio">Folio Auditoría:<br><strong id="folioCode">CMMC-9002-2026</strong></div>
        <button class="btn-pdf" onclick="generateOfficialPDF()">📄 Descargar Certificado Oficial (PDF)</button>
      </div>
    </div>

  </div>
</div>

<div class="pdf-toast" id="toast">Documento PDF generado y descargado</div>

<script>
  let currentAssetName = ""; let currentAssetPrice = ""; let currentAssetId = ""; let currentAssetMaterial = "";
  let selectedMethodName = "Transbank Webpay Plus (Tarjeta Credito/Debito)";
  let selectedShippingLabel = "El dueño anterior realiza el envío de forma directa (Acuerdo privado)";

  function openPrototype(name, price, id, material) {
    currentAssetName = name; currentAssetPrice = price; currentAssetId = id; currentAssetMaterial = material;
    document.getElementById('modalAssetName').innerText = name;
    document.getElementById('modalAssetPrice').innerText = price;
    document.getElementById('modalAssetId').innerText = id;
    document.getElementById('modalAssetMaterial').innerText = material;
    
    const visual = document.getElementById('modalAssetVisual');
    visual.innerText = name.includes('Duhalde') ? "Duhalde" : "$200";
    visual.style.background = name.includes('Duhalde') ? 'linear-gradient(135deg, #AED6F1, #D6EAF8)' : 'radial-gradient(circle at 33% 33%,#F7E48A,var(--gold))';

    document.getElementById('modalPrototype').classList.add('open');
    changeScreen('screenDetail');
  }

  function closeModal() { document.getElementById('modalPrototype').classList.remove('open'); }
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
    document.getElementById(`tab-${method}`).classList.add('active');
    
    // Ocultar todos los paneles informativos/casilleros
    document.getElementById('panel-tbk').style.display = 'none';
    document.getElementById('panel-transfer').classList.remove('active');
    document.getElementById('panel-mach').classList.remove('active');

    if(method === 'tbk') {
      document.getElementById('panel-tbk').style.display = 'block';
      selectedMethodName = "Transbank Webpay Plus (Tarjeta Crédito/Débito)";
    } else if(method === 'transfer') {
      document.getElementById('panel-transfer').classList.add('active');
      selectedMethodName = "Transferencia Bancaria Directa";
    } else if(method === 'mach') {
      document.getElementById('panel-mach').classList.add('active');
      selectedMethodName = "Billetera Digital MACH Bci";
    }
  }

  function processPayment() {
    document.getElementById('processingTitle').innerText = `Conectando con ${selectedMethodName}...`;
    changeScreen('screenProcessing');
    setTimeout(() => {
      document.getElementById('folioCode').innerText = 'CMMC-' + Math.floor(1000 + Math.random() * 9000) + '-2026';
      changeScreen('screenSuccess');
    }, 1600);
  }

  function generateOfficialPDF() {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();
    const buyer = document.getElementById('buyerName').value || 'Ana María Prado';
    const rut = document.getElementById('buyerRut').value || '15.662.341-K';
    const folio = document.getElementById('folioCode').innerText;
    const dateStr = new Date().toLocaleDateString('es-CL');

    // Estilo PDF
    doc.setFillColor(11, 31, 58); doc.rect(0, 0, 210, 40, 'F');
    doc.setTextColor(255, 255, 255); doc.setFont("Helvetica", "bold"); doc.setFontSize(22);
    doc.text("CASA MONEDA DE CHILE", 20, 25);
    doc.setFontSize(10); doc.setTextColor(201, 168, 76);
    doc.text("SISTEMA REGULADO DE TRAZABILIDAD NUMISMÁTICA · MONEDAVIVA", 20, 32);

    doc.setTextColor(11, 31, 58); doc.setFontSize(14); doc.text("CERTIFICADO OFICIAL DE ADQUISICIÓN Y DOMINIO DIGITAL", 20, 58);
    doc.setDrawColor(201, 168, 76); doc.setLineWidth(0.8); doc.line(20, 62, 190, 62);

    doc.setFontSize(11); doc.setTextColor(58, 80, 112); doc.text("Detalle del Activo Auditado mediante Código QR:", 20, 72);
    doc.setFont("Helvetica", "normal"); doc.setFontSize(10); doc.setTextColor(11, 31, 58);
    doc.text(`• Pieza Numismática:   ${currentAssetName}`, 24, 82);
    doc.text(`• ID Registro de Serie: ${currentAssetId}`, 24, 89);
    doc.text(`• Material Evaluado:   ${currentAssetMaterial}`, 24, 96);
    doc.text(`• Estatus Autenticidad: Validado Conforme (100% Original de Origen)`, 24, 103);

    // Cuadro Adquirente
    doc.setFillColor(244, 247, 251); doc.rect(20, 112, 170, 40, 'F');
    doc.setDrawColor(212, 225, 240); doc.rect(20, 112, 170, 40, 'S');
    doc.setTextColor(11, 31, 58); doc.setFont("Helvetica", "bold"); doc.text("NUEVO TITULAR INSCRITO", 25, 122);
    doc.setFont("Helvetica", "normal"); doc.text(`Propietario Legal: ${buyer}`, 25, 131);
    doc.text(`RUT / Cédula:       ${rut}`, 25, 138);

    doc.setFont("Helvetica", "bold"); doc.text("Logística Física Solicitada:", 20, 168);
    doc.setFont("Helvetica", "normal"); doc.text(selectedShippingLabel, 20, 175);

    doc.setFont("Helvetica", "bold"); doc.text("Comprobante Técnico Financiero:", 20, 192);
    doc.setFont("Helvetica", "normal");
    doc.text(`• Código de Liquidación:  ${folio}`, 20, 200);
    doc.text(`• Canal / Pasarela:      ${selectedMethodName}`, 20, 207);
    doc.text(`• Fecha de Timbrado:     ${dateStr}`, 20, 214);

    doc.setDrawColor(212, 225, 240); doc.line(20, 245, 85, 245);
    doc.setFontSize(8.5); doc.text("Firma de Resguardo Tecnológico", 20, 251);
    doc.setFont("Helvetica", "bold"); doc.text("Casa Moneda de Chile S.A.", 20, 256);

    doc.save(`Certificado-QR-${currentAssetId}.pdf`);
    const toast = document.getElementById('toast'); toast.classList.add('show');
    setTimeout(() => toast.classList.remove('show'), 3000);
  }
</script>

</body>
</html>
