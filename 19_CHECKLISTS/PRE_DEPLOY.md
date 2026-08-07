# ✅ Deploy Öncesi Kontrol Listesi

> **RULE-0015: Bu liste eksiksiz uygulanmadan deploy YAPILMAZ.**

---

## 1. Kod Kontrolü

- [ ] Tüm metinler Türkçe (`grep -c "Good Morning\|Search disease\|Open →"` = 0)
- [ ] Cache-bust `?v=N` artırıldı
- [ ] Console.log kalmadı (sadece debug/error)
- [ ] Hardcode renk/token yok (CSS değişkenleri kullanılıyor)
- [ ] EscapeHtml() XSS koruması var
- [ ] `node --check` syntax hatası yok

## 2. Tasarım Kontrolü

- [ ] Renkler design system'a uygun (amber accent, dark theme)
- [ ] Kart border-radius 12px
- [ ] Buton radius 8px
- [ ] Gölgeler `var(--shadow-*)` ile
- [ ] Mobil görünüm (375×812) test edildi
- [ ] Sidebar mobilde hamburger ile çalışıyor

## 3. Fonksiyonel Kontrol (Playwright)

- [ ] Sayfa yükleniyor (networkidle, <3sn)
- [ ] Login çalışıyor
- [ ] Dashboard render ediliyor
- [ ] Tüm modüller açılıyor:
  - [ ] Dashboard
  - [ ] Kovanlar (Hives)
  - [ ] Arılıklar (Apiaries)
  - [ ] Kraliçeler (Queens)
  - [ ] Muayeneler (Inspections)
  - [ ] Hastalık AI (Diseases)
  - [ ] Hasat (Harvest)
  - [ ] Besleme (Feeding)
  - [ ] Tedaviler (Treatments)
  - [ ] Envanter (Inventory)
- [ ] Form submit çalışıyor (en az 1 kayıt)
- [ ] Modal açılıp kapanıyor
- [ ] AI öneri kartı görünüyor
- [ ] Console'da 0 hata

## 4. Offline Kontrolü

- [ ] İnternet kapalıyken sayfa açılıyor
- [ ] localStorage'a veri kaydediliyor
- [ ] İnternet gelince sync çalışıyor

## 5. Deploy

- [ ] `git push origin main` yapıldı
- [ ] Vercel deploy tamamlandı (90sn bekle)
- [ ] Cache-bust yeni versiyonu gösteriyor
- [ ] Canlıda login + dashboard testi yapıldı

## 6. Son Kontrol

- [ ] Screenshot alındı ve görsel olarak doğrulandı
- [ ] Mobil + Desktop her ikisi test edildi
- [ ] Kullanıcıya bildirildi
