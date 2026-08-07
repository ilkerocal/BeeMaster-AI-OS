# BÖLÜM 14 — Platform Mimarisi (Platform Architecture & Engineering Blueprint)

**Sürüm:** 1.0  
**Öncelik:** En Kritik Teknik Bölüm  
**Durum:** Zorunlu Standart  
**Kapsam:** Altyapı, dağıtım, izleme, DevOps

> ⚠️ Bu bölüm, diğer bölümlerde detaylandırılan konuları TEKRARLAMAZ. İlgili bölümlere cross-reference verir.

---

## 14.0 Amaç

BeeMaster AI; küçük bir web sitesi değildir. Amaç; gelecekte milyonlarca koloniyi yönetebilecek, yüz milyonlarca fotoğrafı analiz edebilecek, sürekli öğrenebilecek, AI destekli bir **platform** oluşturmaktır.

---

## 14.1 Genel Mimari (Kapsayıcı Görünüm)

```
Kullanıcı
    │
    ├── Web App (Bölüm 4, 11.3)
    └── Mobile App (Bölüm 11.2)
            │
      ╔═════════════╗
      ║ API Gateway ║  ← Bu bölüm
      ╚══════╤══════╝
             │
    ┌────────┼────────┐
    ▼        ▼        ▼
  Auth   Business  Notification
  (11.16) API      API (Yeni)
             │
      ╔═════════════╗
      ║  Event Bus  ║  ← Bölüm 5.5, 11.14
      ╚══════╤══════╝
             │
  ┌──────────┼──────────┐
  ▼          ▼          ▼
Digital    AI        Knowledge
Twin       Platform  Graph
(Bölüm 5)  (Bölüm 9) (Bölüm 8)
  │          │          │
  ▼          ▼          ▼
Database  Vector DB  Graph DB
(Bölüm 6) (Yeni)    (Yeni)
  │
  ▼
Object Storage (Bölüm 11.8)
  │
  ▼
Monitoring (Yeni)
```

---

## 14.2 API Gateway

Tüm istekler tek giriş noktasından geçer. İstemciler doğrudan iç servislere erişmez.

| Görev | Açıklama |
|-------|----------|
| Kimlik doğrulama | JWT validasyonu, Supabase Auth entegrasyonu |
| Yetkilendirme | Role-based access (Least Privilege) |
| Hız sınırlama (Rate Limiting) | IP/kullanıcı bazlı throttle |
| Günlükleme | Tüm istekler audit log'a |
| API sürümleme | `/v1/`, `/v2/` prefix |
| Trafik yönlendirme | Servis discovery |

Roller: Arıcı, İşletme Yöneticisi, Veteriner Danışman, Araştırmacı, Sistem Yöneticisi.

---

## 14.3 Veri Katmanları Ayrımı

Farklı veri türleri farklı depolarda tutulur:

| Veri Türü | Depolama | Referans |
|-----------|----------|----------|
| Kullanıcı/Operasyonel veri | PostgreSQL (Supabase) | Bölüm 6 |
| Dijital İkiz olayları | **Event Store** (immutable log) | KURAL-0001, 0002 |
| Bilgi Grafiği | **Graph DB** (Dgraph/Neo4j) | Bölüm 8 |
| AI embedding'leri | **Vector DB** (pgvector) | Bölüm 9 |
| Fotoğraf/Video | **Object Storage** (S3) | Bölüm 11.8 |
| Loglar | Log yönetim sistemi | Bu bölüm |

> ⚠️ Medya dosyaları **asla** veritabanında tutulmaz. Object Storage + CDN kullanılır.

---

## 14.4 Bildirim Altyapısı

Bildirim sistemi ayrı bir servis olarak çalışır.

| Kanal | Kullanım | Öncelik |
|-------|----------|---------|
| Uygulama içi | Dashboard toast | Düşük-Orta |
| Push bildirimi | Kritik uyarılar | Yüksek |
| E-posta | Haftalık özet, rapor | Düşük |
| SMS | Acil durum (isteğe bağlı) | Kritik |

Bildirim öncelikleri: Kritik (hemen), Yüksek (1 saat), Orta (günlük), Düşük (haftalık).

---

## 14.5 İzleme (Observability)

Platform sürekli izlenir. Sorunlar kullanıcı fark etmeden tespit edilmelidir.

| Metrik | Eşik | Alarm |
|--------|------|-------|
| API gecikmesi (p95) | >500ms | ⚠️ Uyarı |
| AI analiz süresi | >30sn | ⚠️ Uyarı |
| Başarısız analiz oranı | >%10 | 🔴 Kritik |
| Senkronizasyon hataları | >%5 | 🔴 Kritik |
| Depolama kullanımı | >%80 | ⚠️ Uyarı |

Araçlar: Supabase logs, Vercel Analytics, özel health check endpoint.

---

## 14.6 DevOps ve Sürekli Dağıtım

| Süreç | Uygulama |
|-------|----------|
| Otomatik testler | Playwright E2E (Bölüm 12_TESTING) |
| Kod incelemeleri | PR review, BDAOS standartları (Bölüm 14_GITHUB) |
| Sürekli Entegrasyon (CI) | GitHub Actions → lint + test |
| Sürekli Dağıtım (CD) | Vercel auto-deploy (main branch) |
| Gözlemlenebilirlik | Health check + metrik dashboard |
| Geri Alma (Rollback) | `git revert` + Vercel instant rollback |

---

## 14.7 Sonuç

BeeMaster AI'ın başarısı yalnızca güçlü AI modellerine değil, sağlam bir mühendislik mimarisine bağlıdır. Bu bölümde tanımlanan yaklaşım sayesinde sistem: modüler, ölçeklenebilir, sürdürülebilir, güvenli, test edilebilir ve uzun ömürlü bir yapıya sahip olur.

Önceki bölümlerle birlikte tam sistem:
- Bölüm 4: Frontend (Web/Mobile/PWA)
- Bölüm 5: Digital Twin (veri modeli)
- Bölüm 6: Database (PostgreSQL)
- Bölüm 8: Knowledge Graph + Ontoloji
- Bölüm 9: Multi-Agent AI
- Bölüm 11: Veri Entegrasyonu (sensör, medya, API)
- **Bölüm 14: Platform Mimarisi (bu bölüm — altyapı)**

---

> **"İyi AI yetmez. İyi mühendislik olmadan, iyi AI çalışmaz."**
