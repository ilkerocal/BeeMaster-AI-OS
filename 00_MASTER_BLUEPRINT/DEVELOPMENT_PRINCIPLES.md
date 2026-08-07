# 🐝 BeeMaster AI — Geliştirme Prensipleri

> **Bu prensipler, her kod kararının temelini oluşturur. Bir prensip ile kural çakışırsa, prensip kazanır.**

---

## 1. DRY — Don't Repeat Yourself

İki kez yazıyorsan, fonksiyon yap. Üç kez kullanıyorsan, bileşen yap.

```js
// ❌ YANLIŞ: Tekrarlayan kod
localStorage.setItem('hives', JSON.stringify(data));
localStorage.setItem('queens', JSON.stringify(data));
localStorage.setItem('frames', JSON.stringify(data));

// ✓ DOĞRU: Abstract et
function saveToStorage(key, data) {
  localStorage.setItem(key, JSON.stringify(data));
}
```

## 2. YAGNI — You Aren't Gonna Need It

Gelecekte lazım olabilir diye kod yazma. Şu an ihtiyaç yoksa yazma.

```js
// ❌ YANLIŞ: "Belki ilerde lazım olur"
class HiveManager {
  exportToPDF() { /* ... */ }
  shareToSocialMedia() { /* ... */ }
  generateQRCode() { /* ... */ }
}

// ✓ DOĞRU: Sadece şu an gereken
class HiveManager {
  add(hive) { /* ... */ }
  remove(id) { /* ... */ }
  list() { /* ... */ }
}
```

## 3. KISS — Keep It Simple, Stupid

En basit çözüm genelde en iyisidir. Karmaşıklık ekleme.

```js
// ❌ YANLIŞ: Gereksiz karmaşıklık
const status = data?.status?.current?.state ?? 'unknown';

// ✓ DOĞRU: Basit ve okunaklı
const status = data.status || 'unknown';
```

## 4. Single Responsibility

Her fonksiyon, her modül, her dosya tek bir iş yapmalı.

```js
// ❌ YANLIŞ: Birden fazla sorumluluk
function processHive(hive) {
  validateData(hive);
  saveToDb(hive);
  updateUI(hive);
  sendNotification(hive);
  logActivity(hive);
}

// ✓ DOĞRU: Her fonksiyon tek iş
function validateHiveData(hive) { /* ... */ }
function saveHiveToDb(hive) { /* ... */ }
function updateHiveUI(hive) { /* ... */ }
```

## 5. Fail Fast, Fail Loud

Hata olursa sessizce geçme. Erken yakala, net mesaj ver.

```js
// ❌ YANLIŞ: Sessiz hata
function getHive(id) {
  const hive = db.find(h => h.id === id);
  return hive; // undefined dönebilir, kimse bilmez
}

// ✓ DOĞRU: Net hata
function getHive(id) {
  if (!id) throw new Error('getHive: id gerekli');
  const hive = db.find(h => h.id === id);
  if (!hive) throw new Error(`Kovan bulunamadı: ${id}`);
  return hive;
}
```

## 6. Composition Over Inheritance

Kalıtım yerine birleştirme. Prototype chain'den uzak dur.

```js
// ❌ YANLIŞ: Kalıtım zinciri
class Animal { /* ... */ }
class Insect extends Animal { /* ... */ }
class Bee extends Insect { /* ... */ }
class Queen extends Bee { /* ... */ }

// ✓ DOĞRU: Birleştirme (composition)
function withWings(obj) { return { ...obj, fly: () => 'uçuyor' }; }
function withSting(obj) { return { ...obj, sting: () => 'sokuyor' }; }
const queen = withSting(withWings({ role: 'queen' }));
```

## 7. Progressive Enhancement

Önce temel işlevsellik, sonra geliştirme. Offline önce gelir, cloud sonra.

```js
// ✓ DOĞRU: Önce localStorage çalışsın, sonra cloud
async function saveData(key, data) {
  // Her zaman localStorage'a yaz (hızlı, garantili)
  localStorage.setItem(key, JSON.stringify(data));
  
  // Cloud varsa oraya da yaz (bonus)
  if (navigator.onLine) {
    try {
      await cloudSave(key, data);
    } catch (e) {
      console.warn('Cloud sync başarısız, local veri güvende');
    }
  }
}
```

## 8. Convention Over Configuration

Varsayılanlar akıllı olsun. Her şeyi yapılandırma.

```js
// ❌ YANLIŞ: Her şey config
const btn = new Button({
  color: '#f59e0b',
  size: 'medium',
  variant: 'primary',
  rounded: true,
  shadow: 'medium',
  animation: 'pulse'
});

// ✓ DOĞRU: Varsayılanlar akıllı
const btn = new Button({ variant: 'primary' });
// color: amber (tasarım sistemi)
// size: medium
// rounded: true (tasarım sistemi)
```

## 9. Test-First (TDD)

Önce test yaz, sonra kod. Kırmızı → Yeşil → Refactor.

```js
// 1. KIRMIZI: Önce test
test('yeni kovan eklenince listeye eklenir', () => {
  const app = new App();
  app.addHive({ name: 'Kovan 1' });
  expect(app.hives.length).toBe(1);
});

// 2. YEŞİL: Minimum kod
addHive(hive) {
  this.hives.push(hive);
}

// 3. REFACTOR: Temizle
```

## 10. Documentation Driven

Kod kendini açıklamalı. Açıklayamıyorsa yorum ekle. Karmaşıksa doküman yaz.

```js
// ❌ YANLIŞ: Yorum kodu tekrar ediyor
// Kovan sayısını döndürür
function getHiveCount() {
  return hives.length; // hives dizisinin uzunluğunu döndür
}

// ✓ DOĞRU: Yorum "neden"i açıklıyor
// Her muayenede en az 1 kovan olmalı, boş apiary kontrolü
function getHiveCount() {
  return hives.length;
}
```

---

> **"İyi kod okunur, kötü kod açıklanır. En iyi kod, açıklamaya ihtiyaç duymaz."**
