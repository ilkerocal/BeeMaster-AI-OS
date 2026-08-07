# BÖLÜM 5 — Dijital İkiz Mimarisi (Digital Twin Architecture)

**Sürüm:** 1.0  
**Öncelik:** Kritik  
**Durum:** Zorunlu Standart  
**Kapsam:** Tüm sistemin temel veri modeli

---

## 5.0 Giriş

BeeMaster AI'ın gerçek ürünü;
- web sitesi **değildir,**
- mobil uygulama **değildir,**
- yapay zekâ **değildir.**

**Gerçek ürün; her koloni için yaşayan bir Dijital İkiz oluşturmaktır.**

Dijital İkiz; koloninin geçmişini, bugünkü durumunu, gelecekteki olası davranışlarını **tek bir model içerisinde** temsil eder.

---

## 5.1 Dijital İkiz Nedir?

Bir Dijital İkiz; **gerçek koloninin dijital dünyadaki yaşayan temsilcisidir.**

```
Gerçek Koloni                    Dijital İkiz
─────────────                    ────────────
     │                                │
     │  her olay işlenir              │
     ├───────────────────────────────►│
     │                                │
     │                         uygulama ekranları
     │                         aynı bilgiyi okur
     │                                │
```

Kolonide gerçekleşen her olay önce Dijital İkiz'e işlenir. Sonra uygulama ekranları aynı bilgiyi kullanır.

---

## 5.2 Dijital İkiz'in Temel İlkesi

> Gerçek koloni değiştikçe Dijital İkiz de değişir. Ancak **hiçbir bilgi kaybolmaz.** Koloni büyür. Dijital İkiz de büyür.

Bu ilke **KURAL-0001** (veri silinmez) ve **KURAL-0002** (üzerine yazılmaz, sürümlenir) ile güvence altındadır.

---

## 5.3 Dijital İkiz'in Yapısı

Her koloni yalnızca bir Dijital İkiz'e sahiptir (KURAL-0005).

```
Dijital İkiz
│
├── Kimlik                 ← UUID, ad, ırk, tip, konum
├── Yaşam Döngüsü          ← Kuruluş → Gelişim → Hasat → Kışlama
├── Ana Arı                ← Geçmiş/şimdiki kraliçeler
├── Çerçeveler             ← Her çerçevenin durumu
├── Koloni Gücü            ← Nüfus, yavru alanı
├── Hastalık Geçmişi       ← Tespitler, tedaviler
├── Tedaviler              ← İlaç, doz, süre
├── Beslemeler             ← Şurup, kek, miktar
├── Hasatlar               ← Bal, polen, propolis
├── Hava Durumu            ← Sıcaklık, nem, rüzgar
├── Fotoğraflar            ← Çerçeve taramaları
├── Videolar               ← Kovan kayıtları
├── AI Tahminleri          ← Gelecek kestirimleri
├── AI Kararları           ← Geçmiş öneriler
├── Kullanıcı Düzeltmeleri ← Feedback döngüsü
└── Olay Geçmişi           ← Timeline (tüm olaylar)
```

---

## 5.4 Kimlik Katmanı

Her koloni değişmeyen bir kimliğe sahiptir:

| Alan | Tip | Açıklama |
|------|-----|----------|
| `id` | UUID | Değişmez dijital kimlik |
| `name` | String | Kovan adı |
| `apiary_id` | UUID | Bağlı arılık |
| `strain` | Enum | Irk (karniyol, kafkas...) |
| `box_type` | Enum | Kovan tipi (langstroth, dadant...) |
| `created_at` | Timestamp | Oluşturulma tarihi |

Bu bilgiler değişse bile geçmiş sürümleriyle saklanır.

---

## 5.5 Olay Tabanlı Mimari

BeeMaster AI veri değil, **olay (event) saklar.**

```
12 Mart → Kontrol Yapıldı
15 Mart → Besleme Yapıldı
28 Mart → Varroa Tedavisi
7 Nisan → Hasat Yapıldı
```

Koloni geçmişi olaylardan oluşur. Her olay:
- Zaman damgası taşır
- Türü bellidir (inspection, feeding, treatment, harvest...)
- Değiştirilemez (immutable)
- Sıralıdır (Timeline)

---

## 5.6 Hafıza Katmanı

Dijital İkiz **unutmaz.** Saklanan ilk'ler:

- İlk ana arı
- Değişen ana arılar (tümü)
- İlk hastalık
- İlk oğul
- İlk bal hasadı
- İlk besleme
- İlk tarama
- İlk AI önerisi

Her olay zaman damgası ile birlikte kaydedilir.

---

## 5.7 İlişki Ağı

Kolonide **hiçbir bilgi tek başına değerlendirilmez.**

```
Ana Arı
├── Yumurta Verimi
│   └── Yavru Alanı
│       └── Koloni Gücü
│           └── Bal Verimi
│               └── Hastalık Riski
│                   └── Tedavi
│                       └── Ana Arı (döngü)
```

