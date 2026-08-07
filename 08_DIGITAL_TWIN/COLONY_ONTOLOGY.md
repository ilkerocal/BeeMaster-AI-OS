# BÖLÜM 8.2 — Koloni Ontolojisi ve Veri Sözlüğü (Colony Ontology & Data Dictionary)

**Sürüm:** 1.0  
**Öncelik:** Kritik  
**Durum:** Zorunlu Standart  
**Kapsam:** Tüm varlık tanımları ve isimlendirme

---

## 8.2.0 Amaç

BeeMaster AI'da **herkes aynı dili konuşmalıdır.**

İnsan, AI, mobil uygulama, web uygulaması, API, veritabanı — aynı nesneleri aynı isimlerle tanımalıdır.

Bu nedenle her kavramın **resmi bir tanımı** vardır.

---

## 8.2.1 Ontoloji Nedir?

Ontoloji; bir sistem içerisindeki **bütün varlıkların, özelliklerin ve ilişkilerin** resmi tanımıdır. BeeMaster AI'ın sözlüğüdür.

---

## 8.2.2 Temel İlke

> Bir nesne, sistemde yalnızca **bir kez** tanımlanır.

Örneğin "Kovan" farklı dosyalarda farklı anlamlara gelemez.

---

## 8.2.3 En Üst Seviye Varlıklar (Entity Hierarchy)

BeeMaster AI aşağıdaki ana nesneleri tanır. **Bu liste kontrollüdür.** Yeni ana varlık eklenmesi mimari onay gerektirir.

```
Apiary (Arılık)
    │
    ▼
Hive (Kovan)
    │
    ▼
Colony (Koloni)
    │
    ├── Queen (Ana Arı)
    ├── Frame (Çerçeve)
    │       └── Comb (Petek)
    │           └── Cell (Hücre)
    ├── Bee (Arı)
    ├── Disease (Hastalık)
    │       └── Treatment (Tedavi)
    ├── Harvest (Hasat)
    ├── Feeding (Besleme)
    ├── Inspection (Kontrol)
    ├── Weather (Hava Durumu)
    ├── Sensor (Sensör)
    ├── Media (Fotoğraf/Video/Ses)
    ├── Task (Görev)
    └── AI_Recommendation (AI Önerisi)
```

---

## 8.2.4 Arılık (Apiary) — `ENT-001`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Birden fazla kovanın bulunduğu fiziksel lokasyon |
| **Kod** | `ENT-001` |
| **İngilizce** | Apiary |
| **Türkçe** | Arılık |
| **Çoğul** | Arılıklar |

**Özellikler:** Ad, Konum (lat/lng), Rakım, Bölge, İklim, Sahip

**İlişkiler:** `Arılık ──İÇERİR──→ Kovan`

---

## 8.2.5 Kovan (Hive) — `ENT-002`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Koloninin yaşadığı fiziksel yapı |
| **Kod** | `ENT-002` |
| **İngilizce** | Hive |
| **Türkçe** | Kovan |
| **Çoğul** | Kovanlar |

**Özellikler:** Tip (langstroth/dadant/...), Malzeme, Hacim, Durum, Üretici

**İlişkiler:** `Kovan ──BARINDIRIR──→ Koloni`

> ⚠️ **Kovan ile Koloni aynı şey değildir.** Koloni değişebilir. Kovan kalabilir.

---

## 8.2.6 Koloni (Colony) — `ENT-003`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Aynı ana arı etrafında yaşayan arı topluluğu |
| **Kod** | `ENT-003` |
| **İngilizce** | Colony |
| **Türkçe** | Koloni |
| **Çoğul** | Koloniler |

**Özellikler:** Güç (1-10), Sağlık (0-100), Nüfus, Aktivite, Yaşam Döngüsü Aşaması

**İlişkiler:** `Koloni ──SAHİPTİR──→ Ana Arı`, `Koloni ──İÇERİR──→ Çerçeveler`

---

## 8.2.7 Ana Arı (Queen) — `ENT-004`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Koloninin tek yumurtlayan bireyi |
| **Kod** | `ENT-004` |
| **İngilizce** | Queen |
| **Türkçe** | Ana Arı |
| **Çoğul** | Ana Arılar |

**Özellikler:** Irk, Yaş, İşaret Rengi (beyaz/sarı/kırmızı/yeşil/mavi), Doğum Tarihi, Çiftleşme Durumu, Performans Skoru

**İlişkiler:** `Ana Arı ──ÜRETİR──→ Yumurta`

---

## 8.2.8 Çerçeve (Frame) — `ENT-005`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Peteklerin bulunduğu fiziksel taşıyıcı |
| **Kod** | `ENT-005` |
| **İngilizce** | Frame |
| **Türkçe** | Çerçeve |
| **Çoğul** | Çerçeveler |

**Özellikler:** Numara, Durum, Tip, Son Tarama Tarihi

**İlişkiler:** `Çerçeve ──İÇERİR──→ Petek`

---

## 8.2.9 Petek (Comb) — `ENT-006`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Bal arılarının oluşturduğu balmumu yapısı |
| **Kod** | `ENT-006` |
| **İngilizce** | Comb |
| **Türkçe** | Petek |
| **Çoğul** | Petekler |

**Özellikler:** Bal (%), Polen (%), Açık Yavru (%), Kapalı Yavru (%), Boş Alan (%)

