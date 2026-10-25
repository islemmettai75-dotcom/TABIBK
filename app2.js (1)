const SUPABASE_URL="https://oiclgywmduooeefsvuyn.supabase.co";
const SUPABASE_ANON_KEY="sb_publishable_lYdmmS6jV8Kl6kUgxoks7A_GDIqHWQf";

const T={ar:{h1:"طبيبك",sub:"أطباء ولاية قسنطينة: احجز موعدك دون انتظار طويل.",docs:"الأطباء",mine:"مواعيدي",panel:"لوحة الطبيب",login:"دخول",logout:"خروج",signup:"إنشاء حساب",email:"البريد الإلكتروني",pass:"كلمة المرور (6 أحرف على الأقل)",fn:"الاسم الكامل",ph:"رقم الهاتف",q:"ابحث باسم الطبيب أو البلدية",all:"الكل",book:"احجز",close:"إغلاق",fee:"الكشف",cur:"دج",need:"سجّل الدخول لتحجز موعدًا.",reason:"سبب الزيارة (اختياري)",who:"اسم المريض",confirm:"تأكيد الحجز",noDocs:"لا يوجد أطباء مطابقون.",noSlots:"لا توجد أوقات متاحة في هذا اليوم.",noA:"لا توجد مواعيد بعد.",noR:"لا توجد طلبات حتى الآن.",pending:"بانتظار موافقة الطبيب",confirmed:"تم تأكيد الموعد",declined:"اعتذر الطبيب",cancelled:"أُلغي الموعد",completed:"تمت الزيارة",no_show:"لم يحضر المريض",cancel:"إلغاء",ok:"قبول",no:"اعتذار",done:"تمت الزيارة",hours:"ساعات العمل",add:"إضافة",from:"من",to:"إلى",min:"مدة الموعد (دقيقة)",del:"حذف",reqs:"طلبات الحجز",bad:"تحقق من الاسم والرقم (مثل 0555123456).",sent:"أُرسل طلب الحجز للطبيب.",taken:"حُجز هذا الوقت للتو. اختر وقتًا آخر.",saved:"تم الحفظ.",cfg:"التطبيق غير مربوط بعد. ضع رابط مشروع Supabase والمفتاح في أعلى ملف index.html.",welcome:"تم إنشاء الحساب. إن طُلب منك تأكيد البريد فافتح الرسالة أولًا.",sw:"بدّل اللغة",map:"الخريطة",days:["الأحد","الاثنين","الثلاثاء","الأربعاء","الخميس","الجمعة","السبت"],btn:"Français",loc:"ar-DZ-u-nu-latn",slow:"الاتصال بطيء أو متعطل، حاول مرة أخرى.",agree:"أوافق على جمع بياناتي واستعمالها لإدارة مواعيدي وفق",policy:"سياسة الخصوصية",needAgree:"يجب الموافقة على سياسة الخصوصية للمتابعة."},
fr:{h1:"Tabibek",sub:"Médecins de la wilaya de Constantine : réservez sans attendre.",docs:"Médecins",mine:"Mes rendez-vous",panel:"Espace médecin",login:"Connexion",logout:"Déconnexion",signup:"Créer un compte",email:"E-mail",pass:"Mot de passe (6 caractères min.)",fn:"Nom et prénom",ph:"Téléphone",q:"Médecin ou commune",all:"Tous",book:"Réserver",close:"Fermer",fee:"Consultation",cur:"DA",need:"Connectez-vous pour réserver.",reason:"Motif (facultatif)",who:"Nom du patient",confirm:"Confirmer",noDocs:"Aucun médecin trouvé.",noSlots:"Aucun créneau libre ce jour-là.",noA:"Aucun rendez-vous.",noR:"Aucune demande pour le moment.",pending:"En attente du médecin",confirmed:"Rendez-vous confirmé",declined:"Décliné par le médecin",cancelled:"Rendez-vous annulé",completed:"Consultation effectuée",no_show:"Patient absent",cancel:"Annuler",ok:"Accepter",no:"Décliner",done:"Effectué",hours:"Horaires de travail",add:"Ajouter",from:"De",to:"À",min:"Durée (minutes)",del:"Supprimer",reqs:"Demandes de rendez-vous",bad:"Vérifiez le nom et le numéro (ex. 0555123456).",sent:"Demande envoyée au médecin.",taken:"Ce créneau vient d’être pris. Choisissez-en un autre.",saved:"Enregistré.",cfg:"L’application n’est pas encore connectée. Renseignez l’URL et la clé Supabase en haut du fichier index.html.",welcome:"Compte créé. Si une confirmation est demandée, ouvrez d’abord l’e-mail reçu.",sw:"Changer de langue",map:"Itinéraire",days:["Dimanche","Lundi","Mardi","Mercredi","Jeudi","Vendredi","Samedi"],btn:"عربي",loc:"fr-DZ",slow:"Connexion lente ou bloquée, réessayez.",agree:"J’accepte la collecte et l’utilisation de mes données pour gérer mes rendez-vous, conformément à la",policy:"politique de confidentialité",needAgree:"Vous devez accepter la politique de confidentialité."}};

