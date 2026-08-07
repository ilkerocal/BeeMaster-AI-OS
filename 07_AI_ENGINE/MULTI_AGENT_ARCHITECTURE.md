# BÖLÜM 9 — Çoklu Yapay Zekâ Mimarisi (Multi-Agent AI Architecture)

**Sürüm:** 1.0  
**Öncelik:** Kritik  
**Durum:** Zorunlu Standart  
**Kapsam:** AI ajan sistemi mimarisi

---

## 9.0 Vizyon

BeeMaster AI tek bir yapay zekâ modeli **değildir.**

BeeMaster AI; **birbirleriyle iletişim kurabilen uzman AI ajanlarından oluşan bir ekiptir.**

Her ajan yalnızca kendi uzmanlık alanında karar üretir. Son kararı ise **Koordinatör AI (Orchestrator)** verir.

---

## 9.1 Tasarım Felsefesi

> Tek AI her şeyi bilmeye çalışmaz. Uzman AI'lar birlikte çalışır.

Her ajan:
- ✅ Tek bir sorumluluğa sahiptir
- ✅ Kendi veri kaynaklarını kullanır
- ✅ Kendi güven skorunu üretir
- ✅ Gerektiğinde diğer ajanlarla iş birliği yapar

---

## 9.2 Genel Mimari

```
                         Kullanıcı
                             │
                             ▼
                    ╔═══════════════╗
                    ║ Orchestrator  ║  ← Koordinatör
                    ╚═══════╤═══════╝
                             │
     ┌───────────────────────┼───────────────────────┐
     │                       │                       │
     ▼                       ▼                       ▼
┌─────────┐           ┌──────────┐           ┌──────────┐
│Sağlık   │           │ Görsel   │           │ Tahmin   │
│Ajanı    │           │ Analiz   │           │ Ajanı    │
└────┬────┘           └────┬─────┘           └────┬─────┘
     │                     │                      │
     ▼                     ▼                      ▼
┌─────────┐           ┌──────────┐           ┌──────────┐
│Hastalık │           │ Frame    │           │ Bal      │
│Ajanı    │           │ Scanner  │           │ Üretim   │
└────┬────┘           └────┬─────┘           └────┬─────┘
     │                     │                      │
     ▼                     ▼                      ▼
┌─────────┐           ┌──────────┐           ┌──────────┐
│Ana Arı  │           │ Hava     │           │ Öğrenme  │
│Ajanı    │           │ Ajanı    │           │ Ajanı    │
└────┬────┘           └────┬─────┘           └────┬─────┘
     │                     │                      │
     └─────────┬───────────┴──────────┬───────────┘
               │                      │
               ▼                      ▼
        ╔══════════════╗    ╔═══════════════╗
        ║ Karar Motoru ║    ║ Rapor Ajanı   ║
        ╚══════╤═══════╝    ╚═══════╤═══════╝
               │                      │
               └──────────┬───────────┘
                          ▼
                    AI Önerileri
```

**Hiçbir ajan tek başına tüm sistemi yönetmez.**

---

## 9.3 Orchestrator AI (Koordinatör) — `AGENT-000`

| Özellik | Değer |
|---------|-------|
| **Görevi** | Sistemin yöneticisi (beyni değil) |
| **Kod** | `AGENT-000` |

**Yapacağı işler:**
1. Kullanıcı isteğini anlamak
2. Hangi ajanların çalışacağını belirlemek
3. Görevleri dağıtmak
4. Sonuçları toplamak
5. Çelişkileri çözmek
6. Nihai raporu oluşturmak

**Orchestrator teknik analiz yapmaz.** Uzmanlardan gelen sonuçları yönetir.

---

## 9.4 Colony Health Agent (Sağlık) — `AGENT-001`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Koloninin genel sağlık durumunu değerlendirmek |
| **Kod** | `AGENT-001` |

**İncelediği veriler:**
- Çerçeve analizleri
- Hastalık geçmişi
- Tedaviler
- Koloni gücü
- Aktivite
- Dijital İkiz geçmişi

