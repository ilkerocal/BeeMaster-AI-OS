# BÖLÜM 7 — Çerçeve Tarama ve Görsel Analiz Sistemi (Frame Scanner & Vision Engine)

**Sürüm:** 1.0  
**Öncelik:** En Kritik Modül  
**Durum:** Zorunlu Standart  
**Kapsam:** Görüntü analizi ve Dijital İkiz veri girişi

---

## 7.0 Amaç

Frame Scanner'ın amacı yalnızca fotoğraf çekmek **değildir.**

Amaç;
- bir çerçeveyi dijital ortama aktarmak,
- yapay zekâ ile analiz etmek,
- koloninin Dijital İkiz'ini güncellemek,
- ve gelecekte yapılacak tahminler için güvenilir veri oluşturmaktır.

**Frame Scanner, BeeMaster AI'ın en önemli veri giriş modülüdür.**

---

## 7.1 Temel Felsefe

Bir fotoğraf yalnızca görüntü **değildir.**

Bir fotoğraf;
- zaman bilgisidir,
- koloni bilgisidir,
- sağlık bilgisidir,
- üretim bilgisidir,
- davranış bilgisidir.

**Her tarama, koloninin hafızasına eklenen yeni bir gözlemdir.**

---

## 7.2 Tarama Süreci (Zorunlu İş Akışı)

Her tarama standart bir iş akışını takip eder. **Hiçbir adım atlanmaz.**

```
① Çerçeve Seçimi
      │
      ▼
② Ön Yüz Tarama
      │
      ▼
③ Arka Yüz Tarama
      │
      ▼
④ Görüntü Kalite Kontrolü
      │
      ▼
⑤ AI Analizi
      │
      ▼
⑥ Dijital İkiz Güncellemesi
      │
      ▼
⑦ Rapor ve Öneriler
```

---

## 7.3 Tarama Kuralları

Her çerçeve için aşağıdaki bilgiler kaydedilir:

| Alan | Tip | Zorunlu |
|------|-----|---------|
| Kovan Kimliği (hive_id) | UUID | ✅ |
| Çerçeve Numarası | Integer | ✅ |
| Tarama Tarihi | Date | ✅ |
| Tarama Saati | Time | ✅ |
| Tarayan Kullanıcı | UUID | ✅ |
| Ön Yüz Fotoğrafı | Image | ✅ |
| Arka Yüz Fotoğrafı | Image | ✅ |
| Görüntü Kalitesi | Score (0-100) | ✅ |
| GPS Konumu | Lat/Lng | ⬜ |
| Hava Durumu | JSON | ⬜ |

Bu bilgiler görüntü ile birlikte saklanır.

---

## 7.4 Görüntü Kalite Kontrolü

AI analizden **önce** fotoğrafı değerlendirir.

| Kriter | Eşik | Başarısızsa |
|--------|------|-------------|
| Netlik | >70 | Yeniden çekim öner |
| Odak | Merkez net | Yeniden çekim öner |
| Hareket Bulanıklığı | Yok | Yeniden çekim öner |
| Işık Dengesi | Orta | Uyarı, analiz devam |
| Kontrast | Yeterli | Uyarı, güven düşür |
| Çerçevenin Tam Görünmesi | %100 | Yeniden çekim öner |
| Aşırı Gölge | <%20 | Uyarı, güven düşür |
| Aşırı Parlama | <%10 | Uyarı, güven düşür |

**Düşük kaliteli görüntüler analiz edilse bile güven skoru düşürülür.**

---

## 7.5 Görsel Analiz Katmanları

Frame Scanner tek bir analiz yapmaz. Birden fazla analiz motoru aynı görüntü üzerinde çalışır.

```
Görüntü
   │
   ├── ① Çerçeve Algılama        ← Sınır tespiti
   ├── ② Petek Hücresi Analizi    ← Hücre bazında
   ├── ③ Yavru Analizi            ← Açık/kapalı yavru
   ├── ④ Bal Analizi              ← Kapalı bal hücreleri
   ├── ⑤ Polen Analizi            ← Polen depoları
   ├── ⑥ Ana Arı Tespiti          ← Kraliçe varlığı
   ├── ⑦ Arı Yoğunluğu            ← İşçi arı sayısı
   ├── ⑧ Hastalık Bulguları       ← Görsel semptomlar
   ├── ⑨ Varroa İşaretleri        ← Parazit belirtileri
   └── ⑩ Anomali Tespiti          ← Sınıflandırılamayan
```

Her analiz bağımsız çalışır. Sonuçlar birleştirilir.

---

## 7.6 Hücre (Göz) Seviyesinde Analiz

BeeMaster AI mümkün olduğunca **petek gözü seviyesinde** analiz yapmayı hedefler.

Her hücre şu kategorilerden birine atanabilir:

| Kategori | Açıklama |
|----------|----------|
| Boş | İçi boş hücre |
| Yumurta | Yeni bırakılmış yumurta |
| Larva | Gelişmekte olan larva |
| Kapalı Yavru | Üzeri kapatılmış yavru gözü |
| Bal | Kapalı bal hücresi |
| Polen | Polen deposu |
| Kraliçe Yüksüğü | Oğul/ana arı yüksüğü |
| Hasarlı | Bozuk/ezik hücre |
| Belirsiz | Sınıflandırılamayan |

**Belirsiz sınıflandırmalar işaretlenir ve güven puanı düşürülür.**

---

## 7.7 Çerçeve Sağlık Skoru

Her tarama sonunda çerçeve için bir sağlık puanı hesaplanır.

| Faktör | Ağırlık |
|--------|---------|
| Yavru düzeni (uniformity) | %25 |
| Bal dağılımı | %20 |
| Polen miktarı | %10 |
| Hücre bütünlüğü | %15 |
| Hastalık bulguları | %20 |
| Arı yoğunluğu | %10 |

