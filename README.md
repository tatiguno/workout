[index.html](https://github.com/user-attachments/files/27960112/index.html)<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Workout Tracker</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #f5f3ef;
    --surface: #ffffff;
    --surface2: #f0ede8;
    --border: #e2ddd6;
    --border2: #cdc8bf;
    --text: #1a1814;
    --text2: #6b6560;
    --text3: #9e9890;
    --accent: #2d6a4f;
    --accent-light: #e8f4ee;
    --accent2: #c8724a;
    --accent2-light: #fdf0ea;
    --red: #c0392b;
    --mono: 'DM Mono', monospace;
    --sans: 'DM Sans', sans-serif;
    --radius: 10px;
    --radius-sm: 6px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: var(--sans);
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    font-size: 15px;
    line-height: 1.5;
  }

  header {
    background: var(--surface);
    border-bottom: 1px solid var(--border);
    padding: 0 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 60px;
    position: sticky;
    top: 0;
    z-index: 100;
  }

  .logo {
    font-family: var(--mono);
    font-size: 13px;
    font-weight: 500;
    letter-spacing: .08em;
    color: var(--text2);
    text-transform: uppercase;
  }

  .logo span { color: var(--accent); }

  .header-controls {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .toggle-group {
    display: flex;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 3px;
    gap: 2px;
  }

  .toggle-group button {
    font-family: var(--mono);
    font-size: 11px;
    font-weight: 500;
    letter-spacing: .05em;
    padding: 4px 10px;
    border: none;
    border-radius: 16px;
    background: none;
    color: var(--text3);
    cursor: pointer;
    transition: all .15s;
  }

  .toggle-group button.active {
    background: var(--surface);
    color: var(--text);
    box-shadow: 0 1px 3px rgba(0,0,0,.08);
  }

  .main { max-width: 760px; margin: 0 auto; padding: 28px 20px 80px; }

  .day-tabs {
    display: flex;
    gap: 6px;
    margin-bottom: 24px;
    flex-wrap: wrap;
  }

  .day-tab {
    font-family: var(--mono);
    font-size: 11px;
    font-weight: 500;
    letter-spacing: .06em;
    padding: 7px 14px;
    border-radius: 20px;
    border: 1px solid var(--border2);
    background: var(--surface);
    color: var(--text2);
    cursor: pointer;
    transition: all .15s;
    text-transform: uppercase;
  }

  .day-tab:hover { border-color: var(--accent); color: var(--accent); }

  .day-tab.active {
    background: var(--accent);
    border-color: var(--accent);
    color: white;
  }

  .day-panel { display: none; }
  .day-panel.active { display: block; }

  .day-header {
    margin-bottom: 20px;
  }

  .day-title {
    font-size: 22px;
    font-weight: 500;
    color: var(--text);
    margin-bottom: 4px;
  }

  .day-meta {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--text3);
    letter-spacing: .04em;
  }

  .section {
    margin-bottom: 10px;
  }

  .section-label {
    font-family: var(--mono);
    font-size: 10px;
    font-weight: 500;
    letter-spacing: .12em;
    text-transform: uppercase;
    color: var(--text3);
    padding: 16px 0 8px;
    border-bottom: 1px solid var(--border);
    margin-bottom: 8px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .add-exercise-btn {
    font-family: var(--mono);
    font-size: 10px;
    padding: 3px 9px;
    border-radius: 12px;
    border: 1px dashed var(--border2);
    background: none;
    color: var(--text3);
    cursor: pointer;
    transition: all .15s;
    letter-spacing: .04em;
  }

  .add-exercise-btn:hover { border-color: var(--accent); color: var(--accent); }

  .exercise-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    margin-bottom: 8px;
    overflow: hidden;
    transition: border-color .15s;
  }

  .exercise-card:hover { border-color: var(--border2); }

  .exercise-header {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    padding: 13px 14px 13px 14px;
    cursor: pointer;
    user-select: none;
  }

  .exercise-num {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text3);
    padding-top: 2px;
    min-width: 18px;
    flex-shrink: 0;
  }

  .exercise-info { flex: 1; min-width: 0; }

  .exercise-name-display {
    font-size: 14px;
    font-weight: 500;
    color: var(--text);
    margin-bottom: 2px;
  }

  .exercise-name-edit {
    font-family: var(--sans);
    font-size: 14px;
    font-weight: 500;
    color: var(--text);
    border: none;
    border-bottom: 1.5px solid var(--accent);
    background: none;
    width: 100%;
    outline: none;
    padding: 0 0 2px;
    margin-bottom: 2px;
    display: none;
  }

  .exercise-scheme {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text3);
  }

  .exercise-note {
    font-size: 12px;
    color: var(--text3);
    margin-top: 3px;
    font-style: italic;
  }

  .exercise-actions {
    display: flex;
    gap: 4px;
    flex-shrink: 0;
    padding-top: 1px;
  }

  .icon-btn {
    width: 28px;
    height: 28px;
    border-radius: var(--radius-sm);
    border: 1px solid transparent;
    background: none;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--text3);
    font-size: 14px;
    transition: all .15s;
    flex-shrink: 0;
  }

  .icon-btn:hover { background: var(--surface2); border-color: var(--border); color: var(--text2); }
  .icon-btn.danger:hover { background: #fff5f5; border-color: #ffc5c0; color: var(--red); }
  .icon-btn.save-btn:hover { background: var(--accent-light); border-color: var(--accent); color: var(--accent); }

  .chevron-btn {
    font-size: 10px;
    transition: transform .2s;
    color: var(--text3);
  }

  .chevron-btn.open { transform: rotate(180deg); }

  .log-panel {
    display: none;
    border-top: 1px solid var(--border);
    background: var(--surface2);
    padding: 12px 14px 14px;
  }

  .log-panel.open { display: block; }

  .week-row {
    display: grid;
    grid-template-columns: 52px 1fr 1fr auto;
    gap: 8px;
    align-items: center;
    margin-bottom: 7px;
  }

  .week-label {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text3);
    letter-spacing: .04em;
  }

  .log-input {
    font-family: var(--mono);
    font-size: 12px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    padding: 6px 9px;
    color: var(--text);
    width: 100%;
    outline: none;
    transition: border-color .15s;
  }

  .log-input:focus { border-color: var(--accent); }
  .log-input::placeholder { color: var(--text3); }

  .log-input-label {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--text3);
    margin-bottom: 4px;
    letter-spacing: .04em;
  }

  .log-fields { display: contents; }

  .log-col { display: flex; flex-direction: column; }

  .save-row-btn {
    font-family: var(--mono);
    font-size: 10px;
    padding: 6px 10px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border2);
    background: var(--surface);
    color: var(--text3);
    cursor: pointer;
    transition: all .15s;
    white-space: nowrap;
    letter-spacing: .03em;
  }

  .save-row-btn:hover { background: var(--accent-light); border-color: var(--accent); color: var(--accent); }
  .save-row-btn.saved { background: var(--accent-light); border-color: var(--accent); color: var(--accent); }

  .log-header-row {
    display: grid;
    grid-template-columns: 52px 1fr 1fr auto;
    gap: 8px;
    margin-bottom: 6px;
  }

  .log-header-row span {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--text3);
    letter-spacing: .06em;
    text-transform: uppercase;
  }

  .log-notes-wrap { margin-top: 8px; }

  .log-notes {
    font-family: var(--sans);
    font-size: 12px;
    width: 100%;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    padding: 7px 9px;
    color: var(--text);
    resize: none;
    outline: none;
    min-height: 38px;
    transition: border-color .15s;
    line-height: 1.5;
  }

  .log-notes:focus { border-color: var(--accent); }
  .log-notes::placeholder { color: var(--text3); }

  .warmup-block {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 13px 14px;
    margin-bottom: 8px;
  }

  .warmup-title {
    font-family: var(--mono);
    font-size: 11px;
    font-weight: 500;
    letter-spacing: .06em;
    text-transform: uppercase;
    color: var(--text2);
    margin-bottom: 8px;
  }

  .warmup-items { display: flex; flex-direction: column; gap: 4px; }

  .warmup-item {
    font-size: 13px;
    color: var(--text2);
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .warmup-item::before {
    content: '';
    width: 4px;
    height: 4px;
    border-radius: 50%;
    background: var(--text3);
    flex-shrink: 0;
  }

  .mobility-block {
    background: var(--accent-light);
    border: 1px solid #b7dfc8;
    border-radius: var(--radius);
    padding: 13px 14px;
    margin-top: 8px;
  }

  .mobility-title {
    font-family: var(--mono);
    font-size: 11px;
    font-weight: 500;
    letter-spacing: .06em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 8px;
  }

  .mobility-items { display: flex; flex-direction: column; gap: 4px; }

  .mobility-item {
    font-size: 13px;
    color: #2d6a4f;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .mobility-item::before {
    content: '';
    width: 4px;
    height: 4px;
    border-radius: 50%;
    background: var(--accent);
    flex-shrink: 0;
  }

  .priority-badge {
    display: inline-block;
    font-family: var(--mono);
    font-size: 10px;
    background: var(--accent2-light);
    color: var(--accent2);
    border-radius: 4px;
    padding: 1px 6px;
    margin-left: 6px;
    vertical-align: middle;
    letter-spacing: .02em;
  }

  .day-notes-section {
    margin-top: 24px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 14px;
  }

  .day-notes-label {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: .1em;
    text-transform: uppercase;
    color: var(--text3);
    margin-bottom: 8px;
  }

  .day-notes-input {
    font-family: var(--sans);
    font-size: 13px;
    width: 100%;
    background: none;
    border: none;
    color: var(--text);
    resize: none;
    outline: none;
    min-height: 60px;
    line-height: 1.6;
  }

  .day-notes-input::placeholder { color: var(--text3); }

  .add-week-btn {
    font-family: var(--mono);
    font-size: 10px;
    padding: 5px 10px;
    border-radius: var(--radius-sm);
    border: 1px dashed var(--border2);
    background: none;
    color: var(--text3);
    cursor: pointer;
    transition: all .15s;
    margin-top: 6px;
    letter-spacing: .03em;
  }

  .add-week-btn:hover { border-color: var(--accent); color: var(--accent); }

  .toast {
    position: fixed;
    bottom: 24px;
    right: 24px;
    background: var(--text);
    color: white;
    font-family: var(--mono);
    font-size: 12px;
    padding: 10px 16px;
    border-radius: var(--radius);
    opacity: 0;
    transform: translateY(8px);
    transition: all .2s;
    pointer-events: none;
    z-index: 999;
    letter-spacing: .03em;
  }

  .toast.show { opacity: 1; transform: translateY(0); }

  .unit-hint {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--text3);
    margin-left: 4px;
  }

  @media (max-width: 540px) {
    .week-row, .log-header-row {
      grid-template-columns: 44px 1fr 1fr auto;
      gap: 6px;
    }
    header { padding: 0 14px; }
    .main { padding: 20px 14px 80px; }
  }
