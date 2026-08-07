# ⏳ Yükleme Durumları

> **COMP-0009** — Skeleton, spinner ve loading state bileşenleri.

---

## Spinner

```html
<div class="spinner"></div>
```

```css
.spinner {
  width: 24px;
  height: 24px;
  border: 3px solid var(--color-border);
  border-top-color: var(--color-primary);
  border-radius: 50%;
  animation: spin 0.6s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.spinner-sm { width: 16px; height: 16px; border-width: 2px; }
.spinner-lg { width: 40px; height: 40px; border-width: 4px; }
```

## Sayfa Yükleme

```html
<div class="page-loading">
  <div class="spinner spinner-lg"></div>
  <p class="loading-text">Yükleniyor...</p>
</div>
```

```css
.page-loading {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 60vh;
  gap: var(--space-4);
}

.loading-text {
  color: var(--color-text-secondary);
  font-size: var(--text-sm);
}
```

## Skeleton Loading

```html
<!-- Kart skeleton -->
<div class="card skeleton-card">
  <div class="skeleton skeleton-title"></div>
  <div class="skeleton skeleton-text"></div>
  <div class="skeleton skeleton-text short"></div>
</div>
```

```css
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

.skeleton-title { height: 20px; width: 60%; margin-bottom: 12px; }
.skeleton-text  { height: 14px; width: 100%; margin-bottom: 8px; }
.skeleton-text.short { width: 40%; }
```

## AI Düşünme Durumu

```html
<div class="ai-thinking">
  <div class="ai-dot"></div>
  <span>AI analiz ediyor...</span>
  <div class="thinking-dots">
    <span>.</span><span>.</span><span>.</span>
  </div>
</div>
```

```css
.ai-thinking {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-3) var(--space-4);
  background: var(--color-primary-subtle);
  border-radius: var(--radius-md);
  color: var(--color-primary);
  font-size: var(--text-sm);
}

.thinking-dots span {
  animation: dotPulse 1.4s ease-in-out infinite;
}
.thinking-dots span:nth-child(2) { animation-delay: 0.2s; }
.thinking-dots span:nth-child(3) { animation-delay: 0.4s; }
```

## Progress Bar

```html
<div class="progress">
  <div class="progress-fill" style="width: 65%"></div>
</div>
<div class="progress-label">%65 tamamlandı</div>
```

## Kullanım Kuralları

1. **Skeleton > Spinner.** Skeleton daha az rahatsız edici.
2. **3 saniyeden uzun yüklemelerde ilerleme göster.**
3. **AI işlemlerinde "düşünüyor" animasyonu.** Kullanıcı AI'nın çalıştığını bilsin.
4. **Boş spinner gösterme.** Her zaman bir metin ile ("Yükleniyor...", "Analiz ediliyor...").
