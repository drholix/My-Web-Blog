# aliefk.dev — Hugo Bootstrap Blueprint (ID/EN)

Repositori ini menyiapkan situs statis **Hugo + Hugo Bootstrap (HBS)** dengan konten dwibahasa (Indonesia & Inggris), siap deploy di **Netlify** dan diamankan oleh **Cloudflare**. Seluruh panduan di bawah berfungsi sebagai _runbook_ QA + DevOps: mulai dari setup lokal, konfigurasi inti, alur konten, hingga checklist produksi.

---

## 1. Prasyarat & Lingkungan

| Komponen | Versi minimum | Catatan |
| --- | --- | --- |
| Hugo Extended | `0.152.2` | Pastikan `hugo version` menampilkan "Extended". |
| Node.js / npm | Node `18.x` / npm `9.x` | Opsional; dipakai bila ada automasi tambahan. |
| Git | `>=2.40` | Untuk clone & deploy. |
| Akses Netlify & Cloudflare | Free Plan | Netlify untuk hosting, Cloudflare sebagai proxy & DNS. |

Tambahan rekomendasi: editor dengan dukungan Markdown (VS Code), serta akun GitHub untuk CI.

---

## 2. Setup Cepat (Lokal)

```bash
# 1. Clone repositori
git clone https://github.com/<username>/aliefk.dev.git
cd aliefk.dev

# 2. Sinkronisasi modul tema HBS
hugo mod get

# 3. (Opsional) pasang dependensi tambahan
npm install

# 4. Verifikasi versi Hugo
hugo version

# 5. Jalankan server pengembangan dengan konten draft
hugo server -D
```

> Server lokal berjalan di `http://localhost:1313`. Gunakan `Ctrl+C` untuk menghentikan.

---

## 3. Konfigurasi Inti

File konfigurasi berada di `config/_default/` dan `hugo.toml`.

### 3.1 `hugo.toml`

```toml
baseURL = "https://aliefk.dev/"
title = "Alief Kurniawan — Blue Team Notes"
languageCode = "id"
paginate = 10
defaultContentLanguage = "id"
defaultContentLanguageInSubdir = false
enableRobotsTXT = true

theme = ["github.com/razonyang/hugo-theme-bootstrap"]

[sitemap]
  changefreq = "weekly"
  priority = 0.5
  filename = "sitemap.xml"

[taxonomies]
  category = "categories"
  tag = "tags"

[permalinks]
  posts = "/blog/:year/:month/:slug/"
  portfolio = "/portfolio/:slug/"

[outputs]
  home = ["HTML", "RSS", "JSON"]
  section = ["HTML", "RSS"]
  taxonomy = ["HTML"]
  term = ["HTML"]

[languages]
  [languages.id]
    languageName = "Bahasa Indonesia"
    title = "Alief Kurniawan — Catatan Blue Team"
    weight = 1
  [languages.en]
    languageName = "English"
    title = "Alief Kurniawan — Blue Team Notes"
    weight = 2

[minify]
  [minify.tdewolff]
    [minify.tdewolff.css]
      inlineStyles = "minify"
    [minify.tdewolff.html]
      keepComments = false
    [minify.tdewolff.js]
      keepVarNames = false

[imaging]
  anchor = "smart"
  quality = 85

[markup]
  [markup.highlight]
    noClasses = false
    style = "monokai"
    guessSyntax = true
  [markup.goldmark.renderer]
    unsafe = true
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 3
```

### 3.2 `config/_default/menu.toml`

```toml
[[main]]
  identifier = "blog"
  name = "Blog"
  url = "/"
  weight = 1
[[main]]
  identifier = "portfolio"
  name = "Portfolio"
  url = "/portfolio/"
  weight = 2
[[main]]
  identifier = "tags"
  name = "Tags"
  url = "/tags/"
  weight = 3
[[main]]
  identifier = "archive"
  name = "Archive"
  url = "/archives/"
  weight = 4
[[main]]
  identifier = "about"
  name = "About"
  url = "/about/"
  weight = 5
[[main]]
  identifier = "contact"
  name = "Contact"
  url = "/contact/"
  weight = 6
```

> Untuk menu versi Indonesia gunakan `config/_default/menu.id.toml` dengan terjemahan setara.

### 3.3 `config/_default/params.toml`