</style>
</head>
<body>

<header>
  <div class="logo"><span>◆</span> Workout Log</div>
  <div class="header-controls">
    <div class="toggle-group" id="unit-toggle">
      <button class="active" onclick="setUnit('lbs')">lbs</button>
      <button onclick="setUnit('kg')">kg</button>
    </div>
    <div class="toggle-group" id="measure-toggle">
      <button class="active" onclick="setMeasure('reps')">reps</button>
      <button onclick="setMeasure('sec')">sec</button>
    </div>
  </div>
</header>

<div class="main">
  <div class="day-tabs" id="day-tabs"></div>
  <div id="day-panels"></div>
</div>

<div class="toast" id="toast"></div>

<script>
const DAYS = [
  {
    id: 'd1',
    label: 'Day 1',
    title: 'Day 1 — Lower Body',
    meta: 'Monday · Quads · Glutes · Hamstrings · Balance · Hip Mobility',
    warmup: ['5 min bike (moderate pace)', 'Hip circles — 10 each direction', 'Lateral band walks — 10 each side', 'Bodyweight squats — 10 reps'],
    sections: [
      {
        label: 'Squat — quad priority',
        exercises: [
          { name: 'Bulgarian split squat', scheme: '4×10 R / 3×10 L', note: 'Complete right side first. Right quad focus.', priority: true },
          { name: 'Single-leg press (machine)', scheme: '3×12 each leg', note: 'Right leg first. Full range, controlled descent.', priority: true },
        ]
      },
      {
        label: 'Hinge',
        exercises: [
          { name: 'Single-leg Romanian deadlift', scheme: '3×10 each leg', note: 'Dumbbell in opposite hand, slight knee bend.' },
          { name: 'Single-leg glute bridge', scheme: '3×12 each leg', note: '3 sec hold at top.' },
        ]
      },
      {
        label: 'Accessory + Core',
        exercises: [
          { name: 'Lateral step-up', scheme: '3×12 R / 2×12 L', note: 'Controlled step down — don\'t drop.', priority: true },
          { name: 'Hip abduction machine', scheme: '3×15' },
          { name: 'Pallof press', scheme: '3×10 each side', note: 'Anti-rotation core — brace and hold briefly.' },
        ]
      }
    ],
    mobility: ['Hip flexor stretch (bench or kneeling) — 90 sec / side', '90/90 hip switch — 10 switches', 'World\'s greatest stretch — 5 reps / side']
  },
  {
    id: 'd2',
    label: 'Day 2',
    title: 'Day 2 — Upper Body',
    meta: 'Tuesday · Upper Back · Shoulder Health · Pull Strength · Push Balance',
    warmup: ['5 min bike', 'Arm circles — 10 each direction, each arm', 'Band pull-aparts — 2×15', 'Pec stretch (doorway or cable) — 30 sec / side'],
    sections: [
      {
        label: 'Shoulder mobility — upper back focus',
        exercises: [
          { name: 'Shoulder CARs', scheme: '3×5 each arm', note: 'Very slow, full pain-free range.' },
          { name: 'Wall slide', scheme: '3×10', note: 'Forearms on wall, slide up and down.' },
          { name: 'Prone Y-T-W (incline bench, 1–2 kg)', scheme: '3×10 each position', note: 'Y=diagonal arms, T=arms out, W=elbows bent. Keep weight very light.' },
        ]
      },
      {
        label: 'Upper back — primary focus',
        exercises: [
          { name: 'Seated cable row — single arm', scheme: '4×10 each arm', note: 'Squeeze scapula, pause 1 sec at end.' },
          { name: 'Face pull (rope, high cable)', scheme: '3×15', note: 'Elbows high and wide. Key for right upper back.' },
          { name: 'Cable external rotation', scheme: '3×15 each arm', note: 'Elbow pinned at 90°, start light.' },
          { name: 'Lat pulldown (wide grip)', scheme: '3×10', note: 'Full hang at top, squeeze lats at bottom.' },
        ]
      },
      {
        label: 'Push — balanced volume',
        exercises: [
          { name: 'Single-arm dumbbell press', scheme: '3×10 each arm', note: 'Seated or incline. Left at ~60% if imbalance present.' },
          { name: 'Cable rear delt fly — single arm', scheme: '3×15 each arm', note: 'Slight forward lean, arm sweeps back and slightly up.' },
        ]
      }
    ],
    mobility: []
  },
  {
    id: 'd3',
    label: 'Day 3',
    title: 'Day 3 — Full Body A',
    meta: 'Thursday · Compound Lower · Upper Pull/Push · Rotational Core · Balance',
    warmup: ['5 min incline treadmill walk', 'Hip flexor stretch — 30 sec / side', 'Band pull-aparts — 10 reps', 'Deep squat hold (assisted) — 3×30 sec'],
    sections: [
      {
        label: 'Lower — lunge pattern + hinge',
        exercises: [
          { name: 'Deficit reverse lunge', scheme: '4×10 R / 3×10 L', note: 'Step off a small plate. Right priority.', priority: true },
          { name: 'Lateral lunge', scheme: '3×10 each side', note: 'Bodyweight or light DB.' },
          { name: 'Single-arm RDL', scheme: '3×10 each leg', note: 'Slow and controlled — balance challenge.' },
        ]
      },
      {
        label: 'Upper — pull and shoulder',
        exercises: [
          { name: 'Single-arm lateral raise', scheme: '3×15 each arm', note: 'Left at 60%. Superset with rear delt fly below.' },
          { name: 'Cable rear delt fly — single arm', scheme: '3×15 each arm', note: 'Superset with lateral raise. Rest 60 sec after pair.' },
          { name: 'Seated cable row (bilateral)', scheme: '3×10', note: 'Heavier than Day 2 single-arm.' },
        ]
      },
      {
        label: 'Core + rotation',
        exercises: [
          { name: 'Standing cable twist — low to high', scheme: '3×12 each side', note: 'Controlled, no momentum.' },
          { name: 'Forearm plank with hip dip', scheme: '3×12 dips each side' },
        ]
      }
    ],
    mobility: ['Pigeon pose (or figure-four on bench) — 90 sec / side', 'Thoracic extension over foam roller — 60–90 sec']
  },
  {
    id: 'd4',
    label: 'Day 4',
    title: 'Day 4 — Full Body B',
    meta: 'Saturday · Hip Hinge Emphasis · Upper Back Accessory · Full Mobility',
    warmup: ['5 min bike', 'Shoulder CARs — 2×5 each arm', 'World\'s greatest stretch — 5 reps / side'],
    sections: [
      {
        label: 'Lower — glute and hinge focus',
        exercises: [
          { name: 'Hip thrust machine (or barbell)', scheme: '4×10', note: 'Full hip extension at top.' },
          { name: 'Goblet squat', scheme: '3×10', note: 'Pause 2 sec at bottom.' },
          { name: 'Seated calf raise', scheme: '3×15', note: 'Ankle stability and strength.' },
        ]
      },
      {
        label: 'Upper back — accessory (2nd weekly hit)',
        exercises: [
          { name: 'Prone Y-T-W (incline bench, 1–2 kg)', scheme: '3×10 each position', note: 'Keep weights very light. Form over load.' },
          { name: 'Face pull (rope, high cable)', scheme: '3×15', note: 'High elbows, retract and hold briefly.' },
          { name: 'Lat pulldown (neutral grip)', scheme: '3×10', note: 'Different angle from Day 2 wide grip.' },
        ]
      },
      {
        label: 'Core + balance',
        exercises: [
          { name: 'Dead bug (slow)', scheme: '3×8 each side', note: 'Lower back stays flat on floor the entire time.' },
          { name: 'Farmer\'s carry', scheme: '3×30 m', note: 'Brace through core, full body tension.' },
        ]
      }
    ],
    mobility: ['Seated straddle (floor) — 2 min hold', 'Thoracic extension over foam roller — 90 sec', 'Hip flexor deep stretch — 90 sec / side', '90/90 hip switch — 10 switches']
  }
];

