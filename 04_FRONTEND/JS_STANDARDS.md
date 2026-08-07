# ⚡ JavaScript Yazım Standartları

> **BeeMaster AI JavaScript kuralları. Vanilla ES6+, framework yok.**

---

## Modül Pattern'i

```js
// Her modül aynı pattern'i kullanır
const ModuleName = {
  // Render — DOM'a yaz
  render(container) {
    container.innerHTML = this.template();
    this.attachEvents();
  },
  
  // Template — HTML string döndür
  template() {
    const data = BM.Storage.state.items;
    if (!data.length) return EmptyState('Henüz veri yok', 'Ekle', () => this.showForm());
    return data.map(item => this.itemCard(item)).join('');
  },
  
  // Events — DOM event listener'ları
  attachEvents() {
    // querySelector ile bağla
  },
  
  // Actions — async CRUD
  async add(data) { /* localStorage + cloud */ },
  async update(id, data) { /* ... */ },
  async delete(id) { /* ... */ }
};
```

## Adlandırma

```js
// camelCase — değişkenler, fonksiyonlar
const hiveCount = 0;
function calculateHealth() {}

// PascalCase — sınıflar, modüller
class HiveManager {}
const ApiaryModule = {};

// UPPER_SNAKE — sabitler
const MAX_HIVE_COUNT = 100;
const API_URL = '...';
```

## Async/Await (Promise değil)

```js
// ✓ DOĞRU
async function loadHives() {
  try {
    const hives = await sbFetch('/rest/v1/hives?select=*');
    BM.Storage.state.hives = hives;
    renderHiveList();
  } catch (err) {
    console.error('Kovanlar yüklenemedi:', err);
    // localStorage fallback
    BM.Storage.state.hives = JSON.parse(localStorage.getItem('hives') || '[]');
  }
}

// ❌ YANLIŞ
function loadHives() {
  fetch('/api/hives')
    .then(r => r.json())
    .then(data => { ... })
    .catch(err => { ... });
}
```

## DOM Manipülasyonu

```js
// Template literal ile HTML üret
function HiveCard(hive) {
  return `
    <div class="hive-card" data-id="${hive.id}">
      <h3>${escapeHtml(hive.name)}</h3>
    </div>
  `;
}

// XSS koruması
function escapeHtml(str) {
  const div = document.createElement('div');
  div.textContent = str;
  return div.innerHTML;
}
```

## Event Delegation

```js
// Listede event delegation kullan
function attachEvents() {
  document.getElementById('hive-list').onclick = (e) => {
    const card = e.target.closest('.hive-card');
    if (!card) return;
    
    if (e.target.matches('.btn-delete')) {
      this.deleteHive(card.dataset.id);
    } else {
      App.navigate('hive', card.dataset.id);
    }
  };
}
```

## Hata Yönetimi

```js
// Her async fonksiyonda try/catch
async function saveData(key, data) {
  try {
    // Her zaman localStorage'a yaz
    localStorage.setItem(key, JSON.stringify(data));
    
    // Cloud denenir
    if (BM.Storage.state.isCloud) {
      await sbFetch(`/rest/v1/${key}`, {
        method: 'POST',
        body: JSON.stringify(data)
      });
    }
  } catch (err) {
    console.warn(`Cloud sync başarısız (${key}):`, err.message);
    // Sessiz hata — local veri güvende
  }
}
```

## Yasaklı Pattern'ler

- ❌ `var` — `const` veya `let` kullan
- ❌ `==` — `===` kullan
- ❌ `eval()` / `new Function()`
- ❌ `innerHTML` XSS kontrolsüz — `escapeHtml()` ile
- ❌ Callback hell — async/await kullan
- ❌ Global değişken — `BM.Storage.state` üzerinden
- ❌ `console.log` production'da — `console.debug` kullan
- ❌ jQuery, Lodash, Moment — vanilla JS yeterli
