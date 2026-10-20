<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SFPP Receive 2026</title>
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html5-qrcode/2.3.8/html5-qrcode.min.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Prompt:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  body{font-family:'Prompt',sans-serif;-webkit-tap-highlight-color:transparent;background:#f1f5fb}
  .fld{width:100%;padding:.7rem .9rem;font-size:.9rem;border:1px solid #cbd5e1;border-radius:1rem;background:#fff}
  .fld:focus,button:focus-visible{outline:2px solid #2563eb;outline-offset:1px}
  .lbl{display:block;font-size:.85rem;font-weight:700;margin-bottom:.4rem}
  .sec{display:flex;align-items:center;gap:.6rem;font-weight:700;font-size:1.05rem;margin-bottom:1rem}
  .sec b{display:grid;place-items:center;width:2rem;height:2rem;border-radius:.6rem;color:#fff;font-size:.9rem}
  .opt{display:flex;align-items:center;gap:.75rem;width:100%;text-align:left;padding:.9rem 1rem;border:2px solid #e2e8f0;border-radius:1rem;background:#fff;font-weight:600;cursor:pointer}
  .opt i{width:1.4rem;height:1.4rem;border-radius:50%;border:2px solid #cbd5e1;flex:none}
  .opt[aria-pressed=true]{border-color:#4ade80;background:#f0fdf4}
  .opt[aria-pressed=true] i{border:7px solid #4d9a66}
  .opt.d[aria-pressed=true]{border-color:#f0b429;background:#fffbeb}
  .opt.d[aria-pressed=true] i{border-color:#e8941a}
  .sh{padding:.8rem 0;border:2px solid #e2e8f0;border-radius:1rem;background:#fff;font-weight:700}
  .sh[aria-pressed=true]{background:linear-gradient(#e8961f,#dd6a14);color:#fff;border-color:#f6c744}
  .pill{display:inline-flex;gap:.5rem;align-items:center;padding:.5rem 1rem;border-radius:999px;border:1px solid;font-size:.9rem}
  .pill.off{background:#fffbeb;border-color:#fde68a;color:#92400e}
  .pill.on{background:#ecfdf5;border-color:#a7f3d0;color:#065f46}
  .pill::before{content:"";width:.7rem;height:.7rem;border-radius:50%;background:currentColor}
  .key{padding:1rem 0;font-size:1.5rem;font-weight:600;border-radius:1rem;background:#f8fafc;border:1px solid #e2e8f0}
  .key:active{background:#e2e8f0}
  .lnk{font-size:.8rem;font-weight:700;color:#16a34a;text-decoration:underline;cursor:pointer}
</style>
</head>
<body class="min-h-screen p-3 sm:p-6 text-slate-800">
<div class="max-w-xl mx-auto">

<!-- ========== HOME ========== -->
<section id="home" class="bg-white rounded-3xl shadow-xl border border-slate-200 overflow-hidden">
  <div class="h-1.5 bg-gradient-to-r from-emerald-400 to-blue-500"></div>
  <div class="p-6 space-y-6">
    <button id="goForm" class="w-full rounded-3xl p-10 text-white text-center shadow-lg bg-gradient-to-br from-emerald-500 to-teal-500 active:scale-[.98] transition border-4 border-emerald-200">
      <div class="mx-auto mb-4 w-16 h-16 rounded-2xl bg-white/20 grid place-items-center text-3xl">📝</div>
      <div class="text-4xl font-bold">SFPP Receive</div>
      <div class="mt-3 inline-block bg-white text-slate-800 rounded-full px-5 py-2 text-sm font-semibold">(เพื่อเข้าสู่แบบฟอร์มกรอกข้อมูล)</div>
    </button>
    <hr>
    <div class="space-y-2">
      <div class="font-bold">สถานะระบบ:</div>
      <div><span id="stSheet" class="pill off"></span></div>
      <div><span id="stHook" class="pill off"></span></div>
      <div class="text-sm text-slate-500">· บันทึกแล้ว <b id="cnt" class="text-blue-600 text-lg">0</b> รายการ</div>
    </div>
    <div class="flex justify-end gap-3">
      <button id="shareBtn" class="px-5 py-3 rounded-2xl border border-blue-200 bg-blue-50 text-blue-700 font-bold">🔗 แชร์ลิงก์ฟอร์ม</button>
      <button class="adminBtn px-6 py-3 rounded-2xl bg-red-600 text-white font-bold shadow">🛡 Admin</button>
    </div>
  </div>
</section>

<!-- ========== FORM ========== -->
<section id="formView" class="hidden space-y-4">
  <header class="bg-white rounded-2xl border border-slate-200 p-4 flex items-center gap-3">
    <div class="w-12 h-12 rounded-2xl bg-gradient-to-br from-blue-500 to-indigo-600 text-white font-bold grid place-items-center flex-none">SF</div>
    <div class="flex-1 min-w-0">
      <h1 class="font-bold leading-tight">SENDING &amp; RECEIVE SFPP 2026</h1>
      <p class="text-xs text-slate-500">บันทึกรายการส่งและรับ SFPP พร้อมระบบสแกนบาร์โค้ด</p>
    </div>
    <button id="goHome" class="text-xs font-bold border border-slate-200 rounded-xl px-3 py-2 flex-none">← หน้าแรก</button>
  </header>

  <form id="f" novalidate class="bg-white rounded-3xl border border-slate-200 shadow-xl overflow-hidden">
    <div class="h-1.5 bg-gradient-to-r from-indigo-500 via-purple-500 to-emerald-400"></div>
    <div class="p-5 space-y-8">

      <div class="space-y-5">
        <div class="sec"><b class="bg-blue-600">1</b>ข้อมูลวัน เวลา และ SHIFT</div>
        <div>
          <div class="flex justify-between items-center mb-1">
            <label class="lbl !mb-0" for="date">📅 Date (English) / วันที่ <span class="text-rose-500">*</span></label>
            <span id="dBadge" class="font-mono font-bold text-blue-700 bg-blue-50 border border-blue-200 rounded-full px-3 text-sm"></span>
          </div>
          <input class="fld" type="date" id="date" required>
          <div class="flex justify-between text-sm mt-1.5"><span id="dLong" class="text-slate-600"></span><button type="button" id="todayBtn" class="font-bold text-blue-600">Today</button></div>
        </div>
        <div>
          <div class="flex justify-between items-center mb-1">
            <label class="lbl !mb-0" for="time">🕑 Time / เวลาบันทึก <span class="text-rose-500">*</span></label>
            <button type="button" id="nowBtn" class="text-xs font-bold text-emerald-700 bg-emerald-50 border border-emerald-200 rounded-full px-3 py-1">⚡ ตอนนี้ (Now)</button>
          </div>
          <input class="fld font-mono" type="time" id="time" step="1" required>
        </div>
        <div><span class="lbl">Shift * <span class="float-right font-semibold text-slate-400 text-xs">กะการทำงาน</span></span><div id="shiftG" class="grid grid-cols-4 gap-2"></div></div>
        <div><span class="lbl">Receive ( รับ SFPP ) &amp; Return ( ส่งคืน SFPP ) *</span><div id="typeG" class="space-y-3"></div></div>
      </div>

      <hr>
      <div><div class="sec"><b class="bg-purple-600">2</b>DEPARTMENT (แผนก/พื้นที่) *</div><div id="deptG" class="space-y-3"></div></div>

      <hr>
      <div>
        <div class="sec"><b class="bg-sky-600">3</b><span id="whoTitle"></span></div>
        <div id="personBox"></div>
      </div>

      <hr>
      <div>
        <div class="sec"><b class="bg-blue-600">4</b><span id="poTitle">PROCESS ORDER NUMBER &amp; สแกน BARCODE</span></div>
        <p class="text-sm text-slate-500 -mt-2 mb-3">กรอกตัวเลข หรือกดสแกน Barcode / QR Code (ต้องกรอกอย่างน้อย 1 Line)</p>
        <div id="poG" class="space-y-3"></div>
      </div>

      <hr>
      <div>
        <div class="sec"><b class="bg-emerald-600">5</b>QA SEND (ผู้ส่ง SFPP) *</div>
        <div id="qaBox"></div>
        <label class="lbl mt-4" for="notes">หมายเหตุเพิ่มเติม (Optional Notes)</label>
        <textarea class="fld" id="notes" rows="3" maxlength="500" placeholder="ระบุข้อความเพิ่มเติมหรือบันทึกพิเศษ..."></textarea>
      </div>

      <hr>
      <div class="text-sm space-y-2">
        <div>📄 Google Sheet: <span id="fSheet" class="pill off !py-1"></span></div>
        <div>Webhook: <span id="fHook" class="pill off !py-1"></span></div>
      </div>
      <div class="flex gap-3">
        <button type="button" id="clearBtn" class="px-5 rounded-2xl border border-rose-200 bg-rose-50 text-rose-700 font-bold">↺ ล้างค่า</button>
        <button type="submit" id="submit" class="flex-1 py-4 rounded-2xl text-white font-bold bg-gradient-to-r from-blue-600 to-indigo-600 shadow-lg active:scale-[.98] disabled:opacity-60">➤ บันทึกข้อมูลลงระบบ (Submit SFPP)</button>
      </div>
      <div class="flex justify-between items-center text-sm text-slate-400">
        <span>แบบฟอร์ม SENDING &amp; RECEIVE SFPP 2026</span>
        <button type="button" class="adminBtn px-5 py-3 rounded-2xl bg-red-600 text-white font-bold">🛡 Admin</button>
      </div>
    </div>
  </form>
</section>
</div>

<div id="toast" role="alert" class="hidden fixed top-3 left-1/2 -translate-x-1/2 z-[60] max-w-[92vw] px-5 py-3 rounded-2xl shadow-xl text-sm font-semibold"></div>
<div id="modal" class="hidden fixed inset-0 z-50 bg-slate-900/60 items-center justify-center p-3">
  <div id="mBody" class="bg-white rounded-3xl w-full max-w-md max-h-[92vh] overflow-y-auto p-5"></div>
</div>

<script>
const CFG = {
  Blending:{lines:[1,2,3,4], people:["Santi","Jukapong","Somporn","Seksan","Chalermvuth","Sanya","Thun","Jirasak"]},
  Extruder:{lines:[1,2,3,4], people:["Thanaphat","Pattaraphong","Kriangkrai","Sab","Sirisak","Teerapol","Kittisak","Piya","Niran","Sompong","Samart","Prasit"]},
  LPC:{lines:[5,6], people:["Kiattisak","Supanya","Arnat"]}
};
const QA = ["Chalinee","Natdanai","Watchara","Nuttapong","Pirom","Wanna","Parichat","Theeraphong","Wichuda"];
const TYPES = [
  {v:'Receive ( รับ SFPP )', who:'ผู้มารับ SFPP (Receiver)'},
  {v:'Return ( ส่งคืน SFPP )', who:'ผู้ส่งคืน SFPP (Returner)'}
];
const LINE_CLR = ['blue','cyan','emerald','amber','violet','rose'];
const BOX = {blue:'bg-blue-50 border-blue-200',cyan:'bg-cyan-50 border-cyan-200',emerald:'bg-emerald-50 border-emerald-200',amber:'bg-amber-50 border-amber-200',violet:'bg-violet-50 border-violet-200',rose:'bg-rose-50 border-rose-200'};
const BTN = {blue:'bg-blue-600',cyan:'bg-cyan-600',emerald:'bg-emerald-600',amber:'bg-orange-500',violet:'bg-violet-600',rose:'bg-rose-600'};
const MON = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
const s = {type:TYPES[0], shift:'A', dept:'Blending'};
const $ = id => document.getElementById(id);
const pad = n => String(n).padStart(2,'0');
const esc = t => String(t==null?'':t).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));

const LS = {
  get:(k,d)=>{ try{ const v=localStorage.getItem('sfpp_'+k); return v==null?d:JSON.parse(v); }catch(e){ return d; } },
  set:(k,v)=>{ try{ localStorage.setItem('sfpp_'+k, JSON.stringify(v)); }catch(e){} }
};

/* ---------- helpers ---------- */
function todayLocal(){ const d=new Date(); return `${d.getFullYear()}-${pad(d.getMonth()+1)}-${pad(d.getDate())}`; }
function nowLocal(){ const d=new Date(); return `${pad(d.getHours())}:${pad(d.getMinutes())}:${pad(d.getSeconds())}`; }
function fmtDate(v){ const p=(v||'').split('-'); return p.length===3 ? `${p[2]}-${MON[+p[1]-1]}-${p[0]}` : ''; }
function toast(ok, msg){
  const t=$('toast'); t.textContent=(ok?'✅ ':'⚠️ ')+msg;
  t.className='fixed top-3 left-1/2 -translate-x-1/2 z-[60] max-w-[92vw] px-5 py-3 rounded-2xl shadow-xl text-sm font-semibold '+(ok?'bg-emerald-600 text-white':'bg-rose-600 text-white');
  clearTimeout(toast.t); toast.t=setTimeout(()=>t.classList.add('hidden'),4000);
}
function openModal(html){ $('mBody').innerHTML=html; $('modal').classList.remove('hidden'); $('modal').classList.add('flex'); }
function closeModal(){ stopScan(); $('modal').classList.add('hidden'); $('modal').classList.remove('flex'); }
$('modal').addEventListener('click', e => { if(e.target.id==='modal') closeModal(); });

function group(el, items, cls, isOn, pick, html){
  el.innerHTML='';
  items.forEach(it=>{
    const b=document.createElement('button'); b.type='button'; b.className=cls;
    b.innerHTML=html(it); b.setAttribute('aria-pressed', isOn(it));
    b.onclick=()=>pick(it); el.appendChild(b);
  });
}

/* ---------- status ---------- */
function refreshStatus(){
  const sheet=LS.get('sheetId',''), hook=LS.get('hook','');
  const set=(el,on,t)=>{ el.className=el.className.replace(/\b(on|off)\b/,on?'on':'off'); el.textContent=t; };
  set($('stSheet'),!!sheet,'Status Google Sheet URL: '+(sheet?'เชื่อมต่อแล้ว':'ยังไม่ได้เชื่อมต่อ'));
  set($('stHook'),!!hook,'Status Webhook URL: '+(hook?'เชื่อมต่อแล้ว':'ยังไม่ได้เชื่อมต่อ'));
  set($('fSheet'),!!sheet,sheet?'เชื่อมต่อแล้ว':'ยังไม่เชื่อมต่อ');
  set($('fHook'),!!hook,hook?'เชื่อมต่อแล้ว':'ยังไม่ระบุ');
  $('cnt').textContent=LS.get('records',[]).length;
}

/* ---------- navigation ---------- */
function show(v){ $('home').classList.toggle('hidden',v!=='home'); $('formView').classList.toggle('hidden',v!=='form'); window.scrollTo(0,0); }
$('goForm').onclick=()=>show('form');
$('goHome').onclick=()=>{ show('home'); refreshStatus(); };
$('shareBtn').onclick=async()=>{
  const url=shareUrl();
  try{ if(navigator.share){ await navigator.share({title:'SFPP Receive 2026',url}); return; } await navigator.clipboard.writeText(url); toast(true,'คัดลอกลิงก์แล้ว'); }
  catch(e){ prompt('คัดลอกลิงก์ฟอร์ม:',url); }
};

/* ---------- form UI ---------- */
function personField(box, id, placeholder, list){
  box.innerHTML=`<div class="flex justify-between items-end mb-1"><label class="lbl !mb-0" for="${id}S">ระบุชื่อพนักงาน <span class="text-rose-500">*</span></label><span class="lnk" id="${id}T">พิมพ์ชื่อเอง</span></div>
    <select id="${id}S" class="fld"></select><input id="${id}I" class="fld hidden" placeholder="พิมพ์ชื่อ..." autocomplete="off">`;
  $(id+'S').innerHTML=`<option value="">${placeholder}</option>`+list.map(n=>`<option>${esc(n)}</option>`).join('');
  $(id+'T').onclick=()=>{ const m=$(id+'I').classList.toggle('hidden'); $(id+'S').classList.toggle('hidden',!m); $(id+'T').textContent=m?'พิมพ์ชื่อเอง':'เลือกจากรายการ'; };
}
const person = id => $(id+'I').classList.contains('hidden') ? $(id+'S').value : $(id+'I').value.trim();

function renderType(){ group($('typeG'),TYPES,'opt',t=>t.v===s.type.v,t=>{s.type=t;renderType();$('whoTitle').textContent=t.who+' *';},t=>`<i></i>${t.v}`); $('whoTitle').textContent=s.type.who+' *'; }
function renderShift(){ group($('shiftG'),['A','B','C','D'],'sh',x=>x===s.shift,x=>{s.shift=x;renderShift();},x=>x); }
function renderDept(){
  group($('deptG'),Object.keys(CFG),'opt d',d=>d===s.dept,d=>{s.dept=d;renderDept();renderLines();personField($('personBox'),'rc','-- กรุณาเลือกชื่อพนักงาน --',CFG[d].people);},
    d=>{ const l=CFG[d].lines; return `<span class="flex-1"><span class="block text-lg">${d}</span><span class="block text-sm font-medium text-slate-500">ฝ่าย ${d} (Line ${l[0]}-${l.at(-1)})</span></span><i class="!order-2"></i>`; });
}
function renderLines(){
  const ls=CFG[s.dept].lines;
  $('poTitle').textContent=`PROCESS ORDER NUMBER & สแกน BARCODE (${s.dept.toUpperCase()})`;
  $('poG').innerHTML=ls.map(n=>{ const c=LINE_CLR[n-1]; return `<div class="rounded-2xl border p-4 ${BOX[c]}">
    <label for="po${n}" class="font-bold block mb-2">Process order Number (Line ${n})</label>
    <div class="flex gap-2"><input id="po${n}" class="fld font-mono" inputmode="numeric" autocomplete="off" placeholder="Process order Number">
    <button type="button" data-scan="${n}" class="flex-none px-4 rounded-2xl text-white font-bold ${BTN[c]}">📷 สแกน</button></div></div>`; }).join('');
  document.querySelectorAll('[data-scan]').forEach(b=>b.onclick=()=>startScan(b.dataset.scan));
}
$('date').onchange=()=>{ const v=$('date').value; $('dBadge').textContent=fmtDate(v); const p=v.split('-');
  $('dLong').textContent=p.length===3?new Date(+p[0],+p[1]-1,+p[2]).toLocaleDateString('en-GB',{weekday:'long',day:'numeric',month:'long',year:'numeric'}):''; };
$('todayBtn').onclick=()=>{ $('date').value=todayLocal(); $('date').onchange(); };
$('nowBtn').onclick=()=>$('time').value=nowLocal();

/* ---------- barcode scan ---------- */
let scanner=null;
function startScan(n){
  openModal(`<div class="flex justify-between items-center mb-3"><b>สแกน Line ${n}</b><button onclick="closeModal()" class="text-2xl px-2">✕</button></div>
    <div id="reader" class="rounded-2xl overflow-hidden bg-black min-h-[200px]"></div><p id="scanMsg" class="text-sm text-slate-500 mt-3">เล็งกล้องไปที่ Barcode / QR Code</p>`);
  if(!window.Html5Qrcode){ $('scanMsg').textContent='โหลดตัวสแกนไม่สำเร็จ กรุณากรอกตัวเลขเอง'; return; }
  scanner=new Html5Qrcode('reader');
  scanner.start({facingMode:'environment'},{fps:10,qrbox:{width:260,height:160}},txt=>{
    const m=txt.match(/\d{6,}/); const val=m?m[0]:txt.replace(/\D/g,'');
    closeModal();
    if(!val) return toast(false,'อ่านได้แต่ไม่พบตัวเลข Order');
    $('po'+n).value=val; toast(true,`Line ${n}: ${val}`);
  },()=>{}).catch(()=>{ $('scanMsg').textContent='เปิดกล้องไม่ได้ (ต้องใช้ https และอนุญาตกล้อง) กรุณากรอกตัวเลขเอง'; });
}
function stopScan(){ if(scanner){ const sc=scanner; scanner=null; sc.stop().then(()=>sc.clear()).catch(()=>{}); } }

/* ---------- submit ---------- */
$('f').onsubmit=async e=>{
  e.preventDefault();
  const date=$('date').value, time=$('time').value;
  if(!date||!time) return toast(false,'กรุณาระบุวันที่และเวลา');
  const who=person('rc'); if(!who) return toast(false,'กรุณาระบุชื่อ '+s.type.who);
  const orders={};
  for(let n=1;n<=6;n++){ const el=$('po'+n), v=el?el.value.trim():'';
    if(v&&!/^\d+$/.test(v)) return toast(false,`Line ${n}: ต้องเป็นตัวเลขเท่านั้น`);
    orders['processOrderLine'+n]=v; }
  if(!Object.values(orders).some(Boolean)) return toast(false,'กรอก Process order อย่างน้อย 1 Line');
  const qa=person('qa'); if(!qa) return toast(false,'กรุณาระบุ QA ผู้ส่ง SFPP');

  const rec={id:'REC-'+Date.now(),timestamp:new Date().toISOString(),date:fmtDate(date),time,actionType:s.type.v,shift:s.shift,
    department:s.dept,receiverName:who,qaSenderName:qa,notes:$('notes').value.trim(),...orders};
  const btn=$('submit'); btn.disabled=true; btn.textContent='กำลังบันทึก...';
  const hook=LS.get('hook',''); let sent=false;
  if(hook){ try{ await fetch(hook,{method:'POST',mode:'no-cors',headers:{'Content-Type':'text/plain;charset=utf-8'},
      body:JSON.stringify({...rec,spreadsheetId:LS.get('sheetId','')})}); sent=true; }catch(err){} }
  const all=LS.get('records',[]); all.push({...rec,sent}); LS.set('records',all);
  btn.disabled=false; btn.textContent='➤ บันทึกข้อมูลลงระบบ (Submit SFPP)';
  refreshStatus();
  toast(true, hook ? (sent?'ส่งเข้า Google Sheet แล้ว':'ส่งเข้า Sheet ไม่สำเร็จ (เก็บในเครื่องแล้ว)') : 'บันทึกในเครื่องแล้ว (ยังไม่ได้ตั้งค่า Webhook)');
  if(hook&&!sent) return;
  clearInputs();
};
function clearInputs(){ renderLines(); $('notes').value=''; $('time').value=nowLocal(); }
$('clearBtn').onclick=()=>{ clearInputs(); personField($('personBox'),'rc','-- กรุณาเลือกชื่อพนักงาน --',CFG[s.dept].people); personField($('qaBox'),'qa','-- กรุณาเลือกชื่อพนักงาน QA --',QA); };

/* ---------- admin ---------- */
let pin='', showPin=false;
document.querySelectorAll('.adminBtn').forEach(b=>b.onclick=pinModal);
function pinModal(){
  pin=''; showPin=false;
  const isDefault=LS.get('pin','1234')==='1234';
  openModal(`<div class="text-right"><button onclick="closeModal()" class="text-2xl">✕</button></div>
    <div class="text-center"><div class="mx-auto w-16 h-16 rounded-2xl bg-gradient-to-br from-red-600 to-orange-500 grid place-items-center text-3xl">🔑</div>
    <h2 class="font-bold text-xl mt-3">เข้าสู่ระบบผู้ดูแลระบบ (Admin)</h2><p class="text-sm text-slate-500">กรุณาใส่รหัส PIN 4 หลัก</p></div>
    <div id="pinBoxes" class="flex justify-center gap-3 my-5"></div>
    <div class="flex justify-between text-sm text-slate-500 mb-3"><button id="eye">👁 แสดงตัวเลข</button><span id="pinErr"></span></div>
    <div class="grid grid-cols-3 gap-3">${[1,2,3,4,5,6,7,8,9].map(n=>`<button class="key" data-k="${n}">${n}</button>`).join('')}
    <button class="key !text-base text-slate-500" data-k="C">ล้าง</button><button class="key" data-k="0">0</button><button class="key" data-k="B">⌫</button></div>
    ${isDefault?'<button id="fill" class="mt-4 w-full py-3 rounded-2xl bg-blue-50 border border-blue-200 text-blue-700 font-bold">🔑 รหัสเริ่มต้นคือ 1234 (คลิกเพื่อใส่ทันที)</button>':''}`);
  drawPin();
  document.querySelectorAll('[data-k]').forEach(b=>b.onclick=()=>pinKey(b.dataset.k));
  $('eye').onclick=()=>{ showPin=!showPin; drawPin(); };
  if($('fill')) $('fill').onclick=()=>{ pin='1234'; drawPin(); checkPin(); };
}
function drawPin(){ $('pinBoxes').innerHTML=[0,1,2,3].map(i=>`<div class="w-14 h-16 rounded-2xl border-2 ${i===pin.length?'border-blue-500':'border-slate-200'} bg-slate-50 grid place-items-center text-2xl font-bold">${pin[i]?(showPin?pin[i]:'●'):'<span class="text-slate-300">•</span>'}</div>`).join(''); }
function pinKey(k){ $('pinErr').textContent=''; if(k==='C')pin=''; else if(k==='B')pin=pin.slice(0,-1); else if(pin.length<4)pin+=k; drawPin(); if(pin.length===4)checkPin(); }
function checkPin(){ if(pin===LS.get('pin','1234')) adminPanel(); else { pin=''; drawPin(); $('pinErr').textContent='รหัสไม่ถูกต้อง'; $('pinErr').className='text-rose-600 font-bold'; } }

function sheetUrlOf(id){ return id?`https://docs.google.com/spreadsheets/d/${id}`:''; }
function adminPanel(){
  const recs=LS.get('records',[]).slice().reverse().slice(0,30);
  openModal(`<div class="flex justify-between items-center mb-3"><h2 class="font-bold text-lg">⚙️ ตั้งค่าและจัดการข้อมูล</h2><button onclick="closeModal()" class="text-2xl">✕</button></div>
    <label class="lbl">URL ของ Google Sheet</label>
    <input id="aSheet" class="fld font-mono text-xs" placeholder="https://docs.google.com/spreadsheets/d/..." value="${esc(sheetUrlOf(LS.get('sheetId','')))}">
    <button id="saveSheet" class="w-full mt-2 py-3 rounded-2xl bg-[#1a3a73] text-white font-bold">🔗 เชื่อมต่อ Google Sheet</button>
    <label class="lbl mt-5">Google Apps Script Web App URL (Webhook)</label>
    <input id="aHook" class="fld font-mono text-xs" placeholder="https://script.google.com/macros/s/.../exec" value="${esc(LS.get('hook',''))}">
    <button id="saveHook" class="mt-2 px-5 py-3 rounded-2xl bg-blue-700 text-white font-bold">💾 บันทึก Webhook URL</button>
    <hr class="my-5">
    <div class="flex gap-2 flex-wrap">
      <button id="newPin" class="px-4 py-2 rounded-xl border border-slate-300 text-sm font-bold">⚙ ตั้งค่า PIN ใหม่</button>
      <button id="resetPin" class="px-4 py-2 rounded-xl border border-slate-300 text-sm font-bold">↻ รีเซ็ตเป็น 1234</button>
      <button id="csv" class="px-4 py-2 rounded-xl border border-slate-300 text-sm font-bold">⬇ ส่งออก CSV</button>
      <button id="staffLink" class="px-4 py-2 rounded-xl bg-emerald-600 text-white text-sm font-bold">🔗 คัดลอกลิงก์สำหรับพนักงาน</button>
    </div>
    <h3 class="font-bold mt-5 mb-2">รายการที่บันทึกในเครื่อง (${LS.get('records',[]).length})</h3>
    <div class="space-y-2">${recs.length?recs.map(r=>`<div class="border rounded-xl p-3 text-xs flex gap-2 items-start">
      <div class="flex-1"><b>${esc(r.date)} ${esc(r.time)}</b> · ${esc(r.actionType.split(' ')[0])} · ${esc(r.department)} · กะ ${esc(r.shift)}<br>${esc(r.receiverName)} ← QA ${esc(r.qaSenderName)}<br>
      <span class="text-slate-500">PO: ${[1,2,3,4,5,6].map(n=>r['processOrderLine'+n]?`L${n}=${esc(r['processOrderLine'+n])}`:'').filter(Boolean).join(', ')}</span> ${r.sent?'<span class="text-emerald-600">✓ ส่งแล้ว</span>':'<span class="text-amber-600">เก็บในเครื่อง</span>'}</div>
      <button data-del="${esc(r.id)}" class="text-rose-600 font-bold">ลบ</button></div>`).join(''):'<p class="text-sm text-slate-400">ยังไม่มีรายการ</p>'}</div>`);
  $('saveSheet').onclick=()=>{ const v=$('aSheet').value.trim(); if(!v){ LS.set('sheetId',''); refreshStatus(); return toast(true,'ยกเลิกการเชื่อมต่อ Sheet แล้ว'); }
    const m=v.match(/\/d\/([a-zA-Z0-9_-]+)/); if(!m) return toast(false,'ไม่พบ Spreadsheet ID ใน URL'); LS.set('sheetId',m[1]); refreshStatus(); toast(true,'เชื่อมต่อ Google Sheet แล้ว'); };
  $('saveHook').onclick=()=>{ const v=$('aHook').value.trim(); if(v&&!/^https:\/\/script\.google\.com\/.+\/exec/.test(v)) return toast(false,'URL ต้องเป็น https://script.google.com/.../exec'); LS.set('hook',v); refreshStatus(); toast(true,v?'บันทึก Webhook แล้ว':'ลบ Webhook แล้ว'); };
  $('newPin').onclick=()=>{ const p=prompt('ตั้งรหัส PIN ใหม่ (ตัวเลข 4 หลัก):'); if(p===null)return; if(!/^\d{4}$/.test(p)) return toast(false,'PIN ต้องเป็นตัวเลข 4 หลัก'); LS.set('pin',p); toast(true,'เปลี่ยน PIN แล้ว'); };
  $('resetPin').onclick=()=>{ LS.set('pin','1234'); toast(true,'รีเซ็ต PIN เป็น 1234 แล้ว'); };
  $('csv').onclick=exportCsv;
  $('staffLink').onclick=async()=>{ if(!LS.get('hook','')) return toast(false,'ตั้งค่า Webhook URL ก่อน');
    const u=shareUrl(); try{ await navigator.clipboard.writeText(u); toast(true,'คัดลอกลิงก์สำหรับพนักงานแล้ว'); }catch(e){ prompt('คัดลอกลิงก์:',u); } };
  document.querySelectorAll('[data-del]').forEach(b=>b.onclick=()=>{ if(!confirm('ลบรายการนี้ออกจากเครื่อง? (ไม่ลบใน Google Sheet)')) return;
    LS.set('records',LS.get('records',[]).filter(r=>r.id!==b.dataset.del)); refreshStatus(); adminPanel(); });
}
function exportCsv(){
  const rows=LS.get('records',[]); if(!rows.length) return toast(false,'ไม่มีข้อมูล');
  const keys=['id','timestamp','date','time','actionType','shift','department','receiverName','processOrderLine1','processOrderLine2','processOrderLine3','processOrderLine4','processOrderLine5','processOrderLine6','qaSenderName','notes'];
  const q=v=>'"'+String(v==null?'':v).replace(/"/g,'""')+'"';
  const csv='\ufeff'+[keys.join(',')].concat(rows.map(r=>keys.map(k=>q(r[k])).join(','))).join('\r\n');
  const a=document.createElement('a'); a.href=URL.createObjectURL(new Blob([csv],{type:'text/csv;charset=utf-8'})); a.download='SFPP_Log_2026.csv'; a.click();
}

/* ---------- config via share link ---------- */
function shareUrl(){
  const base=location.href.split('#')[0], hook=LS.get('hook',''), sheet=LS.get('sheetId','');
  if(!hook) return base;
  const b64=btoa(unescape(encodeURIComponent(JSON.stringify({h:hook,s:sheet}))));
  return base+'#cfg='+encodeURIComponent(b64);
}
function loadCfg(){
  const m=location.hash.match(/#cfg=([^&]+)/); if(!m) return;
  try{
    const c=JSON.parse(decodeURIComponent(escape(atob(decodeURIComponent(m[1])))));
    const ok=/^https:\/\/script\.google\.com\/.+\/exec$/.test(c.h||'');
    const sid=/^[\w-]+$/.test(c.s||'')?c.s:'';
    if(ok && (c.h!==LS.get('hook','') || sid!==LS.get('sheetId',''))){
      if(confirm('ตั้งค่าการเชื่อมต่อ Google Sheet จากลิงก์นี้ใช่หรือไม่?\n(กดตกลงเฉพาะลิงก์ที่ได้รับจากแอดมินของคุณ)')){ LS.set('hook',c.h); LS.set('sheetId',sid); }
    }
  }catch(e){}
  history.replaceState(null,'',location.pathname+location.search);
}

/* ---------- init ---------- */
$('date').value=todayLocal(); $('date').onchange(); $('time').value=nowLocal();
renderType(); renderShift(); renderDept(); renderLines();
personField($('personBox'),'rc','-- กรุณาเลือกชื่อพนักงาน --',CFG.Blending.people);
personField($('qaBox'),'qa','-- กรุณาเลือกชื่อพนักงาน QA --',QA);
loadCfg();
refreshStatus();
</script>
</body>
</html>