- Metadata penulis (`[author]`), deskripsi situs, kata kunci.
- Pengaturan UI HBS: toggle mode (`[color]`), switcher ukuran font (`[fontSize]`).
- Integrasi Cloudflare Analytics & Turnstile (`[analytics]`, `[security.turnstile]`).
- Pengendali PWA (`[pwa]`) dan OG default (`[opengraph]`).

Pastikan nilai sensitif (Turnstile sitekey) diisi via variabel lingkungan sebelum build produksi.

### 3.4 Referensi Deskripsi & Keywords

| Halaman | Bahasa | Meta Description | Keywords |
| --- | --- | --- | --- |
| Home | ID/EN | Catatan Blue Team dan portofolio Alief Kurniawan berbasis Depok. | `Blue Team blog`, `SOC playbooks`, `Threat hunting`, `Incident response portfolio` |
| Blog | ID/EN | Artikel SOC automation, incident response, threat hunting, malware triage. | `SOC blog`, `Incident response articles`, `Threat hunting guides`, `Malware analysis notes` |
| Portfolio | ID/EN | Proyek ThreatLens, Wazuh Lab, Sigma Rules, OCR pipeline, laporan DGA. | `SOC portfolio`, `ThreatLens project`, `Wazuh lab`, `Sigma rules`, `OCR pipeline` |
| About | ID/EN | Profil profesional Alief "Awan" Kurniawan dan fokus Blue Team. | `Alief Kurniawan`, `Blue Team`, `SOC analyst`, `Threat hunting` |
| Contact | ID/EN | Form kolaborasi SOC/Blue Team dengan proteksi Turnstile. | `Contact Alief Kurniawan`, `SOC consulting`, `Blue team collaboration` |

---

## 4. Struktur Konten & Penulisan

```
content/
├── id/
│   ├── posts/
│   ├── portfolio/
│   ├── about/
│   └── contact/
└── en/
    ├── posts/
    ├── portfolio/
    ├── about/
    └── contact/
```

### 4.1 Membuat Post Baru

```bash
# Bahasa Indonesia
hugo new posts/nama-post/index.md

# Bahasa Inggris (mirror)
hugo new --lang en posts/post-name/index.md
```

Isi front matter berikut pada masing-masing `index.md`:

```toml
+++
title = "Judul / Title"
date = 2024-06-01T08:00:00+07:00
summary = "Ringkasan singkat"
description = "Deskripsi SEO ±150 karakter"
tags = ["SIEM", "Incident Response"]
categories = ["Operations"]
cover = "cover.webp"
featured = true # opsional
+++
```

Tambahkan konten minimal tiga paragraf, sisipkan kode/shortcode (`alert`, `iframe`, `processed-image`) bila diperlukan. Letakkan gambar dalam folder bundle yang sama dan gunakan shortcode untuk menghasilkan WebP:

```markdown
{{< processed-image src="cover.webp" width="960" alt="SIEM Dashboard" caption="Optimized via Hugo Pipes" >}}
```

### 4.2 About & Portfolio

- Halaman About (`content/*/about/_index.md`) memuat bio profesional Alief "Awan" Kurniawan.
- Setiap item portofolio berada di `content/*/portfolio/<slug>/` dengan `cover.svg/webp`, summary, dan tanggal.

---

## 5. Build & Deploy Netlify

### 5.1 Perintah Build

```bash
# Build produksi dengan garbage collection dan minify
hugo --gc --minify

# Periksa ukuran output
du -sh public/
```

### 5.2 Konfigurasi Netlify

- **Repository**: hubungkan GitHub → Netlify `Add new site` → `Import from Git`.
- **Build command**: `npm install && hugo --minify` (opsional npm jika diperlukan).
- **Publish directory**: `public`.
- **Environment variables**:
  - `HUGO_VERSION=0.152.2`
  - `HUGO_ENABLEGITINFO=true`
  - `TURNSTILE_SITE_KEY`, `TURNSTILE_SECRET_KEY` (opsional).

### 5.3 `netlify.toml`

