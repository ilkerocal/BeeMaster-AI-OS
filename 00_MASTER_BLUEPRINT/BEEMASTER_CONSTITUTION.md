# BÖLÜM 0 — BeeMaster AI Anayasası

**Sürüm:** 1.0  
**Durum:** Değiştirilemez Temel Kurallar  
**Kapsam:** Tüm AI agent'lar ve insan geliştiriciler

---

## Giriş

Bu belge BeeMaster AI'ın en üst seviyedeki teknik standardıdır.

BeeMaster AI üzerinde çalışan;
- Hermes
- DeepSeek
- Claude
- Codex
- GitHub Copilot
- İnsan geliştiriciler

aynı kurallara uymak zorundadır.

Bu belge; tasarımın, kodun, mimarinin, yapay zekânın, veritabanının, arayüzün, testlerin ve gelecekte geliştirilecek bütün sistemlerin temelini oluşturur.

**Bu belgede yazan kurallar, proje sahibinin onayı olmadan değiştirilemez.**

---

## 0.1 BeeMaster AI Nedir?

BeeMaster AI bir kayıt uygulaması **değildir.**

BeeMaster AI bir arıcılık defteri **değildir.**

BeeMaster AI bir bal üretim uygulaması **değildir.**

BeeMaster AI; **her kovan için yaşayan bir Dijital İkiz (Digital Twin) oluşturan yapay zekâ platformudur.**

Her fotoğraf, her kontrol, her hava durumu, her tedavi, her besleme, her hasat, her analiz — Dijital İkiz'in hafızasına eklenir.

Sistem zaman içinde koloniyi öğrenir.

**Amaç veri toplamak değil, koloniyi anlamaktır.**

---

## 0.2 Misyon

BeeMaster AI'ın misyonu; arı kolonilerini insanlardan daha iyi anlamaya çalışan, öğrenen, tahmin yapan, öneriler sunan bir yapay zekâ sistemi oluşturmaktır.

---

## 0.3 Vizyon

Her kovanın yaşayan bir Dijital İkizi olacaktır. BeeMaster AI dünyanın en büyük koloni bilgi ağı olacaktır.

---

## 0.4 Temel İlkeler

Her geliştirme aşağıdaki ilkeler doğrultusunda yapılacaktır.

### İlke 1 — Dijital İkiz Her Şeyden Önce Gelir

Yeni geliştirilecek her özellik şu soruya cevap vermelidir:

> Bu özellik Dijital İkiz'i daha iyi hale getiriyor mu?

Cevap **hayır** ise özellik geliştirilmez.

### İlke 2 — Bilgi Veriden Daha Değerlidir

BeeMaster AI veri depolamaz. **Bilgi üretir.**

**Yanlış (veri):**
> Yavru Alanı: 6 Çerçeve

**Doğru (bilgi):**
> Son üç kontrolde yavru alanı %18 arttı. Bu gelişim devam ederse 12 gün içinde koloni maksimum nüfusa ulaşacaktır.
>
> ⬡ Güven Skoru: %91

### İlke 3 — Tahmin Raporlardan Daha Önemlidir

BeeMaster AI geçmişi göstermek yerine **geleceği tahmin etmelidir.**

Her ekran şu soruyu cevaplamalıdır:

> Bundan sonra ne olacak?

### İlke 4 — Her Veri Birbirine Bağlıdır

```
Ana Arı → Yavru → Nüfus → Bal → Hasat → Gelir
```

Hiçbir bilgi tek başına değerlendirilmez.

### İlke 5 — Zaman Sistemin Bir Parçasıdır

Koloni sürekli değişir. Bu nedenle; **her bilgi zaman damgası ile saklanmalıdır.**

---

## 0.5 BeeMaster AI'ın Beş Temel Direği

Sistemde bulunan her özellik bu beş başlıktan birine ait olmak zorundadır.

| # | Direk | Soru | Açıklama |
|---|-------|------|----------|
| 1 | **Gözlem** | Ne oldu? | Veri toplama: muayene, fotoğraf, hava durumu |
| 2 | **Analiz** | Neden oldu? | Veriyi anlamlandırma: trend, pattern, anomali |
| 3 | **Tahmin** | Bundan sonra ne olacak? | Gelecek kestirimi: hasat, hastalık, nüfus |
| 4 | **Öneri** | Arıcı ne yapmalı? | Aksiyon önerisi: tedavi, besleme, bölme |
| 5 | **Öğrenme** | AI doğru tahmin yaptı mı? | Geri bildirim döngüsü, model güncelleme |

**Bir özellik bu beş başlıktan hiçbirine girmiyorsa projeye eklenmez.**

---

## 0.6 Değiştirilemez Kurallar

### KURAL-0001 — Hiçbir veri silinmez.

Veri asla `DELETE` edilmez. Soft-delete veya arşiv kullanılır. Her kayıt kalıcıdır.

