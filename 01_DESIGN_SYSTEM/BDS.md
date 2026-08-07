# BÖLÜM 2 — BeeMaster AI Tasarım Sistemi (BDS)

**Sürüm:** 1.0  
**Durum:** Zorunlu Standart  
**Kapsam:** Tüm UI geliştirmeleri

---

## 2.0 Amaç

BeeMaster AI'ın amacı güzel görünmek **değildir.**

Amaç; **en az dikkat dağıtan, en güven veren, en hızlı anlaşılabilen profesyonel arayüzü** oluşturmaktır.

Kullanıcı; uygulamaya değil, **koloniye odaklanmalıdır.**

---

## 2.1 Tasarım Felsefesi

BeeMaster AI'ın tasarım dili şu **beş kelimeyle** açıklanmalıdır:

| # | Değer | Anlamı |
|---|-------|--------|
| 1 | **Sade** | Gereksiz eleman yok. Her şey bir amaca hizmet eder. |
| 2 | **Bilimsel** | Veri odaklı, ölçülebilir, kanıta dayalı görünüm. |
| 3 | **Profesyonel** | Apple/Stripe/Linear kalitesinde. Oyuncak değil. |
| 4 | **Canlı** | Statik değil. Koloni yaşıyor, arayüz de yaşamalı. |
| 5 | **Güven Veren** | AI önerileri şeffaf. Kullanıcı sisteme güvenmeli. |

**Eğer yeni eklenen bir bileşen bu beş özelliği taşımıyorsa, tasarım reddedilir.**

---

## 2.2 Görsel Kimlik

BeeMaster AI;

| ❌ Yasak | ✅ Olması Gereken |
|----------|-------------------|
| Oyun gibi görünemez. | Ciddi, profesyonel |
| Çizgi film gibi görünemez. | Yetişkin, kurumsal |
| Eski Windows programı gibi görünemez. | Modern, 2026 |
| Renk karmaşası oluşturamaz. | Tutarlı palet |

**Her ekran; Apple, Stripe, Linear, Vercel, Notion kalitesinde görünmelidir.** Ancak onların kopyası olmayacaktır. BeeMaster AI'ın kendi kimliği olacaktır.

---

## 2.3 Ana Tasarım İlkesi

**Bilgi her zaman süsten önemlidir.**

| ❌ Yanlış | ✅ Doğru |
|-----------|----------|
| Dev ikonlar | Temiz kartlar |
| Büyük animasyonlar | Net başlıklar |
| Parlayan butonlar | Okunabilir grafikler |
| Renk karmaşası | Yumuşak animasyonlar |
| Gereksiz süsleme | Yüksek kontrast |

---

## 2.4 Tasarım Token Sistemi (Zorunlu)

BeeMaster AI'da **hiçbir geliştirici renk, gölge veya boşluğu doğrudan yazamaz.** Bütün değerler tasarım token'larından gelir.

```css
/* ✓ DOĞRU: Token kullan */
color: var(--color-primary);
padding: var(--space-md);
box-shadow: var(--shadow-medium);

/* ❌ YANLIŞ: Sabit değer */
color: #FFAA00;
padding: 18px;
box-shadow: 0 4px 12px rgba(0,0,0,0.3);
```

Token'ların tam listesi: `01_DESIGN_SYSTEM/TOKENS/design-tokens.json`

---

## 2.5 Renk Sistemi

BeeMaster AI'ın renkleri dekorasyon amacıyla kullanılmaz. **Her rengin anlamı vardır.**

| Renk | Anlamı | Kullanım |
|------|--------|----------|
| 🟢 Yeşil | Sağlıklı durum | Başarı, aktif, tamamlandı |
| 🟡 Sarı | Dikkat | Uyarı, bekleyen |
| 🟠 Turuncu | Risk artıyor | Yüksek risk, yaklaşan sorun |
| 🔴 Kırmızı | Kritik | Tehlike, acil, silme |
| 🔵 Mavi | Bilgilendirme | Nötr bilgi, bağlantı |
| ⚪ Gri | Pasif | Devre dışı, placeholder |

**Asla aynı anlam için iki farklı renk kullanılmaz.**

Tam renk paleti: `01_DESIGN_SYSTEM/COLORS.md`

---

## 2.6 Boşluk Sistemi (8px Grid)

Tüm boşluklar yalnızca aşağıdaki ölçekten seçilir:

| Token | Değer | Kullanım |
|-------|-------|----------|
| `--space-xs` | 4px | İkon-padding, inline gap |
| `--space-sm` | 8px | Compact gap, badge padding |
| `--space-md` | 16px | Standart padding, kart içi |
| `--space-lg` | 24px | Bölüm arası boşluk |
| `--space-xl` | 32px | Sayfa padding (mobil) |
| `--space-xxl` | 48px | Büyük section gap |
| `--space-xxxl` | 64px | Hero spacing |

**13px, 19px, 27px gibi rastgele değerler KULLANILMAZ.**

---

## 2.7 Tipografi

Uygulama **en fazla üç** yazı tipi boyutu ailesi kullanır:

| Aile | Boyut Aralığı | Kullanım |
|------|--------------|----------|
| **Başlık** | 20-36px | Sayfa başlığı, bölüm başlığı |
| **İçerik** | 14-16px | Kart metni, form açıklamaları |
| **Yardımcı Metin** | 11-12px | Tarih, etiket, durum bilgisi |

**Farklı ekranlarda farklı font aileleri kullanılmaz.** System font stack tektir.

Tam tipografi: `01_DESIGN_SYSTEM/TYPOGRAPHY.md`

---

## 2.8 Kart Sistemi

Kart, BeeMaster AI'ın **temel yapı taşıdır.** Her kart aynı kurallara uyar.

