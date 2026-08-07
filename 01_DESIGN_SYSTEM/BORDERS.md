# 📐 Kenarlık ve Radius Sistemi

> **BeeMaster AI kenarlık ve köşe yuvarlaklığı standartları.**

---

## Border Radius

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--radius-none` | 0 | Tablo hücresi, separator |
| `--radius-sm` | 4px | Badge, küçük etiket |
| `--radius-md` | 8px | Buton, input, dropdown |
| `--radius-lg` | 12px | Kart, modal |
| `--radius-xl` | 16px | Büyük kart, hero |
| `--radius-2xl` | 24px | Feature card, özel |
| `--radius-full` | 9999px | Pill, avatar, yuvarlak buton |

## Kenarlık (Border)

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--border` | `1px solid var(--color-border)` | Standart kenarlık |
| `--border-light` | `1px solid var(--color-border-light)` | Hafif ayraç |
| `--border-focus` | `2px solid var(--color-border-focus)` | Focus ring |
| `--border-card` | `1px solid rgba(255,255,255,0.05)` | Kart kenarlığı |

## Focus Ring

Tüm interaktif elemanlarda focus visible:

```css
:focus-visible {
  outline: none;
  box-shadow: 0 0 0 2px var(--color-bg-base), 
              0 0 0 4px var(--color-primary);
}
```

## Divider (Ayraç)

```css
.divider {
  height: 1px;
  background: var(--color-border-light);
  margin: var(--space-4) 0;
}

.divider-vertical {
  width: 1px;
  background: var(--color-border-light);
  height: 100%;
}
```

## Kullanım Kuralları

1. **Kartlar her zaman `--radius-lg`.** Tutarlı görünüm.
2. **Butonlar her zaman `--radius-md`.** Çok yuvarlak veya çok köşeli olmaz.
3. **İç içe elemanlarda radius uyumu.** Kart radius = 12px, içindeki resim de 12px.
4. **Focus visible her zaman.** Klavye kullanıcıları için kritik.
5. **Border rengi her zaman token.** `#ccc` gibi hardcode yok.
