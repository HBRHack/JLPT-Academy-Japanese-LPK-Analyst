# JLPT Academy — System Design Documentation

Dokumentasi **analisis sistem** untuk **JLPT Academy**: sistem terintegrasi **3-in-1** milik lembaga **LPK & Sending Organization (SO) berizin Kemenaker** yang mengelola perjalanan penuh calon tenaga kerja Indonesia ke Jepang.

| | |
|---|---|
| **Domain** | LPK & Sending Organization (SO) — persiapan kerja ke Jepang |
| **Jalur karir** | Magang 3 Tahun (*Ginou Jisshuusei*) & SSW I–II (*Tokutei Ginou*) |
| **Ujian** | JLPT N5–N1 + JFT-Basic A2 (dual-track) |
| **Status** | Dokumen analisis **DRAFT v0.2** — jawaban bisnis FINAL, menunggu audit §5c |
| **Bahasa** | Indonesia |

---

## 3-in-1: Apa Isinya

```
┌─────────────────────────────────────────────────────────────┐
│  1. LMS DRILL UJIAN                                        │
│     Materi per level · Flashcard SRS · Mock Exam & CBT     │
├─────────────────────────────────────────────────────────────┤
│  2. ERP DIKLAT & KARANTINA ASRAMA                          │
│     Presensi QR · Kedisiplinan · Kesamaptaan fisik · MCU   │
├─────────────────────────────────────────────────────────────┤
│  3. TALENT PIPELINE & PENYALURAN                           │
│     Rirekisho · Kanban 11 tahap · Matching · COE · Visa    │
└─────────────────────────────────────────────────────────────┘
```

Perjalanan siswa: **daftar → belajar & uji → karantina & MCU → penyaluran ke Jepang**, dikunci dua gerbang keras: **keuangan (bayar)** dan **kelayakan (MCU/ujian)**.

---

## Struktur Repositori

```
.
├── PRD.md                          ← Product Requirements Document
├── README.md                       ← File ini
└── docs/
    └── analyst/
        ├── question-framework.md   ← ★ SUMBER KEBENARAN BISNIS (jawaban FINAL)
        ├── business-rules.md       ← BR-001..012 (tipikal + enforcement)
        ├── nfr.md                  ← NFR-01..09 (format QA scenario 6 bagian)
        ├── assumptions-constraints.md  ← AS-01..05, CN-01..06
        ├── NUMBERING-LOG.md        ← Reserved range ID per chapter (blok 50)
        └── 00-Global/
            ├── NOTATION.md         ← ROOT — aturan pemilihan notasi (GLOBAL-00)
            ├── SRS-MASTER.md       ← Spesifikasi kebutuhan sistem (master)
            ├── ERD-MASTER.md       ← ~43 entitas dalam 11 blok (ASCII box-art)
            ├── GLOSSARY.md         ← ~50 istilah domain
            ├── DATA-DICT-MASTER.md ← Kamus data — makna tiap field
            ├── REQUIREMENTS-MATRIX.md  ← Traceability BREQ/SREQ/FR/NFR/TR
            └── PROCESS-FLOW-MASTER.md  ← PF-001..008 (BPMN Mermaid)
```

---

## Urutan Baca Dokumen

1. **`PRD.md`** — gambaran besar produk, persona, scope fitur, state machine pipeline.
2. **`question-framework.md`** — **sumber kebenaran**; semua dokumen lain diturunkan dari sini.
3. **`00-Global/NOTATION.md`** — aturan notasi sebelum baca diagram mana pun (wajib).
4. **`00-Global/SRS-MASTER.md`** — kebutuhan sistem, aktor, tujuan bisnis (G1–G6), roadmap 4 tahap.
5. **`00-Global/ERD-MASTER.md`** + **`DATA-DICT-MASTER.md`** — struktur data & makna tiap field.
6. **`business-rules.md`** — aturan bisnis lengkap dengan level enforcement.
7. **`00-Global/PROCESS-FLOW-MASTER.md`** — alur proses lintas modul (BPMN).
8. **`00-Global/REQUIREMENTS-MATRIX.md`** — traceability requirement → chapter.

---

## Aturan Notasi (Ringkas — GLOBAL-00)