```toml
[build]
  publish = "public"

[build.environment]
  HUGO_VERSION = "0.152.2"
  HUGO_ENABLEGITINFO = "true"

[context.production]
  command = "npm install && hugo --minify"

[[redirects]]
  from = "https://www.aliefk.dev/*"
  to   = "https://aliefk.dev/:splat"
  status = 301
  force  = true

[[headers]]
  for = "/*"
  [headers.values]
    Referrer-Policy = "strict-origin-when-cross-origin"
    X-Content-Type-Options = "nosniff"
    X-Frame-Options = "DENY"
    Permissions-Policy = "accelerometer=(), camera=(), geolocation=(), gyroscope=(), microphone=()"
    Strict-Transport-Security = "max-age=63072000; includeSubDomains; preload"
    Content-Security-Policy = "default-src 'self'; img-src 'self' data: https:; style-src 'self' 'unsafe-inline'; script-src 'self' https://static.cloudflareinsights.com https://challenges.cloudflare.com https://giscus.app; connect-src 'self' https://cloudflareinsights.com; font-src 'self' data:; frame-src 'self' https://challenges.cloudflare.com https://giscus.app; object-src 'none'; base-uri 'self'; frame-ancestors 'none'; form-action 'self';"
```

Tambahkan blok header tambahan untuk `sw.js`, `manifest.webmanifest`, dan `offline.html` bila menggunakan mode offline.

---

## 6. Integrasi Cloudflare

1. **DNS**: arahkan domain apex (`aliefk.dev`) sebagai flattened CNAME → `apex-loadbalancer.netlify.com`; subdomain `www` → `<site>.netlify.app`.
2. Aktifkan **Proxy (🟠)**, **SSL/TLS mode: Full**, **Always Use HTTPS**, **Auto Minify** (nonaktifkan untuk HTML karena sudah dilakukan Hugo).
3. **Security**: Bot Fight Mode, WAF ruleset bawaan, Rate Limit `/contact/*` bila diperlukan.
4. **Analytics**: dapatkan token Cloudflare Web Analytics → isi `params.analytics.cloudflareToken`.
5. **Turnstile**: buat site key/secret → isi pada params atau environment Netlify.

---

## 7. Pengujian Manual & Validasi

Lakukan regresi berikut setelah setiap perubahan besar.

