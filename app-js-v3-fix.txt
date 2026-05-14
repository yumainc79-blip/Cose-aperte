const STORAGE_KEY = "cose-aperte:v1";
const VIEW_KEY = "cose-aperte:view:v1";

const STATUS = {
  OPEN: "Aperta",
  ACTIVE: "In corso",
  BLOCKED: "Bloccata",
  WAITING: "In attesa",
  DECIDE: "Da decidere",
  CLOSED: "Chiusa",
  ARCHIVED: "Archiviata"
};

const AREAS = ["Casa", "Lavoro", "Soldi", "Salute", "App", "Burocrazia", "Relazioni", "Acquisti"];
const ENERGY = ["Bassa", "Media", "Alta"];
const WHEN = ["Oggi", "Questa settimana", "Più avanti", "Senza scadenza"];

const DEFAULT_FIELD_VALUES = new Set([
  "Nuova cosa aperta",
  "Scrivere il prossimo passo minimo",
  "Commercialista 2026",
  "Scrivere per chiedere i documenti",
  "Non so quali documenti servono",
  "Dentista",
  "Chiamare per fissare appuntamento",
  "Meal Prep",
  "Decidere 3 pasti per lunedì",
  "PAC Tracker",
  "Rivedere schermata Andamenti",
  "Bonus psicologo",
  "Mandare un messaggio di follow-up",
  "Manca risposta del paziente",
  "Preparare report",
  "Raccogliere i dati principali",
  "Aggiornare sito",
  "Rivedere la pagina Servizi",
  "Assicurazione casa",
  "Confrontare 2 offerte",
  "Allenamento",
  "Scegliere 2 giorni questa settimana",
  "Visita oculistica",
  "Controllare copertura assicurazione",
  "Aspetto risposta assicurazione",
  "Newsletter",
  "Scrivere bozza introduzione",
  "Organizzare armadio",
  "Scegliere i capi da tenere",
  "Cambio lampadine",
  "Comprare 2 lampadine per cucina",
  "Vecchia pratica archiviata",
  "Ricevuta completata"
]);

const TEMPLATE_VALUES = new Set([
  "Nuova cosa aperta",
  "Scrivere il prossimo passo minimo"
]);

const PLACEHOLDERS = {
  title: "Nuova cosa aperta",
  nextStep: "Scrivere il prossimo passo minimo",
  blocker: "Cosa sta bloccando questa cosa?",
  notes: "Aggiungi dettagli utili, senza trasformarla in un progetto."
};

