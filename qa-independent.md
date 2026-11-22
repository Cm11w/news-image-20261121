# QA Independen — news-image-20261121

**QA oleh:** subagent QA independen (tidak ikut membangun entri; verifikasi dari nol)
**Tanggal QA:** Sabtu, 21 Nov 2026 ~09:26–09:30 WIB
**Entri:** `~/workspace/makefun/news-image-20261121-entry/`
**File yang diperiksa:** `entry.png`, `draw_entry.py`, `main.ts`, `research-21nov.md`, `README.md`

---

## Verdict keseluruhan: SIAP (dengan satu blokir submit di luar gambar)

Gambar lolos semua pemeriksaan format, visual, determinisme, dan kecocokan
fakta-vs-riset. **Tidak ada perbaikan gambar yang diperlukan.**

Satu-satunya hal yang belum siap adalah **bukan gambarnya, melainkan
kelengkapan submit**: kit check gagal di `transcripts_present` (tidak ada
transkrip/bundle yang diunggah) dan repo belum ada di GitHub. Itu urusan
parent saat submit — QA ini sengaja tidak membuat bundle/transkrip palsu,
tidak membuat repo, tidak push, dan tidak submit.

---

## 1. Format — PASS (semua item)

| Item | Hasil |
|---|---|
| File PNG valid | PASS — `file` melaporkan `PNG image data, 1024 x 1024, 8-bit/color RGB, non-interlaced` |
| Dimensi 1024x1024 | PASS — dikonfirmasi `file` dan PIL (`(1024, 1024) RGB`) |
| Ukuran < 1.048.576 byte | PASS — **149.443 byte** (~14% dari batas 1 MiB) |
| sha256 `entry.png` | `4d1f78f5e1db61b9d195f135c153f35250ca4cad1fcac0615b54f783d9369691` |
| Determinisme `draw_entry.py` | PASS — dijalankan 2x (ke `/tmp/qa_run1` dan `/tmp/qa_run2`); kedua sha256 **identik** dengan `entry.png` yang tersimpan |
| `main.ts` (Node v24.22.1, `MAKEFUN_OUTPUT_DIR=/tmp/out21qa`) | PASS — menyalin `entry.png` byte-identik; sha256 output = `4d1f78f5...9369691`, sama dengan `entry.png` |
| Tanggal "Saturday, November 21, 2026" | PASS — diverifikasi dengan `date -d`: 2026-11-21 memang **Saturday** (WIB maupun UTC); 2026-11-20 adalah Friday, sesuai subline masthead |

---

## 2. Visual — PASS

Diperiksa langsung dari render penuh 1024px, plus downscale 512px dan 300px.

| Item | Hasil |
|---|---|
| Tanggal menonjol | PASS — "Saturday, November 21, 2026" dalam huruf besar tebal warna emas di masthead navy, langsung di bawah "WORLD NEWS" |
| Semua teks terbaca, tidak terpotong/meluber | PASS — semua kartu punya margin bersih; tidak ada teks yang keluar kartu atau terpotong di tepi. `draw_entry.py` juga menggagalkan run bila ada teks overflow (bukan menggambar di luar kotak) |
| Tumpang tindih | PASS — tidak ada teks yang saling menumpuk di 1024px maupun 512px |
| Teks garbled / kotak kosong (missing glyph) | PASS — tidak ada kotak tofu atau karakter rusak; semua teks ASCII (skrip menolak karakter non-ASCII) |
| 5 cerita jelas dari gambar saja | PASS — lead WAR-Ukraine (serangan udara terbesar), MARKETS (Wall Street anjlok), DIPLOMACY (Trump dorong damai Januari), ENERGY (tanker Hormuz terbakar), WEATHER (Siklon Akvan). Masing-masing punya tag warna, judul, dan isi yang berdiri sendiri |
| Artefak | PASS — tidak ada artefak, garis aneh, atau blok warna yang salah tempat |

Catatan kecil (bukan kegagalan): pada downscale 300px, teks isi kartu menjadi
sangat kecil (wajar untuk infografik 1024px) — judul dan tag tetap terbaca.
Pada 512px semua teks terbaca dengan jelas. Tidak ada tindakan yang diperlukan.

---

## 3. Klaim vs riset — PASS (semua item terperiksa cocok)

Setiap angka/nama/fakta di gambar dicocokkan dengan `research-21nov.md`.
Format angka di gambar memakai gaya Inggris (titik desimal, koma ribuan),
sama nilainya dengan gaya Indonesia di riset.

