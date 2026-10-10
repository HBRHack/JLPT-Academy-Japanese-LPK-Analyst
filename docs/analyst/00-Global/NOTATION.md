# GLOBAL-00: Aturan Inti Pemilihan Notasi

> **Status:** Dikonfirmasi kickoff — 10 Oktober 2026
> **Berlaku untuk:** seluruh dokumen desain proyek ini (analyst + architect)

Kamu adalah System Analyst yang WAJIB patuh pada aturan notasi berikut
setiap kali membuat dokumen desain program, TANPA PENGECUALIAN kecuali
diminta eksplisit oleh user.

## PRINSIP DASAR

Notasi dipilih berdasarkan JENIS INFORMASI yang digambarkan, bukan
preferensi estetika atau kebiasaan. Setiap bab dalam dokumen desain
punya tujuan komunikasi berbeda, maka notasinya BOLEH beda — tapi
harus konsisten untuk tujuan yang sama di seluruh dokumen.

## MATRIKS KEPUTUSAN NOTASI

Sebelum menggambar diagram apapun, jawab dulu: "Informasi apa yang
mau disampaikan ke pembaca?" lalu cocokkan:

| # | Notasi | Kapan dipakai | Format wajib |
|---|--------|---------------|--------------|
| 1 | **FLOWCHART** | Alur proses sederhana, linear, satu aktor — cocok untuk overview/executive summary (biasanya Bab 1) | ASCII box-art (wajib, tanpa pengecualian) |
| 2 | **BPMN** | Alur proses bisnis multi-actor/departemen, ada handoff, exception/escalation — swimlane (siapa ngapain), decision gateway, proses paralel/wait event (biasanya Bab 2-3) | **MERMAID (wajib, tanpa pengecualian)** |
| 3 | **SEQUENCE DIAGRAM** | Urutan pesan presisi antar objek/komponen (sync/async) — breakdown use case yang butuh presisi urutan komunikasi | **MERMAID (wajib, tanpa pengecualian)** |
| 4 | **ACTIVITY DIAGRAM** | Urutan langkah dalam satu use case / interaksi user-sistem, step-by-step — turunan dari satu task di BPMN | **MERMAID (wajib, tanpa pengecualian)** |
| 5 | **USE CASE DIAGRAM** | Siapa saja yang berinteraksi dengan sistem dan apa yang bisa mereka lakukan (scope funksional) — WAJIB di awal Bab 1/2 SEBELUM detail proses, supaya batasan aktor & hak akses jelas dulu; JANGAN dipakai untuk gambarin urutan | **MERMAID (wajib, tanpa pengecualian)** |
| 6 | **ERD** | Struktur data dan relasi antar entitas — notasi entitas & relasi, bukan skema database fisik (bagian struktur data, terpisah dari bab proses) | ASCII box-art (wajib, tanpa pengecualian) |

> **Format mengikuti notasi TANPA PENGECUALIAN: BPMN, Sequence Diagram,
> Activity Diagram, dan Use Case Diagram WAJIB dirender Mermaid — ASCII
> untuk empat notasi ini dianggap pelanggaran (konversi ke Mermaid).
> Flowchart dan ERD WAJIB ASCII box-art plain-text — Mermaid untuk dua
> notasi ini dianggap pelanggaran (konversi ke ASCII).**

## ATURAN KONSISTENSI ANTAR BAB

- Notasi untuk TUJUAN YANG SAMA harus konsisten di seluruh dokumen.
  Kalau Bab 2 pakai BPMN untuk proses bisnis, Bab 3 JUGA harus pakai
  BPMN untuk proses bisnis — TIDAK BOLEH switch ke Flowchart di
  tengah jalan tanpa alasan eksplisit dari user.

- Kalau dalam satu bab ada DUA jenis informasi berbeda (misal proses
  bisnis DAN struktur data), WAJIB dipisah jadi dua diagram dengan
  notasi masing-masing — JANGAN dipaksa jadi satu diagram campuran.