const $=id=>document.getElementById(id);
const dbg=m=>{const e=document.getElementById("dbg");if(e)e.textContent=m};
window.addEventListener("error",e=>dbg("JS error: "+e.message));
window.addEventListener("unhandledrejection",e=>dbg("Promise error: "+(e.reason&&e.reason.message||e.reason)));
const esc=s=>String(s??"").replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]));
let lang="ar";try{lang=localStorage.getItem("lang")||"ar"}catch(e){}
const t=k=>T[lang][k],L=()=>lang=="fr"?1:0;
const configured=!SUPABASE_URL.startsWith("PUT_");
const sb=configured?supabase.createClient(SUPABASE_URL,SUPABASE_ANON_KEY,{auth:{lock:async(n,w,fn)=>await fn()}}):null;
const TZ="Africa/Algiers";
let user=null,profile=null,docs=[],view="docs",spec="",q="",mode="login";
let openDoc=null,bk=null,mineList=[],reqList=[],hoursList=[];

function toast(m){const e=$("toast");e.textContent=m;e.classList.add("on");setTimeout(()=>e.classList.remove("on"),5000)}
function fmt(iso){return new Date(iso).toLocaleString(t("loc"),{timeZone:TZ,weekday:"short",day:"numeric",month:"short",hour:"2-digit",minute:"2-digit"})}
function hm(iso){return new Date(iso).toLocaleTimeString("fr-DZ",{timeZone:TZ,hour:"2-digit",minute:"2-digit"})}
async function run(p){const{data,error}=await Promise.race([p,new Promise(r=>setTimeout(()=>r({error:{message:t("slow")}}),12000))]);if(error){toast(error.code=="23505"||/duplicate/i.test(error.message)?t("taken"):error.message);throw error}return data}
function ymd(i){return new Date(Date.now()+i*864e5).toLocaleDateString("en-CA",{timeZone:TZ})}
function wday(s){return new Date(s+"T12:00:00+01:00").getUTCDay()}
function dayLabel(s){return new Date(s+"T12:00:00+01:00").toLocaleDateString(t("loc"),{timeZone:TZ,weekday:"short",day:"numeric",month:"short"})}

