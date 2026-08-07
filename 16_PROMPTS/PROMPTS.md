# 📝 Prompt Kütüphanesi

> **BeeMaster AI geliştirmesi için standart prompt'lar. Hermes'e her görevde bu prompt'lar kullanılır.**

---

## Yeni Özellik Geliştirme

```
BeeMaster AI'da yeni bir özellik geliştir.

KURALLAR:
- BDAOS .hermesrules dosyasındaki tüm kurallara uy
- Önce 01_DESIGN_SYSTEM/ ve 02_COMPONENT_LIBRARY/ kontrol et
- Tasarım token'larını kullan (var(--color-*))
- Bileşen kütüphanesinden hazır bileşen kullan
- Yeni bir şey icat etme

SÜREÇ:
1. Mevcut kodu analiz et
2. Plan oluştur (.hermes/plans/)
3. Onayımı al
4. TDD ile uygula
5. Playwright ile test et
6. Deploy (cache-bust artır)

ÖZELLİK:
[Özellik detayları buraya]
```

## Hata Düzeltme

```
BeeMaster AI'da şu hata var: [HATA AÇIKLAMASI]

KURALLAR:
- RULE-0001: Önce analiz et, sonra düzelt
- RULE-0003: Tek commit
- RULE-0008: Playwright testi şart

SÜREÇ:
1. Hatayı yeniden üret (Chrome DevTools)
2. Root cause bul
3. Test yaz (önce kırık)
4. Düzelt (minimum değişiklik)
5. Testi yeşil yap
6. Deploy et
```

## Deploy

```
BeeMaster AI'ı deploy et.

ADIMLAR:
1. Cache-bust ?v=N artır
2. 19_CHECKLISTS/PRE_DEPLOY.md kontrol listesini uygula
3. Playwright smoke test
4. git commit + push
5. 90 saniye bekle
6. Canlıda test et
7. Sonucu bildir
```

## Kod İnceleme

```
Şu değişiklikleri incele:

KONTROLLER:
- BDAOS kurallarına uygun mu?
- Tasarım sistemi kullanılmış mı?
- Gereksiz kod var mı? (DRY, YAGNI)
- Türkçe metinler doğru mu?
- XSS/performans/güvenlik sorunu var mı?
- Tek bir özellik mi? (RULE-0003)
```

## Günlük Durum

```
BeeMaster AI durum raporu:

- Son deploy: [TARİH]
- Aktif branch: [BRANCH]
- Son değişiklikler: [ÖZET]
- Açık sorunlar: [LISTE]
- Sonraki adım: [PLAN]
```
