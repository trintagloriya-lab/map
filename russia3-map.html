<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<style>
* { margin:0; padding:0; box-sizing:border-box; }
body { background:#0d1b2a; font-family:'Segoe UI',sans-serif; overflow:hidden; }
svg { display:block; }
.region { cursor:pointer; transition:opacity .15s; }
.region:hover { opacity:.72; stroke:#fff !important; stroke-width:1.5 !important; }
.region.active { stroke:#fff !important; stroke-width:2 !important; filter:brightness(1.35); }

#tooltip {
  position:fixed; display:none; pointer-events:none; z-index:200;
  background:rgba(10,20,35,.97); border:1px solid #2d4a6a;
  padding:9px 14px; border-radius:9px; color:#e2e8f0; font-size:13px;
  max-width:270px; line-height:1.6;
}

#panel {
  position:fixed; top:16px; left:16px; z-index:100;
  background:rgba(10,20,35,.93); border:1px solid #2d4a6a;
  border-radius:12px; padding:16px 20px; width:260px;
}
#panel-pretitle { font-size:10px; text-transform:uppercase; letter-spacing:1.5px; color:#64748b; margin-bottom:10px; }
#region-name { font-size:16px; font-weight:600; color:#f1f5f9; min-height:20px; line-height:1.3; }
#tags { display:flex; flex-wrap:wrap; gap:5px; margin-top:8px; min-height:22px; }
.tag { display:inline-block; font-size:11px; padding:3px 9px; border-radius:20px; font-weight:500; }
#scores { margin-top:10px; }
.score-row { display:flex; align-items:center; gap:8px; margin:4px 0; }
.score-lbl { font-size:11px; color:#64748b; width:30px; flex-shrink:0; }
.cells { display:flex; gap:3px; }
.cell { width:20px; height:7px; border-radius:2px; transition:background .3s; }
.score-desc { font-size:11px; color:#94a3b8; margin-left:2px; }
#gap-badge {
  margin-top:10px; padding:6px 10px; border-radius:7px; font-size:12px;
  font-weight:600; display:none; line-height:1.5;
}
#extra { margin-top:8px; font-size:11.5px; color:#94a3b8; line-height:1.55; }

/* Mode toggle */
#mode-toggle {
  position:fixed; top:16px; right:16px; z-index:100;
  display:flex; background:rgba(10,20,35,.93); border:1px solid #2d4a6a; border-radius:10px; overflow:hidden;
}
.mbtn { padding:8px 13px; font-size:12px; cursor:pointer; color:#64748b; background:transparent; border:none; transition:all .2s; white-space:nowrap; }
.mbtn.on { background:#1e3a5f; color:#f1f5f9; font-weight:600; }

#legend {
  position:fixed; bottom:16px; left:16px; z-index:100;
  background:rgba(10,20,35,.93); border:1px solid #2d4a6a;
  border-radius:12px; padding:14px 18px; max-width:270px;
}
#legend h2 { font-size:10px; text-transform:uppercase; letter-spacing:1.5px; color:#64748b; margin-bottom:10px; }
.lrow { display:flex; align-items:flex-start; gap:9px; margin-bottom:7px; cursor:pointer; }
.lrow:hover .lswatch { transform:scale(1.25); }
.lswatch { width:13px; height:13px; border-radius:3px; flex-shrink:0; margin-top:2px; transition:transform .15s; }
.llabel { font-size:12px; color:#cbd5e1; line-height:1.4; }
.lsub { font-size:10px; color:#64748b; }

#zoom-wrap { position:fixed; bottom:16px; right:16px; z-index:100; display:flex; flex-direction:column; gap:6px; }
.zbtn { width:36px; height:36px; border-radius:8px; border:1px solid #2d4a6a; background:rgba(10,20,35,.93); color:#cbd5e1; font-size:18px; cursor:pointer; display:grid; place-items:center; transition:background .15s; }
.zbtn:hover { background:#1e3a5f; }

#loading { position:fixed; inset:0; display:grid; place-items:center; background:#0d1b2a; color:#64748b; z-index:300; }
.spinner { width:36px; height:36px; border:3px solid #1e3a5f; border-top-color:#3b82f6; border-radius:50%; animation:spin .8s linear infinite; margin:0 auto 12px; }
@keyframes spin { to { transform:rotate(360deg); } }

/* source note */
#src { position:fixed; bottom:6px; left:50%; transform:translateX(-50%); font-size:10px; color:#334155; z-index:50; white-space:nowrap; }
</style>
</head>
<body>

<div id="loading"><div style="text-align:center"><div class="spinner"></div>Загрузка карты…</div></div>
<svg id="map"></svg>
<div id="tooltip"></div>

<div id="panel">
  <div id="panel-pretitle">🗺 Карта России</div>
  <div id="region-name" style="color:#475569">Наведите на регион</div>
  <div id="tags"></div>
  <div id="scores"></div>
  <div id="gap-badge"></div>
  <div id="extra"></div>
</div>

<div id="mode-toggle">
  <button class="mbtn on" data-mode="gap">📊 НТР vs ИИ</button>
  <button class="mbtn" data-mode="ai">🤖 Уровень ИИ</button>
  <button class="mbtn" data-mode="district">🗂 Округа</button>
</div>

<div id="legend">
  <h2 id="legend-title">Соотношение НТР и ИИ</h2>
  <div id="legend-items"></div>
</div>

<div id="zoom-wrap">
  <button class="zbtn" id="z-in">+</button>
  <button class="zbtn" id="z-out">−</button>
  <button class="zbtn" id="z-reset" style="font-size:15px">⌂</button>
</div>

<div id="src">Источники: Нац. рейтинг НТР Минобрнауки 2024 · Рейтинг РИА Рейтинг 2024 · РРИИ НИУ ВШЭ 2024</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/7.8.5/d3.min.js"></script>
<script>
// ─── Core data: ai 1-4, ntr 1-4 ──────────────────────────────────────────────
// НТР: Национальный рейтинг НТР Минобрнауки 2024 + РИА Рейтинг 2024
// ИИ:  РРИИ НИУ ВШЭ 2024, Руссофт 2024, рейтинг цифровизации регионов
const RD = {
  // NTR-4 (Топ-10 Минобрнауки 2024)
  'Москва':{ ai:4,ntr:4 }, 'Санкт-Петербург':{ ai:4,ntr:4 },
  'Республика Татарстан':{ ai:4,ntr:4 }, 'Нижегородская область':{ ai:4,ntr:4 },
  'Новосибирская область':{ ai:4,ntr:4 }, 'Томская область':{ ai:3,ntr:4 },
  'Свердловская область':{ ai:3,ntr:4 }, 'Московская область':{ ai:3,ntr:4 },
  'Самарская область':{ ai:3,ntr:4 }, 'Республика Башкортостан':{ ai:2,ntr:4 },
  // NTR-3 (позиции 11-28)
  'Красноярский край':{ ai:3,ntr:3 }, 'Иркутская область':{ ai:2,ntr:3 },
  'Пермский край':{ ai:3,ntr:3 }, 'Ростовская область':{ ai:3,ntr:3 },
  'Краснодарский край':{ ai:3,ntr:3 }, 'Тюменская область':{ ai:2,ntr:3 },
  'Ханты-Мансийский автономный округ — Югра':{ ai:3,ntr:3 },
  'Кемеровская область':{ ai:2,ntr:3 }, 'Воронежская область':{ ai:2,ntr:3 },
  'Саратовская область':{ ai:2,ntr:3 }, 'Омская область':{ ai:2,ntr:3 },
  'Ярославская область':{ ai:2,ntr:3 }, 'Белгородская область':{ ai:2,ntr:3 },
  'Ленинградская область':{ ai:3,ntr:3 }, 'Челябинская область':{ ai:1,ntr:3 },
  'Калужская область':{ ai:3,ntr:3 }, 'Ульяновская область':{ ai:3,ntr:3 },
  'Тверская область':{ ai:2,ntr:3 },
  // NTR-2 (позиции 29-65)
  'Хабаровский край':{ ai:2,ntr:2 }, 'Приморский край':{ ai:2,ntr:2 },
  'Оренбургская область':{ ai:2,ntr:2 }, 'Пензенская область':{ ai:1,ntr:2 },
  'Рязанская область':{ ai:2,ntr:2 }, 'Тульская область':{ ai:2,ntr:2 },
  'Владимирская область':{ ai:2,ntr:2 }, 'Липецкая область':{ ai:2,ntr:2 },
  'Калининградская область':{ ai:2,ntr:2 }, 'Архангельская область':{ ai:2,ntr:2 },
  'Мурманская область':{ ai:2,ntr:2 }, 'Вологодская область':{ ai:1,ntr:2 },
  'Курская область':{ ai:1,ntr:2 }, 'Новгородская область':{ ai:1,ntr:2 },
  'Псковская область':{ ai:1,ntr:2 }, 'Республика Карелия':{ ai:1,ntr:2 },
  'Алтайский край':{ ai:1,ntr:2 }, 'Республика Хакасия':{ ai:1,ntr:2 },
  'Удмуртская Республика':{ ai:1,ntr:2 }, 'Чувашская Республика':{ ai:2,ntr:2 },
  'Республика Марий Эл':{ ai:1,ntr:2 }, 'Республика Саха (Якутия)':{ ai:2,ntr:2 },
  'Амурская область':{ ai:1,ntr:2 }, 'Тамбовская область':{ ai:1,ntr:2 },
  'Орловская область':{ ai:1,ntr:2 }, 'Смоленская область':{ ai:1,ntr:2 },
  'Костромская область':{ ai:1,ntr:2 }, 'Ивановская область':{ ai:1,ntr:2 },
  'Ямало-Ненецкий автономный округ':{ ai:2,ntr:2 },
  'Забайкальский край':{ ai:1,ntr:2 }, 'Республика Мордовия':{ ai:1,ntr:2 },
  'Республика Коми':{ ai:1,ntr:2 }, 'Брянская область':{ ai:1,ntr:2 },
  'Кировская область':{ ai:1,ntr:2 }, 'Волгоградская область':{ ai:2,ntr:2 },
  'Астраханская область':{ ai:1,ntr:2 }, 'Ставропольский край':{ ai:1,ntr:2 },
  'Курганская область':{ ai:1,ntr:2 },
  // NTR-1 (нижний квартиль)
  'Республика Алтай':{ ai:1,ntr:1 }, 'Республика Тыва':{ ai:1,ntr:1 },
  'Республика Калмыкия':{ ai:1,ntr:1 }, 'Республика Адыгея':{ ai:1,ntr:1 },
  'Карачаево-Черкесская Республика':{ ai:1,ntr:1 },
  'Кабардино-Балкарская Республика':{ ai:1,ntr:1 },
  'Республика Ингушетия':{ ai:1,ntr:1 }, 'Чеченская Республика':{ ai:1,ntr:1 },
  'Республика Дагестан':{ ai:1,ntr:1 },
  'Республика Северная Осетия — Алания':{ ai:1,ntr:1 },
  'Еврейская автономная область':{ ai:1,ntr:1 },
  'Чукотский автономный округ':{ ai:1,ntr:1 },
  'Камчатский край':{ ai:1,ntr:1 }, 'Магаданская область':{ ai:1,ntr:1 },
  'Сахалинская область':{ ai:1,ntr:1 },
  'Республика Бурятия':{ ai:2,ntr:1 },   // ИИ опережает НТР
  'Ненецкий автономный округ':{ ai:1,ntr:1 },
  'Республика Крым':{ ai:1,ntr:1 }, 'Севастополь':{ ai:1,ntr:1 },
};
function rd(name) { return RD[name] || { ai:1, ntr:1 }; }

// ─── AI labels ────────────────────────────────────────────────────────────────
const AI_L = {
  4:{ label:'🥇 Лидеры ИИ', sub:'Нац. центры компетенций', color:'#22d3ee', tc:'#cffafe' },
  3:{ label:'🥈 Активные', sub:'Выраженная ИИ-активность', color:'#3b82f6', tc:'#dbeafe' },
  2:{ label:'🥉 Развивающиеся', sub:'Отдельные ИИ-проекты', color:'#8b5cf6', tc:'#ede9fe' },
  1:{ label:'🔵 Начальный этап', sub:'Цифровая инфраструктура', color:'#334155', tc:'#cbd5e1' },
};
const NTR_L = {
  4:'Топ-10 НТР (лидер)', 3:'Выше среднего', 2:'Ниже среднего', 1:'Слабая база',
};

// ─── Gap categories ───────────────────────────────────────────────────────────
// Для каждого региона: gap = ai - ntr
// synergy:  оба ≥ 3 — «Синергия»
// ntr_gap:  ntr ≥ 3, ai < 3 — «Нераскрытый потенциал»
// ai_gap:   ai > ntr (при хотя бы одном < 3) — «ИИ-форсаж»
// balanced: прочие — «В начале пути»
const GAP_CATS = {
  synergy: { label:'🟢 Синергия', sub:'НТР ≥3 и ИИ ≥3 — взаимно развиты', color:'#14b8a6', tc:'#ccfbf1' },
  ntr_gap: { label:'🟠 Нераскрытый потенциал', sub:'НТР ≥3, но ИИ отстаёт', color:'#f97316', tc:'#ffedd5' },
  ai_gap:  { label:'🟣 ИИ-форсаж', sub:'ИИ опережает научную базу', color:'#a855f7', tc:'#f3e8ff' },
  balanced:{ label:'⚫ В начале пути', sub:'Оба показателя невысоки', color:'#1e3a5f', tc:'#94a3b8' },
};
// Градиент для ntr_gap по величине разрыва
const NTR_GAP_COLORS = { 1:'#fb923c', 2:'#f97316', 3:'#c2410c' };

function getGapCat(ai, ntr) {
  if (ai >= 3 && ntr >= 3) return 'synergy';
  if (ntr >= 3 && ai < 3)  return 'ntr_gap';
  if (ai > ntr)            return 'ai_gap';
  return 'balanced';
}
function gapColor(name) {
  const { ai, ntr } = rd(name);
  const cat = getGapCat(ai, ntr);
  if (cat === 'ntr_gap') return NTR_GAP_COLORS[ntr - ai] || '#f97316';
  return GAP_CATS[cat].color;
}

// ─── Districts ────────────────────────────────────────────────────────────────
const DIST = {
  'Центральный':{ color:'#e05252',tc:'#fee2e2' },
  'Северо-Западный':{ color:'#3b82f6',tc:'#dbeafe' },
  'Южный':{ color:'#22c55e',tc:'#dcfce7' },
  'Северо-Кавказский':{ color:'#f59e0b',tc:'#fef3c7' },
  'Приволжский':{ color:'#a855f7',tc:'#f3e8ff' },
  'Уральский':{ color:'#14b8a6',tc:'#ccfbf1' },
  'Сибирский':{ color:'#f97316',tc:'#ffedd5' },
  'Дальневосточный':{ color:'#6366f1',tc:'#e0e7ff' },
};
const R2D = {
  'Белгородская область':'Центральный','Брянская область':'Центральный','Владимирская область':'Центральный','Воронежская область':'Центральный','Ивановская область':'Центральный','Калужская область':'Центральный','Костромская область':'Центральный','Курская область':'Центральный','Липецкая область':'Центральный','Московская область':'Центральный','Москва':'Центральный','Орловская область':'Центральный','Рязанская область':'Центральный','Смоленская область':'Центральный','Тамбовская область':'Центральный','Тверская область':'Центральный','Тульская область':'Центральный','Ярославская область':'Центральный',
  'Республика Карелия':'Северо-Западный','Республика Коми':'Северо-Западный','Архангельская область':'Северо-Западный','Вологодская область':'Северо-Западный','Калининградская область':'Северо-Западный','Ленинградская область':'Северо-Западный','Мурманская область':'Северо-Западный','Новгородская область':'Северо-Западный','Псковская область':'Северо-Западный','Санкт-Петербург':'Северо-Западный','Ненецкий автономный округ':'Северо-Западный',
  'Республика Адыгея':'Южный','Республика Калмыкия':'Южный','Краснодарский край':'Южный','Астраханская область':'Южный','Волгоградская область':'Южный','Ростовская область':'Южный','Республика Крым':'Южный','Севастополь':'Южный',
  'Республика Дагестан':'Северо-Кавказский','Республика Ингушетия':'Северо-Кавказский','Кабардино-Балкарская Республика':'Северо-Кавказский','Карачаево-Черкесская Республика':'Северо-Кавказский','Республика Северная Осетия — Алания':'Северо-Кавказский','Чеченская Республика':'Северо-Кавказский','Ставропольский край':'Северо-Кавказский',
  'Республика Башкортостан':'Приволжский','Республика Марий Эл':'Приволжский','Республика Мордовия':'Приволжский','Республика Татарстан':'Приволжский','Удмуртская Республика':'Приволжский','Чувашская Республика':'Приволжский','Пермский край':'Приволжский','Кировская область':'Приволжский','Нижегородская область':'Приволжский','Оренбургская область':'Приволжский','Пензенская область':'Приволжский','Самарская область':'Приволжский','Саратовская область':'Приволжский','Ульяновская область':'Приволжский',
  'Курганская область':'Уральский','Свердловская область':'Уральский','Тюменская область':'Уральский','Челябинская область':'Уральский','Ханты-Мансийский автономный округ — Югра':'Уральский','Ямало-Ненецкий автономный округ':'Уральский',
  'Республика Алтай':'Сибирский','Республика Тыва':'Сибирский','Республика Хакасия':'Сибирский','Алтайский край':'Сибирский','Красноярский край':'Сибирский','Иркутская область':'Сибирский','Кемеровская область':'Сибирский','Новосибирская область':'Сибирский','Омская область':'Сибирский','Томская область':'Сибирский',
  'Республика Бурятия':'Дальневосточный','Республика Саха (Якутия)':'Дальневосточный','Забайкальский край':'Дальневосточный','Камчатский край':'Дальневосточный','Приморский край':'Дальневосточный','Хабаровский край':'Дальневосточный','Амурская область':'Дальневосточный','Магаданская область':'Дальневосточный','Сахалинская область':'Дальневосточный','Еврейская автономная область':'Дальневосточный','Чукотский автономный округ':'Дальневосточный',
};

// ─── AI Facts ─────────────────────────────────────────────────────────────────
const FACTS = {
  'Москва':'Нац. лидер ИИ: 95/100 в рейтинге цифровизации. Система компьютерного зрения на городских камерах, платформа больших данных, премия «Лидеры ИИ».',
  'Санкт-Петербург':'Топ-2 по НТР и ИИ. Крупнейший R&D-центр страны, экспорт ИКТ — $620 млн (2023), более 1 000 ИТ-компаний.',
  'Республика Татарстан':'Центр компетенций по ИИ в Казани (совм. с КФУ). Особая экономическая зона для ИТ. Лидер по числу вакансий в software.',
  'Новосибирская область':'Академгородок СО РАН и Технопарк НГУ — ядро ИИ-разработок. Топ-3 по НТР, лидер в машинном обучении в медицине и биотехе.',
  'Нижегородская область':'Топ-3 рейтинга инновационного развития ВШЭ 2024. Лидер по экспорту знаний и мерам поддержки ИТ-бизнеса.',
  'Свердловская область':'Топ-4 software-индустрии (оборот 59,8 млрд руб., 2023). Уральский кластер кибербезопасности и промышленного ИИ.',
  'Красноярский край':'ИИ-видеоаналитика: время поиска пропавших сократилось с 20 дней до 7 минут. Проекты в горнодобыче и ЖКХ.',
  'Томская область':'Топ-3 в блоке «Научно-технический потенциал» РРИИ-2024. Один из ведущих академических центров страны.',
  'Ханты-Мансийский автономный округ — Югра':'Активное внедрение ИИ в нефтегазовой отрасли. +14 позиций в рейтинге инновационного развития ВШЭ 2024.',
  'Республика Башкортостан':'Несмотря на мощный НТ-потенциал (топ-4 НТР), ИИ-активность пока в стадии отдельных проектов — типичный «нераскрытый потенциал».',
  'Челябинская область':'Крупный промышленный регион с развитой наукой (топ-3 НТР Урала), однако ИИ-проекты только формируются — наибольший разрыв в регионе.',
  'Республика Бурятия':'Единственный явный случай «ИИ-форсажа»: благодаря федеральной программе «Цифровая экономика» ИИ-активность превышает научную базу региона.',
};

// ─── State ────────────────────────────────────────────────────────────────────
let mode = 'gap', activeEl = null;

// ─── Color dispatch ───────────────────────────────────────────────────────────
function getColor(name) {
  if (mode === 'gap') return gapColor(name);
  if (mode === 'ai')  return AI_L[rd(name).ai].color;
  const d = R2D[name]; return d ? DIST[d].color : '#2d4a6a';
}

// ─── Score bar HTML ───────────────────────────────────────────────────────────
function bars(val, color) {
  return Array.from({length:4}, (_,i) =>
    `<div class="cell" style="background:${i<val ? color : '#1e3a5f'}"></div>`
  ).join('');
}

// ─── Panel update ─────────────────────────────────────────────────────────────
function updatePanel(name) {
  const { ai, ntr } = rd(name);
  document.getElementById('region-name').textContent = name;
  document.getElementById('region-name').style.color = '#f1f5f9';

  // Tags
  const tagEl = document.getElementById('tags');
  tagEl.innerHTML = '';
  const addTag = (txt, bg, tc) => {
    const t = document.createElement('span');
    t.className = 'tag';
    t.style.background = bg + '33'; t.style.color = tc;
    t.textContent = txt; tagEl.appendChild(t);
  };

  const aiInfo = AI_L[ai];
  addTag(aiInfo.label, aiInfo.color, aiInfo.tc);
  const dist = R2D[name];
  if (dist) addTag(dist + ' ФО', DIST[dist].color, DIST[dist].tc);

  // Scores (always shown)
  document.getElementById('scores').innerHTML = `
    <div class="score-row">
      <span class="score-lbl">НТР</span>
      <div class="cells">${bars(ntr,'#f97316')}</div>
      <span class="score-desc">${NTR_L[ntr]}</span>
    </div>
    <div class="score-row">
      <span class="score-lbl">ИИ</span>
      <div class="cells">${bars(ai, aiInfo.color)}</div>
      <span class="score-desc">${aiInfo.sub}</span>
    </div>`;

  // Gap badge
  const badge = document.getElementById('gap-badge');
  if (mode === 'gap') {
    const cat = getGapCat(ai, ntr);
    const ci = GAP_CATS[cat];
    const gap = ai - ntr;
    let gapText = gap === 0 ? 'Баланс' : gap > 0 ? `ИИ опережает НТР на ${gap} ур.` : `НТР опережает ИИ на ${Math.abs(gap)} ур.`;
    badge.style.display = 'block';
    badge.style.background = ci.color + '22';
    badge.style.color = ci.tc;
    badge.style.borderLeft = `3px solid ${ci.color}`;
    badge.innerHTML = `${ci.label}<br><span style="font-weight:400;font-size:11px">${gapText}</span>`;
  } else {
    badge.style.display = 'none';
  }

  // Fact
  document.getElementById('extra').textContent = FACTS[name] || '';
}

function clearPanel() {
  document.getElementById('region-name').textContent = 'Наведите на регион';
  document.getElementById('region-name').style.color = '#475569';
  document.getElementById('tags').innerHTML = '';
  document.getElementById('scores').innerHTML = '';
  document.getElementById('gap-badge').style.display = 'none';
  document.getElementById('extra').textContent = '';
}

// ─── Legend ───────────────────────────────────────────────────────────────────
function buildLegend() {
  const el = document.getElementById('legend-items');
  el.innerHTML = '';
  let items = [];
  if (mode === 'gap') {
    document.getElementById('legend-title').textContent = 'Соотношение НТР и ИИ';
    // Show ntr_gap gradient
    items = [
      { key:'synergy',  color: GAP_CATS.synergy.color, label: GAP_CATS.synergy.label, sub: GAP_CATS.synergy.sub },
      { key:'ntr_gap3', color:'#c2410c', label:'🟠 Нераскрытый потенциал ▲▲', sub:'НТР выше ИИ на 3 ур.' },
      { key:'ntr_gap2', color:'#f97316', label:'🟠 Нераскрытый потенциал ▲▲', sub:'НТР выше ИИ на 2 ур.' },
      { key:'ntr_gap1', color:'#fb923c', label:'🟠 Нераскрытый потенциал ▲',  sub:'НТР выше ИИ на 1 ур.' },
      { key:'ai_gap',   color: GAP_CATS.ai_gap.color,  label: GAP_CATS.ai_gap.label,  sub: GAP_CATS.ai_gap.sub },
      { key:'balanced', color: GAP_CATS.balanced.color, label: GAP_CATS.balanced.label, sub: GAP_CATS.balanced.sub },
    ];
  } else if (mode === 'ai') {
    document.getElementById('legend-title').textContent = 'Уровень развития ИИ';
    items = [4,3,2,1].map(k => ({ key:'ai'+k, color: AI_L[k].color, label: AI_L[k].label, sub: AI_L[k].sub }));
  } else {
    document.getElementById('legend-title').textContent = 'Федеральные округа';
    items = Object.entries(DIST).map(([name,{color}]) => ({ key:name, color, label:name, sub:'', district:name }));
  }
  items.forEach(item => {
    const row = document.createElement('div');
    row.className = 'lrow';
    row.innerHTML = `<div class="lswatch" style="background:${item.color}"></div>
      <div><div class="llabel">${item.label.replace('🟠 Нераскрытый потенциал ▲▲','🟠 Нераскрытый потенциал').replace('🟠 Нераскрытый потенциал ▲','🟠 Нераскрытый потенциал (умер.)')}</div>
      ${item.sub ? `<div class="lsub">${item.sub}</div>` : ''}</div>`;
    el.appendChild(row);

    // Hover highlight
    row.addEventListener('mouseenter', () => {
      d3.selectAll('.region').style('opacity', d => {
        const nm = d.properties.name;
        const { ai, ntr } = rd(nm);
        if (mode === 'gap') {
          const cat = getGapCat(ai, ntr);
          if (item.key === 'ntr_gap1') return cat === 'ntr_gap' && ntr - ai === 1 ? 1 : 0.1;
          if (item.key === 'ntr_gap2') return cat === 'ntr_gap' && ntr - ai === 2 ? 1 : 0.1;
          if (item.key === 'ntr_gap3') return cat === 'ntr_gap' && ntr - ai === 3 ? 1 : 0.1;
          return cat === item.key ? 1 : 0.1;
        } else if (mode === 'ai') {
          return ai === parseInt(item.key.replace('ai','')) ? 1 : 0.1;
        } else {
          return R2D[nm] === item.district ? 1 : 0.1;
        }
      });
    });
    row.addEventListener('mouseleave', () => d3.selectAll('.region').style('opacity', 1));
  });
}

buildLegend();

// ─── Mode toggle ──────────────────────────────────────────────────────────────
document.querySelectorAll('.mbtn').forEach(btn => {
  btn.addEventListener('click', () => {
    mode = btn.dataset.mode;
    document.querySelectorAll('.mbtn').forEach(b => b.classList.toggle('on', b === btn));
    d3.selectAll('.region').attr('fill', d => getColor(d.properties.name));
    buildLegend();
    clearPanel();
  });
});

// ─── D3 setup ─────────────────────────────────────────────────────────────────
const W = window.innerWidth, H = window.innerHeight;
const svg = d3.select('#map').attr('width', W).attr('height', H);
const g = svg.append('g');
const proj = d3.geoMercator().center([100,63]).scale(Math.min(W,H)*.72).translate([W/2, H/2]);
const path = d3.geoPath().projection(proj);
const zoom = d3.zoom().scaleExtent([0.4,10]).on('zoom', e => g.attr('transform', e.transform));
svg.call(zoom);
document.getElementById('z-in').onclick    = () => svg.transition().call(zoom.scaleBy, 1.6);
document.getElementById('z-out').onclick   = () => svg.transition().call(zoom.scaleBy, 1/1.6);
document.getElementById('z-reset').onclick = () => svg.transition().duration(600).call(zoom.transform, d3.zoomIdentity);

const tip = document.getElementById('tooltip');

// ─── Load GeoJSON ─────────────────────────────────────────────────────────────
fetch('https://raw.githubusercontent.com/codeforamerica/click_that_hood/master/public/data/russia.geojson')
  .then(r => { if (!r.ok) throw new Error(); return r.json(); })
  .then(geo => {
    document.getElementById('loading').style.display = 'none';

    g.selectAll('.region').data(geo.features).join('path')
      .attr('class','region')
      .attr('d', path)
      .attr('fill', d => getColor(d.properties.name))
      .attr('stroke','#0d1b2a')
      .attr('stroke-width', 0.4)
      .on('mousemove', function(e, d) {
        const nm = d.properties.name || '—';
        const { ai, ntr } = rd(nm);
        const cat = getGapCat(ai, ntr);
        const aInfo = AI_L[ai];
        const dist = R2D[nm];
        tip.style.display = 'block';
        tip.style.left = (e.clientX + 16) + 'px';
        tip.style.top  = (e.clientY - 12) + 'px';
        tip.innerHTML = `<strong>${nm}</strong><br>
          НТР <strong>${ntr}</strong>/4 · ИИ <strong>${ai}</strong>/4 · разрыв <strong>${ai - ntr > 0 ? '+' : ''}${ai - ntr}</strong><br>
          <span style="color:${GAP_CATS[cat].color}">${GAP_CATS[cat].label}</span>
          ${dist ? `<br><span style="color:#475569;font-size:11px">${dist} ФО</span>` : ''}`;
        updatePanel(nm);
      })
      .on('mouseleave', () => { tip.style.display = 'none'; })
      .on('click', function(e, d) {
        if (activeEl) d3.select(activeEl).classed('active', false);
        if (activeEl === this) { activeEl = null; clearPanel(); return; }
        d3.select(this).classed('active', true);
        activeEl = this;
        const [[x0,y0],[x1,y1]] = path.bounds(d);
        const sc = Math.min(8, 0.85/Math.max((x1-x0)/W,(y1-y0)/H));
        svg.transition().duration(700).call(
          zoom.transform, d3.zoomIdentity.translate(W/2,H/2).scale(sc).translate(-(x0+x1)/2,-(y0+y1)/2));
        e.stopPropagation();
      });

    svg.on('click', () => {
      if (activeEl) { d3.select(activeEl).classed('active', false); activeEl = null; }
      clearPanel();
    });
  })
  .catch(() => {
    document.getElementById('loading').innerHTML = '<div style="color:#ef4444">Ошибка загрузки карты.</div>';
  });
</script>
</body>
</html>