| # | Klaim di gambar | Riset | Hasil |
|---|---|---|---|
| 1 | "Saturday, November 21, 2026" | Riset bertanggal 21 Nov 2026; 21 Nov 2026 = Sabtu (diverifikasi `date`) | PASS |
| 2 | "Morning snapshot - most events took place Friday, Nov 20" | Riset menegaskan sebagian besar peristiwa terjadi Jumat 20 Nov malam dan baru dilaporkan pagi 21 Nov; riset merekomendasikan judul jujur seperti ini | PASS |
| 3 | "110+ missiles and about 400 drones" | "sedikitnya 110 rudal (27 di antaranya balistik) dan sekitar 400 drone" | PASS |
| 4 | "strike lasting over 10 hours" | "serangan yang berlangsung lebih dari 10 jam" | PASS |
| 5 | "at least 9 killed, 28+ wounded" | "Sedikitnya 9 orang tewas dan sedikitnya 28 terluka, menurut otoritas Ukraina" | PASS |
| 6 | "Three Dnipro bridges in Kyiv were damaged" | "Tiga jembatan di atas Sungai Dnipro di Kyiv rusak" | PASS |
| 7 | "emergency blackouts hit Kyiv and the west" | "pemadaman darurat diberlakukan di Kyiv dan wilayah Lviv, Zakarpattia, Ivano-Frankivsk" (wilayah barat Ukraina) — ringkasan "the west" wajar | PASS |
| 8 | "Russian missiles also entered Polish airspace; Polish and NATO jets scrambled" | "Rudal Rusia juga melanggar wilayah udara Polandia; jet tempur Polandia dan NATO dikerahkan dan sistem Patriot diaktifkan" | PASS |
| 9 | "A later strike on Kryvyi Rih killed a 7-year-old boy and a 20-year-old paramedic and wounded 42" | "2 tewas — anak laki-laki 7 tahun dan paramedis perempuan 20 tahun — dan 42 terluka" (KyivPost, terbit 21 Nov 05:09 waktu Kyiv) | PASS |
| 10 | "Nasdaq -5.28% to 22,617.73, its worst week since March 2020" | "Nasdaq Composite anjlok 5,28% ke 22.617,73 — ... minggu terburuknya sejak Maret 2020" | PASS |
| 11 | "S&P 500 -3.70% into correction" | "S&P 500 turun 3,70% ke 6.910,39 — masuk koreksi teknis" | PASS |
| 12 | "Nvidia fell about 14% after Reuters reported an SEC accounting probe" | "Nvidia anjlok ~14% ... Pemicu langsung: Reuters melaporkan SEC sedang menyelidiki praktik akuntansi Nvidia" — atribusi Reuters dipertahankan, tidak disajikan sebagai fakta final SEC | PASS |
| 13 | "The FT reports the US wants a Kyiv-Moscow deal by early January, before Democrats take Congress on Jan 3" | "FT ... melaporkan ... menginginkan kesepakatan damai Kyiv–Moskow tercapai pada awal Januari 2027, sebelum Demokrat mengambil alih Kongres (3 Januari 2027)" — atribusi FT dipertahankan, tidak disajikan sebagai kesepakatan | PASS |
| 14 | "Trump said Putin wants the war to end" | Trump mengatakan Putin "dengan jelas menyatakan keinginannya melihat perang berakhir melalui jalur diplomatik" — disajikan sebagai pernyataan Trump, bukan fakta terverifikasi | PASS |
| 15 | "A tanker leaving the Strait of Hormuz was hit by an unknown projectile and caught fire, UKMTO said" | "sebuah tanker yang berlayar keluar dari Selat Hormuz dihantam proyektil tak dikenal ... menurut UKMTO" — tidak ada pelaku yang disebut | PASS |
| 16 | "Brent rose 0.6% to $92.57 a barrel" | "minyak Brent naik 0,6% ke $92,57/barel" | PASS |
| 17 | "Akvan made landfall near Gopalpur, Odisha, with winds of 60-70 km/h" | "melintasi pesisir dekat Gopalpur, distrik Ganjam, Odisha ... angin 60–70 km/jam" | PASS |
| 18 | "About 370,000 evacuated; no deaths reported" | "Odisha mengevakuasi sekitar 370.000 orang (angka kepala sekretaris negara bagian; media lokal menyebut 4,40 lakh = 440.000)" dan "tidak ada laporan kematian" (pernyataan pejabat negara bagian) — gambar memakai angka 370.000 dengan kata "About"; ini angka resmi negara bagian dan konsisten dengan saran riset memakai satu angka dengan atribusi implisit | PASS |
| 19 | Footer "Sources: Reuters - AP - CNN - Financial Times - IMD - UKMTO" | Semua enam sumber memang dipakai di riset (Reuters, AP, CNN, FT, buletin IMD, UKMTO) | PASS |

**Ketidakcocokan: tidak ada.** Tidak ada angka salah, atribusi hilang, fakta di
luar riset, atau tanggal keliru.

Dua nuansa kecil (bukan kesalahan, dicatat demi kejujuran):
- Kicker lead "Kyiv - reported Saturday morning": serangan utama dilaporkan
  Jumat 20 Nov; yang benar-benar bertanggal 21 Nov hanyalah laporan final
  korban Kryvyi Rih (05:09 waktu Kyiv). Namun subline masthead sudah
  menjelaskan bahwa sebagian besar peristiwa terjadi Jumat 20 Nov, dan riset
  sendiri menyebut gambar ini "snapshot pagi" — jadi frasa ini dapat dibaca
  sebagai "dilaporkan pada snapshot Sabtu pagi". Tidak perlu diubah.
