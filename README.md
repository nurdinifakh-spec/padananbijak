<!DOCTYPE html>
<html lang="ms">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Misi 2: Padanan Bijak</title>
<style>
:root{--cr:#fff6e8;--be:#f3e2c7;--nu:#e6c3a0;--ko:#a8703f;--dk:#5c3a21;--ok:#6a9a5b;--no:#c0614d}
*{box-sizing:border-box}
html,body{margin:0}
body{font-family:"Comic Sans MS","Trebuchet MS",Verdana,sans-serif;background:var(--be);color:var(--dk);min-height:100vh;font-size:clamp(16px,1.9vw,20px);line-height:1.35;overflow-x:hidden}
#bg{position:fixed;inset:0;z-index:0}#bg svg{width:100%;height:100%;display:block}
.top{position:relative;z-index:5;display:flex;gap:8px;flex-wrap:wrap;padding:10px 14px}.sp{flex:1}
main{position:relative;z-index:2;max-width:1000px;margin:0 auto;padding:4px 12px 30px}
.screen{display:none}.screen.on{display:block}
.panel{background:rgba(255,246,232,.95);border:4px solid var(--nu);border-radius:28px;padding:clamp(12px,2.5vw,26px);box-shadow:0 10px 28px rgba(92,58,33,.25);text-align:center}
h1{margin:6px 0;font-size:clamp(28px,5.5vw,50px);color:var(--ko);text-shadow:2px 3px 0 var(--nu);line-height:1.1}
h2{margin:6px 0;font-size:clamp(24px,5vw,42px);color:var(--ko);text-shadow:2px 2px 0 var(--nu);line-height:1.15}
p{margin:8px 0}
.btn{font:inherit;font-weight:bold;background:var(--ko);color:#fff;border:0;border-bottom:5px solid #7a4d27;border-radius:18px;padding:10px 18px;cursor:pointer;box-shadow:0 4px 10px rgba(92,58,33,.3);transition:transform .12s}
.btn:hover{transform:translateY(-2px)}.btn:active{transform:translateY(2px)}
.btn.sm{font-size:.8em;padding:7px 12px;background:var(--cr);color:var(--dk);border-bottom-color:var(--nu)}
.btn.big{font-size:1.15em;padding:12px 26px}.btn.alt{background:var(--nu);color:var(--dk);border-bottom-color:var(--ko)}
.btn:disabled{opacity:.45;cursor:not-allowed;transform:none}
:focus-visible{outline:4px solid #2b6cb0;outline-offset:3px}
.chars{display:flex;justify-content:center;align-items:flex-end;gap:clamp(4px,2vw,22px);margin:6px 0}
.chars figure{margin:0;animation:bob 2.4s ease-in-out infinite}.chars figure:nth-child(2){animation-delay:.5s}.chars figure:nth-child(3){animation-delay:1s}
.chars figcaption{font-size:.8em;font-weight:bold;background:var(--be);border-radius:12px;padding:1px 10px;display:inline-block}
.ch{width:clamp(60px,12vw,110px);height:auto}
@keyframes bob{50%{transform:translateY(-6px)}}
.prog{display:flex;align-items:center;gap:10px;flex-wrap:wrap;justify-content:center;font-weight:bold}
.bar{flex:1;min-width:120px;height:16px;background:var(--be);border-radius:10px;overflow:hidden;border:2px solid var(--nu)}
.bar i{display:block;height:100%;width:0;background:linear-gradient(90deg,var(--ko),#d9a066);transition:width .5s}
.tw{display:inline-block;animation:tw 1.6s ease-in-out infinite}
@keyframes tw{50%{transform:scale(1.3) rotate(20deg);filter:brightness(1.3)}}
.hint{font-size:.85em;color:#8a6a4c;margin:6px 0}
.board{display:grid;grid-template-columns:1.4fr 1fr;gap:14px;align-items:start;text-align:left}
.sits{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.sit{position:relative;background:#fff;border:3px solid var(--nu);border-radius:20px;padding:10px;box-shadow:0 4px 10px rgba(92,58,33,.15);cursor:pointer;transition:background .4s,border-color .4s}
.sit .ic{font-size:1.7em;line-height:1}.sit .st{font-size:.88em;font-weight:bold;margin:4px 0 8px;min-height:2.6em}
.sit.armed{border-color:var(--ko);background:#fff4dc;box-shadow:0 0 0 4px #e6c3a0}
.sit.over{background:#ffe9c4;border-color:var(--ko)}
.sit.shake{animation:shake .5s;border-color:var(--no);background:#fbe6df}
.sit.ok{background:#e6f2dd;border-color:var(--ok);cursor:default}
.sit.ok::after{content:"⭐";position:absolute;top:6px;right:8px;font-size:1.3em;animation:tw 1.6s infinite}
.ex{font-size:.75em;color:#3d6a2e;margin-top:6px}
.slot{min-height:54px;border:3px dashed var(--ko);border-radius:14px;background:var(--cr);display:flex;align-items:center;justify-content:center;padding:4px;font-size:.8em;color:#8a6a4c;text-align:center}
.sit.ok .slot{border-style:solid;border-color:var(--ok);background:#f3faee}
@keyframes shake{20%,60%{transform:translateX(-7px)}40%,80%{transform:translateX(7px)}}
.lab{font-weight:bold;text-align:center;margin-bottom:6px}
.pool{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:9px;min-height:60px;align-content:start}
.card{font:inherit;font-size:.85em;font-weight:bold;color:var(--dk);background:#fff;border:3px solid var(--nu);border-radius:16px;padding:10px 8px;min-height:54px;width:100%;box-shadow:0 4px 8px rgba(92,58,33,.2);cursor:grab;user-select:none;-webkit-user-select:none;text-align:center}
.card:hover{background:#fff4dc}.card.pick{border-color:var(--ko);background:#ffe9c4;transform:scale(1.04)}
.card.drag{opacity:.4}.card.placed{background:#fff4dc;border-color:var(--ko);cursor:pointer;padding:6px}
.card.matched{background:#d9ecce;border-color:var(--ok);cursor:default}
.card.land{animation:land .45s}
@keyframes land{0%{transform:translateY(-22px) scale(1.15);opacity:.3}100%{transform:none;opacity:1}}
.empty{grid-column:1/-1;text-align:center;color:#8a6a4c;font-size:.85em;padding:12px}
.fb{border-radius:16px;font-weight:bold;overflow:hidden;max-height:0;transition:max-height .3s,padding .3s;padding:0 12px}
.fb.show{max-height:120px;padding:10px 12px;margin:10px 0}
.fb.ok{background:#e6f2dd;color:#3d6a2e;border:3px solid var(--ok)}.fb.no{background:#fbe6df;color:#8a3a2a;border:3px solid var(--no)}
.acts{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;margin-top:10px}
.stars{font-size:2em;letter-spacing:3px}.stars .off{filter:grayscale(1);opacity:.3}
.score{font-size:clamp(34px,8vw,60px);font-weight:bold;color:var(--ko)}
.stats{display:flex;gap:18px;justify-content:center;flex-wrap:wrap;align-items:center}
.sum{background:var(--be);border-radius:18px;padding:12px 16px;max-width:640px;margin:10px auto;font-size:.95em;text-align:left}
.chest{width:clamp(170px,34vw,250px);height:auto;cursor:pointer;display:block;margin:0 auto 6px;overflow:visible}
.lid{transform-origin:22px 66px;transition:transform .7s}.open .lid{transform:rotate(-38deg)}
.glow{opacity:0;transition:opacity .6s}.open .glow{opacity:1}
.badge{width:clamp(130px,26vw,190px);animation:pop .8s}
@keyframes pop{0%{transform:scale(.2) rotate(-20deg)}70%{transform:scale(1.12)}100%{transform:scale(1)}}
#fx{position:fixed;left:50%;top:40%;z-index:20;pointer-events:none}
.fly{position:absolute;font-size:2rem;animation:fly 1.1s ease-out forwards}
@keyframes fly{to{transform:translate(var(--x),var(--y)) scale(.4) rotate(360deg);opacity:0}}
#conf{position:fixed;inset:0;z-index:15;pointer-events:none;overflow:hidden}
#conf i{position:absolute;top:-20px;width:10px;height:16px;border-radius:2px;animation:fall linear forwards}
@keyframes fall{to{transform:translateY(110vh) rotate(720deg)}}
#toast{position:fixed;left:50%;bottom:20px;transform:translateX(-50%);background:var(--dk);color:#fff;padding:10px 18px;border-radius:16px;z-index:30;display:none;max-width:90%;text-align:center}
.hero{max-width:780px;margin:0 auto}
.hero h1{display:inline-block;max-width:100%;background:linear-gradient(#b97b45,#a8703f);color:#fff6e8;text-shadow:0 2px 0 #7a4d27;border-radius:20px;border-bottom:6px solid #7a4d27;padding:10px clamp(14px,4vw,32px);margin:0 0 10px;box-shadow:0 6px 14px rgba(92,58,33,.3)}
.sub{display:inline-block;background:var(--be);border:2px solid var(--nu);border-radius:999px;padding:3px 16px;font-weight:bold;font-size:.9em;margin:0 0 12px}
.scene{border:5px solid var(--ko);border-radius:26px;overflow:hidden;box-shadow:0 8px 18px rgba(92,58,33,.3);background:var(--cr);line-height:0}
.scene svg{width:100%;height:auto;display:block}
.names{display:flex;justify-content:center;gap:8px;flex-wrap:wrap;margin:12px 0}
.names span{background:#fff;border:2px solid var(--nu);border-radius:999px;padding:3px 14px;font-size:.85em;font-weight:bold}
.how{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin:10px 0 18px}
.how div{background:#fff;border:3px solid var(--nu);border-radius:18px;padding:10px 6px;font-size:.85em;font-weight:bold;box-shadow:0 3px 8px rgba(92,58,33,.12)}
.how b{display:block;font-size:2em;line-height:1.1}
.pulse{animation:pls 2s ease-in-out infinite}@keyframes pls{50%{transform:scale(1.05)}}
.blink{animation:blink 2s infinite}@keyframes blink{50%{opacity:.2}}
@media(max-width:800px){
 .board{grid-template-columns:1fr}
 .pw{order:2;position:sticky;bottom:0;z-index:4;background:rgba(255,246,232,.97);border:3px solid var(--nu);border-radius:16px;padding:8px;max-height:36vh;overflow:auto}
}
@media(max-width:520px){.sits{grid-template-columns:1fr}}
@media(min-width:801px){.pw{position:sticky;top:8px}}
@media(prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}}
</style>
</head>
<body>
<div id="bg"><svg viewBox="0 0 800 500" preserveAspectRatio="xMidYMid slice" aria-hidden="true">
<rect width="800" height="500" fill="#f6e3c8"/><rect y="380" width="800" height="120" fill="#d9b48c"/><g id="awn"></g>
<rect x="40" y="110" width="300" height="190" rx="10" fill="#c99a6b" opacity=".55"/><rect x="460" y="110" width="300" height="190" rx="10" fill="#c99a6b" opacity=".55"/>
<g fill="#a8703f"><rect x="50" y="190" width="280" height="8" rx="3"/><rect x="50" y="270" width="280" height="8" rx="3"/><rect x="470" y="190" width="280" height="8" rx="3"/><rect x="470" y="270" width="280" height="8" rx="3"/></g>
<g id="items"></g><rect x="0" y="360" width="800" height="40" fill="#b07a48"/><rect x="0" y="352" width="800" height="12" fill="#cf9c68"/></svg></div>

<header class="top">
<button class="btn sm" id="bBack">⬅ Peta Misi</button><span class="sp"></span>
<button class="btn sm tg" id="bMus" aria-pressed="true">🎵 Muzik: ON</button>
<button class="btn sm tg" id="bSfx" aria-pressed="true">🔊 Bunyi: ON</button>
</header>

<main>
<section id="sStart" class="screen on"><div class="panel hero">
<h1>Misi 2: Padanan Bijak</h1><br>
<span class="sub">Adab Jual Beli · Pendidikan Islam Tahun 5</span>
<div class="scene" id="scene"></div>
<div class="names"><span>👦 Amir</span><span>👧 Aina</span><span>🧔 Pak Hasan, penjual</span></div>
<div class="how"><div><b>🃏</b>Seret kad jawapan ke situasi</div><div><b>✅</b>Tekan Semak</div><div><b>🏆</b>Kumpul bintang</div></div>
<button class="btn big pulse" id="bStart">🛍️ Mula Misi</button>
<p class="hint">Di telefon atau iPad, ketik situasi kemudian ketik kad jawapan.</p>
</div></section>

<section id="sGame" class="screen"><div class="panel">
<div class="prog"><span id="pt"></span><div class="bar"><i id="pb"></i></div><span id="ps"></span></div>
<p class="hint">Seret atau ketik kad jawapan untuk memadankan dengan situasi. Tekan Semak bila sedia.</p>
<div class="board">
 <div class="sits" id="sits"></div>
 <div class="pw"><div class="lab">🃏 Kad Jawapan</div><div class="pool" id="pool"></div></div>
</div>
<div class="fb" id="fb" role="status" aria-live="polite"></div>
<div class="acts"><button class="btn big" id="bChk">✅ Semak</button><button class="btn big alt" id="bReset">🔄 Mula Semula</button></div>
</div></section>

<section id="sEnd" class="screen"><div class="panel">
<h2>TAHNIAH, JAGUH JUAL BELI BERKAT!</h2>
<div class="chars" id="cEnd"></div>
<div id="chest"></div>
<div class="stats"><div><div class="score" id="sc"></div><b>Markah</b></div><div><div class="stars" id="stz"></div><b id="stn"></b></div><div id="badge"></div></div>
<p id="msg" style="font-weight:bold"></p>
<div class="sum"><b>Rumusan:</b> Adab ketika jual beli seperti jujur, amanah, bersopan, menghormati orang lain dan saling reda menjadikan urusan kita bersih dan diredai Allah. Penjual dan pembeli yang beradab akan dipercayai ramai, hati menjadi tenang dan rezeki lebih berkat.</div>
<div class="acts"><button class="btn big" id="bAgain">🔄 MAIN SEMULA</button><button class="btn big alt" id="bMenu">🏠 KEMBALI KE MENU</button></div>
</div></section>
</main>
<div id="conf"></div><div id="fx"></div><div id="toast"></div>

<script>
"use strict";
/* ====== MASUKKAN URL PETA MISI CANVA ANDA DI SINI ====== */
const PETA_MISI_URL = ""; // contoh: "https://www.canva.com/design/XXXX/view"
/* ======================================================= */

const Q=[
{i:"💰",s:"Amir menerima wang baki berlebihan daripada penjual.",a:"Bersikap jujur",e:"Amir memulangkan baki lebihan."},
{i:"🎒",s:"Penjual mengetahui beg mempunyai zip rosak.",a:"Memaklumkan kecacatan kepada pembeli",e:"Pembeli tidak tertipu."},
{i:"✏️",s:"Aina ingin membeli pensel.",a:"Meminta dengan sopan",e:"“Tolong, boleh saya beli pensel ini?”"},
{i:"🤝",s:"Pembeli dan penjual bersetuju dengan harga barang.",a:"Saling reda",e:"Jual beli sah apabila kedua-dua pihak reda."},
{i:"📚",s:"Harga buku ialah RM4.",a:"Membayar harga yang dipersetujui",e:"Bayar tepat RM4, tidak kurang."},
{i:"🔁",s:"Penjual tersalah memberikan barang yang lebih mahal.",a:"Memaklumkan kesilapan kepada penjual",e:"Supaya tiada pihak yang rugi."},
{i:"🍜",s:"Faris menunggu giliran dan bercakap baik ketika membeli makanan.",a:"Beradab dan menghormati orang lain",e:"Menunggu giliran tanda hormat."},
{i:"🛍️",s:"Penjual menerangkan kecacatan barang sebelum jual beli.",a:"Amanah dan jujur",e:"Tidak menyembunyikan kecacatan."}];
const N=Q.length;
const $=id=>document.getElementById(id);
const shuf=a=>{a=a.slice();for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]]}return a};

/* ---------- Ilustrasi SVG ---------- */
function kidG(o){
 const sk=o.sk,br="#3b2417";
 let s='<ellipse cx="50" cy="135" rx="30" ry="5" fill="#0002"/>';
 s+=`<rect x="35" y="110" width="12" height="22" rx="5" fill="${o.pt}"/><rect x="53" y="110" width="12" height="22" rx="5" fill="${o.pt}"/><ellipse cx="39" cy="132" rx="9" ry="4.5" fill="#4a2f1c"/><ellipse cx="61" cy="132" rx="9" ry="4.5" fill="#4a2f1c"/>`;
 s+=`<rect x="13" y="72" width="15" height="36" rx="7.5" fill="${o.cl}"/><circle cx="20.5" cy="110" r="6.5" fill="${sk}"/>`;
 s+=o.long?`<path d="M24 72q0-9 12-9h28q12 0 12 9l7 56H17z" fill="${o.cl}"/><path d="M17 126h66" stroke="#0002" stroke-width="3"/>`:`<rect x="23" y="64" width="54" height="54" rx="16" fill="${o.cl}"/>`;
 if(o.sash)s+=`<rect x="23" y="98" width="54" height="11" rx="4" fill="#a8703f"/><path d="M33 103.5l4-3 4 3-4 3zM47 103.5l4-3 4 3-4 3zM61 103.5l4-3 4 3-4 3z" fill="#e0a94a"/><circle cx="50" cy="76" r="2.3" fill="#e0a94a"/><circle cx="50" cy="87" r="2.3" fill="#e0a94a"/>`;
 if(o.ap)s+=`<path d="M36 74h28v44q0 4-4 4H40q-4 0-4-4z" fill="#fff6e8" stroke="#e6c3a0" stroke-width="2"/><rect x="41" y="96" width="18" height="12" rx="3" fill="#f3e2c7" stroke="#e6c3a0" stroke-width="1.5"/><path d="M36 76l-9-8M64 76l9-8" stroke="#e6c3a0" stroke-width="3"/>`;
 s+=`<g transform="rotate(${o.wave?-145:0} 79 78)"><rect x="72" y="72" width="15" height="36" rx="7.5" fill="${o.cl}"/><circle cx="79.5" cy="110" r="6.5" fill="${sk}"/></g>`;
 s+=`<rect x="43" y="58" width="14" height="14" rx="5" fill="${sk}"/>`;
 if(o.hj){
  s+=`<path d="M12 56C12 20 29 8 50 8s38 12 38 48c0 14-6 25-12 32H24c-6-7-12-18-12-32z" fill="${o.hr}"/><path d="M26 84q24 9 48 0" stroke="#0002" stroke-width="2.5" fill="none"/><circle cx="71" cy="78" r="3.5" fill="#e0a94a"/><ellipse cx="50" cy="46" rx="22" ry="24" fill="${sk}" stroke="#a46d49" stroke-width="2"/>`;
 }else{
  s+=`<circle cx="22" cy="46" r="5.5" fill="${sk}"/><circle cx="78" cy="46" r="5.5" fill="${sk}"/><ellipse cx="50" cy="42" rx="28" ry="27" fill="${sk}"/><path d="M23 30q-3 14 3 24q1-14 5-24zM77 30q3 14-3 24q-1-14-5-24z" fill="${o.hr}"/>`;
  if(o.cap==="songkok")s+=`<path d="M27 28L30 6h40l3 22q-23 7-46 0z" fill="#2b2b2b"/><path d="M28 21q22 6 44 0" stroke="#e0a94a" stroke-width="2.5" fill="none"/>`;
  if(o.cap==="kopiah")s+=`<path d="M26 28q0-22 24-22t24 22q-24 8-48 0z" fill="#fff" stroke="#e6c3a0" stroke-width="2"/><path d="M28 21q22 7 44 0M33 12q17 6 34 0" stroke="#e6c3a0" stroke-width="2" fill="none"/>`;
 }
 s+=`<path d="M32 36q5-4 11-1M57 35q6-3 11 1" stroke="${br}" stroke-width="2.6" fill="none" stroke-linecap="round"/><ellipse cx="39" cy="45" rx="4.2" ry="5" fill="${br}"/><ellipse cx="61" cy="45" rx="4.2" ry="5" fill="${br}"/><circle cx="40.7" cy="43" r="1.7" fill="#fff"/><circle cx="62.7" cy="43" r="1.7" fill="#fff"/><ellipse cx="33" cy="55" rx="5" ry="3.2" fill="#f2a58e" opacity=".55"/><ellipse cx="67" cy="55" rx="5" ry="3.2" fill="#f2a58e" opacity=".55"/><path d="M47 52q3 2.5 6 0" stroke="#b9805e" stroke-width="1.6" fill="none" stroke-linecap="round"/>`;
 if(o.mus)s+=`<path d="M37 56q6-6 13-1q7-5 13 1q-6 3-13 1q-7 2-13-1z" fill="#7a5a42"/>`;
 s+=`<path d="M43 ${o.mus?59:57}q7 9 14 0z" fill="#a3473a"/>`;
 return s;
}
const kid=o=>`<svg class="ch" viewBox="0 0 100 140" aria-hidden="true">${kidG(o)}</svg>`;
const AMIR_O={sk:"#e9b98f",hr:"#3b2417",cl:"#9bb58c",pt:"#7d6a55",cap:"songkok",sash:1,wave:1};
const AINA_O={sk:"#f3cfa8",hr:"#c48b66",cl:"#e3a9a0",pt:"#e3a9a0",hj:1,long:1};
const JUAL_O={sk:"#d9a478",hr:"#9a8c80",cl:"#c9a27a",pt:"#6b4a33",cap:"kopiah",ap:1,mus:1};
const fig=(s,n)=>`<figure>${s}<figcaption>${n}</figcaption></figure>`;
const CH=fig(kid(AMIR_O),"Amir")+fig(kid(AINA_O),"Aina")+fig(kid(JUAL_O),"Penjual");
function sceneSvg(){
 const g=(o,x,y,k)=>`<g transform="translate(${x} ${y}) scale(${k})">${kidG(o)}</g>`;
 let st="";for(let i=0;i<16;i++)st+=`<rect x="${i*40}" y="0" width="40" height="34" fill="${i%2?'#fff6e8':'#c99a6b'}"/><path d="M${i*40} 34q20 20 40 0z" fill="${i%2?'#fff6e8':'#c99a6b'}"/>`;
 let sh="";[["📚",40],["✏️",85],["📒",130],["📏",175],["🖍️",455],["✂️",500],["🎒",545],["🧃",590]].forEach(a=>{sh+=`<text x="${a[1]}" y="98" font-size="30">${a[0]}</text>`});
 return `<svg viewBox="0 0 640 340" role="img" aria-label="Kedai Pak Hasan: Amir, penjual dan Aina">
 <defs><linearGradient id="wl" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#fff6e8"/><stop offset="1" stop-color="#f1dcbc"/></linearGradient></defs>
 <rect width="640" height="340" fill="url(#wl)"/><rect y="268" width="640" height="72" fill="#d9b48c"/>${st}
 <rect x="25" y="100" width="190" height="8" rx="3" fill="#a8703f"/><rect x="425" y="100" width="190" height="8" rx="3" fill="#a8703f"/>${sh}
 <path d="M270 34v22M370 34v22" stroke="#7a4d27" stroke-width="3"/>
 <rect x="215" y="54" width="210" height="40" rx="12" fill="#fff6e8" stroke="#a8703f" stroke-width="4"/><text x="320" y="82" text-anchor="middle" font-family="Trebuchet MS,Arial" font-weight="bold" font-size="22" fill="#5c3a21">Kedai Pak Hasan</text>
 ${g(AMIR_O,55,96,1.45)}${g(JUAL_O,238,88,1.6)}${g(AINA_O,425,96,1.45)}
 <rect y="252" width="640" height="88" fill="#a8703f"/><rect y="244" width="640" height="14" rx="6" fill="#cf9c68"/>
 <path d="M0 290h640M0 316h640" stroke="#8a5a34" stroke-width="2"/>
 <text x="40" y="246" font-size="28">📦</text><text x="150" y="246" font-size="26">🍬</text><text x="500" y="246" font-size="28">📚</text><text x="580" y="246" font-size="26">✏️</text>
 <text class="blink" x="205" y="140" font-size="22">✨</text><text class="blink" x="590" y="150" font-size="22" style="animation-delay:.7s">✨</text><text class="blink" x="30" y="170" font-size="20" style="animation-delay:1.2s">✨</text></svg>`;
}
(function(){
 let a="";for(let i=0;i<16;i++)a+=`<rect x="${i*50}" y="0" width="50" height="62" fill="${i%2?'#fff6e8':'#c99a6b'}"/><path d="M${i*50} 62q25 22 50 0z" fill="${i%2?'#fff6e8':'#c99a6b'}"/>`;
 $("awn").innerHTML=a;
 const cols=["#e6c3a0","#a8703f","#fff6e8","#d9a066","#8a5a34"];let it="";
 [[50,190],[50,270],[470,190],[470,270]].forEach((p,r)=>{for(let k=0;k<7;k++){const h=22+((k*7+r*5)%4)*9;it+=`<rect x="${p[0]+8+k*38}" y="${p[1]-h}" width="28" height="${h}" rx="5" fill="${cols[(k+r)%5]}"/>`}});
 $("items").innerHTML=it;$("scene").innerHTML=sceneSvg();$("cEnd").innerHTML=CH;
})();

/* ---------- Audio (Web Audio API) ---------- */
let AC=null,musicOn=true,sfxOn=true,mTimer=null,mStep=0,unlocked=false;
function ac(){if(!AC){try{AC=new(window.AudioContext||window.webkitAudioContext)()}catch(e){AC=null}}if(AC&&AC.state==="suspended")AC.resume();return AC}
function tone(f,t,d,ty,v){const a=ac();if(!a||!f)return;const o=a.createOscillator(),g=a.createGain(),s=a.currentTime+t;o.type=ty||"sine";o.frequency.value=f;g.gain.setValueAtTime(.0001,s);g.gain.exponentialRampToValueAtTime(v||.12,s+.02);g.gain.exponentialRampToValueAtTime(.0001,s+d);o.connect(g);g.connect(a.destination);o.start(s);o.stop(s+d+.05)}
const MEL=[523,587,659,784,659,587,523,0,587,659,784,880,784,659,587,0],BAS=[262,262,196,220];
function startMusic(){if(mTimer||!ac())return;mTimer=setInterval(()=>{tone(MEL[mStep%16],0,.3,"triangle",.045);if(mStep%4===0)tone(BAS[(mStep/4)%4],0,.5,"sine",.05);mStep++},300)}
function stopMusic(){clearInterval(mTimer);mTimer=null}
function sfx(k){if(!sfxOn)return;
 if(k==="click")tone(660,0,.08,"square",.05);
 if(k==="ok")[523,659,784,1047].forEach((f,i)=>tone(f,i*.1,.25,"triangle",.14));
 if(k==="no"){tone(260,0,.18,"sine",.12);tone(200,.16,.28,"sine",.12)}
 if(k==="win")[523,659,784,1047,784,1047,1319,1568].forEach((f,i)=>tone(f,i*.14,.35,"triangle",.14))}
function firstTouch(e){if(unlocked)return;if(e.target.closest&&e.target.closest(".tg"))return;unlocked=true;ac();if(musicOn)startMusic()}
document.addEventListener("pointerdown",firstTouch);document.addEventListener("keydown",firstTouch);
$("bMus").onclick=()=>{unlocked=true;ac();musicOn=!musicOn;musicOn?startMusic():stopMusic();$("bMus").textContent="🎵 Muzik: "+(musicOn?"ON":"OFF");$("bMus").setAttribute("aria-pressed",musicOn);sfx("click")};
$("bSfx").onclick=()=>{unlocked=true;ac();sfxOn=!sfxOn;$("bSfx").textContent="🔊 Bunyi: "+(sfxOn?"ON":"OFF");$("bSfx").setAttribute("aria-pressed",sfxOn);sfx("click")};

/* ---------- Navigasi ---------- */
function show(id){document.querySelectorAll(".screen").forEach(s=>s.classList.toggle("on",s.id===id));window.scrollTo(0,0)}
function toast(t){const e=$("toast");e.textContent=t;e.style.display="block";clearTimeout(toast.t);toast.t=setTimeout(()=>{e.style.display="none"},3500)}
function back(){sfx("click");
 if(PETA_MISI_URL.indexOf("http")!==0){toast("URL Peta Misi belum dimasukkan. Edit PETA_MISI_URL dalam kod.");return}
 const w=window.open(PETA_MISI_URL,"_blank","noopener");
 if(!w)toast("Pelayar menyekat tetingkap baharu. Benarkan pop-up untuk membuka Peta Misi.")}
$("bBack").onclick=back;

/* ---------- Permainan ---------- */
let G=null,gidC=0;const sel={sit:null,ans:null};
function newGame(){
 let o;do{o=shuf([...Array(N).keys()])}while(o.every((v,i)=>v===i));
 G={gid:++gidC,slots:Array(N).fill(null),lock:Array(N).fill(false),tried:Array(N).fill(false),score:0,order:o,busy:false,shake:[],land:-1};
 sel.sit=null;sel.ans=null;clearFb();$("fx").innerHTML="";$("conf").innerHTML="";$("chest").innerHTML="";
 show("sGame");render();
}
function clearFb(){const f=$("fb");f.className="fb";f.textContent=""}
function mkCard(a,placed){
 const c=document.createElement(placed?"div":"button");
 c.className="card"+(placed?" placed":"")+(sel.ans===a?" pick":"");
 c.textContent=Q[a].a;if(!placed)c.type="button";c.draggable=!G.busy;
 c.addEventListener("dragstart",e=>{e.dataTransfer.setData("text",String(a));e.dataTransfer.effectAllowed="move";c.classList.add("drag")});
 c.addEventListener("dragend",()=>c.classList.remove("drag"));
 if(!placed)c.onclick=()=>ansClick(a);
 return c;
}
function render(){
 const done=G.lock.filter(Boolean).length;
 $("pt").textContent=done+" daripada "+N+" pasangan selesai";
 $("pb").style.width=(done/N*100)+"%";
 $("ps").innerHTML='<span class="tw">⭐</span> '+G.score;
 const S=$("sits");S.innerHTML="";
 Q.forEach((q,i)=>{
  const d=document.createElement("div");
  d.className="sit"+(G.lock[i]?" ok":"")+(sel.sit===i?" armed":"")+(G.shake.indexOf(i)>=0?" shake":"");
  d.tabIndex=G.lock[i]?-1:0;d.setAttribute("role","button");
  d.innerHTML='<div class="ic"></div><div class="st"></div><div class="slot"></div>';
  d.children[0].textContent=q.i;d.children[1].textContent=q.s;
  const sl=d.children[2];
  if(G.slots[i]===null)sl.textContent="Letakkan jawapan di sini";
  else{const c=mkCard(G.slots[i],true);if(G.lock[i]){c.draggable=false;c.classList.add("matched")}if(G.land===i)c.classList.add("land");sl.appendChild(c)}
  if(G.lock[i]){const e=document.createElement("div");e.className="ex";e.textContent="✨ "+q.e;d.appendChild(e)}
  d.onclick=()=>sitClick(i);
  d.onkeydown=e=>{if(e.key==="Enter"||e.key===" "){e.preventDefault();sitClick(i)}};
  d.ondragover=e=>{if(!G.lock[i]&&!G.busy){e.preventDefault();d.classList.add("over")}};
  d.ondragleave=()=>d.classList.remove("over");
  d.ondrop=e=>{e.preventDefault();d.classList.remove("over");const a=parseInt(e.dataTransfer.getData("text"),10);if(!isNaN(a))place(i,a)};
  S.appendChild(d);
 });
 const P=$("pool");P.innerHTML="";
 const free=G.order.filter(a=>G.slots.indexOf(a)<0);
 free.forEach(a=>P.appendChild(mkCard(a,false)));
 if(!free.length){const e=document.createElement("div");e.className="empty";e.textContent="Semua kad sudah diletakkan. Tekan Semak!";P.appendChild(e)}
 const any=G.slots.some((a,i)=>a!==null&&!G.lock[i]);
 $("bChk").disabled=!any||G.busy;
}
function place(i,a){
 if(G.lock[i]||G.busy)return;
 if(G.lock[a]&&G.slots[a]===a)return;
 for(let k=0;k<N;k++)if(G.slots[k]===a&&!G.lock[k])G.slots[k]=null;
 G.slots[i]=a;sel.sit=null;sel.ans=null;G.land=i;clearFb();sfx("click");render();G.land=-1;
}
function sitClick(i){
 if(G.lock[i]||G.busy)return;
 if(sel.ans!==null){place(i,sel.ans);return}
 if(G.slots[i]!==null){G.slots[i]=null;sel.sit=null;clearFb();sfx("click");render();return}
 sel.sit=(sel.sit===i)?null:i;sfx("click");render();
}
function ansClick(a){
 if(G.busy)return;
 if(sel.sit!==null){place(sel.sit,a);return}
 sel.ans=(sel.ans===a)?null:a;sfx("click");render();
}
/* letak kad kembali ke kumpulan kad dengan menyeret ke kawasan kad jawapan */
const poolEl=$("pool").parentNode;
poolEl.ondragover=e=>{if(!G.busy)e.preventDefault()};
poolEl.ondrop=e=>{e.preventDefault();if(G.busy)return;const a=parseInt(e.dataTransfer.getData("text"),10);if(isNaN(a))return;
 for(let k=0;k<N;k++)if(G.slots[k]===a&&!G.lock[k])G.slots[k]=null;render()};

const stars=n=>{const L=$("fx");for(let k=0;k<n;k++){const s=document.createElement("span");s.textContent="⭐";s.className="fly";const a=Math.random()*6.283,d=70+Math.random()*150;s.style.setProperty("--x",Math.cos(a)*d+"px");s.style.setProperty("--y",Math.sin(a)*d+"px");L.appendChild(s);setTimeout(()=>s.remove(),1200)}};

$("bChk").onclick=()=>{
 if(G.busy)return;
 let r=0,w=0;G.shake=[];
 for(let i=0;i<N;i++){
  if(G.slots[i]===null||G.lock[i])continue;
  if(G.slots[i]===i){G.lock[i]=true;if(!G.tried[i])G.score++;r++}   /* markah hanya sekali bagi setiap pasangan */
  else{G.shake.push(i);w++}
  G.tried[i]=true;
 }
 if(!r&&!w){toast("Letakkan sekurang-kurangnya satu kad jawapan dahulu.");return}
 sel.sit=null;sel.ans=null;G.busy=true;const gid=G.gid;
 const f=$("fb");f.className="fb show "+(w?"no":"ok");
 if(r&&!w)f.textContent="🌟 Hebat! "+r+" pasangan betul!";
 else if(r)f.textContent="✅ "+r+" pasangan betul. "+w+" belum tepat, cuba lagi! 💪";
 else f.textContent="Belum tepat. Fikir semula dan cuba lagi! 🤔";
 if(r){sfx("ok");stars(8+r*3)}
 if(w)setTimeout(()=>{if(gidC===gid)sfx("no")},r?450:0);
 render();
 setTimeout(()=>{
  if(gidC!==gid)return;
  G.shake.forEach(i=>{G.slots[i]=null});G.shake=[];G.busy=false;render();
  if(G.lock.every(Boolean))setTimeout(()=>{if(gidC===gid)win()},500);
 },w?1100:900);
};
$("bReset").onclick=()=>{sfx("click");newGame()};

/* ---------- Skrin kemenangan ---------- */
function confetti(){
 if(window.matchMedia&&matchMedia("(prefers-reduced-motion:reduce)").matches)return;
 const L=$("conf"),c=["#e0a94a","#a8703f","#e6c3a0","#6a9a5b","#d9a0a0","#8fa9b8","#fff6e8"];
 for(let k=0;k<80;k++){const p=document.createElement("i");p.style.left=Math.random()*100+"%";p.style.background=c[k%c.length];p.style.animationDuration=(2.5+Math.random()*2.5)+"s";p.style.animationDelay=(Math.random()*1.2)+"s";L.appendChild(p)}
 setTimeout(()=>{L.innerHTML=""},7000);
}
function chestSvg(){return `<svg class="chest" id="chSvg" viewBox="-30 -55 200 180" role="button" aria-label="Peti ganjaran" overflow="visible">
<ellipse cx="70" cy="112" rx="55" ry="6" fill="#0002"/>
<g class="glow"><ellipse cx="70" cy="58" rx="50" ry="26" fill="#ffe08a" opacity=".7"/><text x="28" y="40" font-size="22">⭐</text><text x="60" y="12" font-size="28">⭐</text><text x="94" y="40" font-size="22">⭐</text><text x="8" y="8" font-size="18">✨</text><text x="116" y="10" font-size="18">✨</text><text x="44" y="56" font-size="18">🪙</text><text x="78" y="56" font-size="18">🪙</text></g>
<rect x="20" y="62" width="100" height="48" rx="8" fill="#a8703f" stroke="#5c3a21" stroke-width="3"/>
<rect x="20" y="76" width="100" height="8" fill="#e0a94a"/>
<g class="lid"><path d="M18 66V52a52 34 0 0 1 104 0v14z" fill="#8a5a34" stroke="#5c3a21" stroke-width="3"/><rect x="18" y="56" width="104" height="8" fill="#e0a94a"/></g>
<rect x="62" y="70" width="16" height="18" rx="4" fill="#e0a94a" stroke="#5c3a21" stroke-width="2"/><circle cx="70" cy="78" r="3" fill="#5c3a21"/></svg>`}
function win(){
 const gid=G.gid;show("sEnd");sfx("win");confetti();setTimeout(()=>{if(gidC===gid)confetti()},2500);
 $("chest").innerHTML=chestSvg();
 const ch=$("chSvg");const openIt=()=>{ch.classList.add("open");stars(12);sfx("ok")};
 ch.onclick=()=>{ch.classList.remove("open");setTimeout(openIt,350)};
 setTimeout(()=>{if(gidC===gid&&$("chSvg"))openIt()},1000);
 const s=G.score;
 $("sc").textContent=s+" / "+N;
 let st="";for(let i=0;i<N;i++)st+=`<span class="${i<s?"":"off"}">⭐</span>`;
 $("stz").innerHTML=st;$("stn").textContent="Bintang: "+s+" / "+N;
 $("msg").textContent=s===N?"Cemerlang! Semua padanan betul pada percubaan pertama! 🏆":s>=6?"Bagus! Kamu hampir sempurna! 👏":s>=4?"Usaha yang baik! Cuba lagi untuk markah lebih tinggi. 💪":"Syabas kerana tidak berputus asa! Main semula untuk markah lebih tinggi. 🌱";
 const t=s===N?["Emas","#e0a94a"]:s>=6?["Perak","#b8bcc2"]:["Gangsa","#c98f5a"];
 $("badge").innerHTML=`<svg class="badge" viewBox="0 0 200 240" role="img" aria-label="Lencana Detektif Adab ${t[0]}">
 <path d="M60 140l-20 80 40-18 20 20 20-70z" fill="#a8703f"/><path d="M140 140l20 80-40-18-20 20-20-70z" fill="#8a5a34"/>
 <circle cx="100" cy="95" r="82" fill="${t[1]}" stroke="#a8703f" stroke-width="8"/><circle cx="100" cy="95" r="64" fill="#fff6e8" stroke="#a8703f" stroke-width="4"/>
 <circle cx="92" cy="86" r="26" fill="#f3e2c7" stroke="#5c3a21" stroke-width="7"/><path d="M111 105l28 28" stroke="#5c3a21" stroke-width="10" stroke-linecap="round"/>
 <path d="M92 74l4 9 10 1-8 6 3 10-9-6-9 6 3-10-8-6 10-1z" fill="${t[1]}"/>
 <rect x="22" y="170" width="156" height="42" rx="10" fill="#a8703f"/><text x="100" y="188" text-anchor="middle" font-family="Arial" font-weight="bold" font-size="15" fill="#fff6e8">Detektif Adab</text><text x="100" y="205" text-anchor="middle" font-family="Arial" font-size="13" fill="#fff6e8">${t[0]}</text></svg>`;
}
$("bStart").onclick=()=>{sfx("click");newGame()};
$("bAgain").onclick=()=>{sfx("click");newGame()};
$("bMenu").onclick=()=>{sfx("click");G=null;gidC++;$("conf").innerHTML="";$("fx").innerHTML="";show("sStart")};
</script>
</body>
</html>
