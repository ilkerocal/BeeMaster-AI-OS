# 📐 Şablonlar

> **BeeMaster AI kod şablonları. Yeni sayfa/modül/bileşen oluştururken kullan.**

---

## Yeni Sayfa Şablonu

```html
<!-- pages/new-page.html -->
<section class="page" id="page-name">
  <div class="page-header">
    <h1 class="page-title">Sayfa Başlığı</h1>
    <button class="btn btn-primary" onclick="ModuleName.showForm()">
      <svg class="icon icon-sm"><use href="#icon-plus"/></svg>
      Yeni Ekle
    </button>
  </div>
  
  <div class="page-content">
    <!-- İçerik buraya -->
    <div id="content-area"></div>
  </div>
</section>
```

## Yeni Modül Şablonu

```js
// modules/module-name.js
const ModuleName = {
  render(container) {
    container.innerHTML = this.template();
    this.attachEvents();
  },
  
  template() {
    const items = BM.Storage.state.items || [];
    if (!items.length) {
      return EmptyState('Henüz veri yok', 'Yeni Ekle', () => this.showForm());
    }
    return `
      <div class="card-grid">
        ${items.map(item => this.itemCard(item)).join('')}
      </div>
    `;
  },
  
  itemCard(item) {
    return `
      <div class="card" data-id="${item.id}">
        <div class="card-header">
          <h3>${escapeHtml(item.name)}</h3>
        </div>
        <div class="card-body">
          <!-- item detayları -->
        </div>
      </div>
    `;
  },
  
  attachEvents() {
    document.querySelectorAll('.card').forEach(card => {
      card.onclick = () => this.openDetail(card.dataset.id);
    });
  },
  
  showForm(data = null) {
    // Modal ile form göster
    const isEdit = !!data;
    Modal.show({
      title: isEdit ? 'Düzenle' : 'Yeni Ekle',
      content: this.formTemplate(data),
      onSave: async (formData) => {
        if (isEdit) {
          await this.update(data.id, formData);
        } else {
          await this.add(formData);
        }
        Modal.hide();
        this.render(document.getElementById('content-area'));
      }
    });
  },
  
  formTemplate(data) {
    return `
      <form onsubmit="return false">
        <div class="form-group">
          <label>Ad</label>
          <input type="text" class="form-input" id="item-name" 
                 value="${escapeHtml(data?.name || '')}" required>
        </div>
      </form>
    `;
  },
  
  async add(formData) { /* localStorage + cloud */ },
  async update(id, formData) { /* ... */ },
  async delete(id) { /* ... */ },
  
  openDetail(id) {
    App.navigate('module-name', id);
  }
};
```

## Yeni Bileşen Şablonu

```js
// components/component-name.js
function ComponentName(props) {
  const { title, value, variant = 'default' } = props;
  
  return `
    <div class="component component-${variant}">
      <span class="component-label">${escapeHtml(title)}</span>
      <span class="component-value">${escapeHtml(String(value))}</span>
    </div>
  `;
}
```

## Skill Şablonu

```markdown
---
name: beemaster-skill-name
description: BeeMaster AI için [açıklama]
---

# Skill: [Ad]

## Ne zaman kullanılır
[Tetikleyici durumlar]

## Adımlar
1. [Adım 1]
2. [Adım 2]

## Kurallar
- BDAOS RULE-NNNN: [ilgili kural]
