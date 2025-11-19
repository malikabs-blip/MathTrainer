
<!DOCTYPE html>
<html lang="kk">
<head>
<meta charset="UTF-8">
<title>AminaMath AI – Math Trainer (6-сынып)</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
:root {
  --bg: #020617;
  --card: #020617;
  --accent: #38bdf8;
  --text: #e5e7eb;
  --muted: #9ca3af;
  --danger: #f97373;
  --success: #4ade80;
  --border: rgba(148,163,184,0.35);
}

* { box-sizing: border-box; }

body {
  margin: 0;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  background: radial-gradient(circle at top, #1e293b 0, #020617 55%, #020617 100%);
  color: var(--text);
  min-height: 100vh;
  display: flex;
  align-items: stretch;
  justify-content: center;
  padding: 16px;
}

.app-shell {
  width: 100%;
  max-width: 1120px;
  background: linear-gradient(135deg, rgba(15,23,42,0.98), rgba(8,47,73,0.95));
  border-radius: 24px;
  border: 1px solid var(--border);
  box-shadow:
    0 18px 45px rgba(15,23,42,0.7),
    0 0 0 1px rgba(15,23,42,0.8);
  overflow: hidden;
  display: grid;
  grid-template-columns: minmax(0, 1.1fr) minmax(0, 0.9fr);
}

/* Mobile */
@media (max-width: 840px) {
  body { padding: 8px; }
  .app-shell {
    grid-template-columns: minmax(0, 1fr);
    border-radius: 18px;
  }
  .left-pane, .right-pane {
    padding: 16px 14px;
  }
  .left-pane {
    border-right: none;
    border-bottom: 1px solid rgba(148,163,184,0.3);
  }
  .app-title { font-size: 20px; }
  #task { font-size: 18px; }
  .graphic-canvas { height: 140px; }
}

.left-pane {
  padding: 20px 22px 20px 22px;
  border-right: 1px solid rgba(148,163,184,0.3);
}

.app-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 11px;
  padding: 4px 9px;
  border-radius: 999px;
  background: rgba(15,23,42,0.8);
  border: 1px solid rgba(148,163,184,0.4);
  color: var(--muted);
}

.app-badge-dot {
  width: 7px;
  height: 7px;
  border-radius: 999px;
  background: var(--accent);
  box-shadow: 0 0 8px rgba(56,189,248,0.9);
}

.app-title {
  margin: 12px 0 4px;
  font-size: 22px;
  font-weight: 650;
  letter-spacing: 0.02em;
  display: flex;
  align-items: center;
  gap: 8px;
}

.app-title span.logo {
  width: 30px;
  height: 30px;
  border-radius: 12px;
  background: radial-gradient(circle at 30% 20%, #e0f2fe 0, #38bdf8 30%, #0ea5e9 60%, #0369a1 100%);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 18px rgba(56,189,248,0.8);
  flex-shrink: 0;
}

.app-subtitle {
  font-size: 13px;
  color: var(--muted);
  margin-bottom: 16px;
}

.row {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  align-items: center;
  margin-bottom: 14px;
}

.label {
  font-size: 12px;
  color: var(--muted);
}

select {
  background: rgba(15,23,42,0.9);
  border-radius: 999px;
  border: 1px solid rgba(148,163,184,0.6);
  padding: 8px 12px;
  color: var(--text);
  font-size: 13px;
  outline: none;
}

select:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 1px rgba(56,189,248,0.4);
}

button {
  border-radius: 999px;
  border: none;
  padding: 9px 16px;
  font-size: 13px;
  cursor: pointer;
  font-weight: 500;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  transition: transform 0.08s ease, box-shadow 0.08s ease, background 0.12s ease;
}

