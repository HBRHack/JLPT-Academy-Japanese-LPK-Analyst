# ERD-MASTER: JLPT Academy — LPK & Sending Organization

> **Dokumen:** Entity Relationship Diagram — Master (seluruh entitas & relasi)
> **Format:** ASCII box-art (sesuai GLOBAL-00 — ERD wajib ASCII)
> **Sumber kebenaran:** Ya — excerpt per chapter di-generate dari sini, jangan edit manual di excerpt
> **Versi:** 0.2 (Sinkron dengan question-framework FINAL — 10 Okt 2026)
> **Catatan:** Penanda `[?]` = butuh keputusan teknis (lihat Open Questions)

---

## Legenda
- `PK` = Primary Key · `FK` = Foreign Key · `U` = Unique
- Relasi: `1:N` · `N:M` (butuh tabel penghubung) · `•` = nullable
- Enum penting ditulis `← 'val1'|'val2'`

---

## 1. Blok Identitas & Peran (6 Peran)

```
┌──────────────────────────┐
│         users            │
├──────────────────────────┤
│ PK │ id                  │
│    │ nama                │
│    │ email               │
│    │ no_hp               │
│    │ password_hash       │
│    │ role                │←'siswa'|'sensei'|'pembina'|'staff_so'|'admin_keu'|'pimpinan'
│    │ status              │←'aktif'|'nonaktif'
│    │ created_at / updated│
└────────────┬─────────────┘
             │ 1:1 (polimorf via role)
   ┌─────────┼──────────┬───────────┬───────────┬───────────┐
   ▼         ▼          ▼           ▼           ▼           ▼
┌────────┐┌────────┐┌─────────┐┌──────────┐┌──────────┐┌──────────┐
│ siswa  ││ sensei ││ pembina ││staff_so  ││admin_keu ││ pimpinan │
├────────┤├────────┤├─────────┤├──────────┤├──────────┤├──────────┤
│PKFKu_id││PKFKu_id││PKFKu_id ││PKFKu_id  ││PKFKu_id  ││PKFKu_id  │
│ nik    ││sertif_ ││bidang_  ││unit      ││departemen││jabatan   │
│ ttl    ││ _jlpt  ││ _tugas  ││(matching)││          ││          │
│ jk     ││lisensi_││         │└──────────┘└──────────┘└──────────┘
│ tb / bb││ _ajar  │└─────────┘
│ goldar ││spesial_│
│ alamat ││ _isasi │
│ kontak_││jam_    │
│ _darurt││ terbang│
│ no_    ││ honor  │
│ _paspor│└────────┘
│ riwayat│
│ _didik│
│ jalur_ │
│ _karir │
│ status │
└───┬────┘
    │ (relasi ke banyak blok di bawah)
```

---

## 2. Blok MCU & Kesehatan (BARU)

```
┌──────────────────────────┐
│        mcu_record        │
├──────────────────────────┤
│ PK │ id                  │
│ FK │ siswa_user_id       │
│    │ tanggal_mcu         │
│    │ hasil               │←'fit'|'unfit'|'ulang'
│    │ catatan_penyakit    │•
│    │ dokter / klinik     │
│    │ dokumen_url         │•  (scan hasil MCU)
│    │ tahap               │←'awal'|'final'
└──────────────────────────┘
```
> **BR-006:** Siswa wajib MCU **Fit** sebelum lanjut tahap matching/penyaluran.

---

## 3. Blok Asrama & Kedisiplinan (BARU)