let currentUnit = 'lbs';
let currentMeasure = 'reps';
let data = {};

function loadData() {
  try { data = JSON.parse(localStorage.getItem('wt_data') || '{}'); } catch(e) { data = {}; }
}

function saveData() {
  localStorage.setItem('wt_data', JSON.stringify(data));
}

function setUnit(u) {
  currentUnit = u;
  document.querySelectorAll('#unit-toggle button').forEach((b, i) => {
    b.classList.toggle('active', (i === 0 && u === 'lbs') || (i === 1 && u === 'kg'));
  });
  document.querySelectorAll('.unit-hint').forEach(el => el.textContent = u);
  localStorage.setItem('wt_unit', u);
}

function setMeasure(m) {
  currentMeasure = m;
  document.querySelectorAll('#measure-toggle button').forEach((b, i) => {
    b.classList.toggle('active', (i === 0 && m === 'reps') || (i === 1 && m === 'sec'));
  });
  document.querySelectorAll('.measure-hint').forEach(el => el.textContent = m === 'reps' ? 'reps' : 'sec');
  localStorage.setItem('wt_measure', m);
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 1800);
}

function getKey(dayId, sectionIdx, exIdx, week, field) {
  return `${dayId}_s${sectionIdx}_e${exIdx}_w${week}_${field}`;
}

