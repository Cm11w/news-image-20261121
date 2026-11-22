# QA Refresh — news-image-20261121 (independent, from scratch)

**Verdict: SIAP — no blockers.** Entry siap submit apa adanya.
QA dilakukan Minggu 22 Nov 2026 ~07:05 WIB oleh pemeriksa independen
(bukan pembangun entri), terhadap `entry.png` hasil refresh Sabtu malam.

## 1. Format

- File: `entry.png` — PNG valid (`file`: PNG image data, 1024x1024,
  8-bit/color RGB, non-interlaced; PIL: format PNG, size (1024, 1024),
  mode RGB).
- Ukuran: **144.097 byte** (< 1.048.576 byte / 1 MiB) — lolos.
- sha256: `ec48ea42568508cd88b865ca3c96b8b4ec37ddc302d836ae8856e2d5ec4ddae7`
  — sama dengan sha yang diklaim untuk entri hasil refresh.

## 2. Determinisme

- `draw_entry.py` dijalankan 2x ke direktori temp terpisah
  (`/tmp/qa1`, `/tmp/qa2`): kedua output sha256
  `ec48ea42...4ddae7`, **byte-identik** dengan `entry.png`.
- `main.ts` dengan `MAKEFUN_OUTPUT_DIR=/tmp/qa-out`: salinan
  `entry.png` sha256 `ec48ea42...4ddae7`, **byte-identik** dengan
  `entry.png` (dicek dengan `cmp`, identik).
- Script juga menggagalkan run bila ada teks overflow (cek
  `draw_wrapped`/batas kartu di `draw_entry.py`); kedua run sukses
  tanpa error — tidak ada teks yang meluber dari kartunya.

## 3. Visual (dibaca langsung dari entry.png 1024px + downscale ~300px + crop grid)

- Tanggal menonjol: "Saturday, November 21, 2026" huruf emas besar di
  masthead navy; subline "Top stories of the day - as reported on
  Saturday" di kanan atas masthead, terbaca jelas.
- Tidak ada teks terpotong, meluber keluar kartu, tumpang tindih, atau
  glyph rusak/hilang. Semua teks ASCII (script menolak non-ASCII).
- Kelima cerita terbaca lengkap dari gambar saja: 1 lead (WAR) +
  4 panel (MARKETS, DIPLOMACY, ENERGY, CRIME).
- Downscale ~300px: judul, tanggal, dan headline tiap kartu tetap
  terbaca; body mengecil seperti layaknya koran 1024px — wajar, bukan
  cacat.
- Perubahan refresh terlihat di gambar: kartu CRIME (Mexico) menggantikan
  Akvan, kartu ENERGY soal dua tanker Sabtu, angka Kryvyi Rih 60,
  footer tanpa IMD.

## 4. Klaim vs riset (`research-21nov.md` + bagian REFRESH)

Tanggal: `date -d 2026-11-21` = **Saturday** — cocok dengan gambar.