function chrome(){
  document.documentElement.lang=lang;document.documentElement.dir=lang=="fr"?"ltr":"rtl";
  $("h1").textContent=t("h1");$("sub").textContent=t("sub");$("lang").textContent=t("btn");
  $("auth").textContent=user?t("logout"):t("login");
  $("cfg").hidden=configured;$("cfg").textContent=t("cfg");
  const tabs=[["docs",t("docs")],["mine",t("mine")]];
  if(profile&&(profile.role=="doctor"||profile.role=="admin"))tabs.push(["panel",t("panel")]);
  if(!user)tabs.splice(1,1);
  $("nav").innerHTML=tabs.map(([k,l])=>`<button data-view="${k}" aria-pressed="${view==k}">${l}</button>`).join("");
}
function render(){
  chrome();
  if(view=="auth")return renderAuth();
  if(view=="docs")return renderDocs();
  if(view=="mine")return renderMine();
  if(view=="panel")return renderPanel();
}
function renderAuth(){
  $("v").innerHTML=`<div class="box"><h3>${mode=="login"?t("login"):t("signup")}</h3>
  ${mode=="signup"?`<label for="fn">${t("fn")}</label><input id="fn" autocomplete="name"><label for="phn">${t("ph")}</label><input id="phn" type="tel" dir="ltr" placeholder="0555 12 34 56" autocomplete="tel">`:""}
  <label for="em">${t("email")}</label><input id="em" type="email" dir="ltr" autocomplete="email">
  <label for="pw">${t("pass")}</label><input id="pw" type="password" dir="ltr" autocomplete="${mode=="login"?"current-password":"new-password"}">
  ${mode=="signup"?`<label style="display:flex;gap:8px;align-items:flex-start;margin-top:12px"><input id="agree" type="checkbox" style="width:auto;margin-top:6px"><span>${t("agree")} <a href="privacy.html" target="_blank" rel="noopener">${t("policy")}</a></span></label>`:""}
  <div class="acts"><button class="btn" data-act="submit">${mode=="login"?t("login"):t("signup")}</button>
  <button class="pill" data-act="mode">${mode=="login"?t("signup"):t("login")}</button></div></div>`;
}
function specs(){const m=new Map();docs.forEach(d=>m.set(d.specialty_ar,L()?d.specialty_fr:d.specialty_ar));return[...m]}
function renderDocs(){
  $("v").innerHTML=`<input id="q" type="search" placeholder="${t("q")}" value="${esc(q)}"><div class="chips" id="chips"></div><div id="list"></div>`;
  $("q").oninput=e=>{q=e.target.value;renderList()};
  $("chips").innerHTML=[["",t("all")],...specs()].map(([k,l])=>`<button class="chip" data-spec="${esc(k)}" aria-pressed="${spec==k}">${esc(l)}</button>`).join("");
  renderList();
}
function renderList(){
  const s=q.trim().toLowerCase();
  const f=docs.filter(d=>(!spec||d.specialty_ar==spec)&&(!s||[d.full_name,d.commune_ar,d.commune_fr,d.specialty_ar,d.specialty_fr].join(" ").toLowerCase().includes(s)));
  if(!f.length){$("list").innerHTML=`<p class="empty">${t("noDocs")}</p>`;return}
  $("list").innerHTML=f.map(d=>{
    const addr=L()?d.address_fr:d.address_ar,com=L()?d.commune_fr:d.commune_ar;
    const map=`https://www.google.com/maps/search/?api=1&query=${encodeURIComponent((d.address_fr||"")+" "+d.commune_fr+" Constantine")}`;
    return `<div class="doc"><div class="row"><div class="av">${esc((d.full_name||"?").trim().slice(0,1))}</div>
    <div class="grow"><div class="name">${esc(d.full_name)}</div>
    <div class="meta">${esc(L()?d.specialty_fr:d.specialty_ar)} · ${esc(com)} · ${t("fee")} ${d.fee_da} ${t("cur")}</div>
    <div class="meta"><a href="${map}" target="_blank" rel="noopener">${esc(addr||com)} · ${t("map")}</a></div></div>
    <button class="btn" data-act="open" data-id="${d.id}">${openDoc==d.id?t("close"):t("book")}</button></div>
    ${openDoc==d.id?bookingBox(d):""}</div>`}).join("");
}
function bookingBox(d){
  if(!user)return `<div class="box"><div class="meta">${t("need")}</div><div class="acts"><button class="btn" data-act="gologin">${t("login")}</button></div></div>`;
  if(!bk||bk.doc!=d.id)return `<div class="box meta">…</div>`;
  const days=[0,1,2,3,4,5,6].map(ymd),sl=slotsFor(days[bk.day]);
  return `<div class="box"><div class="chips">${days.map((s,i)=>`<button class="chip" data-act="day" data-i="${i}" aria-pressed="${bk.day==i}">${dayLabel(s)}</button>`).join("")}</div>
  ${sl.length?`<div class="slots" dir="ltr">${sl.map(s=>`<button class="slot" data-act="time" data-iso="${s}" aria-pressed="${bk.time==s}">${hm(s)}</button>`).join("")}</div>`:`<p class="meta">${t("noSlots")}</p>`}
  <label for="pn">${t("who")}</label><input id="pn" value="${esc(profile?.full_name||"")}">
  <label for="pp">${t("ph")}</label><input id="pp" type="tel" dir="ltr" value="${esc(profile?.phone||"")}" placeholder="0555 12 34 56">
  <label for="pr">${t("reason")}</label><input id="pr">
  <div class="acts"><button class="btn" data-act="confirm" data-id="${d.id}">${t("confirm")}</button></div></div>`;
}
function slotsFor(day){
  const out=[],now=Date.now()+30*6e4,wd=wday(day);
  bk.hours.filter(h=>h.weekday==wd).forEach(h=>{
    const [sh,sm]=h.start_time.split(":").map(Number),[eh,em]=h.end_time.split(":").map(Number);
    for(let m=sh*60+sm;m+h.slot_minutes<=eh*60+em;m+=h.slot_minutes){
      const iso=`${day}T${String(Math.floor(m/60)).padStart(2,"0")}:${String(m%60).padStart(2,"0")}:00+01:00`,ms=new Date(iso).getTime();
      if(ms>now&&!bk.taken.has(ms))out.push(iso)}});
  return out.sort();
}
function apptRow(a,doctorSide){
  const d=docs.find(x=>x.id==a.doctor_id);
  const who=doctorSide?`${esc(a.patient_name)} · <span dir="ltr">${esc(a.patient_phone)}</span>`:esc(d?d.full_name:"");
  let acts="";
  if(doctorSide&&a.status=="pending")acts=`<button class="btn" data-act="set" data-s="confirmed" data-id="${a.id}">${t("ok")}</button><button class="btn ghost" data-act="set" data-s="declined" data-id="${a.id}">${t("no")}</button>`;
  else if(doctorSide&&a.status=="confirmed")acts=`<button class="btn" data-act="set" data-s="completed" data-id="${a.id}">${t("done")}</button><button class="btn ghost" data-act="set" data-s="no_show" data-id="${a.id}">${t("no_show")}</button>`;
  else if(!doctorSide&&(a.status=="pending"||a.status=="confirmed"))acts=`<button class="btn ghost" data-act="cancelA" data-id="${a.id}">${t("cancel")}</button>`;
  return `<div class="doc"><div class="name">${who}</div><div class="meta">${fmt(a.starts_at)}${a.reason?" · "+esc(a.reason):""}</div><div class="st ${a.status}">${t(a.status)}</div>${acts?`<div class="acts">${acts}</div>`:""}</div>`;
}
function renderMine(){$("v").innerHTML=mineList.length?mineList.map(a=>apptRow(a,false)).join(""):`<p class="empty">${t("noA")}</p>`}
function renderPanel(){
  $("v").innerHTML=`<h2>${t("reqs")}</h2>${reqList.length?reqList.map(a=>apptRow(a,true)).join(""):`<p class="empty">${t("noR")}</p>`}
  <h2>${t("hours")}</h2>${hoursList.map(h=>`<div class="row doc"><div class="grow">${t("days")[h.weekday]} · <span dir="ltr">${h.start_time.slice(0,5)}–${h.end_time.slice(0,5)}</span> · ${h.slot_minutes} min</div><button class="btn ghost" data-act="delH" data-id="${h.id}">${t("del")}</button></div>`).join("")}
  <div class="box"><select id="hd">${t("days").map((d,i)=>`<option value="${i}">${d}</option>`).join("")}</select>
  <div class="grid"><div><label for="hs">${t("from")}</label><input id="hs" type="time" value="09:00"></div><div><label for="he">${t("to")}</label><input id="he" type="time" value="16:00"></div></div>
  <label for="hm">${t("min")}</label><input id="hm" type="number" min="10" max="120" value="30">
  <div class="acts"><button class="btn" data-act="addH">${t("add")}</button></div></div>`;
}

