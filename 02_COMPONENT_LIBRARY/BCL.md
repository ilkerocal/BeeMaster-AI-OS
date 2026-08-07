# BÖLÜM 3 — UI Bileşen Kütüphanesi (BCL)

**Sürüm:** 1.0  
**Durum:** Zorunlu Standart  
**Kapsam:** Tüm UI bileşen geliştirmeleri

---

## 3.0 Amaç

BeeMaster AI içerisinde yeni arayüz elemanları geliştirirken temel kural şudur:

> **Önce mevcut bileşeni ara. Bulamazsan geliştir. Hiç yoksa oluştur.**

Hiçbir geliştirici veya AI, aynı işi yapan ikinci bir bileşen oluşturamaz.

---

## 3.1 Bileşen Felsefesi

Her bileşen aşağıdaki özelliklere sahip olmalıdır:

| # | Özellik | Açıklama |
|---|---------|----------|
| 1 | **Tek görev** | Bir bileşen yalnızca bir iş yapar |
| 2 | **Tekrar kullanılabilir** | Başka sayfalarda da çalışır |
| 3 | **Tasarım Sistemine uygun** | BDS token'larını kullanır |
| 4 | **Responsive** | Tüm breakpoint'lerde çalışır |
| 5 | **Erişilebilir** | Klavye, ekran okuyucu, kontrast |
| 6 | **Test edilebilir** | Birim testi yazılabilir |
| 7 | **Dokümante edilmiş** | COMP numarası ve kullanım kılavuzu var |

**Bir bileşen yalnızca tek bir sayfa için yazılamaz.**

---

## 3.2 Bileşen Hiyerarşisi

BeeMaster AI dört seviyeli bir yapı kullanır:

```
Sayfa (Page)
│
├── Bölüm (Section)
│
├── Bileşen (Component)
│
└── Alt Bileşen (Sub-component)
```

**Örnek:**

```
Dashboard
│
├── AI Özeti
│   ├── AI Kartı
│   ├── Güven Skoru Rozeti
│   └── Durum Göstergesi
│
├── Koloni Listesi
│   └── Hive Card (COMP-006)
│
└── Görevler
    └── Timeline (COMP-009)
```

---

## 3.3 Component Kimlik Sistemi

Her bileşenin benzersiz bir kodu vardır. Hermes geliştirme sırasında bu kimlikleri referans alır.

| Kod | Bileşen | Tip | Durum |
|-----|---------|-----|-------|
| COMP-001 | Button | Temel | ✅ |
| COMP-002 | Card | Temel | ✅ |
| COMP-003 | Sidebar | Yapısal | ✅ |
| COMP-004 | Navbar | Yapısal | ✅ |
| COMP-005 | Stat Card | Birleşik | ✅ |
| COMP-006 | Hive Card | Domain | ✅ |
| COMP-007 | AI Card | Domain | ✅ |
| COMP-008 | Disease Card | Domain | ✅ |
| COMP-009 | Timeline | Birleşik | ✅ |
| COMP-010 | Gauge | Birleşik | 📋 |
| COMP-011 | Weather Widget | Domain | 📋 |
| COMP-012 | Frame Summary | Domain | 📋 |
| COMP-013 | Modal | Temel | ✅ |
| COMP-014 | Input/Select | Temel | ✅ |
| COMP-015 | Badge | Temel | ✅ |

---

## 3.4 COMP-001 — Button

**Amaç:** Kullanıcının bir işlem başlatmasını sağlar.

**Kurallar:**
- Tek işlem yapar
- Kısa metin kullanır (1-3 kelime)
- İkon isteğe bağlıdır
- Yüklenme durumunu gösterebilir
- Devre dışı bırakılabilir

**Türleri (sadece 4):**

| Tür | Kullanım |
|-----|----------|
| Birincil (Primary) | Ana işlem |
| İkincil (Secondary) | Alternatif |
| Tehlike (Danger) | Silme |
| Metin (Ghost) | Düşük öncelik |

**Yasaklar:**
- ❌ Gradient buton
- ❌ Yanıp sönen buton
- ❌ Beş farklı renk
- ❌ Çok satırlı metin

---

## 3.5 COMP-002 — Card

Card, BeeMaster AI'ın **en önemli bileşenidir.** Her bilgi kart içinde gösterilir.

**Kart yapısı:**
```
┌────────────────────────┐
│ Başlık                 │
├────────────────────────┤
│ Ana Bilgi              │
├────────────────────────┤
│ Destek Bilgisi         │
├────────────────────────┤
│ Durum                  │
├────────────────────────┤
│ İşlem                  │
└────────────────────────┘
```

**Kural:** Kart içerisinde kart bulunamaz. İç içe kart kullanılmaz.

---

## 3.6 COMP-003 — Sidebar

Sidebar hiçbir zaman sadece menü değildir. Sidebar; **uygulamanın haritasıdır.**

**İçerik:**
- Dashboard
- Koloniler
- Dijital İkiz
- Frame Scanner
- AI
- Hastalık
- Hasat
- Raporlar
- Bilgi Merkezi
- Ayarlar

**Kurallar:**
- Sabit genişlik (260px)
- Daraltılabilir
- Mobilde Drawer olur

---

## 3.7 COMP-004 — Navbar

