# BÖLÜM 12 — Tahmin, Simülasyon ve Senaryo Motoru (Prediction, Simulation & Scenario Engine)

**Sürüm:** 1.0  
**Öncelik:** Kritik  
**Durum:** Zorunlu Standart  
**Kapsam:** Gelecek tahmini ve senaryo modelleme

---

## 12.0 Vizyon

BeeMaster AI yalnızca geçmişi kaydetmez. Yalnızca bugünü analiz etmez. Aynı zamanda **gelecekte oluşabilecek olası senaryoları hesaplar.**

Sistem kesin gelecek tahmini yapmaz. Farklı olasılıkları ve bunların güven seviyelerini kullanıcıya sunar.

---

## 12.1 Temel Felsefe

Tahmin ile simülasyon aynı şey değildir:

| Tahmin | Simülasyon |
|--------|------------|
| "Muhtemelen şu olacak." | "Eğer bunu yaparsan, şu sonuçlar ortaya çıkabilir." |

BeeMaster AI her iki yaklaşımı da destekler.

---

## 12.2 Simülasyon Döngüsü

Her senaryo aynı süreçten geçer. Gerçek veriler değiştirilmez; yalnızca sanal bir kopya üzerinde hesaplama yapılır.

```
Dijital İkiz → Mevcut Durum Analizi → Senaryo Seçimi → AI Simülasyonu → Risk Hesabı → Tahmini Sonuçlar → Karşılaştırmalı Rapor
```

---

## 12.3 Desteklenen Senaryolar (İlk Sürüm)

| Senaryo | Tip |
|---------|-----|
| Besleme yapılırsa / yapılmazsa | Besleme |
| Ana arı değiştirilirse / değiştirilmezse | Kraliçe |
| Varroa tedavisi uygulanırsa / ertelenirse | Hastalık |
| Hasat erkene alınırsa / geciktirilirse | Hasat |
| Koloni bölünürse / birleştirilirse | Yönetim |

Yeni senaryolar modüler olarak eklenebilir.

---

## 12.4 "Ne Olursa?" Analizi

Kullanıcı örneğin: "Bu hafta besleme yapmazsam ne olur?"

| Gösterge | Beklenen Değişim |
|----------|-----------------|
| Koloni Gücü | Hafif azalma |
| Yavru Alanı | Orta düzey azalma |
| Bal Stoğu | Değişmeyebilir |
| Oğul Riski | Hafif artış |
| **Güven Seviyesi** | **%82** |

Bu sonuçlar olasılık temellidir.

---

## 12.5 Çoklu Senaryo Karşılaştırması

| Senaryo | Beklenen Sonuç | Risk |
|---------|---------------|------|
| Bugün besleme | Düşük risk | 🟢 Düşük |
| 7 gün sonra besleme | Orta risk | 🟡 Orta |
| Besleme yapılmaması | Gelişim yavaşlayabilir | 🟠 Yüksek |

Karşılaştırmalar aynı başlangıç durumuna göre yapılır.

---

## 12.6 Zaman Ufku

| Ufuk | Belirsizlik |
|------|-------------|
| 3 gün | Düşük |
| 7 gün | Düşük-Orta |
| 14 gün | Orta |
| 30 gün | Orta-Yüksek |
| Sezon sonu | Yüksek |
| Kışlama dönemi | Yüksek |

Daha uzun vadeli tahminlerde belirsizlik artabilir. Bu durum kullanıcıya açıkça belirtilir.

---

## 12.7 Belirsizlik Yönetimi

Her simülasyon şu bilgileri içerir: Güven puanı, Kullanılan veri miktarı, Varsayımlar, Belirsizlik seviyesi.

**Belirsizlik gizlenmez.** Kullanıcı, sonucun hangi varsayımlara dayandığını görebilir.

---

## 12.8 Dijital İkiz Kopyası

Simülasyon gerçek koloni üzerinde çalışmaz:

```
Gerçek Dijital İkiz → Geçici Simülasyon Kopyası → Senaryo Çalıştırılır → Sonuçlar Üretilir → Kopya Silinir
```

Gerçek veriler asla değiştirilmez.

---

## 12.9 Çevresel Etkiler

Tahminler yalnızca koloni verilerine dayanmaz: Hava durumu, Mevsim, Nektar akımı, Rakım, Bölgesel iklim, Önceki yılların kayıtları da dikkate alınır.

---

## 12.10 Olay Zinciri Simülasyonu

Tek bir olay yerine olay dizileri test edilebilir:

```
Besleme → Koloni Gücü Artışı → Yavru Artışı → Bal Üretimi → Tahmini Hasat
```

Her adım bir sonrakini etkileyebilir. (Bölüm 5.7: İlişki Ağı)

---

## 12.11 Senaryo Kütüphanesi

Önceden tanımlanmış kategoriler: İlkbahar hazırlığı, Bal akımı, Oğul önleme, Kışlama, Hastalık yönetimi, Ana arı yenileme. Kullanıcı kendi senaryolarını da oluşturabilir.

---

## 12.12 Karşılaştırmalı Görselleştirme

Her senaryo grafiklerle karşılaştırılabilir: Koloni gücü eğrisi, Bal stoğu değişimi, Yavru alanı gelişimi, Risk seviyesi, Sağlık puanı.

> Grafikler gerçek kayıtlarla karıştırılmamalıdır; **simülasyon olduğu açıkça belirtilmelidir.**

---

## 12.13 Öğrenen Simülasyon

Zaman içinde simülasyon sonuçları gerçek sonuçlarla karşılaştırılır:

```
Tahmin: 30 gün içinde koloni güçlenecek.
Gerçek: Beklenenden daha yavaş gelişti.
→ Model güncellenir (Bölüm 10: Sürekli Öğrenme)
```

---

## 12.14 Sınırlar

BeeMaster AI **hiçbir zaman** "Kesinlikle böyle olacak" demez.

Bunun yerine: "Bu verilere göre olası senaryo...", "Tahmini sonuç...", "Belirsizlik seviyesi...", "Alternatif senaryolar..." ifadeleri kullanılır.

---

## 12.15 Performans Ölçümü

| Metrik | Hedef |
|--------|-------|
| Tahmin doğruluğu | >%70 |
| Ortalama hata oranı | <%30 |
| Güven puanı kalibrasyonu | ±%10 sapma |
| Gerçekleşen senaryo uyumu | >%65 |
| Kullanıcı memnuniyeti | >4.0/5 |

---

## 12.16 Sonuç

Tahmin ve Simülasyon Motoru sayesinde BeeMaster AI; yalnızca kayıt tutan, yalnızca analiz yapan bir sistem olmaktan çıkar. Kullanıcının kararlarını farklı senaryolar altında değerlendirmesine yardımcı olan, geleceğe yönelik etkileri modelleyen bir **karar destek platformuna** dönüşür.

---

> **"Geleceği bilmek değil, olasılıkları anlamak."**