| Butir di gambar | Riset | Hasil |
|---|---|---|
| Masthead "Saturday, November 21, 2026" | 21 Nov 2026 = Sabtu | OK |
| Subline "Top stories of the day - as reported on Saturday" | REFRESH: subline diubah ke kalimat ini | OK |
| Lead: "Russia's biggest air attack on Ukraine this year" | §1: Zelensky menyebutnya "terbesar tahun ini" | OK (lihat catatan 1) |
| "110+ missiles and about 400 drones ... over 10 hours, Kyiv says" | §1: sedikitnya 110 rudal, ~400 drone, >10 jam | OK |
| "at least 9 killed, 28+ wounded" | §1: sedikitnya 9 tewas, 28+ luka (otoritas Ukraina) | OK |
| "Three Dnipro bridges in Kyiv were damaged; emergency blackouts hit Kyiv and the west" | §1: 3 jembatan Dnipro rusak; pemadaman darurat Kyiv + Lviv, Zakarpattia, Ivano-Frankivsk | OK |
| "Russian missiles also entered Polish airspace; Polish and NATO jets scrambled" | §1 | OK |
| "Kryvyi Rih ... killed a 7-year-old boy and a 20-year-old paramedic and wounded 60" | §1 (2 tewas: anak 7 th + paramedis 20 th) + REFRESH (42 → **60**, angka terbaru AP, Sabtu) | OK |
| MARKETS: "Nasdaq -5.28% to 22,617.73, its worst week since March 2020" | §2: Nasdaq -5,28% ke 22.617,73; minggu terburuk sejak Maret 2020 | OK |
| "S&P 500 -3.70% into correction" | §2: -3,70% ke 6.910,39, masuk koreksi teknis | OK |
| "Nvidia fell about 14% after Reuters reported an SEC accounting probe" | §2: ~14%; Reuters melaporkan SEC menyelidiki — atribusi Reuters dijaga | OK |
| DIPLOMACY: "The FT reports the US wants a Kyiv-Moscow deal by early January, before Democrats take Congress on Jan 3" | §3: FT, awal Januari, sebelum Demokrat ambil Kongres 3 Jan 2027 | OK |
| "Trump said Putin wants the war to end" | §3: pernyataan Trump, dikutip sebagai pernyataan | OK |
| ENERGY: "Two more tankers hit near Hormuz ... hit by unknown projectiles on Saturday, UKMTO said, a day after a first tanker caught fire there" | REFRESH: dua tanker lagi Sabtu pagi (UKMTO 215-26 05:00 UTC, 216-26 05:50 UTC), sehari setelah tanker pertama terbakar Jumat; pelaku tak disebut; klaim ranjau Iran tidak dimasukkan | OK (lihat catatan 2) |
| CRIME: "Fausto Isidro Meza Flores, 'El Chapo Isidro', was captured in Sinaloa with US intelligence help, AP said" | REFRESH: ditangkap di Guasave, Sinaloa, Jumat malam, bantuan intelijen AS; sumber AP | OK |
| "The violence that followed left 11 dead" | REFRESH: kekerasan menyusul menewaskan **sedikitnya 11** (7 kartel, 4 tentara), menurut Kemhan Meksiko | OK (lihat catatan 3) |
| Footer "Sources: Reuters - AP - CNN - Financial Times - UKMTO \| Reported Saturday, Nov 21, 2026" | REFRESH: IMD keluar dari footer; kelima sumber dipakai di kartu | OK (lihat catatan 4) |
| Tidak ada Akvan / IMD / angka Brent di gambar | REFRESH: Akvan keluar, Brent dihapus | OK |

## Catatan minor (bukan blocker, tidak perlu revisi sebelum submit)

1. Headline lead "biggest air attack ... this year" adalah sebutan
   Zelensky (via CNN), bukan fakta netral — tapi body kartu mengatribusikan
   angka-angkanya ke Kyiv, dan riset mendukung sebutan itu. Sama seperti
   versi pagi; dapat diterima.
2. Kartu ENERGY menulis kedua tanker Sabtu itu "leaving the Strait of
   Hormuz". Riset §4 mencatat tanker Jumat "berlayar keluar dari Selat
   Hormuz", tetapi bagian REFRESH tidak mencatat arah pelayaran kedua
   tanker Sabtu — detail "leaving" untuk pasangan Sabtu tidak tertelusur
   di file riset. Risiko rendah (konsisten dengan pola Jumat), tapi
   secara ketat tidak terdokumentasi di `research-21nov.md`.
3. Kartu CRIME menulis "left 11 dead", sementara REFRESH menulis
   "sedikitnya 11 orang" — kualifikasi "at least" hilang. Angka 11
   sendiri benar; penyajian tanpa "at least" sedikit lebih tegas dari
   sumber.
4. KyivPost tidak tercantum di footer, padahal detail korban Kryvyi Rih
   (anak 7 th, paramedis 20 th) awalnya dari KyivPost. Namun angka
   terbaru (60 luka) adalah laporan AP Sabtu yang tercantum di footer,
   dan CNN juga meliput serangan utama — atribusi sudah memadai.

## Yang TIDAK dilakukan (sesuai tugas)

Tidak menjalankan kit check, tidak membuat bundle/transkrip, tidak
membuat repo, tidak push/submit apa pun. Hanya membaca file, menjalankan
`draw_entry.py` (2x ke /tmp) dan `main.ts` (ke /tmp/qa-out), dan menulis
laporan ini.
