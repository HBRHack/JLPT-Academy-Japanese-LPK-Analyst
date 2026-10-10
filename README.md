# JLPT Academy — System Design Documentation

Analysis & System Design Portfolio — Sistem Terintegrasi LPK & Sending Organization (SO) Jepang

| Parameter | Keterangan |
|---|---|
| **Status proyek** | Analysis-first / design portfolio — **DRAFT v0.3** (jawaban bisnis FINAL, dokumen teknis menunggu audit §5c) |
| **Bentuk** | Dokumentasi analisis: requirement, data model, business rules, process flow, state machine, notation governance, traceability matrix |
| **Implementasi aplikasi** | Bukan fokus repository ini — tersedia sebagai **jalur implementasi yang direkomendasikan** (lihat §7) |
| **Bahasa dokumen** | Indonesia |
| **Open question tersisa** | A1 (stack) & A2 (payment gateway) — **sengaja ditunda** ke fase implementasi |

> 📄 **Mulai dari mana?** — **`PRD.md`** = spesifikasi produk lengkap (persona, ruang lingkup, state machine, business rules, data model, NFR, tech stack). **File ini** = pengantar repo: apa ini, untuk siapa, struktur dokumen, urutan baca, dan apa yang saya demonstrasikan.

---

## 1. Apa sebenarnya proyek ini?

**JLPT Academy** adalah simulasi analisis sistem untuk lembaga **LPK & Sending Organization (SO) berizin Kemenaker** yang mengelola perjalanan penuh calon tenaga kerja Indonesia ke Jepang — dari daftar, drill bahasa, ujian, karantina, sampai berangkat kerja.

Sistemnya **3-in-1**:

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

Repository ini sengaja dibuat **analysis-first**. Saya tidak menjadikan pembuatan aplikasi sebagai tujuan utama. Yang ingin ditunjukkan adalah bagaimana sebuah masalah bisnis diterjemahkan menjadi:

- kebutuhan bisnis dan requirement (BREQ/SREQ/FR/NFR/TR);
- aktor, hak akses, dan tanggung jawab (6 peran);
- master data dan relasi data (41 entitas, 11 blok);
- business rules dengan level enforcement;
- process flow dan state machine (pipeline penyaluran 11 tahap);
- hubungan antar-modul dan gerbang lintas chapter;
- kebutuhan non-fungsional (format QA scenario 6 bagian);
- asumsi dan constraint;
- sambungan ke sistem eksternal (6 interface);
- serta **governance penomoran ID** dan **konsistensi notasi** antar dokumen.

Dengan pendekatan ini, interviewer dapat membaca cara saya berpikir sebagai analis/system designer, tanpa harus terlebih dahulu menjalankan program.

---

## 2. Repository ini ditujukan kepada siapa?

### Untuk interviewer / hiring team

- IT Business Analyst
- System Analyst
- Solution Architect
- System / Software Architecture track
- posisi IT yang berhubungan dengan transformasi proses bisnis

### Untuk technical interviewer

Bagian paling relevan adalah **model data 41 entitas** (terutama blok Keuangan dengan 3 skema bayar), **state machine pipeline penyaluran 11 tahap**, **gerbang keras antar chapter** (BR-004, BR-006), **governance penomoran ID per chapter**, serta **alasan pemilihan notasi diagram**.

### Untuk pembaca non-teknis

Tidak perlu memahami teknologi untuk mengikuti proyek ini. Baca **`PRD.md` §1** (Problem Statement) lalu **§5** (State Machine) — dari sana sudah terlihat alur bisnisnya utuh.

### Catatan penting

Ini adalah proyek latihan dan portofolio, **bukan representasi sistem produksi** dan bukan klaim bahwa seluruh prosedur LPK/SO telah dimodelkan secara lengkap. Seluruh detail sensitif dalam dokumen telah disamarkan untuk publikasi.

---

## 3. Kenapa tidak langsung membuat program?

Karena pada proyek ini program bukan titik utama yang ingin saya demonstrasikan.

