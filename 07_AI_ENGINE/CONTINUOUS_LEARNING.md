# BÖLÜM 10 — Sürekli Öğrenme ve Bilgi Evrimi (Continuous Learning & Knowledge Evolution)

**Sürüm:** 1.0  
**Öncelik:** Kritik  
**Durum:** Zorunlu Standart  
**Kapsam:** Sistem öğrenmesi ve bilgi yönetimi

---

## 10.0 Vizyon

BeeMaster AI yalnızca bugünkü bilgiyi kullanan bir sistem **değildir.**

Amaç; her gün, her kontrol, her tarama, her kullanıcı geri bildirimi ve yeni bilimsel bilgiler sayesinde **daha doğru karar verebilen bir platform** oluşturmaktır.

**Ancak hiçbir öğrenme doğrulanmadan sistemin temel bilgi tabanına eklenmez.**

---

## 10.1 Öğrenme Felsefesi

BeeMaster AI için "öğrenmek" şu anlama gelir:

1. Yeni bir gözlem kazanmak
2. Bu gözlemi mevcut bilgilerle karşılaştırmak
3. Çelişkileri belirlemek
4. Yeterli kanıt oluştuğunda bilgi tabanını güncellemek

> **Tek bir örnek hiçbir zaman genel kural oluşturmaz.**

---

## 10.2 Bilgi Kaynakları

Sistem aşağıdaki kaynaklardan öğrenebilir. **Her kaynağın güven seviyesi farklıdır.**

| Kaynak | Güven Seviyesi | Örnek |
|--------|---------------|-------|
| Bilimsel yayınlar | ⭐⭐⭐⭐⭐ | Hakemli dergi makalesi |
| Uzman doğrulamaları | ⭐⭐⭐⭐ | Veteriner/entomolog onayı |
| Tekrarlanan saha sonuçları | ⭐⭐⭐ | 100+ benzer vaka |
| Kullanıcı gözlemleri | ⭐⭐ | Arıcı notu |
| Sensör verileri | ⭐⭐ | Sıcaklık, nem, ağırlık |
| Ham veri | ⭐ | İşlenmemiş kayıt |

---

## 10.3 Bilgi Güven Piramidi

```
        ╔═══════════════════╗
        ║ Bilimsel Yayınlar ║  ← En yüksek güven
        ╠═══════════════════╣
        ║ Uzman Doğrulamaları║
        ╠═══════════════════╣
        ║ Tekrarlanan Saha   ║
        ║ Sonuçları          ║
        ╠═══════════════════╣
        ║ Kullanıcı          ║
        ║ Gözlemleri         ║
        ╠═══════════════════╣
        ║ Ham Veri           ║  ← En düşük güven
        ╚═══════════════════╝
```

Üst seviyedeki bilgiler daha yüksek önceliğe sahiptir. Karar Motoru bu hiyerarşiyi dikkate alır.

---

## 10.4 Bilgi Türleri

Her bilgi sınıflandırılır:

| Tür | Açıklama | Karar Motoru Kullanımı |
|-----|----------|----------------------|
| **Doğrulanmış** | Güçlü kanıtlarla desteklenmiş | Tam güvenle kullanılır |
| **Güçlü Kanıt** | Birden fazla bağımsız kaynaktan | Yüksek güvenle kullanılır |
| **Gözlemsel** | Tekrar eden saha gözlemleri | Orta güvenle kullanılır |
| **Deneysel** | Test aşamasında | Düşük güvenle, uyarı ile |
| **Belirsiz** | Yetersiz veri bulunan | Kullanılmaz, araştırma önerilir |

---

## 10.5 Öğrenme Döngüsü (Zorunlu Akış)

Yeni bilgi şu süreçten geçer. **Hiçbir adım atlanmaz.**

```
① Yeni Veri
    │
    ▼
② Kalite Kontrolü        ← Kaynak güvenilir mi? Veri eksik mi?
    │
    ▼
③ Mevcut Bilgi ile       ← Çakışma var mı?
   Karşılaştırma
    │
    ▼
④ Çelişki Analizi        ← Varsa: neden? hangisi daha güçlü?
    │
    ▼
⑤ Uzman Kuralları ile    ← Bilimsel literatüre uygun mu?
   Doğrulama
    │
    ▼
⑥ Bilgi Tabanına Aday    ← "İnceleme Bekliyor" statüsü
    │
    ▼
⑦ Onay                   ← Yeterli kanıt → Onaylandı
    │
    ▼
⑧ Yeni Sürüm             ← Knowledge Base güncellenir
```

---

## 10.6 Kullanıcı Geri Bildirimi (KURAL-0004)

Kullanıcı, AI önerilerini değerlendirebilir:

| Geri Bildirim | Anlamı |
|---------------|--------|
| Faydalı | Öneri doğru ve işe yaradı |
| Faydasız | Öneri gereksizdi |
| Eksik | Doğru ama yetersiz |
| Yanlış | Öneri hatalıydı |
| Kararsızım | Değerlendirilemedi |

Bu geri bildirimler tek başına modeli değiştirmez. Ancak sistem performansını ölçmek için kaydedilir.

---

## 10.7 Sonuçların Takibi

Her öneri izlenir:

