# DATA-DICT-MASTER: JLPT Academy

> **Dokumen:** Kamus data — sumber kebenaran makna tiap tabel/field
> **Proyek:** JLPT Academy — LPK & SO
> **Format:** 4 field standar (Name · Alias · Values/format · Description)
> **Versi:** 0.2 (excerpt per chapter di-generate dari sini)

> Mencakup field **kunci** tiap entitas (bukan seluruh kolom teknis seperti `created_at`). Field teknis standar (id, created_at, updated_at) berlaku umum di semua tabel dan tidak diulang.

---

## Blok 1 — Identitas & Peran

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `users.role` | peran pengguna | `siswa`\|`sensei`\|`pembina`\|`staff_so`\|`admin_keu`\|`pimpinan` | Menentukan tabel profil 1:1 mana yang dipakai & hak akses |
| `users.no_hp` | nomor WhatsApp | string (E.164) | Kanal notifikasi utama (WA Gateway) |
| `siswa.nik` | Nomor Induk Kependudukan | 16 digit | **PII sensitif** — wajib enkripsi |
| `siswa.jalur_karir` | track tujuan | `magang`\|`ssw1`\|`ssw2` | Menentukan kurikulum & persyaratan |
| `siswa.goldar` | golongan darah | `A`\|`B`\|`AB`\|`O` | Kebutuhan medis/asrama |
| `siswa.no_paspor` | nomor paspor | string | **PII sensitif** — untuk penyaluran |
| `sensei.sertif_jlpt` | sertifikasi JLPT | `N1`\|`N2`\|`N3` | Kelayakan mengajar per level |
| `pembina.bidang_tugas` | fokus pembinaan | string | Asrama / fisik / kedisiplinan |

## Blok 2 — MCU & Kesehatan

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `mcu_record.hasil` | hasil MCU | `fit`\|`unfit`\|`ulang` | **Fit** = syarat lanjut pipeline (BR-006) |
| `mcu_record.tahap` | tahap MCU | `awal`\|`final` | MCU final jadi gerbang matching |

## Blok 3 — Asrama & Kedisiplinan

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `absensi_apel.jenis` | jenis apel | `apel_pagi`\|`tenko_malam` | Apel pagi vs Tenko malam |
| `absensi_apel.status` | status hadir | `hadir`\|`izin`\|`alpa` | Kedisiplinan karantina |
| `kesamaptaan_fisik.lari_meter` | jarak lari | integer (meter) | Rekam kesamaptaan fisik |
| `log_pelanggaran.tingkat` | tingkat pelanggaran | `ringan`\|`sedang`\|`berat` | Menentukan tindakan pembina |

## Blok 4 — Konten & Level

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `level.kode` | kode level | `N5`..`N1`\|`JFT` | **Unique** — pengelompok utama |
| `level.jenis` | jenis ujian | `jlpt`\|`jft` | Menentukan format timer & tipe soal |
| `level.ambang_total` | ambang lulus total | integer (0–180) | Syarat total skor (BR-003) |
| `level.ambang_sect` | ambang per section | integer | Syarat minimal tiap section (BR-003) |
| `materi.tipe_materi` | jenis materi | `kanji`\|`kosakata`\|`bunpou`\|`choukai`\|`etika_5s` | Kelompok konten belajar |
| `materi.kaki_yomi` | cara baca kanji | string | Kaki (tulis) / Yomi (baca) |
| `bank_soal.section` | bagian soal | `vocab`\|`grammar`\|`reading`\|`listening` | Pemetaan ke scoring section |
| `bank_soal.format` | format soal | `cbt`\|`kertas` | JLPT=kertas, JFT=CBT |

## Blok 5 — Kelas & Presensi

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `kelas.nama_batch` | nama angkatan kelas | string | **DIPISAH** dari `diklat_session.kode_angkatan` |
| `kelas.mode` | mode kelas | `offline`\|`online`\|`hybrid` | Teori bisa online, karantina tatap muka |
| `absensi_akademik.status` | status hadir kelas | `hadir`\|`izin`\|`sakit`\|`alpa` | Presensi akademik |

## Blok 6 — Belajar & SRS

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `srs_card.status` | status penguasaan | `baru`\|`belajar`\|`sulit`\|`dikuasai` | State spaced repetition |
| `srs_card.next_review` | jadwal review | datetime | Kartu muncul tepat sebelum lupa |
| `enrollment.status` | status enrollment | `aktif`\|`lulus`\|`berhenti` | Progres siswa di level |