Bir kart şu bölümlerden oluşur:

```
┌────────────────────────────┐
│ Başlık            [İkon]   │  ← card-header
├────────────────────────────┤
│ Ana bilgi                  │  ← card-body
│ Destek bilgisi             │
├────────────────────────────┤
│ [Eylem]           [Eylem]  │  ← card-footer
└────────────────────────────┘
```

**Kart içinde gereksiz dekoratif öğeler kullanılmaz.**

Tam kart spesifikasyonu: `01_DESIGN_SYSTEM/COMPONENTS/CARDS.md`

---

## 2.9 Buton Sistemi

Sistemde yalnızca **dört temel buton tipi** vardır:

| Tür | Kullanım | Örnek |
|-----|----------|-------|
| **Birincil** (Primary) | Ana işlem | "Kaydet", "Ekle", "Gönder" |
| **İkincil** (Secondary) | Alternatif işlem | "İptal", "Geri" |
| **Metin** (Ghost) | Düşük öncelik | "Düzenle", "Detay" |
| **Tehlike** (Danger) | Geri alınamaz işlem | "Sil", "Hesabı Kapat" |

**Her yeni ekran bu dört tipten birini kullanır. Yeni buton tipi OLUŞTURULMAZ.**

Tam buton spesifikasyonu: `01_DESIGN_SYSTEM/COMPONENTS/BUTTONS.md`

---

## 2.10 İkon Sistemi

Bir ikon yalnızca **anlam taşıdığı zaman** kullanılmalıdır. Aynı kavram için farklı ikonlar seçilmez.

| Kavram | İkon | Asla Değişmez |
|--------|------|---------------|
| Kovan | 🏠 / hexagon | Tüm sayfalarda aynı |
| Ana Arı | 👑 / crown | Tüm sayfalarda aynı |
| Hastalık | 🦠 / microscope | Tüm sayfalarda aynı |
| AI | ⬡ / brain | Tüm sayfalarda aynı |
| Hasat | 🍯 / wheat | Tüm sayfalarda aynı |
| Tedavi | 💊 / pill | Tüm sayfalarda aynı |

Tam ikon seti: `01_DESIGN_SYSTEM/ICONS.md`

---

## 2.11 Hareket (Motion)

Animasyon gösteriş için değil, **yönlendirme için** kullanılır.

Animasyonlar:
- **Kısa** (100-300ms)
- **Akıcı** (ease-out)
- **Dikkat dağıtmayan** (sadece transform + opacity)

**Bir sayfada aynı anda birden fazla büyük animasyon çalışmaz.**

Tam animasyon spesifikasyonu: `01_DESIGN_SYSTEM/ANIMATIONS.md`

---

## 2.12 Responsive Tasarım

BeeMaster AI şu ekran genişliklerinde test edilmeden **yayınlanamaz:**

| Genişlik | Cihaz | Test Zorunlu |
|----------|-------|-------------|
| 360px | Küçük telefon | ✅ |
| 390px | iPhone 14 | ✅ |
| 768px | Tablet dikey | ✅ |
| 1024px | Tablet yatay | ✅ |
| 1440px | Laptop | ✅ |
| 1920px | Masaüstü | ✅ |

**Her ekran bu boyutlarda kullanılabilir olmalıdır.**

---

## 2.13 Erişilebilirlik

BeeMaster AI **herkes** tarafından kullanılabilmelidir.

| Kural | Gereksinim |
|-------|------------|
| Renk kontrastı | Minimum 4.5:1 (AA) |
| Klavye gezintisi | Tüm interaktif elemanlar focus alabilir |
| Buton etiketleri | Anlamlı, eylem belirten |
| Yazı boyutları | Minimum 12px |
| Durum bilgisi | Sadece renkle ifade EDİLEMEZ (ikon/metin de olmalı) |

---

## 2.14 Sayfa Yerleşim Standardı

Tüm ana sayfalar **aynı iskeleti** kullanır:

```
┌────────────────────────────────────┐
│  Üst Bilgi (Sayfa Başlığı + AI)    │
├────────────────────────────────────┤
│  Filtreler / Arama                 │
├────────────────────────────────────┤
│                                    │
│  Ana İçerik                        │
│                                    │
├────────────────────────────────────┤
│  AI Önerileri / İlgili Bilgiler    │
├────────────────────────────────────┤
│  Alt Bilgi                         │
└────────────────────────────────────┘
```

Kullanıcı her sayfada farklı bir düzen öğrenmek zorunda kalmaz.

---

## 2.15 Tasarım Denetimi (Zorunlu)

Yeni bir ekran tamamlandığında Hermes şu soruları cevaplar:

| # | Soru | Beklenen |
|---|------|----------|
| 1 | Mevcut kart sistemi kullanıldı mı? | ✅ Evet |
| 2 | Yeni renk eklendi mi? | ❌ Hayır |
| 3 | Yeni gölge tanımlandı mı? | ❌ Hayır |
| 4 | Rastgele boşluk değeri kullanıldı mı? | ❌ Hayır |
| 5 | Tasarım diğer ekranlarla uyumlu mu? | ✅ Evet |
| 6 | Mobil görünüm test edildi mi? (360, 390, 768) | ✅ Evet |
| 7 | Renkler anlamına uygun mu? (yeşil=iyi, kırmızı=kritik) | ✅ Evet |
| 8 | İkonlar tutarlı mı? (aynı kavram = aynı ikon) | ✅ Evet |

**Herhangi bir soruya olumsuz cevap verilirse, ekran yeniden gözden geçirilir.**

---

> **"Bu bölümden sonra Hermes artık kendi istediği gibi arayüz tasarlamayacak. Her yeni ekran, BeeMaster AI'ın ortak tasarım diline uymak zorundadır."**