function getDayNoteKey(dayId) { return `${dayId}_daynote`; }
function getExNameKey(dayId, sectionIdx, exIdx) { return `${dayId}_s${sectionIdx}_e${exIdx}_name`; }
function getExNoteKey(dayId, sectionIdx, exIdx) { return `${dayId}_s${sectionIdx}_e${exIdx}_exnote`; }
function getWeekCountKey(dayId, sectionIdx, exIdx) { return `${dayId}_s${sectionIdx}_e${exIdx}_wkcount`; }

function getWeekCount(dayId, sectionIdx, exIdx) {
  return parseInt(data[getWeekCountKey(dayId, sectionIdx, exIdx)] || '4');
}

function buildWeekRows(dayId, sectionIdx, exIdx) {
  const count = getWeekCount(dayId, sectionIdx, exIdx);
  let html = '';
  for (let w = 1; w <= count; w++) {
    const wk = `Week ${w}`;
    const wtVal = data[getKey(dayId, sectionIdx, exIdx, w, 'wt')] || '';
    const repVal = data[getKey(dayId, sectionIdx, exIdx, w, 'rep')] || '';
    const savedClass = (wtVal || repVal) ? 'saved' : '';
    html += `<div class="week-row" id="wr_${dayId}_${sectionIdx}_${exIdx}_${w}">
      <span class="week-label">${wk}</span>
      <div class="log-col">
        <input class="log-input" placeholder="0" value="${wtVal}"
          oninput="saveField('${dayId}',${sectionIdx},${exIdx},${w},'wt',this.value)"
          onfocus="this.select()">
      </div>
      <div class="log-col">
        <input class="log-input" placeholder="—"  value="${repVal}"
          oninput="saveField('${dayId}',${sectionIdx},${exIdx},${w},'rep',this.value)"
          onfocus="this.select()">
      </div>
      <button class="save-row-btn ${savedClass}" onclick="markSaved(this)">${savedClass ? '✓ saved' : 'save'}</button>
    </div>`;
  }
  return html;
}