Notasi dipilih berdasarkan **jenis informasi**, bukan selera. Rincian di [`docs/analyst/00-Global/NOTATION.md`](docs/analyst/00-Global/NOTATION.md).

| Notasi | Kapan dipakai | Format wajib |
|---|---|---|
| **Flowchart** | Alur sederhana, linar, **1 aktor** | **ASCII box-art** |
| **BPMN** | Proses bisnis **multi-actor**, handoff, exception | **Mermaid** |
| **Sequence Diagram** | Urutan pesan presisi antar objek (sync/async) | **Mermaid** |
| **Activity Diagram** | Urutan langkah satu use case, step-by-step | **Mermaid** |
| **Use Case Diagram** | Siapa bisa ngapain (scope aktor & hak akses) | **Mermaid** |
| **ERD** | Struktur data & relasi antar entitas | **ASCII box-art** |

> ⚠️ **Catatan teknis:** Mermaid **tidak punya tipe `usecaseDiagram` maupun `bpmn`**. Keduanya dirender memakai `flowchart` + `subgraph` (lihat NOTATION.md §Catatan teknis).

---

## Roadmap Pengembangan

| Tahap | Modul | Isi |
|-------|-------|-----|
| **1 — Fondasi Utama** | Data Master & Siswa · Kelas & Presensi Diklat | Akun 6 peran, profil siswa, jadwal, presensi QR, log kedisiplinan |
| **2 — Akademik Siswa** | Engine Belajar & SRS · Mock Exam & CBT | Materi per level, flashcard SRS, bank soal 12 tipe, timer adaptif, analitik |
| **3 — Operasional Diklat** | Diklat Asrama & MCU · Talent Pipeline | Asrama, kesamaptaan fisik, MCU, Rirekisho, Kanban keberangkatan |
| **4 — Komersial** | Keuangan & Cicilan · Sertifikasi & Analytics | Invoice, payment gateway, dana talangan, e-Sertifikat QR, dasbor |

---

## 6 Aktor Utama

| Aktor | Fokus |
|---|---|
| **Siswa Diklat** | Belajar/drill dari HP, absensi QR, pantau tahapan dokumen, bayar |
| **Sensei / Pengajar** | Input kehadiran & nilai **< 3 ketukan**, kelola materi + bank soal |
| **Pembina Diklat & Asrama** | Absensi Apel/Tenko, rekam kesamaptaan fisik, log pelanggaran |
| **Staff Matching & Penyaluran (SO)** | Gerakkan Kanban, generate Rirekisho, kelola COE/visa |
| **Admin Keuangan / TU** | Invoice per kategori, rekonsiliasi PG, verifikasi berkas |
| **Pimpinan Lembaga** | Dasbor analitik: pass rate, kinerja guru, jumlah berangkat |

---

## Open Questions (Sengaja Ditunda)

Dua keputusan teknis **sengaja dibiarkan kosong** sampai fase implementasi — keputusan owner:

- **A1** — Stack teknologi: `Laravel/Livewire/Alpine` vs `Next.js/Tailwind`
- **A2** — Payment gateway: `Midtrans` vs `Xendit`

Yang sudah final: **A3** (Batch kelas vs Diklat karantina → **dipisah**) dan **A4** (Dana talangan → **multi-sumber**).

---

## Status Validasi §5c (Validation Gate)

| Check | Status |
|---|---|
| 1 · Redundancy | ✅ — field turunan (`sisa_tagihan`, `skor_total`) ditandai `←COMPUTED` |
| 2 · BR vs Data Dict | ✅ |
| 3 · Matrix Completeness | ✅ |
| 4 · UC Overlap | ⏸️ N/A — menunggu chapter BAB-1..8 digarap |
| 5 · Reserved Numbering | ✅ — `NUMBERING-LOG.md` aktif (reserved range blok 50 per chapter) |
| 6 · Value Consistency | ✅ |
| 7 · BACCM | ✅ |
| 8 · Scope-Alignment | ✅ |
| 9 · Notation Consistency | ✅ — 13 diagram Mermaid lolos parse |

---

*Dokumen ini adalah artefak **analisis sistem** (System Analysis), bukan spesifikasi implementasi teknis. Rujukan utama: `question-framework.md` (source of truth bisnis).*