Sebuah aplikasi dapat dibuat dari requirement yang sudah tersedia, tetapi nilai analitisnya justru terlihat **sebelum kode ditulis**: apa masalahnya, siapa yang bertanggung jawab, data apa yang diperlukan, kapan status berubah, apa yang tidak boleh terjadi, dan bagaimana modul saling memengaruhi.

Ditambah lagi, ada dua keputusan teknis yang **sengaja dibiarkan terbuka** (A1 stack, A2 payment gateway — `PRD.md` §9) — keduanya keputusan owner yang dipilih saat implementasi. Mengisi keduanya sekarang justru akan membuat dokumen berpura-pura lebih final dari kenyataannya.

Jadi repository ini diposisikan sebagai:

> **"Bukti bahwa saya mampu memetakan masalah bisnis menjadi rancangan sistem yang dapat diimplementasikan."**

Implementasi tetap dipikirkan sejak awal, tetapi diperlakukan sebagai jalur implementasi yang direkomendasikan, bukan sebagai pusat portofolio.

---

## 4. Struktur Dokumentasi Repository

Struktur utama memisahkan **analisis global**, **analisis per chapter** (belum digarap), dan **dokumen pendukung**.

```
.
├── PRD.md                                ← ★ SPESIFIKASI PRODUK LENGKAP
├── README.md                             ← file ini (pengantar)
│
└── docs/
    └── analyst/                          # ARTIFAK ANALISIS INTI
        ├── question-framework.md         # ★ SUMBER KEBENARAN BISNIS (jawaban FINAL)
        ├── business-rules.md             # 12 BR (definitional + behavioural/enforcement)
        ├── nfr.md                        # 9 NFR — format QA scenario 6 bagian
        ├── assumptions-constraints.md    # AS 5, CN 6
        ├── NUMBERING-LOG.md              # reserved range ID per chapter (blok 50)
        │
        └── 00-Global/
            ├── NOTATION.md               # ROOT — aturan pemilihan notasi (GLOBAL-00)
            ├── SRS-MASTER.md             # G1–G6, aktor, UC-001..008, IF-01..06
            ├── ERD-MASTER.md             # 41 entitas, 11 blok (ASCII box-art)
            ├── GLOSSARY.md               # 47 istilah
            ├── DATA-DICT-MASTER.md       # kamus field — 10 blok
            ├── REQUIREMENTS-MATRIX.md    # traceability BREQ/SREQ/FR/NFR/TR
            └── PROCESS-FLOW-MASTER.md    # PF-001..008 (BPMN Mermaid, swimlane)
```

### Skala dokumen

| Keluarga ID | Jumlah | Sumber |
|---|---|---|
| BREQ (Business Requirements) | 5 | `docs/analyst/00-Global/REQUIREMENTS-MATRIX.md` |
| SREQ (Stakeholder Requirements) | 5 | idem |
| FR (Functional — global/inti) | 12 | idem — *tumbuh per chapter saat BAB-1..8 digarap* |
| NFR | 9 | `docs/analyst/nfr.md` |
| TR (Transition) | 2 | `REQUIREMENTS-MATRIX.md` |
| UC (Use Case — anchor module-level) | 8 | `docs/analyst/00-Global/SRS-MASTER.md` §5 |
| BR (Business Rules) | 12 | `docs/analyst/business-rules.md` |
| PF (Process Flow — BPMN Mermaid) | 8 | `docs/analyst/00-Global/PROCESS-FLOW-MASTER.md` |
| Goals (G) | 6 | `PRD.md` §2 |
| Interface eksternal (IF) | 6 | `SRS-MASTER.md` §6 |
| Asumsi (AS) / Constraint (CN) | 5 / 6 | `docs/analyst/assumptions-constraints.md` |
| Entitas ERD | 41 (11 blok) | `docs/analyst/00-Global/ERD-MASTER.md` |
| Istilah glossary | 47 | `docs/analyst/00-Global/GLOSSARY.md` |
| Diagram Mermaid tervalidasi | 11 — **lolos `mermaid.parse()`** | seluruh `docs/analyst/` |

### Catatan struktur