```
┌──────────────────────────┐       ┌──────────────────────────┐
│       kamar_asrama       │       │    penghuni_kamar        │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │──1:N──│ PK │ id                  │
│    │ nomor_kamar         │       │ FK │ kamar_id            │
│    │ blok                │       │ FK │ siswa_user_id       │
│    │ kapasitas           │       │    │ tanggal_masuk       │
│    │ status              │←'tersedia'|'penuh'|'maintenance'  │    │ tanggal_keluar     │•
└──────────────────────────┘       └──────────────────────────┘

┌──────────────────────────┐       ┌──────────────────────────┐
│      jadwal_piket        │       │      absensi_apel       │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │       │ PK │ id                  │
│ FK │ kamar_id            │       │ FK │ siswa_user_id       │
│ FK │ siswa_user_id       │       │    │ tanggal             │
│    │ tanggal             │       │    │ jenis               │←'apel_pagi'|'tenko_malam'
│    │ shift               │←'pagi'|'sore'|'malam'  │    │ status              │←'hadir'|'izin'|'alpa'
└──────────────────────────┘       │    │ check_in_qr         │•
                                   │    │ waktu_checkin       │•
┌──────────────────────────┐       │ FK │ penginput_user_id   │
│   kesamaptaan_fisik      │       └──────────────────────────┘
├──────────────────────────┤
│ PK │ id                  │       ┌──────────────────────────┐
│ FK │ siswa_user_id       │       │      log_pelanggaran    │
│    │ tanggal             │       ├──────────────────────────┤
│    │ push_up             │       │ PK │ id                  │
│    │ pull_up             │•      │ FK │ siswa_user_id       │
│    │ lari_meter          │       │ FK │ pembina_user_id     │
│    │ catatan             │•      │    │ tanggal             │
└──────────────────────────┘       │    │ jenis_pelanggaran   │
                                   │    │ tingkat             │←'ringan'|'sedang'|'berat'
                                   │    │ tindakan            │
                                   │    │ catatan             │•
                                   └──────────────────────────┘
```

---

## 4. Blok Master Konten (Level, Materi, Bank Soal)

```
┌──────────────────┐       ┌──────────────────────────┐
│      level       │       │          modul           │
├──────────────────┤       ├──────────────────────────┤
│ PK │ id          │──1:N──│ FK │ level_id            │
│ U  │ kode        │       │ PK │ id                  │  ← 'kode' = N5..N1 / JFT
│    │ nama        │       │    │ judul               │
│    │ jenis       │←'jlpt'|'jft'│    │ urutan              │
│    │ ambang_total│       │    │ deskripsi           │
│    │ ambang_sect │       └───────────┬──────────────┘
└────────┬─────────┘                   │ 1:N
         │                             ▼
         │ 1:N               ┌──────────────────────────┐
         │                   │         materi           │
         │                   ├──────────────────────────┤
         │                   │ PK │ id                  │
         │                   │ FK │ modul_id            │
         │                   │    │ tipe_materi         │←'kanji'|'kosakata'|'bunpou'|'choukai'|'etika_5s'
         │                   │    │ kanji               │•
         │                   │    │ kaki_yomi           │•  (bacaan)
         │                   │    │ furigana            │•
         │                   │    │ stroke_order        │•  (JSON)
         │                   │    │ arti                │•
         │                   │    │ contoh_kalimat      │•
         │                   │    │ audio_url           │•
         │                   │    │ difficulty          │
         │                   └──────────────────────────┘
         │
         │ 1:N
         ▼
┌──────────────────────────┐
│        bank_soal         │
├──────────────────────────┤
│ PK │ id                  │
│ FK │ level_id            │
│    │ tipe_soal           │  ← 12 tipe (kanji reading, orthography, dst)
│    │ section             │←'vocab'|'grammar'|'reading'|'listening'
│    │ format              │←'cbt'|'kertas'
│    │ konten_soal         │
│    │ pilihan_jawaban     │  ← JSON (A/B/C/D) [?]
│    │ jawaban_benar       │
│    │ bobot_nilai         │
│    │ pembahasan          │•
│    │ audio_url           │•
│    │ difficulty          │
└──────────────────────────┘
```

---

## 5. Blok Kelas & Presensi Akademik

