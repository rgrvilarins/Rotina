# Rotina
Aplicativo de organização pessoal
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Rotina</title>
<style>
:root{--bg:#F2F4F8;--surface:#fff;--ink:#161B33;--mute:#6A7190;--line:#E3E7F0;--accent:#3A4BDB;--on-accent:#fff;--hi:#E5484D;--md:#D98B1C;--lo:#2E9C8B;color-scheme:light}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0E1120;--surface:#171B30;--ink:#EEF0FA;--mute:#9199B8;--line:#262B45;--accent:#7C8CFF;--on-accent:#0E1120;--hi:#FF7A7F;--md:#F0B253;--lo:#4FC3B0;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#0E1120;--surface:#171B30;--ink:#EEF0FA;--mute:#9199B8;--line:#262B45;--accent:#7C8CFF;--on-accent:#0E1120;--hi:#FF7A7F;--md:#F0B253;--lo:#4FC3B0;color-scheme:dark}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
body{margin:0;background:var(--bg);color:var(--ink);font-family:system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;font-weight:500;line-height:1.4}
main{max-width:560px;margin:0 auto;padding:calc(20px + env(safe-area-inset-top,0px)) 18px 120px}
button{font:inherit;color:inherit;background:none;border:0;cursor:pointer}
button:focus-visible,input:focus-visible{outline:2px solid var(--accent);outline-offset:2px}
.top{display:flex;justify-content:space-between;align-items:flex-start}
.date{color:var(--mute);font-size:14px;text-transform:capitalize}
h1{font-size:28px;font-weight:800;margin:2px 0 0;letter-spacing:-.02em}
.theme{width:40px;height:40px;border-radius:50%;background:var(--surface);border:1px solid var(--line);font-size:18px}
.prog{margin:22px 0 8px;background:var(--surface);border:1px solid var(--line);border-radius:20px;padding:18px}
.prog b{font-size:34px;font-weight:800;letter-spacing:-.03em}
.prog span{color:var(--mute);margin-left:6px}
.bar{height:6px;background:var(--line);border-radius:3px;margin-top:12px;overflow:hidden}
.bar i{display:block;height:100%;width:0;background:var(--accent);border-radius:3px;transition:width .35s}
.chips{display:flex;gap:8px;overflow-x:auto;padding:14px 0 6px;scrollbar-width:none}
.chips::-webkit-scrollbar{display:none}
.chip{flex:none;padding:8px 14px;border-radius:999px;border:1px solid var(--line);background:var(--surface);font-size:14px;color:var(--mute)}
.chip[aria-pressed="true"]{background:var(--ink);color:var(--bg);border-color:var(--ink)}
section{margin-top:22px}
h2{display:flex;align-items:center;gap:8px;font-size:15px;font-weight:800;margin:0 0 10px}
h2 .dot{width:10px;height:10px;border-radius:50%}
h2 small{color:var(--mute);font-weight:500}
.list{background:var(--surface);border:1px solid var(--line);border-radius:18px;overflow:hidden}
.task{display:flex;align-items:center;gap:12px;padding:14px 14px 14px 12px;border-left:4px solid var(--c);border-bottom:1px solid var(--line)}
.task:last-child{border-bottom:0}
.check{flex:none;width:28px;height:28px;border-radius:50%;border:2px solid var(--c);display:grid;place-items:center;color:transparent;font-size:14px;font-weight:800}
.task.done .check{background:var(--c);color:var(--surface)}
.txt{flex:1;min-width:0;text-align:left}
.txt strong{display:block;font-weight:600;font-size:16px;overflow-wrap:anywhere}
.txt em{font-style:normal;color:var(--mute);font-size:13px}
.task.done strong{text-decoration:line-through;color:var(--mute)}
.empty{padding:36px 10px;text-align:center;color:var(--mute)}
.fab{position:fixed;right:20px;bottom:calc(20px + env(safe-area-inset-bottom,0px));width:60px;height:60px;border-radius:20px;background:var(--accent);color:var(--on-accent);font-size:32px;box-shadow:0 8px 24px rgba(40,50,140,.35)}
.scrim{position:fixed;inset:0;background:rgba(10,12,28,.5);display:none;align-items:flex-end;justify-content:center;z-index:20}
.scrim.on{display:flex}
.sheet{width:100%;max-width:560px;max-height:92vh;overflow-y:auto;background:var(--surface);border-radius:26px 26px 0 0;padding:22px 18px calc(22px + env(safe-area-inset-bottom,0px))}
.sheet h3{margin:0 0 14px;font-size:20px;font-weight:800}
.sheet label{display:block;font-size:13px;color:var(--mute);margin:14px 0 6px}
input[type=text],input[type=time]{width:100%;padding:14px;border-radius:14px;border:1px solid var(--line);background:var(--bg);color:var(--ink);font:inherit;font-size:16px}
.seg{display:flex;gap:8px;flex-wrap:wrap}
.seg button{padding:10px 14px;border-radius:12px;border:1px solid var(--line);font-size:14px}
.seg button[aria-pressed="true"]{border-color:var(--c,var(--accent));background:var(--c,var(--accent));color:#fff}
.row{display:flex;align-items:center;justify-content:space-between;margin-top:16px}
.save{width:100%;margin-top:20px;padding:16px;border-radius:16px;background:var(--accent);color:var(--on-accent);font-weight:800;font-size:16px}
.remove{width:100%;margin-top:8px;padding:14px;border-radius:16px;color:var(--hi);font-weight:600}
</style>
</head>
<body>
<main>
  <div class="top">
    <div><div class="date" id="date"></div><h1 id="hello"></h1></div>
    <button class="theme" id="theme" aria-label="Alternar tema">◐</button>
  </div>
  <div class="prog"><b id="n">0</b><span id="of"></span><div class="bar"><i id="fill"></i></div></div>
  <div class="chips" id="chips"></div>
  <div id="lists"></div>
</main>
<button class="fab" id="add" aria-label="Nova tarefa">+</button>

<div class="scrim" id="scrim">
  <div class="sheet" role="dialog" aria-label="Tarefa">
    <h3 id="sheetTitle">Nova tarefa</h3>
    <input type="text" id="title" placeholder="O que precisa ser feito?" maxlength="80">
    <label>Prioridade</label><div class="seg" id="pri"></div>
    <label>Categoria</label><div class="seg" id="cat"></div>
    <input type="text" id="newcat" placeholder="Ou crie uma nova categoria" maxlength="20" style="margin-top:8px">
    <label for="time">Horário (opcional)</label><input type="time" id="time">
    <label>Avisar</label><div class="seg" id="remind"></div>
    <div class="row"><span>Repetir todos os dias</span><button class="chip" id="daily" aria-pressed="false">Não</button></div>
    <button class="save" id="save">Salvar tarefa</button>
    <button class="remove" id="remove">Excluir tarefa</button>
  </div>
</div>

<script>
const PRI={alta:{n:"Alta prioridade",s:"Alta",v:"--hi"},media:{n:"Média prioridade",s:"Média",v:"--md"},baixa:{n:"Baixa prioridade",s:"Baixa",v:"--lo"}};
const DEF_CATS=["Trabalho","Filha","Casa","Compras"];
const REMINDS=[{v:0,label:"Na hora"},{v:5,label:"5 min antes"},{v:15,label:"15 min antes"},{v:30,label:"30 min antes"}];
const $=id=>document.getElementById(id);
const today=()=>new Date().toLocaleDateString("sv-SE");
const uid=()=>Math.random().toString(36).slice(2,9);
const nid=()=>1+Math.floor(Math.random()*2000000000);
let tasks=[],filter="Todas",form={};

function seed(){return[
 {t:"Bater ponto",p:"alta",c:"Trabalho",time:"08:00",daily:true},
 {t:"Levar a filha à escola",p:"alta",c:"Filha",time:"07:00",daily:true},
 {t:"Buscar a filha na escola",p:"alta",c:"Filha",time:"17:30",daily:true},
 {t:"Dar banho na filha",p:"media",c:"Filha",time:"19:30",daily:true},
 {t:"Ir ao mercado",p:"media",c:"Compras",time:"",daily:false},
 {t:"Comprar leite",p:"baixa",c:"Compras",time:"",daily:false}
].map(x=>({...x,id:uid(),nid:nid(),remind:0,done:false,doneOn:""}))}
function load(){try{const s=localStorage.getItem("rotina.v2");tasks=s?JSON.parse(s):seed()}catch(e){tasks=seed()}
 tasks.forEach(t=>{if(t.daily&&t.done&&t.doneOn!==today())t.done=false})}
function save(){try{localStorage.setItem("rotina.v2",JSON.stringify(tasks))}catch(e){}schedule()}
const cats=()=>[...new Set([...DEF_CATS,...tasks.map(t=>t.c)])];

/* Notificações */
const LN=window.Capacitor&&window.Capacitor.Plugins&&window.Capacitor.Plugins.LocalNotifications;
async function schedule(){
 if(!LN)return;
 try{
  let p=await LN.checkPermissions();
  if(p.display!=="granted")p=await LN.requestPermissions();
  if(p.display!=="granted")return;
  const pend=await LN.getPending();
  if(pend.notifications.length)await LN.cancel({notifications:pend.notifications.map(n=>({id:n.id}))});
  const list=[],now=new Date();
  tasks.forEach(t=>{
   if(!t.time)return;
   const[h,m]=t.time.split(":").map(Number);
   let tot=h*60+m-(t.remind||0);if(tot<0)tot+=1440;
   const hh=Math.floor(tot/60),mm=tot%60;
   const body=t.remind?"Em "+t.remind+" min, às "+t.time:"Agora, às "+t.time;
   if(t.daily)list.push({id:t.nid,title:t.t,body,schedule:{on:{hour:hh,minute:mm},allowWhileIdle:true}});
   else if(!t.done){const at=new Date();at.setHours(hh,mm,0,0);if(at>now)list.push({id:t.nid,title:t.t,body,schedule:{at,allowWhileIdle:true}})}
  });
  if(list.length)await LN.schedule({notifications:list});
 }catch(e){}
}

function el(tag,cls,text){const e=document.createElement(tag);if(cls)e.className=cls;if(text!=null)e.textContent=text;return e}
function render(){
 const d=new Date(),h=d.getHours();
 $("date").textContent=d.toLocaleDateString("pt-BR",{weekday:"long",day:"numeric",month:"long"});
 $("hello").textContent=h<12?"Bom dia":h<18?"Boa tarde":"Boa noite";
 const done=tasks.filter(t=>t.done).length;
 $("n").textContent=done;$("of").textContent="de "+tasks.length+" tarefas concluídas";
 $("fill").style.width=(tasks.length?done/tasks.length*100:0)+"%";
 const chips=$("chips");chips.replaceChildren();
 ["Todas",...cats()].forEach(c=>{const b=el("button","chip",c);b.setAttribute("aria-pressed",c===filter);b.onclick=()=>{filter=c;render()};chips.append(b)});
 const box=$("lists");box.replaceChildren();
 const vis=tasks.filter(t=>filter==="Todas"||t.c===filter);
 if(!vis.length){box.append(el("div","empty","Nada por aqui. Toque em + para adicionar uma tarefa."));return}
 Object.keys(PRI).forEach(k=>{
  const items=vis.filter(t=>t.p===k).sort((a,b)=>(a.done-b.done)||(a.time||"99").localeCompare(b.time||"99"));
  if(!items.length)return;
  const s=document.createElement("section"),h2=el("h2"),dot=el("span","dot");
  dot.style.background="var("+PRI[k].v+")";
  h2.append(dot,PRI[k].n+" ",el("small",null,items.filter(t=>!t.done).length+" pendentes"));
  const list=el("div","list");
  items.forEach(t=>{
   const row=el("div","task"+(t.done?" done":""));row.style.setProperty("--c","var("+PRI[k].v+")");
   const ck=el("button","check","✓");ck.setAttribute("aria-label","Concluir "+t.t);
   ck.onclick=()=>{t.done=!t.done;t.doneOn=t.done?today():"";save();render()};
   const tg=el("button","txt");
   tg.append(el("strong",null,t.t),el("em",null,[t.time,t.c,t.daily?"todo dia":""].filter(Boolean).join(" · ")));
   tg.onclick=()=>openSheet(t);
   row.append(ck,tg);list.append(row)});
  s.append(h2,list);box.append(s)});
}

/* Formulário (criar e editar) */
function seg(id,opts,key,color){const w=$(id);w.replaceChildren();
 opts.forEach(o=>{const b=el("button",null,o.label);if(color)b.style.setProperty("--c","var("+o.cv+")");
  b.setAttribute("aria-pressed",form[key]===o.v);b.onclick=()=>{form[key]=o.v;seg(id,opts,key,color)};w.append(b)})}
function setDaily(){const b=$("daily");b.textContent=form.daily?"Sim":"Não";b.setAttribute("aria-pressed",form.daily)}
function openSheet(t){
 form=t?{id:t.id,p:t.p,c:t.c,remind:t.remind||0,daily:t.daily}:{id:null,p:"media",c:"Casa",remind:0,daily:false};
 $("sheetTitle").textContent=t?"Editar tarefa":"Nova tarefa";
 $("title").value=t?t.t:"";$("time").value=t?t.time:"";$("newcat").value="";
 $("remove").style.display=t?"block":"none";
 seg("pri",Object.keys(PRI).map(k=>({v:k,label:PRI[k].s,cv:PRI[k].v})),"p",true);
 seg("cat",cats().map(c=>({v:c,label:c})),"c",false);
 seg("remind",REMINDS,"remind",false);setDaily();
 $("scrim").classList.add("on");
 if(!t)setTimeout(()=>$("title").focus(),50)}
const closeSheet=()=>$("scrim").classList.remove("on");
$("add").onclick=()=>openSheet(null);
$("scrim").onclick=e=>{if(e.target.id==="scrim")closeSheet()};
$("daily").onclick=()=>{form.daily=!form.daily;setDaily()};
$("save").onclick=()=>{
 const t=$("title").value.trim();if(!t){$("title").focus();return}
 const c=$("newcat").value.trim()||form.c,time=$("time").value;
 if(form.id){const x=tasks.find(z=>z.id===form.id);Object.assign(x,{t,p:form.p,c,time,remind:form.remind,daily:form.daily,done:false,doneOn:""})}
 else tasks.push({id:uid(),nid:nid(),t,p:form.p,c,time,remind:form.remind,daily:form.daily,done:false,doneOn:""});
 save();closeSheet();render()};
$("remove").onclick=()=>{tasks=tasks.filter(x=>x.id!==form.id);save();closeSheet();render()};
$("theme").onclick=()=>{const r=document.documentElement;
 const dark=r.dataset.theme?r.dataset.theme==="dark":matchMedia("(prefers-color-scheme:dark)").matches;
 r.dataset.theme=dark?"light":"dark";try{localStorage.setItem("rotina.theme",r.dataset.theme)}catch(e){}};
try{const th=localStorage.getItem("rotina.theme");if(th)document.documentElement.dataset.theme=th}catch(e){}
load();render();schedule();
</script>
</body>
</html>