.btn-primary {
  background: linear-gradient(135deg, #38bdf8, #0ea5e9);
  color: #0b1120;
  box-shadow:
    0 0 0 1px rgba(8,47,73,0.8),
    0 8px 20px rgba(56,189,248,0.35);
}

.btn-primary:hover {
  transform: translateY(-1px);
  box-shadow:
    0 0 0 1px rgba(8,47,73,0.9),
    0 10px 26px rgba(56,189,248,0.45);
}

.btn-ghost {
  background: transparent;
  border: 1px solid rgba(148,163,184,0.5);
  color: var(--muted);
}

.btn-ghost:hover {
  background: rgba(15,23,42,0.8);
}

.pill {
  font-size: 10px;
  padding: 3px 8px;
  border-radius: 999px;
  background: rgba(15,23,42,0.85);
  border: 1px solid rgba(148,163,184,0.45);
  color: var(--muted);
}

/* TASK CARD */

.task-card {
  margin-top: 14px;
  padding: 16px 16px 14px;
  border-radius: 16px;
  background: radial-gradient(circle at top left, rgba(56,189,248,0.18), rgba(15,23,42,0.98));
  border: 1px solid rgba(148,163,184,0.35);
  position: relative;
  overflow: hidden;
}

.task-chip {
  font-size: 11px;
  padding: 4px 9px;
  border-radius: 999px;
  background: rgba(15,23,42,0.9);
  border: 1px solid rgba(148,163,184,0.4);
  color: var(--muted);
  display: inline-flex;
  align-items: center;
  gap: 6px;
}

.task-chip-dot {
  width: 6px;
  height: 6px;
  border-radius: 999px;
  background: #22c55e;
  box-shadow: 0 0 8px rgba(34,197,94,0.7);
}

#task {
  margin-top: 14px;
  font-size: 20px;
  font-weight: 600;
}

/* Answer row */

.answer-row {
  margin-top: 14px;
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  align-items: center;
}

input[type="text"] {
  background: rgba(15,23,42,0.95);
  border-radius: 999px;
  border: 1px solid rgba(148,163,184,0.65);
  padding: 8px 12px;
  color: var(--text);
  font-size: 14px;
  min-width: 130px;
  outline: none;
}

input[type="text"]:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 1px rgba(56,189,248,0.4);
}

#result {
  margin-top: 8px;
  font-size: 13px;
}

.result-ok { color: var(--success); }
.result-bad { color: var(--danger); }

/* RIGHT PANE */

