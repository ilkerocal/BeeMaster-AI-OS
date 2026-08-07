# 🐛 Hata Ayıklama

> **BeeMaster AI debugging stratejisi ve sık yapılan hatalar.**

---

## Debugging Akışı

```
1. Hatayı yeniden üret
   ├── Tarayıcı: Chrome DevTools Console
   ├── Mobil: Remote Debugging
   └── Production: Vercel Logs
   
2. Hatayı izole et
   ├── Hangi modül?
   ├── Hangi aksiyon?
   └── Hangi veri?

3. Root cause bul
   ├── Syntax hatası mı? → node --check
   ├── Runtime hatası mı? → console.trace()
   ├── Veri hatası mı? → localStorage/Supabase kontrol
   └── CSS hatası mı? → DevTools Elements panel

4. Düzeltme
   ├── Test yaz (önce kır)
   ├── Kodu düzelt
   └── Testi yeşil yap

5. Doğrulama
   └── Playwright ile test et
```

## Sık Yapılan Hatalar

### 1. "App is not defined"
**Neden:** Bundle'da syntax hatası → tüm script çalışmıyor.
```bash
node --check app.bundle.js  # Syntax kontrolü
```

### 2. Boş beyaz sayfa
**Neden:** Template literal içinde eksik `}` veya çift tanımlı değişken.
```js
// Kontrol: console.log her render öncesi
console.log('Rendering dashboard...', data);
```

### 3. Login sonrası eski veri
**Neden:** localStorage'da eski test verisi.
```js
// Settings → "Bulut Verisini Sıfırla"
// veya manuel: localStorage.clear()
```

### 4. Sidebar tıklanamıyor
**Neden:** Overlay z-index sidebar'dan yüksek.
```css
/* overlay z-index: 199, sidebar: 200 olmalı */
```

### 5. Modal açılınca sayfa donuyor
**Neden:** Modal overlay tüm tıklamaları yakalıyor.
```js
// Fix: Modal form submit'ten sonra await ile veri kaydını bekle
```

### 6. Cache sorunu — eski kod gösteriliyor
**Neden:** Vercel CDN veya browser cache.
```bash
# Çözüm: ?v=N artır, Ctrl+Shift+R, veya incognito
```

### 7. Supabase "file://" protokolünde çalışmıyor
**Neden:** CDN script'leri file:// ile yüklenmez.
```js
// Çözüm: Inline Supabase client (sbFetch, sbAuth)
```

## Console Logging Standartları

```js
// Geliştirme sırasında
console.debug('🐝 [HiveModule] Kovanlar yükleniyor...', count);
console.warn('⚠️ Cloud sync başarısız, local veri kullanılıyor');
console.error('❌ Kritik hata:', err);

// Production'da: minimal log
// Service Worker'da: sadece hatalar
```

## Chrome DevTools Kısayolları

| Kısayol | İşlev |
|---------|-------|
| F12 | DevTools aç |
| Ctrl+Shift+C | Element seçici |
| Ctrl+Shift+J | Console |
| Ctrl+Shift+R | Hard reload (cache temizle) |
| Application → Storage → Clear | localStorage temizle |
