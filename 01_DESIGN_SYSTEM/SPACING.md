# 📏 Boşluk Sistemi (Spacing)

> **4px tabanlı grid. Tüm boşluklar bu sisteme uyar.**

---

## Spacing Scale

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--space-0` | 0 | Sıfır boşluk |
| `--space-1` | 4px | İkon-padding, inline gap |
| `--space-2` | 8px | Compact gap, badge padding |
| `--space-3` | 12px | Kart padding, buton iç boşluk |
| `--space-4` | 16px | Standart padding, section gap |
| `--space-5` | 20px | Geniş padding |
| `--space-6` | 24px | Bölüm arası boşluk |
| `--space-8` | 32px | Sayfa padding (mobil) |
| `--space-10` | 40px | Sayfa padding (desktop) |
| `--space-12` | 48px | Büyük section gap |
| `--space-16` | 64px | Hero spacing |

## Layout

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--page-padding-mobile` | 16px | Mobil sayfa kenar boşluğu |
| `--page-padding-desktop` | 40px | Desktop sayfa kenar boşluğu |
| `--card-padding` | 16px | Kart iç boşluğu |
| `--modal-padding` | 24px | Modal iç boşluğu |
| `--section-gap` | 24px | Bölümler arası boşluk |
| `--grid-gap` | 16px | Grid hücreleri arası boşluk |

## Grid Sistemi

```css
/* 12 kolon grid (desktop) */
.grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: var(--grid-gap);
}

/* Mobil: tek kolon */
@media (max-width: 640px) {
  .grid { grid-template-columns: 1fr; }
}

/* Tablet: 2 kolon */
@media (min-width: 641px) and (max-width: 1024px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}

/* Desktop: 3 kolon */
@media (min-width: 1025px) {
  .grid { grid-template-columns: repeat(3, 1fr); }
}
```

## Sidebar

| Token | Değer |
|-------|-------|
| `--sidebar-width` | 260px |
| `--sidebar-collapsed` | 0px (mobil) |
| `--sidebar-z` | 200 |

## Kullanım Kuralları

1. **Boşluklar her zaman 4'ün katı.** 5px, 7px, 13px yasak.
2. **Tutarlı ol.** Aynı tür elemanlar arası boşluk aynı olmalı.
3. **Mobil ve desktop farklı.** Mobil dar, desktop geniş — ama orantılı.
4. **Beyaz boşluk düşmandır deme.** Nefes alan tasarım iyidir.