Navbar sayfa başlığı değildir. Navbar **uygulamanın kontrol merkezidir.**

**İçeriği:** Arama, Bildirim, Profil, Tema, Kısayollar

---

## 3.8 COMP-005 — Stat Card

Dashboard'da kullanılır.

**Örnek:**
```
┌─────────────────────┐
│ Koloni Sağlığı      │
│ 94%           ↑ +3% │
│ Son 7 Gün           │
└─────────────────────┘
```

Her Stat Card aynı düzeni kullanır.

---

## 3.9 COMP-006 — Hive Card

Bu BeeMaster AI'a özeldir.

**İçerik:**
- Kovan Adı
- Ana Arı
- Koloni Gücü
- Risk
- Bal
- Yavru
- AI Durumu

**Kural:** Kullanıcı bir bakışta koloniyi anlayabilmelidir.

---

## 3.10 COMP-007 — AI Card

AI önerileri için kullanılır.

**Yapı:**
```
┌─────────────────────────┐
│ ⬡ AI Önerisi            │
│ Besleme Gerekiyor        │
│ Güven: 94%              │
│ Neden? → Gerekçe         │
│ Sonraki İşlem → Aksiyon  │
└─────────────────────────┘
```

**Kural:** AI kartı sebep göstermeden öneri yapamaz (KURAL-0007).

---

## 3.11 COMP-008 — Disease Card

**İçerik:**
- Hastalık Adı
- Risk (yıldız)
- Belirtiler
- AI Güveni (%)
- İlk Görülme
- Son Tedavi

**Kural:** Her hastalık kartı aynı düzeni kullanır.

---

## 3.12 COMP-009 — Timeline

BeeMaster AI'ın en önemli bileşenlerinden biridir. **Her şey Timeline'da gösterilir.**

```
15 Mart  → Kontrol
20 Mart  → Besleme
4 Nisan  → Varroa
18 Nisan → Hasat
```

**Kural:** Hiçbir veri Timeline dışında saklanmaz. (KURAL-0002: her gözlem yeni sürüm)

---

## 3.13 COMP-010 — Gauge

Koloni sağlığı, AI güveni, risk, hasat için kullanılır.

**Özellik:** %0 ile %100 arasında dairesel veya çizgisel gösterge.

---

## 3.14 COMP-011 — Weather Widget

**İçerik:**
- Sıcaklık
- Nem
- Rüzgar
- Yağış
- Nektar Akımı
- AI Yorumu

---

## 3.15 COMP-012 — Frame Summary

Frame Scanner sonucu.

**Örnek:**
```
┌─────────────────────┐
│ Çerçeve             │
│ Yavru: 72%          │
│ Bal: 18%            │
│ Polen: 10%          │
│ Risk: Düşük         │
└─────────────────────┘
```

---

## 3.16 Bileşen Kuralları

Hermes bir bileşeni değiştirmeden önce şunları kontrol eder:

> Bu bileşen başka sayfalarda kullanılıyor mu?

**Evet ise** etkilenecek ekranlar listelenir. Değişiklik tüm ekranlarda test edilir.

---

## 3.17 Bileşen Yaşam Döngüsü

```
① Tasarla → ② Geliştir → ③ Test Et → ④ Dokümante Et → ⑤ Yayınla → ⑥ Bakım Yap
```

Her aşama tamamlanmadan sonrakine geçilmez.

---

## 3.18 Yeni Bileşen Ekleme Süreci (Zorunlu)

Hermes yeni bir bileşen oluşturmadan önce şu soruları cevaplar:

| # | Soru | Beklenen |
|---|------|----------|
| 1 | Aynı işi yapan mevcut bir bileşen var mı? | Kontrol et |
| 2 | Mevcut bileşen genişletilebilir mi? | Önce bunu dene |
| 3 | Yeni bileşen gerçekten gerekli mi? | Gerekçelendir |
| 4 | Tasarım Sistemi'ne uygun mu? | BDS token'ları |
| 5 | En az üç farklı sayfada kullanılabilecek mi? | Evet ise oluştur |

**Bu sorulardan herhangi birine olumsuz cevap verilirse, yeni bileşen oluşturulmaz.**

---

## 3.19 Bileşen Sürümleme

Her bileşenin sürümü vardır:

```
COMP-006 Hive Card v1.0
COMP-006 Hive Card v1.1  ← iyileştirme
COMP-006 Hive Card v2.0  ← büyük değişiklik
```

**Kural:** Eski sürümlerin neden değiştirildiği kayıt altına alınır. Changelog zorunludur.

---

## 3.20 Sonuç

BeeMaster AI'da ekranlar sıfırdan tasarlanmaz. Ekranlar, standart bileşenlerin doğru kombinasyonlarından oluşur.

Bu yaklaşım:
- ✅ Tutarlı bir kullanıcı deneyimi sağlar
- ✅ Bakım maliyetini azaltır
- ✅ Yeni özellik geliştirmeyi hızlandırır
- ✅ AI araçlarının rastgele arayüz üretmesini engeller

---

> **Artık Hermes:**
> 
> ❌ "Disease sayfası için yeni kart yapayım." **demeyecek.**
> 
> ✅ "COMP-008 Disease Card zaten var. Onu kullanacağım. Gerekirse sürümünü geliştireceğim." **diyecek.**
