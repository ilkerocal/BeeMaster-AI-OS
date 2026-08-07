# 🃏 Kartlar

> **COMP-0002** — Kart bileşeni varyantları ve kuralları.

---

## Standart Kart

```html
<div class="card">
  <div class="card-header">
    <h3 class="card-title">Başlık</h3>
    <span class="card-badge">Durum</span>
  </div>
  <div class="card-body">
    <p>İçerik buraya...</p>
  </div>
  <div class="card-footer">
    <button class="btn btn-ghost">İptal</button>
    <button class="btn btn-primary">Kaydet</button>
  </div>
</div>
```

```css
.card {
  background: var(--color-bg-card);
  border: var(--border-card);
  border-radius: var(--radius-lg);
  padding: var(--space-4);
  box-shadow: var(--shadow-md);
  transition: all var(--duration-fast) var(--ease-default);
}
.card:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-lg);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--space-3);
}

.card-title {
  font-size: var(--text-lg);
  font-weight: var(--font-semibold);
  color: var(--color-text-primary);
}

.card-body {
  color: var(--color-text-secondary);
  font-size: var(--text-sm);
}

.card-footer {
  display: flex;
  justify-content: flex-end;
  gap: var(--space-2);
  margin-top: var(--space-4);
  padding-top: var(--space-4);
  border-top: var(--border-light);
}
```

## Kart Varyantları

### AI Kart (Glow)
```css
.card-ai {
  composes: card;
  box-shadow: var(--glow-soft);
  border-color: rgba(245,158,11,0.2);
}
.card-ai:hover {
  box-shadow: var(--glow-medium);
}
```

### İstatistik Kartı
```css
.card-stat {
  composes: card;
  text-align: center;
  padding: var(--space-6);
}
.card-stat .value {
  font-size: var(--text-3xl);
  font-weight: var(--font-bold);
  color: var(--color-primary);
}
.card-stat .label {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  margin-top: var(--space-1);
}
```

### Hive Card (Kovan)
```css
.card-hive {
  composes: card;
  border-left: 3px solid var(--color-primary);
}
```

### Disease Card (Hastalık)
```css
.card-disease {
  composes: card;
  position: relative;
}
.card-disease .severity {
  position: absolute;
  top: 12px;
  right: 12px;
}
```

### Empty State Card
```css
.card-empty {
  composes: card;
  text-align: center;
  padding: var(--space-10);
  border: 2px dashed var(--color-border);
  background: transparent;
  box-shadow: none;
}
.card-empty:hover {
  transform: none;
  border-color: var(--color-primary);
}
```

## Kart Grid

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: var(--space-4);
}

@media (max-width: 640px) {
  .card-grid {
    grid-template-columns: 1fr;
  }
}
```

## Kullanım Kuralları

1. **Her kartın bir başlığı olmalı.**
2. **Kart içi padding her zaman `--card-padding` (16px).**
3. **Hover efekti her kartta olmak zorunda değil.** Statik bilgi kartlarında hover yok.
4. **Kart yüksekliği tutarlı olsun.** Aynı satırdaki kartlar aynı yükseklikte.