const icons = {
  check: `<path d="M20 6 9 17l-5-5" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  circleCheck: `<path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/><path d="m9 11 3 3L22 4" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  search: `<circle cx="11" cy="11" r="8" fill="none" stroke="currentColor" stroke-width="2"/><path d="m21 21-4.3-4.3" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  bell: `<path d="M18 8a6 6 0 0 0-12 0c0 7-3 7-3 7h18s-3 0-3-7" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/><path d="M13.73 21a2 2 0 0 1-3.46 0" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  plus: `<path d="M12 5v14M5 12h14" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  inbox: `<path d="M22 12h-6l-2 3h-4l-2-3H2" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/><path d="M5.45 5.11 2 12v6a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2v-6l-3.45-6.89A2 2 0 0 0 16.76 4H7.24a2 2 0 0 0-1.79 1.11Z" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  sun: `<circle cx="12" cy="12" r="4" fill="none" stroke="currentColor" stroke-width="2"/><path d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M4.93 19.07l1.41-1.41M17.66 6.34l1.41-1.41" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  grid: `<rect x="3" y="3" width="7" height="7" rx="1" fill="none" stroke="currentColor" stroke-width="2"/><rect x="14" y="3" width="7" height="7" rx="1" fill="none" stroke="currentColor" stroke-width="2"/><rect x="14" y="14" width="7" height="7" rx="1" fill="none" stroke="currentColor" stroke-width="2"/><rect x="3" y="14" width="7" height="7" rx="1" fill="none" stroke="currentColor" stroke-width="2"/>`,
  list: `<path d="M8 6h13M8 12h13M8 18h13" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/><path d="M3 6h.01M3 12h.01M3 18h.01" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round"/>`,
  hourglass: `<path d="M6 2h12M6 22h12M8 2c0 5 8 5 8 10s-8 5-8 10M16 2c0 5-8 5-8 10s8 5 8 10" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  lock: `<rect x="4" y="11" width="16" height="10" rx="2" fill="none" stroke="currentColor" stroke-width="2"/><path d="M8 11V7a4 4 0 0 1 8 0v4" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  archive: `<path d="M21 8v13H3V8M1 3h22v5H1z" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/><path d="M10 12h4" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  home: `<path d="m3 10 9-7 9 7v10a2 2 0 0 1-2 2h-4v-7H9v7H5a2 2 0 0 1-2-2Z" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  briefcase: `<rect x="2" y="7" width="20" height="14" rx="2" fill="none" stroke="currentColor" stroke-width="2"/><path d="M16 7V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v2M2 13h20" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  money: `<circle cx="12" cy="12" r="10" fill="none" stroke="currentColor" stroke-width="2"/><path d="M12 6v12M15 9.5c-.5-1-1.6-1.5-3-1.5-1.7 0-3 1-3 2.4 0 3.4 6 1.7 6 5.2 0 1.4-1.3 2.4-3 2.4-1.6 0-2.8-.7-3.4-1.8" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  heart: `<path d="M20.8 4.6a5.5 5.5 0 0 0-7.8 0L12 5.6l-1-1a5.5 5.5 0 0 0-7.8 7.8l1 1L12 21l7.8-7.6 1-1a5.5 5.5 0 0 0 0-7.8Z" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  phone: `<rect x="7" y="2" width="10" height="20" rx="2" fill="none" stroke="currentColor" stroke-width="2"/><path d="M12 18h.01" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round"/>`,
  user: `<path d="M20 21a8 8 0 0 0-16 0" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/><circle cx="12" cy="7" r="4" fill="none" stroke="currentColor" stroke-width="2"/>`,
  sparkle: `<path d="m12 3 1.8 5.2L19 10l-5.2 1.8L12 17l-1.8-5.2L5 10l5.2-1.8L12 3ZM19 16l.8 2.2L22 19l-2.2.8L19 22l-.8-2.2L16 19l2.2-.8L19 16ZM5 2l.8 2.2L8 5l-2.2.8L5 8l-.8-2.2L2 5l2.2-.8L5 2Z" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  arrowLeft: `<path d="m15 18-6-6 6-6" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  chevronRight: `<path d="m9 18 6-6-6-6" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  clock: `<circle cx="12" cy="12" r="10" fill="none" stroke="currentColor" stroke-width="2"/><path d="M12 6v6l4 2" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`,
  battery: `<rect x="2" y="7" width="18" height="10" rx="2" fill="none" stroke="currentColor" stroke-width="2"/><path d="M22 11v2M6 11v2M10 11v2" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  calendar: `<rect x="3" y="4" width="18" height="18" rx="2" fill="none" stroke="currentColor" stroke-width="2"/><path d="M16 2v4M8 2v4M3 10h18" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>`,
  target: `<circle cx="12" cy="12" r="10" fill="none" stroke="currentColor" stroke-width="2"/><circle cx="12" cy="12" r="6" fill="none" stroke="currentColor" stroke-width="2"/><circle cx="12" cy="12" r="2" fill="currentColor"/>`,
  trash: `<path d="M3 6h18M8 6V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2M19 6l-1 14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2L5 6M10 11v6M14 11v6" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>`
};

const areaIcons = {
  Casa: "home",
  Lavoro: "briefcase",
  Soldi: "money",
  Salute: "heart",
  App: "phone",
  Burocrazia: "lock",
  Relazioni: "user",
  Acquisti: "archive"
};

const state = {
  items: [],
  view: localStorage.getItem(VIEW_KEY) || "today",
  selectedId: null,
  search: "",
  toast: ""
};

function svg(name, className = "") {
  return `<svg class="${className}" aria-hidden="true" focusable="false" viewBox="0 0 24 24">${icons[name] || icons.circleCheck}</svg>`;
}

function uid() {
  return `${Date.now().toString(36)}-${Math.random().toString(36).slice(2, 8)}`;
}

function nowIso() {
  return new Date().toISOString();
}

