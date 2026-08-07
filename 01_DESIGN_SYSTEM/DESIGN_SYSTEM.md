# 🎨 BeeMaster AI — Design System

> **Bu doküman, BeeMaster AI'ın görsel dilini tanımlar. Her UI kararı buraya referans verir.**

---

## Tasarım Felsefesi

BeeMaster AI tasarımı üç kelimeyle özetlenir:

**Koyu. Profesyonel. AI-odaklı.**

Bu bir "kayıt uygulaması" değil, bir **AI destekli dijital ikiz platformudur.** Tasarım bunu yansıtmalı — sanki bir uzay istasyonu kontrol paneli gibi, ama arıcının anlayacağı sadelikte.

## Tema

| Özellik | Değer |
|---------|-------|
| Tema | Dark (koyu) |
| Background | `#0B1220` (derin mavi-siyah) |
| Card | `#131D31` (koyu mavi) |
| Primary Accent | Amber `#f59e0b` → `#d97706` |
| Köşe yuvarlaklığı | 12px (kartlar), 8px (butonlar), 6px (inputlar) |
| Gölgeler | Amber glow, soft elevation |
| Tipografi | System font stack, Türkçe optimize |
| İkonlar | Lucide Icons (inline SVG) |

## Tasarım Token'ları

Tüm görsel değerler `TOKENS/design-tokens.json` içinde CSS custom property olarak tanımlıdır. Kod içinde her zaman bu token'lar kullanılır:

```css
/* ✓ DOĞRU */
color: var(--color-primary);
background: var(--color-bg-card);
box-shadow: var(--shadow-card);

/* ❌ YANLIŞ */
color: #f59e0b;
background: #131D31;
```

## Responsive Breakpoints

| Ad | Aralık | Hedef |
|----|--------|-------|
| Mobile | 375px — 640px | Tek kolon, tam genişlik kartlar, bottom nav |
| Tablet | 641px — 1024px | 2 kolon grid, sidebar kapalı (hamburger) |
| Desktop | 1025px+ | 3 kolon grid, sidebar açık |

## Bileşen Hiyerarşisi

```
Tasarım Token'ları (renk, font, spacing)
    ↓
Temel Bileşenler (buton, input, badge)
    ↓
Birleşik Bileşenler (card, modal, form)
    ↓
Domain Bileşenleri (hive-card, disease-card, ai-card)
    ↓
Sayfalar (dashboard, hives, diseases)
```

## Erişilebilirlik

- Minimum kontrast oranı: 4.5:1 (AA)
- Tüm interaktif elemanlar focus visible
- Form elemanlarında label zorunlu
- Touch target minimum 44×44px (mobil)
- `prefers-reduced-motion` desteği

## AI Göstergeleri

BeeMaster AI'ın ayırt edici özelliği AI güven göstergeleridir:

- **Hexagon (⬡)** — AI varlığını gösterir
- **Yeşil pulse** — AI aktif olarak analiz ediyor
- **Yüzde + renk** — Güven skoru (%0-100, kırmızı→sarı→yeşil)
- **Gerekçe kartı** — AI neden bu sonuca vardı?

---

> **"Tasarım, kullanıcının AI'ya güvenmesini sağlamalı."**