1. **Navigasi & UI**: cek menu Blog/Portfolio/Tags/Archive/About/Contact, toggle Light/Dark/Auto, switcher font XS–XL.
2. **i18n**: pastikan `/` (ID) dan `/en/` memuat konten serupa, tautan `hreflang` & canonical benar.
3. **Pagefind/Search**: jika diaktifkan, lakukan pencarian kata kunci populer.
4. **Konten**: pastikan featured & recent post muncul di beranda; archive per tahun menampilkan daftar.
5. **SEO**: gunakan [Google Rich Results Test](https://search.google.com/test/rich-results) untuk JSON-LD, cek `/index.xml`, `sitemap.xml`, dan `robots.txt`.
6. **Security Headers**: periksa via DevTools → Network → Headers atau [Security Headers](https://securityheaders.com/).
7. **Performance**: jalankan Lighthouse (mobile & desktop) dan targetkan skor ≥90.
8. **Offline**: aktifkan service worker di build produksi, matikan koneksi, akses `/offline.html`.
9. **Netlify Logs**: pastikan build `hugo --gc --minify` berhasil tanpa error.

---

## 8. Test Matrix

| Area | Langkah | Perintah/Alat | Expected Result | Status |
| --- | --- | --- | --- | --- |
| Local Dev | Jalankan server | `hugo server -D` | Situs lokal tersedia, tanpa error di terminal | ☐ |
| i18n | Akses `/` & `/en/` | Browser manual | Konten sinkron, switch bahasa bekerja | ☐ |
| Search | Cari "SOC" | UI Pagefind | Hasil relevan muncul | ☐ |
| Build | Produksi | `hugo --gc --minify` | Build sukses, `public/` < 5 MB | ☐ |
| Links | Link checker | `npx broken-link-checker http://localhost:1313` | 0 link rusak | ☐ |
| RSS | Validasi feed | `curl -I http://localhost:1313/index.xml` | HTTP 200 + `application/rss+xml` | ☐ |
| Security | Header audit | securityheaders.com | Nilai ≥ B+ | ☐ |
| SEO | Rich results | Google Rich Results Test | JSON-LD valid | ☐ |
| Performance | Lighthouse Mobile | `npx @lhci/cli autorun` | Skor ≥ 90 semua kategori | ☐ |
| Forms | Kirim kontak | Netlify dashboard | Entri baru muncul, Turnstile valid | ☐ |

---

## 9. Checklist QA Produksi

- [ ] Menu utama (Blog, Portfolio, Tags, Archive, About, Contact) tersedia di ID & EN.
- [ ] Toggle Light/Dark/Auto dan font XS–XL berfungsi.
- [ ] Konten ID & EN memiliki canonical + hreflang yang benar.
- [ ] Pagefind/Search menampilkan hasil.
- [ ] `/index.xml`, `sitemap.xml`, `robots.txt`, `manifest.webmanifest`, dan `/offline.html` dapat diakses.
- [ ] JSON-LD (`Person`, `BlogPosting`, `BreadcrumbList`) lolos validasi.
- [ ] Security headers (CSP, HSTS, Referrer-Policy, Permissions-Policy, X-Content-Type-Options, X-Frame-Options) aktif.
- [ ] Lighthouse (desktop & mobile) menunjukkan skor ≥ 90 untuk Performance, Accessibility, Best Practices, SEO.
- [ ] Netlify build `npm install && hugo --minify` selesai tanpa error.
- [ ] Cloudflare proxy + Bot Fight Mode + WAF aktif tanpa konflik CSP.

---

## 10. Monitoring & Keamanan Berkelanjutan

- **Uptime**: daftarkan URL produksi di UptimeRobot (interval 5 menit).
- **Analytics**: pantau Cloudflare Web Analytics & Google Search Console.
- **Backup**: aktifkan Netlify Deploy Log & simpan `deploy.zip` penting.
- **Audit triwulan**: review CSP (mode report → enforce), perbarui dependensi, audit akses GitHub/Netlify/Cloudflare (2FA wajib).

---

## 11. Troubleshooting

| Gejala | Penyebab Umum | Solusi |
| --- | --- | --- |
| Build gagal karena tema | Modul belum tersinkron | Jalankan `hugo mod get` atau `hugo mod tidy`. |
| Turnstile tidak muncul | Site key kosong | Isi `params.security.turnstile.siteKey` atau env var. |
| CSP block Cloudflare Analytics | `script-src` kurang domain | Tambahkan `https://static.cloudflareinsights.com` ke CSP. |
| Lighthouse skor rendah | Gambar terlalu besar / font eksternal | Optimasi WebP & self-host fonts. |
| Hreflang error | URL canonical belum sinkron | Pastikan `rel="alternate"` di partial SEO memuat path benar. |

---

## 12. Otomasi Tambahan (Opsional)

### 12.1 Konfigurasi LHCI (`lighthouserc.json`)

```json
{
  "ci": {
    "collect": {
      "staticDistDir": "public",
      "numberOfRuns": 3
    },
    "assert": {
      "assertions": {
        "categories:performance": ["error", {"minScore": 0.9}],
        "categories:accessibility": ["error", {"minScore": 0.9}],
        "categories:best-practices": ["error", {"minScore": 0.9}],
        "categories:seo": ["error", {"minScore": 0.9}]
      }
    },
    "upload": {
      "target": "temporary-public-storage"
    }
  }
}
```

### 12.2 GitHub Actions (`.github/workflows/lighthouse.yml`)

```yaml
name: Lighthouse CI

on:
  pull_request:
  push:
    branches: ["main"]

jobs:
  lhci:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: "18"
      - name: Install dependencies
        run: npm install -g @lhci/cli
      - name: Build site
        run: hugo --gc --minify
      - name: Run Lighthouse CI
        run: lhci autorun
```

### 12.3 Template Issue & PR

`.github/ISSUE_TEMPLATE.md`
```markdown
## Ringkasan

## Langkah Reproduksi / Konteks

## Checklist
- [ ] Sudah dicek di branch terbaru
- [ ] Tersedia log/error terkait
- [ ] Dampak ke produksi dijelaskan
```

`.github/pull_request_template.md`
```markdown
## Ringkasan
- [ ] Perubahan sudah diuji lokal (`hugo --gc --minify`)
- [ ] Dokumentasi/README diperbarui
- [ ] Security headers & Lighthouse tetap ≥ 90

## Detail Perubahan

## Screenshot / Bukti (opsional)
```

---

## 13. Lisensi & Atribusi

- Kode dalam repositori ini berada di bawah lisensi MIT (lihat `LICENSE`).
- Tema: [Hugo Theme Bootstrap](https://hbs.razonyang.com/).
- Ikon/gambar mengikuti lisensi masing-masing sumber.

Selamat membangun pusat knowledge Blue Team Anda! 🚀
