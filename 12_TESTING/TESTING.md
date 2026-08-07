# 🧪 Test Stratejisi

> **BeeMaster AI test standartları. Her özellik test edilmeden deploy edilmez.**

---

## Test Piramidi

```
        ┌───────┐
        │  E2E  │  Playwright (kritik akışlar)
        ├───────┤
        │  Int. │  Modül entegrasyon testleri
        ├───────┤
        │ Unit  │  Fonksiyon birim testleri
        └───────┘
```

## Playwright E2E Testleri (Python)

**RULE-0008:** Her deploy öncesi Playwright testi zorunlu.

```python
# test_smoke.py — Minimum canlılık testi
import asyncio
import time
from playwright.async_api import async_playwright

async def smoke_test():
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=True)
        ctx = await browser.new_context(
            viewport={'width': 375, 'height': 812}  # mobil
        )
        page = await ctx.new_page()
        
        errors = []
        page.on('pageerror', lambda err: errors.append(str(err)))
        
        # 1. Sayfa yükleme
        await page.goto(f'https://beemaster-ai.vercel.app/?cb={int(time.time())}',
                        wait_until='networkidle')
        
        # 2. Login
        await page.fill('#email', 'adnanmurat021@gmail.com')
        await page.fill('#password', '123456')
        await page.click('button[type="submit"]')
        await page.wait_for_selector('.dashboard', timeout=10000)
        
        # 3. Dashboard kontrolü
        assert await page.is_visible('.dashboard')
        
        # 4. 0 console hatası
        assert len(errors) == 0, f'Console errors: {errors}'
        
        # 5. Screenshot
        await page.screenshot(path='smoke_test.png')
        
        await browser.close()
        return True

result = asyncio.run(smoke_test())
print('✅ Smoke test passed' if result else '❌ Failed')
```

## Test Check-list'i (Her Deploy Öncesi)

- [ ] Sayfa yükleniyor (networkidle, <3sn)
- [ ] Login çalışıyor
- [ ] Dashboard render ediliyor
- [ ] Tüm modüller açılıyor
- [ ] Form submit çalışıyor
- [ ] Modal açılıp kapanıyor
- [ ] Console'da 0 hata
- [ ] Mobil görünüm düzgün (375×812)
- [ ] Tüm metinler Türkçe
- [ ] Cache-bust versiyon artırıldı
- [ ] Screenshot alındı ve kontrol edildi

## Visual QA Protokolü

```python
# Visual QA — kritik sayfaların ekran görüntüleri
PAGES_TO_CHECK = [
    ('/', 'dashboard'),
    ('/#hives', 'hives'),
    ('/#diseases', 'diseases'),
    ('/#inspections', 'inspections'),
]

for url, name in PAGES_TO_CHECK:
    await page.goto(f'https://beemaster-ai.vercel.app/{url}')
    await page.screenshot(path=f'qa_{name}.png', full_page=True)
```

## Birim Testleri (test.html)

```html
<!-- Basit test runner — framework yok -->
<script>
const tests = [];
function test(name, fn) { tests.push({ name, fn }); }
function assert(condition, msg) { if (!condition) throw new Error(msg); }

function runTests() {
  let passed = 0, failed = 0;
  for (const t of tests) {
    try {
      t.fn();
      passed++;
      console.log(`✅ ${t.name}`);
    } catch (e) {
      failed++;
      console.error(`❌ ${t.name}: ${e.message}`);
    }
  }
  console.log(`${passed}/${tests.length} passed, ${failed} failed`);
}

// Örnek testler
test('escapeHtml — XSS koruması', () => {
  assert(escapeHtml('<script>alert("xss")</script>') === 
    '&lt;script&gt;alert("xss")&lt;/script&gt;');
});

test('BM.uid — benzersiz ID', () => {
  const ids = new Set();
  for (let i = 0; i < 1000; i++) ids.add(BM.uid());
  assert(ids.size === 1000, 'Duplicate IDs found');
});
</script>
```
