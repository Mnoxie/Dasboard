<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Vista de Campaña Comercial · Portfolio Manager</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700;800&display=swap');

:root{
  --rojo:#EC0000;
  --rojo-osc:#B80000;
  --rojo-soft:#FDECEC;
  --navy:#141C2E;
  --tinta:#1F2226;
  --tinta-60:#5C6268;
  --tinta-35:#949BA2;
  --fondo:#EFF1F3;
  --panel:#FFFFFF;
  --panel-2:#F7F8FA;
  --linea:#DCE1E6;
  --linea-suave:#EBEEF1;
  --verde:#357A39;
  --verde-soft:#E9F4EA;
  --ambar:#A96A00;
  --ambar-soft:#FCF2E1;
  --sombra:0 1px 3px rgba(20,28,46,.10), 0 1px 1px rgba(20,28,46,.04);
}
*{box-sizing:border-box;}
body{
  margin:0;background:var(--fondo);color:var(--tinta);
  font-family:'Open Sans',system-ui,sans-serif;font-size:13px;line-height:1.45;
}

/* ---------- Cabecera ---------- */
.topbar{
  background:var(--panel);
  border-bottom:3px solid var(--rojo);
  padding:12px 22px;
  display:flex;align-items:center;justify-content:space-between;
  gap:18px;flex-wrap:wrap;
}
.tb-left{display:flex;align-items:center;gap:12px;}
/* SLOT DEL LOGO — reemplazá por: <img src="logo-santander.svg" alt="Santander" class="logo-img"> */
.logo-slot{
  width:38px;height:38px;border-radius:5px;background:var(--rojo);
  display:grid;place-items:center;color:#fff;font-size:7px;font-weight:700;
  letter-spacing:.06em;text-align:center;line-height:1.1;flex-shrink:0;
}
.logo-img{width:38px;height:38px;object-fit:contain;display:block;}
.tb-title{font-size:17px;font-weight:700;margin:0;letter-spacing:-.01em;}
.tb-sub{font-size:12px;color:var(--tinta-60);margin:0;}

.tb-right{display:flex;align-items:center;gap:8px;flex-wrap:wrap;}
.filtro{
  display:flex;align-items:center;gap:7px;
  background:var(--panel-2);border:1px solid var(--linea);
  border-radius:5px;padding:6px 10px;
}
.filtro-ico{width:13px;height:13px;flex-shrink:0;color:var(--tinta-60);}
.filtro-lab{font-size:9px;font-weight:700;letter-spacing:.13em;text-transform:uppercase;color:var(--tinta-35);}
.filtro select{
  font-family:inherit;font-size:12px;font-weight:600;color:var(--tinta);
  border:none;background:transparent;cursor:pointer;padding:0;outline:none;
}
.ms{position:relative;}
.ms-btn{
  display:flex;align-items:center;gap:6px;
  font-family:inherit;font-size:12px;font-weight:600;color:var(--tinta);
  background:none;border:none;padding:0;cursor:pointer;
}
.ms-btn svg{width:11px;height:11px;color:var(--tinta-35);transition:transform .15s;}
.ms-btn[aria-expanded="true"] svg{transform:rotate(180deg);}
.ms-panel{
  display:none;position:absolute;top:calc(100% + 9px);right:0;z-index:30;
  min-width:190px;padding:5px;
  background:var(--panel);border:1px solid var(--linea);border-radius:7px;
  box-shadow:0 6px 20px rgba(20,28,46,.16);
}
.ms-panel.abierto{display:block;}
.ms-opt{
  display:flex;align-items:center;gap:9px;
  padding:8px 10px;border-radius:5px;cursor:pointer;
  font-size:12.5px;font-weight:600;color:var(--tinta-60);
  user-select:none;
}
.ms-opt:hover{background:var(--panel-2);color:var(--tinta);}
.ms-opt input{width:15px;height:15px;accent-color:var(--rojo);cursor:pointer;margin:0;flex-shrink:0;}
.ms-opt.todos{border-bottom:1px solid var(--linea-suave);border-radius:5px 5px 0 0;margin-bottom:3px;padding-bottom:9px;}
.btn-borrar{
  display:flex;align-items:center;gap:6px;
  font-family:inherit;font-size:11px;font-weight:600;color:var(--tinta-60);
  background:none;border:1px solid transparent;border-radius:5px;
  padding:7px 10px;cursor:pointer;
}
.btn-borrar:hover{background:var(--rojo-soft);color:var(--rojo-osc);}

