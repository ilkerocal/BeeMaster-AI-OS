# 🗄️ Backend (Supabase)

> **BeeMaster AI backend standartları. Supabase = PostgreSQL + Auth + Storage + RLS.**

---

## Supabase Yapılandırması

| Parametre | Değer |
|-----------|-------|
| Proje URL | `https://assfwtjbvuuxclioqsih.supabase.co` |
| Anon Key | `sb_publishable_3j7uCLoJRximHZjlAi4Frw_7HCwHm6M` |
| Veritabanı | PostgreSQL 15 |
| Auth | Email/Şifre (Supabase Auth) |
| Storage | Kovan fotoğrafları için |

## Client (Inline, CDN Yok)

```js
// Supabase REST API — inline client
const SUPABASE_URL = 'https://assfwtjbvuuxclioqsih.supabase.co';
const SUPABASE_ANON_KEY = 'sb_publishable_3j7uCLoJRximHZjlAi4Frw_7HCwHm6M';

async function sbFetch(path, opts = {}) {
  const headers = {
    'apikey': SUPABASE_ANON_KEY,
    'Content-Type': 'application/json',
    ...opts.headers
  };
  
  // JWT token varsa ekle
  const session = JSON.parse(localStorage.getItem('sb-session') || '{}');
  if (session.access_token) {
    headers['Authorization'] = `Bearer ${session.access_token}`;
  }
  
  const res = await fetch(`${SUPABASE_URL}${path}`, { ...opts, headers });
  if (!res.ok) throw new Error(`Supabase: ${res.status}`);
  return res.json();
}

async function sbAuth(email, password) {
  const data = await sbFetch('/auth/v1/token?grant_type=password', {
    method: 'POST',
    body: JSON.stringify({ email, password })
  });
  localStorage.setItem('sb-session', JSON.stringify(data));
  return data;
}
```

## Kimlik Doğrulama (Auth)

```js
// Giriş
async function login(email, password) {
  const session = await sbAuth(email, password);
  BM.Storage.state.currentUser = session.user;
  BM.Storage.state.isCloud = true;
}

// Çıkış
async function logout() {
  await sbFetch('/auth/v1/logout', { method: 'POST' });
  localStorage.removeItem('sb-session');
  BM.Storage.state.currentUser = null;
  BM.Storage.state.isCloud = false;
}

// Oturum kontrolü
async function checkSession() {
  const session = JSON.parse(localStorage.getItem('sb-session') || '{}');
  if (!session.access_token) return false;
  
  try {
    const user = await sbFetch('/auth/v1/user');
    BM.Storage.state.currentUser = user;
    BM.Storage.state.isCloud = true;
    return true;
  } catch {
    localStorage.removeItem('sb-session');
    return false;
  }
}
```

## Row Level Security (RLS)

```sql
-- Her tablo için RLS politikası
ALTER TABLE hives ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Kullanıcı kendi kovanlarını görür"
ON hives FOR SELECT
USING (auth.uid() = user_id);

CREATE POLICY "Kullanıcı kendi kovanlarını ekler"
ON hives FOR INSERT
WITH CHECK (auth.uid() = user_id);

CREATE POLICY "Kullanıcı kendi kovanlarını günceller"
ON hives FOR UPDATE
USING (auth.uid() = user_id);

CREATE POLICY "Kullanıcı kendi kovanlarını siler"
ON hives FOR DELETE
USING (auth.uid() = user_id);
```

## Offline-First Strateji

```js
// Her yazma işlemi önce localStorage'a
async function saveHive(hive) {
  hive.user_id = BM.Storage.state.currentUser?.id;
  
  // 1. LocalStorage'a yaz (anlık, garantili)
  BM.Storage.state.hives.push(hive);
  localStorage.setItem('hives', JSON.stringify(BM.Storage.state.hives));
  
  // 2. UI güncelle (optimistic)
  renderHiveList();
  
  // 3. Cloud'a yaz (best-effort)
  if (BM.Storage.state.isCloud) {
    try {
      await sbFetch('/rest/v1/hives', {
        method: 'POST',
        body: JSON.stringify(hive)
      });
    } catch (err) {
      console.warn('Cloud sync ertelendi:', err.message);
    }
  }
}
```

## Rate Limiting

```js
// Debounce — arama, autosave
function debounce(fn, delay = 300) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
}

const searchHives = debounce(async (query) => {
  const results = await sbFetch(`/rest/v1/hives?name=ilike.*${query}*`);
  renderResults(results);
}, 300);
```
