# BÖLÜM 4 — Frontend Mimarisi ve Geliştirme Standartları

**Sürüm:** 1.0  
**Durum:** Zorunlu Standart  
**Kapsam:** Tüm frontend geliştirmeleri

---

## 4.1 Temel Mimari İlkesi

BeeMaster AI'da **hiçbir dosya "her şeyi yapan dosya" olamaz.**

| ❌ Yanlış | ✅ Doğru |
|-----------|----------|
| `index.html` — 14.800 satır | Her ekran kendi modülünde |
| `app.js` — 9.300 satır | Her modül kendi sorumluluğunda |

**Doğru yaklaşım:**

```
/pages
    dashboard/
    colonies/
    diseases/
    scanner/
    queen/
    reports/
```

Her modül yalnızca kendi ekranından sorumludur.

---

## 4.2 Klasör Yapısı

```
src/
│
├── assets/
│   ├── icons/          # Lucide SVG ikonlar
│   ├── images/         # Statik görseller
│   └── fonts/          # (System font stack — genelde boş)
│
├── components/
│   ├── ui/             # Temel UI: Button, Input, Badge
│   ├── cards/          # Kart bileşenleri: HiveCard, DiseaseCard
│   ├── charts/         # Grafikler: HealthRing, BarChart
│   ├── forms/          # Form elemanları
│   └── layout/         # Sidebar, Navbar, PageShell
│
├── features/
│   ├── dashboard/      # Dashboard sayfası
│   ├── hives/          # Kovan yönetimi
│   ├── diseases/       # Hastalık modülü
│   ├── scanner/        # Frame Scanner
│   └── weather/        # Hava durumu
│
├── services/           # API/Supabase servis katmanı
│   ├── hiveService.js
│   ├── diseaseService.js
│   └── authService.js
│
├── stores/             # State yönetimi (Digital Twin)
│   └── digitalTwinStore.js
│
├── utils/              # Yardımcı fonksiyonlar
│   ├── formatters.js
│   └── validators.js
│
├── styles/             # Global CSS, token'lar
│   ├── tokens.css
│   └── global.css
│
├── routes/             # SPA routing
│   └── router.js
│
└── app/                # Uygulama giriş noktası
    └── main.js
```

**Her klasörün tek bir sorumluluğu vardır.**

---

## 4.3 Feature (Özellik) Tabanlı Geliştirme

BeeMaster AI ekran tabanlı değil, **özellik tabanlı** geliştirilir.

**Örnek:** "Disease" yalnızca bir sayfa değildir. Şunları içerir:

```
Disease Feature
├── AI Engine          ← Hastalık tespiti
├── Treatment          ← Tedavi yönetimi
├── Photos             ← Fotoğraf analizi
├── Timeline           ← Hastalık geçmişi
├── Digital Twin       ← Koloniyle bağlantı
└── Risk Analysis      ← Risk değerlendirmesi
```

Bunlar tek bir feature altında yaşar.

---

## 4.4 Bileşen Ayrımı

Bir bileşen üç gruptan birine ait olmalıdır:

| Tip | Sorumluluk | Örnek |
|-----|------------|-------|
| **Sunum Bileşeni** (Presentation) | Sadece görünüm. İş mantığı içermez. | `DiseaseCard`, `StatBadge` |
| **Akıllı Bileşen** (Container) | Veriyi alır, işler, sunum bileşenlerine aktarır. | `DiseaseList` |
| **Ortak Bileşen** (Shared) | Her sayfada kullanılabilir. | `Button`, `Modal`, `Card`, `Input` |

---

## 4.5 CSS Mimarisi

En önemli kurallardan biri: **Hermes yeni CSS yazmadan önce mevcut sınıfları aramak zorundadır.**

### Değiştirici (Modifier) Yapısı

| ❌ Yanlış (yeni sınıf) | ✅ Doğru (modifier) |
|------------------------|---------------------|
| `.card` `.dashboard-card` `.disease-card` `.ai-card` | `.card` `.card--disease` `.card--ai` `.card--dashboard` |

```css
/* ✓ DOĞRU: Base + Modifier */
.card { /* temel stil */ }
.card--ai { box-shadow: var(--glow-soft); }
.card--disease { border-left: 3px solid var(--color-danger); }
.card--dashboard { background: var(--gradient-card-top); }
```

---

## 4.6 JavaScript Mimarisi

JavaScript dosyaları **küçük ve odaklı** olmalıdır. Bir dosya yalnızca tek bir işi yapmalıdır.

| Dosya | Sorumluluk | Yapmaz |
|-------|------------|--------|
| `diseaseService.js` | Yalnızca hastalık verileriyle ilgilenir | UI çizmez |
| `diseaseView.js` | Yalnızca ekranı oluşturur | Veri çekmez |
| `diseaseController.js` | İkisini birbirine bağlar | Tek başına çalışmaz |

---

## 4.7 Durum Yönetimi (State)

BeeMaster AI'da **tek bir gerçek veri kaynağı** vardır: **Digital Twin State.**

Ekranlar kendi verilerini oluşturmaz. Hepsi merkezi durumdan okur.

```
Digital Twin State (tek kaynak)
├── Hive       ← Kovan verisi
├── Disease    ← Hastalık geçmişi
├── Weather    ← Hava durumu
├── Scanner    ← Çerçeve analizi
└── Dashboard  ← Tümünün özeti
```

Böylece tüm ekranlar aynı bilgiyi görür. (KURAL-0006)

---

## 4.8 Sayfalar Arası İletişim