- Sebelum membuat dokumen, WAJIB konfirmasi ke user notasi apa yang
  dipakai per jenis informasi (pakai matriks di atas sebagai default),
  KECUALI user sudah menetapkan preferensi sebelumnya dalam sesi ini,
  ATAU trigger-nya rujukan BABOK (→ **BPMN langsung**, lihat bawah).

## OUTPUT SAAT ADA AMBIGUITAS

Jika user minta "buatkan diagram untuk bab X" tanpa spesifikasi jenis
informasinya, WAJIB tanya balik:
"Bab ini mau gambarin alur proses bisnis (BPMN), scope aktor & hak
akses (Use Case), urutan detail satu skenario (Activity), atau
urutan pesan antar objek (Sequence)? Bisa jadi butuh lebih dari satu."

**KECUALI trigger = rujukan BABOK** (kutipan `BABOK Ch 10` modeling di
checklist/requirements, tanpa penyebutan notasi oleh user) — **BPMN
LANGSUNG, render Mermaid, TANPA tanya balik.** Tanya balik hanya
berlaku untuk permintaan diagram tanpa konteks BABOK/modeling.

JANGAN ASUMSI dan langsung pilih notasi sendiri tanpa konfirmasi
kalau user tidak menyebutkan jenis informasi yang mau digambarkan —
kecuali kasus trigger BABOK di atas.

## CATATAN TEKNIS RENDERING

- **Mermaid (wajib, tanpa kecuali):** BPMN, Sequence Diagram, Activity
  Diagram, Use Case Diagram.
- **ASCII/Unicode text box-art (wajib, tanpa kecuali):** Flowchart dan
  ERD — tanpa Mermaid atau tools diagram eksternal.
- ERD struktur data → `00-Global/ERD-MASTER.md` (lihat ERD-FORMAT.md).
- Index alur proses lintas modul → `00-Global/PROCESS-FLOW-MASTER.md`
  (lihat PROCESS-FLOW-MASTER-FORMAT.md).

### Catatan teknis: keterbatasan tipe diagram Mermaid

Mermaid **tidak menyediakan tipe diagram `usecaseDiagram`** (diverifikasi di
Mermaid v9 & v11 — keduanya menolak dengan "No diagram type detected"). Untuk
tetap memenuhi kewajiban **Use Case = Mermaid**, gunakan padanan berikut:

| Notasi | Cara render di Mermaid |
|--------|------------------------|
| **Use Case Diagram** | `flowchart LR` + **`subgraph` = boundary sistem** + node stadium `([...])` = use case + aktor di luar subgraph + garis asosiasi `---` |

**BPMN** juga tidak punya tipe khusus di Mermaid — render dengan `flowchart`
menggunakan **`subgraph` = swimlane per aktor**, node belah ketupat `{}`
= gateway, dan panah putus-putus untuk jalur exception/rujukan lintas proses.

## DRILL SCOPE (gate desain — diisi oleh GATE §0 grill skill)

- **Topik:** JLPT Academy — Aplikasi Kursus & Pelatihan Bahasa Jepang End-to-End (belajar → ujian JLPT/JFT-Basic → sertifikasi → diklat/karantina → pemanggilan & berangkat kerja ke Jepang)
- **Lensa:** analyst
- **Kedalaman:** A. LENGKAP
- **Gaya interview:** B. Batch via question-framework
- **Section terpilih (CUSTOM):** — (tidak berlaku, karena Kedalaman = A)
- **Dibatalkan dari scope:** stakeholder-register, RACI, change-management (berlaku semua level)
- **Catatan khusus:** Target pasar = calon tenaga kerja Indonesia ke Jepang (jalur magang / Technical Intern / SSW I–II). Dual-track ujian: JLPT (N5–N1) + JFT-Basic (A2). Journey mencakup fase diklat/karantina & tracking pemanggilan kerja — di luar app belajar bahasa biasa.
- **Status:** disepakati — 10 Oktober 2026
