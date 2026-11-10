# Template Tesis Magister (S2) IPB University

[![LaTeX](https://img.shields.io/badge/LaTeX-LuaLaTeX-blue.svg)](https://www.latex-project.org/)
[![Tectonic](https://img.shields.io/badge/Tectonic-supported-blueviolet.svg)](https://tectonic-typesetting.github.io/)
[![TeX Live](https://img.shields.io/badge/TeX%20Live-2024%2B-green.svg)](https://tug.org/texlive/)
[![MiKTeX](https://img.shields.io/badge/MiKTeX-supported-brightgreen.svg)](https://miktex.org/)
[![GitHub Stars](https://img.shields.io/github/stars/nicabisha/ipb-masters-thesis-latex)](https://github.com/nicabisha/ipb-masters-thesis-latex/stargazers)

Template LaTeX untuk penulisan **tesis magister (S-2)** di Institut Pertanian
Bogor (IPB University). Template ini mengikuti **Pedoman Penyajian Tugas Akhir
(PPTA) IPB 2026** dan templat Word resmi `format tesis terbaru.docx`. Margin,
font, penomoran, caption, bagian awal, dan format sitasi telah disesuaikan
dengan acuan terbaru tersebut.

Template ini merupakan adaptasi mandiri dan bukan produk resmi IPB
University. Jika terdapat perbedaan, pedoman dan templat resmi yang berlaku
menjadi acuan utama.

Template ini adalah port program magister dari
[raihanpka/ipb-thesis-latex](https://github.com/raihanpka/ipb-thesis-latex)
(template S1). Kredit dan lisensi upstream dipertahankan; lihat
[Kredit dan Atribusi](#kredit-dan-atribusi).

## Perbedaan utama dengan template S1

| Aspek | S1 | S2 (repositori ini) |
|---|---|---|
| halaman pernyataan | "skripsi" | "tesis" dan gelar magister |
| abstrak | `ABSTRAK`/`ABSTRACT`, satu paragraf | `RINGKASAN`/`SUMMARY`, beberapa paragraf, maksimum dua halaman |
| abstrak grafis | `ABSTRAK GRAFIS` | `RINGKASAN VISUAL` dengan kotak placeholder netral |
| jumlah pembimbing | dua | dua (bawaan) atau tiga, diatur satu sakelar |
| pejabat pengesahan | dua pejabat | Ketua Program Studi dan Dekan Fakultas/Sekolah |
| riwayat hidup | riwayat S-1 | riwayat S-2, pekerjaan, dan publikasi |

## Memulai

1. **Fork** repositori ini di GitHub ke akun Anda.
2. **Clone** fork Anda ke komputer lokal.
3. **Isi** data Anda di `src/config/information.tex` (nama, NIM, judul,
   pembimbing, program studi, dan sebagainya).
4. **Ganti** teks panduan pada `src/preliminaries/`, `src/ringkasan/`,
   `src/chapters/`, dan `src/backmatter/` dengan isi tesis Anda.
5. **Build** PDF dengan `make` (lihat [Penggunaan](#penggunaan)).

## Kebutuhan

Template ini mendukung compiler modern **Tectonic** (ringan, mengunduh paket
secara otomatis) maupun distribusi LaTeX lengkap dengan **LuaLaTeX**,
`latexmk`, `biber`, dan paket-paket yang tercantum dalam
`src/config/ipb-thesis.sty`. `chktex` diperlukan untuk validasi.

- **Tectonic** (lintas platform, sangat direkomendasikan: instalasi ringan,
  paket diunduh otomatis)
- **macOS**: Tectonic, BasicTeX, atau MacTeX
- **Windows**: Tectonic, MiKTeX, atau TeX Live
- **Linux**: Tectonic atau TeX Live (`texlive-full` atau `texlive-latex-extra`)

Detail instalasi per platform tersedia di [GUIDE.md](GUIDE.md).

## Penggunaan

Linux atau macOS:

```
make              Build PDF (otomatis memilih compiler)
make build        Build PDF (dapat ditambah ENGINE=tectonic atau ENGINE=lualatex)
make tectonic     Build PDF khusus dengan Tectonic
make lualatex     Build PDF khusus dengan LuaLaTeX
make doctor       Cek ketersediaan compiler dan tool
make clean        Hapus artefak atau file sementara
make distclean    Hapus direktori build/ dan dist/
make validate     Validasi sumber LaTeX dengan chktex
make watch        Build ulang otomatis saat ada perubahan
make help         Tampilkan pesan bantuan
```

Windows:

```
make.bat           Build PDF (otomatis memilih compiler)
make.bat build     Build PDF (sama dengan default)
make.bat tectonic  Build PDF khusus dengan Tectonic
make.bat lualatex  Build PDF khusus dengan LuaLaTeX
make.bat clean     Hapus artefak
make.bat distclean Hapus direktori build/ dan dist/
make.bat validate  Validasi dengan chktex
```

Tanpa Makefile:

```
# LuaLaTeX (distribusi lengkap):
latexmk -lualatex -output-directory=build src/main.tex

# Tectonic (ringan):
tectonic -Z search-path=. -Z search-path=src/config -Z search-path=src -o build src/main.tex
```

Nama PDF dihasilkan otomatis dari data di `src/config/information.tex`
dengan format `Tesis_<ProgramStudiSingkat>_<NamaPenulis>_<Bulan Tahun>.pdf`.
Contoh: `Tesis_Ilmu_Komputer_Nama_Penulis_Jun_2026.pdf`.

## Mengatur jumlah pembimbing

Bawaannya dua pembimbing. Untuk komisi pembimbing bertiga, ubah satu baris di
`src/config/information.tex`:

```latex
\newcommand{\TampilkanPembimbingTiga}{true}
\newcommand{\NamaPembimbingTiga}{Nama Pembimbing 3}
```

Sakelar ini mengatur baris tanda tangan ketiga pada halaman pengesahan sekaligus
penyebutan nama pada Sorotan/Highlights, Ringkasan/Summary, dan Prakata.

## Menyembunyikan catatan panduan

Templat memuat teks merah berisi instruksi dari templat Word resmi, misalnya
`(jika tabel hanya satu tidak perlu dibuat daftar)` di bawah judul Daftar
Tabel/Gambar/Lampiran dan catatan di akhir Prakata. Seluruhnya dikendalikan
satu sakelar di `src/config/information.tex`:

```latex
\renewcommand{\TampilkanCatatanPanduan}{false}  % true = tampilkan (bawaan)
```

Semua teks merah hilang sekaligus, tetapi tata letak halaman daftar tidak
bergeser karena ruang catatan tetap dicadangkan. Catatan tambahan Anda sendiri
dapat memakai `\ipbcatatan{...}` agar ikut tersembunyi oleh sakelar yang sama.

## Struktur Proyek

```
ipb-masters-thesis-latex/
|
+-- Makefile                    Target: build, clean, validate, dst.
+-- make.bat                    Wrapper Windows
+-- .chktexrc                   Konfigurasi chktex
+-- main.pdf                    Salinan hasil build terbaru
+-- ipb.bst                     Kompatibilitas BibTeX lama
+-- ipb.csl                     Kompatibilitas citeproc lama
+-- chapters/                   Kompatibilitas struktur repositori asli
+-- docs/                       Templat Word resmi dan PDF pembanding
+-- scripts/                    Skrip pembantu
+-- src/
    +-- main.tex                Entry point LaTeX
    +-- config/
    |   +-- ipb-thesis.sty      Style utama
    |   +-- information.tex     Data penulis, tesis, institusi
    |   +-- hyphenation-id.tex  Aturan pemenggalan kata
    |   +-- indonesian.lbx      Lokalisasi BibLaTeX Bahasa Indonesia
    |
    +-- ringkasan/              Ringkasan (id) dan Summary (en)
    |   +-- ringkasan.tex
    |   +-- ringkasan-id.tex
    |   +-- ringkasan-en.tex
    |
    +-- preliminaries/          Bagian Awal
    |   +-- cover.tex
    |   +-- pernyataan.tex
    |   +-- sorotan.tex
    |   +-- ringkasan-visual.tex
    |   +-- tim-penguji.tex
    |   +-- lembar-persetujuan.tex
    |   +-- prakata.tex
    |   +-- daftar-isi.tex
    |
    +-- chapters/               Bagian Inti (bab 1 s.d. bab 5)
    +-- backmatter/             Bagian Akhir
    |   +-- daftar-pustaka.tex
    |   +-- lampiran.tex
    |   +-- riwayat-hidup.tex
    |
    +-- refs/                   Database referensi BibTeX/biber
    +-- resources/              Gambar, logo, dan sumber daya lain
```

## Menulis Tesis

- Setiap berkas `.tex` memiliki komentar header yang menjelaskan fungsinya.
- Atur judul, nama, NIM, pembimbing, program studi, dan data lain di
  `src/config/information.tex` (satu sumber kebenaran untuk semua halaman).
- Nilai bawaan berupa placeholder seperti `Nama Penulis`, `NIM`, `20XX`, dan
  `Nama Pembimbing 1`; ganti seluruh placeholder sebelum naskah diserahkan.
- Tulis isi bab di `src/chapters/chapter-N.tex`. Untuk menambah bab baru, buat
  berkas baru lalu tambahkan `\input{chapters/chapter-N}` di `src/main.tex`.
- Ringkasan dan Summary ditulis di `src/ringkasan/ringkasan-id.tex` dan
  `src/ringkasan/ringkasan-en.tex`; keduanya digabung oleh
  `src/ringkasan/ringkasan.tex`. Panjang maksimum dua halaman.
- Ringkasan Visual memakai kotak placeholder kosong. Isi `\BerkasRingkasanVisual`
  (dan `\BerkasRingkasanVisualInggris`) dengan path gambar bila sudah ada.
- Tambahkan referensi di `src/refs/daftar-pustaka.bib` dan sitasi dengan
  `\citep{key}` atau `\citet{key}`.
- Halaman kosong pada keluaran berasal dari aturan `openright` (setiap bagian
  besar dimulai pada halaman ganjil) dan memang disengaja untuk pencetakan.
  Halaman tersebut benar-benar kosong: tanpa nomor halaman dan tanpa header.

## Spesifikasi Format

Seluruh pengaturan berikut sudah diterapkan di `src/config/ipb-thesis.sty`
sesuai PPTA IPB 2026 dan templat `format tesis terbaru.docx`.

| Elemen | Spesifikasi |
|---|---|
| Kertas | A4 (210 x 297 mm) |
| Margin | sisi dalam 4 cm; sisi luar, atas, dan bawah 3 cm |
| Mirror margins | Aktif (twoside) |
| Font teks | Times New Roman 12pt |
| Spasi teks | Tunggal (single spacing) |
| Indentasi awal paragraf | 1 cm |
| Jarak antar paragraf | 0 pt |
| Judul bab | 14pt, tebal, rata tengah, huruf kapital penuh |
| Judul subbab | 12pt, tebal, rata kiri |
| Judul sub-subbab | 12pt, tidak tebal, rata kiri |
| Penomoran bab | Angka Romawi kapital (I, II, III, IV, V) |
| Penomoran subbab | Angka Arab desimal (1.1, 1.2, 2.1, 2.2) |
| Penomoran sub-subbab | Angka Arab desimal (1.1.1) |
| Nomor halaman bagian awal | Hitungan Romawi dimulai dari Sorotan; tidak dicetak |
| Nomor halaman isi/akhir | Arab di sudut luar atas; disembunyikan pada pembuka bagian |
| Pembukaan bagian | Bab dan bagian besar dimulai pada halaman ganjil |
| Daftar ilustrasi | Daftar tabel/gambar/lampiran muncul jika jumlahnya lebih dari satu |
| Sitasi dan daftar pustaka | BibLaTeX + biber, Harvard nama–tahun/CSE edisi ke-9 |
| Bahasa utama | Indonesia, dengan dukungan Inggris |
| Compiler utama | LuaLaTeX atau Tectonic |

## Kontribusi

Kontribusi berupa laporan masalah, saran perbaikan, maupun pull request sangat
disambut. Silakan baca [CONTRIBUTING.md](CONTRIBUTING.md) untuk panduan singkat
sebelum berkontribusi.

## Lisensi

Template ini dilisensikan di bawah [Lisensi MIT](LICENSE). Pedoman dan templat
Word resmi merupakan milik **IPB University**. Template LaTeX ini merupakan
hasil adaptasi mandiri yang tidak bersifat resmi dan tidak terafiliasi dengan
IPB University.

## Kredit dan Atribusi

Template ini adalah port program magister dari
**[raihanpka/ipb-thesis-latex](https://github.com/raihanpka/ipb-thesis-latex)**
karya *Raihan Putra Kirana* dan para kontributor, dengan lisensi MIT. Struktur
proyek, style dasar, Makefile, dan berkas pendukung berasal dari proyek
tersebut; bagian awal, ringkasan, dan penyesuaian format magister ditambahkan
di repositori ini.

Pedoman dan templat Word asli merupakan milik **IPB University**.

**Kontributor upstream:**
- *Raihan Putra Kirana* — GitHub: [@raihanpka](https://github.com/raihanpka)
- *Mochamad Chairulridjal Nurvikri* — GitHub: [@chairulridjal](https://github.com/chairulridjal)
- *Ghiffari Bravia Hisham* — GitHub: [@ghiffaribraviah](https://github.com/ghiffaribraviah)

**Atribusi tambahan:**
- Berkas CSL di `src/refs/ipb.csl` dan `src/refs/ipb-en.csl` diadaptasi dari
  [auriza/csl-ipb](https://github.com/auriza/csl-ipb) karya *Auriza Rahmad
  Akbar* ([@auriza](https://github.com/auriza)).
- Struktur proyek terinspirasi dari *Petra Novandi*
  ([petrabarus/if-itb-latex](https://github.com/petrabarus/if-itb-latex)).

Jika template ini bermanfaat, silakan berikan bintang (star) pada repositori ini
sebagai bentuk apresiasi.

Lihat [GUIDE.md](GUIDE.md) untuk detail instalasi per platform, troubleshooting,
dan kustomisasi lanjutan. Riwayat perubahan ada di
[CHANGELOG.md](CHANGELOG.md).
