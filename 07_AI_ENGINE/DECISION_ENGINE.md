# BÖLÜM 6 — BeeMaster AI Karar Motoru (Decision Engine)

**Sürüm:** 1.0  
**Öncelik:** Kritik  
**Durum:** Zorunlu Standart  
**Kapsam:** Tüm AI karar ve öneri süreçleri

---

## 6.0 Amaç

Karar Motoru'nun görevi kullanıcıya bilgi göstermek **değildir.**

Görevi;
- eldeki verileri değerlendirmek,
- eksik bilgileri tespit etmek,
- riskleri hesaplamak,
- olası senaryoları oluşturmak,
- en uygun öneriyi sunmaktır.

**Karar Motoru hiçbir zaman kesin hüküm vermez.** Her zaman olasılık ve güven seviyesi ile çalışır.

---

## 6.1 Karar Felsefesi

BeeMaster AI aşağıdaki sıraya göre düşünür:

```
VERİ → BİLGİ → ANALİZ → TAHMİN → RİSK → ÖNERİ → ÖĞRENME
```

Sadece veri gösteren sistemler akıllı değildir. BeeMaster AI'ın amacı; **veriden anlam üretmektir.**

---

## 6.2 Karar Katmanları

Karar Motoru **yedi katmandan** oluşur. Her katman tamamlanmadan sonraki katmana geçilemez.

```
① Veri Kontrolü
    ↓
② Bağlam Analizi
    ↓
③ İlişki Analizi
    ↓
④ Risk Analizi
    ↓
⑤ Tahmin
    ↓
⑥ Öneri
    ↓
⑦ Öğrenme
```

---

## 6.3 Katman 1 — Veri Kontrolü

İlk adım veri kalitesidir. Karar Motoru şu soruları sorar:

| Soru | Kontrol |
|------|---------|
| Veri eksik mi? | Zorunlu alanlar dolu mu? |
| Veri güncel mi? | Son 30 gün içinde mi? |
| Veri çelişkili mi? | Aynı tarihte çakışan kayıt var mı? |
| Fotoğraf kalitesi yeterli mi? | Çözünürlük, ışık, netlik |
| Sensör verisi güvenilir mi? | Anomali tespiti |
| Kullanıcı girişi mantıklı mı? | Aralık kontrolü (örn: varroa 0-50) |

**Eksik veya güvenilmez veri varsa sistem bunu açıkça belirtir.** Tahmin üretmez.

---

## 6.4 Katman 2 — Bağlam Analizi

Aynı veri her zaman aynı anlama gelmez.

**Örnek:** 6 çerçeve yavru

| Bağlam | Değerlendirme |
|--------|---------------|
| İlkbahar | ✅ Normal |
| Sonbahar | ⚠️ Beklenmedik olabilir |

Karar Motoru her zaman şu bağlamları değerlendirir:
- Mevsim
- Bölge (rakım, iklim)
- Hava durumu
- Koloni yaşı
- Ana arı yaşı
- Son müdahaleler (tedavi, besleme, hasat)

---

## 6.5 Katman 3 — İlişki Analizi

Tek bir veriyle karar verilmez.

**Örnek:** Varroa riski hesaplanırken değerlendirilen veriler:

```
Varroa Riski
├── Çerçeve taraması (son 3)
├── Açık yavru miktarı
├── Kapalı yavru miktarı
├── Son tedavi tarihi
├── Hava sıcaklığı
├── Koloni gücü
└── Geçmiş enfestasyon kayıtları
```

Karar, bu verilerin birlikte değerlendirilmesiyle oluşur. (İlke 4)

---

## 6.6 Katman 4 — Risk Analizi

Her öneri önce risk açısından değerlendirilir.

| Seviye | Açıklama | Aksiyon |
|--------|----------|---------|
| 🟢 Düşük | Müdahale gerekmiyor | Rutin takip |
| 🟡 Orta | Takip önerilir | Sıkı gözlem |
| 🟠 Yüksek | Yakın zamanda müdahale edilmeli | Planlı aksiyon |
| 🔴 Kritik | Acil işlem önerilir | Hemen müdahale |

Risk puanı hesaplanırken:
- Veri güvenilirliği
- Olası sonuçların etkisi
- Geçmiş olaylar

birlikte değerlendirilir.

---

## 6.7 Katman 5 — Tahmin

Karar Motoru geleceği tahmin etmeye çalışır.

| Tahmin | Dayanak |
|--------|---------|
| 10 gün içinde oğul riski artabilir | Nüfus artışı + mevsim |
| 7 gün içinde besleme gerekebilir | Bal stoğu düşüşü |
| Bal akımı başlayabilir | Flora + hava durumu |
| Ana arı performansı düşebilir | Yaş + yumurta verimi trendi |
| Hastalık yayılma riski yükselebilir | Komşu kovan verisi |

**Her tahmin tarih ve güven puanı içerir.**

---

## 6.8 Katman 6 — Öneri

Öneriler emir değildir. Her öneri şu formatta sunulur:

