# 📊 Tablolar

> **COMP-0005** — Veri tablosu bileşeni ve responsive davranışı.

---

## Standart Tablo

```html
<div class="table-container">
  <table class="table">
    <thead>
      <tr>
        <th>Kovan</th>
        <th>Irk</th>
        <th>Kraliçe</th>
        <th class="text-right">Çerçeve</th>
        <th class="text-center">Durum</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="font-medium">Bahçe Kovanı 1</td>
        <td>Karniyol</td>
        <td>2024 Ana</td>
        <td class="text-right tabular-nums">10/12</td>
        <td class="text-center">
          <span class="badge badge-success">Aktif</span>
        </td>
      </tr>
    </tbody>
  </table>
</div>
```

```css
.table-container {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}

.table {
  width: 100%;
  border-collapse: collapse;
}

.table th {
  text-align: left;
  font-size: var(--text-xs);
  font-weight: var(--font-semibold);
  color: var(--color-text-tertiary);
  text-transform: none; /* uppercase yok — Türkçe sorunu */
  padding: var(--space-2) var(--space-3);
  border-bottom: var(--border-light);
}

.table td {
  padding: var(--space-3);
  font-size: var(--text-sm);
  color: var(--color-text-primary);
  border-bottom: 1px solid rgba(255,255,255,0.03);
}

.table tbody tr:hover {
  background: var(--color-bg-hover);
}
```

## Responsive Tablo (Mobil)

Mobilde tablo yatay scroll veya card view'a dönüşür:

```css
@media (max-width: 640px) {
  /* Seçenek 1: Yatay scroll */
  .table-responsive .table-container {
    margin: 0 calc(-1 * var(--page-padding-mobile));
    padding: 0 var(--page-padding-mobile);
  }
  
  /* Seçenek 2: Card view (önerilen) */
  .table-cards thead { display: none; }
  .table-cards tbody tr {
    display: block;
    padding: var(--space-3);
    border: var(--border-card);
    border-radius: var(--radius-md);
    background: var(--color-bg-card);
    margin-bottom: var(--space-2);
  }
  .table-cards td {
    display: flex;
    justify-content: space-between;
    padding: var(--space-1) 0;
    border: none;
  }
  .table-cards td::before {
    content: attr(data-label);
    font-weight: var(--font-medium);
    color: var(--color-text-secondary);
  }
}
```

## Tablo Boş Durum

```html
<tr>
  <td colspan="5" class="text-center py-8">
    <div class="empty-state">
      <svg class="icon icon-xl">...</svg>
      <p>Henüz kovan eklenmemiş</p>
      <button class="btn btn-primary btn-sm">Kovan Ekle</button>
    </div>
  </td>
</tr>
```

## Kullanım Kuralları

1. **Sayısal veriler sağa hizalı.** `text-right tabular-nums`
2. **Mobilde card view tercih et.** Yatay scroll ikinci seçenek.
3. **Boş durumda CTA göster.** "Henüz veri yok" değil, "İlk kovanını ekle".
4. **Tablo başlıkları kısa ve Türkçe.**
5. **Sticky header uzun tablolarda.**