function saveField(dayId, sectionIdx, exIdx, week, field, val) {
  data[getKey(dayId, sectionIdx, exIdx, week, field)] = val;
  saveData();
}

function markSaved(btn) {
  btn.classList.add('saved');
  btn.textContent = '✓ saved';
  showToast('Saved');
}

function toggleLog(id) {
  const panel = document.getElementById('lp_' + id);
  const chev = document.getElementById('chev_' + id);
  if (!panel) return;
  panel.classList.toggle('open');
  chev.classList.toggle('open');
}

function startEdit(dayId, sectionIdx, exIdx) {
  const display = document.getElementById(`ename_${dayId}_${sectionIdx}_${exIdx}`);
  const input = document.getElementById(`einput_${dayId}_${sectionIdx}_${exIdx}`);
  display.style.display = 'none';
  input.style.display = 'block';
  input.focus();
  input.select();
}

function saveExName(dayId, sectionIdx, exIdx, val) {
  const key = getExNameKey(dayId, sectionIdx, exIdx);
  data[key] = val;
  saveData();
  const display = document.getElementById(`ename_${dayId}_${sectionIdx}_${exIdx}`);
  const input = document.getElementById(`einput_${dayId}_${sectionIdx}_${exIdx}`);
  display.textContent = val || display.textContent;
  display.style.display = 'block';
  input.style.display = 'none';
  showToast('Exercise name updated');
}