- Chapter (`BAB-1..8/`) **belum ada** — akan berisi `USE-CASE.md` + `PROCESS-FLOW.md` per chapter, dijalankan lewat Validation Gate §5c (Check 4 *UC Overlap* & Check 5 *Reserved Numbering* baru bisa jalan setelah chapter ada).
- Setiap PF-XXX yang dibuat di chapter **wajib diindeks** di `PROCESS-FLOW-MASTER.md`.
- `NUMBERING-LOG.md` menyimpan **reserved range per chapter (blok 50)** + kolom *Next available* — dipakai tiga skill berbeda (`grill-with-docs`, `design-reviewer`, `extract-code`) supaya ID tidak tumpang-tindih.

---

## 5. Why This Repository Is Interview-Friendly

Repository ini dirancang supaya interviewer dapat membaca artefaknya terlebih dahulu, lalu melakukan *deep-dive* pada reasoning saya.

### Urutan baca yang disarankan

```
README.md                                   ← anda di sini
   ↓
PRD.md                                      ← spesifikasi produk lengkap
   ↓
docs/analyst/question-framework.md          ← source of truth bisnis
   ↓
docs/analyst/00-Global/NOTATION.md          ← WAJIB sebelum baca diagram
   ↓
docs/analyst/00-Global/SRS-MASTER.md
   ↓
docs/analyst/business-rules.md
   ↓
docs/analyst/00-Global/ERD-MASTER.md + DATA-DICT-MASTER.md
   ↓
docs/analyst/00-Global/PROCESS-FLOW-MASTER.md + SRS-MASTER §5 (Use Case)
   ↓
docs/analyst/nfr.md + 00-Global/REQUIREMENTS-MATRIX.md
   ↓
docs/analyst/NUMBERING-LOG.md                ← governance penomoran
```

Dengan urutan itu, pembaca bisa melihat hubungan antara **keputusan bisnis** dan **keputusan teknis/dokumental**, bukan hanya melihat diagram yang berdiri sendiri.

### Dua hal yang membedakan repo ini dari dokumentasi analisis biasa

**1. Governance notasi (GLOBAL-00).** Notasi dipilih berdasarkan **jenis informasi**, bukan selera:

| Notasi | Kapan dipakai | Format wajib |
|---|---|---|
| Flowchart | alur sederhana, linar, **1 aktor** | **ASCII box-art** |
| BPMN | proses bisnis **multi-actor**, handoff, exception | **Mermaid** |
| Sequence / Activity / Use Case | urutan pesan, langkah, siapa bisa ngapain | **Mermaid** |
| ERD | struktur data & relasi | **ASCII box-art** |

> ⚠️ **Catatan teknis:** Mermaid **tidak punya tipe `usecaseDiagram` maupun `bpmn`** (diverifikasi di Mermaid v9 & v11 — keduanya menolak). Keduanya dirender memakai `flowchart` + `subgraph`. Ini didokumentasikan di `NOTATION.md` §Catatan teknis, bukan disembunyikan.

**2. Validation Gate §5c — 9 check lintas dokumen:**

| # | Check | Status |
|---|---|---|
| 1 | Redundancy (field turunan ditandai `←COMPUTED`) | ✅ |
| 2 | BR vs Data Dictionary | ✅ |
| 3 | Matrix Completeness | ✅ |
| 4 | UC Overlap | ⏸️ N/A — menunggu chapter BAB-1..8 |
| 5 | Reserved Numbering | ✅ — `NUMBERING-LOG.md` aktif (blok 50 per chapter) |
| 6 | Value Consistency (literal vs Value List) | ✅ |
| 7 | BACCM | ✅ |
| 8 | Scope-Alignment | ✅ |
| 9 | Notation Consistency | ✅ — **11 diagram Mermaid lolos `mermaid.parse()`** |

Check 4 & 5 sengaja dibiarkan terbuka karena chapter-nya memang belum digarap — bukan karena dilupakan.

---

## 6. What I Am Demonstrating

Repository ini tidak dimaksudkan untuk membuktikan bahwa saya bisa membuat sebanyak mungkin halaman atau fitur.

