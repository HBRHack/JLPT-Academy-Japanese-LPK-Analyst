# Assumptions & Constraints: JLPT Academy

> **Dokumen:** Log asumsi & constraint
> **Proyek:** JLPT Academy — LPK & SO
> **Versi:** 0.2

---

## Asumsi (belum diverifikasi — bisa berubah, jadi risiko)

| ID | Asumsi | Dampak bila salah | cara verifikasi |
|----|--------|-------------------|-----------------|
| AS-01 | Target pasar: fresh graduate SMK/SMA & pekerja Indonesia yang mau magang/SSW ke Jepang | Salah sasaran → fitur & bahasa UI meleset | Validasi ke data pendaftar & agen mitra |
| AS-02 | Mayoritas siswa pakai **HP Android** kelas menengah–bawah | Infra & UI tidak optimal di perangkat target | Survei perangkat pendaftar |
| AS-03 | Teori dasar (N5) bisa online dari daerah; karantina wajib tatap muka | Asumsi hybrid meleset → desain delivery salah | Konfirmasi kebijakan lembaga |
| AS-04 | Kemitraan Kumiai/TSK sudah terikat & bisa kirim status | Pipeline tanpa data mitra → Kanban tidak hidup | Konfirmasi kontrak mitra |
| AS-05 | Ada **donasi pemerintah** sebagai sumber dana talangan (A4) | Rencana talangan tidak realistis | Konfirmasi sumber dana aktual |

## Constraint (mengikat — membatasi solusi)

| ID | Constraint | Sumber | Kepatuhan |
|----|-----------|--------|-----------|
| CN-01 | Kepatuhan **UU PDP No. 27/2022** (enkripsi, retensi, hak hapus) | Regulasi | NFR-04, BR-007 |
| CN-02 | Legalitas **LPK-SO Ditjen Binalavotas Kemenaker** | Regulasi | SRS §1.1 |
| CN-03 | Sertifikat harus memenuhi syarat **jam belajar 150–300 jam** (Imigrasi Jepang) | Regulasi | BR-005 |
| CN-04 | Sistem harus berjalan di **cloud DC Region Jakarta** | Kebijakan infra | NFR-08 |
| CN-05 | Dibangun **in-house**, stack fleksibel (A1 ditunda) | Kapasitas tim | — |
| CN-06 | Target skala awal **300–500 siswa simultan**, scale ke 2.500+/tahun | Kapasitas lembaga | NFR-03 |

## Kandidat Constraint yang perlu DIUJI (bukan fakta pasti)

- **"Payment gateway harus Midtrans/Xendit"** → A2 masih ditunda; belum jadi constraint final, jangan dikunci.
- **"Stack harus Laravel atau Next.js"** → A1 masih ditunda; jangan diimplementasi seolah-olah sudah final.

---

## Open Questions / Trade-off
1. **AS-05 (donasi pemerintah)** — sumber dana ini nyata atau rencana? Perlu bukti sebelum masuk perhitungan bisnis.
2. **CN-05** — kapasitas tim in-house (berapa orang, skill apa) belum diketahui → memengaruhi estimasi roadmap 4 tahap.
3. Belum ada **constraint deadline** (target go-live per tahap) — perlu ditetapkan owner.
