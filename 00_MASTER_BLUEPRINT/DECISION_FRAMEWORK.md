# 🐝 BeeMaster AI — Karar Çerçevesi

> **Bir mimari veya tasarım kararı verirken bu çerçeveyi kullan. Her karar `03_ARCHITECTURE/DECISIONS/` altında dokümante edilir.**

---

## Karar Ağacı

```
Bir karar verilmesi gerekiyor
│
├── Bu bir KULLANICI DENEYİMİ kararı mı?
│   ├── EVET → Kullanıcı 3 tıklamada hedefe ulaşabiliyor mu?
│   │   ├── EVET → OK
│   │   └── HAYIR → Akışı basitleştir
│   └── HAYIR → Devam et
│
├── Bu bir PERFORMANS kararı mı?
│   ├── EVET → Sayfa 3 saniyede yükleniyor mu?
│   │   ├── EVET → OK
│   │   └── HAYIR → Optimize et (bundle size, lazy load, cache)
│   └── HAYIR → Devam et
│
├── Bu bir OFFLINE kararı mı?
│   ├── EVET → İnternetsiz çalışıyor mu?
│   │   ├── EVET → OK
│   │   └── HAYIR → localStorage fallback ekle
│   └── HAYIR → Devam et
│
├── Bu bir GÜVENLİK kararı mı?
│   ├── EVET → Kullanıcı verisi korunuyor mu?
│   │   ├── EVET → OK
│   │   └── HAYIR → RLS, encryption, input validation ekle
│   └── HAYIR → Devam et
│
├── Bu bir MİMARİ karar mı?
│   ├── EVET → "Vanilla JS ile yapılabilir mi?"
│   │   ├── EVET → Framework ekleme, vanilla ile yap
│   │   ├── HAYIR, KÜTÜPHANE GEREKLİ → "500 byte için 50KB kütüphane mi?"
│   │   │   ├── EVET → Kütüphaneyi inline et veya kendi implementasyonunu yaz
│   │   │   └── HAYIR → Kütüphane kullan, ama tek dosyada kal
│   │   └── HAYIR, FRAMEWORK GEREKLİ → "Gerçekten mi?"
│   │       └── DECISION doc yaz, onay al
│   └── HAYIR → Devam et
│
└── Bu bir TASARIM kararı mı?
    ├── EVET → Design System'da var mı?
    │   ├── EVET → Kullan
    │   └── HAYIR → Önce Design System'a ekle, sonra kullan
    └── HAYIR → Muhtemelen bir şeyi atlıyorsun, tekrar düşün
```

---

## Yeni Teknoloji Ekleme Kriterleri

Yeni bir teknoloji (kütüphane, framework, araç) eklemeden önce:

1. **Mevcut sistemle yapılamıyor mu?** Vanilla JS ile 30 satırda yapılabilecek şey için kütüphane ekleme.
2. **Bundle boyutuna etkisi ne?** 10KB'den büyükse çok iyi düşün.
3. **Offline çalışıyor mu?** CDN bağımlılığı varsa inline et.
4. **Bakım yükü ne?** Haftalık güncelleme gerekiyorsa alternatif ara.
5. **Ekip bu teknolojiyi biliyor mu?** (AI agent'lar dahil)

## Tasarım Kararı Matrisi

| Kriter | Ağırlık | Açıklama |
|--------|---------|----------|
| Kullanıcı deneyimi | 40% | Arıcı memnuniyeti her şeyden önemli |
| Performans | 25% | 3sn yükleme, 60fps animasyon |
| Bakım kolaylığı | 15% | AI agent'ların anlayabileceği basitlikte |
| Geliştirme hızı | 10% | Hızlı iterasyon |
| Ölçeklenebilirlik | 10% | 5000 kovan, 10000 kullanıcı |

## Sık Karşılaşılan İkilemler

### "Framework kullanalım mı?"
**Cevap: HAYIR.** 15 kural:
- PWA 250KB'ın altında kalmalı
- Service Worker cache basit olmalı
- Offline-first mimari framework'lerle zor
- AI agent'lar vanilla JS'de daha az hata yapar
- Bağımlılık yok = kırılacak şey yok

### "Yeni bir sayfa/modül ekleyelim mi?"
**Cevap:**
1. Kullanıcı ihtiyacı var mı? (veri ile kanıtla)
2. Mevcut modülle yapılamaz mı?
3. Dijital İkiz'i güçlendiriyor mu?
4. 3 soruya da EVET → ekle, DEĞİLSE → bekle

### "TypeScript'e geçelim mi?"
**Cevap: ŞİMDİLİK HAYIR.**
- Build step ekler (PWA sadeliğini bozar)
- AI agent'lar vanilla JS'de daha üretken
- JSDoc ile type güvenliği sağlanabilir
- Gelecekte değerlendirilebilir (karar DEC-0005 olarak kaydedildi)

### "State management kütüphanesi kullanalım mı?"
**Cevap: HAYIR.**
- `BM.Storage.state` objesi yeterli
- Global event bus ile değişiklik bildirimi
- localStorage senkron state zaten

---

## Karar Dokümantasyon Formatı

Her önemli mimari karar `03_ARCHITECTURE/DECISIONS/DEC-NNNN.md` olarak kaydedilir:

```markdown
# DEC-0001: [Karar Başlığı]

**Tarih:** YYYY-MM-DD
**Durum:** Accepted | Proposed | Deprecated | Superseded

## Bağlam
Bu karar neden gerekli?

## Karar
Ne karar verildi?

## Alternatifler
Hangi alternatifler değerlendirildi?

## Sonuçlar
Bu kararın sonuçları neler? (pozitif ve negatif)
```

---

> **"İyi karar, veriyle desteklenen karardır. Her kararın bir DEC numarası olmalı."**