Yang ingin saya tunjukkan adalah kemampuan untuk:

> **Problem → Requirement → Data → Rule → Process → State → Integration → Architecture → Governance**

### Contoh konkret — satu siswa dari daftar sampai berangkat

```
Siswa mendaftar & enroll level
   ↓
Data master tersimpan (terenkripsi — BR-007)
   ↓
Presensi QR 2 moda → jam belajar terakumulasi (BR-011)
   ↓
Drill SRS + materi → progress per level
   ↓
Mock exam → timer adaptif per section (BR-002)
   ↓
Skor dihitung: total ≥ ambang DAN sectional ≥ ambang (BR-003)
   ↓
MCU dinyatakan Fit? (BR-006)  ── Unfit ──► skema banding [OPEN]
   ↓ Fit
Invoice: lunas / DP+angsuran / dormant (BR-012)
   ↓ lunas (BR-004)
Sertifikat terbit + bukti 150–300 jam (BR-005)
   ↓
Pipeline 11 tahap → matching → Mensetsu → COE → visa → berangkat
   ↓
Setiap perpindahan Kanban diaudit (BR-008)
   ↓
Dasbor pimpinan: pass rate, jumlah berangkat (G1, G2)
```

### Pada titik ini, interviewer dapat menguji saya dengan pertanyaan lanjutan seperti:

- Kenapa **DP atau cicilan yang berjalan tidak cukup** untuk menerbitkan sertifikat?
- Apa bedanya `kelas.nama_batch` dengan `diklat_session.kode_angkatan`, dan kenapa keduanya dipisah?
- Apa yang terjadi kalau siswa dinyatakan MCU **Unfit** — ke mana pipeline-nya?
- Bagaimana sistem mencegah status pipeline diubah sembarang role?
- Kenapa `invoice.sisa_tagihan` disimpan meski nilainya turunan?
- Siapa yang boleh memakai nomor BR-051, dan bagaimana mencegah dua chapter memakai nomor yang sama?
- Kenapa Use Case digambar dengan `flowchart` + `subgraph`, bukan `usecaseDiagram`?
- Kalau status `dormant`, kenapa pengingat jatuh tempo harus dinonaktifkan?
- Apa konsekuensi kalau gerbang BR-004 dilonggarkan?

Jawaban terhadap pertanyaan tersebut **diturunkan dari artefak yang ada di `docs/analyst/`**, bukan dari ingatan.

---

## 7. Development Path (Bila Nanti Diimplementasikan)

Apabila simulasi ini dilanjutkan menjadi aplikasi, urutan implementasi yang disarankan:

```
Pilih stack (A1) + payment gateway (A2)   ← satu-satunya keputusan yang tertunda
      ↓
Database Schema (dari ERD-MASTER 41 entitas)
      ↓
Seeder / Dummy Data (6 peran, level JLPT, bank soal)
      ↓
CRUD Modul Inti (siswa, kelas, jadwal, presensi)
      ↓
State Machine Pipeline 11 Tahap + enforcement BR-006/003/004/008
      ↓
Engine Belajar & SRS → Mock Exam / CBT (timer adaptif + scoring)
      ↓
Keuangan: invoice + 3 skema bayar (DP / Dormant / Angsuran) + `jadwal_cicilan`
      ↓
Integrasi IF-01 (payment gateway) + IF-02 (WhatsApp) dengan fallback manual
      ↓
Sertifikat QR + Dasbor Analytics
      ↓
Validation & Feature Tests
      ↓
Optional Deployment Demo
```

**Fokus testing pertama adalah dua area yang paling mudah rusak secara logika:**

1. **Gerbang BR-004** — DP terbayar sebagian atau status `dormant` → sertifikat **tidak boleh** terbit.
2. **Perubahan status pipeline** — selalu mengikuti business rule (MCU Fit, skor lulus, lunas), **bukan input bebas role**.

---

## 8. Limitations

Model ini sengaja dibatasi agar dapat dikerjakan sebagai *solo-project* dan tetap terbaca dalam sesi interview.