/* ---------- Estructura ---------- */
.shell{display:flex;gap:16px;padding:16px 22px 40px;align-items:flex-start;}
.main{flex:1;min-width:0;}

/* ---------- Menú de vistas (placeholder, no navegable) ---------- */
.rail{
  width:104px;flex-shrink:0;
  display:flex;flex-direction:column;gap:8px;
  position:sticky;top:16px;
}
.rail-tit{
  font-size:9px;font-weight:700;letter-spacing:.14em;text-transform:uppercase;
  color:var(--tinta-35);padding-left:4px;margin-bottom:2px;
}
.vista{
  font-family:inherit;font-size:11.5px;font-weight:700;letter-spacing:.09em;
  text-transform:uppercase;color:var(--tinta-35);
  background:var(--panel);border:1px solid var(--linea);
  border-radius:999px;padding:11px 8px;text-align:center;
  cursor:not-allowed;user-select:none;
}
.vista[data-activa="true"]{background:var(--rojo);border-color:var(--rojo);color:#fff;cursor:default;}

/* ---------- Pestañas de segmentador ---------- */
.tabs{display:flex;justify-content:flex-end;gap:8px;flex-wrap:wrap;margin-bottom:-9px;padding-right:6px;position:relative;z-index:2;}
.tab{
  position:relative;
  font-family:inherit;font-size:11.5px;font-weight:700;letter-spacing:.09em;
  text-transform:uppercase;color:var(--tinta-60);
  background:var(--panel);border:1px solid var(--linea);
  border-radius:9px 9px 0 0;padding:9px 22px 15px;cursor:pointer;
  box-shadow:0 -1px 2px rgba(20,28,46,.05);
  transition:background .15s,color .15s,border-color .15s;
}
.tab:hover{color:var(--tinta);border-color:var(--tinta-35);}
.tab[aria-pressed="true"]{background:var(--rojo);border-color:var(--rojo);color:#fff;}
.tab:focus-visible{outline:2px solid var(--navy);outline-offset:2px;}
.tab.enter{animation:pop .22s ease-out backwards;}
@keyframes pop{from{opacity:0;transform:translateY(-4px);}to{opacity:1;transform:none;}}

/* ---------- Tarjetas ---------- */
.card{
  background:var(--panel);border:1px solid var(--linea);border-radius:9px;
  box-shadow:var(--sombra);padding:16px;margin-bottom:18px;position:relative;
}
.card.flash{animation:flash .5s ease-out;}
@keyframes flash{
  0%{box-shadow:0 0 0 0 rgba(236,0,0,.32),var(--sombra);}
  100%{box-shadow:0 0 0 8px rgba(236,0,0,0),var(--sombra);}
}
.card-tag{font-size:12px;font-weight:700;color:var(--tinta-60);margin:0 0 10px;}
.card-scope{font-size:11px;color:var(--tinta-35);font-weight:400;margin-left:8px;}
.card-body{display:flex;gap:16px;align-items:stretch;flex-wrap:wrap;}
.card-body > .tabla-wrap{flex:1 1 620px;min-width:0;overflow-x:auto;}

/* ---------- Matriz ---------- */
table{border-collapse:collapse;width:100%;min-width:620px;}
thead th{
  background:var(--navy);color:#fff;
  font-size:10px;font-weight:700;letter-spacing:.05em;text-transform:uppercase;
  padding:9px 5px;text-align:center;white-space:nowrap;
  border-right:1px solid rgba(255,255,255,.10);
}
thead th:first-child,thead th:nth-child(2){background:var(--panel);border-right-color:var(--linea);}
tbody th{
  text-align:left;font-size:10.5px;font-weight:700;letter-spacing:.06em;
  text-transform:uppercase;white-space:nowrap;padding:10px 9px;
  border:1px solid var(--linea);background:var(--panel);
}
tbody td{
  padding:10px 5px;text-align:right;font-size:12px;font-weight:600;
  font-variant-numeric:tabular-nums;border:1px solid var(--linea);white-space:nowrap;
}
td.unidad{
  text-align:center;font-size:10px;font-weight:700;color:var(--tinta-35);
  letter-spacing:.05em;background:var(--panel-2);
}
.chip{display:inline-block;min-width:48px;padding:2px 5px;border-radius:4px;
  font-size:11.5px;font-weight:700;font-variant-numeric:tabular-nums;}
.chip.alta{background:var(--verde-soft);color:var(--verde);}
.chip.media{background:var(--ambar-soft);color:var(--ambar);}
.chip.baja{background:var(--rojo-soft);color:var(--rojo-osc);}

/* ---------- KPIs ---------- */
.kpis{
  flex:1 1 244px;
  display:grid;grid-template-columns:1fr 1fr;gap:1px;
  background:var(--linea);border:1px solid var(--linea);border-radius:7px;overflow:hidden;
}
.kpi{background:var(--panel);padding:14px 10px;text-align:center;display:flex;
  flex-direction:column;justify-content:center;gap:5px;}
.kpi-lab{font-size:9.5px;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:var(--tinta-60);line-height:1.25;}
.kpi-val{font-size:26px;font-weight:800;letter-spacing:-.02em;line-height:1;}
.kpi-val.rojo{color:var(--rojo-osc);}

.aporte{
  flex:1 1 244px;
  border:1px solid var(--linea);border-radius:7px;overflow:hidden;
  display:flex;flex-direction:column;
}
.aporte-head{
  background:var(--navy);color:#fff;text-align:center;padding:8px;
  font-size:10px;font-weight:700;letter-spacing:.13em;text-transform:uppercase;
}
.aporte-body{flex:1;display:grid;grid-template-columns:1fr 1fr 1fr;background:var(--linea);gap:1px;}
.aporte-cel{background:var(--panel);padding:12px 5px;text-align:center;display:flex;
  flex-direction:column;justify-content:center;gap:5px;}
.aporte-lab{font-size:9px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:var(--tinta-60);}
.aporte-val{font-size:21px;font-weight:800;letter-spacing:-.02em;line-height:1;}

@media (max-width:820px){
  .shell{flex-direction:column;padding:14px;}
  .rail{width:100%;flex-direction:row;flex-wrap:wrap;position:static;}
  .rail-tit{width:100%;margin-bottom:0;}
  .vista{flex:1;min-width:72px;padding:9px 4px;font-size:10.5px;}
  .tabs{justify-content:flex-start;}
  .card-body > .tabla-wrap{flex:1 1 100%;}
}
@media (prefers-reduced-motion:reduce){*{animation:none !important;transition:none !important;}}
</style>
</head>
<body>

<header class="topbar">
  <div class="tb-left">
    <!-- Reemplazá por: <img src="logo-santander.svg" alt="Santander" class="logo-img"> -->
    <div class="logo-slot">LOGO</div>
    <div>
      <h1 class="tb-title">Vista de Campaña Comercial</h1>
      <p class="tb-sub">Portfolio Manager Particulares &amp; BP</p>
    </div>
  </div>
  <div class="tb-right">
    <div class="filtro">
      <svg class="filtro-ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polygon points="22 3 2 3 10 12.46 10 19 14 21 14 12.46 22 3"/></svg>
      <div class="ms" id="msSegmento">
        <div class="filtro-lab">Segmento</div>
        <button class="ms-btn" id="msBtn" type="button" aria-haspopup="true" aria-expanded="false">
          <span id="msLabel">Todos</span>
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 12 15 18 9"/></svg>
        </button>
        <div class="ms-panel" id="msPanel" role="group" aria-label="Segmentos"></div>
      </div>
    </div>
    <button class="btn-borrar" id="btnBorrar" type="button">
      <svg class="filtro-ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 6h18M8 6V4h8v2M19 6l-1 14H6L5 6"/></svg>
      Borrar filtros
    </button>
  </div>
</header>

<div class="shell">

  <nav class="rail" aria-label="Vistas del reporte">
    <div class="rail-tit">Vistas</div>
    <div class="vista" data-activa="true" aria-current="page">Vista 1</div>
    <div class="vista" aria-disabled="true">Vista 2</div>
    <div class="vista" aria-disabled="true">Vista 3</div>
    <div class="vista" aria-disabled="true">Vista 4</div>
    <div class="vista" aria-disabled="true">Vista 5</div>
  </nav>

  <main class="main">

  <div class="tabs" id="tabsProducto" role="group" aria-label="Producto"></div>

  <section class="card" id="panelTotal">
    <p class="card-tag">Total<span class="card-scope" id="scopeTotal"></span></p>
    <div class="card-body">
      <div class="tabla-wrap"><table id="tablaTotal"></table></div>
      <div class="kpis">
        <div class="kpi"><div class="kpi-lab">% Atraso</div><div class="kpi-val rojo" id="kpiAtraso">—</div></div>
        <div class="kpi"><div class="kpi-lab">Cobertura morosos</div><div class="kpi-val" id="kpiCobertura">—</div></div>
        <div class="kpi"><div class="kpi-lab">Venta promedio</div><div class="kpi-val" id="kpiVenta">—</div></div>
        <div class="kpi"><div class="kpi-lab">Oferta promedio</div><div class="kpi-val" id="kpiOferta">—</div></div>
      </div>
    </div>
  </section>

  <div class="tabs" id="tabsCartera" role="group" aria-label="Tipo de cartera"></div>

  <section class="card" id="panelDetalle">
    <p class="card-tag">Detalle<span class="card-scope" id="scopeDetalle"></span></p>
    <div class="card-body">
      <div class="tabla-wrap"><table id="tablaDetalle"></table></div>
      <div class="aporte">
        <div class="aporte-head">Aporte al total</div>
        <div class="aporte-body">
          <div class="aporte-cel"><div class="aporte-lab">Oferta</div><div class="aporte-val" id="apOferta">—</div></div>
          <div class="aporte-cel"><div class="aporte-lab">Venta</div><div class="aporte-val" id="apVenta">—</div></div>
          <div class="aporte-cel"><div class="aporte-lab">% Atraso</div><div class="aporte-val" id="apAtraso">—</div></div>
        </div>
      </div>
    </div>
  </section>

  </main>
</div>

<script>
const SEGMENTOS = ['Classic','A','B','Select','Negocio','P1','P2'];
const PRODUCTOS = {
  'Consumo':   ['Gestión Anticipada','Cartera Irregular','Cartera Vencida'],
  'Hipoteca':  ['Reestructuración Hipotecaria','Salida Integral','Reorganiza','Posterga','OTC'],
  'Comercial': ['Gestión Anticipada','Compra Cartera Interna','Adendum','Comercial']
};
const MESES = ['Ene','Feb','Mar','Abr','May','Jun','Jul','Ago','Sep','Oct','Nov','Dic'];

function seed(s){let h=2166136261;for(let i=0;i<s.length;i++){h^=s.charCodeAt(i);h=Math.imul(h,16777619);}return (h>>>0)/4294967295;}
function datos(seg,prod,sub,mes){
  const k=seg+prod+sub+mes;
  const oferta=Math.round(180+seed(k)*1650);
  const venta =Math.round(oferta*(0.16+seed(sub+mes+seg)*0.40));
  const atraso=venta*(0.06+seed(mes+prod+seg)*0.22);
  return {oferta,venta,atraso};
}

const nMil = new Intl.NumberFormat('es-CL');
const nDec = new Intl.NumberFormat('es-CL',{minimumFractionDigits:1,maximumFractionDigits:1});

let segmentosSel = new Set(); // vacio = todos
let productoSel='Consumo', carteraSel=PRODUCTOS['Consumo'][0];

const segsActivos = () => segmentosSel.size ? [...segmentosSel] : SEGMENTOS;
function etiquetaSegmento(){
  if(segmentosSel.size===0) return 'Todos';
  if(segmentosSel.size===1) return [...segmentosSel][0];
  if(segmentosSel.size===SEGMENTOS.length) return 'Todos';
  return segmentosSel.size + ' seleccionados';
}

function agregados(subs){
  const segs=segsActivos();
  return MESES.map(mes=>{
    let o=0,v=0,a=0;
    segs.forEach(s=>subs.forEach(sub=>{
      const d=datos(s,productoSel,sub,mes); o+=d.oferta; v+=d.venta; a+=d.atraso;
    }));
    return {oferta:o,venta:v,atraso:a};
  });
}
const suma = arr => arr.reduce((t,c)=>({oferta:t.oferta+c.oferta,venta:t.venta+c.venta,atraso:t.atraso+c.atraso}),{oferta:0,venta:0,atraso:0});

function chipEfect(c){
  const p=c.oferta?c.venta/c.oferta*100:0;
  const cls=p>=34?'alta':(p>=26?'media':'baja');
  return `<span class="chip ${cls}">${nDec.format(p)}%</span>`;
}

function pintarTabla(el,cols){
  const filas=[
    ['Oferta','MM$', c=>nMil.format(c.oferta)],
    ['Venta','MM$',  c=>nMil.format(c.venta)],
    ['Efectividad','%', chipEfect],
    ['Atraso venta','%', c=>nDec.format(c.venta?c.atraso/c.venta*100:0)+'%']
  ];
  el.innerHTML =
    '<thead><tr><th></th><th></th>' + MESES.map(m=>`<th>${m}</th>`).join('') + '</tr></thead><tbody>' +
    filas.map(([lab,uni,fn]) =>
      `<tr><th>${lab}</th><td class="unidad">${uni}</td>` +
      cols.map(c=>`<td>${fn(c)}</td>`).join('') + '</tr>'
    ).join('') + '</tbody>';
}

function pintarTabs(id,valores,activo,onPick,animar){
  const cont=document.getElementById(id);
  cont.innerHTML='';
  valores.forEach((v,i)=>{
    const b=document.createElement('button');
    b.className='tab'+(animar?' enter':'');
    if(animar) b.style.animationDelay=(i*40)+'ms';
    b.type='button'; b.textContent=v;
    b.setAttribute('aria-pressed', v===activo);
    b.onclick=()=>onPick(v);
    cont.appendChild(b);
  });
}

function render(animarCartera,paneles){
  document.getElementById('msLabel').textContent = etiquetaSegmento();
  const panel = document.getElementById('msPanel');
  panel.innerHTML =
    `<label class="ms-opt todos"><input type="checkbox" data-todos="1"${segmentosSel.size===0?' checked':''}>Todos</label>` +
    SEGMENTOS.map(v=>
      `<label class="ms-opt"><input type="checkbox" value="${v}"${segmentosSel.has(v)?' checked':''}>${v}</label>`
    ).join('');
  panel.querySelectorAll('input').forEach(inp=>{
    inp.onchange = ()=>{
      if(inp.dataset.todos){ segmentosSel.clear(); }
      else if(inp.checked){ segmentosSel.add(inp.value); }
      else { segmentosSel.delete(inp.value); }
      render(false,['panelTotal','panelDetalle']);
    };
  });

  pintarTabs('tabsProducto',Object.keys(PRODUCTOS),productoSel,v=>{
    productoSel=v; carteraSel=PRODUCTOS[v][0]; render(true,['panelTotal','panelDetalle']);
  },false);
  pintarTabs('tabsCartera',PRODUCTOS[productoSel],carteraSel,v=>{
    carteraSel=v; render(false,['panelDetalle']);
  },animarCartera);

  const subsTotal = PRODUCTOS[productoSel];
  const colsTotal = agregados(subsTotal);
  const colsDet   = agregados([carteraSel]);

  pintarTabla(document.getElementById('tablaTotal'),colsTotal);
  pintarTabla(document.getElementById('tablaDetalle'),colsDet);

  const T=suma(colsTotal), n=colsTotal.length;
  document.getElementById('kpiAtraso').textContent    = Math.round(T.venta?T.atraso/T.venta*100:0)+'%';
  document.getElementById('kpiCobertura').textContent = Math.round(38+(T.oferta%25))+'%';
  document.getElementById('kpiVenta').textContent     = Math.round(T.venta/n)+' M';
  document.getElementById('kpiOferta').textContent    = nDec.format(T.oferta/n/1000)+' MM';

  const D=suma(colsDet);
  const pct=(a,b)=> b? Math.round(a/b*100)+'%' : '—';
  document.getElementById('apOferta').textContent = pct(D.oferta,T.oferta);
  document.getElementById('apVenta').textContent  = pct(D.venta,T.venta);
  document.getElementById('apAtraso').textContent = Math.round(D.venta?D.atraso/D.venta*100:0)+'%';

  document.getElementById('scopeTotal').textContent =
    `· ${etiquetaSegmento()} · ${productoSel} — suma de ${PRODUCTOS[productoSel].length} tipos de cartera`;
  document.getElementById('scopeDetalle').textContent = `· ${etiquetaSegmento()} · ${productoSel} › ${carteraSel}`;

  (paneles||[]).forEach(id=>{
    const el=document.getElementById(id);
    el.classList.remove('flash'); void el.offsetWidth; el.classList.add('flash');
  });
}

const msBtn=document.getElementById('msBtn'), msPanel=document.getElementById('msPanel');
msBtn.onclick = e=>{
  e.stopPropagation();
  const abierto = msPanel.classList.toggle('abierto');
  msBtn.setAttribute('aria-expanded', abierto);
};
msPanel.onclick = e=>e.stopPropagation();
document.addEventListener('click', ()=>{
  msPanel.classList.remove('abierto');
  msBtn.setAttribute('aria-expanded','false');
});
document.addEventListener('keydown', e=>{
  if(e.key==='Escape'){ msPanel.classList.remove('abierto'); msBtn.setAttribute('aria-expanded','false'); }
});
document.getElementById('btnBorrar').onclick = ()=>{
  segmentosSel.clear(); productoSel='Consumo'; carteraSel=PRODUCTOS['Consumo'][0];
  render(true,['panelTotal','panelDetalle']);
};
render(false,[]);
</script>
</body>
</html>
