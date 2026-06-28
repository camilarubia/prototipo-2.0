<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MonedaViva · Casa Moneda de Chile</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --navy:#0B1F3A;--navy2:#122847;--navy3:#1A3A5C;--navy4:#234E75;
  --nlight:#2E6DA4;--white:#FFFFFF;--offwhite:#F4F7FB;--soft:#E8EEF6;--soft2:#D0DCF0;
  --gold:#C9A84C;--goldlt:#E2C06A;--golddk:#9A7530;
  --text:#0B1F3A;--text2:#3A5070;--text3:#6B87A8;
  --bdr:rgba(11,31,58,0.10);--bdr2:rgba(11,31,58,0.20);
  --r:10px;--rlg:16px;
  --gbg:#EAF3DE;--gtx:#2E6B0F;--gbr:#8CBF50;
  --abg:#FEF3DC;--atx:#7A5200;--abr:#E8B84B;
  --rbg:#FDECEA;--rtx:#9B2020;--rbr:#E57373;
}
html{scroll-behavior:smooth}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Helvetica,sans-serif;background:var(--offwhite);color:var(--text);line-height:1.65}
a{color:inherit;text-decoration:none}
button{font-family:inherit}

/* ── NAV ── */
.nav{background:var(--navy);position:sticky;top:0;z-index:200;border-bottom:3px solid var(--gold)}
.nav-in{max-width:1160px;margin:0 auto;padding:0 1.5rem;display:flex;align-items:center;justify-content:space-between;height:68px}
.logo{display:flex;align-items:center;gap:14px}
/* Logo SVG oficial CM */
.logo-svg{width:44px;height:44px;flex-shrink:0}
.logo-txt strong{display:block;font-size:18px;font-weight:800;color:var(--white);letter-spacing:-.01em}
.logo-txt span{font-size:10px;color:var(--goldlt);letter-spacing:.1em;text-transform:uppercase}
.nav-links{display:flex;align-items:center;gap:1.75rem}
.nav-links a{font-size:13px;font-weight:500;color:rgba(255,255,255,0.6);transition:color .15s}
.nav-links a:hover,.nav-links a.active{color:var(--goldlt)}
.nav-cta{background:var(--gold);color:var(--navy)!important;font-weight:800!important;padding:8px 18px;border-radius:var(--r);font-size:13px!important}
.nav-cta:hover{background:var(--goldlt)!important}
.nav-mb{display:none;background:none;border:none;color:var(--goldlt);font-size:24px;cursor:pointer}
@media(max-width:740px){.nav-links{display:none}.nav-mb{display:block}}

/* ── HERO ── */
.hero{background:var(--navy);padding:5rem 1.5rem 0;text-align:center;position:relative;overflow:hidden}
.hero::after{content:'';display:block;height:56px;background:linear-gradient(to bottom right,var(--navy) 49.5%,var(--offwhite) 50%)}
.hero-eb{display:inline-flex;align-items:center;gap:7px;font-size:11px;color:var(--goldlt);text-transform:uppercase;letter-spacing:.14em;border:1px solid rgba(201,168,76,.35);border-radius:20px;padding:5px 14px;margin-bottom:1.75rem}
.hero-dot{width:7px;height:7px;border-radius:50%;background:#4CAF50;animation:pulse 1.6s infinite}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}
.hero h1{font-size:clamp(2.2rem,5vw,3.8rem);font-weight:800;color:var(--white);line-height:1.1;margin-bottom:1rem;letter-spacing:-.025em}
.hero h1 em{color:var(--goldlt);font-style:normal}
.hero-sub{font-size:17px;color:rgba(255,255,255,.55);max-width:560px;margin:0 auto 2.5rem;line-height:1.75}
.hero-acts{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;margin-bottom:3.5rem}
.btn-gold{background:var(--gold);color:var(--navy);font-weight:800;padding:14px 30px;border-radius:var(--r);font-size:15px;border:none;cursor:pointer;transition:background .15s;display:inline-block}
.btn-gold:hover{background:var(--goldlt)}
.btn-ghost{background:transparent;color:rgba(255,255,255,.7);font-weight:500;padding:14px 30px;border-radius:var(--r);font-size:15px;border:1.5px solid rgba(255,255,255,.18);cursor:pointer;transition:all .15s;display:inline-block}
.btn-ghost:hover{border-color:var(--goldlt);color:var(--goldlt)}
.hero-coins{display:flex;align-items:flex-end;justify-content:center;gap:1.5rem}
.hc{border-radius:50%;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800);border:2.5px solid var(--goldlt);display:flex;align-items:center;justify-content:center;font-weight:800;color:#3A2800;text-align:center;line-height:1.3;flex-shrink:0;box-shadow:0 6px 24px rgba(0,0,0,.35)}
.hc-lg{width:118px;height:118px;font-size:12px;animation:float 3.2s ease-in-out infinite}
.hc-md{width:84px;height:84px;font-size:10px;animation:float 3.6s ease-in-out infinite .5s;opacity:.88}
.hc-sm{width:60px;height:60px;font-size:9px;animation:float 2.9s ease-in-out infinite 1s;opacity:.72}
@keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-10px)}}

/* ── STATS ── */
.stats{background:var(--navy2);border-bottom:1px solid var(--navy3);padding:1.4rem}
.stats-in{max-width:1160px;margin:0 auto;display:flex;align-items:center;justify-content:space-around;gap:1rem;flex-wrap:wrap}
.stat-n{font-size:23px;font-weight:800;color:var(--goldlt)}
.stat-l{font-size:10px;color:rgba(255,255,255,.4);text-transform:uppercase;letter-spacing:.08em;margin-top:3px}

/* ── GENERAL SEC ── */
.sec{padding:5.5rem 1.5rem}
.sec-in{max-width:1160px;margin:0 auto}
.eb{font-size:11px;text-transform:uppercase;letter-spacing:.12em;color:var(--nlight);font-weight:700;margin-bottom:.6rem}
.st{font-size:clamp(1.7rem,3vw,2.5rem);font-weight:800;color:var(--navy);margin-bottom:1rem;line-height:1.15;letter-spacing:-.02em}
.ss{font-size:16px;color:var(--text2);max-width:580px;line-height:1.75}

/* ── SLIDE: VENDE TU COLECCION ── */
.sell-slide{background:linear-gradient(135deg,var(--navy) 0%,var(--navy3) 60%,var(--navy4) 100%);padding:5.5rem 1.5rem;position:relative;overflow:hidden}
.sell-slide::before{content:'';position:absolute;right:-80px;top:-80px;width:400px;height:400px;border-radius:50%;background:rgba(201,168,76,.07);pointer-events:none}
.sell-in{max-width:1160px;margin:0 auto;display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:center}
@media(max-width:760px){.sell-in{grid-template-columns:1fr}}
.sell-text .st{color:var(--white)}
.sell-text .ss{color:rgba(255,255,255,.55)}
.sell-steps{margin-top:2rem;display:flex;flex-direction:column;gap:.9rem}
.sell-step{display:flex;align-items:flex-start;gap:12px}
.ss-num{width:28px;height:28px;border-radius:50%;background:var(--gold);color:var(--navy);font-size:12px;font-weight:800;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px}
.ss-txt strong{font-size:13px;font-weight:700;color:var(--white);display:block;margin-bottom:2px}
.ss-txt span{font-size:12px;color:rgba(255,255,255,.5)}
.sell-cta{margin-top:2.5rem;display:flex;gap:10px;flex-wrap:wrap}
/* Cards trust */
.trust-cards{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.tc{background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.12);border-radius:var(--rlg);padding:1.25rem}
.tc-icon{font-size:24px;margin-bottom:.75rem}
.tc h4{font-size:13px;font-weight:700;color:var(--white);margin-bottom:.4rem}
.tc p{font-size:12px;color:rgba(255,255,255,.45);line-height:1.6}