function seedItems() {
  const base = [
    { title: "Commercialista 2026", area: "Soldi", status: STATUS.BLOCKED, nextStep: "Scrivere per chiedere i documenti", blocker: "Non so quali documenti servono", energy: "Bassa", minutes: 5, when: "Oggi" },
    { title: "Dentista", area: "Salute", status: STATUS.OPEN, nextStep: "Chiamare per fissare appuntamento", blocker: "", energy: "Bassa", minutes: 5, when: "Oggi" },
    { title: "Meal Prep", area: "Casa", status: STATUS.OPEN, nextStep: "Decidere 3 pasti per lunedì", blocker: "", energy: "Bassa", minutes: 10, when: "Questa settimana" },
    { title: "PAC Tracker", area: "App", status: STATUS.ACTIVE, nextStep: "Rivedere schermata Andamenti", blocker: "", energy: "Media", minutes: 25, when: "Questa settimana" },
    { title: "Bonus psicologo", area: "Burocrazia", status: STATUS.BLOCKED, nextStep: "Mandare un messaggio di follow-up", blocker: "Manca risposta del paziente", energy: "Bassa", minutes: 5, when: "Questa settimana" },
    { title: "Preparare report", area: "Lavoro", status: STATUS.OPEN, nextStep: "Raccogliere i dati principali", blocker: "", energy: "Media", minutes: 30, when: "Questa settimana" },
    { title: "Aggiornare sito", area: "Lavoro", status: STATUS.OPEN, nextStep: "Rivedere la pagina Servizi", blocker: "", energy: "Media", minutes: 20, when: "Più avanti" },
    { title: "Assicurazione casa", area: "Soldi", status: STATUS.DECIDE, nextStep: "Confrontare 2 offerte", blocker: "", energy: "Media", minutes: 20, when: "Questa settimana" },
    { title: "Allenamento", area: "Salute", status: STATUS.OPEN, nextStep: "Scegliere 2 giorni questa settimana", blocker: "", energy: "Bassa", minutes: 5, when: "Oggi" },
    { title: "Visita oculistica", area: "Salute", status: STATUS.WAITING, nextStep: "Controllare copertura assicurazione", blocker: "Aspetto risposta assicurazione", energy: "Bassa", minutes: 10, when: "Più avanti" },
    { title: "Newsletter", area: "Lavoro", status: STATUS.OPEN, nextStep: "Scrivere bozza introduzione", blocker: "", energy: "Media", minutes: 25, when: "Più avanti" },
    { title: "Organizzare armadio", area: "Casa", status: STATUS.OPEN, nextStep: "Scegliere i capi da tenere", blocker: "", energy: "Alta", minutes: 45, when: "Più avanti" },
    { title: "Cambio lampadine", area: "Casa", status: STATUS.OPEN, nextStep: "Comprare 2 lampadine per cucina", blocker: "", energy: "Bassa", minutes: 10, when: "Questa settimana" },
    { title: "Vecchia pratica archiviata", area: "Burocrazia", status: STATUS.ARCHIVED, nextStep: "", blocker: "", energy: "Bassa", minutes: 5, when: "Senza scadenza" },
    { title: "Ricevuta completata", area: "Soldi", status: STATUS.CLOSED, nextStep: "", blocker: "", energy: "Bassa", minutes: 5, when: "Oggi", closedAt: nowIso() }
  ];

  return base.map((item, index) => ({
    id: uid(),
    notes: "",
    createdAt: nowIso(),
    updatedAt: nowIso(),
    order: index,
    ...item
  }));
}

function loadItems() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return seedItems();
    const parsed = JSON.parse(raw);
    return Array.isArray(parsed) ? parsed.filter((item) => !item.isDraft) : seedItems();
  } catch (error) {
    console.warn("Impossibile leggere il salvataggio locale", error);
    return seedItems();
  }
}

function saveItems() {
  const persistableItems = state.items.filter((item) => !item.isDraft);
  localStorage.setItem(STORAGE_KEY, JSON.stringify(persistableItems));
}

function discardSelectedDraft() {
  if (!state.selectedId) return;
  const item = state.items.find((entry) => entry.id === state.selectedId);
  if (item?.isDraft) {
    state.items = state.items.filter((entry) => entry.id !== state.selectedId);
  }
}

function setView(view) {
  discardSelectedDraft();
  state.view = view;
  state.selectedId = null;
  localStorage.setItem(VIEW_KEY, view);
  render();
}

function showToast(message) {
  state.toast = message;
  renderToast();
  window.clearTimeout(showToast.timer);
  showToast.timer = window.setTimeout(() => {
    state.toast = "";
    renderToast();
  }, 2400);
}

function normalizeAreaClass(area) {
  return area.toLowerCase().replaceAll(" ", "-");
}

function isActiveItem(item) {
  return ![STATUS.CLOSED, STATUS.ARCHIVED].includes(item.status);
}

function matchesSearch(item) {
  const q = state.search.trim().toLowerCase();
  if (!q) return true;
  return [item.title, item.area, item.status, item.nextStep, item.blocker, item.notes]
    .filter(Boolean)
    .join(" ")
    .toLowerCase()
    .includes(q);
}

function visibleItems() {
  return state.items.filter(matchesSearch).filter((item) => {
    if (state.view === "today") return isActiveItem(item) && ["Oggi", "Questa settimana"].includes(item.when);
    if (state.view === "all") return item.status !== STATUS.ARCHIVED;
    if (state.view === "areas") return isActiveItem(item);
    if (state.view === "waiting") return item.status === STATUS.WAITING;
    if (state.view === "blocked") return item.status === STATUS.BLOCKED;
    if (state.view === "archive") return [STATUS.ARCHIVED, STATUS.CLOSED].includes(item.status);
    return true;
  });
}

function priorityScore(item) {
  const statusWeight = {
    [STATUS.BLOCKED]: 0,
    [STATUS.OPEN]: 1,
    [STATUS.ACTIVE]: 2,
    [STATUS.DECIDE]: 3,
    [STATUS.WAITING]: 4,
    [STATUS.CLOSED]: 9,
    [STATUS.ARCHIVED]: 10
  }[item.status] ?? 5;
  const whenWeight = { Oggi: 0, "Questa settimana": 1, "Più avanti": 3, "Senza scadenza": 4 }[item.when] ?? 4;
  const energyWeight = { Bassa: 0, Media: 1, Alta: 2 }[item.energy] ?? 1;
  return statusWeight * 100 + whenWeight * 20 + energyWeight * 5 + Number(item.minutes || 0);
}

