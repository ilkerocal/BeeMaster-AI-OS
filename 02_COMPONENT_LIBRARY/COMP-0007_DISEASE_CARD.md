# COMP-0007: Disease Card (Hastalık Kartı)

**Kategori:** Domain
**Durum:** Active

---

## Kullanım

Hastalık modülünde her hastalık için gösterilen kart. Tıklanınca detay modal'ı açar.

## HTML

```html
<div class="disease-card" onclick="openDiseaseDetail('varroa')">
  <div class="disease-severity">
    <div class="severity-stars">
      ★★★★★
    </div>
    <span class="badge badge-danger">Kritik</span>
  </div>
  
  <div class="disease-icon">🕷️</div>
  
  <h3 class="disease-name">Varroa</h3>
  <p class="disease-desc">Varroa destructor akarı, en tehlikeli arı parazitidir.</p>
  
  <div class="disease-meta">
    <span class="meta-item">
      <span class="meta-label">Kategori</span>
      <span class="meta-value">Parazit</span>
    </span>
    <span class="meta-item">
      <span class="meta-label">Mevsim</span>
      <span class="meta-value">İlkbahar-Sonbahar</span>
    </span>
  </div>
  
  <div class="disease-ai">
    <div class="ai-badge">
      <svg class="icon icon-sm"><!-- Hexagon --></svg>
      <span>⬡ AI İzliyor</span>
    </div>
    <span class="confidence high">%92</span>
  </div>
</div>
```

## CSS

```css
.disease-card {
  background: var(--color-bg-card);
  border: var(--border-card);
  border-radius: var(--radius-lg);
  padding: var(--space-4);
  position: relative;
  overflow: hidden;
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease-default);
}
.disease-card:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-lg);
}
.disease-card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
  background: linear-gradient(90deg, var(--color-danger), var(--color-warning));
}

.disease-severity {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--space-2);
}

.severity-stars {
  color: var(--color-warning);
  font-size: var(--text-sm);
  letter-spacing: 2px;
}

.disease-icon {
  font-size: 2rem;
  margin-bottom: var(--space-2);
}

.disease-name {
  font-size: var(--text-lg);
  font-weight: var(--font-bold);
  margin-bottom: var(--space-1);
}

.disease-desc {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  margin-bottom: var(--space-3);
  line-height: 1.4;
}

.disease-meta {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-2);
  margin-bottom: var(--space-3);
  padding: var(--space-2);
  background: var(--color-bg-base);
  border-radius: var(--radius-md);
}

.meta-label {
  display: block;
  font-size: var(--text-xs);
  color: var(--color-text-tertiary);
}
.meta-value {
  font-size: var(--text-sm);
  font-weight: var(--font-medium);
  color: var(--color-text-primary);
}

.disease-ai {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: var(--space-3);
  border-top: var(--border-light);
}

.confidence.high   { color: var(--color-success); }
.confidence.medium { color: var(--color-warning); }
.confidence.low    { color: var(--color-danger); }
```

## JavaScript

```js
const DISEASES = [
  {
    id: 'varroa',
    name: 'Varroa',
    icon: '🕷️',
    severity: 5,
    category: 'Parazit',
    season: 'İlkbahar-Sonbahar',
    description: 'Varroa destructor akarı, en tehlikeli arı parazitidir.',
    confidence: 92,
    symptoms: ['Kanatsız arılar', 'Deforme larvalar', 'Kovan önünde ölü arılar'],
    treatment: 'Formik asit veya oksalik asit uygulaması...',
    prevention: 'Düzenli varroa sayımı, hijyenik ırk seçimi...'
  }
  // ... 5 hastalık daha
];

function renderDiseaseCard(disease) {
  const stars = '★'.repeat(disease.severity) + '☆'.repeat(5 - disease.severity);
  const confClass = disease.confidence >= 90 ? 'high' : disease.confidence >= 70 ? 'medium' : 'low';
  
  return `
    <div class="disease-card" onclick="openDiseaseDetail('${disease.id}')">
      <div class="disease-severity">
        <div class="severity-stars">${stars}</div>
        <span class="badge ${disease.severity >= 4 ? 'badge-danger' : 'badge-warning'}">
          ${disease.severity >= 4 ? 'Kritik' : 'Önemli'}
        </span>
      </div>
      <div class="disease-icon">${disease.icon}</div>
      <h3 class="disease-name">${disease.name}</h3>
      <p class="disease-desc">${disease.description}</p>
      <div class="disease-meta">
        <span class="meta-item">
          <span class="meta-label">Kategori</span>
          <span class="meta-value">${disease.category}</span>
        </span>
        <span class="meta-item">
          <span class="meta-label">Mevsim</span>
          <span class="meta-value">${disease.season}</span>
        </span>
      </div>
      <div class="disease-ai">
        <div class="ai-badge">
          <svg class="icon icon-sm"><!-- Hexagon --></svg>
          <span>⬡ AI İzliyor</span>
        </div>
        <span class="confidence ${confClass}">%${disease.confidence}</span>
      </div>
    </div>
  `;
}
```
