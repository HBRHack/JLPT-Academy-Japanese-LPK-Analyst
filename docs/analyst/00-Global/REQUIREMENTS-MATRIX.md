# REQUIREMENTS-MATRIX: JLPT Academy

> **Dokumen:** Index requirement dengan label tipe & penanda chapter
> **Proyek:** JLPT Academy — LPK & SO
> **Label tipe:** **BREQ** (business requirement/tujuan) · **SREQ** (stakeholder) · **FR** (functional) · **NFR** (non-functional) · **TR** (transition)
> **Versi:** 0.2

> FR atomik akan bertambah saat chapter digarap (§5a–5c). Baris di bawah adalah requirement **global/inti** hasil sinkronisasi `question-framework.md`.

---

## Business Requirements (BREQ) — tujuan bisnis

| ID | Requirement | Target/Metrik | Chapter |
|----|-------------|---------------|---------|
| BREQ-01 | Lembaga meluluskan siswa yang lolos ujian bahasa | Pass rate **≥ 85%** | BAB-3, BAB-4 |
| BREQ-02 | Lembaga menyukseskan penyaluran kerja ke Jepang | **200+ berangkat/tahun**; gagal wawancara **< 5%** | BAB-6 |
| BREQ-03 | Lembaga menumbuhkan skala & menjaga integritas | 300–500 siswa simultan, **zero-deserter**, akreditasi A | BAB-1, BAB-6 |
| BREQ-04 | Administrasi lembaga menjadi efisien | Waktu admin turun **≥ 50%** | BAB-2, BAB-7 |
| BREQ-05 | Kepatuhan perlindungan data siswa | **0 insiden**; UU PDP | lintas chapter |

## Stakeholder Requirements (SREQ)

| ID | Requirement | Aktor | Chapter |
|----|-------------|-------|---------|
| SREQ-01 | Siswa bisa belajar/drill mandiri dari HP | Siswa | BAB-3 |
| SREQ-02 | Siswa & orang tua menerima notifikasi (jadwal, tagihan, wawancara) | Siswa | lintas chapter |
| SREQ-03 | Sensei/Pembina input kehadiran/nilai **< 3 ketukan** | Sensei/Pembina | BAB-2 |
| SREQ-04 | Staff SO memindahkan status Kanban pipeline saat ada kabar Jepang | Staff SO | BAB-6 |
| SREQ-05 | Pimpinan melihat dasbor pass rate & kinerja | Pimpinan | BAB-8 |

## Functional Requirements (FR) — inti (tumbuh per chapter)

| ID | Requirement | Terkait BR | Chapter |
|----|-------------|-----------|---------|
| FR-01 | Sistem mengunci mock exam ke level enrollment siswa | BR-001 | BAB-4 |
| FR-02 | Sistem menerapkan timer adaptif per section & auto-submit | BR-002 | BAB-4 |
| FR-03 | Sistem menghitung kelulusan (total + sectional) otomatis | BR-003 | BAB-4 |
| FR-04 | Sistem menerbitkan sertifikat setelah modul+mock+lunas | BR-004, BR-005 | BAB-8 |
| FR-05 | Sistem mengunci pipeline bila MCU tidak Fit | BR-006 | BAB-5, BAB-6 |
| FR-06 | Sistem mencatat jejak audit setiap perpindahan pipeline | BR-008 | BAB-6 |
| FR-07 | Sistem mencatat presensi 2 moda (akademik & apel) | BR-011 | BAB-2 |
| FR-08 | Sistem menyediakan retake bimbingan 1x untuk siswa gagal | BR-010 | BAB-3 |
| FR-09 | Sistem mengelola invoice per kategori & cicilan | BR-012 | BAB-7 |
| FR-10 | Sistem mengelola dana talangan multi-sumber (A4) | — | BAB-7 |
| FR-11 | Sistem menerapkan **3 skema bayar: DP, Dormant (indent), Angsuran** + jadwal cicilan otomatis | BR-012 | BAB-7 |
| FR-12 | Sistem menahan jatuh tempo & pengingat saat `status='dormant'` | BR-012 | BAB-7 |

## Non-Functional Requirements (NFR)

| ID | Requirement | Metrik | Chapter |
|----|-------------|--------|---------|
| NFR-01 | Performance | materi < 1,5 dtk; submit < 500 ms | lintas chapter |
| NFR-02 | Availability | uptime ≥ 99% | lintas chapter |
| NFR-03 | Scalability | 300–500 simultan → 2.500+/th; 100+ concurrent exam | lintas chapter |
| NFR-04 | Security | AES-256 + TLS 1.3 | lintas chapter |
| NFR-05 | Compliance | UU PDP + Kemenaker | lintas chapter |
| NFR-06 | Usability | input < 3 ketukan; furigana | lintas chapter |
| NFR-07 | Offline | cache flashcard/audio | BAB-3 |
| NFR-08 | Operasional | backup harian, RPO<24h/RTO<2h, DC Jakarta | lintas chapter |
| NFR-09 | Maintainability | CMS konten terpisah | BAB-3, BAB-4 |

## Transition Requirements (TR)

| ID | Requirement | Kedaluwarsa | Chapter |
|----|-------------|-------------|---------|
| TR-01 | Import data siswa lama via template Excel | Setelah migrasi selesai | BAB-1 |
| TR-02 | Import/inventaris bank soal existing lembaga | Setelah CMS konten terisi penuh | BAB-4 |

---

## Relasi Traceability (ringkas)

| Dari | Ke | Tipe |
|------|-----|------|
| BREQ-01 | FR-03, FR-08 | Derive |
| BREQ-02 | FR-05, FR-06 | Derive |
| BR-003 | FR-03 | Satisfy |
| NFR-03 | FR-02 | Depends-Necessity |

---

## Open Questions / Trade-off
1. FR atomik per chapter belum lengkap — akan bertambah saat BAB-1..8 digarap (§5a).
2. Belum ada pemetaan ke **test case** (kolom Validate) — menyusul setelah acceptance criteria ditulis.
3. Kebutuhan **JFT-Basic** (CBT, aturan lulus berbeda dari JLPT) belum punya FR sendiri — perlu chapter khusus atau subset BAB-4.