Sayfalar birbirini doğrudan çağırmaz.

```
❌ Dashboard → Disease → Scanner (doğrudan bağımlı)
✅ Dashboard → Service Layer ← Disease ← Scanner (ortak servis)
```

Hepsi ortak servis katmanı üzerinden iletişim kurar.

---

## 4.9 Olay Sistemi (Event Bus)

Her değişiklik olay olarak yayınlanır:

```
Hive Updated → Scanner Updated → AI Updated → Dashboard Updated
```

Bu sayede manuel yenileme ihtiyacı azalır.

```js
// Event Bus pattern
BM.Events.emit('hive:updated', { hiveId, changes });
BM.Events.on('hive:updated', ({ hiveId, changes }) => {
  // Digital Twin güncelle
  // Dashboard yenile
});
```

---

## 4.10 API Katmanı

Frontend hiçbir zaman API ayrıntılarını bilmez. Tüm istekler servis katmanından geçer.

```
UI → HiveService → sbFetch() → Supabase API
```

Yarın API değişirse yalnızca servis katmanı güncellenir. UI etkilenmez.

---

## 4.11 Performans Kuralları

Bir ekran açılırken:

| Kural | Uygulama |
|-------|----------|
| Gereksiz veri yüklenmez | Sadece görünen modülün verisi çekilir |
| Görünmeyen bileşenler oluşturulmaz | Lazy rendering |
| Büyük tablolar sanallaştırılır | Sadece görünen satırlar DOM'da |
| Resimler tembel yüklenir | `loading="lazy"` |
| Ağ istekleri tekrarlanmaz | Cache + debounce |

---

## 4.12 Hata Yönetimi

Her hata **üç seviyede** ele alınır:

| Seviye | Hedef | Format |
|--------|-------|--------|
| 1. Kullanıcı | Kullanıcıya gösterilir | "Bir sorun oluştu. Lütfen tekrar deneyin." |
| 2. Geliştirici | Console'a yazılır | `console.error('[DiseaseService]', err)` |
| 3. AI Analiz | ai_logs tablosuna | `{timestamp, module, error, context}` |

**Kullanıcı asla teknik hata mesajı görmez.**

---

## 4.13 Frontend Kalite Kontrolü

Her geliştirme sonunda Hermes şu kontrol listesini uygular:

| # | Kontrol | Beklenen |
|---|---------|----------|
| 1 | Yeni HTML eklendi mi? | Minimum, bileşenlerden |
| 2 | Mevcut bileşen kullanılabilir miydi? | BCL kontrolü |
| 3 | Yeni CSS sınıfı gerçekten gerekli miydi? | Modifier kullan |
| 4 | JavaScript modüler mi? | Tek sorumluluk |
| 5 | Responsive test edildi mi? | 360-1920px |
| 6 | Karanlık tema kontrol edildi mi? | Dark theme |
| 7 | Performans etkilendi mi? | <3sn yükleme |
| 8 | Konsol hatası var mı? | 0 hata |

---

## 4.14 Frontend Geliştirme Akışı

Her görev şu sırayla ilerler. **Hiçbir adım atlanamaz.**

```
① İstek
    │
② Gereksinim Analizi
    │
③ Etkilenecek Feature'lar
    │
④ Mevcut Bileşen Kontrolü (BCL)
    │
⑤ Tasarım Sistemi Kontrolü (BDS)
    │
⑥ Geliştirme (TDD)
    │
⑦ Test (Playwright)
    │
⑧ Kod İncelemesi
    │
⑨ Yayınlama (Deploy)
```

---

## 4.15 BeeMaster AI'ya Özel Frontend Kuralları

Her sayfa şu **dört soruya** cevap vermelidir:

| # | Soru | Eksikse |
|---|------|---------|
| 1 | Bu ekranda koloni hakkında ne öğreniyorum? | Bilgi eksik |
| 2 | AI bana ne öneriyor? | AI entegrasyonu yok |
| 3 | Geçmişte ne oldu? | Timeline eksik |
| 4 | Bundan sonra ne olacak? | Tahmin eksik |

**Bu dört sorudan biri eksikse ekran tamamlanmış sayılmaz.**

---

## 4.16 Yasaklar

Hermes aşağıdaki davranışları **yapamaz:**

| # | Yasak | Sınır |
|---|-------|-------|
| ❌ | 1000 satırdan büyük CSS dosyası | Max 1000 satır |
| ❌ | 1000 satırdan büyük JS modülü | Max 1000 satır |
| ❌ | Aynı HTML yapısını farklı dosyalarda kopyalamak | DRY |
| ❌ | Tek dosyada birden fazla ekran mantığı | Single responsibility |
| ❌ | İş mantığını HTML içine gömmek | `onclick="...logic..."` |
| ❌ | Stil tanımlarını JavaScript içinde yazmak | `element.style.color = ...` |

---

## 4.17 Sonuç

Frontend, BeeMaster AI'ın görünen yüzüdür; ancak amacı "güzel görünmek" değil, **Dijital İkiz'in bilgisini doğru ve anlaşılır şekilde sunmaktır.**

Her yeni ekran:
- ✅ Mevcut bileşenleri kullanmalı (BCL)
- ✅ Ortak tasarım sistemine uymalı (BDS)
- ✅ Merkezi durum yönetimiyle çalışmalı (Digital Twin)
- ✅ Performans ve erişilebilirlik kurallarını karşılamalı

---

> **"Frontend'in görevi güzel görünmek değil, Dijital İkiz'i konuşturmaktır."**