function sortItems(list) {
  return [...list].sort((a, b) => priorityScore(a) - priorityScore(b));
}

function getCounts() {
  const active = state.items.filter(isActiveItem);
  const now = new Date();
  return {
    open: active.length,
    closedThisMonth: state.items.filter((item) => {
      if (item.status !== STATUS.CLOSED || !item.closedAt) return false;
      const closed = new Date(item.closedAt);
      return closed.getFullYear() === now.getFullYear() && closed.getMonth() === now.getMonth();
    }).length,
    blocked: state.items.filter((item) => item.status === STATUS.BLOCKED).length,
    waiting: state.items.filter((item) => item.status === STATUS.WAITING).length,
    today: state.items.filter((item) => isActiveItem(item) && item.when === "Oggi").length
  };
}

function getFocusItems() {
  return sortItems(state.items.filter((item) => isActiveItem(item) && ["Oggi", "Questa settimana"].includes(item.when))).slice(0, 3);
}

function areaForColumns() {
  const preferred = ["Casa", "Lavoro", "Soldi", "Salute"];
  const activeAreas = [...new Set(state.items.filter(isActiveItem).map((item) => item.area))];
  return [...preferred, ...activeAreas.filter((area) => !preferred.includes(area))].slice(0, 4);
}

function createNewItem(area = "Casa") {
  const item = {
    id: uid(),
    title: "",
    area,
    status: STATUS.OPEN,
    nextStep: "",
    blocker: "",
    notes: "",
    energy: "Bassa",
    minutes: 5,
    when: "Oggi",
    isTemplate: true,
    isDraft: true,
    createdAt: nowIso(),
    updatedAt: nowIso(),
    order: state.items.length
  };
  state.items.unshift(item);
  state.selectedId = item.id;
  render();
}

function openDetail(id) {
  state.selectedId = id;
  render();
}

function updateItem(id, patch) {
  const index = state.items.findIndex((item) => item.id === id);
  if (index === -1) return;
  const previous = state.items[index];
  const nextStatus = patch.status || previous.status;
  const closedAt = nextStatus === STATUS.CLOSED && previous.status !== STATUS.CLOSED ? nowIso() : previous.closedAt;
  state.items[index] = { ...previous, ...patch, closedAt, updatedAt: nowIso() };
  saveItems();
}

function deleteItem(id) {
  state.items = state.items.filter((item) => item.id !== id);
  saveItems();
  state.selectedId = null;
  render();
  showToast("Cosa eliminata.");
}

function reduceToNextStep(item) {
  const title = item.title.trim() || "questa cosa";
  const blocker = item.blocker.trim();

  let suggestion;
  if (item.status === STATUS.BLOCKED && blocker) {
    suggestion = `Chiarire il blocco: ${blocker}`;
  } else if (item.status === STATUS.WAITING) {
    suggestion = `Verificare se posso sollecitare o aspettare su: ${title}`;
  } else if (item.status === STATUS.DECIDE) {
    suggestion = `Scrivere le 2 opzioni principali per decidere su: ${title}`;
  } else if (!item.nextStep.trim()) {
    suggestion = `Aprire ${title} e scrivere solo il primo micro-passaggio`;
  } else {
    suggestion = item.nextStep.length > 64
      ? item.nextStep.slice(0, 61).trim() + "..."
      : item.nextStep;
    suggestion = `Fare solo questo: ${suggestion}`;
  }

  updateItem(item.id, { nextStep: suggestion, minutes: Math.min(Number(item.minutes || 10), 10), energy: "Bassa" });
  render();
  showToast("Prossimo passo reso più piccolo.");
}

function renderAppChrome(inner) {
  const navItems = [
    ["today", "Oggi", "sun"],
    ["all", "Tutte", "list"],
    ["areas", "Aree", "grid"],
    ["waiting", "In attesa", "hourglass"],
    ["blocked", "Bloccate", "lock"],
    ["archive", "Archivio", "archive"]
  ];
  const bottomItems = [
    ["all", "Inbox", "inbox"],
    ["today", "Oggi", "calendar"],
    ["areas", "Aree", "grid"],
    ["archive", "Archivio", "archive"]
  ];

  return `
    <aside class="sidebar">
      <div class="brand">
        <div class="logo">${svg("circleCheck")}</div>
        <div>
          <div class="brand-title">Cose Aperte</div>
          <div class="brand-subtitle">Un passo minimo alla volta</div>
        </div>
      </div>
      <nav class="nav-list" aria-label="Sezioni principali">
        ${navItems.map(([view, label, icon]) => `
          <button class="nav-button ${state.view === view && !state.selectedId ? "active" : ""}" data-view="${view}">
            ${svg(icon)}<span>${label}</span>
          </button>
        `).join("")}
      </nav>
      <div class="nav-spacer"></div>
      <div class="sidebar-tip"><span class="tip-leaf">🌿</span>Un passo alla volta,<br>è così che le cose<br>prendono forma.</div>
    </aside>
    <main class="main">
      ${inner}
    </main>
    <nav class="bottom-nav" aria-label="Navigazione mobile">
      ${bottomItems.map(([view, label, icon]) => `
        <button class="${state.view === view && !state.selectedId ? "active" : ""}" data-view="${view}">${svg(icon)}<span>${label}</span></button>
      `).join("")}
    </nav>
    <div id="toast" class="toast" role="status"></div>
  `;
}

