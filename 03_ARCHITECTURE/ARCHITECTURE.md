# 🏗️ Mimari

> **BeeMaster AI sistem mimarisi. Tüm teknik kararların temeli.**

---

## Mimari Felsefe

BeeMaster AI, **monolith PWA** mimarisini benimser. Mikroservis yok, framework yok, build step yok. Tek HTML dosyası, tek JavaScript bundle'ı, tek CSS bloğu.

**Neden:**
- Basitlik en büyük özelliktir
- Her eklenen katman bir kırılma noktasıdır
- AI agent'lar basit kodda daha az hata yapar
- PWA offline çalışma için sadelik şart

## Sistem Katmanları

```
┌──────────────────────────────────────────┐
│              KULLANICI                    │
│    (Tarayıcı — Chrome/Safari/Firefox)     │
└──────────────┬───────────────────────────┘
               │
┌──────────────▼───────────────────────────┐
│           PWA SHELL                       │
│  ┌──────────────────────────────────┐    │
│  │  Service Worker                  │    │
│  │  (Cache-First, Offline Fallback) │    │
│  └──────────────────────────────────┘    │
│  ┌──────────────────────────────────┐    │
│  │  index.html (Tek dosya)          │    │
│  │  ├── CSS (inline)                │    │
│  │  ├── HTML (SPA shell)            │    │
│  │  └── JS (App + Modüller)         │    │
│  └──────────────────────────────────┘    │
└──────────────┬───────────────────────────┘
               │
       ┌───────┴───────┐
       │               │
┌──────▼──────┐ ┌──────▼──────┐
│ localStorage│ │  Supabase   │
│ (Offline)   │ │  (Online)   │
└─────────────┘ └─────────────┘
```

## Veri Akışı

```
1. Kullanıcı etkileşimi
   ↓
2. App modülü olayı yakalar
   ↓
3. BM.Storage'a yaz (her zaman localStorage'a)
   ↓
4. UI güncellenir (anlık, optimistic)
   ↓
5. Cloud sync denenir (Supabase)
   ├── Başarılı → veri bulutta
   └── Başarısız → veri local'de, sonra sync
```

## State Yönetimi

```js
// Global state — tek kaynak
BM.Storage.state = {
  apiaries: [],
  hives: [],
  queens: [],
  frames: [],
  inspections: [],
  harvests: [],
  feedings: [],
  treatments: [],
  diseases: [],
  inventory: [],
  // UI state
  currentUser: null,
  currentPage: 'dashboard',
  isCloud: false,
  sidebarOpen: false,
  activeModal: null
};
```

## Modül Mimarisi

```js
// Her modül aynı pattern'i takip eder
const HiveModule = {
  // State (BM.Storage.state üzerinden)
  
  // Render
  render(container) {
    container.innerHTML = this.template();
    this.attachEvents();
  },
  
  // Template
  template() {
    const hives = BM.Storage.state.hives;
    if (!hives.length) return EmptyState('Henüz kovan eklenmemiş');
    return hives.map(h => HiveCard(h)).join('');
  },
  
  // Events
  attachEvents() {
    document.querySelectorAll('.hive-card').forEach(card => {
      card.onclick = () => this.openDetail(card.dataset.id);
    });
  },
  
  // Actions
  async addHive(data) { /* ... */ },
  async deleteHive(id) { /* ... */ },
  openDetail(id) { App.navigate('hive', id); }
};
```

## Routing (SPA)

```js
// Hash-based routing, framework yok
window.onhashchange = () => App.route();

App.route = function() {
  const [page, id] = location.hash.slice(1).split('/');
  const module = MODULES[page] || MODULES.dashboard;
  module.render(document.getElementById('main-content'));
};
```

## Deployment Mimarisi

```
GitHub (ilkerocal/beemaster-ai)
    │
    │ git push main
    ▼
Vercel (otomatik deploy)
    │
    │ CDN + SSL
    ▼
beemaster-ai.vercel.app
    │
    ├── index.html (PWA shell)
    ├── sw.js (Service Worker)
    └── supabase.co (API)
```

---

## Mimari Kararlar

Detaylı karar kayıtları için: `03_ARCHITECTURE/DECISIONS/`

| ID | Karar | Gerekçe |
|----|-------|---------|
| DEC-0001 | PWA (App Store yok) | Anında güncelleme, düşük maliyet, offline |
| DEC-0002 | Supabase (PostgreSQL) | Ücretsiz tier, RLS, gerçek zamanlı |
| DEC-0003 | Inline bundle (tek dosya) | Basit deploy, kolay cache, az bağımlılık |
| DEC-0004 | Framework yok (Vanilla JS) | Küçük bundle, AI uyumlu, hızlı |