```
┌──────────────────────────┐       ┌──────────────────────────┐
│          kelas           │       │         jadwal           │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │──1:N──│ PK │ id                  │
│ FK │ level_id            │       │ FK │ kelas_id            │
│ FK │ sensei_user_id      │       │    │ hari / jam_mulai     │
│ U  │ nama_batch          │← 'Batch A/B/...'  │    │ jam_selesai / ruang   │
│    │ kapasitas           │       │    │ topik / meeting_link│•
│    │ tanggal_mulai/selesai│      └──────────────────────────┘
│    │ mode                │←'offline'|'online'|'hybrid'
└────────────┬─────────────┘
             │ N:M
             ▼
┌──────────────────────────┐       ┌──────────────────────────┐
│     enrollment_kelas     │       │    absensi_akademik      │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │       │ PK │ id                  │
│ FK │ siswa_user_id       │──1:N──│ FK │ kelas_id            │
│ FK │ kelas_id            │       │ FK │ siswa_user_id       │
│    │ tanggal_join        │       │    │ tanggal             │
└──────────────────────────┘       │    │ status              │←'hadir'|'izin'|'sakit'|'alpa'
                                   │    │ check_in_qr / waktu │•
                                   │ FK │ penginput_user_id   │
                                   └──────────────────────────┘
```

---

## 6. Blok Belajar & SRS Drill

```
┌──────────────────────────┐       ┌──────────────────────────┐
│        enrollment        │       │        srs_card          │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │       │ PK │ id                  │
│ FK │ siswa_user_id       │       │ FK │ siswa_user_id       │
│ FK │ level_id            │       │ FK │ materi_id           │
│    │ tanggal_daftar      │       │    │ status              │←'baru'|'belajar'|'sulit'|'dikuasai'
│    │ status              │←'aktif'|'lulus'|'berhenti'  │    │ ease / interval_hari│
└──────────────────────────┘       │    │ next_review / count │
                                   │    │ last_review         │
                                   └──────────────────────────┘
```

---

## 7. Blok Mock Exam & CBT

```
┌──────────────────────────┐       ┌──────────────────────────┐
│       mock_exam          │       │      exam_answer         │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │──1:N──│ PK │ id                  │
│ FK │ siswa_user_id       │       │ FK │ mock_exam_id        │
│ FK │ level_id            │       │ FK │ bank_soal_id        │
│    │ format              │←'cbt'|'kertas'  │    │ jawaban_user / benar  │
│    │ tanggal_mulai/selesai│      │    │ waktu_jawab         │
│    │ skor_vocab          │       └──────────────────────────┘
│    │ skor_reading        │
│    │ skor_listening      │       ┌──────────────────────────┐
│    │ skor_total          │←COMPUTED (vocab+reading+listening)       │       exam_timer         │
│    │ result              │←'lulus'|'gagal'  ├──────────────────────────┤
│    │ attempt_ke          │       │ PK │ id                  │
└──────────────────────────┘       │ FK │ mock_exam_id        │
                                   │    │ section             │
┌──────────────────────────┐       │    │ durasi_menit        │
│   hasil_ujian_resmi      │       │    │ started_at / ends_at│
├──────────────────────────┤       └──────────────────────────┘
│ PK │ id                  │
│ FK │ siswa_user_id       │       (Redis caching session ujian
│    │ jenis_ujian         │←'jlpt'|'jft'|'skill_test'   untuk 100+ concurrent)
│    │ level / tanggal     │
│    │ skor                │
│    │ sertifikat_url      │•
│    │ sumber              │←'import'|'manual'
└──────────────────────────┘
```

---

## 8. Blok Diklat Asrama (Sesi Karantina)

```
┌──────────────────────────┐       ┌──────────────────────────┐
│     diklat_session       │       │     peserta_diklat       │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │──N:M──│ PK │ id                  │
│ U  │ kode_angkatan       │← DIPISAH dari kelas.nama_batch  │ FK │ diklat_session_id    │
│    │ tanggal_mulai/selesai│      │ FK │ siswa_user_id        │
│    │ lokasi              │       │    │ status_lulus         │←'lulus'|'tidak'
│    │ jadwal_harian       │       │    │ catatan              │•
│    │ deskripsi           │       └──────────────────────────┘
└──────────────────────────┘
```
> Absensi selama karantina → `absensi_apel` (Blok 3), bukan tabel terpisah.

---

## 9. Blok Dokumen, Pipeline & Penyaluran (BARU — inti SO)

