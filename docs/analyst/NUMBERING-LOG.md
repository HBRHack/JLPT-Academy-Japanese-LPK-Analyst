# NUMBERING-LOG: JLPT Academy

> **Dokumen:** Log penomoran ID — reserved range per chapter + "Next available"
> **Proyek:** JLPT Academy — LPK & Sending Organization (SO)
> **Fungsi:** Mencegah **tumpang-tindih nomor ID** antar chapter & menjaga urutan tetap terstruktur (bukan acak).
> **Dipakai oleh:**
> - `analyst-grill-with-docs` **§5c Check 5 — Reserved Numbering Check** (baca range sebelum assign BR baru)
> - `analyst-design-reviewer` **Check 5 — Numbering** (flag gap / ID di luar range)
> - `analyst-extract-code` **Check 5 — Numbering** (BR hasil inferensi ambil nomor dari block chapter, update "Next available")
>
> **Versi:** 0.1

---

## Aturan Penomoran

1. **Blok per chapter = 50 nomor.** Kalau satu chapter butuh lebih dari 50, buka blok **cadangan** (lihat §Cadangan) — **jangan** menembus range chapter berikutnya.
2. **Sebelum generate ID baru** (terutama BR/FR/UC/PF), **wajib baca "Next available"** dari tabel di bawah, ambil nomor dari sana, lalu **UPDATE kolomnya**.
3. **Jangan pernah pakai ulang nomor lama** (legacy) meski ID-nya sudah dihapus dari dokumen — nomor yang pernah terbit dianggap terbakar (audit trail).
4. **Gap = warning.** Urutan tidak berurutan / lompat tidak wajar → tanda proses generate tidak terstruktur (dicek design-reviewer).
5. ID **global/lintas chapter** memakai bloknya sendiri (001–050 per prefix) — tidak dicampur dengan blok chapter.

---

## §1 — Reserved Range: BR (Business Rules)

Blok per chapter + satu blok global. **Next available global = `BR-013`.**

| Chapter | Range | Terpakai | **Next available** |
|---------|-------|----------|--------------------|
| **GLOBAL** (lintas chapter) | BR-001 – BR-050 | BR-001 … BR-012 | **BR-013** |
| BAB-1 — Data Master & Siswa | BR-051 – BR-100 | — (belum ada) | **BR-051** |
| BAB-2 — Kelas & Presensi Diklat | BR-101 – BR-150 | — (belum ada) | **BR-101** |
| BAB-3 — Engine Belajar & SRS | BR-151 – BR-200 | — (belum ada) | **BR-151** |
| BAB-4 — Mock Exam & CBT | BR-201 – BR-250 | — (belum ada) | **BR-201** |
| BAB-5 — Diklat Asrama & MCU | BR-251 – BR-300 | — (belum ada) | **BR-251** |
| BAB-6 — Talent Pipeline & Penyaluran | BR-301 – BR-350 | — (belum ada) | **BR-301** |
| BAB-7 — Keuangan & Cicilan | BR-351 – BR-400 | — (belum ada) | **BR-351** |
| BAB-8 — Sertifikasi & Analytics | BR-401 – BR-450 | — (belum ada) | **BR-401** |

> **Catatan:** BR-001 … BR-012 (di `business-rules.md`) bersifat **global/lintas chapter** — jadi masuk blok GLOBAL, bukan BAB-1. Saat BAB-1 digarap dan butuh BR khusus chapter-nya, mulai dari **BR-051**, bukan BR-013.

---

## §2 — Reserved Range: FR (Functional Requirements)

Blok per chapter + satu blok global. **Next available global = `FR-13`.**

