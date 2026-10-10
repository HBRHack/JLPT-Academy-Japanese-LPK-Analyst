# Business Rules: JLPT Academy — LPK & Sending Organization

> **Dokumen:** Business Rules global (lintas chapter)
> **Proyek:** JLPT Academy
> **Sumber kebenaran bisnis:** `question-framework.md` (FINAL) — dirutekan ke sini
> **Versi:** 0.2

**Tipe rule:**
- **Definitional** = tak bisa dilanggar (kebenaran definisi), tapi bisa salah-pakai → enforce konsistensi.
- **Behavioural** = BISA dilanggar → tentukan level enforcement: **ketat** / **override-otorisasi** / **override-alasan** / **guideline**.

---

## BR-001 — Enrollment mengunci level mock exam
- **Tipe:** Definitional
- **Enforcement:** Ketat (validasi sistem)
- **Rule:** Siswa hanya bisa mengikuti mock exam untuk **level** yang tercantum pada `enrollment`-nya.
- **Rationale:** Mencegah siswa N5 uji level N1 (skor tidak bermakna, boros bank soal).
- **Ditandai di:** `enrollment.level_id`, `mock_exam.level_id`

## BR-002 — Timer adaptif per section
- **Tipe:** Behavioural
- **Enforcement:** Ketat (server-side timer)
- **Rule:** Setiap sesi mock exam/CBT menggunakan **timer per section** sesuai blueprint ujian (mis. N1: Vocab/Grammar+Reading 110 mnt, Listening 55 mnt). Jawaban **submit otomatis** saat waktu habis.
- **Rationale:** Meniru kondisi ujian nyata; mencegah kecurangan waktu.
- **Ditandai di:** `exam_timer.durasi_menit`, `bank_soal.section`

## BR-003 — Syarat kelulusan mock (total + sectional)
- **Tipe:** Definitional
- **Enforcement:** Ketat (kalkulasi otomatis)
- **Rule:** `result = 'lulus'` HANYA bila **skor total ≥ ambang level** DAN **tiap section ≥ ambang sectional**. Satu section di bawah ambang = **gagal** walau total tinggi.
- **Rationale:** Meniru skoring resmi JLPT/JFT.
- **Ditandai di:** `level.ambang_total`, `level.ambang_sect`, `mock_exam.result`

## BR-004 — Sertifikat butuh modul selesai + mock lulus + biaya lunas
- **Tipe:** Behavioural
- **Enforcement:** Ketat (gerbang terbit sertifikat)
- **Rule:** Sertifikat internal hanya terbit bila: seluruh **modul** level selesai **DAN** mock exam lulus **DAN** `invoice.status = 'paid'`.
- **Rationale:** Menjaga nilai sertifikat & ikut menagih kewajiban bayar.
- **Ditandai di:** `sertifikat`, `invoice.status`

## BR-005 — Sertifikat internal = syarat Mensetsu & bukti jam belajar
- **Tipe:** Definitional
- **Enforcement:** Ketat (syarat proses penyaluran)
- **Rule:** Sertifikat internal LPK berfungsi sebagai **syarat kelayakan Mensetsu** & bukti **jam belajar minimal 150–300 jam** (diwajibkan Imigrasi Jepang/Kemenaker). Sertifikat kompetensi kerja final tetap mengacu sertifikat resmi JLPT/JFT & Prometric SSW.
- **Rationale:** Legalitas dokumen ke Jepang.
- **Ditandai di:** `sertifikat.jam_belajar`, `sertifikat.jenis`

## BR-006 — MCU Fit syarat lanjut penyaluran
- **Tipe:** Behavioural
- **Enforcement:** Ketat (gerbang pipeline)
- **Rule:** Siswa **wajib MCU `hasil='fit'`** (tahap akhir) sebelum tahap `pipeline_status` bisa maju ke `siap_matching`/setelahnya.
- **Rationale:** Kesehatan = syarat kerja di Jepang; cegah penempatan siswa tak layak.
- **Ditandai di:** `mcu_record.hasil`, `pipeline_status.tahap`

## BR-007 — Enkripsi, retensi, & hak hapus data (UU PDP)
- **Tipe:** Behavioural (kepatuhan)
- **Enforcement:** Ketat (kebijakan + mekanisme)
- **Rule:** Data pribadi sensitif **wajib dienkripsi** (AES-256 at-rest, TLS 1.3 in-transit). Data siswa disimpan **10 tahun** (audit Kemenaker/Imigrasi). Pendaftar gugur screening → **soft delete**; data sensitif (KTP/KK) **dihapus permanen setelah 1 tahun** (UU PDP No. 27/2022).
- **Rationale:** Kepatuhan hukum & proteksi siswa.
- **Ditandai di:** seluruh tabel ber-PII; `siswa.status`