.right-pane {
  position: relative;
  padding: 20px 20px 20px 20px;
  background: radial-gradient(circle at top right, rgba(56,189,248,0.22), #020617);
}

.section-title {
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.05em;
  color: var(--muted);
  text-transform: uppercase;
}

.theory-box {
  margin-top: 10px;
  padding: 14px 12px 14px;
  border-radius: 16px;
  background: rgba(15,23,42,0.9);
  border: 1px solid rgba(148,163,184,0.5);
  font-size: 13px;
}

.theory-title {
  font-weight: 600;
  margin-bottom: 4px;
  color: #e0f2fe;
}

.theory-body {
  color: var(--muted);
  line-height: 1.5;
}

.example {
  margin-top: 6px;
  padding: 8px 10px;
  border-radius: 12px;
  background: rgba(15,23,42,0.9);
  border: 1px dashed rgba(148,163,184,0.7);
  font-size: 12px;
}

/* Mini tags */

.topic-meta {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 8px;
}

.tag {
  font-size: 10px;
  padding: 3px 7px;
  border-radius: 999px;
  background: rgba(15,23,42,0.8);
  border: 1px solid rgba(148,163,184,0.5);
  color: var(--muted);
}

/* GRAPHIC AREA */

.graphic-card {
  margin-top: 14px;
  padding: 12px;
  border-radius: 16px;
  background: radial-gradient(circle at top left, rgba(56,189,248,0.16), rgba(15,23,42,0.96));
  border: 1px solid rgba(148,163,184,0.4);
  font-size: 12px;
  color: var(--muted);
}

.graphic-title {
  font-size: 12px;
  font-weight: 600;
  margin-bottom: 2px;
  color: #e5e7eb;
}

.graphic-canvas {
  margin-top: 8px;
  border-radius: 12px;
  background: radial-gradient(circle at center, rgba(15,23,42,0.9), #020617);
  border: 1px solid rgba(30,64,175,0.7);
  position: relative;
  overflow: hidden;
  height: 170px;
}

.grid-lines {
  position: absolute;
  inset: 0;
  background-image: linear-gradient(to right, rgba(30,64,175,0.4) 1px, transparent 1px),
                    linear-gradient(to bottom, rgba(30,64,175,0.4) 1px, transparent 1px);
  background-size: 22px 22px;
  opacity: 0.5;
}

.axis-x, .axis-y {
  position: absolute;
  background: rgba(248,250,252,0.9);
}

.axis-x {
  height: 1px;
  left: 0;
  right: 0;
  top: 50%;
}

.axis-y {
  width: 1px;
  top: 0;
  bottom: 0;
  left: 50%;
}

.point {
  position: absolute;
  width: 8px;
  height: 8px;
  border-radius: 999px;
  background: #f97316;
  box-shadow: 0 0 10px rgba(249,115,22,0.9);
  transform: translate(-50%, -50%);
}

.point-label {
  position: absolute;
  font-size: 11px;
  color: #e5e7eb;
  transform: translate(-50%, -140%);
}

/* ORB */

.orb {
  position: absolute;
  width: 160px;
  height: 160px;
  border-radius: 999px;
  background: radial-gradient(circle at 30% 20%, rgba(56,189,248,0.8), transparent 55%);
  top: -40px;
  right: -60px;
  opacity: 0.28;
  filter: blur(1px);
  pointer-events: none;
}
</style>
</head>
<body>
<div class="app-shell">
  <div class="left-pane">
    <div class="app-badge">
      <div class="app-badge-dot"></div>
      AminaMath AI · 6-сынып
    </div>

    <div class="app-title">
      <span class="logo">AI</span>
      <span>AminaMath AI – Math Trainer</span>
    </div>
    <div class="app-subtitle">
      6-сыныпқа арналған ақылды математикалық жаттықтырғыш: ережені оқыңыз, мысалды көріңіз, содан кейін өзіңіз есеп шығарып көріңіз.
    </div>

    <div class="row">
      <div class="label">Тақырып:</div>
      <select id="topic" onchange="onTopicChange()">
        <option value="fractions">Бөлшектерді қосу</option>
        <option value="integers">Рационал сандарды қосу</option>
        <option value="negative_add">Теріс сандарды қосу</option>
        <option value="rational_mul">Рационал сандарды көбейту</option>
        <option value="rational_div">Рационал сандарды бөлу</option>
        <option value="proportion">Пропорция</option>
        <option value="percent">Пайыз есептері</option>
        <option value="coord_segment">Координаталық түзудегі кесінді</option>
        <option value="coord_plane">Координаталық жазықтық</option>
        <option value="equation">Сызықтық теңдеулер</option>
        <option value="inequality">Сызықтық теңсіздіктер</option>
      </select>
      <span class="pill">Таңдаңыз</span>
    </div>

    <div class="row">
      <button class="btn-primary" onclick="generateTask()">Тапсырма жасау</button>
      <button class="btn-ghost" onclick="resetTask()">Қайта бастау</button>
    </div>

    <div class="task-card">
      <div class="task-chip">
        <span class="task-chip-dot"></span>
        Тапсырма
      </div>
      <div id="task">Алдымен тақырыпты таңдап, «Тапсырма жасау» батырмасын басыңыз.</div>

      <div class="answer-row">
        <input type="text" id="answer" placeholder="Жауабыңызды жазыңыз">
        <button class="btn-primary" onclick="check()">Тексеру</button>
      </div>
      <div id="result"></div>
    </div>
  </div>

  <div class="right-pane">
    <div class="orb"></div>

    <div class="section-title">Ереже және түсіндірме</div>
    <div id="theory" class="theory-box"></div>

    <div class="topic-meta" id="topic-meta"></div>

    <div class="graphic-card">
      <div class="graphic-title">Көрнекі модель</div>
      <div id="graphic-text">Таңдалған тақырыпқа байланысты қарапайым визуалды түсіндірме көрсетіледі.</div>
      <div class="graphic-canvas" id="graphic-canvas">
        <div class="grid-lines"></div>
        <div class="axis-x"></div>
        <div class="axis-y"></div>
      </div>
    </div>
  </div>
</div>

<script>
let correct = null;

const theoryContent = {
  "fractions": {
    title: "Бөлшектерді қосу",
    body: "Бөлшектерді қосу үшін алдымен оларды ортақ бөлімге келтіреміз. Содан кейін алымдарын қосып, бөлімін сол күйінде қалдырамыз. Қажет болса, шыққан бөлшекті қысқарта аламыз.",
    example: "Мысал: 1/3 + 1/6 = ?  Ортақ бөлім 6: 1/3 = 2/6, 1/6 = 1/6.  Сонда 2/6 + 1/6 = 3/6 = 1/2.",
    tags: ["Бөлшектер", "Қосу", "Ортақ бөлім"]
  },
  "integers": {
    title: "Рационал сандарды қосу",
    body: "Бірдей таңбалы рационал сандарды қосқанда, олардың модульдерін қосып, нәтижеге сол таңбаны қоямыз. Әр түрлі таңбалы сандарды қосқанда үлкен модульден кіші модульді азайтып, үлкен модульдің таңбасын қалдырамыз.",
    example: "Мысал: -7 + (-5) = -12;  -9 + 4 = -5.",
    tags: ["Рационал сандар", "Қосу", "Модуль"]
  },
  "negative_add": {
    title: "Теріс сандарды қосу",
    body: "Екі теріс санды қосқанда, олардың модульдерін қосып, нәтижеге теріс таңба қоямыз. Бұл қарыздың үстіне тағы қарыз қосылғанға ұқсайды.",
    example: "Мысал: -6 + (-3) = -(6 + 3) = -9.",
    tags: ["Теріс сандар", "Қосу"]
  },
  "rational_mul": {
    title: "Рационал сандарды көбейту",
    body: "Рационал бөлшектерді көбейту үшін алымдарды бір-біріне, бөлімдерді бір-біріне көбейтеміз. Мүмкін болса, нәтижені қысқартамыз.",
    example: "Мысал: 2/3 · 5/4 = (2·5)/(3·4) = 10/12 = 5/6.",
    tags: ["Рационал сандар", "Көбейту", "Бөлшектер"]
  },
  "rational_div": {
    title: "Рационал сандарды бөлу",
    body: "Бөлшекті бөлшекке бөлгенде, бөлгіштің керісына көбейтеміз: a/b ÷ c/d = a/b · d/c.",
    example: "Мысал: 3/5 ÷ 2/3 = 3/5 · 3/2 = 9/10.",
    tags: ["Рационал сандар", "Бөлу", "Кері сан"]
  },
  "proportion": {
    title: "Пропорция және оның қасиеті",
    body: "Пропорция — екі қатынастың теңдігі. Негізгі қасиеті: a/b = c/d болса, онда a·d = b·c. Осы қасиетті пайдаланып, белгісіз мүшені табамыз.",
    example: "Мысал: 2:5 = x:15 → 2·15 = 5·x → 30 = 5x → x = 6.",
    tags: ["Пропорция", "Қатынас", "Крестпен көбейту"]
  },
  "percent": {
    title: "Пайызды табу",
    body: "a санының p%-ын табу үшін a санын p-ға көбейтіп, 100-ге бөлеміз. Пайыз – жүзден бір үлес, сондықтан формула a·p/100 түрінде.",
    example: "Мысал: 200 санының 15%-ын табу: 200 · 15 / 100 = 30.",
    tags: ["Пайыз", "Пропорция", "Қаржы есептері"]
  },
  "coord_segment": {
    title: "Координаталық түзудегі кесіндінің ұзындығы",
    body: "Координаталық түзудегі екі нүктенің арақашықтығы олардың координаталарының айырмасының модуліне тең. Нүктелердің координаталары x₁ және x₂ болса, қашықтық |x₂ − x₁| формуласы арқылы табылады.",
    example: "Мысал: 3 және 9 нүктелері үшін |9 − 3| = 6.",
    tags: ["Координаталық түзу", "Қашықтық", "Модуль"]
  },
  "coord_plane": {
    title: "Координаталық жазықтықтағы нүкте",
    body: "Координаталық жазықтықта әр нүкте (x, y) жұбы арқылы беріледі. x — горизонталь, y — вертикаль бағыт. Нүктенің координаталары оның осьтерге қатысты орнын анықтайды.",
    example: "Мысал: A(2, 3) нүктесі x осінен 2 бірлік оңға, y осінен 3 бірлік жоғары орналасқан.",
    tags: ["Координаталық жазықтық", "Нүкте", "Координаталар"]
  },
  "equation": {
    title: "Сызықтық теңдеулер",
    body: "Сызықтық теңдеу әдетте ax + b = c түрінде болады. Мұндай теңдеуді шешу үшін x айнымалысын жеке қалдырамыз: алдымен b-ні теңдеудің оң жағына көшіреміз, содан кейін a коэффициентіне бөлеміз.",
    example: "Мысал: 3x + 4 = 19 → 3x = 15 → x = 5.",
    tags: ["Теңдеу", "Сызықтық модель", "Алгоритм"]
  },
  "inequality": {
    title: "Сызықтық теңсіздіктер",
    body: "Сызықтық теңсіздікті шешу теңдеуге ұқсас: айнымалыны бір жаққа, сандарды екінші жаққа жинаймыз. Егер теңсіздікті теріс санға бөлсек немесе көбейтсек, теңсіздік белгісінің бағытын ауыстыру керек.",
    example: "Мысал: 2x − 3 > 5 → 2x > 8 → x > 4.",
    tags: ["Теңсіздік", "Сан осі", "Шешім жиыны"]
  }
};

function renderTheory(topic) {
  const box = document.getElementById("theory");
  const meta = document.getElementById("topic-meta");
  const data = theoryContent[topic];

  if (!data) {
    box.innerHTML = "<div class='theory-title'>Тақырып таңдалмаған</div><div class='theory-body'>Алдымен тақырыпты таңдаңыз.</div>";
    meta.innerHTML = "";
    return;
  }

  box.innerHTML = `
    <div class="theory-title">${data.title}</div>
    <div class="theory-body">${data.body}</div>
    <div class="example">${data.example}</div>
  `;

  meta.innerHTML = "";
  data.tags.forEach(t => {
    const span = document.createElement("span");
    span.className = "tag";
    span.textContent = t;
    meta.appendChild(span);
  });
}

function clearGraphic() {
  const canvas = document.getElementById("graphic-canvas");
  const old = canvas.querySelectorAll(".point, .point-label");
  old.forEach(el => el.remove());
}

function placePoint(x, y, labelText) {
  const canvas = document.getElementById("graphic-canvas");
  const w = canvas.clientWidth;
  const h = canvas.clientHeight;
  const px = 50 + (w - 100) * (x + 5) / 10;
  const py = h - (50 + (h - 100) * (y + 5) / 10);

  const p = document.createElement("div");
  p.className = "point";
  p.style.left = px + "px";
  p.style.top = py + "px";

  const label = document.createElement("div");
  label.className = "point-label";
  label.style.left = px + "px";
  label.style.top = py + "px";
  label.textContent = labelText;

  canvas.appendChild(p);
  canvas.appendChild(label);
}

function updateGraphic(topic) {
  clearGraphic();
  const text = document.getElementById("graphic-text");
  if (topic === "coord_plane") {
    const x = Math.floor(Math.random()*7) - 3;
    const y = Math.floor(Math.random()*7) - 3;
    placePoint(x, y, `A(${x}, ${y})`);
    text.textContent = "Координаталық жазықтықта нүктенің орнын визуалды түрде көруге болады: A(x, y).";
  } else if (topic === "coord_segment") {
    const a = Math.floor(Math.random()*8);
    const b = Math.floor(Math.random()*8) + 2;
    placePoint((a-5)/2, 0, String(a));
    placePoint((b-5)/2, 0, String(b));
    text.textContent = "Екі нүктенің арақашықтығы олардың айырмасының модуліне тең.";
  } else if (topic === "equation" || topic === "inequality") {
    text.textContent = "Сызықтық теңдеу мен теңсіздікті сан осінде кескіндеп, шешімін аралық түрінде көрсетуге болады.";
  } else {
    text.textContent = "Бұл аймақта координаталық тор мен осьтер арқылы қарапайым геометриялық түсіндіру беріледі.";
  }
}

function onTopicChange() {
  const topic = document.getElementById("topic").value;
  renderTheory(topic);
  updateGraphic(topic);
  resetTask();
}

function generateTask(){
  const topic = document.getElementById("topic").value;
  const task = document.getElementById("task");
  const resultEl = document.getElementById("result");
  const ans = document.getElementById("answer");

  let a = Math.floor(Math.random()*9)+1;
  let b = Math.floor(Math.random()*9)+1;
  let c = Math.floor(Math.random()*9)+1;
  let d = Math.floor(Math.random()*9)+1;

  if(topic==="fractions"){
      correct = a/b + c/d;
      task.textContent = `${a}/${b} + ${c}/${d} = ?`;
  } else if(topic==="integers"){
      let x = Math.floor(Math.random()*40)-20;
      let y = Math.floor(Math.random()*40)-20;
      correct = x + y;
      task.textContent = `${x} + ${y} = ?`;
  } else if(topic==="negative_add"){
      let x = -Math.floor(Math.random()*20)-1;
      let y = -Math.floor(Math.random()*20)-1;
      correct = x + y;
      task.textContent = `${x} + ${y} = ?`;
  } else if(topic==="rational_mul"){
      correct = (a/b) * (c/d);
      task.textContent = `${a}/${b} × ${c}/${d} = ?`;
  } else if(topic==="rational_div"){
      correct = (a/b) / (c/d);
      task.textContent = `${a}/${b} ÷ ${c}/${d} = ?`;
  } else if(topic==="proportion"){
      correct = (a*d)/b;
      task.textContent = `Пропорцияны толықтырыңыз: ${a} : ${b} = x : ${d}.  x = ?`;
  } else if(topic==="percent"){
      let p = Math.floor(Math.random()*50)+1;
      correct = a * p / 100;
      task.textContent = `${a} санының ${p}% табыңыз.`;
  } else if(topic==="coord_segment"){
      let x1 = Math.floor(Math.random()*20)-10;
      let x2 = Math.floor(Math.random()*20)-10;
      correct = Math.abs(x1 - x2);
      task.textContent = `Кесіндінің ұзындығын табыңыз: |${x2} − ${x1}| = ?`;
  } else if(topic==="coord_plane"){
      let x = Math.floor(Math.random()*11)-5;
      let y = Math.floor(Math.random()*11)-5;
      correct = x + y;
      task.textContent = `A(${x}, ${y}) нүктесі үшін x + y мәнін табыңыз.`;
  } else if(topic==="equation"){
      let A = Math.floor(Math.random()*7)+1;
      let X = Math.floor(Math.random()*11)-5;
      let B = Math.floor(Math.random()*10)-5;
      let C = A*X + B;
      correct = X;
      task.textContent = `${A}x + ${B} = ${C}.  x = ?`;
  } else if(topic==="inequality"){
      let A = Math.floor(Math.random()*7)+1;
      let X = Math.floor(Math.random()*11)-5;
      let B = Math.floor(Math.random()*10)-5;
      let C = A*X + B;
      correct = X;
      task.textContent = `${A}x + ${B} > ${C}.  x > ? (шекара мәнін жазыңыз)`;
  }

  ans.value = "";
  resultEl.textContent = "";
  resultEl.className = "";
}

function resetTask() {
  document.getElementById("task").textContent = "Жаңа тапсырма үшін «Тапсырма жасау» батырмасын басыңыз.";
  document.getElementById("answer").value = "";
  document.getElementById("result").textContent = "";
  document.getElementById("result").className = "";
  correct = null;
}

function check(){
  const resultEl = document.getElementById("result");
  if(correct === null){
      resultEl.textContent = "Алдымен тапсырма жасаңыз.";
      resultEl.className = "result-bad";
      return;
  }
  let raw = document.getElementById("answer").value.trim();
  if(!raw){
      resultEl.textContent = "Алдымен жауабыңызды жазыңыз.";
      resultEl.className = "result-bad";
      return;
  }
  let user = parseFloat(raw.replace(",", "."));
  if(isNaN(user)){
      resultEl.textContent = "Жауап сан болуы керек.";
      resultEl.className = "result-bад";
      return;
  }
  if(Math.abs(user - correct) < 0.001){
      resultEl.textContent = "Дұрыс! Жарайсың! ✔";
      resultEl.className = "result-ok";
  } else {
      resultEl.textContent = "Қате. Дұрыс жауап: " + correct;
      resultEl.className = "result-bad";
  }
}

// initial
onTopicChange();
</script>
</body>
</html>
