# 🎨 Renk Sistemi

> **BeeMaster AI renk paleti. Tüm renkler CSS custom property olarak tanımlanır, asla hardcode edilmez.**

---

## Ana Palet

### Background Layer'ları

| Token | Hex | Kullanım |
|-------|-----|----------|
| `--color-bg-base` | `#0B1220` | Ana arka plan |
| `--color-bg-card` | `#131D31` | Kart arka planı |
| `--color-bg-elevated` | `#1A2744` | Yükseltilmiş eleman (modal, dropdown) |
| `--color-bg-hover` | `#1F3050` | Hover durumu |
| `--color-bg-input` | `#0D1525` | Input arka planı |
| `--color-bg-sidebar` | `#0A1120` | Sidebar arka planı |

### Metin Renkleri

| Token | Hex | Kullanım |
|-------|-----|----------|
| `--color-text-primary` | `#E8EDF5` | Başlıklar, ana metin |
| `--color-text-secondary` | `#8895B3` | Alt metin, açıklamalar |
| `--color-text-tertiary` | `#5A6785` | Placeholder, disabled |
| `--color-text-inverse` | `#0B1220` | Koyu zeminde açık metin |

### Accent — Amber (Primary)

| Token | Hex | Kullanım |
|-------|-----|----------|
| `--color-primary` | `#f59e0b` | Ana vurgu rengi |
| `--color-primary-light` | `#fbbf24` | Hover/active |
| `--color-primary-dark` | `#d97706` | Pressed |
| `--color-primary-glow` | `rgba(245,158,11,0.15)` | Glow efekti |
| `--color-primary-subtle` | `rgba(245,158,11,0.08)` | Hafif arka plan |

### Semantic Renkler

| Token | Hex | Anlam |
|-------|-----|-------|
| `--color-success` | `#10b981` | Başarı, tamamlandı, sağlıklı |
| `--color-success-subtle` | `rgba(16,185,129,0.12)` | Başarı arka plan |
| `--color-warning` | `#f59e0b` | Uyarı, dikkat |
| `--color-warning-subtle` | `rgba(245,158,11,0.12)` | Uyarı arka plan |
| `--color-danger` | `#ef4444` | Hata, kritik, silme |
| `--color-danger-subtle` | `rgba(239,68,68,0.12)` | Hata arka plan |
| `--color-info` | `#3b82f6` | Bilgi, nötr |
| `--color-info-subtle` | `rgba(59,130,246,0.12)` | Bilgi arka plan |

### AI Güven Renkleri

| Skor | Renk | Anlam |
|------|------|-------|
| %90-100 | `#10b981` (green) | Yüksek güven |
| %70-89 | `#f59e0b` (amber) | Orta güven |
| %50-69 | `#f97316` (orange) | Düşük güven |
| %0-49 | `#ef4444` (red) | Çok düşük güven |

### Kenarlık Renkleri

| Token | Hex | Kullanım |
|-------|-----|----------|
| `--color-border` | `#1E2D4A` | Standart kenarlık |
| `--color-border-light` | `#253355` | Hafif kenarlık |
| `--color-border-focus` | `#f59e0b` | Focus kenarlığı |

---

## Kullanım Kuralları

1. **Asla hex kod yazma.** Her zaman `var(--color-*)` kullan.
2. **Arka plan her zaman `--color-bg-base` başlar.** Kartlar `--color-bg-card`.
3. **Amber sadece primary action'larda.** Her şeyi amber yapma.
4. **Semantic renkleri amacına uygun kullan.** Başarı mesajında kırmızı olmaz.
5. **Metin kontrastına dikkat et.** `--color-text-secondary` min 4.5:1 kontrast.

## Gradient'ler

```css
/* Amber glow — hero section, öne çıkan kartlar */
--gradient-amber: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);

/* Card gradient — üst kenar vurgusu */
--gradient-card-top: linear-gradient(180deg, rgba(245,158,11,0.15) 0%, transparent 40%);

/* Background subtle — sayfa arka plan derinliği */
--gradient-bg: radial-gradient(ellipse at top, #131D31 0%, #0B1220 70%);
```
