# ⏱️ Timeline

> **COMP-0011** — Zaman çizelgesi bileşeni. Muayene geçmişi, tedavi takibi, hasat kaydı için kullanılır.

---

## Standart Timeline

```html
<div class="timeline">
  <div class="timeline-item">
    <div class="timeline-marker success"></div>
    <div class="timeline-content">
      <div class="timeline-header">
        <span class="timeline-date">15 Tem 2025</span>
        <span class="badge badge-success">Normal</span>
      </div>
      <h4>Rutin Muayene</h4>
      <p>Kovan güçlü, ana arı aktif. 8 çerçeve dolu.</p>
    </div>
  </div>
  
  <div class="timeline-item">
    <div class="timeline-marker warning"></div>
    <div class="timeline-content">
      <div class="timeline-header">
        <span class="timeline-date">8 Tem 2025</span>
        <span class="badge badge-warning">Dikkat</span>
      </div>
      <h4>Varroa Tespiti</h4>
      <p>5 akar / 100 arı. Tedavi önerildi.</p>
    </div>
  </div>
  
  <div class="timeline-item">
    <div class="timeline-marker"></div>
    <div class="timeline-content">
      <div class="timeline-header">
        <span class="timeline-date">1 Tem 2025</span>
      </div>
      <h4>Hasat</h4>
      <p>12 kg süzme bal, kalite: A</p>
    </div>
  </div>
</div>
```

## CSS

```css
.timeline {
  position: relative;
  padding-left: var(--space-8);
}

/* Dikey çizgi */
.timeline::before {
  content: '';
  position: absolute;
  left: 15px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: var(--color-border);
}

.timeline-item {
  position: relative;
  padding-bottom: var(--space-6);
}
.timeline-item:last-child {
  padding-bottom: 0;
}

.timeline-marker {
  position: absolute;
  left: calc(-1 * var(--space-8) + 8px);
  top: 4px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: var(--color-bg-card);
  border: 2px solid var(--color-border);
  z-index: 1;
}
.timeline-marker.success { border-color: var(--color-success); background: var(--color-success); }
.timeline-marker.warning { border-color: var(--color-warning); background: var(--color-warning); }
.timeline-marker.danger  { border-color: var(--color-danger);  background: var(--color-danger); }
.timeline-marker.active  { 
  border-color: var(--color-primary); 
  background: var(--color-primary);
  box-shadow: var(--glow-soft);
}

.timeline-content {
  background: var(--color-bg-card);
  border: var(--border-card);
  border-radius: var(--radius-md);
  padding: var(--space-3);
}

.timeline-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--space-1);
}

.timeline-date {
  font-size: var(--text-xs);
  color: var(--color-text-tertiary);
}

.timeline-content h4 {
  font-size: var(--text-sm);
  font-weight: var(--font-semibold);
  margin-bottom: var(--space-1);
}

.timeline-content p {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  margin: 0;
}
```

## Varyantlar

### Kompakt Timeline (Sidebar/Widget)
```css
.timeline-compact .timeline-item {
  padding-bottom: var(--space-3);
}
.timeline-compact .timeline-content {
  padding: var(--space-2);
  background: transparent;
  border: none;
}
```

### AI Öneri Timeline
```html
<div class="timeline-item">
  <div class="timeline-marker ai"></div>
  <div class="timeline-content card-ai">
    <div class="timeline-header">
      <span class="ai-badge">⬡ AI Önerisi</span>
      <span class="confidence">%87</span>
    </div>
    <p>Nosema riski yüksek. Son 2 haftada yağış artışı ve sıcaklık düşüşü tespit edildi.</p>
  </div>
</div>
```

## Kullanım Kuralları

1. **En fazla 3 marker rengi.** Success / Warning / Danger yeterli.
2. **Tarih formatı: "15 Tem 2025".** Ay ismi kısa Türkçe.
3. **Her item'ın bir başlığı olmalı.**
4. **AI önerileri her zaman farklı stil.** Amber glow + hexagon.