```
┌──────────────────────────┐       ┌──────────────────────────┐
│       berkas_siswa       │       │    pipeline_status       │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │       │ PK │ id                  │
│ FK │ siswa_user_id       │       │ FK │ siswa_user_id       │
│    │ jenis_berkas        │←'ktp'|'kk'|'ijazah'|'surat_ortu'|'mcu'|'paspor'  │    │ tahap               │
│    │ file_url            │       │    │                     │←'screening_mcu'|'diklat_bahasa'|'lulus_ujian'|
│    │ status_verifikasi   │←'menunggu'|'verified'|'revisi'  │    │                     │'siap_matching'|'panggilan_mensetsu'|
│ FK │ verifier_user_id    │•      │    │                     │'lolos_interview'|'ttd_kontrak'|'pengajuan_coe'|
└──────────────────────────┘       │    │                     │'coe_terbit'|'visa_issued'|'tiket_berangkat'
                                   │    │ tanggal_update      │
                                   │    │ catatan             │•
                                   │ FK │ staff_user_id       │
                                   └──────────────────────────┘

┌──────────────────────────┐       ┌──────────────────────────┐
│   mitra_penempatan       │       │        coe_visa         │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │       │ PK │ id                  │
│    │ nama                │       │ FK │ siswa_user_id       │
│    │ jenis               │←'kumiai'|'kaisha'|'tsk'  │    │ coe_number         │•
│    │ negara / kontak     │       │    │ tanggal_coe         │•
│    │ sektor              │←'kaigo'|'manufaktur'|'konstruksi'|'pengolahan_makanan'  │    │ tanggal_visa / expiry│•
│    │ moU_date / status   │       │    │ status              │←'proses'|'terbit'|'ditolak'
└──────────────────────────┘       └──────────────────────────┘

┌──────────────────────────┐       ┌──────────────────────────┐
│       penempatan         │       │       rirekisho         │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │       │ PK │ id                  │
│ FK │ siswa_user_id       │       │ FK │ siswa_user_id       │
│ FK │ mitra_id            │       │    │ versi               │
│    │ sektor / perusahaan │•      │    │ file_url            │
│    │ tanggal_kontrak     │•      │    │ generated_at        │
│    │ hasil_mensetsu      │←'goukaku'|'shippai'  └──────────────────────────┘
└──────────────────────────┘
```

---

## 10. Blok Keuangan

```
┌──────────────────────────┐       ┌──────────────────────────┐
│         invoice          │       │        transaksi        │
├──────────────────────────┤       ├──────────────────────────┤
│ PK │ id                  │──1:N──│ PK │ id                  │
│ FK │ siswa_user_id       │       │ FK │ invoice_id          │
│ U  │ no_invoice          │       │    │ jumlah / tanggal    │
│    │ kategori_biaya      │←'bahasa'|'asrama_makan'|'ujian'|'visa'  │    │ metode              │←'va'|'qris'|'tunai'
│    │ jumlah_total / bayar│       │    │ ref_transaksi       │•
│    │ skema_bayar         │←'lunas'|'dp_angsuran'|'dormant_indent'  │    │ status              │←'sukses'|'gagal'|'pending'
│    │ dp_jumlah           │• (untuk dp_angsuran)  │    │ bukti_url           │•
│    │ sisa_tagihan        │←COMPUTED (jumlah_total − jumlah_bayar)  └──────────────────────────┘
│    │ tanggal_jatuh_tempo │•
│    │ dormant_mulai       │• (indent — layanan/keberangkatan belum datang)
│    │ dormant_alasan      │•
│    │ status              │←'unpaid'|'dp_terbayar'|'cicilan'|'dormant'|'paid'|'pending'|'refund'
└────────────┬─────────────┘
             │ 1:N
             ▼
┌──────────────────────────┐
│      jadwal_cicilan      │
├──────────────────────────┤
│ PK │ id                  │
│ FK │ invoice_id          │
│    │ nomor_angsuran      │
│    │ tanggal_jatuh_tempo │
│    │ jumlah              │
│    │ status              │←'menunggu'|'terbayar'|'terlambat'
└──────────────────────────┘

┌──────────────────────────┐
│      dana_talangan       │
├──────────────────────────┤
│ PK │ id                  │
│ FK │ siswa_user_id       │
│    │ jumlah / sisa       │
│    │ sumber              │←'koperasi_mitra'|'internal_lpk'|'donasi_pemerintah'|'mitra_lain'
│    │ status              │←'aktif'|'lunas'
│    │ keterangan          │•
└──────────────────────────┘
```

