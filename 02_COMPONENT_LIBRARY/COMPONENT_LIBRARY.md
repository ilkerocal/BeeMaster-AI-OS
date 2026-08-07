# 🧩 Component Library

> **BeeMaster AI Bileşen Kütüphanesi. Her bileşen bir COMP numarası ile tanımlanır.**

---

## Kullanım Kuralı

**RULE-0005:** Her UI parçası bu kütüphanede tanımlı olmalı. Yeni UI icat etme.

Eğer ihtiyacın olan bileşen burada yoksa:
1. Önce bileşeni buraya ekle (yeni COMP-NNNN)
2. Tasarım token'larını kullan
3. Dokümante et
4. Sonra kodda kullan

## Bileşen Listesi

| ID | Bileşen | Dosya | Durum |
|----|---------|-------|-------|
| COMP-0001 | Button | `COMP-0001_BUTTON.md` | ✅ |
| COMP-0002 | Card | `COMP-0002_CARD.md` | ✅ |
| COMP-0003 | Modal | `COMP-0003_MODAL.md` | ✅ |
| COMP-0004 | Timeline | `COMP-0004_TIMELINE.md` | ✅ |
| COMP-0005 | Hive Card | `COMP-0005_HIVE_CARD.md` | ✅ |
| COMP-0006 | AI Card | `COMP-0006_AI_CARD.md` | ✅ |
| COMP-0007 | Disease Card | `COMP-0007_DISEASE_CARD.md` | ✅ |
| COMP-0008 | Stats Card | `COMP-0008_STATS_CARD.md` | ✅ |
| COMP-0009 | Health Ring | `COMP-0009_HEALTH_RING.md` | ✅ |
| COMP-0010 | AI Confidence | `COMP-0010_AI_CONFIDENCE.md` | ✅ |
| COMP-0011 | Empty State | `COMP-0011_EMPTY_STATE.md` | ✅ |
| COMP-0012 | Error State | `COMP-0012_ERROR_STATE.md` | ✅ |
| COMP-0013 | Search Bar | `COMP-0013_SEARCH_BAR.md` | ✅ |
| COMP-0014 | Filter Bar | `COMP-0014_FILTER_BAR.md` | ✅ |
| COMP-0015 | Quick Action | `COMP-0015_QUICK_ACTION.md` | ✅ |

## Bileşen Formatı

Her bileşen dosyası şu formatta olmalı:

```markdown
# COMP-NNNN: [Bileşen Adı]

**Kategori:** [Temel | Birleşik | Domain]
**Durum:** [Active | Draft | Deprecated]

## Kullanım

## HTML

## CSS

## JavaScript

## Varyantlar

## Örnekler
```