```
Öneri: "Besleme yap."
    │
    ├── Senaryo A: Besleme yapıldı → Koloni güçlendi ✅
    │   └── Kayıt: olumlu sonuç, güven artar
    │
    └── Senaryo B: Besleme yapılmadı → Koloni yine güçlendi ⚠️
        └── Kayıt: öneri gereksiz olabilir, incelenir
```

Bu sonuçlar gelecekte benzer durumların değerlendirilmesinde kullanılır.

---

## 10.8 Bilimsel Bilgi Entegrasyonu

Yeni bilimsel çalışmalar değerlendirilebilir. Ancak **her yayın otomatik olarak sisteme eklenmez.**

| Değerlendirme Ölçütü | Kontrol |
|---------------------|---------|
| Hakemli yayın mı? | ✅ Zorunlu |
| Tekrar edilebilir mi? | ✅ Zorunlu |
| Mevcut bilgiyle çelişiyor mu? | Çelişki analizi |
| Arıcılık uygulamalarıyla uyumlu mu? | Saha kontrolü |

Bu süreç tamamlanmadan bilgi **"doğrulanmış" kabul edilmez.**

---

## 10.9 Model Sürümleme

Her AI modeli sürümlenir:

```
Vision Engine v2.1
Decision Engine v1.8
Disease Agent v3.0
```

Üretilen öneriler hangi model sürümüyle oluşturulduğunu kaydeder. Bu, geçmiş kararların yeniden incelenmesini kolaylaştırır. (KURAL-0003)

---

## 10.10 Bilgi Tabanı Sürümleme

Bilgi tabanı da sürümlenir:

```
Knowledge Base 2026.08
Knowledge Base 2027.01
```

Böylece hangi önerinin hangi bilgi setine dayandığı izlenebilir. Eski sürümler silinmez, arşivlenir.

---

## 10.11 Çelişki Yönetimi

Yeni bilgi mevcut kurallarla çelişiyorsa:

1. ✅ Çelişki kaydedilir
2. ✅ Eski bilgi **silinmez** (KURAL-0001)
3. ✅ Yeni bilgi "inceleme bekliyor" durumuna alınır
4. ✅ Yeterli kanıt oluşursa yeni sürüm yayımlanır

**Sistem geçmiş bilgisini kaybetmez.**

---

## 10.12 Öğrenme Günlüğü (Audit Log)

Her değişiklik kayıt altına alınır:

| Alan | İçerik |
|------|--------|
| Tarih | Değişiklik zamanı |
| Kaynak | Hangi kaynaktan geldi |
| Değişiklik Nedeni | Neden güncellendi |
| Etkilenen Modüller | Hangi ajan/modül etkilendi |
| Sürüm Numarası | Yeni KB sürümü |
| Onay Durumu | Kim tarafından onaylandı |

Bu günlük **denetlenebilir** olmalıdır.

---

## 10.13 Gizlilik ve Etik

Öğrenme süreçleri kullanıcı gizliliğini korumalıdır:

| İlke | Uygulama |
|------|----------|
| Kullanıcı onayı olmadan kişisel veri paylaşılmaz | Opt-in zorunlu |
| Kimlik bilgileri anonimleştirilir | UUID, isim yok |
| Toplulaştırılmış analizler bireyi tanımlayamaz | Minimum 50 kullanıcı |
| Öğrenme verileri güvenli saklanır | Şifreleme + RLS |

---

## 10.14 Performans Ölçümü

Sistemin gelişimi düzenli olarak ölçülür:

| Metrik | Hedef | Ölçüm Sıklığı |
|--------|-------|---------------|
| AI öneri doğruluk oranı | >%80 | Aylık |
| Kullanıcı memnuniyeti | >4.0/5 | Sürekli |
| Yanlış pozitif oranı | <%10 | Aylık |
| Yanlış negatif oranı | <%5 | Aylık |
| Tahmin doğruluğu | >%75 | Aylık |
| Görsel analiz başarısı | >%85 | Aylık |

Bu metrikler sürümler arasında karşılaştırılır.

---

## 10.15 İnsan Denetimi

BeeMaster AI sürekli öğrenebilir. Ancak kritik bilgi değişiklikleri;

- ✅ Uzman incelemesi
- ✅ Kalite kontrolü
- ✅ Sürüm onayı

gerektirebilir. Bu yaklaşım bilgi kalitesini korur.

---

## 10.16 Bilginin Evrimi

BeeMaster AI'ın bilgi tabanı **yaşayan bir sistemdir.** Ancak değişim;

- ✅ İzlenebilir
- ✅ Geri alınabilir
- ✅ Gerekçelendirilebilir

olmalıdır. Her yeni sürüm önceki sürümlerle karşılaştırılabilir.

---

## 10.17 Sonuç

BeeMaster AI'ın en büyük gücü yalnızca öğrenmesi değil, **nasıl öğrendiğini açıklayabilmesi** olacaktır.

Sistem:
- ❌ Rastgele öğrenmez
- ❌ Doğrulanmamış bilgiyi temel kural yapmaz
- ✅ Geçmişini unutmaz
- ✅ Her değişikliği kayıt altına alır
- ✅ Bilimsel ve saha verilerini birlikte değerlendirir

Bu yaklaşım, platformun yıllar içinde daha güvenilir ve sürdürülebilir hale gelmesini sağlar.

---

> **"Öğrenmek yetmez. Ne öğrendiğini kanıtlayabilmelisin."**