async function loadDocs(){docs=await run(sb.from("doctors_public").select("*").order("full_name"))}
async function loadProfile(){
  if(!user){profile=null;return}
  const{data}=await sb.from("profiles").select("*").eq("id",user.id).maybeSingle();profile=data;
}
async function loadMine(){if(user)mineList=await run(sb.from("appointments").select("*").eq("patient_id",user.id).order("starts_at",{ascending:false}))}
async function loadPanel(){
  if(!profile||profile.role=="patient")return;
  reqList=await run(sb.from("appointments").select("*").eq("doctor_id",user.id).order("starts_at",{ascending:false}));
  hoursList=await run(sb.from("doctor_hours").select("*").eq("doctor_id",user.id).order("weekday").order("start_time"));
}
async function loadBooking(id){
  bk={doc:id,day:0,time:null,hours:[],taken:new Set()};render();
  const from=new Date(Date.now()-864e5).toISOString(),to=new Date(Date.now()+9*864e5).toISOString();
  bk.hours=await run(sb.from("doctor_hours").select("*").eq("doctor_id",id).eq("active",true));
  const tk=await run(sb.rpc("taken_slots",{p_doctor:id,p_from:from,p_to:to}));
  bk.taken=new Set(tk.map(x=>new Date(x.starts_at).getTime()));render();
}
const phoneOk=p=>/^0[567]\d{8}$/.test(p);

