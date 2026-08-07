# 🤖 AI Engine

> **BeeMaster AI öneri motoru. Hastalık tespiti, kovan analizi, hasat tahmini.**

---

## AI Felsefesi

**RULE-0007:** Her AI önerisi şu üç bileşeni içermelidir:
- **Confidence (güven skoru):** %0-100
- **Reasoning (gerekçe):** AI neden bu sonuca vardı
- **Evidence (kanıt):** Hangi verilere dayanarak

**RULE-0006:** Her ekran Dijital İkiz'i güçlendirmeli. Veri girişi → AI içgörüsü → arıcı kararı.

## Öneri Formatı

```
╔══════════════════════════════════╗
║  ⬡ AI ÖNERİSİ                    ║
║                                  ║
║  Güven: %87 ████████░░           ║
║                                  ║
║  Gerekçe:                        ║
║  Son 3 muayenede varroa sayısı   ║
║  artış gösteriyor (3→5→8).      ║
║  Mevsimsel risk yüksek.          ║
║                                  ║
║  Kanıt:                          ║
║  • Muayene #42: 3 akar/100 arı  ║
║  • Muayene #45: 5 akar/100 arı  ║
║  • Muayene #48: 8 akar/100 arı  ║
║                                  ║
║  Öneri: Formik asit uygulaması   ║
║  ⚠️ Bu bir öneridir, kesin      ║
║  tanı değildir.                  ║
╚══════════════════════════════════╝
```

## AI Modülleri

### 1. Hastalık Tespiti
```js
function analyzeDiseaseRisk(hive, inspections) {
  const factors = {
    varroaCount: getTrend(inspections, 'varroa_count'),
    population: getTrend(inspections, 'population'),
    season: getCurrentSeason(),
    weather: getRecentWeather()
  };
  
  const diseases = DISEASE_DB.filter(d => matchSymptoms(factors, d.symptoms));
  
  return diseases.map(d => ({
    disease: d.name,
    confidence: calculateConfidence(factors, d),
    reasoning: generateReasoning(factors, d),
    evidence: getEvidence(inspections, d)
  }));
}
```

### 2. Hasat Tahmini
```js
function predictHarvest(hive, pastHarvests, weather) {
  // Makine öğrenmesi olmadan, kural tabanlı
  const avgYield = pastHarvests.reduce((sum, h) => sum + h.weight_kg, 0) / pastHarvests.length;
  const weatherFactor = getWeatherFactor(weather);
  const populationFactor = hive.population / 10;
  
  return {
    estimated: Math.round(avgYield * weatherFactor * populationFactor),
    confidence: calculateHarvestConfidence(pastHarvests.length),
    factors: { avgYield, weatherFactor, populationFactor }
  };
}
```

### 3. Kraliçe Performansı
```js
function analyzeQueenPerformance(queen, hiveInspections, harvests) {
  return {
    score: calculateQueenScore(queen, hiveInspections, harvests),
    recommendations: getQueenRecommendations(queen),
    confidence: 75 // sabit — az veri
  };
}
```

## Güven Skorlaması

| Veri Miktarı | Güven |
|-------------|-------|
| 0 kayıt | %0 — yetersiz veri |
| 1-5 kayıt | %30-50 — düşük güven |
| 6-20 kayıt | %50-75 — orta güven |
| 20-50 kayıt | %75-90 — yüksek güven |
| 50+ kayıt | %90-99 — çok yüksek güven |

**Asla %100 gösterme.** AI her zaman yanılma payı bırakır.