function renderDashboard() {
  const counts = getCounts();
  const columns = state.view === "areas" ? AREAS : areaForColumns();
  const focus = getFocusItems();
  const items = visibleItems();

  return renderAppChrome(`
    <div class="mobile-topbar">
      <h1>Cose Aperte</h1>
      <button class="icon-button" aria-label="Notifiche">${svg("bell")}</button>
    </div>

    <header class="page-header">
      <div class="header-copy">
        <h1>${pageTitle()}</h1>
        <p>Tutto ciò che hai in sospeso, con il prossimo passo minimo.</p>
      </div>
      <div class="header-actions">
        <div class="search-wrap">
          ${svg("search")}
          <input class="search-input" id="searchInput" type="search" placeholder="Cerca una cosa aperta" value="${escapeAttr(state.search)}" />
        </div>
        <button class="primary-button" id="newItemBtn">${svg("plus")} Nuova</button>
      </div>
    </header>

    <section class="summary-grid" aria-label="Riepilogo">
      ${summaryCard("Oggi", counts.today, "sun", "today")}
      ${summaryCard("Chiuse questo mese", counts.closedThisMonth, "circleCheck", "closed")}
      ${summaryCard("Bloccate", counts.blocked, "lock", "blocked")}
      ${summaryCard("In attesa", counts.waiting, "hourglass", "waiting")}
    </section>

    <section class="mobile-sections">
      ${renderMobileSections()}
    </section>

    <section class="content-grid">
      <div class="board" aria-label="Panoramica per aree">
        ${columns.map((area) => renderColumn(area)).join("")}
      </div>
      ${renderFocusPanel(focus)}
    </section>
  `);
}

function pageTitle() {
  const map = {
    today: "Panoramica",
    all: "Tutte le cose aperte",
    areas: "Aree",
    waiting: "In attesa",
    blocked: "Bloccate",
    archive: "Archivio"
  };
  return map[state.view] || "Panoramica";
}

function summaryCard(label, value, icon, extraClass = "") {
  return `
    <article class="summary-card ${extraClass}">
      <div class="summary-label">${label}</div>
      <div class="summary-value"><span>${value}</span>${svg(icon)}</div>
    </article>
  `;
}

function renderColumn(area) {
  const areaItems = sortItems(visibleItems().filter((item) => item.area === area)).slice(0, 4);
  return `
    <section class="column">
      <div class="column-header">
        <span class="column-title">${svg(areaIcons[area] || "grid")} ${area}</span>
        <small>${state.items.filter((item) => isActiveItem(item) && item.area === area).length}</small>
      </div>
      <div class="card-list">
        ${areaItems.map(renderTaskCard).join("") || `<div class="empty-state"><strong>Nessuna cosa</strong>Aggiungi il prossimo passo.</div>`}
      </div>
      <button class="add-card-button" data-new-area="${escapeAttr(area)}">+ Nuova cosa</button>
    </section>
  `;
}

function renderTaskCard(item) {
  return `
    <button class="task-card" data-open-id="${escapeAttr(item.id)}">
      <div class="task-card-title-row">
        <h3 class="task-title">${escapeHtml(item.title || PLACEHOLDERS.title)}</h3>
        ${statusDot(item)}
      </div>
      <p class="task-step">${escapeHtml(item.nextStep || "Definisci il prossimo passo minimo")}</p>
      <div class="task-meta">
        ${badge(item.area)}
        <span class="badge">${Number(item.minutes || 5)} min</span>
      </div>
    </button>
  `;
}


function renderMobileSections() {
  const items = sortItems(visibleItems());
  if (state.view === "today") {
    const today = sortItems(state.items.filter((item) => isActiveItem(item) && item.when === "Oggi" && matchesSearch(item))).slice(0, 6);
    const small = sortItems(state.items.filter((item) => isActiveItem(item) && item.energy === "Bassa" && item.when !== "Oggi" && matchesSearch(item))).slice(0, 6);
    const blocked = sortItems(state.items.filter((item) => item.status === STATUS.BLOCKED && matchesSearch(item))).slice(0, 6);
    return [
      mobileSection("Da fare oggi", today),
      mobileSection("Prossimi passi piccoli", small),
      mobileSection("Bloccate", blocked),
      today.length + small.length + blocked.length === 0 ? emptyState() : ""
    ].join("");
  }

  if (state.view === "areas") {
    return renderMobileAreaSections(items);
  }

  return mobileSection(pageTitle(), items) || emptyState();
}

