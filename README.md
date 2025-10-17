<!doctype html>
<html lang="ru">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>STUDBISS — Кабинет резидента (защищённый)</title>
<style>
  :root{--brand:#0b63a4;--bg:#f7f9fb;--card:#fff;--muted:#6b7280;}
  body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,'Helvetica Neue',Arial;background:var(--bg);color:#111;}
  header{background:var(--brand);color:#fff;padding:18px 20px;text-align:center;font-weight:700;font-size:1.25rem;}
  .container{max-width:1024px;margin:28px auto;padding:0 18px;}
  .card{background:var(--card);border-radius:12px;padding:18px;box-shadow:0 6px 18px rgba(2,6,23,0.06);}
  .center{display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;}
  h1,h2{margin:0 0 12px 0;color:var(--brand);}
  p.lead{color:var(--muted);margin:0 0 18px 0;}
  .btn{background:var(--brand);color:#fff;border:none;padding:10px 14px;border-radius:10px;font-weight:700;cursor:pointer;margin:8px;}
  .btn.ghost{background:transparent;color:var(--brand);border:2px solid var(--brand);}
  .flex{display:flex;gap:12px;flex-wrap:wrap;align-items:center;}
  .page{display:none;margin-top:18px;}
  .active{display:block;}
  .big-actions{display:flex;gap:18px;justify-content:center;flex-wrap:wrap;margin-top:14px;}
  .input-wrap{max-width:420px;margin:0 auto;text-align:left;}
  label{display:block;font-weight:600;margin-top:8px;font-size:0.95rem;}
  input[type="password"], input[type="text"], input[type="email"], textarea, select{width:100%;padding:10px;border-radius:8px;border:1px solid #d6d8dd;margin-top:6px;box-sizing:border-box;font-size:0.95rem;}
  .hint{font-size:0.88rem;color:var(--muted);margin-top:6px;}
  .cards-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:14px;margin-top:14px;}
  .dept-card{background:#fff;border-radius:10px;padding:16px;box-shadow:0 6px 16px rgba(2,6,23,0.05);cursor:pointer;border-left:6px solid var(--brand);}
  .dept-card h3{margin:0 0 6px 0;}
  .small{font-size:0.86rem;color:var(--muted);}
  .popup{position:fixed;inset:0;background:rgba(0,0,0,0.45);display:none;align-items:center;justify-content:center;padding:20px;z-index:60;}
  .popup .modal{max-width:520px;width:100%;background:#fff;padding:18px;border-radius:12px;box-shadow:0 8px 30px rgba(2,6,23,0.2);}
  .row{display:flex;gap:10px;align-items:center;}
  .table-wrap{overflow:auto;margin-top:12px;}
  table{width:100%;border-collapse:collapse;background:#fff;border-radius:8px;overflow:hidden;}
  th,td{padding:10px;border-bottom:1px solid #eef2f7;text-align:left;}
  th{background:#f3f7fb;color:var(--muted);font-weight:700;}
  td[contenteditable]{background:linear-gradient(180deg,rgba(11,99,164,0.03),transparent);}
  select.inline{padding:6px;border-radius:6px;border:1px solid #d6d8dd;}
  .controls{display:flex;gap:8px;align-items:center;margin-top:12px;}
  .muted{color:var(--muted);font-size:0.9rem;}
  .right{margin-left:auto;}
  .danger{background:#ff4d4f;color:#fff;border:none;padding:8px 10px;border-radius:8px;cursor:pointer;}
  footer{margin:28px 0 60px 0;text-align:center;color:var(--muted);font-size:0.9rem;}
  .status-pill{display:inline-block;padding:6px 8px;border-radius:999px;font-weight:700;font-size:0.85rem;}
  .status-inprogress{background:#fff4e6;color:#b45309;border:1px solid #fde7c8;}
  .status-done{background:#ecfdf5;color:#065f46;border:1px solid #bbf7d0;}
  .status-onhold{background:#f3f4f6;color:#374151;border:1px solid #e5e7eb;}
  .status-cancel{background:#fff1f2;color:#831843;border:1px solid #fed7e2;}
  .topbar{display:flex;align-items:center;gap:12px;margin-bottom:12px;}
  .back-link{background:transparent;border:0;color:var(--brand);cursor:pointer;font-weight:700;padding:6px 8px;border-radius:8px;}
</style>
</head>
<body>
<header>Бизнес-клуб УУНиТ «STUDBISS» — защищённый доступ</header>

<div class="container">

  <!-- Home page -->
  <div id="homePage" class="page active card center">
    <h1>Добро пожаловать в STUDBISS</h1>
    <p class="lead">Вы резидент или хотите присоединиться? Выберите действие ниже.</p>
    <div class="big-actions">
      <button class="btn" onclick="showPage('residentLogin')">💼 Я — резидент (войти)</button>
      <button class="btn ghost" onclick="showPage('new')">🚀 Я — новый участник</button>
    </div>
    <p class="hint">Пароли защищены — ввод требуется для доступа в кабинет и департаменты.</p>
  </div>

  <!-- New participant -->
  <div id="new" class="page card">
    <h2>Регистрация нового участника</h2>
    <p class="small">Заполните форму, и мы свяжемся с вами.</p>
    <form id="regForm" onsubmit="event.preventDefault(); alert('Спасибо! Заявка отправлена — пока симуляция.'); showPage('homePage')">
      <div class="input-wrap">
        <label>Имя</label><input type="text" required>
        <label>Фамилия</label><input type="text" required>
        <label>Электронная почта</label><input type="email" required>
        <label>Телефон</label><input type="text" required>
        <label>Направление интереса</label>
        <select required>
          <option value="">-- выберите --</option>
          <option>Медиа</option>
          <option>Ивент</option>
          <option>Стратегическое развитие</option>
          <option>Фандрайз</option>
        </select>
        <label>Почему хотите в STUDBISS?</label><textarea rows="4" required></textarea>
        <div class="controls"><button class="btn" type="submit">Отправить заявку</button><button class="btn ghost" type="button" onclick="showPage('homePage')">Назад</button></div>
      </div>
    </form>
  </div>

  <!-- Resident login -->
  <div id="residentLogin" class="page card">
    <h2>Вход в кабинет резидента</h2>
    <p class="small">Введите пароль резидента, чтобы продолжить.</p>
    <div class="input-wrap">
      <label>Пароль резидента</label>
      <input id="residentPassword" type="password" />
      <div style="margin-top:10px;" class="controls">
        <button class="btn" onclick="checkResident()">Войти</button>
        <button class="btn ghost" onclick="showPage('homePage')">Отмена</button>
        <div id="resHint" class="muted right"></div>
      </div>
    </div>
  </div>

  <!-- Resident cabinet (protected) -->
  <div id="cabinet" class="page card">
    <div class="topbar">
      <button class="back-link" onclick="logout()">⟵ Выйти</button>
      <h2 style="margin:0">Кабинет резидента</h2>
    </div>
    <p class="small">Выберите департамент для доступа — для каждого требуется отдельный пароль.</p>
    <div class="cards-grid">
      <div class="dept-card" onclick="promptDept('media')"><h3>🎥 Медиа</h3><p class="small">Контент, соцсети, дизайн — пароль требуется.</p></div>
      <div class="dept-card" onclick="promptDept('event')"><h3>🎤 Ивент</h3><p class="small">Организация мероприятий. Пароль требуется.</p></div>
      <div class="dept-card" onclick="promptDept('strat')"><h3>📈 Стратегическое развитие</h3><p class="small">Стратегия и развитие проектов. Пароль требуется.</p></div>
      <div class="dept-card" onclick="promptDept('fund')"><h3>💰 Фандрайз</h3><p class="small">Поиск спонсоров и партнёров. Пароль требуется.</p></div>
    </div>
  </div>

  <!-- Department: Media (protected page) -->
  <div id="mediaPage" class="page card">
    <div class="topbar">
      <button class="back-link" onclick="showPage('cabinet')">⟵ Назад в кабинет</button>
      <h2 style="margin:0">Медиа — контент-план</h2>
    </div>
    <p class="small">Таблица контент-плана. Можно редактировать ячейки и выбирать ответственного / статус. Изменения сохраняются в браузере.</p>
    <div class="controls" style="margin-top:12px;">
      <button class="btn" onclick="addRow()">+ Добавить задачу</button>
      <button class="btn ghost" onclick="clearMedia()">Очистить всё</button>
      <div class="right muted">Ответственные: Никита (руководитель медиа), Юля (зам. руководителя)</div>
    </div>

    <div class="table-wrap">
      <table id="mediaTable" class="card" style="margin-top:12px;">
        <thead>
          <tr><th style="width:110px">Дата</th><th style="width:120px">Формат</th><th>Описание</th><th style="width:160px">Ответственный</th><th style="width:140px">Статус</th><th style="width:90px">Действия</th></tr>
        </thead>
        <tbody id="mediaBody">
        </tbody>
      </table>
    </div>
  </div>

  <!-- Event page -->
  <div id="eventPage" class="page card">
    <div class="topbar"><button class="back-link" onclick="showPage('cabinet')">⟵ Назад</button><h2 style="margin:0">Ивент</h2></div>
    <p class="small">Страница Ивент-департамента. Здесь можно разместить планы мероприятий, таймлайны и задачи.</p>
  </div>

  <!-- Strategy page -->
  <div id="stratPage" class="page card">
    <div class="topbar"><button class="back-link" onclick="showPage('cabinet')">⟵ Назад</button><h2 style="margin:0">Стратегическое развитие</h2></div>
    <p class="small">Страница стратегического развития — место для идей, дорожных карт и аналитики.</p>
  </div>

  <!-- Fundraising page -->
  <div id="fundPage" class="page card">
    <div class="topbar"><button class="back-link" onclick="showPage('cabinet')">⟵ Назад</button><h2 style="margin:0">Фандрайз</h2></div>
    <p class="small">Страница фандрайзинга — списки спонсоров, предложения и коммуникация.</p>
  </div>

</div>

<!-- Popup modal for passwords and messages -->
<div id="modal" class="popup">
  <div class="modal card">
    <div id="modalContent"></div>
    <div style="margin-top:12px;display:flex;gap:8px;justify-content:flex-end;">
      <button id="modalOk" class="btn">ОК</button>
      <button id="modalCancel" class="btn ghost">Отмена</button>
    </div>
  </div>
</div>

<footer>STUDBISS — внутренний интерактивный макет. Локальные данные хранятся в браузере (localStorage).</footer>

<script>
// Passwords (hardcoded as requested)
const PASSWORDS = {
  resident: '39681',
  media: '23789',
  event: '98709',
  strat: '34578',
  fund: '58920'
};

// Simple page navigation
function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  const el = document.getElementById(id);
  if(el) el.classList.add('active');
  window.scrollTo(0,0);
}

// Resident login check
function checkResident(){
  const val = document.getElementById('residentPassword').value.trim();
  const hint = document.getElementById('resHint');
  if(val === PASSWORDS.resident){
    hint.innerText = '';
    document.getElementById('residentPassword').value = '';
    showPage('cabinet');
  } else {
    hint.innerText = '❌ Неверный пароль, попробуйте снова.';
    document.getElementById('residentPassword').value = '';
    document.getElementById('residentPassword').focus();
  }
}

// Prompt for department password
function promptDept(dept){
  const prompts = {
    media: {title:'Вход в Медиа', body:'Введите пароль департамента "Медиа":', id:'mediaPass'},
    event: {title:'Вход в Ивент', body:'Введите пароль департамента "Ивент":', id:'eventPass'},
    strat: {title:'Вход в Стратегическое развитие', body:'Введите пароль департамента "Стратегическое развитие":', id:'stratPass'},
    fund: {title:'Вход в Фандрайз', body:'Введите пароль департамента "Фандрайз":', id:'fundPass'}
  };
  const cfg = prompts[dept];
  showModal(`<h3 style="margin-top:0">${cfg.title}</h3><p>${cfg.body}</p><label>Пароль</label><input id="${cfg.id}" type="password" style="width:100%;padding:8px;margin-top:6px;border-radius:6px;border:1px solid #d6d8dd;">`,
    ()=>{ // OK
      const v = document.getElementById(cfg.id).value.trim();
      validateDept(dept, v);
    });
}

// Validate dept password
function validateDept(dept, value){
  if(!value) return showMessage('Нужно ввести пароль.');
  const mapping = {media: 'media', event:'event', strat:'strat', fund:'fund'};
  const key = mapping[dept];
  if(value === PASSWORDS[key]){
    // Open corresponding page
    if(dept === 'media') loadMedia(); showPage(dept+'Page'==='mediaPage'? 'mediaPage': dept+'Page');
    if(dept === 'event') showPage('eventPage');
    if(dept === 'strat') showPage('stratPage');
    if(dept === 'fund') showPage('fundPage');
    closeModal();
  } else {
    showMessage('❌ Неверный пароль, попробуйте снова.');
  }
}

// Modal helpers
function showModal(html, onOk){
  document.getElementById('modalContent').innerHTML = html;
  document.getElementById('modal').style.display = 'flex';
  document.getElementById('modalOk').onclick = ()=>{ if(onOk) onOk(); };
  document.getElementById('modalCancel').onclick = closeModal;
}
function closeModal(){ document.getElementById('modal').style.display = 'none'; }
function showMessage(msg){ showModal('<p>'+msg+'</p>', closeModal); }

// Data storage for media table (localStorage)
const MEDIA_KEY = 'studdiss_media_plan_v1';

function loadMedia(){
  // show page and load rows
  const raw = localStorage.getItem(MEDIA_KEY);
  let rows = [];
  if(raw){
    try{ rows = JSON.parse(raw); } catch(e){ rows = []; }
  } else {
    // seed with one example row
    rows = [
      {date:'2025-10-20', format:'Пост', desc:'Анонс встречи клуба', resp:'Никита', status:'В процессе'}
    ];
  }
  renderMedia(rows);
}

function saveMedia(rows){
  localStorage.setItem(MEDIA_KEY, JSON.stringify(rows));
  showToast('Сохранено в браузере');
}

function renderMedia(rows){
  const tbody = document.getElementById('mediaBody');
  tbody.innerHTML = '';
  rows.forEach((r, idx)=>{
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td contenteditable="true" data-field="date" data-idx="${idx}">${r.date || ''}</td>
      <td contenteditable="true" data-field="format" data-idx="${idx}">${r.format || ''}</td>
      <td contenteditable="true" data-field="desc" data-idx="${idx}">${r.desc || ''}</td>
      <td>
        <select class="inline" data-field="resp" data-idx="${idx}">
          <option ${r.resp==='Никита'?'selected':''}>Никита</option>
          <option ${r.resp==='Юля'?'selected':''}>Юля</option>
        </select>
      </td>
      <td>
        <select class="inline" data-field="status" data-idx="${idx}">
          <option ${r.status==='В процессе'?'selected':''}>В процессе</option>
          <option ${r.status==='Готово'?'selected':''}>Готово</option>
          <option ${r.status==='Отложено'?'selected':''}>Отложено</option>
          <option ${r.status==='Отменено'?'selected':''}>Отменено</option>
        </select>
      </td>
      <td><button class="btn ghost" data-action="delete" data-idx="${idx}">Удалить</button></td>
    `;
    tbody.appendChild(tr);
  });

  // Attach listeners for inline edits and selects and delete
  tbody.querySelectorAll('[contenteditable]').forEach(cell=>{
    cell.onblur = ()=>{
      const idx = parseInt(cell.dataset.idx), field = cell.dataset.field;
      rows[idx][field] = cell.innerText.trim();
      saveMedia(rows);
      renderMedia(rows);
    };
  });
  tbody.querySelectorAll('select').forEach(sel=>{
    sel.onchange = ()=>{
      const idx = parseInt(sel.dataset.idx), field = sel.dataset.field;
      rows[idx][field] = sel.value;
      saveMedia(rows);
      renderMedia(rows);
    };
  });
  tbody.querySelectorAll('button[data-action="delete"]').forEach(btn=>{
    btn.onclick = ()=>{
      const idx = parseInt(btn.dataset.idx);
      if(confirm('Удалить задачу?')){
        rows.splice(idx,1);
        saveMedia(rows);
        renderMedia(rows);
      }
    };
  });

  // Save after rendering to keep storage in sync
  saveMedia(rows);
}

// Add new blank row
function addRow(){
  const raw = localStorage.getItem(MEDIA_KEY);
  let rows = raw ? JSON.parse(raw) : [];
  rows.push({date:'', format:'', desc:'', resp:'Никита', status:'В процессе'});
  saveMedia(rows);
  renderMedia(rows);
}

// Clear media table
function clearMedia(){
  if(confirm('Очистить весь контент-план?')){
    localStorage.removeItem(MEDIA_KEY);
    renderMedia([]);
  }
}

// Toast helper (small temporary message)
let toastTimer = null;
function showToast(msg){
  const existing = document.getElementById('toast');
  if(existing) existing.remove();
  const d = document.createElement('div');
  d.id='toast';
  d.style.position='fixed';
  d.style.right='18px';
  d.style.bottom='18px';
  d.style.background='rgba(11,99,164,0.95)';
  d.style.color='#fff';
  d.style.padding='10px 14px';
  d.style.borderRadius='10px';
  d.style.boxShadow='0 6px 18px rgba(2,6,23,0.2)';
  d.style.zIndex='120';
  d.innerText=msg;
  document.body.appendChild(d);
  if(toastTimer) clearTimeout(toastTimer);
  toastTimer = setTimeout(()=>{ d.remove(); }, 2200);
}

// Logout back to home
function logout(){ showPage('homePage'); showToast('Вы вышли из кабинета'); }

// Utility: show simple message
function showMessageSimple(msg){ alert(msg); }

// Initialize: ensure home visible
showPage('homePage');
</script>

</body>
</html># -