**Çıktıları:** Sağlık puanı, Risk seviyesi, Öncelikli sorunlar

---

## 9.5 Queen Agent (Ana Arı) — `AGENT-002`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Ana arıyı analiz etmek |
| **Kod** | `AGENT-002` |

**Kontrol ettiği bilgiler:** Yaş, Irk, Performans, Yumurtlama düzeni, Görülme geçmişi, Değişim ihtimali

**Örnek çıktı:**
```
Ana Arı Durumu: İyi
Güven: %93
Öneri: Değişim gerekmiyor.
```

---

## 9.6 Brood Agent (Yavru) — `AGENT-003`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Yavru alanını değerlendirmek |
| **Kod** | `AGENT-003` |

**İncelediği alanlar:** Açık yavru, Kapalı yavru, Yumurta, Dağılım, Düzen, Gelişim hızı

**Tahminler:** Koloni büyümesi, Ana arı performansı, Gelişim eğilimi

---

## 9.7 Honey Production Agent (Bal Üretim) — `AGENT-004`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Bal üretimini analiz etmek |
| **Kod** | `AGENT-004` |

**Veriler:** Bal alanı, Nektar akımı, Hava, Geçmiş hasatlar, Koloni gücü

**Çıktılar:** Tahmini hasat tarihi, Beklenen verim, Riskler

---

## 9.8 Weather & Nectar Agent (Hava) — `AGENT-005`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Çevresel koşulları değerlendirmek |
| **Kod** | `AGENT-005` |

**Analiz:** Sıcaklık, Nem, Yağış, Rüzgâr, Çiçeklenme, Nektar akımı

**Çıktılar:** Uçuş uygunluğu, Besleme ihtiyacı, Bal akımı tahmini

---

## 9.9 Disease Agent (Hastalık) — `AGENT-006`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Hastalık belirtilerini değerlendirmek |
| **Kod** | `AGENT-006` |

**Kaynaklar:** Görsel analiz, Tedavi geçmişi, Lab sonuçları, Kullanıcı notları, Çevresel riskler

> ⚠️ **Bu ajan kesin teşhis koymaz.** Risk ve olası senaryolar üretir.

---

## 9.10 Vision Agent (Görsel) — `AGENT-007`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Tüm görsel verileri analiz etmek |
| **Kod** | `AGENT-007` |

**Kaynaklar:** Fotoğraf, Video, Termal görüntü, Yakın plan çekimler

**Görevleri:** Nesne tanıma, Hücre sınıflandırma, Anomali tespiti, Görüntü kalite analizi

---

## 9.11 Prediction Agent (Tahmin) — `AGENT-008`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Yalnızca geleceği tahmin etmek |
| **Kod** | `AGENT-008` |

**Örnek tahminler:** Oğul riski, Ana arı değişimi, Bal üretimi, Koloni büyümesi, Hastalık olasılığı

**Her tahmin:** Olasılık + Güven + Beklenen tarih ile sunulur.

---

## 9.12 Report Agent (Rapor) — `AGENT-009`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Bütün analizleri kullanıcıya anlaşılır şekilde sunmak |
| **Kod** | `AGENT-009` |

**Rapor içeriği:** Kısa özet, Detaylı analiz, Grafikler, Zaman çizelgesi, Öneriler

> Teknik veriler kullanıcıya olduğu gibi aktarılmaz.

---

## 9.13 Learning Agent (Öğrenme) — `AGENT-010`

| Özellik | Değer |
|---------|-------|
| **Sorumluluk** | Sistemin gelişmesini sağlamak |
| **Kod** | `AGENT-010` |

**Öğrendiği kaynaklar:**
- Kullanıcı düzeltmeleri (KURAL-0004)
- Sonuçlanan öneriler
- Gerçekleşen olaylar
- Yeni bilimsel bilgiler
- Model performansı

> ⚠️ Yeni bilgi otomatik olarak üretim sistemine eklenmez. Doğrulama sürecinden geçer.

---

## 9.14 Agent İletişim Kuralları

