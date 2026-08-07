# 🌑 Gölge Sistemi

> **BeeMaster AI gölge sistemi. Amber glow ve elevation seviyeleri.**

---

## Gölge Seviyeleri

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--shadow-none` | `none` | Düz elemanlar |
| `--shadow-sm` | `0 1px 3px rgba(0,0,0,0.3)` | Input, badge |
| `--shadow-md` | `0 4px 12px rgba(0,0,0,0.25)` | Kart (default) |
| `--shadow-lg` | `0 8px 24px rgba(0,0,0,0.3)` | Yükseltilmiş kart, hover |
| `--shadow-xl` | `0 12px 36px rgba(0,0,0,0.35)` | Modal |
| `--shadow-2xl` | `0 20px 48px rgba(0,0,0,0.4)` | Drawer, sidebar overlay |

## Amber Glow

BeeMaster AI'ın imza efekti. AI varlığını ve önemli aksiyonları vurgular.

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--glow-subtle` | `0 0 12px rgba(245,158,11,0.08)` | AI badge, pasif durum |
| `--glow-soft` | `0 0 20px rgba(245,158,11,0.15)` | Buton hover, aktif kart |
| `--glow-medium` | `0 0 30px rgba(245,158,11,0.2)` | Primary CTA, featured card |
| `--glow-strong` | `0 0 40px rgba(245,158,11,0.25)` | Hero element, AI pulse |
| `--glow-intense` | `0 0 60px rgba(245,158,11,0.3)` | Özel vurgu (az kullan!) |

## Semantic Glow'lar

```css
--glow-success: 0 0 20px rgba(16,185,129,0.2);
--glow-danger:  0 0 20px rgba(239,68,68,0.2);
--glow-info:    0 0 16px rgba(59,130,246,0.15);
```

## Elevation Sistemi

Her UI katmanının bir z-index değeri vardır:

| Katman | z-index | Eleman |
|--------|---------|--------|
| Base | 0 | Sayfa içeriği |
| Dropdown | 100 | Dropdown, tooltip |
| Sticky | 150 | Sticky header |
| Sidebar | 200 | Sidebar |
| Overlay | 300 | Modal overlay, backdrop |
| Modal | 400 | Modal |
| Toast | 500 | Bildirim, toast |

## Kullanım Kuralları

1. **Her zaman CSS değişkeni kullan.** `box-shadow: var(--shadow-md)`
2. **Amber glow'u sadece AI elemanlarında kullan.** Her kart glow yapma.
3. **Gölge + elevation tutarlı ol.** Modal en yüksek gölgeye sahip olmalı.
4. **Hover'da bir seviye yükselt.** `shadow-md` → `shadow-lg`
5. **Text-shadow kullanma.** Dark theme'de okunmaz.
