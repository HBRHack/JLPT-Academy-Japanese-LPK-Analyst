# Non-Functional Requirements: JLPT Academy

> **Dokumen:** NFR global (lintas chapter)
> **Proyek:** JLPT Academy — LPK & SO
> **Format:** QA Scenario 6 bagian (Stimulus Source → Stimulus → Environment → Artifact → Response → Response Measure)
> **Versi:** 0.2

---

## NFR-01 — Performance (kecepatan)
**Kelas:** Runtime
- **Sumber:** Siswa (HP Android)
- **Stimulus:** Membuka modul flashcard/materi; menekan submit jawaban soal
- **Environment:** Jam sibuk (05.30–06.30 WIB apel, 19.00–21.30 WIB drill malam, Sabtu pagi mock serentak)
- **Artifact:** Aplikasi (modul belajar & engine ujian)
- **Response:** Konten tampil / jawaban tercatat
- **Measure:** Buka materi **< 1,5 detik**; submit jawaban **< 500 ms**; streaming audio listening instan tanpa buffering
- **Fit Criterion:** 95% request < 1,5 dtk; 99% submit < 500 ms (diukur APM)

## NFR-02 — Availability (ketersediaan)
**Kelas:** Runtime
- **Sumber:** Gangguan internal/eksternal (server, jaringan)
- **Stimulus:** Fault (crash, down)
- **Environment:** Operasional 24/7 (drill malam & apel pagi kritis)
- **Artifact:** Sistem
- **Response:** Deteksi, failover, pemulihan
- **Measure:** Uptime **≥ 99%** (down maks ~7 jam/bulan); RTO < 2 jam
- **Fit Criterion:** Monitoring uptime bulanan ≥ 99%

## NFR-03 — Scalability (skala & kapasitas)
**Kelas:** Runtime
- **Sumber:** Lonjakan pengguna serentak
- **Stimulus:** 100+ siswa ujian mock serentak; 300–500 siswa aktif simultan
- **Environment:** Jam sibuk & hari ujian serentak
- **Artifact:** Engine ujian + database
- **Response:** Tetap responsif; session ujian di-cache (Redis)
- **Measure:** Stabil hingga **2.500+ siswa/tahun**; 100+ concurrent exam tanpa degradasi
- **Fit Criterion:** Load test 100 concurrent submit < 500 ms

## NFR-04 — Security (keamanan data)
**Kelas:** Runtime
- **Sumber:** Penyerang / akses tak sah
- **Stimulus:** Upaya bocor/modifikasi data pribadi (NIK, KTP/KK, Paspor, rekam medis MCU, keuangan)
- **Environment:** Runtime & penyimpanan
- **Artifact:** Data sensitif & kredensial
- **Response:** Enkripsi, otorisasi per peran, audit
- **Measure:** **AES-256 at-rest**, **TLS 1.3 in-transit**; autentikasi wajib per role
- **Fit Criterion:** Audit keamanan lolos; 0 insiden kebocoran

## NFR-05 — Compliance (kepatuhan regulasi)
**Kelas:** Runtime + Development
- **Sumber:** Regulator (Kemenaker, Imigrasi)
- **Stimulus:** Kewajiban hukum perlindungan data & legalitas LPK-SO
- **Environment:** Operasional
- **Artifact:** Sistem & proses
- **Response:** Penuhi UU PDP (enkripsi, retensi 10 th, hak hapus); dukung audit Kemenaker
- **Measure:** Kepatuhan **UU PDP No. 27/2022**; legalitas Ditjen Binalavotas
- **Fit Criterion:** Opini kepatuhan; prosedur hak-hak subjek data berjalan

## NFR-06 — Usability (kemudahan pakai)
**Kelas:** Runtime
- **Sumber:** Siswa (literasi menengah–bawah), Sensei/Pembina (input kilat)
- **Stimulus:** Navigasi belajar, absensi, input nilai
- **Environment:** HP Android kelas menengah–bawah
- **Artifact:** UI aplikasi
- **Response:** Antarmuka sederhana, ikonik, tombol besar, teks kanji ber-furigana
- **Measure:** Input kehadiran/nilai **< 3 ketukan**; tanpa jargon teknis
- **Fit Criterion:** Uji tugas selesai tanpa bantuan; SUS ≥ 70

## NFR-07 — Offline (akses tanpa kuota)
**Kelas:** Runtime
- **Sumber:** Siswa tanpa kuota / sinyal lemah
- **Stimulus:** Akses materi saat offline
- **Environment:** Offline sementara
- **Artifact:** Modul flashcard & audio
- **Response:** Sajikan dari cache lokal
- **Measure:** Flashcard kanji/kosakata + audio materi aktif **di-caching lokal**
- **Fit Criterion:** Drill & audio tetap jalan tanpa koneksi

## NFR-08 — Operasional (backup & pemulihan)
**Kelas:** Runtime + Development
- **Sumber:** Kegagalan data / bencana
- **Stimulus:** Kehilangan/kerusakan data
- **Environment:** Operasional harian
- **Artifact:** Database & file
- **Response:** Backup otomatis, restore terencana
- **Measure:** Snapshot **harian 02.00 WIB**, retensi **30 hari offsite**, **RPO < 24 jam, RTO < 2 jam**; **cloud DC Region Jakarta**
- **Fit Criterion:** Drill restore < 2 jam; backup harian terverifikasi

## NFR-09 — Maintainability (pemeliharaan konten)
**Kelas:** Development
- **Sumber:** Guru konten / admin
- **Stimulus:** Update bank soal & materi
- **Environment:** CMS terpisah
- **Artifact:** Bank soal & modul materi
- **Response:** Update konten tanpa ganggu modul siswa
- **Measure:** CMS independen; versioning konten
- **Fit Criterion:** Guru konten bisa update soal sendiri tanpa deploy aplikasi siswa

---

## Open Questions / Trade-off
1. **NFR-01** target < 500 ms submit — perlu dikunci di environment tertentu saja, atau semua environment?
2. **NFR-03** 100+ concurrent exam — perlu autoscaling atau cukup provisioning statis DC Jakarta?
3. **NFR-07** offline caching — seberapa besar kuota cache yang wajar di HP siswa kelas menengah–bawah?
4. Konflik **NFR-04 (security)** vs **NFR-06 (usability)** — enkripsi ketat bisa menambah langkah login; perlu trade-off (mis. biometrik)?
