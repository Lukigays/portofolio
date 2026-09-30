# 🚀 Panduan Deploy ke Vercel — Portofolio V5

Build lokal sudah terverifikasi berhasil (`npm run build` ✅).
Konfigurasi Vercel sudah termasuk di folder ini:
- **`vercel.json`** — rewrite semua route ke `/` (wajib, karena pakai React Router SPA)
- **Framework auto-detect** — Vite (Vercel otomatis menjalankan `npm install` + `npm run build`)

---

## Cara 1: Upload ZIP di Vercel Dashboard (paling gampang)

1. Buka [vercel.com](https://vercel.com) → login.
2. Klik **Add New… → Project** → tab **Deploy** → pilih/unggah file
   **`portofolio-v5-vercel.zip`** (upload zip langsung).
   - *Alternatif:* import dari GitHub repo `EkiZR/Portofolio_V5`.
3. Vercel otomatis mendeteksi **Vite** → biarkan default.
4. **WAJIB** — klik **Environment Variables** (muncul sebelum Build) lalu isi:

   | Name | Value |
   |---|---|
   | `VITE_SUPABASE_URL` | URL project Supabase Anda (contoh: `https://xxxx.supabase.co`) |
   | `VITE_SUPABASE_ANON_KEY` | anon key Supabase Anda (`eyJhbGciOi...`) |

   > Cari di: Dashboard Supabase → **Project Settings → API**.
   > Tanpa 2 variabel ini, website akan **blank/blank putih** karena `src/supabase.js` melempar error saat load.
5. Klik **Deploy** → tunggu build (± 1–2 menit) → selesai! 🎉
   URL Anda: `https://nama-project.vercel.app`

> Env var juga bisa ditambahkan nanti di **Settings → Environment Variables**
> (isi untuk scope **Production**, **Preview**, dan **Development**), lalu
> **Redeploy** project.

---

## Cara 2: CLI (terminal)

```bash
# dari folder project
npx vercel        # pertama kali: login + set project
npx vercel --prod # deploy production
```

Lalu set env var via CLI:
```bash
npx vercel env add VITE_SUPABASE_URL production preview development
npx vercel env add VITE_SUPABASE_ANON_KEY production preview development
npx vercel --prod
```

---

## Setelah Deploy

- Ganti domain custom (opsional): **Settings → Domains** (mis. `ekizr.com`).
- Google Site Verification (`google69971c601d2409b3.html`) sudah ikut di `public/`
  → tersedia otomatis di `https://domainanda/google69971c601d2409b3.html`.

## Catatan

- Zip ini **tidak** berisi `node_modules`, `.git`, atau `dist` — Vercel akan
  menginstall & build sendiri.
- `vercel.json` berisi rewrite SPA — **jangan dihapus**, kalau dihapus halaman
  `/portofolio`, `/about`, dll. akan 404 saat di-refresh.