function addWeek(dayId, sectionIdx, exIdx) {
  const key = getWeekCountKey(dayId, sectionIdx, exIdx);
  const current = getWeekCount(dayId, sectionIdx, exIdx);
  const next = current + 1;
  data[key] = String(next);
  saveData();
  const container = document.getElementById(`wrows_${dayId}_${sectionIdx}_${exIdx}`);
  const w = next;
  const div = document.createElement('div');
  div.className = 'week-row';
  div.id = `wr_${dayId}_${sectionIdx}_${exIdx}_${w}`;
  div.innerHTML = `
    <span class="week-label">Week ${w}</span>
    <div class="log-col"><input class="log-input" placeholder="0"
      oninput="saveField('${dayId}',${sectionIdx},${exIdx},${w},'wt',this.value)" onfocus="this.select()"></div>
    <div class="log-col"><input class="log-input" placeholder="—"
      oninput="saveField('${dayId}',${sectionIdx},${exIdx},${w},'rep',this.value)" onfocus="this.select()"></div>
    <button class="save-row-btn" onclick="markSaved(this)">save</button>`;
  container.appendChild(div);
}

function addExercise(dayId, sectionIdx) {
  const day = DAYS.find(d => d.id === dayId);
  if (!day) return;
  const section = day.sections[sectionIdx];
  const exIdx = section.exercises.length;
  section.exercises.push({ name: 'New exercise', scheme: '3×10', note: '' });

  const sectionEl = document.getElementById(`section_${dayId}_${sectionIdx}`);
  const addBtn = sectionEl.querySelector('.add-exercise-btn');
  const card = createExerciseCard(dayId, sectionIdx, exIdx, section.exercises[exIdx]);
  sectionEl.insertBefore(card, addBtn.parentElement);

  setTimeout(() => startEdit(dayId, sectionIdx, exIdx), 50);
}

