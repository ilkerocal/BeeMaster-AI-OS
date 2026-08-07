# 📄 HTML Yazım Standartları

> **BeeMaster AI HTML kuralları. Her HTML sayfası bu standartlara uymalı.**

---

## Semantik HTML

```html
<!-- ✓ DOĞRU: Semantik elementler -->
<header>
  <nav>...</nav>
</header>
<main>
  <section>
    <article class="card">...</article>
  </section>
</main>
<footer>...</footer>

<!-- ❌ YANLIŞ: Div çorbası -->
<div class="header">
  <div class="nav">...</div>
</div>
<div class="main">
  <div class="section">
    <div class="card">...</div>
  </div>
</div>
```

## Form Yapısı

```html
<!-- ✓ DOĞRU -->
<form onsubmit="handleSubmit(event)">
  <div class="form-group">
    <label for="hiveName">Kovan Adı</label>
    <input type="text" id="hiveName" required>
  </div>
</form>

<!-- ❌ YANLIŞ: Label yok -->
<input type="text" placeholder="Kovan adı">
```

## Erişilebilirlik

```html
<!-- ARIA etiketleri -->
<button aria-label="Menüyü kapat">
  <svg>...</svg>
</button>

<!-- Resimlerde alt metni -->
<img src="hive.jpg" alt="Bahçedeki mavi kovan">

<!-- Tablo başlıkları -->
<table>
  <thead>
    <tr><th scope="col">Kovan</th></tr>
  </thead>
</table>
```

## Türkçe Karakterler

```html
<!-- charset her zaman UTF-8 -->
<meta charset="UTF-8">

<!-- lang="tr" her zaman -->
<html lang="tr">
```

## Performans

```html
<!-- Lazy loading -->
<img loading="lazy" src="...">

<!-- Input autocomplete -->
<input autocomplete="off" type="search">

<!-- Preconnect Supabase -->
<link rel="preconnect" href="https://assfwtjbvuuxclioqsih.supabase.co">
```

## Yasaklı Pattern'ler

- ❌ Inline style (`style="..."`)
- ❌ Inline event handler (`onclick="..."`) — istisna: modül render içinde
- ❌ `<br>` ile boşluk — CSS margin/padding kullan
- ❌ `<table>` ile layout — grid/flexbox kullan
- ❌ `<font>`, `<center>`, `<b>`, `<i>` — CSS kullan
- ❌ `<div onclick>` yerine `<button>`