function renderMobileAreaSections(items) {
  return AREAS.map((area) => {
    const areaItems = sortItems(items.filter((item) => item.area === area));
    const count = state.items.filter((item) => isActiveItem(item) && item.area === area).length;
    const preview = areaItems.slice(0, 5).map(renderMobileCard).join("");

    return `
      <section class="section area-section">
        <div class="area-section-head">
          <div class="area-section-title">
            <span class="area-section-icon">${svg(areaIcons[area] || "grid")}</span>
            <span>${escapeHtml(area)}</span>
            <small>${count}</small>
          </div>
          <button class="mini-add-button" data-new-area="${escapeAttr(area)}">+ Nuova</button>
        </div>
        ${preview || `<div class="empty-state compact"><strong>Nessuna cosa aperta.</strong>Puoi aggiungerne una in questa area.</div>`}
      </section>
    `;
  }).join("");
}

function mobileSection(title, list) {
  if (!list.length) return "";
  return `
    <section class="section">
      <h2 class="section-title">${title}</h2>
      ${list.map(renderMobileCard).join("")}
    </section>
  `;
}

function renderMobileCard(item) {
  const iconName = areaIcons[item.area] || "circleCheck";
  return `
    <button class="mobile-card" data-open-id="${escapeAttr(item.id)}">
      <span class="mobile-card-icon">${svg(iconName)}</span>
      <span>
        <span class="mobile-card-title">${escapeHtml(item.title || PLACEHOLDERS.title)}</span>
        <span class="mobile-card-step">${escapeHtml(item.nextStep || "Definisci il prossimo passo minimo")}</span>
      </span>
      ${badge(item.area)}
    </button>
  `;
}

function renderFocusPanel(focus) {
  return `
    <aside class="focus-panel">
      <div class="focus-head">
        <h2>Focus di oggi ${svg("target")}</h2>
        <p>3 passi minimi per fare progressi senza riaprire tutto.</p>
      </div>
      <div class="focus-items">
        ${focus.map((item) => `
          <button class="focus-item" data-open-id="${escapeAttr(item.id)}">
            <span class="focus-icon">${svg(areaIcons[item.area] || "circleCheck")}</span>
            <span>
              <span class="focus-title">${escapeHtml(item.title)}</span>
              <span class="focus-step">${escapeHtml(item.nextStep || "Definisci il prossimo passo minimo")}</span>
              <span class="focus-time">${Number(item.minutes || 5)} min</span>
            </span>
          </button>
        `).join("") || `<div class="empty-state"><strong>Nessun focus</strong>Aggiungi una cosa per oggi.</div>`}
      </div>
      <div class="focus-footer"><button class="secondary-button" data-view="all">Vedi tutti</button></div>
    </aside>
  `;
}

function badge(area) {
  return `<span class="badge ${normalizeAreaClass(area)}">${escapeHtml(area)}</span>`;
}

function statusDot(item) {
  const cls = item.status === STATUS.BLOCKED ? "blocked" : item.status === STATUS.WAITING ? "waiting" : item.status === STATUS.CLOSED ? "closed" : "";
  return `<span class="status-dot ${cls}" title="${escapeAttr(item.status)}"></span>`;
}

function emptyState() {
  return `<div class="empty-state"><strong>Niente da mostrare.</strong>Prova a cambiare sezione o aggiungi una nuova cosa aperta.</div>`;
}