| Chapter | Range | Terpakai | **Next available** |
|---------|-------|----------|--------------------|
| **GLOBAL** (lintas chapter) | FR-01 – FR-50 | FR-01 … FR-12 | **FR-13** |
| BAB-1 — Data Master & Siswa | FR-51 – FR-100 | — (belum ada) | **FR-51** |
| BAB-2 — Kelas & Presensi Diklat | FR-101 – FR-150 | — (belum ada) | **FR-101** |
| BAB-3 — Engine Belajar & SRS | FR-151 – FR-200 | — (belum ada) | **FR-151** |
| BAB-4 — Mock Exam & CBT | FR-201 – FR-250 | — (belum ada) | **FR-201** |
| BAB-5 — Diklat Asrama & MCU | FR-251 – FR-300 | — (belum ada) | **FR-251** |
| BAB-6 — Talent Pipeline & Penyaluran | FR-301 – FR-350 | — (belum ada) | **FR-301** |
| BAB-7 — Keuangan & Cicilan | FR-351 – FR-400 | — (belum ada) | **FR-351** |
| BAB-8 — Sertifikasi & Analytics | FR-401 – FR-450 | — (belum ada) | **FR-401** |

> **Catatan:** FR-01 … FR-12 (di `REQUIREMENTS-MATRIX.md`) adalah FR **global/inti** hasil sinkronisasi master — meski beberapa menunjuk chapter tertentu (mis. FR-02 → BAB-4), ID-nya tetap di blok GLOBAL. FR atomik **per chapter** (dihasilkan saat §5a–5c BAB digarap) pakai blok chapter masing-masing.

---

## §3 — Reserved Range: UC (Use Cases)

`UC-001 … UC-008` = **anchor module-level** (1 UC per chapter, FINAL di `SRS-MASTER.md` §5). Use case **detail** per chapter mulai dari blok setelah anchor — **Next available = `UC-009`.**

| Chapter | Range (detail) | Anchor (final) | **Next available** |
|---------|----------------|----------------|--------------------|
| BAB-1 — Data Master & Siswa | UC-009 – UC-058 | UC-001 | **UC-009** |
| BAB-2 — Kelas & Presensi Diklat | UC-059 – UC-108 | UC-002 | **UC-059** |
| BAB-3 — Engine Belajar & SRS | UC-109 – UC-158 | UC-003 | **UC-109** |
| BAB-4 — Mock Exam & CBT | UC-159 – UC-208 | UC-004 | **UC-159** |
| BAB-5 — Diklat Asrama & MCU | UC-209 – UC-258 | UC-005 | **UC-209** |
| BAB-6 — Talent Pipeline & Penyaluran | UC-259 – UC-308 | UC-006 | **UC-259** |
| BAB-7 — Keuangan & Cicilan | UC-309 – UC-358 | UC-007 | **UC-309** |
| BAB-8 — Sertifikasi & Analytics | UC-359 – UC-408 | UC-008 | **UC-359** |

> **Kenapa anchor ≠ blok:** UC-001…008 sudah FINAL di SRS-MASTER sebagai use case **module-level** (jawaban "siapa bisa ngapain" di scope sistem). Use case **detail** (breakdown per chapter) butuh nomor sendiri — makanya mulai UC-009 dengan blok 50. Nomor anchor **jangan di-reuse** atau diubah.

---

## §4 — Reserved Range: PF (Process Flows)

Pola sama dengan UC: `PF-001 … PF-008` = **anchor 1 alur per chapter** (FINAL di `PROCESS-FLOW-MASTER.md`). Alur **tambahan** per chapter mulai dari blok setelah anchor — **Next available = `PF-009`.**

| Chapter | Range (tambahan) | Anchor (final) | **Next available** |
|---------|------------------|----------------|--------------------|
| BAB-1 — Data Master & Siswa | PF-009 – PF-058 | PF-001 | **PF-009** |
| BAB-2 — Kelas & Presensi Diklat | PF-059 – PF-108 | PF-002 | **PF-059** |
| BAB-3 — Engine Belajar & SRS | PF-109 – PF-158 | PF-003 | **PF-109** |
| BAB-4 — Mock Exam & CBT | PF-159 – PF-208 | PF-004 | **PF-159** |
| BAB-5 — Diklat Asrama & MCU | PF-209 – PF-258 | PF-005 | **PF-209** |
| BAB-6 — Talent Pipeline & Penyaluran | PF-259 – PF-308 | PF-006 | **PF-259** |
| BAB-7 — Keuangan & Cicilan | PF-309 – PF-358 | PF-007 | **PF-309** |
| BAB-8 — Sertifikasi & Analytics | PF-359 – PF-408 | PF-008 | **PF-359** |

