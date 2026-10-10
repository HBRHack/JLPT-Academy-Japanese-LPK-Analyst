# GLOSSARY: JLPT Academy — LPK & Sending Organization

> **Dokumen:** Glosarium Istilah Lintas Modul (Sumber kebenaran terminologi)
> **Proyek:** JLPT Academy — LPK & SO Jepang
> **Versi:** 0.2 (Sinkron dengan question-framework FINAL — 10 Okt 2026)

Aturan: satu istilah = satu makna di seluruh dokumen. Istilah masuk bila unik-domain, multi-definisi, di luar makna umum, atau rawan salah paham.

---

## A

**Apel**
Rapat/apel pembuka hari di asrama (pagi) — bagian dari absensi karantina. Lihat juga **Tenko**.

---

## B

**Bank Soal**
Kumpulan soal mock exam/CBT, dikelompokkan per level × 12 tipe soal × section. Dielola via **CMS terpisah** agar guru konten bisa update tanpa ganggu modul siswa.

**Batch (Kelas)**
Nama angkatan **kelas akademik** (mis. "Batch A") — field `kelas.nama_batch`. Secara resmi **DIPISAH** dari **Diklat Session** (`diklat_session.kode_angkatan`) — dua entitas & penamaan berbeda (keputusan final).

---

## C

**CBT (Computer Based Test)**
Ujian berbasis komputer — dipakai untuk mock exam & format **JFT-Basic** (berbeda dari JLPT yang berbasis kertas per section).

**Choukai (聴解)**
Materi **listening/mendengar** — audio MP3/WAV untuk drill.

**COE (Certificate of Eligibility)**
Sertifikat kelayakan tinggal yang diterbitkan Imigrasi Jepang — tahap penting sebelum visa. Tracker: `coe_visa`.

---

## D

**Deserter / Kabur**
Siswa yang menghilang setelah tiba di Jepang. Target lembaga: **zero-deserter** (reputasi & audit).

**Diklat Session**
Satu angkatan/periode **diklat karantina** (tanggal mulai–selesai, lokasi, peserta) — field `diklat_session.kode_angkatan` (bukan `nama_batch`). **DIPISAH** dari Batch kelas (keputusan final).

**Dana Talangan**
Pembiayaan awal yang menutup biaya siswa sebelum dibayar penuh — sumbernya **multi-skenario**: koperasi mitra, internal LPK, **donasi pemerintah**, atau mitra lain (`dana_talangan.sumber`).

**DP (Down Payment)**
Uang muka yang dibayar di muka sebelum total tagihan — `invoice.skema_bayar='dp_angsuran'` dengan `dp_jumlah`; sisanya dijadwalkan sebagai angsuran (`jadwal_cicilan`).

**Dormant (Indent)**
Status tagihan **ditahan karena layanan/keberangkatan belum datang** (indent kuota) — `invoice.skema_bayar='dormant_indent'`, `status='dormant'`, `dormant_mulai` diisi; **belum jatuh tempo** & pengingat dinonaktifkan sampai aktif kembali.

**Angsuran (Cicilan)**
Pembayaran berkala per bulan atas sisa tagihan setelah DP — direkam per baris di **`jadwal_cicilan`** (`nomor_angsuran`, `tanggal_jatuh_tempo`, `jumlah`, `status='menunggu|terbayar|terlambat'`).

**Dokkai (読解)**
Materi **membaca/pemahaman bacaan**.

---

## G

**Ginou Jisshuusei (技能実習生)**
Istilah resmi **Magang/Technical Intern** — jalur kerja 3 tahun ke Jepang.

**Goukaku (合格)**
**Lulus** (khusus hasil wawancara *Mensetsu*). Lawannya **Shippai** (gagal).

---

## J

**JFT-Basic (Japan Foundation Test for Basic Japanese)**
Ujian komputer, fokus **komunikasi situasi kerja & hidup**, setara **A2**. Diterima sebagai syarat visa **SSW I** (alternatif JLPT N4).

**Jalur Karir**
Track siswa: **Magang 3 tahun (Ginou Jisshuusei) → SSW I → SSW II**.