function renderDetail() {
  const item = state.items.find((entry) => entry.id === state.selectedId);
  if (!item) {
    state.selectedId = null;
    return renderDashboard();
  }

  const titleValue = shouldShowAsPlaceholder(item.title, "title") ? "" : item.title;
  const stepValue = shouldShowAsPlaceholder(item.nextStep, "nextStep") ? "" : item.nextStep;
  const blockerValue = shouldShowAsPlaceholder(item.blocker, "blocker") ? "" : item.blocker;
  const notesValue = shouldShowAsPlaceholder(item.notes, "notes") ? "" : item.notes;

  return renderAppChrome(`
    <section class="detail-layout">
      <button class="back-button" id="backBtn">${svg("arrowLeft")} Torna</button>
      <article class="detail-card">
        <div class="detail-top">
          <div style="min-width:0; flex:1">
            <input class="detail-title-input" id="titleInput" value="${escapeAttr(titleValue)}" placeholder="${escapeAttr(PLACEHOLDERS.title)}" aria-label="Titolo" autocomplete="off" />
          </div>
          <button class="icon-button" id="deleteBtn" aria-label="Elimina">${svg("trash")}</button>
        </div>

        <div class="form-grid">
          <div class="form-field">
            <label for="areaSelect">Area</label>
            <select class="select" id="areaSelect">${AREAS.map((area) => `<option ${item.area === area ? "selected" : ""}>${area}</option>`).join("")}</select>
          </div>
          <div class="form-field">
            <label for="statusSelect">Stato</label>
            <select class="select" id="statusSelect">${Object.values(STATUS).map((status) => `<option ${item.status === status ? "selected" : ""}>${status}</option>`).join("")}</select>
          </div>

          <div class="form-field full">
            <label for="stepInput">Prossimo passo minimo</label>
            <textarea class="textarea" id="stepInput" maxlength="220" placeholder="${escapeAttr(PLACEHOLDERS.nextStep)}">${escapeHtml(stepValue || "")}</textarea>
          </div>

          <div class="form-field full">
            <label for="blockerInput">Bloccante</label>
            <textarea class="textarea" id="blockerInput" maxlength="220" placeholder="${escapeAttr(PLACEHOLDERS.blocker)}">${escapeHtml(blockerValue || "")}</textarea>
          </div>

          <div class="form-field">
            <label>Tempo stimato</label>
            <div class="chip-row" id="minutesChips">
              ${[5, 10, 20, 30, 45].map((min) => `<button class="filter-chip ${Number(item.minutes) === min ? "active" : ""}" data-minutes="${min}">${min} min</button>`).join("")}
            </div>
          </div>

          <div class="form-field">
            <label>Energia</label>
            <div class="chip-row" id="energyChips">
              ${ENERGY.map((energy) => `<button class="filter-chip ${item.energy === energy ? "active" : ""}" data-energy="${energy}">${energy} energia</button>`).join("")}
            </div>
          </div>

          <div class="form-field full">
            <label>Quando</label>
            <div class="chip-row" id="whenChips">
              ${WHEN.map((when) => `<button class="filter-chip ${item.when === when ? "active" : ""}" data-when="${when}">${when}</button>`).join("")}
            </div>
          </div>

          <div class="form-field full">
            <button class="helper-card" id="reduceBtn">
              <span class="helper-icon">${svg("sparkle")}</span>
              <span>
                <span class="helper-title">Riduci al prossimo passo minimo</span>
                <span class="helper-copy">Trasforma la cosa in un'azione semplice e concreta da fare subito.</span>
              </span>
              <span class="chevron">${svg("chevronRight")}</span>
            </button>
          </div>

          <div class="form-field full">
            <label for="notesInput">Note</label>
            <textarea class="textarea" id="notesInput" maxlength="800" placeholder="${escapeAttr(PLACEHOLDERS.notes)}">${escapeHtml(notesValue || "")}</textarea>
          </div>
        </div>

        <div class="form-actions">
          <button class="primary-button" id="saveBtn">${svg("check")} Salva</button>
          <button class="secondary-button" id="archiveBtn">Archivia</button>
          <button class="secondary-button" id="closeBtn">Chiudi</button>
        </div>
      </article>
    </section>
  `);
}

function renderToast() {
  const toast = document.getElementById("toast");
  if (!toast) return;
  toast.textContent = state.toast;
  toast.classList.toggle("show", Boolean(state.toast));
}

function render() {
  const app = document.getElementById("app");
  app.innerHTML = state.selectedId ? renderDetail() : renderDashboard();
  bindEvents();
  renderToast();
}