## BR-008 — Perubahan pipeline hanya oleh petugas & ter-audit
- **Tipe:** Behavioural
- **Enforcement:** Ketat (otorisasi + log)
- **Rule:** `pipeline_status.tahap` hanya boleh diubah **Staff SO/Pembina**. Setiap perpindahan Kanban wajib mencatat `staff_user_id`, `tanggal_update`, `catatan` (jejak audit).
- **Rationale:** Integritas penyaluran (zero-deserter) butuh jejak audit.
- **Ditandai di:** `pipeline_status.staff_user_id`

## BR-009 — Retensi & audit dokumen
- **Tipe:** Behavioural (kepatuhan)
- **Enforcement:** Ketat
- **Rule:** Seluruh data siswa (termasuk dokumen, ujian, penyaluran) disimpan **10 tahun** untuk kepatuhan Kemenaker & audit Imigrasi Jepang.
- **Rationale:** Regulasi & perpanjangan kontrak alumni.
- **Ditandai di:** seluruh tabel siswa

## BR-010 — Free retake bimbingan 1x
- **Tipe:** Behavioural
- **Enforcement:** Ketat (hak siswa)
- **Rule:** Siswa yang gagal ujian berhak **pendampingan kelas ulang + akses mock exam gratis 1x** pada batch berikutnya (tanpa SPP tambahan). Biaya pendaftaran **ujian resmi** tetap mandiri.
- **Rationale:** Kebijakan layanan lembaga.
- **Ditandai di:** `enrollment.status`, `mock_exam.attempt_ke`

## BR-011 — Presensi wajib 2 moda (akademik & karantina)
- **Tipe:** Definitional
- **Enforcement:** Ketat
- **Rule:** Kehadiran dicatat di **dua tabel terpisah**: `absensi_akademik` (per kelas) & `absensi_apel` (Apel Pagi/Tenko). Karantina = absensi harian apel.
- **Rationale:** Dua domain kehadiran berbeda (belajar vs kedisiplinan asrama).
- **Ditandai di:** `absensi_akademik`, `absensi_apel`

## BR-012 — Tiga skema pembayaran (DP, Dormant/Indent, Angsuran)
- **Tipe:** Behavioural
- **Enforcement:** Ketat (kalkulasi & jadwal otomatis)
- **Rule:** Setiap `invoice` punya `skema_bayar` salah satu dari:
  1. **`lunas`** — bayar penuh sekaligus → `status='paid'` langsung.
  2. **`dp_angsuran`** — bayar **DP** di muka (`dp_jumlah`) → `status='dp_terbayar'`, sisanya dijadwalkan per bulan di **`jadwal_cicilan`** → tiap angsuran tercatat (`menunggu/terbayar/terlambat`) → lunas saat `sisa_tagihan=0`.
  3. **`dormant_indent`** — **indent / layanan belum datang**: tagihan ditahan (`status='dormant'`, `dormant_mulai` diisi), **belum jatuh tempo** sampai siswa/layanan aktif → diakhiri dengan konversi ke `lunas`/`dp_angsuran`/tetap dormant.
- **Aturan turunan:**
  - `sisa_tagihan` = `jumlah_total − jumlah_bayar` (**COMPUTED**, bukan input manual).
  - Sertifikat butuh `status='paid'` (BR-004) → **DP atau cicilan berjalan BELUM cukup** untuk terbitkan sertifikat.
  - Saat `status='dormant'`, pengingat jatuh tempo **dinonaktifkan** sampai aktif kembali.
- **Rationale:** Fleksibilitas finansial siswa (umum untuk siswa yang menunggu keberangkatan/indent kuota).
- **Ditandai di:** `invoice.skema_bayar`, `invoice.dp_jumlah`, `invoice.dormant_*`, `jadwal_cicilan.*`

---

## Open Questions / Trade-off
1. **BR-003 ambang sectional** — untuk JFT-Basic (CBT, bukan skoring section 3 bagian) perlu aturan lulus tersendiri? (belum didefinisikan eksplisit)
2. **BR-010 retake** — apakah ada batas jumlah percobaan selamanya, atau hanya 1x per batch?
3. **BR-006** — bagaimana jika MCU 'unfit' masih ingin lanjut: apakah ada jalur banding/MCU ulang?
