# 🔄 GitHub İş Akışı

> **BeeMaster AI GitHub standartları. Branch, commit, PR, CI/CD.**

---

## Repo Yapısı

| Repo | Amaç |
|------|------|
| `ilkerocal/beemaster-ai` | Uygulama kodu |
| `ilkerocal/BeeMaster-AI-OS` | Geliştirme standartları (bu repo) |

## Branch Stratejisi

```
main           ← Production (Vercel'e otomatik deploy)
  └── feat/*   ← Yeni özellikler
  └── fix/*    ← Hata düzeltmeleri
  └── style/*  ← CSS/UI değişiklikleri
  └── refactor/* ← Kod iyileştirme
```

**Kural:** Doğrudan main'e push YOK. Her değişiklik branch'te başlar.

## Commit Formatı

```
<type>: <kısa açıklama>

<detaylı açıklama — opsiyonel>
```

**Type'lar:**
- `feat`: Yeni özellik
- `fix`: Hata düzeltme
- `style`: CSS/UI değişikliği
- `refactor`: Kod iyileştirme (davranış değişmez)
- `test`: Test ekleme/düzeltme
- `docs`: Dokümantasyon
- `chore`: Yapılandırma, bağımlılık

**Örnekler:**
```
feat: Hastalık detay modal'ı eklendi
fix: Sidebar overlay z-index düzeltildi
style: v6 dark theme renk token'ları güncellendi
docs: BDAOS kuralları eklendi
```

## PR (Pull Request) Süreci

1. Branch oluştur: `feat/disease-modal`
2. Kodu yaz, test et
3. Commit: `feat: Hastalık detay modal'ı eklendi`
4. Push: `git push -u origin feat/disease-modal`
5. PR aç (opsiyonel — direkt merge de yapılabilir)
6. Playwright testi
7. Merge → main
8. Vercel otomatik deploy

## CI/CD

```yaml
# .github/workflows/deploy.yml (opsiyonel)
# Vercel otomatik deploy kullanıldığı için şu an gerekli değil
# Ama ileride test otomasyonu eklenebilir
```

## Vercel Deploy

```bash
# Manuel deploy (Vercel auto-deploy yeterli)
git push origin main
# Vercel 90 saniye içinde deploy eder
# URL: https://beemaster-ai.vercel.app
```

## Deploy Sonrası Kontrol

```bash
# Deploy oldu mu?
curl -sI https://beemaster-ai.vercel.app | head -5

# Cache-bust versiyon kontrolü
curl -s https://beemaster-ai.vercel.app/ | grep "app.bundle.*?v="

# Playwright ile canlı test (90 saniye sonra)
```