document.addEventListener("click",async e=>{
  const b=e.target.closest("button");if(!b)return;const D=b.dataset;
  dbg("v3 click: "+(b.id||D.act||D.view||D.spec||"?"));
  try{
    if(D.view){view=D.view;if(view=="mine")await loadMine();if(view=="panel")await loadPanel();render()}
    else if(D.spec!==undefined){spec=D.spec;renderDocs()}
    else if(b.id=="lang"){lang=lang=="fr"?"ar":"fr";try{localStorage.setItem("lang",lang)}catch(_){}render()}
    else if(b.id=="auth"){if(user){user=null;profile=null;mineList=[];view="docs";render();sb.auth.signOut({scope:"local"}).catch(()=>{})}else{view="auth";render()}}
    else if(b.id=="reset"){try{Object.keys(localStorage).filter(k=>k.startsWith("sb-")).forEach(k=>localStorage.removeItem(k))}catch(_){}location.reload()}
    else if(D.act=="gologin"){view="auth";render()}
    else if(D.act=="mode"){mode=mode=="login"?"signup":"login";render()}
    else if(D.act=="submit"){
      const email=$("em").value.trim(),password=$("pw").value;
      if(mode=="signup"){
        if(!$("agree").checked)return toast(t("needAgree"));
        const full_name=$("fn").value.trim(),phone=$("phn").value.replace(/[\s.-]/g,"");
        if(!full_name||!phoneOk(phone))return toast(t("bad"));
        await run(sb.auth.signUp({email,password,options:{data:{full_name,phone}}}));toast(t("welcome"));
      }else await run(sb.auth.signInWithPassword({email,password}));
    }
    else if(D.act=="open"){openDoc=openDoc==D.id?null:D.id;bk=null;renderList();if(openDoc&&user)await loadBooking(openDoc)}
    else if(D.act=="day"){bk.day=+D.i;bk.time=null;renderList()}
    else if(D.act=="time"){bk.time=D.iso;renderList()}
    else if(D.act=="confirm"){
      const name=$("pn").value.trim(),phone=$("pp").value.replace(/[\s.-]/g,"");
      if(!name||!phoneOk(phone))return toast(t("bad"));
      if(!bk.time)return toast(t("noSlots"));
      await run(sb.rpc("book_appointment",{p_doctor:D.id,p_starts_at:bk.time,p_patient_name:name,p_phone:phone,p_reason:$("pr").value.trim()||null}));
      toast(t("sent"));openDoc=null;bk=null;view="mine";await loadMine();render();
    }
    else if(D.act=="cancelA"){await run(sb.from("appointments").update({status:"cancelled"}).eq("id",D.id));await loadMine();render()}
    else if(D.act=="set"){await run(sb.from("appointments").update({status:D.s}).eq("id",D.id));await loadPanel();render()}
    else if(D.act=="addH"){
      const row={doctor_id:user.id,weekday:+$("hd").value,start_time:$("hs").value,end_time:$("he").value,slot_minutes:+$("hm").value};
      await run(sb.from("doctor_hours").insert(row));toast(t("saved"));await loadPanel();render();
    }
    else if(D.act=="delH"){await run(sb.from("doctor_hours").delete().eq("id",D.id));await loadPanel();render()}
  }catch(err){console.error(err)}
});

async function boot(){
  render();
  if(configured)fetch(SUPABASE_URL+"/rest/v1/specialties?select=id&limit=1",{headers:{apikey:SUPABASE_ANON_KEY}}).then(r=>dbg("v3 · server: "+r.status)).catch(e=>dbg("v3 · server unreachable: "+e.message));
  if(!configured)return;
  sb.auth.onAuthStateChange((_ev,session)=>{
    user=session?session.user:null;
    setTimeout(async()=>{
      try{await loadProfile()}catch(e){}
      if(user&&view=="auth")view="docs";
      if(!user&&(view=="mine"||view=="panel"))view="docs";
      openDoc=null;bk=null;render();
    },0);
  });
  const{data}=await sb.auth.getSession();user=data.session?data.session.user:null;render();dbg(($("dbg")?$("dbg").textContent:"")+" · session: "+(user?"yes":"no"));
  await loadProfile();
  try{await loadDocs()}catch(e){}
  render();
}
boot();