Bir değişiklik tüm ilgili göstergeleri etkileyebilir. (İlke 4: Her Veri Birbirine Bağlıdır)

---

## 5.8 Yaşam Döngüsü

Her koloni aşağıdaki aşamalardan geçebilir:

```
① Kuruluş
    ↓
② Gelişim
    ↓
③ Nektar Akımı
    ↓
④ Bal Üretimi
    ↓
⑤ Hasat
    ↓
⑥ Sonbahar Hazırlığı
    ↓
⑦ Kışlama
    ↓
⑧ İlkbahar Uyanışı
    ↓
    (döngü)
```

Dijital İkiz bulunduğu aşamayı bilir. Aşama değişimleri olay olarak kaydedilir.

---

## 5.9 Öğrenme Katmanı

Yapay zekâ her kullanıcı müdahalesini öğrenir (KURAL-0004).

**Örnek:**

| Adım | Olay |
|------|------|
| AI | "Besleme önerildi." |
| Kullanıcı | Besleme yapmadı. |
| Sonuç | Koloni güçlü kaldı. |
| Öğrenme | Bu koloni tipinde bu mevsimde besleme gerekmiyor olabilir. |

Bu bilgi, gelecekte benzer koloniler için değerlendirilir.

---

## 5.10 Tahmin Motoru

Dijital İkiz yalnızca geçmişi saklamaz. **Geleceği tahmin eder.**

| Tahmin | Dayanak |
|--------|---------|
| Oğul riski | Nüfus artış hızı, mevsim, kovan doluluğu |
| Açlık riski | Bal stoğu, nüfus, mevsim |
| Ana arı değişim ihtimali | Yaş, yumurta verimi düşüşü |
| Hastalık olasılığı | Geçmiş hastalıklar, hava durumu, bölge |
| Bal verimi | Geçmiş hasatlar, flora, hava durumu |
| Hasat tarihi | Çerçeve doluluk oranı, mevsim |
| Koloni nüfusu | Yumurta verimi, mevsim, besleme |

Her tahmin güven puanı ile birlikte sunulur (KURAL-0007).

---

## 5.11 Güven Skoru

Her AI çıktısı şu alanları içerir:

```
Varroa Riski: %87

╔════════════════════════════╗
║ ⬡ AI GÜVEN ANALİZİ         ║
║                            ║
║ Güven:        %87         ║
║ Veri Kalitesi: %94         ║
║ Gözlem Sayısı: 12 kontrol  ║
║               134 fotoğraf ║
║               2 tedavi     ║
║ Son Güncelleme: 2 saat önce║
║                            ║
║ Açıklama:                  ║
║ Son 3 kontrolde varroa     ║
║ sayısı artıyor.            ║
╚════════════════════════════╝
```

---

## 5.12 Dijital İkiz Sağlık Puanı

Her koloni için **tek bir sağlık puanı** hesaplanır.

Bu puan şu faktörlerden oluşur:

| Faktör | Ağırlık |
|--------|---------|
| Ana Arı durumu | %20 |
| Yavru alanı | %20 |
| Bal stoğu | %15 |
| Hastalık durumu | %15 |
| Besleme durumu | %10 |
| Hava durumu etkisi | %10 |
| Aktivite seviyesi | %5 |
| Geçmiş performans | %5 |

---

## 5.12A Davranış Profili

Her koloni zaman içinde kendine özgü bir **davranış profili** oluşturur. Bu profil, geçmiş verilere dayanarak sürekli güncellenir.

| Özellik | Veri Kaynağı |
|----------|-------------|
| Erken gelişme eğilimi | İlkbahar nüfus artış hızı |
| Oğul verme eğilimi | Geçmiş oğul olayları, ana arı yaşı |
| Bal depolama davranışı | Mevsimsel bal stoğu değişimi |
| Polen toplama yoğunluğu | Polen hücresi yüzdesi trendi |
| Savunmacılık gözlemleri | Kullanıcı notları, mizaç kayıtları |
| Mevsimsel değişim paterni | Yıllık döngü karşılaştırması |

## 5.12B Çerçeve Haritası

Koloninin tüm çerçeveleri Dijital İkiz içinde temsil edilir. Her çerçeve için: son tarama tarihi, bal oranı (%), polen oranı (%), yavru alanı (%), geçmiş değişimler saklanır. Bu sayede zaman içinde aynı çerçevenin gelişimi izlenebilir. (Bölüm 7.8: Değişim Analizi)

## 5.12C Tahmin Hafızası

Sistem yalnızca geçmişi değil, **geçmiş tahminlerini de saklar.** Örnek:

```
Tahmin (15 Nisan): 15 gün içinde oğul riski %70
Gerçek sonuç (30 Nisan): Oğul gerçekleşmedi
→ Model kalibrasyonu için kaydedilir
```