Ajanlar birbirlerine **doğrudan müdahale etmez.** İletişim standart mesajlarla yapılır.

```
Disease Agent → "Risk Güncellendi"
    ↓
Prediction Agent → "Yeni Tahmin"
    ↓
Decision Engine → "Öneri Güncellendi"
```

Bu yapı bağımlılığı azaltır. Her ajan sadece kendi çıktısını üretir, Orchestrator birleştirir.

---

## 9.15 Güven Birleştirme

Farklı ajanlar farklı güven puanları üretebilir:

| Ajan | Güven |
|------|-------|
| Vision | %94 |
| Disease | %76 |
| Weather | %98 |
| Prediction | %81 |

Orchestrator bu puanları değerlendirir. **En düşük güven puanı otomatik olarak en doğru sonucu temsil etmez.** Karar, bağlama göre verilir.

---

## 9.16 Çelişki Yönetimi

**Örnek çelişki:**

| Ajan | Sonuç |
|------|-------|
| Vision Agent | "Ana arı görüldü." |
| Queen Agent | "Son üç kontrolde görülmedi." |

Bu durumda sistem:
1. Çelişkiyi işaretler
2. Nedenlerini açıklar
3. Ek gözlem önerir

**Belirsizlik gizlenmez.** (Bölüm 6.11)

---

## 9.17 Ajan Yaşam Döngüsü

Her ajan şu süreçten geçer. **Tüm ajanlar için aynıdır.**

```
① Veri Al → ② Doğrula → ③ Analiz Et → ④ Güven Hesapla → ⑤ Sonuç Üret → ⑥ Raporla → ⑦ Öğren
```

---

## 9.18 Performans ve Ölçeklenebilirlik

Sistem yalnızca **gerekli ajanları** çalıştırır.

| Kullanıcı Aksiyonu | Çalışan Ajanlar |
|-------------------|-----------------|
| Hava durumu ekranı | Weather Agent (+ Prediction gerekirse) |
| Frame Scanner | Vision Agent + Health Agent |
| Dashboard | Orchestrator → tümü (hafif) |
| Hastalık sayfası | Disease Agent + Vision Agent |

**Çalışmayan ajanlar:** Vision, Disease (hava ekranında) — boş yere kaynak tüketmez.

Bu yaklaşım: maliyeti düşürür, yanıt süresini hızlandırır, kaynak kullanımını optimize eder.

---

## 9.19 Ajan Kayıt Tablosu

| Kod | Ajan | Sorumluluk | Durum |
|-----|------|-----------|-------|
| AGENT-000 | Orchestrator | Koordinasyon | ✅ |
| AGENT-001 | Colony Health | Sağlık değerlendirme | 📋 |
| AGENT-002 | Queen | Ana arı analizi | 📋 |
| AGENT-003 | Brood | Yavru değerlendirme | 📋 |
| AGENT-004 | Honey Production | Bal üretim analizi | 📋 |
| AGENT-005 | Weather & Nectar | Çevresel koşullar | 📋 |
| AGENT-006 | Disease | Hastalık risk analizi | 📋 |
| AGENT-007 | Vision | Görsel analiz | 📋 |
| AGENT-008 | Prediction | Gelecek tahmini | 📋 |
| AGENT-009 | Report | Rapor oluşturma | 📋 |
| AGENT-010 | Learning | Sistem öğrenmesi | 📋 |

---

## 9.20 Sonuç

BeeMaster AI'ın yapay zekâ mimarisi;
- ❌ tek modelden cevap üreten bir sistem değil,
- ✅ **uzmanlaşmış AI ajanlarının koordineli çalıştığı bir platformdur.**

Bu yapı sayesinde:
- Modüller bağımsız gelişebilir
- Yeni ajanlar kolayca eklenebilir
- Açıklanabilir kararlar üretilebilir
- Sistem zaman içinde büyürken mimari bütünlüğünü korur

---

> **"Tek bir AI her şeyi bilemez. Ama 10 uzman AI birlikte her şeyi anlayabilir."**
