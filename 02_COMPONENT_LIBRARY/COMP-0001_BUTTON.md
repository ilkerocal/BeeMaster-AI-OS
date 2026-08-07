# COMP-0001: Button

**Kategori:** Temel
**Durum:** Active

---

## Kullanım

Tüm butonlar bu bileşen üzerinden oluşturulur. Asla raw `<button>` kullanma.

## HTML

```html
<!-- Primary -->
<button class="btn btn-primary" onclick="handleSave()">
  <svg class="icon icon-sm"><use href="#icon-save"/></svg>
  Kaydet
</button>

<!-- Secondary -->
<button class="btn btn-secondary">İptal</button>

<!-- Ghost -->
<button class="btn btn-ghost">
  <svg class="icon icon-sm"><use href="#icon-settings"/></svg>
</button>

<!-- Danger -->
<button class="btn btn-danger">Sil</button>

<!-- Icon Only (tooltip zorunlu) -->
<button class="btn btn-ghost btn-icon" data-tooltip="Düzenle">
  <svg class="icon"><use href="#icon-edit"/></svg>
</button>

<!-- Full Width -->
<button class="btn btn-primary w-full">Gönder</button>

<!-- Disabled -->
<button class="btn btn-primary" disabled>Kaydet</button>

<!-- Loading -->
<button class="btn btn-primary loading">Kaydediliyor</button>
```

## CSS

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  padding: 10px 20px;
  border: none;
  border-radius: var(--radius-md);
  font-size: var(--text-sm);
  font-weight: var(--font-semibold);
  font-family: inherit;
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease-default);
  white-space: nowrap;
  user-select: none;
  -webkit-tap-highlight-color: transparent;
}

.btn-primary {
  background: var(--gradient-amber);
  color: var(--color-text-inverse);
  box-shadow: var(--glow-soft);
}
.btn-primary:hover { filter: brightness(1.1); transform: translateY(-1px); }
.btn-primary:active { transform: translateY(0); }

.btn-secondary {
  background: var(--color-bg-card);
  color: var(--color-text-primary);
  border: var(--border);
}
.btn-secondary:hover { border-color: var(--color-primary); color: var(--color-primary); }

.btn-ghost {
  background: transparent;
  color: var(--color-text-secondary);
}
.btn-ghost:hover { background: var(--color-bg-hover); color: var(--color-text-primary); }

.btn-danger {
  background: var(--color-danger);
  color: white;
}
.btn-danger:hover { background: #dc2626; }

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  transform: none !important;
  box-shadow: none !important;
}

.btn-sm { padding: 6px 12px; font-size: var(--text-xs); }
.btn-lg { padding: 14px 28px; font-size: var(--text-base); }
.btn-icon { padding: 8px; }
.w-full { width: 100%; }
```

## JavaScript

```js
// Buton loading state
function setButtonLoading(btn, text = 'Yükleniyor...') {
  btn.disabled = true;
  btn.dataset.originalText = btn.textContent;
  btn.textContent = text;
  btn.classList.add('loading');
}

function resetButton(btn) {
  btn.disabled = false;
  btn.textContent = btn.dataset.originalText || btn.textContent;
  btn.classList.remove('loading');
}
```