Sağlık puanı tek başına karar değildir; yalnızca Dijital İkiz'in değerlendirme sürecine katkı sağlar.

---

## 7.8 Değişim Analizi

BeeMaster AI tek bir fotoğrafı değerlendirmekle yetinmez. Aynı çerçevenin farklı tarihlerdeki görüntülerini karşılaştırır.

```
15 Nisan → Yavru Alanı: %42
22 Nisan → Yavru Alanı: %58
         ────────────────
         Artış: +%16
```

Bu değişim Dijital İkiz'in büyüme modeline işlenir.

---

## 7.9 Ana Arı Analizi

Ana arı görüntüde tespit edilirse:

| Veri | Açıklama |
|------|----------|
| Konum | Çerçeve üzerindeki koordinat |
| Durum | Görüldü / Görülmedi |
| İşaret Rengi | Varsa: beyaz, sarı, kırmızı, yeşil, mavi |
| Görüntü Kalitesi | Ana arı bölgesinin netliği |
| Güven Puanı | Tespit güveni |

**Ana arının görülmemesi tek başına "ana arı yok" anlamına gelmez.**

---

## 7.10 Hastalık Analizi

Frame Scanner **hastalık teşhisi koymaz.** Yalnızca görsel bulguları tespit eder.

| Bulgu | Olası Hastalık |
|-------|---------------|
| Düzensiz yavru deseni | Yavru Çürüklüğü, Nosema |
| Çökük kapaklar | Yavru Çürüklüğü (AFB/EFB) |
| Delikli yavru gözleri | Varroa hasarı |
| Renk değişiklikleri | Kireç Hastalığı, Küf |
| Küf benzeri oluşumlar | Kireç Hastalığı |
| Şüpheli larvalar | Torba Hastalığı |

Bu bulgular Karar Motoru (Bölüm 6) tarafından diğer verilerle birlikte değerlendirilir.

---

## 7.11 Anomali Tespiti

Sistem daha önce görmediği veya sınıflandıramadığı bir görüntüyle karşılaşırsa:

1. **"Anomali"** olarak işaretler
2. Kullanıcıdan doğrulama ister
3. Gerekirse uzman incelemesine yönlendirir

Bu sayede model zamanla yeni durumları öğrenebilir (KURAL-0004).

---

## 7.12 Tarama Sonrası AI Raporu

Her tarama sonunda standart bir rapor oluşturulur:

```
╔═══════════════════════════════╗
║  📸 TARAMA RAPORU              ║
║                               ║
║  Tarama Kalitesi: %88         ║
║  Çerçeve Sağlık Skoru: 72/100 ║
║                               ║
║  Yavru Alanı:    %42          ║
║  Bal Alanı:      %31          ║
║  Polen Alanı:    %12          ║
║  Boş Hücre:      %15          ║
║                               ║
║  Hastalık Bulgusu: Yok        ║
║  Ana Arı: Görüldü (%94)      ║
║                               ║
║  Öneri: Rutin takip           ║
║  Güven: %91                   ║
╚═══════════════════════════════╝
```

---

## 7.13 Dijital İkiz Güncellemesi

Tarama tamamlandıktan sonra:

1. ✅ Ham görüntü saklanır
2. ✅ AI analiz sonuçları kaydedilir
3. ✅ Eski kayıtlar korunur (KURAL-0002)
4. ✅ Dijital İkiz güncellenir
5. ✅ Tahmin modelleri yeniden çalıştırılır
6. ✅ Gerekirse Dashboard uyarıları güncellenir

---

## 7.14 Gelecek Geliştirmeler

Frame Scanner ilerleyen sürümlerde aşağıdaki yetenekleri destekleyecek şekilde tasarlanmalıdır:

| Yetenek | Açıklama |
|---------|----------|
| Video analizi | Hareketli görüntüden çerçeve analizi |
| Çoklu çerçeve taraması | Aynı anda birden fazla çerçeve |
| 3B petek modeli | Üç boyutlu hücre haritası |
| Termal kamera desteği | Isı haritası ile kuluçka tespiti |
| UV görüntüleme | Çiçek/nektar haritalama |
| Ses analizi entegrasyonu | Görüntü + ses birleşik analiz |
| Otomatik çerçeve numarası tanıma | OCR ile numara okuma |
| Robotik tarama sistemleri | Otonom kovan içi tarama |

**Mimari bu genişlemelere açık olmalıdır.**

---

## 7.15 Başarı Ölçütleri

Frame Scanner'ın başarısı yalnızca görüntü işleme doğruluğu ile ölçülmez.

| Metrik | Hedef |
|--------|-------|
| Analiz doğruluğu (hücre sınıflandırma) | >%85 |
| Yeniden çekim oranı | <%15 |
| Kullanıcı onay oranı (AI bulguları) | >%80 |
| AI güven puanlarının kalibrasyonu | ±%5 sapma |
| Aynı çerçeve zaman tutarlılığı | >%90 |
| Dijital İkiz tahminlerine katkısı | Sürekli artan |

---

## 7.16 Sonuç

Frame Scanner, BeeMaster AI'ın "kamera" modülü **değildir.**

**O, Dijital İkiz'in gözüdür.**

Her tarama;
- koloninin hafızasını genişletir,
- AI'ın öğrenmesini destekler,
- gelecekteki tahminlerin doğruluğunu artırır.

Bu nedenle görüntü kalitesi, analiz şeffaflığı ve veri bütünlüğü bu modülün temel öncelikleridir.

---

> **"Her fotoğraf bir gözlemdir. Her gözlem Dijital İkiz'i büyütür."**
