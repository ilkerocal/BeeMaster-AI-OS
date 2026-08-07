# BÖLÜM 11 — Veri Toplama ve Entegrasyon Ekosistemi (Data Acquisition & Integration Ecosystem)

**Sürüm:** 1.0  
**Öncelik:** Kritik  
**Durum:** Zorunlu Standart  
**Kapsam:** Tüm veri giriş ve entegrasyon süreçleri

---

## 11.0 Vizyon

BeeMaster AI'ın amacı kullanıcıdan **mümkün olduğunca az veri istemektir.**

Sistem; otomatik veri toplamalı, manuel girişleri desteklemeli, farklı kaynakları birleştirmeli, çelişkileri tespit etmeli, Dijital İkiz'i sürekli güncel tutmalıdır.

> **Kullanıcı aynı bilgiyi iki kez girmek zorunda kalmamalıdır.**

---

## 11.1 Veri Kaynakları

BeeMaster AI çok sayıda veri kaynağını destekler. Tüm kaynaklar standart bir veri katmanına bağlanır.

```
Mobil Uygulama ──┐
Web Uygulaması ──┤
Frame Scanner ────┤
IoT Sensörleri ───┤
Hava Durumu ──────┤
Harita Servisleri ┤────→ Data Ingestion Layer ────→ Dijital İkiz
Fotoğraflar ──────┤
Videolar ─────────┤
Ses Kayıtları ────┤
Laboratuvar ──────┤
Kullanıcı Notları ┤
Harici API'ler ───┘
```

---

## 11.2 Mobil Uygulama

Mobil uygulama **en önemli veri toplama aracıdır.**

| İşlem | Açıklama |
|-------|----------|
| Kovan kontrolü | Muayene kaydı |
| Fotoğraf çekimi | Frame Scanner için |
| Video kaydı | Kovan içi gözlem |
| QR kod okuma | Kovan/çerçeve tanıma |
| Sesli not | Hızlı not alma |
| Konum kaydı | GPS (isteğe bağlı) |
| Çevrimdışı çalışma | İnternetsiz veri girişi |
| Senkronizasyon | Bağlantı gelince otomatik |

İnternet bağlantısı olmadığında veriler yerel olarak saklanır ve daha sonra senkronize edilir.

---

## 11.3 Web Uygulaması

Web uygulaması; detaylı analiz, raporlama, planlama, veri düzenleme ve yönetim için kullanılır.

**Mobil ve web aynı veri modelini kullanmalıdır.**

---

## 11.4 Frame Scanner Entegrasyonu

Frame Scanner tarafından üretilen her analiz; ham görüntü, işlenmiş sonuç, güven puanı ve sürüm bilgisi ile birlikte Dijital İkiz'e aktarılır.

**Eski analizler silinmez.** (KURAL-0001)

---

## 11.5 IoT Sensörleri

Gelecekte desteklenebilecek sensörler. **Her sensör isteğe bağlıdır.** Sensör bulunmaması sistemin çalışmasını engellemez.

| Sensör | Veri Tipi |
|--------|----------|
| İç sıcaklık | °C |
| Dış sıcaklık | °C |
| Nem | % |
| Ağırlık | kg |
| Ses seviyesi | dB |
| Titreşim | Hz |
| CO₂ | ppm |
| Işık | lux |
| Kovan eğimi | derece |

---

## 11.6 Hava Durumu Entegrasyonu

Koloni davranışı çevresel koşullardan etkilenir.

| Veri | Kaynak |
|------|--------|
| Sıcaklık, Nem, Yağış, Rüzgâr, Basınç | Meteoroloji API |
| UV indeksi | Hava durumu servisi |
| Gün doğumu/batımı | Astronomik hesaplama |

Bu veriler gözlemlerle ilişkilendirilir.

---

## 11.7 Harita ve Konum

Arılık için tutulabilecek bilgiler: Bölge, Rakım, Arazi tipi, Çevredeki bitki örtüsü, Nektar kaynakları, Su kaynakları.

> Konum bilgisi **kullanıcı kontrolünde** olmalıdır.

---

## 11.8 Medya Yönetimi

Her medya dosyası **bir olaya bağlanmalıdır.**

| Tür | Durum |
|-----|-------|
| Fotoğraf | ✅ |
| Video | 📋 |
| Ses | 📋 |
| Termal görüntü | 📋 |
| 3B tarama | 📋 Gelecek |

Her dosya meta verilerle saklanır: Tarih, Kaynak, Kalite, İlgili kovan, İlgili kontrol.

