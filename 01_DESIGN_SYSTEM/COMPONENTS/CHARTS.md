# 📊 Grafikler

> **COMP-0006** — Grafik ve veri görselleştirme bileşenleri.

---

## Felsefe

BeeMaster AI'da grafikler için **harici kütüphane kullanılmaz.** Tüm grafikler SVG ile çizilir.

**Neden:** Chart.js = 60KB+. D3 = 80KB+. PWA bundle'ı 250KB altında kalmalı.

## Grafik Tipleri

### 1. Health Ring (Sağlık Halkası)
Kovan sağlığını gösteren dairesel progress:

```html
<svg class="health-ring" viewBox="0 0 100 100">
  <circle class="ring-bg" cx="50" cy="50" r="42" />
  <circle class="ring-fill" cx="50" cy="50" r="42" 
          stroke-dasharray="264" 
          stroke-dashoffset="53" />
  <text x="50" y="50" class="ring-text">%80</text>
</svg>
```

### 2. Bar Chart (Çubuk Grafik)
Aylık hasat miktarı:

```html
<div class="bar-chart">
  <div class="bar" style="height: 70%"><span class="bar-label">Oca</span></div>
  <div class="bar" style="height: 45%"><span class="bar-label">Şub</span></div>
  <div class="bar" style="height: 85%"><span class="bar-label">Mar</span></div>
  <div class="bar active" style="height: 92%"><span class="bar-label">Nis</span></div>
</div>
```

### 3. Stat Grid (İstatistik Kartları)
En yaygın kullanılan veri gösterimi:

```html
<div class="stat-grid">
  <div class="stat-card">
    <div class="stat-icon amber">🐝</div>
    <div class="stat-value">24</div>
    <div class="stat-label">Toplam Kovan</div>
  </div>
  <div class="stat-card">
    <div class="stat-value">156 kg</div>
    <div class="stat-label">Bu Yıl Hasat</div>
  </div>
</div>
```

### 4. Timeline (Zaman Çizelgesi)
Muayene geçmişi:

```html
<div class="timeline">
  <div class="timeline-item">
    <div class="timeline-dot success"></div>
    <div class="timeline-date">15 Tem</div>
    <div class="timeline-content">
      <strong>Varroa Kontrolü</strong>
      <p>3 akar / 100 arı — Normal</p>
    </div>
  </div>
</div>
```

## Renk Skalası

```css
.chart-color-1 { background: #f59e0b; } /* Amber — primary */
.chart-color-2 { background: #10b981; } /* Green — success */
.chart-color-3 { background: #3b82f6; } /* Blue — info */
.chart-color-4 { background: #8b5cf6; } /* Purple */
.chart-color-5 { background: #ec4899; } /* Pink */
```

## Kullanım Kuralları

1. **Her zaman SVG veya CSS-only.** JavaScript canvas yok.
2. **Renkler anlamlı.** Yeşil = iyi, kırmızı = kötü.
3. **Etiketler Türkçe.** "Jan" değil "Oca".
4. **Veri yoksa grafik gösterme.** Boş durum göster.
