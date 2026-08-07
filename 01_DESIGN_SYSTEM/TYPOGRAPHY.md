# 🔤 Tipografi

> **BeeMaster AI font sistemi. System font stack ile maksimum performans ve doğal görünüm.**

---

## Font Stack

```css
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 
             'Helvetica Neue', Arial, sans-serif, 'Apple Color Emoji', 
             'Segoe UI Emoji', 'Segoe UI Symbol';
```

**Neden system font?**
- Sıfır KB yükleme (custom font yok)
- Her cihazda native rendering
- Türkçe karakter garantili (İ, ı, ğ, ş, ç, ö, ü)
- Offline çalışır
- PWA bundle'ı küçük kalır

## Tipografi Skalası

| Token | Boyut | Satır Yüksekliği | Ağırlık | Kullanım |
|-------|-------|-----------------|---------|----------|
| `--text-xs` | 0.75rem (12px) | 1rem (16px) | 400 | Badge, etiket |
| `--text-sm` | 0.875rem (14px) | 1.25rem (20px) | 400 | Alt metin, tablo |
| `--text-base` | 1rem (16px) | 1.5rem (24px) | 400 | Gövde metni |
| `--text-lg` | 1.125rem (18px) | 1.75rem (28px) | 500 | Kart başlıkları |
| `--text-xl` | 1.25rem (20px) | 1.75rem (28px) | 600 | Bölüm başlıkları |
| `--text-2xl` | 1.5rem (24px) | 2rem (32px) | 700 | Sayfa başlıkları |
| `--text-3xl` | 1.875rem (30px) | 2.25rem (36px) | 700 | Hero başlık |
| `--text-4xl` | 2.25rem (36px) | 2.5rem (40px) | 800 | Ana ekran başlık |

## Ağırlıklar

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--font-normal` | 400 | Gövde metni |
| `--font-medium` | 500 | Vurgulu metin, buton |
| `--font-semibold` | 600 | Alt başlık |
| `--font-bold` | 700 | Başlık |
| `--font-extrabold` | 800 | Hero, logo |

## Özel Stiller

```css
/* Monospace — kod, veri, teknik metin */
--font-mono: 'SF Mono', 'Fira Code', 'Fira Mono', 'Roboto Mono', 
             'Cascadia Code', Consolas, monospace;

/* Sayılar — finansal veri, istatistik */
.tabular-nums {
  font-variant-numeric: tabular-nums;
}
```

## Türkçe Karakter Desteği

Tüm system font'lar Türkçe karakterleri destekler:
- Büyük harf: İ (dotted I), I (dotless I), Ğ, Ş, Ç, Ö, Ü
- Küçük harf: ı, i, ğ, ş, ç, ö, ü

**CSS ile Türkçe locale:**
```css
html {
  -webkit-locale: "tr-TR";
}
```

## Kullanım Kuralları

1. **Metin hiyerarşisi 3 seviyeyi geçmesin.** Başlık → Alt başlık → Gövde.
2. **Tüm büyük harf (uppercase) kullanma.** Türkçe'de İ/I sorunu var. Badge'lerde bile.
3. **Minimum font boyutu 12px.** Daha küçük okunmaz (mobilde).
4. **Satır yüksekliği en az 1.5.** Uzun metinlerde okunabilirlik için.
5. **Font ağırlığını anlam için kullan.** Kalın = önemli, değil = süsleme.
