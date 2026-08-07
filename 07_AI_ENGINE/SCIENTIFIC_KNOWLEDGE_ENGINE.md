# BÖLÜM 13 — Bilimsel Bilgi Motoru ve Küresel Arıcılık Bilgi Ağı (Scientific Knowledge Engine & Global Beekeeping Knowledge Network)

**Sürüm:** 1.0  
**Öncelik:** Stratejik  
**Durum:** Zorunlu Standart  
**Kapsam:** Bilimsel bilgi yönetimi ve entegrasyonu

---

## 13.0 Vizyon

BeeMaster AI yalnızca bir yapay zekâ değildir. Aynı zamanda **yaşayan bir bilimsel bilgi platformudur.**

Sistem; bilimsel araştırmaları, saha deneyimlerini, kullanıcı gözlemlerini ve Dijital İkiz verilerini aynı bilgi ekosisteminde bir araya getirir.

**Ancak her bilgi aynı ağırlığa sahip değildir.** Bilgi, kaynağına ve doğrulama düzeyine göre değerlendirilir.

---

## 13.1 Temel Felsefe

Bilgi üretmek ile bilgi doğrulamak farklı süreçlerdir. BeeMaster AI; yeni hipotezler oluşturabilir, gözlemsel ilişkiler tespit edebilir, ancak bunları doğrulanmış bilimsel gerçekler olarak sunmaz. **Her önerinin bilgi türü açıkça belirtilir.**

---

## 13.2 Bilgi Kaynakları

| Kaynak | Güven | Örnek |
|--------|-------|-------|
| Hakemli bilimsel makaleler | ⭐⭐⭐⭐⭐ | Journal of Apicultural Research |
| Üniversite araştırmaları | ⭐⭐⭐⭐ | Tarım fakültesi raporu |
| Resmî teknik rehberler | ⭐⭐⭐⭐ | Bakanlık yayını |
| Bölgesel arıcılık uygulamaları | ⭐⭐⭐ | Yerel birlik raporu |
| Uzman doğrulamalı saha raporları | ⭐⭐⭐ | Veteriner onaylı |
| Kullanıcı geri bildirimleri | ⭐⭐ | Arıcı değerlendirmesi |
| Dijital İkiz verileri | ⭐⭐ | Otomatik kayıt |

Her kaynak için; yayın tarihi, sürüm, güven düzeyi, kapsam kaydedilir.

---

## 13.3 Bilgi Sınıflandırması

| Seviye | Açıklama | Karar Motoru Kullanımı |
|--------|----------|----------------------|
| **A** | Güçlü bilimsel kanıt | Tam güven |
| **B** | Birden fazla bağımsız saha doğrulaması | Yüksek güven |
| **C** | Uzman görüşü | Orta güven |
| **D** | Gözlemsel kullanıcı verisi | Düşük güven |
| **E** | Deneysel / doğrulanmamış | Araştırma amaçlı |

Karar Motoru önerilerini oluştururken bu seviyeleri dikkate alır (Bölüm 10.3-10.4).

---

## 13.4 Bilgi Nesnesi

Her bilgi standart bir yapıda saklanır:

| Alan | Tip |
|------|-----|
| Bilgi Kimliği | UUID |
| Başlık | String |
| Özet | Text |
| Kaynak Türü | Enum |
| Yayın Tarihi | Date |
| Geçerlilik Durumu | Enum |
| Kanıt Seviyesi | A/B/C/D/E |
| İlgili Konular | Tag[] |
| Anahtar Kavramlar | Tag[] |
| Sürüm | SemVer |

Bu yapı bilgi tabanının tutarlı olmasını sağlar.

---

## 13.5 Kavramlar Arası İlişkiler

Bilgiler birbirinden bağımsız değildir. Bilgi Motoru bu ilişkileri Bilgi Grafiği ile birleştirir (Bölüm 8).

```
Varroa ──ETKİLER──→ Yavru Gelişimi ──ETKİLER──→ Koloni Gücü ──ETKİLER──→ Bal Verimi
```

---

## 13.6 Kanıt Zinciri

