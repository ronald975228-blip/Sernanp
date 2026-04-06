<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Reporte MGAS — SERNANP</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:Arial,sans-serif;background:#F0F4F8;color:#1a1a1a;font-size:13px;}
.topbar{background:#1F3864;color:#fff;padding:11px 24px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100;}
.topbar h1{font-size:14px;font-weight:700;}
.topbar .sub{font-size:10px;color:#93B8DC;margin-top:2px;}
.topbar-right{text-align:right;}
#timer{font-size:11px;color:#93B8DC;}
#anp-badge{background:rgba(255,255,255,.15);border-radius:16px;padding:3px 12px;font-size:11px;margin-top:4px;display:inline-block;}
.container{max-width:1100px;margin:0 auto;padding:16px;}
.steps{display:flex;background:#fff;border-radius:8px;border:1px solid #D0D9E8;overflow:hidden;margin-bottom:14px;box-shadow:0 1px 3px rgba(0,0,0,.06);}
.step{flex:1;padding:9px 10px;border:none;background:transparent;cursor:pointer;font-family:Arial,sans-serif;font-size:11.5px;color:#666;border-right:1px solid #E0E8F0;text-align:left;transition:.15s;}
.step:last-child{border-right:none;}
.step.active{background:#EBF3FB;color:#1F3864;font-weight:700;}
.step.done{color:#2e7d32;}
.step .sn{display:inline-flex;align-items:center;justify-content:center;width:20px;height:20px;border-radius:50%;background:#D0D9E8;color:#555;font-size:10px;font-weight:700;margin-right:6px;}
.step.active .sn{background:#2E75B6;color:#fff;}
.step.done .sn{background:#2e7d32;color:#fff;}
.step .sub{display:block;font-size:10px;color:#999;margin-top:2px;margin-left:26px;}
.sec{display:none;animation:fadein .2s;}
.sec.active{display:block;}
@keyframes fadein{from{opacity:0;transform:translateY(4px)}to{opacity:1;transform:translateY(0)}}
.card{background:#fff;border-radius:8px;border:1px solid #D0D9E8;padding:14px 18px;margin-bottom:12px;box-shadow:0 1px 3px rgba(0,0,0,.04);}
.card-hdr{font-size:10.5px;font-weight:700;color:#2E75B6;text-transform:uppercase;letter-spacing:.07em;border-bottom:1px solid #E6F1FB;padding-bottom:7px;margin-bottom:11px;}
.anp-hero{background:#1F3864;border-radius:8px;padding:14px 20px;margin-bottom:12px;display:flex;align-items:flex-end;gap:14px;flex-wrap:wrap;}
.anp-hero label{font-size:10px;color:#93B8DC;display:block;margin-bottom:3px;font-weight:600;}
.anp-hero select,.anp-hero input[type=number]{background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.25);border-radius:5px;color:#fff;padding:6px 10px;font-size:12px;font-family:Arial,sans-serif;}
.anp-hero select{min-width:300px;}
.anp-hero select option{color:#1a1a1a;background:#fff;}
.g2{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.g3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;}
.f{display:flex;flex-direction:column;gap:3px;margin-bottom:6px;}
.f label{font-size:10.5px;color:#555;font-weight:700;}
.f input,.f select,.f textarea{padding:6px 9px;border:1px solid #C8D6E5;border-radius:5px;font-size:12px;font-family:Arial,sans-serif;color:#1a1a1a;}
.f input:focus,.f select:focus,.f textarea:focus{outline:none;border-color:#2E75B6;box-shadow:0 0 0 3px rgba(46,117,182,.1);}
.f textarea{resize:vertical;min-height:68px;line-height:1.5;}
.cats{display:flex;gap:6px;flex-wrap:wrap;padding:5px 0;}
.cats label{display:flex;align-items:center;gap:3px;font-size:11px;background:#F0F4F8;padding:4px 8px;border-radius:4px;border:1px solid #D0D9E8;cursor:pointer;}
.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:12px;}
.stat{background:#fff;border-radius:8px;border:1px solid #D0D9E8;padding:10px 12px;text-align:center;}
.stat-n{font-size:22px;font-weight:700;color:#2E75B6;}
.stat-l{font-size:10px;color:#888;margin-top:2px;}
.gbar{height:6px;background:#D0D9E8;border-radius:3px;margin-top:5px;overflow:hidden;}
.gbar-fill{height:100%;background:#2E75B6;border-radius:3px;transition:width .3s;}
.tbl{overflow-x:auto;border-radius:6px;border:1px solid #D0D9E8;}
table{width:100%;border-collapse:collapse;font-size:11px;}
thead th{background:#1F3864;color:#fff;padding:7px 5px;text-align:center;font-size:9.5px;font-weight:700;white-space:nowrap;border-right:1px solid rgba(255,255,255,.12);}
th.tl{text-align:left;}
tbody tr:nth-child(even){background:#F8FBFF;}
tbody tr:hover:not(.eas-row){background:#EBF3FB;}
td{padding:4px 5px;border-bottom:1px solid #E8EFF7;border-right:1px solid #E8EFF7;vertical-align:middle;}
tr.eas-row td{background:#D6E4F0;font-weight:700;color:#1F3864;font-size:10px;padding:5px 10px;border-bottom:1px solid #B5D4F4;}
td input[type=number]{width:100%;border:1px solid #C8D6E5;border-radius:3px;padding:3px 3px;font-size:11px;text-align:center;font-family:Arial,sans-serif;}
td input[type=number]:focus{outline:none;border-color:#2E75B6;}
td input[type=text],td input[type=date]{width:100%;border:1px solid #C8D6E5;border-radius:3px;padding:3px 5px;font-size:10px;font-family:Arial,sans-serif;}
.tn{text-align:center;color:#999;font-size:10px;width:26px;}
.tc{background:#EBF3FB;color:#0C447C;text-align:center;font-weight:700;}
.tind{font-size:10px;line-height:1.4;}
.tact{font-size:10px;color:#555;}
.tu{font-size:10px;color:#666;text-align:center;}
.pb{display:flex;align-items:center;gap:4px;}
.pb-bg{flex:1;height:5px;background:#D0D9E8;border-radius:3px;overflow:hidden;}
.pb-fill{height:100%;background:#1D9E75;border-radius:3px;transition:width .2s;}
.pb-lbl{font-size:10px;font-weight:700;color:#0C447C;min-width:30px;}
.acts{display:flex;justify-content:space-between;align-items:center;padding-top:10px;}
.btn{padding:7px 18px;border-radius:6px;font-size:12px;font-weight:600;cursor:pointer;font-family:Arial,sans-serif;border:1px solid #C8D6E5;background:#fff;color:#333;transition:.15s;}
.btn:hover{background:#F0F4F8;}
.btn-p{background:#2E75B6;color:#fff;border-color:#2E75B6;}
.btn-p:hover{background:#1F3864;}
.export-box{background:#E6F1FB;border:1px solid #B5D4F4;border-radius:8px;padding:14px 20px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px;margin-bottom:12px;}
.export-title{font-size:13px;font-weight:700;color:#1F3864;}
.export-sub{font-size:11px;color:#2E75B6;margin-top:3px;}
.btn-xl{background:#1F3864;color:#fff;border:none;padding:11px 28px;font-size:13px;font-weight:700;border-radius:6px;cursor:pointer;font-family:Arial,sans-serif;}
.btn-xl:hover{background:#2E75B6;}
.btn-xl:disabled{background:#999;cursor:not-allowed;}
.badge-ok{background:#E8F5E9;color:#2e7d32;font-size:10.5px;padding:3px 10px;border-radius:12px;font-weight:600;}
.badge-w{background:#FFF8E1;color:#795548;font-size:10.5px;padding:3px 10px;border-radius:12px;font-weight:600;}
.clbl{font-size:10.5px;font-weight:700;color:#2E75B6;margin-bottom:4px;}
.cblk{margin-bottom:10px;}
.mv-inp{font-size:10px;color:#2E75B6;}
footer{text-align:center;padding:14px;font-size:10px;color:#aaa;}
#toast{position:fixed;bottom:24px;right:24px;background:#1F3864;color:#fff;padding:10px 20px;border-radius:8px;font-size:12px;font-weight:600;display:none;z-index:200;}
</style>
</head>
<body>

<div class="topbar">
  <div>
    <h1>Reporte Trimestral de Salvaguardas — MGAS-SERNANP</h1>
    <div class="sub">EAS 1, 2, 3, 4, 5, 7, 8, 10 — Banco Mundial &nbsp;|&nbsp; 39 indicadores &nbsp;|&nbsp; 78 ANP</div>
  </div>
  <div class="topbar-right">
    <div id="timer">⏱ 00:00</div>
    <div id="anp-badge">Sin ANP seleccionada</div>
  </div>
</div>

<div class="container">
  <div class="steps">
    <button class="step active" onclick="goStep(0)"><span class="sn">1</span>Identificación<span class="sub">ANP y período</span></button>
    <button class="step" onclick="goStep(1)"><span class="sn">2</span>Ejecución MGAS<span class="sub">39 indicadores</span></button>
    <button class="step" onclick="goStep(2)"><span class="sn">3</span>Conclusiones<span class="sub">Narrativa trimestral</span></button>
    <button class="step" onclick="goStep(3)"><span class="sn">4</span>Medios de verificación<span class="sub">Links y evidencias</span></button>
  </div>

  <!-- PASO 1 -->
  <div id="sec0" class="sec active">
    <div class="anp-hero">
      <div style="flex:2;min-width:260px;">
        <label>Área Natural Protegida</label>
        <select id="anp_sel" onchange="setANP(this.value)" style="width:100%;">
          <option value="">-- Seleccione el ANP --</option>
        </select>
      </div>
      <div>
        <label>Trimestre</label>
        <select id="p_trim">
          <option value="">Seleccionar...</option>
          <option value="I">I Trimestre</option>
          <option value="II">II Trimestre</option>
          <option value="III">III Trimestre</option>
          <option value="IV">IV Trimestre</option>
        </select>
      </div>
      <div>
        <label>Año</label>
        <input type="number" id="p_anio" value="2025" min="2020" max="2035" style="width:78px;">
      </div>
    </div>
    <div class="card">
      <div class="card-hdr">Datos generales del reporte</div>
      <div class="g2">
        <div class="f"><label>Nombre del Proyecto REDD+</label><input type="text" id="p_nombre" placeholder="Ej. Proyecto REDD+ AIDER-PNBS"></div>
        <div class="f"><label>Código del proyecto</label><input type="text" id="p_codigo" placeholder="Ej. FP001-PE"></div>
      </div>
      <div class="g2">
        <div class="f"><label>Entidad Ejecutora / UCP</label><input type="text" id="p_entidad" placeholder="Ej. AIDER"></div>
        <div class="f"><label>Dependencia SERNANP</label><input type="text" id="p_dep" placeholder="Jefatura / Dirección..."></div>
      </div>
      <div class="g2">
        <div class="f"><label>Período — Desde</label><input type="date" id="p_desde"></div>
        <div class="f"><label>Período — Hasta</label><input type="date" id="p_hasta"></div>
      </div>
      <div class="g3">
        <div class="f"><label>Jefe(a) de ANP</label><input type="text" id="p_jefe"></div>
        <div class="f"><label>Punto Focal de Salvaguardas</label><input type="text" id="p_focal"></div>
        <div class="f"><label>Responsable del reporte</label><input type="text" id="p_resp"></div>
      </div>
      <div class="g3">
        <div class="f"><label>Fecha de elaboración</label><input type="date" id="p_fecha"></div>
        <div class="f"><label>N° de reporte</label><input type="text" id="p_nro" placeholder="001-2025"></div>
        <div class="f"><label>Versión</label><input type="text" id="p_ver" value="1.0"></div>
      </div>
      <div class="f">
        <label>Categoría de Manejo</label>
        <div class="cats">
          <label><input type="checkbox" name="cat" value="PN"> PN</label>
          <label><input type="checkbox" name="cat" value="RN"> RN</label>
          <label><input type="checkbox" name="cat" value="SN"> SN</label>
          <label><input type="checkbox" name="cat" value="RC"> RC</label>
          <label><input type="checkbox" name="cat" value="BP"> BP</label>
          <label><input type="checkbox" name="cat" value="ZR"> ZR</label>
          <label><input type="checkbox" name="cat" value="RVS"> RVS</label>
          <label><input type="checkbox" name="cat" value="SH"> SH</label>
          <label><input type="checkbox" name="cat" value="RP"> RP</label>
          <label><input type="checkbox" name="cat" value="CC"> CC</label>
          <label><input type="checkbox" name="cat" value="ACR"> ACR</label>
          <label><input type="checkbox" name="cat" value="ACP"> ACP</label>
        </div>
      </div>
    </div>
    <div class="acts">
      <span id="s0-status" class="badge-w">Seleccione un ANP para comenzar</span>
      <button class="btn btn-p" onclick="goStep(1)">Siguiente: Ejecución MGAS →</button>
    </div>
  </div>

  <!-- PASO 2 -->
  <div id="sec1" class="sec">
    <div class="stats">
      <div class="stat"><div class="stat-n">39</div><div class="stat-l">Indicadores</div></div>
      <div class="stat"><div class="stat-n" id="st-meta">0</div><div class="stat-l">Meta anual total</div></div>
      <div class="stat"><div class="stat-n" id="st-ejec">0</div><div class="stat-l">Total ejecutado</div></div>
      <div class="stat">
        <div class="stat-n" id="st-pct">0%</div>
        <div class="stat-l">Avance global</div>
        <div class="gbar"><div class="gbar-fill" id="gbar" style="width:0%"></div></div>
      </div>
    </div>
    <div class="card" style="padding:10px;">
      <div class="tbl">
        <table>
          <colgroup>
            <col style="width:26px"><col style="width:110px"><col style="width:220px"><col style="width:72px">
            <col style="width:56px"><col style="width:44px"><col style="width:44px"><col style="width:44px"><col style="width:44px">
            <col style="width:58px"><col style="width:82px">
          </colgroup>
          <thead><tr>
            <th>N°</th><th class="tl">EAS / Actividad</th><th class="tl">Indicador / Medida</th><th>Unidad</th>
            <th>Meta<br>anual</th><th>I<br>Trim.</th><th>II<br>Trim.</th><th>III<br>Trim.</th><th>IV<br>Trim.</th>
            <th>Total<br>ejec.</th><th>Avance %</th>
          </tr></thead>
          <tbody id="mgas-tbody"></tbody>
        </table>
      </div>
    </div>
    <div class="acts">
      <button class="btn" onclick="goStep(0)">← Identificación</button>
      <button class="btn btn-p" onclick="goStep(2)">Siguiente: Conclusiones →</button>
    </div>
  </div>

  <!-- PASO 3 -->
  <div id="sec2" class="sec">
    <div class="card">
      <div class="card-hdr">Conclusiones, lecciones aprendidas y compromisos</div>
      <div class="cblk"><div class="clbl">1. Síntesis del estado de cumplimiento de salvaguardas del trimestre</div><textarea id="c1" placeholder="Describa el nivel de cumplimiento general..."></textarea></div>
      <div class="cblk"><div class="clbl">2. Principales logros vs. trimestre anterior</div><textarea id="c2" placeholder="Avances más relevantes..."></textarea></div>
      <div class="cblk"><div class="clbl">3. Lecciones aprendidas y buenas prácticas a escalar</div><textarea id="c3" placeholder="Aprendizajes clave y prácticas replicables..."></textarea></div>
      <div class="cblk"><div class="clbl">4. Compromisos y metas para el siguiente trimestre</div><textarea id="c4" placeholder="Compromisos asumidos..."></textarea></div>
      <div class="cblk"><div class="clbl">5. Recomendaciones al SERNANP / financiadores</div><textarea id="c5" placeholder="Recomendaciones institucionales..."></textarea></div>
    </div>
    <div class="acts">
      <button class="btn" onclick="goStep(1)">← Ejecución</button>
      <button class="btn btn-p" onclick="goStep(3)">Siguiente: Medios de verificación →</button>
    </div>
  </div>

  <!-- PASO 4 -->
  <div id="sec3" class="sec">
    <div class="card" style="padding:10px;">
      <div class="card-hdr">Catálogo de medios de verificación</div>
      <p style="font-size:11px;color:#666;margin-bottom:8px;">Registre el link o ruta de archivo por cada indicador. Puede dejarlo en blanco si no aplica este trimestre.</p>
      <div class="tbl">
        <table>
          <colgroup>
            <col style="width:26px"><col style="width:90px"><col style="width:185px"><col style="width:110px"><col style="width:240px"><col style="width:100px">
          </colgroup>
          <thead><tr>
            <th>N°</th><th class="tl">EAS</th><th class="tl">Indicador</th><th>Tipo de evidencia</th><th>Link / Ruta al documento</th><th>Fecha del doc.</th>
          </tr></thead>
          <tbody id="mv-tbody"></tbody>
        </table>
      </div>
    </div>
    <div class="export-box">
      <div>
        <div class="export-title">Generar reporte Excel institucional</div>
        <div class="export-sub" id="export-info">Complete la identificación y ejecución antes de descargar</div>
      </div>
      <button class="btn-xl" id="btn-export" onclick="generarExcel()">⬇ Descargar Reporte .xlsx</button>
    </div>
    <div class="acts">
      <button class="btn" onclick="goStep(2)">← Conclusiones</button>
      <span class="badge-ok">Formulario listo para exportar</span>
    </div>
  </div>
</div>

<footer>SERNANP — Sistema de Reporte MGAS-REDD+ &nbsp;|&nbsp; Uso interno institucional</footer>
<div id="toast">✓ Reporte generado y descargado</div>

<script>
const ANP_LIST = [
  {n:'Parque Nacional del Manu',c:'PN-MAN-001',cat:'PN'},
  {n:'Parque Nacional Bahuaja-Sonene',c:'PN-BAS-002',cat:'PN'},
  {n:'Parque Nacional Río Abiseo',c:'PN-RIA-003',cat:'PN'},
  {n:'Parque Nacional Yanachaga-Chemillén',c:'PN-YCH-004',cat:'PN'},
  {n:'Parque Nacional Tingo María',c:'PN-TMA-005',cat:'PN'},
  {n:'Parque Nacional Huascarán',c:'PN-HUA-006',cat:'PN'},
  {n:'Parque Nacional Cerros de Amotape',c:'PN-CAM-007',cat:'PN'},
  {n:'Parque Nacional Cutervo',c:'PN-CUT-008',cat:'PN'},
  {n:'Parque Nacional Otishi',c:'PN-OTI-009',cat:'PN'},
  {n:'Parque Nacional Sierra del Divisor',c:'PN-SDD-010',cat:'PN'},
  {n:'Parque Nacional Ichigkat Muja-Cordillera del Cóndor',c:'PN-IMC-011',cat:'PN'},
  {n:'Parque Nacional Alto Purús',c:'PN-APU-012',cat:'PN'},
  {n:'Reserva Nacional Pampa Galeras',c:'RN-PAG-013',cat:'RN'},
  {n:'Reserva Nacional de Paracas',c:'RN-PAR-014',cat:'RN'},
  {n:'Reserva Nacional de Junín',c:'RN-JUN-015',cat:'RN'},
  {n:'Reserva Nacional Pacaya Samiria',c:'RN-PSA-016',cat:'RN'},
  {n:'Reserva Nacional Titicaca',c:'RN-TIT-017',cat:'RN'},
  {n:'Reserva Nacional de Calipuy',c:'RN-CAL-018',cat:'RN'},
  {n:'Reserva Nacional Lachay',c:'RN-LAC-019',cat:'RN'},
  {n:'Reserva Nacional Tambopata',c:'RN-TAM-020',cat:'RN'},
  {n:'Reserva Nacional Allpahuayo-Mishana',c:'RN-ALM-021',cat:'RN'},
  {n:'Reserva Nacional Sistema de Islas y Puntas Guaneras',c:'RN-SIP-022',cat:'RN'},
  {n:'Reserva Nacional Matsés',c:'RN-MAT-023',cat:'RN'},
  {n:'Reserva Nacional Pucacuro',c:'RN-PUC-024',cat:'RN'},
  {n:'Reserva Nacional Cordillera Azul',c:'RN-CAZ-025',cat:'RN'},
  {n:'Refugio de Vida Silvestre Los Pantanos de Villa',c:'RVS-LPV-026',cat:'RVS'},
  {n:'Refugio de Vida Silvestre Laquipampa',c:'RVS-LAQ-027',cat:'RVS'},
  {n:'Refugio de Vida Silvestre Bosques Nublados de Udima',c:'RVS-BNU-028',cat:'RVS'},
  {n:'Santuario Nacional de Huayllay',c:'SN-HUY-029',cat:'SN'},
  {n:'Santuario Nacional Lagunas de Mejía',c:'SN-LME-030',cat:'SN'},
  {n:'Santuario Nacional Los Manglares de Tumbes',c:'SN-LMT-031',cat:'SN'},
  {n:'Santuario Nacional Tabaconas Namballe',c:'SN-TNM-032',cat:'SN'},
  {n:'Santuario Nacional Ampay',c:'SN-AMP-033',cat:'SN'},
  {n:'Santuario Nacional Pampa Hermosa',c:'SN-PHE-034',cat:'SN'},
  {n:'Santuario Nacional Megantoni',c:'SN-MEG-035',cat:'SN'},
  {n:'Santuario Histórico de Chacamarca',c:'SH-CHA-036',cat:'SH'},
  {n:'Santuario Histórico Bosque de Pómac',c:'SH-BPO-037',cat:'SH'},
  {n:'Santuario Histórico Pampas de Ayacucho',c:'SH-PAY-038',cat:'SH'},
  {n:'Santuario Histórico Machu Picchu',c:'SH-MAP-039',cat:'SH'},
  {n:'Reserva Comunal El Sira',c:'RC-ELS-040',cat:'RC'},
  {n:'Reserva Comunal Amarakaeri',c:'RC-AMA-041',cat:'RC'},
  {n:'Reserva Comunal Purús',c:'RC-PUR-042',cat:'RC'},
  {n:'Reserva Comunal Machiguenga',c:'RC-MAC-043',cat:'RC'},
  {n:'Reserva Comunal Ashaninka',c:'RC-ASH-044',cat:'RC'},
  {n:'Reserva Comunal Matses',c:'RC-MAS-045',cat:'RC'},
  {n:'Reserva Comunal Tuntanain',c:'RC-TUN-046',cat:'RC'},
  {n:'Reserva Comunal Airo Pai',c:'RC-AIP-047',cat:'RC'},
  {n:'Reserva Comunal Huimeki',c:'RC-HUI-048',cat:'RC'},
  {n:'Bosque de Protección Alto Mayo',c:'BP-ALM-049',cat:'BP'},
  {n:'Bosque de Protección Pagaibamba',c:'BP-PAG-050',cat:'BP'},
  {n:'Bosque de Protección Pui Pui',c:'BP-PUI-051',cat:'BP'},
  {n:'Bosque de Protección San Matías-San Carlos',c:'BP-SMS-052',cat:'BP'},
  {n:'Bosque de Protección Cuenca del Río Nemos',c:'BP-CRN-053',cat:'BP'},
  {n:'Zona Reservada Chancaybaños',c:'ZR-CHA-054',cat:'ZR'},
  {n:'Zona Reservada Cordillera Huayhuash',c:'ZR-CHU-055',cat:'ZR'},
  {n:'Zona Reservada Güeppí',c:'ZR-GUE-056',cat:'ZR'},
  {n:'Zona Reservada Megantoni',c:'ZR-MEG-057',cat:'ZR'},
  {n:'Zona Reservada Río Nieva',c:'ZR-RNI-058',cat:'ZR'},
  {n:'Zona Reservada Santiago Comaina',c:'ZR-SCO-059',cat:'ZR'},
  {n:'Zona Reservada Sierra del Divisor',c:'ZR-SDD-060',cat:'ZR'},
  {n:'Zona Reservada Tumbes',c:'ZR-TUM-061',cat:'ZR'},
  {n:'Zona Reservada Illescas',c:'ZR-ILL-062',cat:'ZR'},
  {n:'Zona Reservada Los Pantanos de Villa',c:'ZR-LPV-063',cat:'ZR'},
  {n:'Zona Reservada Pucacuro',c:'ZR-PUC-064',cat:'ZR'},
  {n:'Zona Reservada Udima',c:'ZR-UDI-065',cat:'ZR'},
  {n:'Reserva Paisajística Subcuenca del Cotahuasi',c:'RP-SCO-066',cat:'RP'},
  {n:'Reserva Paisajística Nor Yauyos-Cochas',c:'RP-NYC-067',cat:'RP'},
  {n:'Coto de Caza El Angolo',c:'CC-ANG-068',cat:'CC'},
  {n:'Coto de Caza Sunchubamba',c:'CC-SUN-069',cat:'CC'},
  {n:'ACR Cordillera Escalera',c:'ACR-CES-070',cat:'ACR'},
  {n:'ACR Comunal Tamshiyacu Tahuayo',c:'ACR-CTT-071',cat:'ACR'},
  {n:'ACR Imiría',c:'ACR-IMI-072',cat:'ACR'},
  {n:'ACR Punchana',c:'ACR-PUN-073',cat:'ACR'},
  {n:'ACR Salitral-Huarmaca',c:'ACR-SHU-074',cat:'ACR'},
  {n:'ACR Humedales de Puerto Viejo',c:'ACR-HPV-075',cat:'ACR'},
  {n:'ACR Albufera de Medio Mundo',c:'ACR-AMM-076',cat:'ACR'},
  {n:'ACR Bosques Secos Salitral',c:'ACR-BSS-077',cat:'ACR'},
  {n:'ACR Vilacota-Maure',c:'ACR-VMA-078',cat:'ACR'},
];

const INDS = [
  {eas:'EAS-1',lbl:'EAS-1: Evaluación y gestión de riesgos e impactos ambientales y sociales'},
  {n:1,act:'Gestión Ambiental en ANP',ind:'N° de informes de seguimiento a ≥10% de proyectos habilitados (construcción, operación o cierre)',u:'Informe',mv:'Informe de seguimiento a los proyectos'},
  {n:2,act:'Gestión Ambiental en ANP',ind:'N° de infraestructuras con conformidad y compatibilidad de la DGANP',u:'Infraestructura',mv:'Informe DGANP - conformidad y compatibilidad'},
  {eas:'EAS-2',lbl:'EAS-2: Trabajo y condiciones laborales — Guardaparques y personal ANP'},
  {n:3,act:'Vigilancia y Control',ind:'Capacitaciones en prevención de riesgos laborales (puesto de trabajo)',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:4,act:'Vigilancia y Control',ind:'Capacitaciones sobre patrullajes acuáticos',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:5,act:'Vigilancia y Control',ind:'Capacitaciones sobre patrullajes terrestres',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:6,act:'Vigilancia y Control',ind:'Capacitaciones sobre hallazgos y avistamientos de PIACI',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:7,act:'Vigilancia y Control',ind:'Reportes de hallazgos/avistamientos de PIACI enviados a MINCUL',u:'Reporte',mv:'Reportes enviados a MINCUL'},
  {n:8,act:'Vigilancia y Control',ind:'Capacitaciones en rescate de alta montaña / alta mar / vía fluvial',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:9,act:'Vigilancia y Control',ind:'Puestos de vigilancia con números de emergencia visibles',u:'Puesto de Vigilancia',mv:'Foto del número de emergencia en el PVC'},
  {n:10,act:'Vigilancia y Control',ind:'Puestos de vigilancia con flujograma de comunicación visible',u:'Puesto de Vigilancia',mv:'Foto del flujograma en el PVC'},
  {n:11,act:'Vigilancia y Control',ind:'Capacitaciones en primeros auxilios',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:12,act:'Vigilancia y Control',ind:'Puestos de vigilancia con botiquín de primeros auxilios equipado',u:'Puesto de Vigilancia',mv:'Foto del botiquín en el PVC'},
  {n:13,act:'Vigilancia y Control',ind:'Capacitaciones sobre conducción de vehículos / embarcaciones',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:14,act:'Vigilancia y Control',ind:'Capacitaciones sobre riesgos biológicos (vectores)',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:15,act:'Vigilancia y Control',ind:'Capacitaciones en los procesos de intervención',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:16,act:'Vigilancia y Control',ind:'Capacitaciones para prevenir y tratar mordeduras de reptiles u otros animales',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {eas:'EAS-3',lbl:'EAS-3: Eficiencia en el uso de recursos y gestión de contaminación'},
  {n:17,act:'Gestión Ambiental',ind:'Capacitaciones al personal sobre manejo de residuos sólidos',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:18,act:'Gestión Ambiental',ind:'Planes de gestión de residuos sólidos elaborados/actualizados',u:'Plan',mv:'Plan aprobado por la DGANP'},
  {n:19,act:'Gestión Ambiental',ind:'Informes trimestrales de gestión de residuos sólidos',u:'Informe',mv:'4 informes trimestrales'},
  {eas:'EAS-4',lbl:'EAS-4: Salud y seguridad de la comunidad — Turismo y aprovechamiento'},
  {n:20,act:'Turismo',ind:'Capacitaciones en identificación de peligros/riesgos en rutas turísticas',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:21,act:'Turismo',ind:'Capacitaciones en primeros auxilios para emergencias turísticas',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:22,act:'Turismo',ind:'Señaléticas instaladas para prevenir accidentes en el ANP',u:'Señalética',mv:'Fotos de señaléticas instaladas'},
  {n:23,act:'Turismo',ind:'Planes de Sitio con medidas/normas de seguridad',u:'Plan de Sitio',mv:'Plan de Sitio aprobado'},
  {n:24,act:'Turismo',ind:'Capacitaciones a operadores de turismo sobre riesgos del ANP',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:25,act:'Turismo',ind:'Capacitaciones a visitantes para prevenir accidentes en el ANP',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {n:26,act:'Recursos Naturales',ind:'Planes de Manejo de Recursos con recomendaciones de seguridad',u:'Plan de Manejo',mv:'Plan aprobado'},
  {n:27,act:'Recursos Naturales',ind:'Capacitaciones a usuarios de aprovechamiento sobre medidas de seguridad',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {eas:'EAS-5',lbl:'EAS-5: Adquisición de tierras y restricciones sobre uso de la tierra'},
  {n:28,act:'Consulta y Participación',ind:'Talleres de consulta previa por cambio de zonificación o establecimiento de nuevas ANP',u:'Taller',mv:'Informe con lista de asistencia, fotos'},
  {n:29,act:'Consulta y Participación',ind:'Actas de reuniones descentralizadas con PI y comunidades (zonificación, Planes Maestros)',u:'Actas',mv:'Carpeta con actas de todas las reuniones'},
  {n:30,act:'Acciones Comunicativas',ind:'Actividades comunicativas en consulta previa (enfoque intercultural, intergeneracional, género)',u:'Acción',mv:'Fotos, flyers, links de publicación'},
  {eas:'EAS-7',lbl:'EAS-7: Pueblos indígenas / comunidades locales tradicionales'},
  {n:31,act:'Consulta y Participación',ind:'Informes del Mapa de Actores con identificación de PI y comunidades locales',u:'Informe semestral',mv:'Informe del Mapa de Actores'},
  {n:32,act:'Consulta y Participación',ind:'Actas de reuniones en espacios/mecanismos participativos con PI (CG, AdC, VC, GPV, ECA)',u:'Actas',mv:'Carpeta con actas de todas las reuniones'},
  {n:33,act:'Acciones Comunicativas',ind:'Actividades comunicativas con actores (enfoque intercultural, intergeneracional, género)',u:'Acción',mv:'Fotos, flyers, links de publicación'},
  {eas:'EAS-8',lbl:'EAS-8: Patrimonio cultural — Saberes ancestrales y PIACI'},
  {n:34,act:'Enfoque Intercultural',ind:'Informes de recopilación de saberes ancestrales',u:'Informe',mv:'Informe de recopilación'},
  {n:35,act:'Enfoque Intercultural',ind:'Plan de Contingencia Antropológica para PIACI aprobado e implementado',u:'Documento',mv:'Documento aprobado e implementado'},
  {n:36,act:'Enfoque Intercultural',ind:'Capacitaciones sobre enfoque intercultural al personal del ANP',u:'Capacitación',mv:'Lista de asistencia, fotos'},
  {eas:'EAS-10',lbl:'EAS-10: Participación de partes involucradas y divulgación de información'},
  {n:37,act:'Sistematización',ind:'Reportes de alerta de conflictos socioambientales en el ANP y ZA (RATCS)',u:'Reporte',mv:'Informe o Reporte'},
  {n:38,act:'Sistematización',ind:'Registros del MAQS (Mecanismo de Atención de Quejas, Consultas y Sugerencias)',u:'Reporte',mv:'Informe o Reporte MAQS'},
  {n:39,act:'Participación',ind:'Capacitaciones al personal en uso y gestión del MAQS',u:'Capacitación',mv:'Lista de asistencia, fotos'},
];

const inds = INDS.filter(d=>d.n);
let vals={}, mvVals={};
inds.forEach(d=>{vals[d.n]={meta:0,t1:0,t2:0,t3:0,t4:0}; mvVals[d.n]={link:'',fecha:''};});

// Timer
let startTime = Date.now();
setInterval(()=>{
  const s = Math.floor((Date.now()-startTime)/1000);
  const m = Math.floor(s/60), sec = s%60;
  document.getElementById('timer').textContent = `⏱ ${String(m).padStart(2,'0')}:${String(sec).padStart(2,'0')}`;
}, 1000);

// Populate ANP select
const sel = document.getElementById('anp_sel');
ANP_LIST.forEach(a=>{
  const o = document.createElement('option');
  o.value = a.c;
  o.textContent = a.n + ' (' + a.c + ')';
  sel.appendChild(o);
});

function setANP(codigo){
  const a = ANP_LIST.find(x=>x.c===codigo);
  if(!a) return;
  document.getElementById('anp-badge').textContent = a.n;
  document.getElementById('s0-status').textContent = 'ANP: ' + a.c;
  document.getElementById('s0-status').className = 'badge-ok';
  const cats = document.querySelectorAll('input[name=cat]');
  cats.forEach(c=>{ c.checked = c.value===a.cat; });
}

function goStep(i){
  document.querySelectorAll('.step').forEach((s,j)=>{
    s.classList.toggle('active',j===i);
    if(j<i) s.classList.add('done'); else s.classList.remove('done');
  });
  document.querySelectorAll('.sec').forEach((s,j)=>s.classList.toggle('active',j===i));
  if(i===1) renderMGAS();
  if(i===3){ renderMV(); updateExportInfo(); }
}

function renderMGAS(){
  const tbody = document.getElementById('mgas-tbody');
  tbody.innerHTML='';
  INDS.forEach(item=>{
    if(item.eas){
      const tr=document.createElement('tr');
      tr.className='eas-row';
      tr.innerHTML=`<td colspan="11">${item.lbl}</td>`;
      tbody.appendChild(tr); return;
    }
    const v=vals[item.n];
    const tot=(+v.t1||0)+(+v.t2||0)+(+v.t3||0)+(+v.t4||0);
    const meta=+v.meta||0;
    const pct=meta>0?Math.min(100,Math.round(tot/meta*100)):0;
    const tr=document.createElement('tr');
    tr.innerHTML=`
      <td class="tn">${item.n}</td>
      <td class="tact">${item.act}</td>
      <td class="tind">${item.ind}</td>
      <td class="tu">${item.u}</td>
      <td><input type="number" min="0" step="1" value="${v.meta||0}" onchange="upd(${item.n},'meta',this.value)"></td>
      <td><input type="number" min="0" step="1" value="${v.t1||0}" onchange="upd(${item.n},'t1',this.value)"></td>
      <td><input type="number" min="0" step="1" value="${v.t2||0}" onchange="upd(${item.n},'t2',this.value)"></td>
      <td><input type="number" min="0" step="1" value="${v.t3||0}" onchange="upd(${item.n},'t3',this.value)"></td>
      <td><input type="number" min="0" step="1" value="${v.t4||0}" onchange="upd(${item.n},'t4',this.value)"></td>
      <td class="tc" id="tot-${item.n}">${tot}</td>
      <td class="tc"><div class="pb"><div class="pb-bg"><div class="pb-fill" id="bar-${item.n}" style="width:${pct}%"></div></div><span class="pb-lbl" id="pct-${item.n}">${pct}%</span></div></td>`;
    tbody.appendChild(tr);
  });
  updateStats();
}

function renderMV(){
  const tbody=document.getElementById('mv-tbody');
  tbody.innerHTML='';
  inds.forEach(item=>{
    const mv=mvVals[item.n];
    const tr=document.createElement('tr');
    tr.innerHTML=`
      <td class="tn">${item.n}</td>
      <td class="tact">${item.act}</td>
      <td class="tind">${item.ind}</td>
      <td class="tu" style="font-size:10px;color:#666;">${item.mv}</td>
      <td><input type="text" class="mv-inp" placeholder="https://drive.google.com/..." value="${mv.link||''}" onchange="mvVals[${item.n}].link=this.value"></td>
      <td><input type="date" value="${mv.fecha||''}" onchange="mvVals[${item.n}].fecha=this.value"></td>`;
    tbody.appendChild(tr);
  });
}

function upd(n,campo,v){
  vals[n][campo]=parseFloat(v)||0;
  const vv=vals[n];
  const tot=(+vv.t1||0)+(+vv.t2||0)+(+vv.t3||0)+(+vv.t4||0);
  const meta=+vv.meta||0;
  const pct=meta>0?Math.min(100,Math.round(tot/meta*100)):0;
  const el=id=>document.getElementById(id);
  if(el('tot-'+n)) el('tot-'+n).textContent=tot;
  if(el('bar-'+n)) el('bar-'+n).style.width=pct+'%';
  if(el('pct-'+n)) el('pct-'+n).textContent=pct+'%';
  updateStats();
}

function updateStats(){
  let tMeta=0,tEjec=0;
  inds.forEach(d=>{
    tMeta+=(+vals[d.n].meta||0);
    tEjec+=(+vals[d.n].t1||0)+(+vals[d.n].t2||0)+(+vals[d.n].t3||0)+(+vals[d.n].t4||0);
  });
  const pct=tMeta>0?Math.round(tEjec/tMeta*100):0;
  document.getElementById('st-meta').textContent=tMeta;
  document.getElementById('st-ejec').textContent=tEjec;
  document.getElementById('st-pct').textContent=pct+'%';
  document.getElementById('gbar').style.width=pct+'%';
}

function updateExportInfo(){
  const anpSel=document.getElementById('anp_sel').value;
  const trim=document.getElementById('p_trim').value;
  const anio=document.getElementById('p_anio').value;
  if(anpSel&&trim&&anio){
    document.getElementById('export-info').textContent=`ANP: ${anpSel}  |  ${trim} Trimestre ${anio}`;
  }
}

function getPortada(){
  const cats=[...document.querySelectorAll('input[name=cat]:checked')].map(c=>c.value).join(', ');
  const anpSel=document.getElementById('anp_sel').value;
  const anpObj=ANP_LIST.find(a=>a.c===anpSel)||{};
  return {
    nombre:document.getElementById('p_nombre').value||'',
    codigo_proyecto:document.getElementById('p_codigo').value||'',
    anp:anpObj.n||anpSel,
    codigo_anp:anpSel,
    categoria:cats||anpObj.cat||'',
    anio:document.getElementById('p_anio').value||'',
    trimestre:document.getElementById('p_trim').value||'',
    entidad:document.getElementById('p_entidad').value||'',
    dependencia:document.getElementById('p_dep').value||'',
    periodo_desde:document.getElementById('p_desde').value||'',
    periodo_hasta:document.getElementById('p_hasta').value||'',
    jefe:document.getElementById('p_jefe').value||'',
    focal:document.getElementById('p_focal').value||'',
    responsable:document.getElementById('p_resp').value||'',
    fecha_elaboracion:document.getElementById('p_fecha').value||'',
    nro_reporte:document.getElementById('p_nro').value||'',
    version:document.getElementById('p_ver').value||'1.0',
  };
}

async function generarExcel(){
  const btn = document.getElementById('btn-export');
  btn.disabled = true;
  btn.textContent = '⏳ Generando...';
  const payload = {
    portada: getPortada(),
    ejecucion: vals,
    conclusiones: {
      sintesis:document.getElementById('c1').value||'',
      logros:document.getElementById('c2').value||'',
      lecciones:document.getElementById('c3').value||'',
      compromisos:document.getElementById('c4').value||'',
      recomendaciones:document.getElementById('c5').value||'',
    },
    medios: mvVals
  };
  try {
    const res = await fetch('/generar', {
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body: JSON.stringify(payload)
    });
    if(!res.ok) throw new Error('Error del servidor');
    const blob = await res.blob();
    const cd = res.headers.get('Content-Disposition')||'';
    const match = cd.match(/filename="?([^"]+)"?/);
    const filename = match ? match[1] : 'Reporte_MGAS.xlsx';
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href=url; a.download=filename; a.click();
    URL.revokeObjectURL(url);
    const toast = document.getElementById('toast');
    toast.style.display='block';
    setTimeout(()=>toast.style.display='none', 3000);
  } catch(e){
    alert('Error al generar el reporte: ' + e.message);
  }
  btn.disabled=false;
  btn.textContent='⬇ Descargar Reporte .xlsx';
}

renderMGAS();
</script>
</body>
</html>
