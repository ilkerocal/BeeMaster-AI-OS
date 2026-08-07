# BÖLÜM 8 — Koloni Bilgi Grafiği (Colony Knowledge Graph)

**Sürüm:** 1.0  
**Öncelik:** Kritik  
**Durum:** Zorunlu Standart  
**Kapsam:** Veri ilişkileri ve anlamsal ağ

---

## 8.0 Giriş

BeeMaster AI'ın amacı yalnızca veri depolamak **değildir.**

Amaç; **veriler arasındaki ilişkileri anlamaktır.**

Örneğin; bir ana arının yaşlanması tek başına önemli değildir. Ama;

- yavru miktarı,
- bal üretimi,
- oğul eğilimi,
- hastalık riski,
- besleme ihtiyacı

ile birlikte değerlendirildiğinde anlam kazanır.

İşte bu ilişkileri yöneten sistem: **Koloni Bilgi Grafiği'dir.**

---

## 8.1 Bilgi Grafiği Nedir?

Bilgi Grafiği; koloniye ait **her varlığı** ve bunların birbirleriyle olan **ilişkilerini** tek bir ağ içerisinde temsil eder.

```
Tablo Bazlı (İlişkisel DB)          Bilgi Grafiği (Graph)
─────────────────────────          ────────────────────
hives → inspections                Hive ──HAS──→ Queen
  (foreign key)                             │
                                     Queen ──PRODUCES──→ Eggs
                                               │
                                     Eggs ──BECOME──→ Larvae
                                               │
                                     Larvae ──BECOME──→ Workers
                                               │
                                     Workers ──PRODUCE──→ Honey
```

BeeMaster AI verileri tablo olarak değil, **ilişki ağı olarak** düşünür.

---

## 8.2 Temel Prensip

> Her bilgi; başka bilgilerle bağlantılıdır. Hiçbir kayıt tek başına değerlendirilmez.

```
Ana Arı → Yumurta → Larva → Yavru → İşçi Arı → Bal Üretimi
```

Bu zincirin herhangi bir halkasındaki değişiklik, diğer halkaları da etkileyebilir. (İlke 4: Her Veri Birbirine Bağlıdır)

---

## 8.3 Bilgi Grafiğinin Yapısı

Grafik iki temel parçadan oluşur:

### Düğümler (Nodes)

Her gerçek nesne bir düğümdür:

| Düğüm Tipi | Örnek |
|------------|-------|
| Koloni | Kovan #42 |
| Ana Arı | Kraliçe 2024-A |
| Çerçeve | Çerçeve #7 |
| Petek | Hücre (x,y) |
| Yumurta | Yumurta kümesi |
| Larva | 3 günlük larva |
| Bal | Kapalı bal hücresi |
| Polen | Polen deposu |
| Varroa | Parazit tespiti |
| İlaç | Oksalik asit |
| Fotoğraf | Tarama #128 |
| Video | Kovan kaydı |
| Hava Durumu | 28°C, %35 nem |
| Hasat | 14 kg süzme bal |
| Görev | "Besleme yap" |
| AI Tahmini | "Oğul riski: %72" |

### İlişkiler (Edges)

Düğümler birbirine anlamlı bağlantılarla bağlanır.

---

## 8.4 Temel Varlık Hiyerarşisi

Her Dijital İkiz aşağıdaki ana varlıklardan oluşur:

```
Koloni
├── Ana Arı
│   └── Yumurta → Larva → Yavru → İşçi Arı
├── Çerçeveler
│   └── Petek Hücreleri
│       ├── Bal
│       ├── Polen
│       └── Yavru
├── Hastalıklar
│   └── Tedaviler
├── Hasatlar
├── Beslemeler
├── Fotoğraflar
│   └── AI Analizleri
├── Videolar
├── Sensör Verileri
├── Hava Durumu Kayıtları
└── AI Kararları
    └── Kullanıcı Geri Bildirimleri
```

---

## 8.5 İlişki Türleri (Standart)

Her bağlantının tanımlı bir anlamı vardır. Yeni ilişki eklenmeden önce mevcut tanımlar kontrol edilir.