function createExerciseCard(dayId, sectionIdx, exIdx, ex) {
  const id = `${dayId}_${sectionIdx}_${exIdx}`;
  const savedName = data[getExNameKey(dayId, sectionIdx, exIdx)] || ex.name;
  const weekRows = buildWeekRows(dayId, sectionIdx, exIdx);
  const noteVal = data[getExNoteKey(dayId, sectionIdx, exIdx)] || '';

  const card = document.createElement('div');
  card.className = 'exercise-card';
  card.id = `card_${id}`;
  card.innerHTML = `
    <div class="exercise-header" onclick="toggleLog('${id}')">
      <span class="exercise-num">${exIdx + 1}.</span>
      <div class="exercise-info">
        <div class="exercise-name-display" id="ename_${id}">${savedName}${ex.priority ? '<span class="priority-badge">R priority</span>' : ''}</div>
        <input class="exercise-name-edit" id="einput_${id}" value="${savedName}"
          onblur="saveExName('${dayId}',${sectionIdx},${exIdx},this.value)"
          onkeydown="if(event.key==='Enter')this.blur()">
        <div class="exercise-scheme">${ex.scheme}</div>
        ${ex.note ? `<div class="exercise-note">${ex.note}</div>` : ''}
      </div>
      <div class="exercise-actions" onclick="event.stopPropagation()">
        <button class="icon-btn" title="Edit name" onclick="startEdit('${dayId}',${sectionIdx},${exIdx})">✎</button>
        <button class="icon-btn chevron-btn" id="chev_${id}">▼</button>
      </div>
    </div>
    <div class="log-panel" id="lp_${id}">
      <div class="log-header-row">
        <span></span>
        <span>weight <span class="unit-hint">${currentUnit}</span></span>
        <span><span class="measure-hint">${currentMeasure === 'reps' ? 'reps' : 'sec'}</span></span>
        <span></span>
      </div>
      <div id="wrows_${id}">${weekRows}</div>
      <button class="add-week-btn" onclick="addWeek('${dayId}',${sectionIdx},${exIdx})">+ add week</button>
      <div class="log-notes-wrap">
        <textarea class="log-notes" placeholder="Notes for this exercise…"
          oninput="data['${dayId}_s${sectionIdx}_e${exIdx}_note']=this.value;saveData()"
        >${data[`${dayId}_s${sectionIdx}_e${exIdx}_note`] || ''}</textarea>
      </div>
    </div>`;
  return card;
}