> Petek; Frame Scanner tarafından analiz edilir. Hücre seviyesinde sınıflandırılır (Bölüm 7.6).

---

## 8.2.10 Hastalık (Disease) — `ENT-007`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Koloni sağlığını etkileyen biyolojik problem |
| **Kod** | `ENT-007` |
| **İngilizce** | Disease |
| **Türkçe** | Hastalık |
| **Çoğul** | Hastalıklar |

**Özellikler:** Tür (varroa/nosema/afb/efb/chalkbrood/sacbrood/shb), Şiddet, Risk, İlk Görülme, Durum

**İlişkiler:** `Hastalık ──TEDAVİ_EDİLİR──→ Tedavi`

---

## 8.2.11 Tedavi (Treatment) — `ENT-008`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Hastalığa karşı uygulanan işlem |
| **Kod** | `ENT-008` |
| **İngilizce** | Treatment |
| **Türkçe** | Tedavi |
| **Çoğul** | Tedaviler |

**Özellikler:** Ürün, Doz, Tarih, Sonuç, Bekleme Süresi

---

## 8.2.12 Kontrol (Inspection) — `ENT-009`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Arıcının yaptığı gözlem. Kontrol bir **olaydır.** |
| **Kod** | `ENT-009` |
| **İngilizce** | Inspection |
| **Türkçe** | Kontrol / Muayene |
| **Çoğul** | Kontroller / Muayeneler |

**Özellikler:** Tarih, Süre, Not, Fotoğraf, Video, AI Sonucu

---

## 8.2.13 Medya (Media) — `ENT-010`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Koloniye ait görsel/işitsel kayıt |
| **Kod** | `ENT-010` |
| **İngilizce** | Media |
| **Türkçe** | Medya |
| **Çoğul** | Medyalar |

**Türler:** Fotoğraf, Video, Ses, Termal Görüntü

> Her medya dosyası bir olaya bağlanmalıdır.

---

## 8.2.14 AI Önerisi (AI_Recommendation) — `ENT-011`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Karar Motoru tarafından üretilen tavsiye |
| **Kod** | `ENT-011` |
| **İngilizce** | AI Recommendation |
| **Türkçe** | AI Önerisi |
| **Çoğul** | AI Önerileri |

**Özellikler:** Güven (%), Risk, Sebep, Alternatif, Durum (bekleyen/kabul/red)

---

## 8.2.15 Görev (Task) — `ENT-012`

| Özellik | Değer |
|---------|-------|
| **Tanım** | Yapılması gereken işlem |
| **Kod** | `ENT-012` |
| **İngilizce** | Task |
| **Türkçe** | Görev |
| **Çoğul** | Görevler |

**Örnekler:** Besleme, Ana Arı Kontrolü, Varroa Tedavisi, Hasat

> Görevler AI tarafından oluşturulabilir ancak kullanıcı tarafından onaylanır.

---

## 8.2.16 İsimlendirme Kuralları

Her nesnenin:

| Kural | Örnek |
|-------|-------|
| Tekil adı vardır | Kovan |
| Çoğul adı vardır | Kovanlar |
| İngilizce teknik adı vardır | Hive |
| Türkçe görünen adı vardır | Kovan |
| Benzersiz kısa kodu vardır | ENT-002 |

### Varlık Kod Tablosu

| Kod | Türkçe | İngilizce | Tablo |
|-----|--------|-----------|-------|
| ENT-001 | Arılık | Apiary | `apiaries` |
| ENT-002 | Kovan | Hive | `hives` |
| ENT-003 | Koloni | Colony | `colonies` |
| ENT-004 | Ana Arı | Queen | `queens` |
| ENT-005 | Çerçeve | Frame | `frames` |
| ENT-006 | Petek | Comb | `combs` |
| ENT-007 | Hastalık | Disease | `diseases` |
| ENT-008 | Tedavi | Treatment | `treatments` |
| ENT-009 | Kontrol | Inspection | `inspections` |
| ENT-010 | Medya | Media | `media` |
| ENT-011 | AI Önerisi | AI Recommendation | `ai_recommendations` |
| ENT-012 | Görev | Task | `tasks` |

Bu standart API, veritabanı ve kullanıcı arayüzünde tutarlılık sağlar.

---

## 8.2.17 Zorunlu Kurallar

Her yeni nesne:

| # | Kural |
|---|-------|
| 1 | Resmi tanıma sahip olmalıdır |
| 2 | Benzersiz kimliğe (ENT-XXX) sahip olmalıdır |
| 3 | İzin verilen ilişkileri tanımlanmalıdır |
| 4 | Yaşam döngüsü belirtilmelidir |
| 5 | Dijital İkiz ile bağlantısı kurulmalıdır |

**Tanımlanmamış kavramlar sisteme eklenemez.**

---

## 8.2.18 Sonuç

Koloni Ontolojisi, BeeMaster AI'ın **ortak dilidir.**

Bu sayede:
- ✅ AI modelleri aynı kavramlarla çalışır
- ✅ Geliştiriciler farklı isimler üretmez
- ✅ API tutarlı kalır
- ✅ Veri analizi kolaylaşır
- ✅ Dijital İkiz uzun yıllar sürdürülebilir bir yapıya sahip olur

---

> **"Aynı şeyi iki farklı isimle çağırıyorsan, ontolojin eksiktir."**
