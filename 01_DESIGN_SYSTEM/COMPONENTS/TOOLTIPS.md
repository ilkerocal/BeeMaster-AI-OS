# 💬 Tooltip'ler

> **COMP-0010** — Tooltip ve popover bileşenleri.

---

## Standart Tooltip

```html
<button class="btn btn-ghost" data-tooltip="Kovan ekle">
  <svg class="icon"><!-- Plus --></svg>
</button>
```

```css
[data-tooltip] {
  position: relative;
}
[data-tooltip]::after {
  content: attr(data-tooltip);
  position: absolute;
  bottom: calc(100% + 8px);
  left: 50%;
  transform: translateX(-50%);
  padding: 4px 8px;
  background: var(--color-bg-elevated);
  color: var(--color-text-primary);
  font-size: var(--text-xs);
  border-radius: var(--radius-sm);
  white-space: nowrap;
  pointer-events: none;
  opacity: 0;
  transition: opacity var(--duration-fast);
  z-index: var(--z-dropdown);
}
[data-tooltip]:hover::after {
  opacity: 1;
}
```

## Tooltip Pozisyonları

```css
[data-tooltip-pos="bottom"]::after {
  bottom: auto;
  top: calc(100% + 8px);
}
[data-tooltip-pos="left"]::after {
  left: auto;
  right: calc(100% + 8px);
  top: 50%;
  bottom: auto;
  transform: translateY(-50%);
}
[data-tooltip-pos="right"]::after {
  left: calc(100% + 8px);
  right: auto;
  top: 50%;
  bottom: auto;
  transform: translateY(-50%);
}
```

## Popover (Zengin Tooltip)

```html
<div class="popover-container">
  <button class="btn btn-ghost" onclick="togglePopover()">
    <svg class="icon"><!-- Info --></svg>
  </button>
  <div class="popover">
    <h4>AI Güven Skoru</h4>
    <p>Bu skor, AI'nın önerisine olan güvenini gösterir. Geçmiş verilere ve benzer vakalara dayanır.</p>
  </div>
</div>
```

```css
.popover {
  position: absolute;
  top: calc(100% + 8px);
  right: 0;
  width: 280px;
  padding: var(--space-4);
  background: var(--color-bg-elevated);
  border: var(--border);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-xl);
  z-index: var(--z-dropdown);
}
```

## Kullanım Kuralları

1. **Tooltip kısa olsun.** 2-3 kelime.
2. **Sadece ikon butonlarda.** Metinli butonlarda gereksiz.
3. **Mobilde tooltip gösterme.** Touch cihazlarda hover yok. Yerine popover veya bottom sheet.
4. **Tooltip metni Türkçe.**