Bu karşılaştırmalar modelin geliştirilmesine katkı sağlar. (Bölüm 10.7: Sonuçların Takibi, Bölüm 12.13: Öğrenen Simülasyon)

## 5.12D Dijital İkiz Güncelleme Süreci

Her yeni veri şu akıştan geçer:

```
Yeni Veri → Doğrulama → İlgili DI Bulunur → Olay Kaydı → AI Analizi → Profil Güncellenir → Tahminler Yenilenir
```

Bu süreç tutarlı bir Dijital İkiz yapısı sağlar. (Bölüm 11.14: Olay Tabanlı Entegrasyon)

## 5.12E Sürüm Geçmişi (DI Snapshot)

Dijital İkiz yalnızca son durumu değil, **geçmiş sürümlerini de saklar.** Kullanıcı belirli bir tarihteki koloni durumunu, o günkü AI değerlendirmesini ve kullanılan model sürümünü görebilir. (KURAL-0002, Bölüm 10.10: Bilgi Tabanı Sürümleme)

## 5.12F Karşılaştırmalı Analiz

Sistem aynı koloniyi farklı dönemlerde karşılaştırabilir:

```
İlkbahar 2026 vs İlkbahar 2027 vs İlkbahar 2028
```

Karşılaştırmalar: gelişim hızı, bal üretimi, hastalık sıklığı, ana arı performansı üzerinden yapılır.

## 5.12G Çoklu AI Entegrasyonu

Dijital İkiz tüm uzman ajanlardan veri alır (Bölüm 9):

```
Vision Agent → Disease Agent → Prediction Agent → Learning Agent → Digital Twin
```

Her ajan aynı Dijital İkiz üzerinde çalışır; ancak kendi uzmanlık alanındaki bilgileri günceller. (KURAL-0006)

---

## 5.13 Dijital İkiz Zaman Çizelgesi

Koloninin tüm geçmişi tek bir zaman çizelgesinde görülebilir:

```
2025 ──────────────────────────────────────
│
├── Nisan: İlk Kurulum
├── Mayıs: İlk Kontrol
├── Haziran: İlk Besleme
├── Temmuz: Varroa Tespiti
├── Ağustos: Hasat (14 kg)
├── Eylül: Sonbahar Beslemesi
├── Kasım: Kışlama Başlangıcı
│
2026 ──────────────────────────────────────
│
├── Mart: İlkbahar Kontrolü
├── Nisan: Oğul Önleme
└── ...
```

---

## 5.14 Dijital İkiz Kuralları (Değiştirilemez)

| # | Kural |
|---|-------|
| 1 | Her olay kayıt altına alınır |
| 2 | Hiçbir veri silinmez (KURAL-0001) |
| 3 | Veriler sürümlenir (KURAL-0002) |
| 4 | AI tahminleri geçmişte saklanır (KURAL-0003) |
| 5 | Kullanıcı düzeltmeleri kaydedilir (KURAL-0004) |
| 6 | Her güncelleme zaman damgası taşır (İlke 5) |
| 7 | Tüm modüller aynı Dijital İkiz'i kullanır (KURAL-0006) |

---

## 5.15 Modüllerle İlişki

Dijital İkiz, tüm modüllerin **ortak veri kaynağıdır:**

```
Dijital İkiz (tek kaynak)
├── Dashboard       ← Özet, sağlık puanı
├── Hives           ← Kovan detayı
├── Diseases        ← Hastalık geçmişi
├── Frame Scanner   ← Çerçeve analizi
├── Weather         ← Hava durumu
├── Harvest         ← Hasat verisi
├── Queen Manager   ← Ana arı takibi
├── Reports         ← Raporlar
└── Tasks           ← Görevler
```

**Hiçbir modül kendi kopya verisini tutmaz.** (KURAL-0006)

---

## 5.16 Gelecek Vizyonu

BeeMaster AI yalnızca geçmişi gösteren bir sistem olmayacaktır.

Amaç; her koloni için **yaşayan, öğrenen, tahmin yapan, öneriler sunan, kendini geliştiren** bir Dijital İkiz oluşturmaktır.

Uzun vadede bu Dijital İkiz;
- IoT sensörleri (sıcaklık, nem, ağırlık, ses),
- yüksek çözünürlüklü çerçeve taramaları,
- ses analizleri (oğul tespiti, ana arı varlığı),
- hava durumu servisleri,
- genetik bilgiler (ırk, direnç),
- ve kullanıcı geri bildirimleriyle

sürekli zenginleşecektir.

---

## 5.17 Sonuç

BeeMaster AI'da gerçek "ürün" ekranlar değil, **Dijital İkiz'dir.**

- Ekranlar değişebilir.
- Teknolojiler değişebilir.
- Mobil uygulama, web uygulaması veya masaüstü uygulaması değişebilir.

**Ancak Dijital İkiz modeli kalıcıdır ve tüm sistem onun etrafında şekillenir.**

---

> **"Her kovanın bir ruhu vardır. Biz ona Dijital İkiz diyoruz."**