```
╔══════════════════════════════════╗
║  ⬡ AI ÖNERİSİ                    ║
║                                  ║
║  Öneri: Varroa kontrolü          ║
║  yapılması önerilir.             ║
║                                  ║
║  Neden: Son iki kontrolde        ║
║  risk artışı gözlendi.           ║
║                                  ║
║  Güven: %91  Risk: Yüksek       ║
║                                  ║
║  Alternatifler:                  ║
║  • 3 gün gözlem yap              ║
║  • Hemen tedavi uygula           ║
║  • Laboratuvar doğrulaması       ║
║                                  ║
║  ⚠️ Son karar arıcıya aittir.   ║
╚══════════════════════════════════╝
```

**Kullanıcı son kararı verir.**

---

## 6.9 Katman 7 — Öğrenme

Kullanıcının verdiği karar sistem için değerlidir (KURAL-0004).

**Örnek:**

| Adım | Olay |
|------|------|
| AI | Besleme önerdi |
| Kullanıcı | Besleme yapmadı |
| Sonuç | Koloni güçlü kaldı |
| Kayıt | Olay kaydedildi |

Ancak **tek bir olaydan genel kural üretilmez.** Öğrenme, çok sayıda benzer olayın değerlendirilmesiyle gerçekleşir.

---

## 6.10 Güven Skoru

Her AI çıktısı bir güven skoru taşır. Bu skor şu faktörlerden etkilenir:

| Faktör | Etki |
|--------|------|
| Veri miktarı | Ne kadar çok veri, o kadar yüksek güven |
| Veri güncelliği | Eski veri → düşük güven |
| Görsel analiz kalitesi | Net fotoğraf → yüksek güven |
| Kullanılan model | Model versiyonu ve doğruluk oranı |
| Benzer geçmiş olay sayısı | Çok örnek → yüksek güven |

**Düşük kaliteli veri yüksek güven puanı üretemez.**

---

## 6.11 Çelişkili Veriler

Farklı kaynaklar farklı sonuç verirse:

1. Çelişki kullanıcıya bildirilir
2. Olası nedenler açıklanır
3. Ek gözlem önerilir

**Sistem kesin olmayan bir sonucu kesinmiş gibi sunmaz.**

---

## 6.12 Karar Kayıtları

Her AI kararı saklanır (KURAL-0003).

Kayıt içeriği:
- Tarih
- Kullanılan veriler
- Üretilen öneri
- Güven puanı
- Kullanıcı kararı (kabul/red/düzeltme)
- Sonuç (ne oldu?)

Bu kayıtlar gelecekte model değerlendirmesi için kullanılır.

---

## 6.13 İnsan Kontrolü

BeeMaster AI **hiçbir zaman** kullanıcı adına işlem yapmaz.

| AI yapar | Kullanıcı yapar |
|----------|-----------------|
| Önerir | Karar verir |
| Açıklar | Uygular |
| Gerekçelendirir | Düzeltir |

---

## 6.14 Şeffaflık

Her öneri şu soruları cevaplamalıdır:

| Soru | Cevap formatı |
|------|---------------|
| Bu öneri neden verildi? | Gerekçe metni |
| Hangi verilere dayanıyor? | Veri kaynakları listesi |
| Güven seviyesi nedir? | %0-99 |
| Belirsizlik var mı? | Varsa açıkça belirt |
| Alternatif seçenekler nelerdir? | En az 2 alternatif |

**Kullanıcı "kara kutu" bir sistemle karşı karşıya kalmamalıdır.**

---

## 6.15 Hata Yönetimi

Karar Motoru aşağıdaki durumlarda **karar üretmez:**

| Durum | Aksiyon |
|-------|---------|
| Veri yetersizse | "Daha fazla veri gerekiyor" |
| Fotoğraf okunamıyorsa | "Fotoğraf kalitesi yetersiz" |
| Tarihler tutarsızsa | "Tarih çakışması tespit edildi" |
| Çelişkili kayıtlar çözülememişse | "Çelişkili veri, ek gözlem önerilir" |

Bu durumda kullanıcıdan ek bilgi ister. **Yanlış tahmin yapmaktansa hiç yapmamak.**

---

## 6.16 Sürekli Gelişim

Karar Motoru;
- bilimsel araştırmalar,
- saha deneyimleri,
- kullanıcı geri bildirimleri,
- ve yeni AI modelleri

doğrultusunda güncellenebilir.

Ancak her değişiklik sürümlendirilir ve geçmiş kararların hangi sürümle üretildiği kayıt altına alınır.

---

## 6.17 Sonuç

BeeMaster AI'ın değeri yalnızca veri toplamasında değil, **güvenilir ve açıklanabilir karar desteği sunmasında** yatar.

Karar Motoru;
- ✅ belirsizliği gizlemez,
- ✅ kullanıcıyı yönlendirir,
- ✅ gerekçe sunar,
- ✅ öğrenir,
- ✅ ancak son kararı her zaman arıcıya bırakır.

---

> **"AI karar vermez. AI düşünür, önerir, açıklar. Karar arıcınındır."**