function bindEvents() {
  document.querySelectorAll("[data-view]").forEach((el) => {
    el.addEventListener("click", () => setView(el.dataset.view));
  });

  document.querySelectorAll("[data-open-id]").forEach((el) => {
    el.addEventListener("click", () => openDetail(el.dataset.openId));
  });

  document.querySelectorAll("[data-new-area]").forEach((el) => {
    el.addEventListener("click", () => createNewItem(el.dataset.newArea));
  });

  const newBtn = document.getElementById("newItemBtn");
  if (newBtn) newBtn.addEventListener("click", () => createNewItem());

  const search = document.getElementById("searchInput");
  if (search) {
    search.addEventListener("input", (event) => {
      state.search = event.target.value;
      render();
      const nextSearch = document.getElementById("searchInput");
      if (nextSearch) {
        nextSearch.focus();
        nextSearch.setSelectionRange(state.search.length, state.search.length);
      }
    });
  }

  const backBtn = document.getElementById("backBtn");
  if (backBtn) backBtn.addEventListener("click", () => { discardSelectedDraft(); state.selectedId = null; render(); });

  const saveBtn = document.getElementById("saveBtn");
  if (saveBtn) saveBtn.addEventListener("click", saveAndGoToInbox);

  const closeBtn = document.getElementById("closeBtn");
  if (closeBtn) closeBtn.addEventListener("click", () => {
    saveCurrentDetail({ status: STATUS.CLOSED }, false);
    state.selectedId = null;
    state.view = "all";
    localStorage.setItem(VIEW_KEY, "all");
    render();
    showToast("Cosa chiusa.");
  });

  const archiveBtn = document.getElementById("archiveBtn");
  if (archiveBtn) archiveBtn.addEventListener("click", () => {
    saveCurrentDetail({ status: STATUS.ARCHIVED }, false);
    state.selectedId = null;
    state.view = "all";
    localStorage.setItem(VIEW_KEY, "all");
    render();
    showToast("Cosa archiviata.");
  });

  const deleteBtn = document.getElementById("deleteBtn");
  if (deleteBtn) deleteBtn.addEventListener("click", () => {
    const item = state.items.find((entry) => entry.id === state.selectedId);
    const ok = window.confirm(`Eliminare "${item?.title || "questa cosa"}"?`);
    if (ok) deleteItem(state.selectedId);
  });

  const reduceBtn = document.getElementById("reduceBtn");
  if (reduceBtn) reduceBtn.addEventListener("click", (event) => {
    event.preventDefault();
    saveCurrentDetail({}, false);
    const item = state.items.find((entry) => entry.id === state.selectedId);
    if (item) reduceToNextStep(item);
  });

  document.querySelectorAll("[data-minutes]").forEach((el) => {
    el.addEventListener("click", (event) => {
      event.preventDefault();
      updateItem(state.selectedId, { minutes: Number(el.dataset.minutes) });
      render();
    });
  });

  document.querySelectorAll("[data-energy]").forEach((el) => {
    el.addEventListener("click", (event) => {
      event.preventDefault();
      updateItem(state.selectedId, { energy: el.dataset.energy });
      render();
    });
  });

  document.querySelectorAll("[data-when]").forEach((el) => {
    el.addEventListener("click", (event) => {
      event.preventDefault();
      updateItem(state.selectedId, { when: el.dataset.when });
      render();
    });
  });

  bindDefaultTextAutoClear();
}

function bindDefaultTextAutoClear() {
  ["titleInput", "stepInput", "blockerInput", "notesInput"].forEach((id) => {
    const el = document.getElementById(id);
    if (!el) return;

    const clearDefault = () => {
      const currentValue = el.value.trim();
      if (!currentValue || !DEFAULT_FIELD_VALUES.has(currentValue)) return;

      el.value = "";
      el.dataset.defaultCleared = "true";
    };

    // pointerdown/touchstart anticipano la selezione nativa del testo su mobile.
    // focus resta come fallback per tastiera, desktop e browser meno prevedibili.
    el.addEventListener("pointerdown", clearDefault, { passive: true });
    el.addEventListener("touchstart", clearDefault, { passive: true });
    el.addEventListener("focus", clearDefault);
  });
}

function shouldShowAsPlaceholder(value, field) {
  const text = String(value || "").trim();
  if (!text) return false;
  return text === PLACEHOLDERS[field] || TEMPLATE_VALUES.has(text);
}

function cleanFieldValue(value) {
  const text = String(value || "").trim();
  return DEFAULT_FIELD_VALUES.has(text) ? "" : text;
}

function saveCurrentDetail(extraPatch = {}, leaveDetail = true) {
  if (!state.selectedId) return;
  const title = cleanFieldValue(document.getElementById("titleInput")?.value);
  const patch = {
    title: title || "Senza titolo",
    area: document.getElementById("areaSelect")?.value || "Casa",
    status: document.getElementById("statusSelect")?.value || STATUS.OPEN,
    nextStep: cleanFieldValue(document.getElementById("stepInput")?.value),
    blocker: cleanFieldValue(document.getElementById("blockerInput")?.value),
    notes: cleanFieldValue(document.getElementById("notesInput")?.value),
    isTemplate: false,
    isDraft: false,
    ...extraPatch
  };
  updateItem(state.selectedId, patch);
  if (leaveDetail) showToast("Salvato in locale.");
}

function saveAndGoToInbox() {
  saveCurrentDetail({}, false);
  state.selectedId = null;
  state.view = "all";
  localStorage.setItem(VIEW_KEY, "all");
  render();
  showToast("Salvato in Inbox.");
}

function escapeHtml(value) {
  return String(value ?? "")
    .replaceAll("&", "&amp;")
    .replaceAll("<", "&lt;")
    .replaceAll(">", "&gt;")
    .replaceAll('"', "&quot;")
    .replaceAll("'", "&#039;");
}

function escapeAttr(value) {
  return escapeHtml(value).replaceAll("`", "&#096;");
}

function registerServiceWorker() {
  if (!("serviceWorker" in navigator)) return;
  window.addEventListener("load", () => {
    navigator.serviceWorker.register("sw.js").catch((error) => {
      console.info("Service worker non registrato", error);
    });
  });
}

state.items = loadItems();
render();
registerServiceWorker();