function switchDay(dayId) {
  document.querySelectorAll('.day-tab').forEach(t => t.classList.toggle('active', t.dataset.day === dayId));
  document.querySelectorAll('.day-panel').forEach(p => p.classList.toggle('active', p.id === 'panel_' + dayId));
}

function buildUI() {
  loadData();
  currentUnit = localStorage.getItem('wt_unit') || 'lbs';
  currentMeasure = localStorage.getItem('wt_measure') || 'reps';
  setUnit(currentUnit);
  setMeasure(currentMeasure);

  const tabsEl = document.getElementById('day-tabs');
  const panelsEl = document.getElementById('day-panels');

  DAYS.forEach((day, di) => {
    const tab = document.createElement('button');
    tab.className = 'day-tab' + (di === 0 ? ' active' : '');
    tab.textContent = day.label;
    tab.dataset.day = day.id;
    tab.onclick = () => switchDay(day.id);
    tabsEl.appendChild(tab);

    const panel = document.createElement('div');
    panel.className = 'day-panel' + (di === 0 ? ' active' : '');
    panel.id = 'panel_' + day.id;

    let html = `<div class="day-header"><div class="day-title">${day.title}</div><div class="day-meta">${day.meta}</div></div>`;

    html += `<div class="warmup-block"><div class="warmup-title">Warm-up</div><div class="warmup-items">`;
    day.warmup.forEach(item => { html += `<div class="warmup-item">${item}</div>`; });
    html += `</div></div>`;

    panel.innerHTML = html;

    day.sections.forEach((section, si) => {
      const sectionDiv = document.createElement('div');
      sectionDiv.className = 'section';
      sectionDiv.id = `section_${day.id}_${si}`;

      const labelDiv = document.createElement('div');
      labelDiv.className = 'section-label';
      labelDiv.innerHTML = `<span>${section.label}</span><button class="add-exercise-btn" onclick="addExercise('${day.id}',${si})">+ add exercise</button>`;
      sectionDiv.appendChild(labelDiv);

      section.exercises.forEach((ex, ei) => {
        const card = createExerciseCard(day.id, si, ei, ex);
        sectionDiv.appendChild(card);
      });

      panel.appendChild(sectionDiv);
    });

    if (day.mobility.length > 0) {
      const mobDiv = document.createElement('div');
      mobDiv.className = 'mobility-block';
      let mobHtml = `<div class="mobility-title">Mobility</div><div class="mobility-items">`;
      day.mobility.forEach(item => { mobHtml += `<div class="mobility-item">${item}</div>`; });
      mobHtml += `</div>`;
      mobDiv.innerHTML = mobHtml;
      panel.appendChild(mobDiv);
    }

    const dayNoteKey = getDayNoteKey(day.id);
    const noteSection = document.createElement('div');
    noteSection.className = 'day-notes-section';
    noteSection.innerHTML = `<div class="day-notes-label">Session notes</div>
      <textarea class="day-notes-input" placeholder="How did today feel? Any pain, PRs, adjustments…"
        oninput="data['${dayNoteKey}']=this.value;saveData()">${data[dayNoteKey] || ''}</textarea>`;
    panel.appendChild(noteSection);

    panelsEl.appendChild(panel);
  });
}

buildUI();
</script>
</body>
</html>