- Gambar menyebut paramedis "20-year-old" tanpa kata "perempuan" seperti di
  riset; ini bukan kesalahan faktual, hanya detail yang dihilangkan.

---

## 4. Kit check FRESH — hasil (bukan PASS penuh; blokir ada di sisi submit)

Perintah (tanpa `--transcripts`, sesuai instruksi):
`node cli/makefun.mjs check --kit . --repo ~/workspace/makefun/news-image-20261121-entry`
dari kit `~/workspace/makefun/news-image-20261121-kit/news-image-20261121-kit/`

**Percobaan pertama (tanpa `--worktree`):** check menolak jalan — "is not in a
git repository: run check inside your repository, name it with --repo, or
pass --worktree to check the files as they are". Kit sendiri memverifikasi
11 file ("kit news-image-20261121 dev: verified 11 files").

**Percobaan kedua (dengan `--worktree`, opsi yang disarankan CLI):** check
berjalan penuh atas file apa adanya. Hasil: **4 passed, 1 failed,
14 skipped, 5 checked at submission; exit 1 — "not ready: fix
transcripts_present, then check again".**

| Check | Hasil | Keterangan |
|---|---|---|
| `competition_open` | pass | Sekarang (21 Nov 02:26 UTC) berada antara pembukaan 2026-11-21T00:00:00Z dan deadline 2026-11-23T00:00:00Z |
| `snapshot` | pass | 6 file, 181.217 byte — dalam batas intake |
| `license_osi` | pass | LICENSE menyatakan MIT, OSI-approved |
| `entrypoint` | pass | `main.ts` di root memilih node22, diterima kompetisi ini |
| `strategy_note` | skip | Kompetisi tidak meminta strategy note |
| `committed_secret` | skip | Tidak ada `--dotenv` diberikan |
| `transcripts_present` | **FAIL** | **Tidak ada transkrip yang diunggah** — kompetisi ini mewajibkan transkrip. Perlu bundle sesi agen yang membangun entri (`makefun bundle ... --out transcripts.tar.gz`) lalu `check --transcripts <bundle>`. QA tidak membuat bundle/transkrip apa pun (dilarang oleh tugas) |
| `transcripts_recorded`, `thinking_wellformed`, `thinking_in_window`, `thinking_committed`, `thinking_reproduces`, `thinking_on_task`, `thinking_turns`, `thinking_priced`, `thinking_revised`, `thinking_fresh`, `transcripts_run_record`, `thinking_own_work` | skip (12) | Tidak ada sesi transkrip untuk diperiksa — konsekuensi dari `transcripts_present` |
| `repo_public` | at submission | Site membaca repo dari GitHub saat submit: repo harus publik saat itu |
| `repo_owner` | at submission | Owner GitHub harus login akun, atau commit membawa `.makefun/owner.json` dengan wallet |
| `repo_created_after_open` | at submission | Repo GitHub harus dibuat pada/after 2026-11-21T00:00:00Z (pembukaan) |
| `commit_in_repo` | at submission | Commit yang disubmit harus sudah di-push ke branch repo |
| `duplicate_snapshot` | at submission | File harus berbeda dari entri akun lain yang lebih dulu |

Catatan kit: "grading is the server's, not check's: there is no local grade
of this competition, the server grades every entry."

**Artinya:** semua yang bisa diperiksa secara lokal tanpa repo GitHub dan
tanpa transkrip sudah lolos. Blokir yang tersisa adalah proses submit
(transkrip + repo GitHub publik yang dibuat setelah pembukaan + owner/wallet),
bukan isi gambarnya.

---

## 5. Daftar perbaikan yang masih diperlukan

**Untuk gambar (`entry.png`): tidak ada.**

**Untuk submit (urusan parent, di luar gambar):**
1. Bundle transkrip sesi pembangunan yang sebenarnya (jangan buat/palsukan)
   dan jalankan ulang kit check dengan `--transcripts <bundle>` sebelum
   deadline **2026-11-23T00:00:00Z**.
2. Buat repo GitHub publik baru (setelah 2026-11-21T00:00:00Z), push entri,
   dan pastikan owner/wallet sesuai aturan (`repo_owner`).
3. Perhatian riset: riset ini adalah snapshot pagi 21 Nov (~02:15–02:30 UTC)
   dan riset sendiri merekomendasikan refresh sore/malam — bila ada peristiwa
   besar siang 21 Nov, Cerita 4/5 bisa tergeser. Keputusan refresh/pertahankan
   ada di parent; gambar saat ini akurat terhadap riset yang ada.

---

## Ringkasan angka kunci

- `entry.png`: 1024x1024, 149.443 byte, sha256
  `4d1f78f5e1db61b9d195f135c153f35250ca4cad1fcac0615b54f783d9369691`
- Determinisme: 2 run `draw_entry.py` + 1 run `main.ts` → sha256 identik
- Kit check: 4 pass / 1 fail (`transcripts_present`) / 14 skip / 5 at-submission
- Klaim vs riset: 19/19 cocok, 0 ketidakcocokan
