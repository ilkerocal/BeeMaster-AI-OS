# 🎨 CSS Yazım Standartları

> **BeeMaster AI CSS kuralları. Her stil bu standartlara uymalı.**

---

## CSS Değişkenleri (Token)

```css
/* ✓ DOĞRU: Her zaman token kullan */
.card {
  background: var(--color-bg-card);
  border-radius: var(--radius-lg);
  padding: var(--space-4);
}

/* ❌ YANLIŞ: Hardcode değer */
.card {
  background: #131D31;
  border-radius: 12px;
  padding: 16px;
}
```

## Organizasyon

```css
/* 
  1. Display & Position
  2. Box Model (margin, padding, border)
  3. Typography
  4. Visual (background, shadow, color)
  5. Animation
*/
.component {
  /* Display */
  display: flex;
  position: relative;
  
  /* Box Model */
  padding: var(--space-4);
  margin-bottom: var(--space-3);
  border: var(--border);
  
  /* Typography */
  font-size: var(--text-sm);
  font-weight: var(--font-medium);
  
  /* Visual */
  background: var(--color-bg-card);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
  
  /* Animation */
  transition: all var(--duration-fast) var(--ease-default);
}
```

## Responsive (Mobile-First)

```css
/* Mobil önce, sonra genişlet */
.card-grid {
  display: grid;
  grid-template-columns: 1fr; /* mobil */
  gap: var(--space-4);
}

@media (min-width: 641px) {
  .card-grid {
    grid-template-columns: repeat(2, 1fr); /* tablet */
  }
}

@media (min-width: 1025px) {
  .card-grid {
    grid-template-columns: repeat(3, 1fr); /* desktop */
  }
}
```

## Performans

```css
/* Sadece transform ve opacity animate et */
/* ✓ DOĞRU */
.card { transition: transform 200ms; }
.card:hover { transform: translateY(-3px); }

/* ❌ YANLIŞ */
.card { transition: height 200ms; } /* repaint tetikler */
```

## Selector Spesifikliği

```css
/* ✓ DOĞRU: Düşük spesifiklik */
.card { /* ... */ }
.card-highlighted { /* ... */ }

/* ❌ YANLIŞ: Gereksiz nesting */
body main .content .card-list .card { /* ... */ }
```

## Yasaklı Pattern'ler

- ❌ `!important` (sadece utility class'larda)
- ❌ ID selector (`#header`) — class kullan
- ❌ `float` — flexbox/grid kullan
- ❌ Magic numbers (`margin-top: 37px`)
- ❌ `@import` — inline <style> kullan
- ❌ Inline style (`style="..."`) HTML'de