---

## 11.9 Laboratuvar Sonuçları

Laboratuvar verileri sisteme eklenebilir: Hastalık testleri, Kalıntı analizleri, Polen analizleri, Bal kalite analizleri. Bu sonuçlar AI analizlerini destekleyen ek veri olarak kullanılır.

---

## 11.10 Kullanıcı Notları

Serbest metin desteklenir. Örnek: "Bugün uçuş normalden daha yoğundu."

Bu notlar; zaman damgası, kullanıcı ve ilgili koloni ile birlikte kaydedilir. İleride doğal dil işleme ile analiz edilebilir.

---

## 11.11 Harici API Entegrasyonları

BeeMaster AI gelecekte farklı servislerle çalışabilir: Meteoroloji, Haritalar, Tarım verileri, Çiçeklenme/bitki örtüsü, Takvim, Bildirim servisleri.

**Her entegrasyon ayrı bir adaptör üzerinden bağlanmalıdır.** (Bölüm 4.10: API Katmanı)

---

## 11.12 Veri Doğrulama

Sisteme gelen her veri doğrulanır:

| Kontrol | Başarısızsa |
|---------|-------------|
| Zorunlu alanlar | İşaretle, kullanıcıya bildir |
| Tarih tutarlılığı | Çakışma kaydı |
| Konum doğruluğu | Uyarı |
| Dosya bütünlüğü | Bozuk dosya işaretle |
| Görsel kalite | Düşük kalite → güven düşür |
| Sensör aralıkları | Anomali işaretle |

**Hatalı veri reddedilmez; işaretlenir ve kullanıcıya bildirilir.**

---

## 11.13 Senkronizasyon

Veri birden fazla cihazda kullanılabilir.

| Kural | Açıklama |
|-------|----------|
| Her kaydın benzersiz kimliği vardır | UUID |
| Çakışmalar kayıt altına alınır | Conflict log |
| Gerekirse kullanıcı seçim yapar | Manuel merge |
| Son değişiklik tek başına doğru kabul edilmez | Akıllı çakışma çözümü |

---

## 11.14 Olay Tabanlı Entegrasyon

Tüm veri akışı olaylar üzerinden çalışır:

```
Fotoğraf Çekildi → Frame Scanner → AI Analizi → Dijital İkiz Güncellendi → Dashboard Yenilendi → Bildirim
```

Bu yapı modüllerin birbirinden bağımsız çalışmasını sağlar. (Bölüm 5.5: Olay Tabanlı Mimari)

---

## 11.15 Veri Kalite Skoru

Her veri kaynağı için kalite puanı hesaplanır:

| Kriter | Ağırlık |
|--------|---------|
| Tamlık (eksik alan yok) | %25 |
| Güncellik (son 30 gün) | %25 |
| Tutarlılık (çelişki yok) | %20 |
| Doğrulanabilirlik | %15 |
| Kaynak güvenilirliği | %15 |

Karar Motoru bu puanları dikkate alır. (Bölüm 6.10)

---

## 11.16 Güvenlik

Tüm veri aktarımı güvenli olmalıdır. **Güvenlik, sonradan eklenen bir özellik değil, mimarinin temel parçasıdır.**

| İlke | Uygulama |
|------|----------|
| Kimlik doğrulama | Supabase Auth + JWT |
| Yetkilendirme | RLS (Row Level Security) |
| Şifreli iletişim | HTTPS/TLS |
| Veri bütünlüğü | Checksum doğrulama |
| Düzenli yedekleme | Supabase automated |
| Denetim kayıtları | Audit log |

---

## 11.17 Ölçeklenebilirlik

Sistem; tek bir arıcı, yüzlerce arılık, binlerce kovan, milyonlarca medya dosyası ile çalışabilecek şekilde tasarlanmalıdır.

**Yeni veri kaynakları mevcut yapıyı bozmadan eklenebilmelidir.**

---

## 11.18 Sonuç

BeeMaster AI'ın başarısı yalnızca iyi bir yapay zekâya değil, **yüksek kaliteli ve bütünleşik veri ekosistemine** bağlıdır.

Bu mimari sayesinde: veri tek merkezde toplanır, Dijital İkiz sürekli güncel kalır, modüller ortak veri modelini kullanır, yeni entegrasyonlar kolayca eklenebilir, sistem uzun vadede büyümeye hazır hale gelir.

---

> **"Veri ne kadar zenginse, AI o kadar akıllıdır."**
