# 🐝 BeeMaster AI Development OS (BDAOS)

> **AI'lar için İşletim Sistemi.** Bu repo, BeeMaster AI uygulamasının kodunu değil, **nasıl geliştirileceğini** tanımlar.

---

## Bu Nedir?

BDAOS, BeeMaster AI projesinde çalışan tüm AI agent'ların (Hermes, DeepSeek, Claude, Codex, GitHub Copilot) uyması gereken standartları, kuralları ve karar çerçevelerini içeren bir **geliştirme işletim sistemidir**.

Bir AI, BeeMaster AI üzerinde çalışmaya başlamadan önce bu repoyu okur. Kod yazmadan önce kuralları, tasarım sistemini ve bileşen kütüphanesini referans alır.

## Neden Var?

Çünkü AI'lar tutarlı değil. Her oturumda farklı stiller, farklı yaklaşımlar, farklı kalite seviyeleri.

BDAOS bunu çözer:
- **Aynı kurallar** → aynı kalite
- **Aynı tasarım sistemi** → aynı görünüm
- **Aynı bileşenler** → aynı davranış
- **Aynı karar çerçevesi** → aynı mimari seçimler

## Nasıl Kullanılır?

### Hermes için
```bash
# Hermes otomatik olarak .hermesrules dosyasını okur
# Her geliştirme oturumunda BDAOS kuralları aktiftir
```

### Diğer AI'lar için
```
1. Repoyu klonla
2. 00_MASTER_BLUEPRINT/MASTER_BLUEPRINT.md oku
3. İlgili modülün dokümanlarını oku
4. Kurallara göre geliştir
```

## Dizin Yapısı

| Dizin | İçerik |
|-------|--------|
| `00_MASTER_BLUEPRINT/` | **📜 Anayasa**, şirket felsefesi, ürün vizyonu, geliştirme prensipleri |
| `01_DESIGN_SYSTEM/` | Renkler, tipografi, bileşen tasarımları |
| `02_COMPONENT_LIBRARY/` | Bileşen kod şablonları ve kullanım kuralları |
| `03_ARCHITECTURE/` | Sistem mimarisi, veri akışı, state yönetimi |
| `04_FRONTEND/` | HTML, CSS, JS yazım standartları |
| `05_BACKEND/` | Supabase, auth, RLS |
| `06_DATABASE/` | Şema, migration, sorgu pattern'leri |
| `07_AI_ENGINE/` | Öneri sistemi, güven skorlaması |
| `08_DIGITAL_TWIN/` | Dijital ikiz modeli |
| `09_FRAME_SCANNER/` | Çerçeve tarayıcı |
| `10_DISEASE_ENGINE/` | Hastalık tespit motoru |
| `11_API/` | API endpoint'leri |
| `12_TESTING/` | Test stratejisi |
| `13_DEBUGGING/` | Hata ayıklama |
| `14_GITHUB/` | Branch, commit, PR standartları |
| `15_HERMES/` | Hermes yapılandırması |
| `16_PROMPTS/` | Prompt kütüphanesi |
| `17_SKILLS/` | Hermes skill'leri |
| `18_TEMPLATES/` | Kod şablonları |
| `19_CHECKLISTS/` | Kontrol listeleri |
| `20_RELEASES/` | Sürüm notları, changelog |

## Hızlı Başlangıç (AI Agent için)

1. `00_MASTER_BLUEPRINT/MASTER_BLUEPRINT.md` — sistemin tamamını anla
2. `.hermesrules` — tüm kuralları yükle
3. `01_DESIGN_SYSTEM/DESIGN_SYSTEM.md` — tasarım dilini öğren
4. `02_COMPONENT_LIBRARY/COMPONENT_LIBRARY.md` — hazır bileşenleri tanı
5. Göreve başla

---

> **"Kod yazmadan önce düşün. Plan yap. Onay al. Sonra uygula."**
> — BDAOS Rule-0001
