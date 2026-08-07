# 🐝 BeeMaster AI — Master Blueprint

> **Bu doküman, BeeMaster AI sisteminin kuşbakışı görünümüdür. Her AI agent'ın ilk okuması gereken dosya budur.**

---

## Sistem Özeti

BeeMaster AI, **tek dosya PWA** mimarisinde, **Supabase** backend'li, **inline JavaScript** ile çalışan, **offline-first** bir arıcılık yönetim platformudur.

### Teknik Özet

| Bileşen | Teknoloji | Açıklama |
|---------|-----------|----------|
| Frontend | Vanilla HTML/CSS/JS | Framework yok, tek HTML dosyası |
| Backend | Supabase | PostgreSQL + Auth + Storage + RLS |
| Deployment | Vercel + GitHub Pages | Otomatik deploy, global CDN |
| AI | Supabase Edge Functions | Öneri motoru, hastalık tespiti |
| Offline | Service Worker + localStorage | İnternetsiz tam işlevsellik |
| Test | Playwright (Python) | Görsel + fonksiyonel E2E testler |

### Mimari Kararlar (Özet)

| Karar | Sebep |
|-------|-------|
| **Vanilla JS, framework yok** | PWA'nın küçük kalması, bağımlılık olmaması, offline çalışma |
| **Tek HTML dosyası** | Basit deploy, cache kolaylığı, tek kaynak |
| **Supabase** | Ücretsiz tier, PostgreSQL, anlık RLS, gerçek zamanlı |
| **PWA (Service Worker)** | App Store gerektirmez, offline, anında güncelleme |
| **İngilizce kod, Türkçe UI** | Kod global standart, kullanıcı ana dilinde |
| **Inline Supabase client** | CDN bağımlılığı yok, file:// protokolünde çalışır |

---

## Sistem Bileşenleri

### 1. Frontend (Tek HTML Dosyası)

```
index.html
├── <style> — Tüm CSS inline (Design System token'ları)
├── <div id="app"> — Ana uygulama konteyneri
├── <script> — Inline Supabase client (sbFetch, sbAuth)
├── <script> — Ana uygulama kodu (App, Router, tüm modüller)
└── Service Worker kaydı
```

### 2. Modüller

| Modül | Sorumluluk | Durum |
|-------|-----------|-------|
| **Dashboard** | Ana sayfa, istatistikler, hızlı erişim | ✅ v6 |
| **Hives** | Kovan CRUD, detay sayfası | ✅ v6 |
| **Apiaries** | Arılık yönetimi | ✅ v6 |
| **Queens** | Kraliçe takibi | ✅ v6 |
| **Frames** | Çerçeve yönetimi | 🔄 v6 |
| **Inspections** | Muayene kaydı | ✅ v6 |
| **Disease AI** | Hastalık tespit ve öneri | ✅ v6 |
| **Harvest** | Hasat takibi | 🔄 |
| **Feeding** | Besleme kaydı | 🔄 |
| **Treatments** | Tedavi yönetimi | 🔄 |
| **Inventory** | Envanter takibi | 🔄 |
| **Frame Scanner** | Görüntü analizi | 📋 Plan |
| **Digital Twin** | 3D kovan görselleştirme | 📋 Plan |

### 3. Veri Katmanı

```
Supabase (PostgreSQL)
├── apiaries          — Arılıklar
├── hives             — Kovanlar
├── queens            — Kraliçeler
├── frames            — Çerçeveler
├── inspections       — Muayeneler
├── harvests          — Hasatlar
├── feedings          — Beslemeler
├── treatments        — Tedaviler
├── diseases          — Hastalıklar
├── inventory         — Envanter
└── profiles          — Kullanıcı profilleri

Fallback: localStorage (offline mod)
```

### 4. Auth Akışı

```
Kullanıcı → Email/Şifre → Supabase Auth → JWT Token
                                              ↓
                              Tüm API çağrıları JWT ile
                              RLS politikaları user_id bazlı
                                              ↓
                              Offline: localStorage'dan devam
```

---

## Tasarım Dili (v6)

- **Tema:** Dark theme (#0B1220 / #131D31)
- **Accent:** Amber (#f59e0b)
- **Tipografi:** System font stack, Türkçe karakter desteği
- **Bileşenler:** Kart bazlı, glass morphism, 3D hover
- **AI Göstergesi:** Hexagon (⬡) + yüzde güven skoru + yeşil pulse animasyonu

---

## Geliştirme İş Akışı

```
1. BDAOS kurallarını yükle (.hermesrules)
2. Görevi analiz et
3. Plan oluştur (.hermes/plans/)
4. Tasarım sistemini kontrol et
5. Bileşen kütüphanesini kontrol et
6. Kodu yaz (TDD ile)
7. Playwright ile test et
8. Visual QA checklist'ini uygula
9. Commit (tek özellik)
10. Deploy (cache-bust artır)
11. Canlıda test et
```

---

## Dosya Konumları

| Ne | Nerede |
|----|--------|
| Uygulama kodu | `C:\Users\hatbi\OneDrive\Masaüstü\arı-gelisen-yapay-zeka\beaios\` |
| GitHub (uygulama) | `github.com/ilkerocal/beemaster-ai` |
| GitHub (BDAOS) | `github.com/ilkerocal/BeeMaster-AI-OS` |
| Vercel | `beemaster-ai.vercel.app` |
| Supabase | `assfwtjbvuuxclioqsih.supabase.co` |
| Test kullanıcısı | `adnanmurat021@gmail.com` |

---

> **"Bu blueprint, BeeMaster AI'ın DNA'sıdır. Her karar buraya referans verir."**