/* ── GALERIA ── */
.gallery-sec{background:var(--white)}
.gal-tabs{display:flex;gap:8px;margin-top:2rem;flex-wrap:wrap}
.gtab{padding:7px 16px;border-radius:20px;border:1.5px solid var(--soft2);background:var(--offwhite);font-size:12px;font-weight:600;color:var(--text2);cursor:pointer;transition:all .15s}
.gtab.active{background:var(--navy);color:var(--goldlt);border-color:var(--navy)}
.gal-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(180px,1fr));gap:1rem;margin-top:1.5rem}
.gal-item{background:var(--offwhite);border:1.5px solid var(--soft2);border-radius:var(--rlg);overflow:hidden;cursor:pointer;transition:transform .2s,box-shadow .2s}
.gal-item:hover{transform:translateY(-4px);box-shadow:0 12px 32px rgba(11,31,58,.12)}
.gal-img{height:130px;display:flex;align-items:center;justify-content:center;position:relative;overflow:hidden}
.gal-badge{position:absolute;top:8px;right:8px;font-size:9px;font-weight:700;padding:2px 7px;border-radius:20px}
.badge-cert{background:var(--gbg);color:var(--gtx);border:1px solid var(--gbr)}
.badge-oro{background:var(--abg);color:var(--atx);border:1px solid var(--abr)}
.badge-bill{background:#EEF2FF;color:#3730A3;border:1px solid #A5B4FC}
.gal-info{padding:.8rem .9rem}
.gal-info h4{font-size:12px;font-weight:700;color:var(--navy);margin-bottom:2px}
.gal-info p{font-size:11px;color:var(--text3)}
.gal-price{font-size:13px;font-weight:800;color:var(--navy);margin-top:.4rem}
/* Billetes SVG art */
.bill-art{width:120px;height:65px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:700;text-align:center;line-height:1.4;position:relative;overflow:hidden}
/* Moneda art */
.mon-art{border-radius:50%;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800);border:2px solid var(--goldlt);display:flex;align-items:center;justify-content:center;font-weight:800;color:#3A2800;text-align:center;line-height:1.3}
/* Oro art */
.oro-art{border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:800;color:#3A2800;text-align:center;line-height:1.4}

/* ── COMO FUNCIONA ── */
.how-sec{background:var(--offwhite)}
.steps-g{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:1.5rem;margin-top:3rem}
.step-c{background:var(--white);border:1.5px solid var(--soft2);border-radius:var(--rlg);padding:1.75rem}
.snum{width:38px;height:38px;border-radius:50%;background:var(--navy);color:var(--goldlt);font-size:15px;font-weight:800;display:flex;align-items:center;justify-content:center;margin-bottom:1.1rem}
.step-c h3{font-size:15px;font-weight:700;color:var(--navy);margin-bottom:.5rem}
.step-c p{font-size:13px;color:var(--text2);line-height:1.65}

/* ── BENEFICIOS ── */
.ben-sec{background:var(--white)}
.ben-g{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:1.25rem;margin-top:2.5rem}
.ben-c{background:var(--offwhite);border:1.5px solid var(--soft2);border-radius:var(--rlg);padding:1.6rem}
.ben-icon{width:46px;height:46px;border-radius:12px;background:var(--navy);display:flex;align-items:center;justify-content:center;font-size:22px;margin-bottom:1.1rem}
.ben-c h3{font-size:15px;font-weight:700;color:var(--navy);margin-bottom:.5rem}
.ben-c p{font-size:13px;color:var(--text2);line-height:1.65}
.ben-n{font-size:24px;font-weight:900;color:var(--navy);margin-top:.85rem}
.ben-nl{font-size:11px;color:var(--text3)}

/* ── CTA ── */
.cta-sec{background:var(--navy2);border-top:3px solid var(--gold);padding:5rem 1.5rem;text-align:center}
.cta-sec h2{font-size:clamp(1.7rem,3vw,2.5rem);font-weight:800;color:var(--white);margin-bottom:1rem;letter-spacing:-.02em}
.cta-sec p{font-size:16px;color:rgba(255,255,255,.5);max-width:500px;margin:0 auto 2rem}
.cta-acts{display:flex;gap:12px;justify-content:center;flex-wrap:wrap}

/* ── FOOTER ── */
.foot{background:var(--navy);border-top:1px solid var(--navy3);padding:2.5rem 1.5rem}
.foot-in{max-width:1160px;margin:0 auto;display:flex;align-items:flex-start;justify-content:space-between;gap:2rem;flex-wrap:wrap}
.foot-logo{font-size:19px;font-weight:800;color:var(--goldlt)}
.foot-copy{font-size:11px;color:rgba(255,255,255,.25);margin-top:.3rem;line-height:1.6}
.foot-links{display:flex;gap:1.5rem;flex-wrap:wrap}
.foot-links a{font-size:12px;color:rgba(255,255,255,.38);transition:color .15s}
.foot-links a:hover{color:var(--goldlt)}

/* ════════════ MODAL ════════════ */
.overlay{display:none;position:fixed;inset:0;z-index:300;background:rgba(5,15,30,.9);align-items:flex-start;justify-content:center;padding:1.5rem 1rem;overflow-y:auto}
.overlay.open{display:flex}
.mbox{background:var(--white);border-radius:var(--rlg);width:100%;max-width:520px;max-height:93vh;overflow-y:auto;margin:auto;box-shadow:0 30px 90px rgba(0,0,0,.4);border:1.5px solid var(--soft2)}
.mscreen{display:none}
.mscreen.active{display:block;animation:fadeUp .22s ease}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}

/* Modal header */
.mh{background:var(--navy);padding:1rem 1.25rem;display:flex;align-items:center;justify-content:space-between;border-radius:var(--rlg) var(--rlg) 0 0}
.mh-badge{display:flex;align-items:center;gap:7px;font-size:11px;color:var(--goldlt);text-transform:uppercase;letter-spacing:.09em;font-weight:700}
.mh-dot{width:7px;height:7px;border-radius:50%;background:#4CAF50;animation:pulse 1.6s infinite}
.mclose{background:none;border:none;color:rgba(255,255,255,.4);font-size:20px;cursor:pointer;line-height:1;transition:color .15s}
.mclose:hover{color:var(--white)}

/* Cert screen */
.cert-body{padding:1.35rem}
.cref-row{display:flex;gap:1.1rem;align-items:flex-start;margin-bottom:1.2rem}
.cert-vis{width:72px;height:72px;border-radius:50%;flex-shrink:0;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800);border:2.5px solid var(--goldlt);display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:800;color:#3A2800;text-align:center;line-height:1.3}
.cert-info h2{font-size:15px;font-weight:700;color:var(--navy);margin-bottom:4px}
.cert-info p{font-size:12px;color:var(--text2);margin-bottom:7px}
.tag-auth{display:inline-flex;align-items:center;gap:4px;font-size:10px;font-weight:700;padding:3px 10px;border-radius:20px;background:var(--gbg);color:var(--gtx);border:1px solid var(--gbr)}
.div{border:none;border-top:1.5px solid var(--soft);margin:.85rem 0}
.dgrid{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-bottom:1rem}
.dc{background:var(--offwhite);border-radius:var(--r);padding:9px 11px;border:1px solid var(--soft2)}
.dc .l{font-size:9px;color:var(--text3);text-transform:uppercase;letter-spacing:.07em;margin-bottom:3px;font-weight:600}
.dc .v{font-size:12px;font-weight:600;color:var(--navy)}
.ow-lbl{font-size:9px;color:var(--text3);text-transform:uppercase;letter-spacing:.07em;font-weight:600;margin-bottom:7px}
.ow-row{display:flex;align-items:center;gap:9px;padding:6px 0;border-bottom:1px solid var(--soft);font-size:11px}
.ow-row:last-child{border-bottom:none}
.ow-av{width:26px;height:26px;border-radius:50%;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:700}
.ow-name{flex:1;color:var(--navy)}
.ow-dt{color:var(--text3);font-size:10px}
.ow-p{font-weight:700;color:var(--navy);font-size:11px;font-family:monospace}
.info-note{font-size:11px;border-radius:var(--r);padding:9px 11px;margin:.8rem 0;display:flex;gap:7px;line-height:1.55}
.note-blue{background:#E6F1FB;border:1px solid #85B7EB;color:#0C447C}
.note-gold{background:var(--abg);border:1px solid var(--abr);color:var(--atx)}

/* Cert footer */
.cert-foot{display:flex;gap:8px;padding:1rem 1.25rem;background:var(--offwhite);border-top:1.5px solid var(--soft2);flex-wrap:wrap;border-radius:0 0 var(--rlg) var(--rlg)}
.btn-sm{flex:1;min-width:100px;padding:9px 10px;border-radius:var(--r);border:1.5px solid var(--soft2);background:var(--white);font-size:12px;font-weight:600;cursor:pointer;color:var(--text2);text-align:center;transition:all .15s}
.btn-sm:hover{border-color:var(--navy);color:var(--navy)}
.btn-navy{flex:1;min-width:140px;padding:9px 10px;border-radius:var(--r);border:none;background:var(--navy);font-size:12px;font-weight:700;cursor:pointer;color:var(--goldlt);text-align:center;transition:opacity .15s}
.btn-navy:hover{opacity:.85}

/* Pay screen */
.ph{background:var(--navy);padding:.9rem 1.25rem;display:flex;align-items:center;gap:8px;border-radius:var(--rlg) var(--rlg) 0 0}
.ph h3{font-size:14px;font-weight:700;color:var(--goldlt);flex:1}
.back-btn{background:none;border:none;color:rgba(255,255,255,.45);font-size:18px;cursor:pointer;line-height:1;transition:color .15s}
.back-btn:hover{color:var(--white)}
.pb{padding:1.35rem}
.mini-row{display:flex;align-items:center;gap:11px;margin-bottom:1.2rem;padding:9px 11px;background:var(--offwhite);border-radius:var(--r);border:1.5px solid var(--soft2)}
.mini-coin{width:38px;height:38px;border-radius:50%;background:radial-gradient(circle at 33% 33%,#F7E48A,var(--gold) 55%,#7A5800);border:1.5px solid var(--goldlt);flex-shrink:0}
.mini-row p{font-size:13px;font-weight:700;color:var(--navy)}
.mini-row span{font-size:11px;color:var(--text3)}
.fl{font-size:10px;text-transform:uppercase;letter-spacing:.07em;color:var(--text2);font-weight:600;display:block;margin-bottom:5px}
.fi{width:100%;padding:10px 12px;border-radius:var(--r);border:1.5px solid var(--soft2);background:var(--white);color:var(--navy);font-size:13px;font-weight:500;margin-bottom:1rem;transition:border-color .15s;font-family:inherit}
.fi:focus{outline:none;border-color:var(--nlight)}
.fi option{background:var(--white)}
.mtabs{display:flex;gap:6px;margin-bottom:1rem}
.mtab{flex:1;padding:8px 5px;border-radius:var(--r);border:1.5px solid var(--soft2);background:var(--offwhite);font-size:11px;font-weight:600;cursor:pointer;color:var(--text2);text-align:center;transition:all .15s}
.mtab.active{border-color:var(--navy);background:var(--navy);color:var(--goldlt)}
.crow{display:grid;grid-template-columns:1fr 1fr;gap:8px}

/* Envio options */
.ship-opts{display:flex;flex-direction:column;gap:9px;margin-bottom:1.1rem}
.ship-opt{border:2px solid var(--soft2);border-radius:var(--rlg);padding:1rem;cursor:pointer;transition:all .18s;position:relative}
.ship-opt.sel{border-color:var(--navy);background:#EEF4FF}
.ship-opt-head{display:flex;align-items:flex-start;gap:10px}
.ship-rb{width:18px;height:18px;border:2px solid var(--soft2);border-radius:50%;flex-shrink:0;margin-top:1px;display:flex;align-items:center;justify-content:center;transition:all .18s;background:var(--white)}
.ship-rb.on{border-color:var(--navy);background:var(--navy)}
.ship-rb.on::after{content:'';width:7px;height:7px;border-radius:50%;background:var(--goldlt);display:block}
.ship-lbl strong{font-size:13px;font-weight:700;color:var(--navy);display:block;margin-bottom:2px}
.ship-lbl span{font-size:11px;color:var(--text3)}
.ship-badge{display:inline-block;font-size:10px;font-weight:700;padding:2px 8px;border-radius:20px;background:var(--abg);color:var(--atx);border:1px solid var(--abr);margin-top:4px}
.ship-detail{font-size:12px;color:var(--text2);line-height:1.6;margin-top:.75rem;padding-top:.75rem;border-top:1px solid var(--soft2);display:none}
.ship-detail.show{display:block}
.ship-security{background:var(--gbg);border:1px solid var(--gbr);border-radius:var(--r);padding:7px 10px;font-size:11px;color:var(--gtx);margin-top:.5rem;font-weight:600}

/* Resumen */
.ps{background:var(--offwhite);border-radius:var(--r);border:1.5px solid var(--soft2);padding:.95rem 1.1rem;margin-bottom:1rem}
.ps-t{font-size:10px;text-transform:uppercase;letter-spacing:.07em;color:var(--text3);font-weight:600;margin-bottom:8px}
.ps-r{display:flex;justify-content:space-between;font-size:12px;padding:3.5px 0}
.ps-r.tot{border-top:1.5px solid var(--soft2);margin-top:5px;padding-top:7px;font-weight:800;font-size:14px;color:var(--navy)}
.ps-r span:last-child{font-family:monospace}
.ps-m{color:var(--text3)}
.tbk-brand{display:flex;align-items:center;gap:7px;font-size:10px;color:var(--text3);margin-bottom:1rem}
.tbk-logo{background:#E60012;color:#fff;font-size:9px;font-weight:800;padding:2px 7px;border-radius:3px;letter-spacing:.04em}
.btn-confirm{width:100%;padding:13px;border-radius:var(--r);background:var(--navy);color:var(--goldlt);border:none;font-size:14px;font-weight:800;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:7px;transition:opacity .15s}
.btn-confirm:hover{opacity:.85}

/* Processing */
.proc-wrap{padding:3rem 1.25rem;text-align:center}
.spin{width:46px;height:46px;border:3.5px solid var(--soft2);border-top-color:var(--navy);border-radius:50%;margin:0 auto 1.4rem;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.vsteps{list-style:none;max-width:260px;margin:1.25rem auto 0;text-align:left}
.vsteps li{font-size:12px;color:var(--text3);padding:6px 0;display:flex;gap:8px;border-bottom:1px solid var(--soft);transition:color .3s}
.vsteps li:last-child{border-bottom:none}
.vsteps li.done{color:var(--navy);font-weight:600}

/* Success */
.ok-wrap{padding:2.5rem 1.5rem;text-align:center}
.ok-circle{width:64px;height:64px;border-radius:50%;background:var(--gbg);border:2px solid var(--gbr);margin:0 auto 1.25rem;display:flex;align-items:center;justify-content:center}
.ok-circle svg{width:28px;height:28px;stroke:var(--gtx);fill:none;stroke-width:2.5}
.ok-folio{font-family:monospace;font-size:10px;color:var(--text3);background:var(--offwhite);padding:8px 12px;border-radius:var(--r);border:1.5px solid var(--soft2);margin:.9rem auto;max-width:320px;word-break:break-all;line-height:1.75}
.ok-log-note{background:var(--abg);border:1px solid var(--abr);border-radius:var(--r);padding:9px 12px;font-size:12px;color:var(--atx);margin-bottom:1rem;text-align:left;display:none}
.ok-log-note.show{display:block}
/* PDF button — solo post-venta */
.btn-pdf{display:inline-flex;align-items:center;gap:8px;padding:13px 26px;border-radius:var(--r);background:var(--navy);color:var(--goldlt);border:none;font-size:14px;font-weight:800;cursor:pointer;transition:opacity .15s;margin-top:.5rem}
.btn-pdf:hover{opacity:.85}
.ok-acts{display:flex;gap:8px;justify-content:center;margin-top:1rem;flex-wrap:wrap}

/* PDF viewer modal */
.pdf-viewer{display:none;position:fixed;inset:0;z-index:400;background:rgba(5,15,30,.95);align-items:flex-start;justify-content:center;padding:1.5rem 1rem;overflow-y:auto}
.pdf-viewer.open{display:flex}
.pdf-box{background:var(--white);border-radius:var(--rlg);width:100%;max-width:580px;margin:auto;overflow:hidden}
.pdf-head{background:var(--navy);padding:1rem 1.25rem;display:flex;align-items:center;justify-content:space-between}
.pdf-head h3{font-size:14px;font-weight:700;color:var(--goldlt)}
.pdf-content{padding:1.5rem;font-size:13px;color:var(--text)}
/* Certificado visual */
.cert-doc{border:2px solid var(--navy);border-radius:var(--r);overflow:hidden}
.cert-doc-head{background:var(--navy);padding:1.25rem;text-align:center}
.cert-doc-head .cm-name{font-size:15px;font-weight:800;color:var(--white);letter-spacing:.02em}
.cert-doc-head .cm-sub{font-size:9px;color:var(--goldlt);letter-spacing:.12em;text-transform:uppercase;margin-top:3px}
.cert-doc-gold{height:3px;background:var(--gold)}
.cert-doc-body{padding:1.5rem}
.cert-qr-row{display:flex;gap:1.5rem;align-items:center;margin-bottom:1.25rem}
.cert-qr-box{flex-shrink:0;background:var(--white);padding:6px;border:1px solid var(--soft2);border-radius:6px}
#qrcode-cert canvas,#qrcode-cert img{display:block}
.cert-doc-title{font-size:17px;font-weight:800;color:var(--navy);margin-bottom:.25rem}
.cert-doc-sub{font-size:12px;color:var(--text2);margin-bottom:.75rem}
.cert-auth-badge{display:inline-flex;align-items:center;gap:5px;font-size:11px;font-weight:700;padding:4px 12px;border-radius:20px;background:var(--gbg);color:var(--gtx);border:1px solid var(--gbr)}
.cert-dgrid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:1.1rem}
.cert-dc{background:var(--offwhite);border-radius:var(--r);padding:8px 10px;border:1px solid var(--soft2)}
.cert-dc .l{font-size:9px;color:var(--text3);text-transform:uppercase;letter-spacing:.07em;margin-bottom:3px;font-weight:600}
.cert-dc .v{font-size:11px;font-weight:600;color:var(--navy)}
.cert-ow-sec{margin-bottom:1.1rem}
.cert-ow-lbl{font-size:9px;color:var(--text3);text-transform:uppercase;letter-spacing:.07em;font-weight:600;margin-bottom:7px}
.cert-ow-row{display:flex;align-items:center;gap:8px;padding:5px 0;border-bottom:1px solid var(--soft);font-size:11px}
.cert-ow-row:last-child{border-bottom:none}
.cert-ow-av{width:24px;height:24px;border-radius:50%;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:700}
.cert-new-owner{background:var(--soft);border:1.5px solid var(--navy);border-radius:var(--r);padding:8px 10px;margin-top:4px;font-size:11px}
.cert-new-owner strong{color:var(--navy)}
.cert-code{background:var(--offwhite);border:1px solid var(--soft2);border-radius:var(--r);padding:8px 10px;font-family:monospace;font-size:9px;color:var(--text3);word-break:break-all;line-height:1.6;margin-bottom:1rem}
.cert-doc-foot{background:var(--navy);padding:.85rem 1.25rem;text-align:center}
.cert-doc-foot p{font-size:9px;color:rgba(255,255,255,.4);line-height:1.6}
.cert-doc-foot .cm-url{font-size:10px;color:var(--goldlt);font-weight:600;margin-top:3px}
.pdf-acts{display:flex;gap:8px;padding:1.25rem;background:var(--offwhite);border-top:1.5px solid var(--soft2);flex-wrap:wrap}

/* Toast */
.toast{position:fixed;bottom:2rem;left:50%;transform:translateX(-50%);background:var(--navy);color:var(--goldlt);border:1.5px solid var(--navy3);padding:10px 20px;border-radius:var(--r);font-size:13px;font-weight:600;z-index:999;opacity:0;transition:opacity .3s;pointer-events:none;white-space:nowrap}
.toast.show{opacity:1}

@media(max-width:600px){.sec{padding:4rem 1rem}.sell-slide{padding:4rem 1rem}.hero{padding:4rem 1rem 0}.hc-sm{display:none}.trust-cards{grid-template-columns:1fr}}
</style>
</head>
<body>

<!-- NAV -->
<header class="nav">
  <div class="nav-in">
    <div class="logo">
      <!-- Logo oficial CM dibujado en SVG -->
      <svg class="logo-svg" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="50" cy="50" r="48" fill="#0B1F3A" stroke="#C9A84C" stroke-width="3"/>
        <circle cx="50" cy="50" r="38" fill="none" stroke="#C9A84C" stroke-width="1.2"/>
        <text x="50" y="38" font-family="Georgia,serif" font-size="11" font-weight="bold" fill="#C9A84C" text-anchor="middle">CASA</text>
        <text x="50" y="50" font-family="Georgia,serif" font-size="11" font-weight="bold" fill="#C9A84C" text-anchor="middle">MONEDA</text>
        <text x="50" y="62" font-family="Georgia,serif" font-size="8" fill="#C9A84C" text-anchor="middle">DE CHILE</text>
        <text x="50" y="75" font-family="Georgia,serif" font-size="7" fill="#E2C06A" text-anchor="middle">EST. 1743</text>
      </svg>
      <div class="logo-txt">
        <strong>MonedaViva</strong>
        <span>Casa Moneda de Chile</span>
      </div>
    </div>
    <nav class="nav-links">
      <a href="#galeria">Galeria</a>
      <a href="#vender">Vende aqui</a>
      <a href="#como-funciona">Como funciona</a>
      <a href="#beneficios">Beneficios</a>
      <a href="#vender" class="nav-cta">Vender mi coleccion</a>
    </nav>
    <button class="nav-mb" onclick="alert('Menu movil — implementar en produccion')">&#9776;</button>
  </div>
</header>

<!-- HERO -->
<section class="hero" id="inicio">
  <div class="hero-eb"><div class="hero-dot"></div>Plataforma oficial de coleccionismo · Casa Moneda de Chile</div>
  <h1>Cada pieza tiene historia.<br><em>Ahora tambien tiene mercado.</em></h1>
  <p class="hero-sub">Verifica, vende y certifica tus monedas, medallas, billetes conmemorativos y oro con respaldo oficial de Casa Moneda de Chile.</p>
  <div class="hero-acts">
    <button class="btn-gold" onclick="document.getElementById('vender').scrollIntoView({behavior:'smooth'})">Vender mi coleccion</button>
    <a href="#galeria" class="btn-ghost">Ver galeria &#8595;</a>
  </div>
  <div class="hero-coins" aria-hidden="true">
    <div class="hc hc-sm" style="font-size:9px">$100<br>1998</div>
    <div class="hc hc-md" style="font-size:10px">$200<br>2010</div>
    <div class="hc hc-lg" style="font-size:11px">Bicentenario<br>$500<br>Chile</div>
    <div class="hc hc-md" style="font-size:10px">Oro<br>999,9</div>
    <div class="hc hc-sm" style="font-size:9px">Medalla<br>Bronce</div>
  </div>
</section>

<!-- STATS -->
<div class="stats">
  <div class="stats-in">
    <div class="stat-item"><div class="stat-n">+280</div><div class="stat-l">Anos de historia</div></div>
    <div class="stat-item"><div class="stat-n">111</div><div class="stat-l">Medallas en catalogo</div></div>
    <div class="stat-item"><div class="stat-n">PDF</div><div class="stat-l">Certificado post-venta</div></div>
    <div class="stat-item"><div class="stat-n">QR</div><div class="stat-l">Autenticidad verificable</div></div>
    <div class="stat-item"><div class="stat-n">Transbank</div><div class="stat-l">Pago 100% seguro</div></div>
  </div>
</div>

<!-- GALERIA -->
<section class="gallery-sec sec" id="galeria">
  <div class="sec-in">
    <p class="eb">Catalogo oficial</p>
    <h2 class="st">Galeria de coleccion</h2>
    <p class="ss">Billetes conmemorativos, monedas, medallas y oro. Todo verificado y certificado por Casa Moneda de Chile.</p>
    <div class="gal-tabs">
      <div class="gtab active" onclick="filterGal('all',this)">Todo</div>
      <div class="gtab" onclick="filterGal('billete',this)">Billetes conmemorativos</div>
      <div class="gtab" onclick="filterGal('moneda',this)">Monedas</div>
      <div class="gtab" onclick="filterGal('medalla',this)">Medallas</div>
      <div class="gtab" onclick="filterGal('oro',this)">Oro</div>
    </div>
    <div class="gal-grid" id="galGrid"></div>
  </div>
</section>

<!-- SLIDE: VENDE TU COLECCION -->
<section class="sell-slide" id="vender">
  <div class="sell-in">
    <div class="sell-text">
      <p style="font-size:11px;text-transform:uppercase;letter-spacing:.12em;color:var(--goldlt);font-weight:700;margin-bottom:.6rem">Para coleccionistas</p>
      <h2 class="st">Vende tu coleccion aqui</h2>
      <p class="ss">La unica plataforma con respaldo oficial de Casa Moneda. Tu comprador recibe el certificado PDF con codigo QR que confirma la autenticidad y el cambio de propietario.</p>
      <div class="sell-steps">
        <div class="sell-step"><div class="ss-num">1</div><div class="ss-txt"><strong>Registra tu pieza</strong><span>Ingresa el numero de serie del QR grabado en tu moneda o medalla</span></div></div>
        <div class="sell-step"><div class="ss-num">2</div><div class="ss-txt"><strong>Fija tu precio</strong><span>Ves el historial de precios de piezas similares para valorar correctamente</span></div></div>
        <div class="sell-step"><div class="ss-num">3</div><div class="ss-txt"><strong>Elige el envio</strong><span>Casa Moneda gestiona el envio (mas seguro) o tu lo envias directamente</span></div></div>
        <div class="sell-step"><div class="ss-num">4</div><div class="ss-txt"><strong>Cobra y certifica</strong><span>Pago via Transbank. El PDF con QR oficial se descarga solo despues de confirmar la venta</span></div></div>
      </div>
      <div class="sell-cta">
        <button class="btn-gold" onclick="openModal()">Iniciar venta ahora</button>
      </div>
    </div>
    <div class="trust-cards">
      <div class="tc"><div class="tc-icon">&#128274;</div><h4>Sin estafas</h4><p>El pago queda retenido hasta que el comprador confirma recibir la pieza. Casa Moneda actua como intermediario oficial.</p></div>
      <div class="tc"><div class="tc-icon">&#128196;</div><h4>Certificado PDF con QR</h4><p>Solo tras confirmar la venta, el sistema emite el PDF oficial con el codigo QR que acredita el nuevo propietario.</p></div>
      <div class="tc"><div class="tc-icon">&#128667;</div><h4>Logistica segura</h4><p>Opcion de que Casa Moneda reciba la pieza del vendedor, la verifique y la despache directamente al comprador.</p></div>
      <div class="tc"><div class="tc-icon">&#128176;</div><h4>Pago garantizado</h4><p>Webpay Plus, transferencia bancaria o MACH. El dinero llega a tu cuenta en 24-48 hrs habiles sin riesgo.</p></div>
    </div>
  </div>
</section>

<!-- COMO FUNCIONA -->
<section class="how-sec sec" id="como-funciona">
  <div class="sec-in">
    <p class="eb">El proceso completo</p>
    <h2 class="st">Como funciona MonedaViva</h2>
    <p class="ss">Desde que vendes hasta que el comprador recibe su certificado PDF con QR. Todo trazado, todo seguro.</p>
    <div class="steps-g">
      <div class="step-c"><div class="snum">1</div><h3>Escaneas el QR de tu pieza</h3><p>Cada pieza de Casa Moneda lleva un QR unico grabado. Al escanearlo aparece el historial completo y puedes iniciar la venta.</p></div>
      <div class="step-c"><div class="snum">2</div><h3>El comprador paga por Transbank</h3><p>Webpay, transferencia o MACH. El dinero queda retenido en custodia hasta que se confirma la entrega de la pieza.</p></div>
      <div class="step-c"><div class="snum">3</div><h3>Eliges como enviar la pieza</h3><p>Tu la envias directamente (y asumes la responsabilidad) o Casa Moneda la recibe de ti, la verifica y la despacha con seguimiento oficial.</p></div>
      <div class="step-c"><div class="snum">4</div><h3>El comprador confirma recepcion</h3><p>Al confirmar que recibio la pieza, el pago se libera a tu cuenta. En ese momento se genera el certificado PDF con QR oficial.</p></div>
    </div>
  </div>
</section>

<!-- BENEFICIOS -->
<section class="ben-sec sec" id="beneficios">
  <div class="sec-in">
    <p class="eb">Para Casa Moneda</p>
    <h2 class="st">Que gana la institucion</h2>
    <p class="ss">MonedaViva no reemplaza nada. Amplifica lo que Casa Moneda ya hace mejor que nadie.</p>
    <div class="ben-g">
      <div class="ben-c"><div class="ben-icon">&#128176;</div><h3>Ingresos por reventa</h3><p>Cada reventa genera un 2% automatico. Si se transan 10.000 piezas al año a $40.000 promedio, son $8 MM en ingresos pasivos.</p><div class="ben-n">+$8 MM</div><div class="ben-nl">estimado anual en comisiones</div></div>
      <div class="ben-c"><div class="ben-icon">&#128196;</div><h3>Certificado PDF oficial</h3><p>El PDF con QR se genera solo tras la venta confirmada, con el nuevo propietario ya registrado. Prueba de autenticidad inamovible.</p><div class="ben-n">100%</div><div class="ben-nl">piezas con certificado post-venta</div></div>
      <div class="ben-c"><div class="ben-icon">&#128667;</div><h3>Logistica como servicio</h3><p>Casa Moneda puede ofrecer recepcion, verificacion y despacho de piezas. Nueva linea de ingresos y posicionamiento como intermediario oficial.</p><div class="ben-n">+$4.990</div><div class="ben-nl">por envio gestionado</div></div>
      <div class="ben-c"><div class="ben-icon">&#128200;</div><h3>Datos de mercado</h3><p>Por primera vez, Casa Moneda sabria a que precio se revenden sus piezas, que ediciones tienen mas demanda y quienes coleccionan.</p><div class="ben-n">100%</div><div class="ben-nl">trazabilidad post-venta</div></div>
    </div>
  </div>
</section>

<!-- CTA -->
<section class="cta-sec">
  <h2>Listo para presentar MonedaViva?</h2>
  <p>Prototipo funcional. PDF real. Logistica contemplada. El siguiente paso es una reunion con el equipo digital de Casa Moneda.</p>
  <div class="cta-acts">
    <button class="btn-gold" onclick="openModal()">Ver el prototipo completo</button>
    <a href="mailto:cmch-ventadigital@casamoneda.cl" class="btn-ghost">Contactar venta digital</a>
  </div>
</section>

<!-- FOOTER -->
<footer class="foot">
  <div class="foot-in">
    <div>
      <div class="foot-logo">MonedaViva</div>
      <div class="foot-copy">Propuesta de innovacion · Casa Moneda de Chile · Design Thinking 2024<br>contacto@casamoneda.cl · T. +56 2 2598 5100</div>
    </div>
    <div class="foot-links">
      <a href="#galeria">Galeria</a>
      <a href="#vender">Vender</a>
      <a href="#como-funciona">Como funciona</a>
      <a href="https://tienda.casamoneda.cl" target="_blank">tienda.casamoneda.cl</a>
      <a href="https://www.casamoneda.cl" target="_blank">casamoneda.cl</a>
    </div>
  </div>
</footer>

<!-- ════════════ MODAL VENTA ════════════ -->
<div class="overlay" id="modal">
  <div class="mbox">

    <!-- MS1: Certificado info -->
    <div class="mscreen active" id="ms1">
      <div class="mh">
        <div class="mh-badge"><div class="mh-dot"></div>Autenticidad verificada · Casa Moneda</div>
        <button class="mclose" onclick="closeModal()">&#10005;</button>
      </div>
      <div class="cert-body">
        <div class="cref-row">
          <div class="cert-vis">Chile<br>$200<br>2010</div>
          <div class="cert-info">
            <h2>Moneda Bicentenario 2010</h2>
            <p>$200 &middot; Cobre-Niquel &middot; Edicion limitada</p>
            <span class="tag-auth">&#10003; Autentica</span>
          </div>
        </div>
        <hr class="div">
        <div class="dgrid">
          <div class="dc"><div class="l">N de serie</div><div class="v" style="font-family:monospace;font-size:11px">CM-2010-00847</div></div>
          <div class="dc"><div class="l">Acunacion</div><div class="v">14 Sep 2010</div></div>
          <div class="dc"><div class="l">Composicion</div><div class="v">Cu 75% - Ni 25%</div></div>
          <div class="dc"><div class="l">Tirada</div><div class="v">50.000 uds.</div></div>
          <div class="dc"><div class="l">Valor mercado</div><div class="v">$38.500 CLP</div></div>
          <div class="dc"><div class="l">N certificado</div><div class="v" style="font-family:monospace;font-size:11px">CERT-4721</div></div>
        </div>
        <div class="ow-lbl">Historial de propietarios</div>
        <div class="ow-row"><div class="ow-av" style="background:#E6F1FB;color:#0C447C">CM</div><span class="ow-name">Casa Moneda de Chile <span style="font-size:10px;color:var(--text3)">(origen)</span></span><span class="ow-dt">Sep 2010</span></div>
        <div class="ow-row"><div class="ow-av" style="background:#EEEDFE;color:#534AB7">RP</div><span class="ow-name">Roberto Perez</span><span class="ow-dt">Mar 2018</span><span class="ow-p">$18.000</span></div>
        <div class="ow-row"><div class="ow-av" style="background:var(--soft);color:var(--navy)">TU</div><span class="ow-name">Tu <span style="font-size:10px;color:var(--text3)">(propietario actual)</span></span><span class="ow-dt">Ene 2024</span><span class="ow-p">$25.000</span></div>
        <div class="info-note note-blue">&#8505; <span>El certificado PDF con codigo QR se genera <strong>solo tras confirmar la venta</strong>, con el nuevo propietario registrado.</span></div>
      </div>
      <div class="cert-foot">
        <button class="btn-sm" onclick="closeModal()">Cerrar</button>
        <button class="btn-navy" onclick="showMS('ms2')">&#128179; Iniciar venta &rarr;</button>
      </div>
    </div>

    <!-- MS2: Formulario venta -->
    <div class="mscreen" id="ms2">
      <div class="ph">
        <button class="back-btn" onclick="showMS('ms1')">&#8592;</button>
        <h3>Vender · Datos de la transaccion</h3>
        <button class="mclose" onclick="closeModal()">&#10005;</button>
      </div>
      <div class="pb">
        <div class="mini-row">
          <div class="mini-coin"></div>
          <div><p>Moneda Bicentenario 2010</p><span>CM-2010-00847 &middot; CERT-4721</span></div>
        </div>

        <label class="fl" for="sp">Precio de venta (CLP)</label>
        <input id="sp" class="fi" type="number" value="38500" oninput="updS()">

        <label class="fl">Metodo de pago del comprador</label>
        <div class="mtabs">
          <div class="mtab active" id="t-wp" onclick="setM('wp')">&#128179; Webpay</div>
          <div class="mtab" id="t-tf" onclick="setM('tf')">&#127968; Transferencia</div>
          <div class="mtab" id="t-mc" onclick="setM('mc')">&#128241; MACH</div>
        </div>
        <div id="f-wp">
          <label class="fl" for="cn">Numero de tarjeta</label>
          <input id="cn" class="fi" type="text" placeholder="xxxx xxxx xxxx xxxx" maxlength="19" oninput="fmtC(this)">
          <div class="crow">
            <div><label class="fl" for="ce">Vencimiento</label><input id="ce" class="fi" type="text" placeholder="MM/AA" maxlength="5" oninput="fmtE(this)"></div>
            <div><label class="fl" for="cv">CVV</label><input id="cv" class="fi" type="text" placeholder="xxx" maxlength="3"></div>
          </div>
          <label class="fl" for="cn2">Nombre en tarjeta</label>
          <input id="cn2" class="fi" type="text" placeholder="NOMBRE APELLIDO">
        </div>
        <div id="f-tf" style="display:none">
          <label class="fl" for="rut">RUT del comprador</label>
          <input id="rut" class="fi" type="text" placeholder="12.345.678-9">
          <label class="fl" for="bk">Banco</label>
          <select id="bk" class="fi"><option>Banco de Chile</option><option>BancoEstado</option><option>Santander</option><option>BCI</option><option>Scotiabank</option><option>Itau</option></select>
          <label class="fl" for="ac">N de cuenta</label>
          <input id="ac" class="fi" type="text" placeholder="000000000">
        </div>
        <div id="f-mc" style="display:none">
          <label class="fl" for="mp">Telefono o alias MACH</label>
          <input id="mp" class="fi" type="text" placeholder="+56 9 1234 5678 o @usuario">
        </div>

        <!-- OPCIONES DE ENVIO -->
        <label class="fl" style="margin-bottom:8px">Como se entrega la pieza al comprador</label>
        <div class="ship-opts">
          <div class="ship-opt sel" id="so1" onclick="selShip(1)">
            <div class="ship-opt-head">
              <div class="ship-rb on" id="sr1"></div>
              <div class="ship-lbl">
                <strong>&#127968; Casa Moneda gestiona el envio (recomendado)</strong>
                <span>Tu entregas la pieza a Casa Moneda, ellos la verifican y despachan al comprador</span>
                <div class="ship-badge">+$4.990 CLP &middot; Mas seguro</div>
              </div>
            </div>
            <div class="ship-detail show" id="sd1">
              <p>&#128667; Casa Moneda recibe la pieza de ti en sus instalaciones (Quinta Normal, Santiago), la verifica fisicamente, la embala con sello oficial y la despacha al comprador con numero de seguimiento.</p>
              <p style="margin-top:6px">&#128197; Plazo: 3-5 dias habiles RM, 5-7 dias regiones.</p>
              <div class="ship-security">&#9989; El pago queda retenido hasta que el comprador confirme recepcion. Sin riesgo de estafa para ninguna parte.</div>
            </div>
          </div>
          <div class="ship-opt" id="so2" onclick="selShip(2)">
            <div class="ship-opt-head">
              <div class="ship-rb" id="sr2"></div>
              <div class="ship-lbl">
                <strong>&#128230; El vendedor (tu) envias directamente</strong>
                <span>Te haces cargo del despacho. El pago se libera cuando el comprador confirma recepcion.</span>
                <div class="ship-badge" style="background:#FEE2E2;color:#9B2020;border-color:#F87171">Asumo la responsabilidad del envio</div>
              </div>
            </div>
            <div class="ship-detail" id="sd2">
              <p>&#9888;&#65039; Debes enviar la pieza con numero de seguimiento y compartirlo con el comprador a traves de la plataforma.</p>
              <p style="margin-top:6px">El pago solo se libera cuando el comprador confirma que recibio la pieza en buen estado. Si no se confirma en 7 dias habiles, se activa mediacion de Casa Moneda.</p>
            </div>
          </div>
        </div>

        <!-- Resumen -->
        <div class="ps">
          <p class="ps-t">Resumen de la transaccion</p>
          <div class="ps-r"><span>Precio de venta</span><span id="ps-total">$38.500</span></div>
          <div class="ps-r"><span class="ps-m">Comision Transbank (1,99%)</span><span id="ps-tbk" class="ps-m">- $766</span></div>
          <div class="ps-r"><span class="ps-m">Cargo MonedaViva (2%)</span><span id="ps-mv" class="ps-m">- $770</span></div>
          <div class="ps-r" id="ps-ship-row"><span class="ps-m">Logistica Casa Moneda</span><span id="ps-ship" class="ps-m">- $4.990</span></div>
          <div class="ps-r tot"><span>Recibes en tu cuenta</span><span id="ps-you">$31.974</span></div>
        </div>
        <div class="tbk-brand"><div class="tbk-logo">Transbank</div><span>Pago seguro &middot; SSL 256-bit &middot; PCI DSS</span></div>
        <button class="btn-confirm" onclick="procesar()">&#128274; Confirmar venta y generar certificado PDF</button>
      </div>
    </div>

    <!-- MS3: Procesando -->
    <div class="mscreen" id="ms3">
      <div class="ph"><h3>Procesando</h3><button class="mclose" onclick="closeModal()">&#10005;</button></div>
      <div class="proc-wrap">
        <div style="background:#E60012;color:#fff;font-size:13px;font-weight:800;padding:5px 14px;border-radius:4px;display:inline-block;margin-bottom:1.4rem">Transbank</div>
        <div class="spin"></div>
        <p style="font-size:15px;font-weight:700;color:var(--navy);margin-bottom:.4rem">Procesando pago seguro...</p>
        <p style="font-size:12px;color:var(--text3)">No cierres esta ventana</p>
        <ul class="vsteps">
          <li id="p1"><span>&#9203;</span> Iniciando sesion segura Transbank</li>
          <li id="p2"><span>&#9203;</span> Autorizando con banco emisor</li>
          <li id="p3"><span>&#9203;</span> Reteniendo pago en custodia</li>
          <li id="p4"><span>&#9203;</span> Preparando certificado PDF con QR</li>
        </ul>
      </div>
    </div>

    <!-- MS4: Exito -->
    <div class="mscreen" id="ms4">
      <div class="ph" style="background:var(--navy)"><h3 style="color:#97C459">Venta confirmada</h3><button class="mclose" onclick="closeModal()">&#10005;</button></div>
      <div class="ok-wrap">
        <div class="ok-circle"><svg viewBox="0 0 24 24"><polyline points="20 6 9 17 4 12"/></svg></div>
        <h3 style="font-size:17px;font-weight:800;color:var(--navy);margin-bottom:.4rem">Pago procesado con exito</h3>
        <p style="font-size:13px;color:var(--text2)">Recibiras <strong id="ok-amt">$31.974</strong> en tu cuenta cuando el comprador confirme la recepcion.</p>
        <div class="ok-folio" id="ok-folio"></div>
        <div class="ok-log-note" id="ok-log-note"></div>
        <p style="font-size:12px;color:var(--text2);margin-bottom:.75rem">Tu certificado PDF con codigo QR oficial esta listo:</p>
        <button class="btn-pdf" onclick="openPDFViewer()">
          &#128196; Ver y descargar certificado PDF
        </button>
        <div class="ok-acts">
          <button class="btn-sm" onclick="closeModal()">Cerrar</button>
        </div>
      </div>
    </div>

  </div>
</div>

<!-- ════════════ PDF VIEWER ════════════ -->
<div class="pdf-viewer" id="pdfViewer">
  <div class="pdf-box">
    <div class="pdf-head">
      <h3>Certificado oficial MonedaViva</h3>
      <button class="mclose" onclick="closePDFViewer()">&#10005;</button>
    </div>
    <div class="pdf-content">
      <div class="cert-doc">
        <!-- Head -->
        <div class="cert-doc-head">
          <!-- Logo CM inline -->
          <svg width="50" height="50" viewBox="0 0 100 100" style="margin:0 auto 8px;display:block">
            <circle cx="50" cy="50" r="48" fill="#0B1F3A" stroke="#C9A84C" stroke-width="3"/>
            <circle cx="50" cy="50" r="38" fill="none" stroke="#C9A84C" stroke-width="1.2"/>
            <text x="50" y="38" font-family="Georgia,serif" font-size="11" font-weight="bold" fill="#C9A84C" text-anchor="middle">CASA</text>
            <text x="50" y="50" font-family="Georgia,serif" font-size="11" font-weight="bold" fill="#C9A84C" text-anchor="middle">MONEDA</text>
            <text x="50" y="62" font-family="Georgia,serif" font-size="8" fill="#C9A84C" text-anchor="middle">DE CHILE</text>
            <text x="50" y="75" font-family="Georgia,serif" font-size="7" fill="#E2C06A" text-anchor="middle">EST. 1743</text>
          </svg>
          <div class="cm-name">CASA MONEDA DE CHILE</div>
          <div class="cm-sub">Certificado oficial de autenticidad &middot; MonedaViva</div>
        </div>
        <div class="cert-doc-gold"></div>
        <div class="cert-doc-body">
          <!-- QR + titulo -->
          <div class="cert-qr-row">
            <div class="cert-qr-box"><div id="qrcode-cert"></div></div>
            <div>
              <div class="cert-doc-title">Moneda Bicentenario 2010</div>
              <div class="cert-doc-sub">$200 &middot; Cobre-Niquel &middot; Edicion Limitada</div>
              <span class="cert-auth-badge">&#10003; AUTENTICA &middot; CERTIFICADA</span>
              <p style="font-size:10px;color:var(--text3);margin-top:8px">Escanea el QR para verificar<br>en monedaviva.casamoneda.cl</p>
            </div>
          </div>
          <!-- Datos -->
          <div class="cert-dgrid">
            <div class="cert-dc"><div class="l">N. de serie</div><div class="v">CM-2010-00847</div></div>
            <div class="cert-dc"><div class="l">Fecha acunacion</div><div class="v">14 Sep 2010</div></div>
            <div class="cert-dc"><div class="l">Composicion</div><div class="v">Cu 75% - Ni 25%</div></div>
            <div class="cert-dc"><div class="l">Tirada</div><div class="v">50.000 uds.</div></div>
            <div class="cert-dc"><div class="l">Diametro</div><div class="v">23.5 mm</div></div>
            <div class="cert-dc"><div class="l">Peso</div><div class="v">3.5 gramos</div></div>
            <div class="cert-dc"><div class="l">N. certificado</div><div class="v">CERT-4721</div></div>
            <div class="cert-dc"><div class="l">Fecha emision</div><div class="v" id="cert-date"></div></div>
          </div>
          <!-- Propietarios -->
          <div class="cert-ow-sec">
            <div class="cert-ow-lbl">Historial verificado de propietarios</div>
            <div class="cert-ow-row"><div class="cert-ow-av" style="background:#E6F1FB;color:#0C447C">CM</div><span style="flex:1;color:var(--navy)">Casa Moneda de Chile (origen)</span><span style="color:var(--text3);font-size:10px">Sep 2010</span></div>
            <div class="cert-ow-row"><div class="cert-ow-av" style="background:#EEEDFE;color:#534AB7">RP</div><span style="flex:1;color:var(--navy)">Roberto Perez</span><span style="color:var(--text3);font-size:10px">Mar 2018</span><span style="font-weight:700;font-size:11px;font-family:monospace">$18.000</span></div>
            <div class="cert-ow-row"><div class="cert-ow-av" style="background:var(--soft);color:var(--navy)">P2</div><span style="flex:1;color:var(--navy)">Propietario anterior</span><span style="color:var(--text3);font-size:10px">Ene 2024</span><span style="font-weight:700;font-size:11px;font-family:monospace">$25.000</span></div>
            <div class="cert-new-owner">
              <strong>&#9989; Nuevo propietario registrado:</strong> Comprador confirmado &middot; <span id="cert-tx-date"></span><br>
              <span style="font-size:10px;color:var(--text2)">Precio de la transaccion: <strong id="cert-tx-price">$38.500</strong> &middot; Via Transbank &middot; Folio: <span id="cert-tx-folio"></span></span>
            </div>
          </div>
          <!-- Codigo autenticidad -->
          <div style="font-size:9px;color:var(--text3);text-transform:uppercase;letter-spacing:.06em;font-weight:600;margin-bottom:5px">Codigo de autenticidad</div>
          <div class="cert-code">CM2010-847-AUTH-3A7F8B2C1D9E4F6A0B5C8D2E7F1A3B6C &middot; Verificado en monedaviva.casamoneda.cl</div>
        </div>
        <div class="cert-doc-foot">
          <p>Casa Moneda de Chile &middot; Documento oficial &middot; <span id="cert-footer-date"></span></p>
          <p>Este certificado es valido como prueba de autenticidad y cambio de propiedad de la pieza descrita.</p>
          <div class="cm-url">monedaviva.casamoneda.cl</div>
        </div>
      </div>
    </div>
    <div class="pdf-acts">
      <button class="btn-sm" onclick="closePDFViewer()">Cerrar</button>
      <button class="btn-navy" onclick="generarPDF()" style="flex:1">&#128196; Descargar PDF</button>
    </div>
  </div>
</div>

<div class="toast" id="toast">&#128196; Descargando certificado oficial...</div>

<script>
/* ════ GALERIA ════ */
const GAL=[
  // Billetes conmemorativos
  {cat:'billete',name:'Billete $1.000 - Ignacio Carrera Pinto',sub:'Serie conmemorativa 1993',price:'$45.000',color:'#1B4332',color2:'#2D6A4F',text:'$1.000\nCarrera Pinto\n1993'},
  {cat:'billete',name:'Billete $5.000 - Gabriela Mistral',sub:'Edicion especial Nobel 1945',price:'$120.000',color:'#1E3A5F',color2:'#2E6DA4',text:'$5.000\nG. Mistral\nNobel 1945'},
  {cat:'billete',name:'Billete $10.000 - Arturo Prat',sub:'Conmemorativo Combate Iquique',price:'$85.000',color:'#4A1942',color2:'#7B2D8B',text:'$10.000\nA. Prat\nIquique'},
  {cat:'billete',name:'Billete $2.000 - Manuel Rodriguez',sub:'Serie bicentenario 2010',price:'$55.000',color:'#7A2E0E',color2:'#B45309',text:'$2.000\nM. Rodriguez\n2010'},
  // Monedas
  {cat:'moneda',name:'Moneda Bicentenario $500',sub:'Cobre-Niquel · 2010 · 50.000 uds.',price:'$38.500'},
  {cat:'moneda',name:'Moneda $200 Escudo de Chile',sub:'Serie especial 2015 · 30.000 uds.',price:'$25.000'},
  {cat:'moneda',name:'Moneda $100 Pueblos Originarios',sub:'Edicion Mapuche 2018',price:'$18.000'},
  {cat:'moneda',name:'Moneda $1.000 Plata Pura',sub:'999 · Edicion limitada 5.000 uds.',price:'$180.000',isPlata:true},
  // Medallas
  {cat:'medalla',name:'Medalla Bronce - Patricio Aylwin',sub:'Serie Presidencial · 40mm',price:'$27.990'},
  {cat:'medalla',name:'Medalla Bronce - Gabriela Mistral',sub:'Serie Poetas · 40mm · Ed. limitada',price:'$27.990'},
  {cat:'medalla',name:'Medalla Cobre - Flora y Fauna',sub:'Condor de los Andes · 45mm',price:'$33.990'},
  {cat:'medalla',name:'Medalla Bronce - Heroes Chilenos',sub:'Arturo Prat Chacon · 38mm',price:'$27.990'},
  {cat:'medalla',name:'Medalla Pueblos Originarios',sub:'Cultura Atacamena · 42mm',price:'$29.990'},
  // Oro
  {cat:'oro',name:'Barra de Oro 1 oz · 999,9',sub:'Refinacion CMCH · Certificado UAF',price:'$3.200.000'},
  {cat:'oro',name:'Barra de Oro 1/2 oz · 999,9',sub:'Refinacion CMCH · Ed. inversion',price:'$1.650.000'},
  {cat:'oro',name:'Moneda Oro 1/10 oz · 999,9',sub:'Escudo nacional · Ed. coleccion',price:'$380.000'},
]

function buildBillSVG(item){
  const c=item.color||'#1B4332',c2=item.color2||'#2D6A4F',lines=item.text.split('\n')
  return `<div class="bill-art" style="background:linear-gradient(135deg,${c},${c2});border:1.5px solid rgba(255,255,255,.2)">
    <div style="position:absolute;inset:4px;border:1px solid rgba(255,255,255,.15);border-radius:4px;pointer-events:none"></div>
    <div style="z-index:1;color:rgba(255,255,255,.9)">${lines.map(l=>`<div>${l}</div>`).join('')}</div>
    <div style="position:absolute;bottom:4px;right:6px;font-size:7px;color:rgba(255,255,255,.4)">CHILE</div>
  </div>`
}
function buildMonSVG(item){
  const bg=item.isPlata?'radial-gradient(circle at 33% 33%,#F0F0F0,#B0B8C0 55%,#707880)':'radial-gradient(circle at 33% 33%,#F7E48A,#C9A84C 55%,#7A5800)'
  const bc=item.isPlata?'#B0B8C0':'#E2C06A',tc=item.isPlata?'#3A4048':'#3A2800'
  const sz=item.isPlata?'72px':'72px'
  const parts=item.name.replace('Moneda ','').split(' ')
  return `<div class="mon-art" style="width:${sz};height:${sz};background:${bg};border:2px solid ${bc};color:${tc}">
    <div style="font-size:9px;line-height:1.3">${parts.slice(0,2).join('<br>')}</div>
  </div>`
}
function buildOroSVG(item){
  const h=item.name.includes('1 oz')?'70px':item.name.includes('1/2')?'55px':'45px'
  return `<div class="oro-art" style="width:90px;height:${h};background:linear-gradient(135deg,#F7E48A,#C9A84C 50%,#9A7530);border:2px solid #E2C06A">
    <div><div style="font-size:8px;color:#3A2800;font-weight:800">CHILE</div><div style="font-size:8px;color:#3A2800">999,9</div></div>
  </div>`
}

function renderGal(filter){
  const g=document.getElementById('galGrid')
  g.innerHTML=''
  GAL.filter(i=>filter==='all'||i.cat===filter).forEach(item=>{
    const badgeMap={billete:'badge-bill',moneda:'badge-cert',medalla:'badge-cert',oro:'badge-oro'}
    const badgeTxt={billete:'Billete',moneda:'Moneda',medalla:'Medalla',oro:'Oro 999,9'}
    let imgHtml=''
    if(item.cat==='billete')imgHtml=buildBillSVG(item)
    else if(item.cat==='moneda')imgHtml=buildMonSVG(item)
    else if(item.cat==='medalla')imgHtml=`<div class="mon-art" style="width:70px;height:70px;background:radial-gradient(circle at 33% 33%,#D4A84C,#8B6914 55%,#5A4008);border:2px solid #C9A84C;color:#2A1800;font-size:9px">${item.name.split('-')[1]||'Medalla'}</div>`
    else imgHtml=buildOroSVG(item)
    const el=document.createElement('div')
    el.className='gal-item'
    el.innerHTML=`<div class="gal-img">${imgHtml}<span class="gal-badge ${badgeMap[item.cat]}">${badgeTxt[item.cat]}</span></div>
    <div class="gal-info"><h4>${item.name}</h4><p>${item.sub}</p><div class="gal-price">${item.price}</div></div>`
    el.onclick=()=>openModal()
    g.appendChild(el)
  })
}
function filterGal(f,el){document.querySelectorAll('.gtab').forEach(t=>t.classList.remove('active'));el.classList.add('active');renderGal(f)}
renderGal('all')

/* ════ MODAL ════ */
let curM='wp',shipMode=1,lastFolio='',lastPrice=38500

function openModal(){document.getElementById('modal').classList.add('open');document.body.style.overflow='hidden';showMS('ms1')}
function closeModal(){document.getElementById('modal').classList.remove('open');document.body.style.overflow=''}
document.getElementById('modal').addEventListener('click',function(e){if(e.target===this)closeModal()})
document.addEventListener('keydown',function(e){if(e.key==='Escape'){closeModal();closePDFViewer()}})
function showMS(id){document.querySelectorAll('.mscreen').forEach(s=>s.classList.remove('active'));document.getElementById(id).classList.add('active')}

/* Envio */
function selShip(n){
  shipMode=n
  ;[1,2].forEach(i=>{
    document.getElementById('so'+i).classList.toggle('sel',i===n)
    document.getElementById('sr'+i).classList.toggle('on',i===n)
    document.getElementById('sd'+i).classList.toggle('show',i===n)
  })
  updS()
}

/* Resumen */
function fmt(n){return '$'+Math.round(n).toLocaleString('es-CL')}
function updS(){
  const p=parseFloat(document.getElementById('sp').value)||0
  const tbk=p*0.0199,mv=p*0.02,ship=shipMode===1?4990:0,you=p-tbk-mv-ship
  document.getElementById('ps-total').textContent=fmt(p)
  document.getElementById('ps-tbk').textContent='- '+fmt(tbk)
  document.getElementById('ps-mv').textContent='- '+fmt(mv)
  document.getElementById('ps-ship').textContent='- '+fmt(ship)
  document.getElementById('ps-ship-row').style.display=shipMode===1?'flex':'none'
  document.getElementById('ps-you').textContent=fmt(you)
}
updS()

/* Tabs metodo */
const mL={wp:'Webpay Plus',tf:'Transferencia bancaria',mc:'MACH / BancoEstado'}
function setM(m){curM=m;['wp','tf','mc'].forEach(k=>{document.getElementById('t-'+k).classList.toggle('active',k===m);document.getElementById('f-'+k).style.display=k===m?'block':'none'})}

/* Formateo */
function fmtC(el){let v=el.value.replace(/\D/g,'').substring(0,16);el.value=v.replace(/(.{4})/g,'$1 ').trim()}
function fmtE(el){let v=el.value.replace(/\D/g,'');if(v.length>=2)v=v.slice(0,2)+'/'+v.slice(2,4);el.value=v}

/* Procesar */
function procesar(){
  showMS('ms3')
  ;['p1','p2','p3','p4'].forEach((id,i)=>{
    setTimeout(()=>{const li=document.getElementById(id);li.innerHTML=li.innerHTML.replace(/⏳|&#9203;/,'✓');li.classList.add('done')},(i+1)*750)
  })
  setTimeout(()=>{
    lastPrice=parseFloat(document.getElementById('sp').value)||38500
    const ship=shipMode===1?4990:0
    const you=lastPrice-lastPrice*0.0199-lastPrice*0.02-ship
    document.getElementById('ok-amt').textContent=fmt(you)
    lastFolio='TBK-'+new Date().getFullYear()+'-'+String(Math.floor(Math.random()*99999)).padStart(5,'0')+'-X'
    const auth=String(Math.floor(Math.random()*900000)+100000)
    document.getElementById('ok-folio').innerHTML='Folio: '+lastFolio+'<br>Auth: '+auth+' &middot; '+mL[curM]
    const logNote=document.getElementById('ok-log-note')
    if(shipMode===1){logNote.className='ok-log-note show';logNote.innerHTML='&#128667; <strong>Casa Moneda gestionara el envio.</strong> Recibiras instrucciones para entregar la pieza en Quinta Normal. El comprador sera notificado con el numero de seguimiento.'}
    else{logNote.className='ok-log-note show';logNote.style.background='#FEE2E2';logNote.style.borderColor='#F87171';logNote.style.color='#9B2020';logNote.innerHTML='&#9888;&#65039; <strong>Tu envias la pieza.</strong> Compartiras el numero de seguimiento en la plataforma. El pago se libera cuando el comprador confirme la recepcion.'}
    showMS('ms4')
  },3800)
}

/* ════ PDF VIEWER ════ */
let qrGenerated=false
function openPDFViewer(){
  const now=new Date()
  const dateStr=now.toLocaleDateString('es-CL')
  document.getElementById('cert-date').textContent=dateStr
  document.getElementById('cert-footer-date').textContent=dateStr
  document.getElementById('cert-tx-date').textContent=dateStr
  document.getElementById('cert-tx-price').textContent=fmt(lastPrice)
  document.getElementById('cert-tx-folio').textContent=lastFolio||'TBK-2024-00001-X'
  // Generar QR
  if(!qrGenerated){
    const qrEl=document.getElementById('qrcode-cert')
    qrEl.innerHTML=''
    try{
      new QRCode(qrEl,{text:'https://monedaviva.casamoneda.cl/cert/CM-2010-00847',width:80,height:80,colorDark:'#0B1F3A',colorLight:'#FFFFFF',correctLevel:QRCode.CorrectLevel.M})
      qrGenerated=true
    }catch(e){qrEl.innerHTML='<div style="width:80px;height:80px;background:#EEF2FF;display:flex;align-items:center;justify-content:center;font-size:9px;color:#3730A3;font-weight:700;border-radius:4px">QR</div>'}
  }
  document.getElementById('pdfViewer').classList.add('open')
}
function closePDFViewer(){document.getElementById('pdfViewer').classList.remove('open')}
document.getElementById('pdfViewer').addEventListener('click',function(e){if(e.target===this)closePDFViewer()})

/* ════ GENERAR PDF ════ */
function generarPDF(){
  const toast=document.getElementById('toast')
  toast.classList.add('show')
  setTimeout(()=>toast.classList.remove('show'),3000)
  try{
    const {jsPDF}=window.jspdf
    const doc=new jsPDF({orientation:'portrait',unit:'mm',format:'a4'})
    const W=210,H=297,now=new Date().toLocaleDateString('es-CL')

    // Fondo
    doc.setFillColor(255,255,255);doc.rect(0,0,W,H,'F')
    // Header navy
    doc.setFillColor(11,31,58);doc.rect(0,0,W,26,'F')
    // Linea dorada
    doc.setFillColor(201,168,76);doc.rect(0,26,W,3,'F')
    // Logo CM (circulo SVG like)
    doc.setFillColor(11,31,58);doc.circle(18,13,11,'F')
    doc.setDrawColor(201,168,76);doc.setLineWidth(1.2);doc.circle(18,13,10)
    doc.setDrawColor(201,168,76);doc.setLineWidth(0.5);doc.circle(18,13,8)
    doc.setTextColor(201,168,76);doc.setFont('helvetica','bold');doc.setFontSize(5.5)
    doc.text('CASA',18,10,{align:'center'})
    doc.text('MONEDA',18,14,{align:'center'})
    doc.text('CHILE',18,18,{align:'center'})
    // Titulos
    doc.setTextColor(255,255,255);doc.setFont('helvetica','bold');doc.setFontSize(14)
    doc.text('CASA MONEDA DE CHILE',W/2+5,12,{align:'center'})
    doc.setFontSize(8);doc.setFont('helvetica','normal')
    doc.setTextColor(201,168,76)
    doc.text('CERTIFICADO OFICIAL DE AUTENTICIDAD  |  MonedaViva',W/2+5,19,{align:'center'})
    // Numero cert
    doc.setTextColor(150,150,150);doc.setFontSize(7)
    doc.text('CERT-4721  |  '+now,W-12,35,{align:'right'})
    // Moneda dibujo
    doc.setDrawColor(201,168,76);doc.setLineWidth(2.5);doc.circle(W/2,62,24)
    doc.setLineWidth(0.8);doc.circle(W/2,62,21.5)
    doc.setTextColor(90,55,0);doc.setFont('helvetica','bold')
    doc.setFontSize(9);doc.text('CHILE',W/2,55,{align:'center'})
    doc.setFontSize(14);doc.text('$200',W/2,64,{align:'center'})
    doc.setFontSize(8);doc.text('2010',W/2,71,{align:'center'})
    // QR placeholder
    doc.setFillColor(238,242,255);doc.setDrawColor(165,180,252)
    doc.setLineWidth(0.5);doc.rect(16,33,22,22,'FD')
    doc.setTextColor(55,48,163);doc.setFont('helvetica','bold');doc.setFontSize(6)
    doc.text('QR',27,43,{align:'center'});doc.text('CERT',27,48,{align:'center'})
    // Titulo pieza
    doc.setTextColor(11,31,58);doc.setFont('helvetica','bold');doc.setFontSize(20)
    doc.text('Moneda Bicentenario 2010',W/2,88,{align:'center'})
    doc.setFont('helvetica','normal');doc.setFontSize(10);doc.setTextColor(58,80,112)
    doc.text('$200  |  Cobre-Niquel  |  Edicion Limitada 50.000 uds.',W/2,95,{align:'center'})
    // Badge autentica
    doc.setFillColor(234,243,222);doc.setDrawColor(140,191,80);doc.setLineWidth(0.8)
    doc.roundedRect(W/2-25,99,50,9,2,2,'FD')
    doc.setTextColor(46,107,15);doc.setFont('helvetica','bold');doc.setFontSize(8)
    doc.text('AUTENTICA  |  CERTIFICADA',W/2,105,{align:'center'})
    // Divisor
    doc.setDrawColor(208,220,240);doc.setLineWidth(0.5);doc.line(16,114,W-16,114)
    // Datos grid
    const datos=[['N. de Serie','CM-2010-00847'],['Fecha Acunacion','14 Sep 2010'],['Composicion','Cu 75%  Ni 25%'],['Tirada Total','50.000 uds.'],['Diametro','23.5 mm'],['Peso','3.5 gramos'],['Valor Mercado',fmt(lastPrice)+' CLP'],['N. Certificado','CERT-4721']]
    let yD=126
    datos.forEach(([k,v],i)=>{
      const col=i%2,x=col===0?16:W/2+4
      if(col===0&&i>0)yD+=13
      doc.setFont('helvetica','normal');doc.setTextColor(107,135,168);doc.setFontSize(7);doc.text(k.toUpperCase(),x,yD)
      doc.setFont('helvetica','bold');doc.setTextColor(11,31,58);doc.setFontSize(9.5);doc.text(v,x,yD+6)
    })
    yD+=18
    doc.setDrawColor(208,220,240);doc.line(16,yD,W-16,yD)
    // Propietarios
    yD+=9
    doc.setFont('helvetica','bold');doc.setFontSize(8);doc.setTextColor(107,135,168)
    doc.text('HISTORIAL VERIFICADO DE PROPIETARIOS',16,yD);yD+=9
    const props=[
      {i:'CM',n:'Casa Moneda de Chile (origen)',f:'Sep 2010',p:''},
      {i:'RP',n:'Roberto Perez',f:'Mar 2018',p:'$18.000 CLP'},
      {i:'P2',n:'Propietario anterior',f:'Ene 2024',p:'$25.000 CLP'},
      {i:'NP',n:'NUEVO PROPIETARIO (esta transaccion)',f:now,p:fmt(lastPrice)+' CLP'},
    ]
    props.forEach((p,idx)=>{
      if(idx===3){doc.setFillColor(232,238,246);doc.rect(16,yD-4,W-32,12,'F')}
      doc.setFillColor(idx===3?11:220,idx===3?31:225,idx===3?58:240)
      doc.circle(21,yD-0.5,3,idx===3?'F':'F')
      doc.setFont('helvetica','bold');doc.setFontSize(5.5);doc.setTextColor(idx===3?201:58,idx===3?168:80,idx===3?76:112)
      doc.text(p.i,21,yD+1,{align:'center'})
      doc.setFont(idx===3?'helvetica':'helvetica',idx===3?'bold':'normal');doc.setFontSize(9);doc.setTextColor(11,31,58)
      doc.text(p.n,29,yD)
      doc.setTextColor(107,135,168);doc.text(p.f,W-55,yD)
      doc.setFont('helvetica','bold');doc.setTextColor(11,31,58)
      if(p.p)doc.text(p.p,W-14,yD,{align:'right'})
      doc.setDrawColor(208,220,240);doc.setLineWidth(0.2);doc.line(16,yD+5,W-16,yD+5)
      yD+=12
    })
    // Envio
    if(shipMode===1){
      yD+=4;doc.setFillColor(254,243,220);doc.setDrawColor(232,184,75);doc.roundedRect(16,yD,W-32,12,2,2,'FD')
      doc.setFont('helvetica','bold');doc.setFontSize(8);doc.setTextColor(122,82,0)
      doc.text('ENVIO GESTIONADO OFICIALMENTE POR CASA MONEDA DE CHILE',W/2,yD+8,{align:'center'});yD+=12
    }
    // Codigo
    yD+=7;doc.setFillColor(244,247,251);doc.setDrawColor(208,220,240);doc.roundedRect(16,yD,W-32,16,2,2,'FD')
    doc.setFont('helvetica','bold');doc.setFontSize(7);doc.setTextColor(107,135,168)
    doc.text('CODIGO DE AUTENTICIDAD',20,yD+7)
    doc.setFont('courier','normal');doc.setFontSize(7);doc.setTextColor(11,31,58)
    doc.text('CM2010-847-AUTH-3A7F8B2C1D9E4F6A0B5C8D2E7F1A3B',20,yD+13)
    // Transbank
    yD+=24;doc.setFillColor(230,241,251);doc.setDrawColor(133,183,235);doc.roundedRect(16,yD,W-32,12,2,2,'FD')
    doc.setFont('helvetica','normal');doc.setFontSize(8);doc.setTextColor(12,68,124)
    doc.text('Pago procesado via Webpay Plus (Transbank) · Folio: '+(lastFolio||'TBK-2024-00001-X'),W/2,yD+5,{align:'center'})
    doc.text('Verifica en: monedaviva.casamoneda.cl · '+now,W/2,yD+10,{align:'center'})
    // Footer
    doc.setFillColor(11,31,58);doc.rect(0,H-18,W,18,'F')
    doc.setFillColor(201,168,76);doc.rect(0,H-20,W,2,'F')
    doc.setTextColor(107,135,168);doc.setFont('helvetica','normal');doc.setFontSize(7)
    doc.text('Casa Moneda de Chile  |  Documento oficial  |  '+now,W/2,H-11,{align:'center'})
    doc.setTextColor(201,168,76);doc.text('monedaviva.casamoneda.cl',W/2,H-6,{align:'center'})
    doc.save('Certificado-MonedaViva-CM-2010-00847.pdf')
  }catch(e){console.error(e);alert('Error generando PDF. Verifica tu conexion.')}
}

/* Smooth scroll */
document.querySelectorAll('a[href^="#"]').forEach(a=>{
  a.addEventListener('click',function(e){const t=document.querySelector(this.getAttribute('href'));if(t){e.preventDefault();t.scrollIntoView({behavior:'smooth',block:'start'})}})
})
</script>
</body>
</html>
