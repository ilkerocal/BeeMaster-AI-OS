# ✨ Animasyon Sistemi

> **BeeMaster AI animasyon kuralları. Amaç: profesyonel, pürüzsüz, AI hissiyatı.**

---

## Süreler

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--duration-instant` | 100ms | Hover rengi, çok hızlı |
| `--duration-fast` | 200ms | Buton press, toggle |
| `--duration-normal` | 300ms | Panel aç/kapa, modal |
| `--duration-slow` | 500ms | Sayfa geçişi |
| `--duration-very-slow` | 800ms | Hero animasyonu |

## Easing (Zamanlama)

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--ease-default` | `cubic-bezier(0.4, 0, 0.2, 1)` | Genel amaçlı |
| `--ease-in` | `cubic-bezier(0.4, 0, 1, 1)` | Giriş |
| `--ease-out` | `cubic-bezier(0, 0, 0.2, 1)` | Çıkış |
| `--ease-bounce` | `cubic-bezier(0.68, -0.55, 0.265, 1.55)` | Vurgulu (az kullan) |

## Hazır Animasyon Sınıfları

### Fade
```css
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}
.animate-fade-in { animation: fadeIn var(--duration-normal) var(--ease-default); }
```

### Slide
```css
@keyframes slideUp {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: translateY(0); }
}
.animate-slide-up { animation: slideUp var(--duration-normal) var(--ease-out); }

@keyframes slideDown {
  from { opacity: 0; transform: translateY(-12px); }
  to   { opacity: 1; transform: translateY(0); }
}
.animate-slide-down { animation: slideDown var(--duration-normal) var(--ease-out); }
```

### Scale
```css
@keyframes scaleIn {
  from { opacity: 0; transform: scale(0.95); }
  to   { opacity: 1; transform: scale(1); }
}
.animate-scale-in { animation: scaleIn var(--duration-fast) var(--ease-default); }
```

### AI Pulse (BeeMaster imza animasyonu)
```css
@keyframes aiPulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(16,185,129,0.4); }
  50%      { box-shadow: 0 0 0 8px rgba(16,185,129,0); }
}
.ai-pulse {
  animation: aiPulse 2s ease-in-out infinite;
}

/* AI dot */
.ai-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--color-success);
  animation: aiPulse 2s ease-in-out infinite;
}
```

### Hover Efektleri
```css
/* Kart hover — hafif yükselme */
.card-hover {
  transition: transform var(--duration-fast) var(--ease-default),
              box-shadow var(--duration-fast) var(--ease-default);
}
.card-hover:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-lg);
}

/* Buton hover */
.btn-hover {
  transition: all var(--duration-instant) var(--ease-default);
}
.btn-hover:hover {
  filter: brightness(1.1);
  transform: translateY(-1px);
}
```

### Skeleton Loading
```css
@keyframes shimmer {
  0%   { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}
.skeleton {
  background: linear-gradient(90deg, 
    var(--color-bg-card) 25%, 
    var(--color-bg-elevated) 50%, 
    var(--color-bg-card) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s ease-in-out infinite;
  border-radius: var(--radius-md);
}
```

## Kullanım Kuralları

1. **Kısa ve anlamlı.** 300ms'den uzun animasyonlar sıkıcı.
2. **prefers-reduced-motion saygılı.** Hareket hassasiyeti olan kullanıcılar için:
   ```css
   @media (prefers-reduced-motion: reduce) {
     *, *::before, *::after {
       animation-duration: 0.01ms !important;
       transition-duration: 0.01ms !important;
     }
   }
   ```
3. **Performans.** Sadece `transform` ve `opacity` animate et. `width`, `height`, `top`, `left` değil.
4. **AI pulse'ı sadece aktif AI durumunda kullan.** Her yerde yeşil dot olmaz.
5. **Animasyon hikaye anlatır.** Modal açılış scale+fade, kapanış sadece fade. Anlamı olsun.