---

## 11. Blok Sertifikat

```
┌──────────────────────────┐
│        sertifikat        │
├──────────────────────────┤
│ PK │ id                  │
│ FK │ siswa_user_id       │
│ FK │ level_id            │•
│ U  │ nomor_seri          │
│    │ jenis               │←'internal_lpk'|'jlpt_resmi'|'jft_resmi'|'skill_test'
│    │ qr_code             │  (verifikasi publik)
│    │ jam_belajar         │  (bukti 150–300 jam)
│    │ tanggal_terbit      │
│    │ file_url            │
└──────────────────────────┘
```

---

## Ringkasan Relasi Lintas Blok

| Dari | Ke | Relasi | Keterangan |
|------|-----|--------|------------|
| users | siswa/sensei/pembina/staff_so/admin_keu/pimpinan | 1:1 | Polimorf via `role` |
| siswa | mcu_record, penghuni_kamar, absensi_apel, kesamaptaan_fisik, log_pelanggaran | 1:N | Blok kesehatan & asrama |
| siswa | enrollment, srs_card, mock_exam, hasil_ujian_resmi | 1:N | Blok akademik |
| siswa | berkas_siswa, pipeline_status, coe_visa, penempatan, rirekisho | 1:N | Blok penyaluran (inti SO) |
| siswa | invoice → transaksi, dana_talangan, sertifikat | 1:N | Blok keuangan & sertifikat |
| level | modul, bank_soal, mock_exam, enrollment | 1:N | |
| modul | materi | 1:N | |
| materi | srs_card | 1:N | per siswa |
| kelas | jadwal, absensi_akademik | 1:N | |
| siswa ↔ kelas | enrollment_kelas | N:M | |
| diklat_session ↔ siswa | peserta_diklat | N:M | |
| kamar_asrama | penghuni_kamar, jadwal_piket | 1:N | |
| mitra_penempatan | penempatan | 1:N | |
| bank_soal | exam_answer | 1:N | |
| mock_exam | exam_answer, exam_timer | 1:N | |
| invoice | transaksi | 1:N | |

---

## Open Questions / Trade-off
1. **`bank_soal.pilihan_jawaban` JSON** vs tabel terpisah — asumsi JSON (cukup 4–5 pilihan).
2. **`pipeline_status`** apakah cukup satu baris terakhir per siswa (history per tahap) atau tabel log penuh — asumsi **log penuh** (audit Imigrasi).
3. ~~**`nama_batch` (kelas)** vs **`diklat_session` (karantina)**~~ → **SELESAI (keputusan owner):** entitas & penamaan **DIPISAH** — `kelas.nama_batch` (akademik) vs `diklat_session.kode_angkatan` (karantina); keduanya tetap ada sebagai skenario terpisah.
4. **`exam_timer`** apakah perlu tabel terpisah atau cukup kolom di `mock_exam` — asumsi terpisah karena multi-section.
5. Entitas **`absensi_apel`** menampung apel pagi & Tenko malam; kelas akademik pakai `absensi_akademik` terpisah — konfirmasi pemisahan ini sudah sesuai kebutuhan operasional.

---

## Catatan Field Turunan (keputusan Check 1 §5c)

Dua field ditandai **`←COMPUTED`** dan **dipertahankan** (keputusan owner — bukan dual source of truth):
- `invoice.sisa_tagihan` = `jumlah_total − jumlah_bayar`
- `mock_exam.skor_total` = `skor_vocab + skor_reading + skor_listening`

**Aturan:** field ini **dihitung sistem**, bukan diinput manual. Seluruh tulis/ubah wajib melewati validasi kalkulasi agar tidak kontradiksi dengan field dasarnya. Disimpan untuk optimasi query laporan.