**Beberapa hal yang belum dimodelkan secara penuh antara lain:**

- **chapter BAB-1..8 belum digarap** — Use Case & Process Flow detail per chapter masih menyusul; karena itu FR atomik masih 12 (global), bukan ratusan
- inkonsistensi gerbang di state machine (A5, `PRD.md` §11) — **baru terdeteksi & belum diputuskan**
- jalur **banding MCU Unfit** (PF-005) — masih *open*
- **rematch** setelah gagal Mensetsu (PF-006) — masih *open*
- **batas maksimum periode dormant** (PF-007) — masih *open*
- urutan **bayar vs MCU** di PF-001 — masih *open*
- kebutuhan **JFT-Basic** belum punya FR sendiri (aturan lulus berbeda dari JLPT) — perlu chapter khusus atau subset BAB-4
- belum ada pemetaan ke **test case** (kolom *Validate* di matrix) — menyusul setelah acceptance criteria ditulis
- **stakeholder register, RACI, change-management** — dibatalkan dari scope
- **19 Architecture Decision Records (ADR)** — dipantau lewat `NUMBERING-LOG.md`, tetapi file fisiknya tidak disertakan di repository ini

Dokumen dalam repository ini juga telah diredaksi untuk publikasi: kredensial contoh disamarkan, domain disamarkan, dan detail teknis keamanan yang bersifat sensitif diringkas.

Karena itu, pembaca sebaiknya melihat proyek ini sebagai **analisis dan system design simulation, bukan blueprint produksi** untuk lembaga sungguhan.

---

## 9. Closing

Saya tidak sedang menunjukkan "aplikasi LPK yang sudah jadi".

Saya sedang menunjukkan bagaimana saya membedah sebuah domain bisnis — perjalanan seorang calon tenaga kerja Indonesia menuju Jepang — menemukan aturan penting (gerbang MCU, kelulusan, dan keuangan), menghubungkan data dan proses, lalu menurunkannya menjadi rancangan sistem yang siap diimplementasikan, **lengkap dengan governance supaya dokumentasinya sendiri tidak berantakan saat tumbuh**.

Repository ini adalah **analysis portfolio** dengan implementasi sebagai langkah lanjutan, bukan syarat utama untuk memahami hasil analisis.

---

## Source of Decisions

Keputusan fungsional dan teknis pada README ini mengacu pada dokumen berikut:

| Dokumen | Yang diputuskan |
|---|---|
| `PRD.md` | lingkup produk, persona/role, ruang lingkup 8 modul, state machine, G1–G6, business rules, data model, NFR, tech stack, scope-cut, A1–A5 |
| `docs/analyst/question-framework.md` | **sumber kebenaran bisnis** — semua jawaban FINAL (A–F) |
| `docs/analyst/00-Global/SRS-MASTER.md` | aktor, UC-001..008, IF-01..06, asumsi terbuka |
| `docs/analyst/business-rules.md` | 12 BR + level enforcement (definitional/behavioural) |
| `docs/analyst/00-Global/ERD-MASTER.md` | 41 entitas dalam 11 blok, relasi lintas blok, field `←COMPUTED` |
| `docs/analyst/00-Global/DATA-DICT-MASTER.md` | makna & validasi tiap field, 10 blok |
| `docs/analyst/00-Global/PROCESS-FLOW-MASTER.md` | PF-001..008 (BPMN Mermaid) + relationship map lintas modul |
| `docs/analyst/nfr.md` | 9 NFR format QA scenario 6 bagian |
| `docs/analyst/00-Global/REQUIREMENTS-MATRIX.md` | traceability BREQ/SREQ/FR/NFR/TR |
| `docs/analyst/00-Global/NOTATION.md` | **GLOBAL-00** — aturan pemilihan notasi + catatan keterbatasan Mermaid |
| `docs/analyst/NUMBERING-LOG.md` | inventaris otoritatif reserved range seluruh keluarga ID |
| `docs/analyst/assumptions-constraints.md` | AS-01..05, CN-01..06 |
