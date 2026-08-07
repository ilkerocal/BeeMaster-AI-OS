# 🏷️ Rozet ve Etiketler

> **COMP-0007** — Badge, tag, status indicator bileşenleri.

---

## Standart Badge

```html
<span class="badge badge-primary">Yeni</span>
<span class="badge badge-success">Aktif</span>
<span class="badge badge-warning">Uyarı</span>
<span class="badge badge-danger">Kritik</span>
<span class="badge badge-info">Bilgi</span>
```

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 2px 8px;
  border-radius: var(--radius-full);
  font-size: var(--text-xs);
  font-weight: var(--font-medium);
  line-height: 1.5;
  white-space: nowrap;
}

.badge-primary { background: var(--color-primary-subtle); color: var(--color-primary); }
.badge-success { background: var(--color-success-subtle); color: var(--color-success); }
.badge-warning { background: var(--color-warning-subtle); color: var(--color-warning); }
.badge-danger  { background: var(--color-danger-subtle);  color: var(--color-danger); }
.badge-info    { background: var(--color-info-subtle);    color: var(--color-info); }
```

## Dot Indicator

```html
<span class="status-dot online"></span> Çevrimiçi
<span class="status-dot offline"></span> Çevrimdışı
<span class="status-dot warning"></span> Dikkat
```

```css
.status-dot {
  display: inline-block;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  margin-right: 6px;
}
.status-dot.online  { background: var(--color-success); }
.status-dot.offline { background: var(--color-text-tertiary); }
.status-dot.warning { background: var(--color-warning); animation: aiPulse 2s infinite; }
```

## AI Güven Badge'i

```html
<div class="ai-confidence">
  <svg class="icon icon-sm"><!-- Hexagon --></svg>
  <span class="confidence-value">%87</span>
  <div class="confidence-bar">
    <div class="confidence-fill" style="width: 87%"></div>
  </div>
</div>
```

## Sayı Badge'i (Counter)

```html
<button class="btn btn-ghost">
  Bildirimler
  <span class="badge-counter">3</span>
</button>
```

```css
.badge-counter {
  background: var(--color-danger);
  color: white;
  min-width: 20px;
  height: 20px;
  border-radius: var(--radius-full);
  font-size: 11px;
  font-weight: var(--font-bold);
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
```

## Kullanım Kuralları

1. **1-2 badge yeterli.** Her şeye badge koyma.
2. **Metin kısa olsun.** "Beklemede" değil "Bekliyor".
3. **Renk anlamlı olsun.** Yeşil = iyi, kırmızı = kötü, sarı = dikkat.
4. **AI badge'leri her zaman hexagon ile.**