---

## §5 — ID Global Tanpa Pembagian Chapter

Prefix berikut **hanya dipakai di level global/master** — tidak dibagi per chapter, tidak butuh reserved block.

| Prefix | Fungsi | Terpakai | **Next available** | File sumber |
|--------|--------|----------|--------------------|-------------|
| `G{1..6}` | Tujuan bisnis (Goals) | G1 – G6 | **G7** | `00-Global/SRS-MASTER.md` |
| `BREQ-` | Business Requirements | BREQ-01 – BREQ-05 | **BREQ-06** | `00-Global/REQUIREMENTS-MATRIX.md` |
| `SREQ-` | Stakeholder Requirements | SREQ-01 – SREQ-05 | **SREQ-06** | `00-Global/REQUIREMENTS-MATRIX.md` |
| `NFR-` | Non-Functional Requirements | NFR-01 – NFR-09 | **NFR-10** | `nfr.md` |
| `TR-` | Transition Requirements | TR-01 – TR-02 | **TR-03** | `00-Global/REQUIREMENTS-MATRIX.md` |
| `IF-` | Interface / sambungan sistem eksternal | IF-01 – IF-06 | **IF-07** | `00-Global/SRS-MASTER.md` |
| `AS-` | Asumsi | AS-01 – AS-05 | **AS-06** | `assumptions-constraints.md` |
| `CN-` | Constraints | CN-01 – CN-06 | **CN-07** | `assumptions-constraints.md` |

---

## §6 — Blok Cadangan (Jika Range Habis)

Kalau satu chapter melebihi 50 nomor, buka blok cadangan berikut (**jangan** menembus range chapter lain):

| Prefix | Blok Cadangan |
|--------|---------------|
| BR | BR-451 – BR-900 (dipakai berurutan, tandai chapter asal di kolom catatan) |
| FR | FR-451 – FR-900 |
| UC | UC-409 – UC-858 |
| PF | PF-409 – PF-858 |

> Blok cadangan dibuka **hanya bila blok utama habis** — buka lebih dulu = tanda perencanaan buruk (design-reviewer akan flag).

---

## Log Perubahan Penomoran

| Tanggal | ID | Aksi | Chapter | Alasan |
|---------|-----|------|---------|--------|
| 10 Okt 2026 | BR-001 … BR-012 | Terbit (global) | GLOBAL | Sinkronisasi `question-framework.md` FINAL → `business-rules.md` |
| 10 Okt 2026 | FR-01 … FR-12 | Terbit (global) | GLOBAL | Inti functional requirement hasil sinkronisasi master |
| 10 Okt 2026 | UC-001 … UC-008 | Terbit (anchor) | BAB-1..8 | Module-level use case, FINAL di SRS-MASTER §5 |
| 10 Okt 2026 | PF-001 … PF-008 | Terbit (anchor) | BAB-1..8 | 1 alur utama per chapter, FINAL di PROCESS-FLOW-MASTER |
| 10 Okt 2026 | NFR-01..09, IF-01..06, BREQ-01..05, SREQ-01..05, TR-01..02, AS-01..05, CN-01..06, G1..6 | Terbit (global) | GLOBAL | Master docs |

---

## Open Questions / Trade-off

1. **Anchor vs blok detail (UC/PF)** — desain sekarang: anchor `001–008` dipakai module-level, detail mulai `009` dengan blok 50. Alternatif: gabung jadi satu range berurutan (tapi numbering per chapter jadi tidak berblok rapi). **Belum diputuskan mana yang dianggap final** — saat ini asumsi: anchor tetap, detail pakai blok terpisah.
2. **Blok cadangan** — apakah 450 nomor (9 chapter × 50) cukup, atau perlu buka blok lebih awal untuk chapter berat (BAB-4 Mock Exam, BAB-6 Pipeline)?
3. **Legacy numbering** — jika lembaga punya nomor BR/FR lama dari dokumen sebelum sistem ini, perlu mapping table khusus agar tidak dobel (belum ada datanya).
