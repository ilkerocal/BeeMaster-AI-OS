# DEC-0001: Neden PWA?

**Tarih:** 2026-01
**Durum:** Accepted

## Bağlam
BeeMaster AI'ın mobil cihazlarda nasıl dağıtılacağına karar verilmesi gerekiyordu. Native app (iOS/Android) vs PWA.

## Karar
**PWA (Progressive Web App)** seçildi.

## Alternatifler

| Seçenek | Artıları | Eksileri |
|---------|----------|----------|
| PWA | App Store yok, anında güncelleme, tek kod tabanı, offline | Native API erişimi sınırlı |
| React Native | Native hissiyat, App Store varlığı | İki platform, build süreci, maliyet |
| Flutter | Tek kod tabanı, iyi performans | Öğrenme eğrisi, büyük bundle |

## Sonuçlar
- ✅ Anında güncelleme (Vercel deploy → kullanıcı anında görür)
- ✅ Offline çalışma (Service Worker)
- ✅ Düşük maliyet (App Store ücreti yok)
- ❌ iOS'ta push notification sınırlı
- ❌ App Store keşfedilebilirliği yok

---

# DEC-0002: Neden Supabase?

**Tarih:** 2026-01
**Durum:** Accepted

## Bağlam
Backend olarak ne kullanılacağına karar verilmesi gerekiyordu.

## Karar
**Supabase** seçildi.

## Alternatifler

| Seçenek | Artıları | Eksileri |
|---------|----------|----------|
| Supabase | PostgreSQL, RLS, Auth hazır, ücretsiz tier | Vendor lock-in |
| Firebase | Google ekosistemi, geniş topluluk | NoSQL (ilişkisel veri zor), Google bağımlılığı |
| Custom REST API | Tam kontrol | Geliştirme süresi, bakım maliyeti |

## Sonuçlar
- ✅ İlişkisel veritabanı (kovan→muayene→hastalık)
- ✅ RLS ile satır bazlı güvenlik
- ✅ Ücretsiz tier yeterli (500MB DB, 50K kullanıcı)
- ✅ Gerçek zamanlı (Realtime subscriptions)

---

# DEC-0003: Neden Inline Bundle (Tek Dosya)?

**Tarih:** 2026-07
**Durum:** Accepted

## Bağlam
v3 bundle mimarisinden sonra deploy ve cache sorunları yaşandı.

## Karar
**Tek HTML dosyası, inline CSS/JS** mimarisine geçildi.

## Alternatifler

| Seçenek | Artıları | Eksileri |
|---------|----------|----------|
| Inline bundle | Basit deploy, tek cache, file:// çalışır | Büyük dosya (250KB) |
| CDN + module | Küçük dosyalar, paralel yükleme | Cache sorunu, file:// çalışmaz |
| Webpack bundle | Optimize, tree-shaking | Build step, AI zorlanır |

## Sonuçlar
- ✅ Tek dosya deploy (Vercel'e tek HTML yükle)
- ✅ Service Worker cache kolay (tek dosya)
- ✅ file:// protokolünde çalışır (CDN bağımlılığı yok)
- ❌ Dosya büyük (ama 250KB kabul edilebilir)

---

# DEC-0004: Neden Framework Yok?

**Tarih:** 2026-01
**Durum:** Accepted

## Bağlam
Modern JS framework'ü (React, Vue, Svelte) kullanıp kullanmamaya karar verilmesi gerekiyordu.

## Karar
**Vanilla JavaScript (framework yok).**

## Alternatifler

| Seçenek | Artıları | Eksileri |
|---------|----------|----------|
| Vanilla JS | Küçük bundle, AI uyumlu, hızlı | State yönetimi manuel |
| React | Geniş ekosistem, component model | 40KB+ bundle, build step |
| Svelte | Küçük bundle, reactive | Az bilinen, AI deneyimsiz |
| Vue | Kolay öğrenme, iyi DX | Build step, AI uyum sorunu |

## Sonuçlar
- ✅ Bundle 250KB altında (React ile 300KB+)
- ✅ AI agent'lar vanilla JS'de daha az hata yapar
- ✅ Build step yok → daha az kırılma noktası
- ✅ Service Worker cache daha basit
- ❌ State yönetimi manuel (BM.Storage.state ile çözüldü)
- ❌ Component reusability sınırlı (template literal ile çözüldü)
