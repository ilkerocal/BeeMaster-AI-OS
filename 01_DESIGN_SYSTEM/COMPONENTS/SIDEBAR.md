# 📌 Sidebar

> **COMP-0008** — Ana navigasyon sidebar bileşeni.

---

## Yapı

```html
<aside class="sidebar" id="sidebar">
  <div class="sidebar-header">
    <div class="sidebar-logo">
      <span class="logo-icon">🐝</span>
      <span class="logo-text">BeeMaster AI</span>
    </div>
    <span class="badge badge-primary badge-xs">AI</span>
  </div>
  
  <nav class="sidebar-nav">
    <!-- Bölüm 1: Ana -->
    <div class="nav-section">
      <span class="nav-section-title">Ana</span>
      <a href="#dashboard" class="nav-item active">
        <svg class="icon">...</svg>
        <span>Dashboard</span>
      </a>
      <a href="#hives" class="nav-item">
        <svg class="icon">...</svg>
        <span>Kovanlar</span>
      </a>
    </div>
    
    <!-- Bölüm 2: AI Platform -->
    <div class="nav-section">
      <span class="nav-section-title">AI Platform</span>
      <a href="#diseases" class="nav-item">
        <svg class="icon">...</svg>
        <span>Hastalık AI</span>
      </a>
      <a href="#queens" class="nav-item">
        <svg class="icon">...</svg>
        <span>Kraliçe Yönetici</span>
      </a>
      <a href="#harvest" class="nav-item">
        <svg class="icon">...</svg>
        <span>Hasat</span>
      </a>
    </div>
    
    <!-- Bölüm 3: Yönetim -->
    <div class="nav-section">
      <span class="nav-section-title">Yönetim</span>
      <a href="#inspections" class="nav-item">
        <svg class="icon">...</svg>
        <span>Muayeneler</span>
      </a>
      <a href="#feeding" class="nav-item">
        <svg class="icon">...</svg>
        <span>Besleme</span>
      </a>
      <a href="#treatments" class="nav-item">
        <svg class="icon">...</svg>
        <span>Tedaviler</span>
      </a>
      <a href="#inventory" class="nav-item">
        <svg class="icon">...</svg>
        <span>Envanter</span>
      </a>
    </div>
    
    <!-- Bölüm 4: Sistem -->
    <div class="nav-section">
      <span class="nav-section-title">Sistem</span>
      <a href="#settings" class="nav-item">
        <svg class="icon">...</svg>
        <span>Ayarlar</span>
      </a>
    </div>
  </nav>
  
  <div class="sidebar-footer">
    <div class="user-info">
      <div class="avatar">A</div>
      <div class="user-details">
        <span class="user-name">Adnan Murat</span>
        <span class="user-plan">Ücretsiz</span>
      </div>
    </div>
  </div>
</aside>
```

## CSS

```css
.sidebar {
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;
  width: var(--sidebar-width);
  background: var(--color-bg-sidebar);
  border-right: var(--border-light);
  z-index: var(--z-sidebar);
  display: flex;
  flex-direction: column;
  backdrop-filter: blur(20px);
  transition: transform var(--duration-normal) var(--ease-default);
}

/* Mobil: Sidebar gizli, hamburger ile açılır */
@media (max-width: 640px) {
  .sidebar {
    transform: translateX(-100%);
  }
  .sidebar.open {
    transform: translateX(0);
    box-shadow: var(--shadow-2xl);
  }
}

/* Sidebar overlay (mobil) */
.sidebar-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.5);
  z-index: calc(var(--z-sidebar) - 1);
  display: none;
}
.sidebar-overlay.active { display: block; }
```

## Nav Item

```css
.nav-item {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  padding: var(--space-2) var(--space-3);
  border-radius: var(--radius-md);
  color: var(--color-text-secondary);
  text-decoration: none;
  font-size: var(--text-sm);
  transition: all var(--duration-fast);
}
.nav-item:hover {
  background: var(--color-bg-hover);
  color: var(--color-text-primary);
}
.nav-item.active {
  background: var(--color-primary-subtle);
  color: var(--color-primary);
}
```

## Kullanım Kuralları

1. **En fazla 4 bölüm.** Daha fazlası karmaşa.
2. **Aktif sayfa her zaman vurgulu.**
3. **Mobilde hamburger menü.** Sidebar her zaman görünmez.
4. **Kullanıcı bilgisi en altta.** Sabit footer.
