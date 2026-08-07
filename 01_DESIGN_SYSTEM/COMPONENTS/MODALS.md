# 🪟 Modallar

> **COMP-0003** — Modal bileşeni ve kullanım kuralları.

---

## Standart Modal

```html
<div class="modal-overlay" id="myModal">
  <div class="modal">
    <div class="modal-header">
      <h2 class="modal-title">Modal Başlığı</h2>
      <button class="btn-close" onclick="closeModal('myModal')">
        <svg class="icon">...</svg> <!-- X icon -->
      </button>
    </div>
    <div class="modal-body">
      <p>Modal içeriği...</p>
    </div>
    <div class="modal-footer">
      <button class="btn btn-secondary">İptal</button>
      <button class="btn btn-primary">Onayla</button>
    </div>
  </div>
</div>
```

```css
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.6);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: var(--z-modal-overlay);
  animation: fadeIn var(--duration-fast) var(--ease-default);
}

.modal {
  background: var(--color-bg-card);
  border: var(--border-card);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-xl);
  width: 90vw;
  max-width: 520px;
  max-height: 85vh;
  display: flex;
  flex-direction: column;
  animation: scaleIn var(--duration-normal) var(--ease-out);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-4) var(--space-6);
  border-bottom: var(--border-light);
}

.modal-title {
  font-size: var(--text-lg);
  font-weight: var(--font-semibold);
}

.modal-body {
  padding: var(--space-6);
  overflow-y: auto;
  flex: 1;
}

.modal-footer {
  display: flex;
  justify-content: flex-end;
  gap: var(--space-2);
  padding: var(--space-4) var(--space-6);
  border-top: var(--border-light);
}
```

## Varyantlar

### Tam Ekran Modal (Hastalık Detay)
```css
.modal-full {
  max-width: 90vw;
  max-height: 95vh;
}
```

### Bottom Sheet (Mobil)
```css
@media (max-width: 640px) {
  .modal-overlay {
    align-items: flex-end;
  }
  .modal {
    width: 100vw;
    max-width: 100vw;
    max-height: 90vh;
    border-radius: var(--radius-xl) var(--radius-xl) 0 0;
    animation: slideUp var(--duration-normal) var(--ease-out);
  }
}
```

### Confirm Dialog
```html
<div class="modal-overlay">
  <div class="modal modal-sm">
    <div class="modal-body text-center">
      <div class="icon-circle danger">⚠</div>
      <h3>Emin misiniz?</h3>
      <p>Bu işlem geri alınamaz.</p>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost">İptal</button>
      <button class="btn btn-danger">Sil</button>
    </div>
  </div>
</div>
```

## Kullanım Kuralları

1. **Modal'ı kapatmanın 3 yolu:** X butonu, İptal butonu, overlay'e tıklama.
2. **Escape tuşu modal'ı kapatır.**
3. **Modal açıkken arka plan scroll'u kilitlenir.** `document.body.style.overflow = 'hidden'`
4. **Modal içinde modal açma.** Karışıklık yaratır.
5. **Form içeren modal'larda Enter = Submit.**
6. **Mobilde bottom sheet tercih et.** Başparmak erişimi için.