---

## K

**Kaigo (介護)**
Sektor **perawatan lansia** — salah satu sektor penempatan SSW yang paling banyak diminati.

**Kaki / Yomi (書き / 読み)**
Cara **menulis** & **membaca** kanji — atribut materi kanji.

**Kenshuusei (研修生)**
Istilah terkait magang/pelatih — sering disebut saat alih status alumni di Jepang.

**Kumiai (組合)**
**Organisasi pengawas/serikat** di Jepang yang mengawasi penempatan magang — mitra resmi LPK/SO.

---

## M

**MCU (Medical Check Up)**
**Pemeriksaan kesehatan** calon siswa — hasil **Fit/Unfit** menentukan kelayakan lanjut ke tahap penyaluran.

**Mensetsu (面接)**
**Wawancara kerja** dengan perusahaan Jepang — hasil **Goukaku/Shippai**. Simulasi dilakukan saat diklat.

---

## P

**Pass Rate**
Persentase siswa yang lulus ujian (mock maupun resmi) — metrik utama (target ≥ 85%).

**Pipeline (Talent Pipeline)**
Alur penyaluran siswa: **Screening MCU → Diklat → Lulus Ujian → Siap Matching → Mensetsu → Kontrak → COE → Visa → Berangkat**. Ditampilkan sebagai **Kanban**.

**Pembina Diklat & Asrama**
Peran pengelola karantina: absensi apel/Tenko, kesamaptaan fisik, log pelanggaran.

---

## R

**Rirekisho (履歴書)**
**CV standar Jepang (format JIS)** — digenerate otomatis 1-klik dari profil siswa untuk Kumiai.

---

## S

**Section (Bagian Soal)**
Kelompok skor ujian. N1–N3: **Vocab/Grammar · Reading · Listening**. N4–N5: **Vocab/Grammar+Reading · Listening**.

**Sektor Kerja**
Bidang penempatan: **Kaigo (lansia), Manufaktur/Pabrik, Konstruksi, Pengolahan Makanan**.

**Sensei (先生)**
Istilah untuk **guru/pengajar** bahasa Jepang.

**Shippai (失敗)**
**Gagal** (khusus hasil *Mensetsu*). Lawan **Goukaku**.

**SRS (Spaced Repetition System)**
Metode drill dengan interval review menyesuaikan penguasaan — kartu kanji/kosakata muncul tepat sebelum lupa.

**SSW (Specified Skilled Worker)**
Visa kerja terampil Jepang. Butuh **lulus JLPT N4 ATAU JFT-Basic A2** + lulus uji keahlian sektor (Prometric).

**Staff Matching & Penyaluran (SO)**
Peran **Sending Organization** yang mengelola matching Kumiai, Kanban pipeline, Rirekisho, COE, visa.

---

## T

**Tenko (点呼)**
**Absensi/apel malam** di asrama — bagian karantina. Lihat **Apel**.

**Tokutei Ginou (特定技能)**
Istilah resmi **SSW (Pekerja Berketerampilan Khusus)** — tahap lanjutan setelah magang.

**TSK (Toroku Shien Kikan)**
**Lembaga dukungan pendaftaran** — mitra penyaluran resmi di samping Kumiai.

**5S**
Prinsip etika kerja Jepang: **Seiri, Seiton, Seiso, Seiketsu, Shitsuke** — materi modul persiapan kerja.

---

## U

**UU PDP No. 27/2022**
**Undang-Undang Perlindungan Data Pribadi** — dasar enkripsi, retensi, & hak hapus data siswa.

---

## Open Questions / Trade-off
1. ~~Istilah **"Batch"** dipakai untuk dua hal (kelas & diklat)~~ → **SELESAI:** sudah dipisah eksplisit — `kelas.nama_batch` vs `diklat_session.kode_angkatan`.
2. Perlu istilah lokal untuk **"Jalur Karir"** agar siswa awam paham (mis. "Track Magang", "Track SSW")?
3. **Kenshuusei vs Ginou Jisshuusei** — sering dipakai bergantian; perlu definisikan mana yang dipakai resmi di sistem?
