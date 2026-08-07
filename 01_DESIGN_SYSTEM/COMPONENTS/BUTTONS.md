# 🔘 Butonlar

> **COMP-0001** — Tüm buton varyantları ve kullanım kuralları.

---

## Varyantlar

### Primary (Ana Aksiyon)
```html
<button class="btn btn-primary">
  <svg class="icon">...</svg>
  Kaydet
</button>
```

```css
.btn-primary {
  background: var(--gradient-amber);
  color: var(--color-text-inverse);
  padding: 10px 20px;
  border: none;
  border-radius: var(--radius-md);
  font-weight: var(--font-semibold);
  font-size: var(--text-sm);
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease-default);
  box-shadow: var(--glow-soft);
  display: inline-flex;
  align-items: center;
  gap: var(--space-2);
}
.btn-primary:hover {
  transform: translateY(-1px);
  box-shadow: var(--glow-medium);
  filter: brightness(1.1);
}
.btn-primary:active {
  transform: translateY(0);
}
```

### Secondary
```css
.btn-secondary {
  background: var(--color-bg-card);
  color: var(--color-text-primary);
  border: var(--border);
  /* diğer özellikler primary ile aynı */
}
.btn-secondary:hover {
  border-color: var(--color-primary);
  color: var(--color-primary);
}
```

### Ghost
```css
.btn-ghost {
  background: transparent;
  color: var(--color-text-secondary);
  border: none;
}
.btn-ghost:hover {
  background: var(--color-bg-hover);
  color: var(--color-text-primary);
}
```

### Danger
```css
.btn-danger {
  background: var(--color-danger);
  color: white;
}
.btn-danger:hover {
  background: #dc2626;
}
```

## Boyutlar

| Boyut | Padding | Font | Yükseklik |
|-------|---------|------|-----------|
| sm | 6px 12px | 12px | 32px |
| md | 10px 20px | 14px | 40px |
| lg | 14px 28px | 16px | 48px |

## Durumlar

```css
.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}

.btn.loading {
  pointer-events: none;
  color: transparent;
  position: relative;
}
.btn.loading::after {
  content: '';
  position: absolute;
  width: 16px; height: 16px;
  border: 2px solid transparent;
  border-top-color: currentColor;
  border-radius: 50%;
  animation: spin 0.6s linear infinite;
}
```

## Buton Grupları

```html
<div class="btn-group">
  <button class="btn btn-secondary active">Günlük</button>
  <button class="btn btn-secondary">Haftalık</button>
  <button class="btn btn-secondary">Aylık</button>
</div>
```

## Kullanım Kuralları

1. **Sayfa başına 1 primary buton.** Öne çıkan aksiyon.
2. **Buton metni eylem fiili olsun.** "Gönder", "Kaydet", "İptal" — "Tamam" değil.
3. **İkon + metin > sadece ikon.** Sadece ikonsa tooltip şart.
4. **Disabled durumda nedenini göster.** Tooltip ile "Önce formu doldurun" gibi.
