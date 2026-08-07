# 🗃️ Veritabanı Şeması

> **BeeMaster AI Supabase veritabanı tablo şemaları.**

---

## Tablo Listesi

| Tablo | Açıklama | Kayıtlar |
|-------|----------|----------|
| `apiaries` | Arılıklar | ~10 |
| `hives` | Kovanlar | ~500 |
| `queens` | Kraliçeler | ~500 |
| `frames` | Çerçeveler | ~5000 |
| `inspections` | Muayeneler | ~10000 |
| `harvests` | Hasatlar | ~1000 |
| `feedings` | Beslemeler | ~2000 |
| `treatments` | Tedaviler | ~1000 |
| `diseases` | Hastalık kayıtları | ~500 |
| `inventory` | Envanter | ~200 |
| `profiles` | Kullanıcı profilleri | ~1000 |

## Tablo: hives

```sql
CREATE TABLE hives (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES auth.users NOT NULL,
  apiary_id UUID REFERENCES apiaries(id),
  name VARCHAR(100) NOT NULL,
  strain VARCHAR(50),           -- carniolan, caucasian, anatolian, italian, ...
  box_type VARCHAR(50),         -- langstroth, dadant, ...
  frame_count INT DEFAULT 10,
  location_lat DECIMAL(10,7),
  location_lng DECIMAL(10,7),
  installed_at DATE,
  status VARCHAR(20) DEFAULT 'active',  -- active, inactive, dead, sold
  notes TEXT,
  health_score INT DEFAULT 100,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);
```

## Tablo: queens

```sql
CREATE TABLE queens (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES auth.users NOT NULL,
  hive_id UUID REFERENCES hives(id),
  strain VARCHAR(50),
  marked_color VARCHAR(20),     -- white, yellow, red, green, blue
  birth_date DATE,
  source VARCHAR(50),           -- purchased, reared, swarm, gift, unknown
  supplier VARCHAR(100),
  cost_try DECIMAL(10,2),
  performance_score INT,
  status VARCHAR(20) DEFAULT 'active',
  notes TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## Tablo: inspections

```sql
CREATE TABLE inspections (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES auth.users NOT NULL,
  hive_id UUID REFERENCES hives(id) NOT NULL,
  date DATE NOT NULL,
  population INT,               -- 1-10 ölçeği
  queen_seen BOOLEAN,
  varroa_count INT,             -- 100 arı başına
  temperament VARCHAR(20),      -- calm, normal, aggressive
  actions TEXT[],               -- dizi: ['added_super', 'checked_queen']
  notes TEXT,
  weather VARCHAR(50),
  temperature DECIMAL(4,1),
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## Tablo: harvests

```sql
CREATE TABLE harvests (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES auth.users NOT NULL,
  hive_id UUID REFERENCES hives(id) NOT NULL,
  date DATE NOT NULL,
  weight_kg DECIMAL(5,2),
  quality VARCHAR(1),           -- A, B, C
  frames INT,
  honey_type VARCHAR(50),       -- çiçek, çam, kestane, ...
  notes TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## Tablo: diseases

```sql
CREATE TABLE diseases (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES auth.users NOT NULL,
  hive_id UUID REFERENCES hives(id) NOT NULL,
  date DATE NOT NULL,
  disease VARCHAR(50) NOT NULL,  -- varroa, nosema, afb, efb, chalkbrood, sacbrood, shb
  severity VARCHAR(20),          -- low, medium, high, critical
  symptoms TEXT[],
  treatment TEXT,
  treatment_status VARCHAR(20),  -- pending, in_progress, completed
  ai_confidence INT,             -- 0-100
  ai_reasoning TEXT,
  notes TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## Tablo: inventory

```sql
CREATE TABLE inventory (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES auth.users NOT NULL,
  name VARCHAR(100) NOT NULL,
  category VARCHAR(50),         -- medicine, equipment, feed, hive_parts
  unit VARCHAR(20),             -- kg, adet, litre, ml
  quantity DECIMAL(10,2),
  min_stock DECIMAL(10,2),
  cost_try DECIMAL(10,2),
  supplier VARCHAR(100),
  notes TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## Index'ler

```sql
-- Sık sorgulanan alanlar
CREATE INDEX idx_hives_user ON hives(user_id);
CREATE INDEX idx_inspections_hive ON inspections(hive_id);
CREATE INDEX idx_inspections_date ON inspections(date DESC);
CREATE INDEX idx_harvests_date ON harvests(date DESC);
CREATE INDEX idx_diseases_hive ON diseases(hive_id);
```

## Migration Kuralları

1. **Her migration geri alınabilir olmalı.**
2. **Yeni kolon: DEFAULT değer ile ekle.**
3. **Kolon silme: Önce deprecate et, 2 sürüm sonra sil.**
4. **Index eklerken production'da CONCURRENTLY kullan.**
5. **Migration'ları asla manuel yapma — migration dosyası yaz.**