Her AI önerisi mümkün olduğunca bir kanıt zinciri oluşturur:

```
Gözlem → Bilimsel Bilgi → Dijital İkiz → Risk Analizi → AI Önerisi
```

Kullanıcı önerinin hangi verilere dayandığını görebilir (KURAL-0007, Bölüm 6.14).

---

## 13.7 Çelişkili Bilgiler

Bilimsel kaynaklar arasında görüş ayrılığı olabilir. Bu durumda sistem: çelişkiyi saklar, hangi kaynakların farklı düşündüğünü gösterir, tek bir görüşü mutlak doğru olarak sunmaz. **Belirsizlik kullanıcıdan gizlenmez.**

---

## 13.8 Bilgi Güncelleme Süreci

```
Yeni Bilgi → Kalite Kontrolü → Kaynak Değerlendirmesi → Çelişki Analizi → Uzman İncelemesi → Yeni Bilgi Sürümü
```

Yeni bilgi doğrudan üretim sistemine eklenmez. (Bölüm 10.5)

---

## 13.9 Bölgesel Bilgi

Arıcılık uygulamaları bölgelere göre değişebilir: İklim, Rakım, Bitki örtüsü, Arı ırkı, Üretim hedefi. Bilgi Motoru önerilerini mümkün olduğunca bölgesel bağlama göre uyarlamaya çalışır.

---

## 13.10 Bilimsel ve Gözlemsel Bilginin Ayrımı

| Bilimsel Bilgi | Gözlemsel Bilgi |
|---------------|-----------------|
| Literatür tarafından desteklenir | Dijital İkiz ve saha kayıtlarından |
| Hakemli, tekrar edilebilir | Kullanıcı deneyimi |

Her ikisi birlikte değerlendirilebilir; ancak **aynı şey değildir.**

---

## 13.11 Bilgi Arama Motoru

AI ajanları bilgi tabanını sorgulayabilir:

- "Benzer kolonilerde hangi uygulamalar başarılı oldu?"
- "Bu hastalık için hangi doğrulanmış yaklaşımlar bulunuyor?"
- "Benzer iklim koşullarında öneriler nasıl değişiyor?"

Bu sorgular yapılandırılmış bilgi üzerinde çalışır.

---

## 13.12 Kaynak Gösterimi

Kullanıcı isterse önerinin dayandığı bilgi özeti gösterilebilir: Kanıt seviyesi, Yayın yılı, Bilgi sürümü, İlgili konu başlıkları. Uzun akademik metinler yerine anlaşılır özetler sunulur.

---

## 13.13 Bilgi Sürümleme

```
Disease Knowledge v1.0 → v2.4
Queen Management v2.4 → v3.1
Nutrition Rules v3.1
```

Geçmiş sürümler saklanır. Hangi öneri hangi sürümle üretildi izlenir (Bölüm 10.10).

---

## 13.14 Bilgi Kalite Göstergeleri

| Metrik | Hedef |
|--------|-------|
| Güncellik (son 12 ay) | >%80 |
| Kaynak çeşitliliği | En az 3 farklı tip |
| Kanıt seviyesi dağılımı | A+B >%50 |
| Çelişki oranı | <%10 |
| Doğrulanmış bilgi oranı | >%70 |

---

## 13.15 Açıklanabilirlik

Her öneri şu soruları cevaplayabilmelidir: Bu öneri hangi verilere dayanıyor? Hangi bilgi sınıfı kullanıldı? Belirsizlik var mı? Alternatif görüşler mevcut mu? **Kullanıcı "neden?" sorusunun cevabını görebilmelidir.**

---

## 13.16 Sonuç

Bilimsel Bilgi Motoru sayesinde BeeMaster AI; yalnızca kullanıcı kayıtlarından öğrenen, yalnızca yapay zekâ tahminleri üreten bir sistem olmaktan çıkar. Bilimsel kanıtlar, saha gözlemleri ve Dijital İkiz verilerini birlikte değerlendiren, açıklanabilir ve izlenebilir bir **karar destek platformuna** dönüşür.

---

> **"Bilgi güçtür. Doğrulanmış bilgi ise güvenilir güçtür."**
