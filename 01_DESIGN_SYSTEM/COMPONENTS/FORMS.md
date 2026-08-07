# 📋 Formlar

> **COMP-0004** — Form elemanları ve validasyon kuralları.

---

## Form Yapısı

```html
<form class="form" onsubmit="handleSubmit(event)">
  <!-- Input -->
  <div class="form-group">
    <label class="form-label" for="name">Kovan Adı</label>
    <input type="text" id="name" class="form-input" 
           placeholder="Örn: Bahçe Kovanı 1" required>
    <span class="form-hint">En az 2 karakter</span>
    <span class="form-error">Bu alan zorunlu</span>
  </div>
  
  <!-- Select -->
  <div class="form-group">
    <label class="form-label" for="strain">Irk</label>
    <select id="strain" class="form-select">
      <option value="">Seçiniz...</option>
      <option value="carniolan">Karniyol</option>
      <option value="caucasian">Kafkas</option>
      <option value="anatolian">Anadolu</option>
      <option value="italian">İtalyan</option>
    </select>
  </div>
  
  <!-- Textarea -->
  <div class="form-group">
    <label class="form-label" for="notes">Notlar</label>
    <textarea id="notes" class="form-textarea" rows="3"></textarea>
  </div>
  
  <button type="submit" class="btn btn-primary w-full">Kaydet</button>
</form>
```

## Input Stilleri

```css
.form-input, .form-select, .form-textarea {
  width: 100%;
  padding: 10px 12px;
  background: var(--color-bg-input);
  border: var(--border);
  border-radius: var(--radius-md);
  color: var(--color-text-primary);
  font-size: var(--text-sm);
  font-family: inherit;
  transition: border-color var(--duration-instant);
}
.form-input:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(245,158,11,0.15);
}
.form-input.error {
  border-color: var(--color-danger);
}
.form-input.error:focus {
  box-shadow: 0 0 0 3px rgba(239,68,68,0.15);
}
```

## Label ve Hint

```css
.form-label {
  display: block;
  font-size: var(--text-sm);
  font-weight: var(--font-medium);
  color: var(--color-text-primary);
  margin-bottom: var(--space-1);
}

.form-hint {
  font-size: var(--text-xs);
  color: var(--color-text-tertiary);
  margin-top: var(--space-1);
}

.form-error {
  font-size: var(--text-xs);
  color: var(--color-danger);
  margin-top: var(--space-1);
  display: none;
}
.form-input.error ~ .form-error {
  display: block;
}
```

## Checkbox / Radio / Toggle

```html
<!-- Checkbox -->
<label class="checkbox-label">
  <input type="checkbox" class="checkbox">
  <span>Ana arı görüldü</span>
</label>

<!-- Toggle Switch -->
<label class="toggle">
  <input type="checkbox">
  <span class="toggle-slider"></span>
  <span class="toggle-label">Bildirimler</span>
</label>
```

## Form Grupları (Inline)

```html
<div class="form-row">
  <div class="form-group" style="flex:2">
    <input class="form-input" placeholder="Tarih">
  </div>
  <div class="form-group" style="flex:1">
    <select class="form-select">
      <option>kg</option>
    </select>
  </div>
</div>
```

## Arama Çubuğu

```html
<div class="search-bar">
  <svg class="icon">...</svg> <!-- Search icon -->
  <input type="search" class="form-input" placeholder="Hastalık ara...">
</div>
```

## Kullanım Kuralları

1. **Her input'un label'ı olmalı.** Placeholder label değildir.
2. **Validation anlık değil, submit'te.** Kullanıcıyı yazarken rahatsız etme.
3. **Hata mesajı spesifik olsun.** "Geçersiz" değil, "En az 3 karakter girin".
4. **Zorunlu alanları `*` ile işaretle.**
5. **Mobilde input font-size min 16px.** iOS zoom sorunu.