### KURAL-0002 — Hiçbir gözlem üzerine yazılmaz. Yeni sürüm oluşturulur.

Aynı güne ait ikinci bir muayene girildiğinde, ilk kayıt güncellenmez. Yeni bir sürüm (version) oluşturulur. Tüm geçmiş korunur.

### KURAL-0003 — Her AI çıktısı kayıt altına alınır.

AI tarafından üretilen her öneri, tahmin ve analiz `ai_logs` tablosuna yazılır. Geriye dönük denetlenebilirlik şarttır.

### KURAL-0004 — Kullanıcının yaptığı her düzeltme AI'ın öğrenmesine katkı sağlar.

Kullanıcı bir AI önerisini reddeder veya düzeltirse, bu geri bildirim sisteme işlenir. `feedback` alanı ile model güncellenir.

### KURAL-0005 — Her koloni yalnızca bir Dijital İkiz'e sahiptir.

Bir kovan (hive) için yalnızca bir Digital Twin instance'ı oluşturulur. Aynı kovan için mükerrer ikiz OLUŞTURULAMAZ.

### KURAL-0006 — Verinin sahibi modüller değildir. Verinin sahibi Dijital İkiz'dir.

**Yanlış (module-centric):**
```
Hastalık Modülü → Hastalık Geçmişini Saklıyor
```

**Doğru (twin-centric):**
```
Dijital İkiz → Hastalık Geçmişi → Hastalık Modülü (bu bilgiyi okuyor)
```

Tüm veriler Dijital İkiz'de merkezileşir. Modüller sadece bu veriyi **okur** ve **görselleştirir.**

### KURAL-0007 — Her AI önerisi aşağıdaki bilgileri içermek zorundadır.

| Bileşen | Açıklama | Format |
|---------|----------|--------|
| **Güven Skoru** | AI'ın öneriye olan güveni | %0-99 (asla %100 değil) |
| **Dayanaklar** | Hangi verilere dayanarak | Liste: muayene ID'leri, tarihler |
| **Gerekçe** | Neden bu sonuca vardı | Doğal dil açıklama |
| **Risk Analizi** | Öneri uygulanmazsa ne olur | Senaryo: en kötü/olası/en iyi |
| **Önerilen İşlem** | Arıcının ne yapması önerilir | Aksiyon listesi |

---

## 0.7 BeeMaster AI'ın Kimliği

BeeMaster AI;
- bir internet sitesi **değildir,**
- bir mobil uygulama **değildir,**
- bir yapay zekâ sohbet ekranı **değildir,**
- bir kamera uygulaması **değildir,**
- bir raporlama sistemi **değildir.**

BeeMaster AI; **bunların tamamını yöneten tek bir yapay zekâ işletim sistemidir.**

---

## 0.8 Hermes İçin Altın Kurallar (Baş Yazılım Mimarı Protokolü)

Hermes hiçbir zaman doğrudan kod yazmaya başlamaz.

**Her geliştirme şu sırayla ilerler. Bu adımlardan herhangi biri atlanamaz:**

| Adım | Eylem | Kontrol Noktası |
|------|-------|-----------------|
| 1 | Mevcut sistemi analiz et. | Kod, veritabanı, UI mevcut durumu |
| 2 | İlgili dokümanları oku. | BDAOS ilgili bölümleri |
| 3 | Mevcut bileşenleri kontrol et. | Component Library'de var mı? |
| 4 | Yeni bileşene gerçekten ihtiyaç var mı? | DRY kontrolü |
| 5 | Geliştirme planını oluştur. | `.hermes/plans/` içine yaz |
| 6 | Riskleri belirle. | Yan etki, regresyon, veri kaybı |
| 7 | Kodu küçük ve kontrollü adımlarla yaz. | Her adım tek sorumluluk |
| 8 | Test et. | Playwright + birim testleri |
| 9 | Mobil görünümü doğrula. | 375×812 viewport |
| 10 | Performansı kontrol et. | <3sn yükleme, <60fps animasyon |
| 11 | Değişikliği özetle. | Commit mesajı + değişiklik listesi |

---

## 0.9 Uyumluluk Matrisi

| Kural | Hermes | DeepSeek | Claude | Codex | Copilot | İnsan |
|-------|--------|----------|--------|-------|---------|-------|
| KURAL-0001..0007 | ✅ Zorunlu | ✅ Zorunlu | ✅ Zorunlu | ✅ Zorunlu | ✅ Zorunlu | ✅ Zorunlu |
| Bölüm 0.4 İlkeler | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Bölüm 0.5 Beş Direk | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Bölüm 0.8 Hermes Protokolü | ✅ | ⬜ | ⬜ | ⬜ | ⬜ | ⬚ Referans |

---

> **"Bu anayasa, BeeMaster AI'ın DNA'sıdır. Her karar buraya döner."**
