# 🎯 İkonlar

> **Lucide Icons. Hepsi bu.**

---

## Neden Lucide?

- Açık kaynak (ISC license)
- 1000+ ikon
- SVG tabanlı (piksel mükemmel, her boyutta net)
- Tree-shakeable (sadece kullanılan ikonlar yüklenir)
- Tutarlı tasarım dili (stroke-width: 2, rounded corners)

## Kullanım

```html
<!-- Inline SVG (önerilen) -->
<svg class="icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
  <path d="M..."/>
</svg>
```

```css
.icon {
  width: 20px;
  height: 20px;
  color: var(--color-text-secondary);
  flex-shrink: 0;
}
```

## Boyutlar

| Boyut | Değer | Kullanım |
|-------|-------|----------|
| xs | 14px | Badge içi, inline |
| sm | 16px | Liste, tablo |
| md | 20px | Buton, sidebar, standart |
| lg | 24px | Başlık yanı, hero |
| xl | 32px | Boş durum, feature |

## Renkler

İkonlar CSS `color` ile renklendirilir (`stroke="currentColor"`):

```css
.icon-muted    { color: var(--color-text-tertiary); }
.icon-default  { color: var(--color-text-secondary); }
.icon-primary  { color: var(--color-primary); }
.icon-success  { color: var(--color-success); }
.icon-danger   { color: var(--color-danger); }
```

## Sık Kullanılan İkonlar

### Navigasyon
- `home` — Dashboard
- `layout-grid` — Hives / Colonies
- `map-pin` — Apiaries

### AI
- `brain` — AI Engine
- `scan` — Frame Scanner
- `microscope` — Disease AI
- `cpu` — AI Processing

### Veri / İşlem
- `clipboard-check` — Inspections
- `wheat` — Harvest
- `droplets` — Feeding
- `pill` — Treatments
- `package` — Inventory

### Kovan
- `hexagon` — Hive / AI
- `crown` — Queen
- `layout-template` — Frames
- `thermometer` — Health

### Arayüz
- `plus` — Ekle
- `search` — Ara
- `filter` — Filtrele
- `more-vertical` — Menü
- `x` — Kapat
- `chevron-right` — İleri
- `chevron-left` — Geri
- `chevron-down` — Aç
- `chevron-up` — Kapat
- `menu` — Hamburger
- `settings` — Ayarlar
- `user` — Profil
- `log-out` — Çıkış

### Durum
- `check-circle` — Başarı
- `alert-triangle` — Uyarı
- `x-circle` — Hata
- `info` — Bilgi
- `loader-2` — Yükleniyor (animasyonlu)
- `wifi-off` — Offline

## Kullanım Kuralları

1. **Sadece Lucide kullan.** Başka ikon seti karıştırma.
2. **20px varsayılan boyut.** Özel durumlarda yukarıdaki skalayı kullan.
3. **İkon + metin her zaman.** Tek başına ikon asla (tooltip olmadan). Erişilebilirlik.
4. **Dekoratif değil, işlevsel.** Her ikon bir anlam taşımalı.
5. **Renk, durumu anlatır.** Kırmızı ikon = kritik, yeşil = iyi.
