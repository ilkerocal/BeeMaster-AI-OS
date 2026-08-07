# COMP-0005: Hive Card (Kovan Kartı)

**Kategori:** Domain
**Durum:** Active

---

## Kullanım

Kovan listesinde her kovan için gösterilen kart bileşeni.

## HTML

```html
<div class="hive-card" data-hive-id="1" onclick="App.navigate('hive', '1')">
  <div class="hive-card-header">
    <div class="hive-info">
      <h3 class="hive-name">Bahçe Kovanı 1</h3>
      <span class="hive-strain">Karniyol</span>
    </div>
    <div class="hive-status">
      <span class="status-dot online"></span>
      <span>Aktif</span>
    </div>
  </div>
  
  <div class="hive-card-body">
    <div class="hive-stats">
      <div class="hive-stat">
        <span class="stat-value">8/12</span>
        <span class="stat-label">Çerçeve</span>
      </div>
      <div class="hive-stat">
        <span class="stat-value">2024</span>
        <span class="stat-label">Kraliçe</span>
      </div>
      <div class="hive-stat">
        <span class="stat-value">12 kg</span>
        <span class="stat-label">Son Hasat</span>
      </div>
    </div>
    
    <!-- Health Ring -->
    <div class="hive-health">
      <svg class="health-ring" viewBox="0 0 60 60">
        <circle class="ring-bg" cx="30" cy="30" r="24"/>
        <circle class="ring-fill" cx="30" cy="30" r="24" 
                stroke-dasharray="151" stroke-dashoffset="30"/>
        <text x="30" y="34" class="ring-text">80</text>
      </svg>
      <span class="health-label">Sağlık</span>
    </div>
  </div>
  
  <div class="hive-card-footer">
    <span class="hive-location">
      <svg class="icon icon-sm"><use href="#icon-map-pin"/></svg>
      Bahçe Arılığı
    </span>
    <span class="hive-last-inspection">Son muayene: 3 gün önce</span>
  </div>
</div>
```

## CSS

```css
.hive-card {
  background: var(--color-bg-card);
  border: var(--border-card);
  border-left: 3px solid var(--color-primary);
  border-radius: var(--radius-lg);
  padding: var(--space-4);
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease-default);
}
.hive-card:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-lg);
  border-left-color: var(--color-primary-light);
}

.hive-card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: var(--space-3);
}

.hive-name {
  font-size: var(--text-lg);
  font-weight: var(--font-semibold);
  margin: 0;
}

.hive-strain {
  font-size: var(--text-xs);
  color: var(--color-text-tertiary);
}

.hive-card-body {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--space-3);
}

.hive-stats {
  display: flex;
  gap: var(--space-4);
}

.hive-stat {
  text-align: center;
}
.hive-stat .stat-value {
  display: block;
  font-size: var(--text-base);
  font-weight: var(--font-semibold);
  color: var(--color-text-primary);
}
.hive-stat .stat-label {
  font-size: var(--text-xs);
  color: var(--color-text-tertiary);
}

.hive-card-footer {
  display: flex;
  justify-content: space-between;
  padding-top: var(--space-3);
  border-top: var(--border-light);
  font-size: var(--text-xs);
  color: var(--color-text-tertiary);
}
```

## JavaScript

```js
function renderHiveCard(hive) {
  const healthPercent = hive.healthScore || 80;
  const circumference = 2 * Math.PI * 24; // ~151
  const offset = circumference * (1 - healthPercent / 100);
  
  return `
    <div class="hive-card" data-hive-id="${hive.id}" onclick="App.navigate('hive','${hive.id}')">
      <div class="hive-card-header">
        <div class="hive-info">
          <h3 class="hive-name">${escapeHtml(hive.name)}</h3>
          <span class="hive-strain">${STRAINS[hive.strain] || hive.strain}</span>
        </div>
        <div class="hive-status">
          <span class="status-dot ${hive.status === 'active' ? 'online' : 'offline'}"></span>
          <span>${hive.status === 'active' ? 'Aktif' : 'Pasif'}</span>
        </div>
      </div>
      <div class="hive-card-body">...</div>
      <div class="hive-card-footer">...</div>
    </div>
  `;
}
```