## Blok 7 — Mock Exam & CBT

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `mock_exam.format` | format ujian | `cbt`\|`kertas` | Meniru ujian resmi |
| `mock_exam.skor_vocab/reading/listening` | skor per section | integer (0–60) | Dasar penentuan lulus sectional |
| `mock_exam.result` | hasil | `lulus`\|`gagal` | Total ≥ ambang DAN tiap section ≥ ambang (BR-003) |
| `hasil_ujian_resmi.jenis_ujian` | jenis ujian resmi | `jlpt`\|`jft`\|`skill_test` | Hasil impor/manual |

## Blok 8 — Penyaluran & Dokumen

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `berkas_siswa.jenis_berkas` | jenis dokumen | `ktp`\|`kk`\|`ijazah`\|`surat_ortu`\|`mcu`\|`paspor` | Berkas persyaratan |
| `berkas_siswa.status_verifikasi` | status verifikasi | `menunggu`\|`verified`\|`revisi` | Gerbang kelengkapan dokumen |
| `pipeline_status.tahap` | tahap penyaluran | `screening_mcu`→`diklat_bahasa`→`lulus_ujian`→`siap_matching`→`panggilan_mensetsu`→`lolos_interview`→`ttd_kontrak`→`pengajuan_coe`→`coe_terbit`→`visa_issued`→`tiket_berangkat` | **11 tahap Kanban** (BR-008 audit) |
| `mitra_penempatan.jenis` | jenis mitra | `kumiai`\|`kaisha`\|`tsk` | Mitra penempatan Jepang |
| `penempatan.hasil_mensetsu` | hasil wawancara | `goukaku`\|`shippai` | Lulus/gagal wawancara |
| `coe_visa.status` | status dokumen | `proses`\|`terbit`\|`ditolak` | Tracking COE & visa |

## Blok 9 — Keuangan

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `invoice.kategori_biaya` | jenis tagihan | `bahasa`\|`asrama_makan`\|`ujian`\|`visa` | Pengelompokan biaya |
| `invoice.skema_bayar` | skema pembayaran | `lunas`\|`dp_angsuran`\|`dormant_indent` | **3 skema wajib** (BR-012): lunas sekaligus / DP+lalu cicilan / indent belum datang |
| `invoice.dp_jumlah` | uang muka | decimal • | Diisi bila `skema_bayar='dp_angsuran'` |
| `invoice.sisa_tagihan` | sisa tagihan | decimal **COMPUTED** | `jumlah_total − jumlah_bayar` (bukan input manual) |
| `invoice.dormant_mulai` | mulai indent | date • | Diisi bila `skema_bayar='dormant_indent'` — tagihan ditahan |
| `invoice.dormant_alasan` | alasan indent | string • | Mis. menunggu kuota keberangkatan |
| `invoice.status` | status bayar | `unpaid`\|`dp_terbayar`\|`cicilan`\|`dormant`\|`paid`\|`pending`\|`refund` | `paid` = syarat sertifikat (BR-004); `dormant` = jatuh tempo ditahan (BR-012) |
| `jadwal_cicilan.nomor_angsuran` | ke berapa | integer | Urutan cicilan per `invoice` |
| `jadwal_cicilan.status` | status angsuran | `menunggu`\|`terbayar`\|`terlambat` | Jadwal DP→cicilan (BR-012) |
| `transaksi.metode` | cara bayar | `va`\|`qris`\|`tunai` | Payment gateway / manual |
| `dana_talangan.sumber` | sumber talangan | `koperasi_mitra`\|`internal_lpk`\|`donasi_pemerintah`\|`mitra_lain` | **Multi-sumber** (keputusan A4) |

## Blok 10 — Sertifikat

| Name | Alias | Values/Format | Description |
|------|-------|---------------|-------------|
| `sertifikat.jenis` | jenis sertifikat | `internal_lpk`\|`jlpt_resmi`\|`jft_resmi`\|`skill_test` | Internal = syarat Mensetsu (BR-005) |
| `sertifikat.jam_belajar` | jumlah jam belajar | integer (jam) | Bukti 150–300 jam (BR-005) |
| `sertifikat.nomor_seri` | nomor seri | string **UNIQUE** | Verifikasi keaslian |
| `sertifikat.qr_code` | QR verifikasi | string (URL) | Laman verifikasi publik |

---

## Open Questions / Trade-off
1. **Retensi 10 tahun** (BR-009) — perlu field `tanggalhapus`/status arsip eksplisit, atau kebijakan luar DB?
2. **`pipeline_status.tahap`** — apakah menyimpan history penuh (banyak baris/siswa) untuk audit, atau hanya status terakhir?
3. **PII field** — daftar field terenkripsi (AES-256) perlu dideklarasikan eksplisit di satu tempat agar audit mudah.