| İlişki | Açıklama | Örnek |
|--------|----------|-------|
| `SAHİPTİR` | Üst varlık alt varlığa sahiptir | Koloni → Ana Arı |
| `İÇERİR` | Kapsayıcılık | Kovan → Çerçeve |
| `OLUŞTURUR` | Üretim | Ana Arı → Yumurta |
| `DÖNÜŞÜR` | Gelişim | Larva → İşçi Arı |
| `ETKİLER` | Nedensel olmayan etki | Hastalık → Koloni Gücü |
| `TEDAVİ_EDİLDİ` | Tedavi ilişkisi | Hastalık → İlaç |
| `GÖZLENDİ` | Gözlem kaydı | Çerçeve → Fotoğraf |
| `ANALİZ_EDİLDİ` | AI analizi | Fotoğraf → AI Sonucu |
| `TAHMİN_EDER` | AI kestirimi | AI → Risk |
| `ÖNERİR` | Aksiyon önerisi | AI → Görev |
| `SONUÇLANDI` | Karar sonucu | Öneri → Kullanıcı Kararı |
| `KAYDEDİLDİ` | Veri girişi | Kullanıcı → Gözlem |

---

## 8.6 Zaman Boyutu

Bilgi Grafiği yalnızca "şu anı" göstermez. **Her ilişki zaman damgası taşır.**

```
15 Nisan → Koloni ──BESLENDİ──→ 2 kg şurup
20 Nisan → Koloni ──DURUMU──→ Bal stoğu +3 kg
```

Aynı ilişki farklı tarihlerde farklı değerlere sahip olabilir. Grafik zaman içinde **katmanlanır.**

---

## 8.7 Nedensellik

BeeMaster AI ilişki ile nedenselliği **karıştırmaz.**

| Korelasyon | Nedensellik |
|------------|-------------|
| Yağmurdan sonra bal üretimi arttı | Yağmur bal üretimini artırdı |
| Sistem bunu KAYDEDER | Sistem bunu KESİN OLARAK söylemez |

Sistem yalnızca destekleyen **yeterli veri olduğunda** nedensel çıkarımlar üretir. Aksi halde "korelasyon tespit edildi, nedensellik doğrulanmadı" der.

---

## 8.8 Bilgi Grafiğinin Güncellenmesi

Grafik aşağıdaki olaylarla güncellenir:

| Olay | Eklenen |
|------|---------|
| Yeni kontrol | Düğüm: Inspection |
| Yeni fotoğraf | Düğüm: Photo → İlişki: GÖZLENDİ |
| Frame Scanner analizi | Düğüm: Analysis → İlişki: ANALİZ_EDİLDİ |
| Hava durumu değişimi | Düğüm: Weather |
| Hastalık kaydı | Düğüm: Disease → İlişki: ETKİLER |
| Tedavi | Düğüm: Treatment → İlişki: TEDAVİ_EDİLDİ |
| Besleme | Düğüm: Feeding |
| Hasat | Düğüm: Harvest |
| Ana arı değişimi | Yeni Düğüm: Queen → İlişki: SAHİPTİR |
| Kullanıcı düzeltmesi | İlişki: SONUÇLANDI (KURAL-0004) |

**Hiçbir güncelleme eski ilişkileri silmez; yeni sürümler oluşturur.** (KURAL-0002)

---

## 8.9 AI ve Bilgi Grafiği

Karar Motoru yalnızca ham veriyi kullanmaz. **Önce Bilgi Grafiğini sorgular.**

**Örnek sorgu:**

> "Son üç yılda benzer ana arı yaşına, benzer iklime ve benzer yavru desenine sahip kolonilerde hangi sonuçlar gözlendi?"

Bu sayede öneriler tek bir ölçüme değil, **ilişkiler ağına** dayanır. (Bölüm 6.5: İlişki Analizi)

---

## 8.10 Dijital İkiz ile Entegrasyon

Bilgi Grafiği, Dijital İkiz'in **ilişkisel katmanıdır.**

| Sistem | Rolü |
|--------|------|
| **Dijital İkiz** | Hafızayı tutar (ham veri) |
| **Bilgi Grafiği** | Bağlantıları yönetir (ilişki ağı) |
| **Karar Motoru** | Bu bağlantıları analiz eder |
| **Frame Scanner** | Yeni düğümler ve ilişkiler ekler |

```
Frame Scanner → [yeni düğüm/ilişki] → Bilgi Grafiği
                                         │
                                    Karar Motoru ← sorgular
                                         │
                                    Dijital İkiz ← güncellenir
```

Bu dört sistem birlikte çalışır.

---

## 8.11 Sonuç

Koloni Bilgi Grafiği sayesinde BeeMaster AI;

- ❌ yalnızca kayıt tutan,
- ❌ yalnızca analiz yapan,

bir uygulama olmaktan çıkar.

Bunun yerine;
- ✅ ilişkileri anlayan,
- ✅ zaman içindeki değişimleri takip eden,
- ✅ ve bu ilişkilerden yeni çıkarımlar üretebilen

bir **karar destek platformuna** dönüşür.

---

> **"Veri tek başına anlamsızdır. Anlam, ilişkilerdedir."**
