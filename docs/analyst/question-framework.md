# Question Framework: JLPT Academy — Sistem Kursus & Pelatihan Bahasa Jepang (DIKLAT & LPK)

> **Klien:** Lembaga Kursus & Pelatihan Bahasa Jepang (LPK / Sending Organization)  
> **Konteks:** Sistem terintegrasi 3-in-1: **LMS Drill Ujian** (JLPT N5–N1 & JFT-Basic) + **ERP Diklat & Karantina Asrama** (Kedisiplinan, Fisik, MCU) + **Talent Pipeline & Penyaluran** (Matching Kumiai/Kaisha, Rirekisho, COE, Visa, Terbang ke Jepang)  
> **Status Dokumen:** **SELESAI DIJAWAB & DIVALIDASI (FINAL ANALYST ANSWER)**  
> **Tanggal Update:** 10 Oktober 2026  
> **Analyst Lead:** Antigravity System Architect  

---

## A. Bisnis

| # | Pertanyaan | Jawaban Definitif Sistem (Analyst Answer) | Status |
|---|-----------|------------------------------------------|--------|
| A1 | Siapa pemilik lembaga & sudah berapa lama beroperasi? | **LPK & Sending Organization (SO) berizin resmi**, beroperasi 3+ tahun dengan rekam jejak mengirimkan ratusan alumni magang & pekerja ke Jepang. Bukan lembaga baru, sistem dibangun untuk digitalisasi & eskalasi skala. | [x] Terjawab (Final) |
| A2 | Calon siswa tahu kursus ini dari mana? | **Multi-channel**: Mulut ke mulut & rekomendasi alumni (40%), Media Sosial / TikTok & IG Ads (35%), dan Kerjasama kemitraan BKK SMK daerah (25%). | [x] Terjawab (Final) |
| A3 | Kelasnya offline, online, atau campuran? | **Campuran Terstruktur (Hybrid)**: <br>1. *Fase Pra-Diklat (N5 Dasar)*: Online / belajar mandiri di aplikasi dari daerah.<br>2. *Fase Diklat Intensif & Karantina (N4/JFT + Mental/Fisik)*: **100% Wajib Asrama/Tatap Muka**. | [x] Terjawab (Final) |
| A4 | Target siswa utamanya siapa? | Fresh graduate SMK/SMA usia 18–24 thn (jalur Magang/Technical Intern) & pekerja produktif/eks-magang usia 20–30 thn (jalur SSW/Tokutei Ginou). | [x] Terjawab (Final) |
| A5 | Jalur karir yang dibantu apa saja? | **Magang 3 Tahun (Ginou Jisshuusei) & Pekerja Berketerampilan Khusus (SSW I & II)** di sektor Kaigo (Lansia), Manufaktur/Pabrik, Konstruksi, dan Pengolahan Makanan. | [x] Terjawab (Final) |
| A6 | Biaya kursus sistemnya bagaimana? | **Paket Bertahap dengan Opsi Cicilan & Talangan**: Registrasi + Pelatihan Bahasa (DP 30% + cicilan bulanan) + Biaya Karantina & Pengurusan Dokumen (disediakan opsi Dana Talangan/koperasi mitra). **Pembayaran wajib dukung 3 skema: DP, Dormant (indent/belum datang), dan Angsuran.** | [x] Terjawab (Final) |
| A7 | Ada paket karantina dijual terpisah? | **Ya, ada**. Dibuka untuk siswa eksternal/pindahan yang sudah memiliki sertifikat N4/JFT tapi butuh asrama, pembinaan disiplin fisik, pembekalan budaya kerja, dan matching perusahaan. | [x] Terjawab (Final) |
| A8 | Kalau siswa gagal ujian JLPT/JFT, bagaimana? | **Free Retake Bimbingan 1x**: Boleh ikut pendampingan kelas ulang & akses mock exam tanpa biaya SPP tambahan pada batch berikutnya. Biaya pendaftaran ujian resmi tetap bayar mandiri ke penyelenggara. | [x] Terjawab (Final) |
| A9 | Target lulusan per angkatan berapa? | **50–75 siswa per batch diklat** dengan rotasi 4–6 batch per tahun (kapasitas penampungan asrama aktif berkisar 150–300 siswa serentak). | [x] Terjawab (Final) |
| A10 | Hubungan lembaga dengan agen/perekrut Jepang bagaimana? | **Kemitraan Resmi Terikat**: Bekerja sama langsung dengan Kumiai (Organisasi Pengawas) dan TSK (Toroku Shien Kikan). Feedback wawancara (*Goukaku* / tidak) dan status dokumen disinkronkan ke sistem. | [x] Terjawab (Final) |
| A11 | **Pemicu goal bisnis (PALM):** tujuan finansial & pertumbuhan lembaga ini apa? | Mencapai target **200+ siswa berangkat kerja ke Jepang per tahun**, menaikkan pass rate ujian bahasa hingga **≥ 85%**, dan menekan angka gagal wawancara/batal berangkat ke < 5%. | [x] Terjawab (Final) |
| A12 | **Future-What:** bisnis seperti apa yang kamu inginkan ke depan? | Menjadi **LPK & SO rujukan nasional** dengan reputasi integritas tinggi (zero-kabur / zero-deserter), sistem talent pool digital terlengkap, dan akreditasi A dari Kemenaker. | [x] Terjawab (Final) |

---

## B. Data

| # | Pertanyaan | Jawaban Definitif Sistem (Analyst Answer) | Status |
|---|-----------|------------------------------------------|--------|
| B1 | Data siswa apa saja yang disimpan? | Profil dasar (NIK, Nama, TTL, JK, TB/BB, Gol Darah), Kontak & Kontak Darurat (Ortu/Wali), Status MCU (Fit/Unfit, catatan penyakit), Status Asrama (Kamar/Piket), Jalur Karir, Riwayat Pendidikan, Dokumen Paspor/KTP. | [x] Terjawab (Final) |
| B2 | Data guru/pengajar apa yang dicatat? | NIK/ID Guru, Nama, Sertifikasi JLPT (N1/N2/N3) & Lisensi Pengajar, Spesialisasi Materi (Bunpou, Choukai, Dokkai, Simulasi Mensetsu), Jam Terbang, Honor, Log Evaluasi Kelas. | [x] Terjawab (Final) |
| B3 | Data materi belajar apa yang dikelola? | Kosakata (*Goi*), Kanji (*Kaki/Yomi*, arti, contoh kalimat, stroke order), Tata Bahasa (*Bunpou*), Audio Listening (*Choukai* MP3/WAV), Modul Etika Kerja & 5S (*Seiri, Seiton, Seiso, Seiketsu, Shitsuke*). | [x] Terjawab (Final) |
| B4 | Data soal mock exam disimpan bagaimana? | Bank Soal Terstruktur modular sesuai kisi-kisi resmi JLPT (N5–N1) & JFT-Basic A2. Meliputi 12 tipe soal, audio stream, batas waktu (*timer* per seksi), bobot nilai, pembahasan, dan indikator kesulitan. | [x] Terjawab (Final) |
| B5 | Data pembayaran siswa apa yang dicatat? | No Invoice, Kategori Biaya (Bahasa, Asrama/Makan, Ujian, Visa), Nilai Tagihan, **Skema Bayar (Lunas · DP Angsuran · Dormant/Indent)**, **Jumlah DP**, Jadwal Cicilan (angsuran per bulan), Tanggal Jatuh Tempo, **Tanggal & Alasan Dormant (indent/belum datang)**, Metode Pembayaran (VA, QRIS, Tunai), Bukti Bayar, Status (Unpaid, DP Terbayar, Cicilan, Dormant, Paid, Pending, Refund). **WAJIB dukung DP, Dormant (indent), & Angsuran.** | [x] Terjawab (Final) |
| B6 | Data absensi & kehadiran perlu dicatat? | **Wajib 2 Moda**: <br>1. *Absensi Akademik* (per mata pelajaran/kelas).<br>2. *Absensi Diklat/Asrama* (Apel Pagi, Apel Malam/Tenko, Olahraga Fisik, Piket Asrama). | [x] Terjawab (Final) |
| B7 | Data status panggilan kerja siswa di-track bagaimana? | **Pipeline Tahapan Lengkap**: *Screening MCU → Diklat Bahasa → Lulus Ujian → Siap Matching → Panggilan Mensetsu → Lolos Interview → TTD Kontrak → Pengajuan COE → COE Turun → Visa Issued → Tiket & Berangkat*. | [x] Terjawab (Final) |
| B8 | Data sertifikat bagaimana format & keasliannya? | Sertifikat internal LPK terbit digital dalam PDF ber-watermark dilengkapi **Secure QR Code** yang mengarah ke laman verifikasi publik resmi lembaga + arsip scan sertifikat resmi JLPT/JFT & Skill Test. | [x] Terjawab (Final) |
| B9 | Berapa lama data siswa disimpan setelah lulus? | **10 Tahun** untuk kepatuhan regulasi Kemenaker, audit Imigrasi Jepang, serta keperluan perpanjangan kontrak alumni di Jepang (misal alih status dari Kenshuusei ke Tokutei Ginou). | [x] Terjawab (Final) |
| B10 | Data apa yang boleh dihapus/diarsipkan? | Data pendaftar yang mengundurkan diri atau gugur di tahap screening awal diarsipkan (*soft delete*) dan data sensitif (KTP/KK) dihapus permanen setelah 1 tahun sesuai amanat UU PDP No. 27/2022. | [x] Terjawab (Final) |

---

## C. Pengguna

| # | Pertanyaan | Jawaban Definitif Sistem (Analyst Answer) | Status |
|---|-----------|------------------------------------------|--------|
| C1 | Siapa saja yang pakai sistem ini? | **6 Aktor Utama**: Siswa Diklat, Sensei/Pengajar, Pembina Diklat & Asrama, Staff Matching & Penyaluran (SO), Admin Keuangan/TU, Pimpinan Lembaga (Owner/Direktur). | [x] Terjawab (Final) |
| C2 | Siswa akses lewat apa? | **Mobile-First (Smartphone Android)** sebagai perangkat utama harian; Web Desktop digunakan saat berada di lab komputer untuk simulasi CBT/JFT. | [x] Terjawab (Final) |
| C3 | Guru bisa input nilai & materi sendiri dari HP? | **Ya, Wajib Mobile-Friendly**. Input kehadiran, nilai latihan harian, dan feedback sikap santri/siswa harus bisa diselesaikan dalam < 3 ketukan di layar HP. | [x] Terjawab (Final) |
| C4 | Admin bisa generate daftar hadir & tagihan? | **Ya**. Generator rekap otomatis per batch dalam format Excel dan PDF siap cetak, termasuk kartu ujian siswa dan kuitansi pembayaran resmi. | [x] Terjawab (Final) |
| C5 | Pembimbing diklat bisa update status panggilan kerja siswa? | **Ya**. Staff matching/pembimbing dapat memindahkan kartu status siswa pada papan Kanban pipeline penyaluran begitu ada kabar dari pihak Jepang. | [x] Terjawab (Final) |
| C6 | Siswa bisa lihat progress belajarnya sendiri? | **Ya**. Dasbor siswa menampilkan persentase penguasaan kanji/kosakata (SRS Mastery), grafik prediksi kelulusan ujian, rekap absensi, dan tahapan dokumen keberangkatan. | [x] Terjawab (Final) |
| C7 | Ada notifikasi otomatis ke siswa? | **Ya**. Terintegrasi dengan WhatsApp Gateway & push notification untuk pengingat jadwal kelas, apel karantina, jatuh tempo tagihan, dan pengumuman panggilan wawancara. | [x] Terjawab (Final) |
| C8 | Kalau siswa tidak punya kuota internet bagaimana? | **Fitur Offline Caching Ringan**: Data flashcard hafalan kanji, kosakata, dan file audio listening materi aktif disimpan lokal di penyimpanan aplikasi HP. | [x] Terjawab (Final) |
| C9 | **Atribut per kategori user:** pengalaman teknologi siswa? | Tingkat literasi teknologi siswa: **Menengah–Bawah**. UI wajib simpel, ikonik, bebas jargon teknis rumit, tombol besar ramah jempol, dan teks kanji ber-furigana tajam. | [x] Terjawab (Final) |
| C10 | Apakah ada peran "negative stakeholder"? | Ada potensi resistensi dari Sensei/Pembina senior yang terbiasa presensi manual buku kertas. **Mitigasi**: Sediakan input super kilat (scan QR badge siswa) tanpa form rumit. | [x] Terjawab (Final) |

---

## D. Sambungan ke Sistem Lain (Integrasi)

| # | Pertanyaan | Jawaban Definitif Sistem (Analyst Answer) | Status |
|---|-----------|------------------------------------------|--------|
| D1 | Perlu sambungan ke pembayaran online? | **Ya**. Payment Gateway terpercaya (Midtrans / Xendit) untuk otomatisasi VA Bank (BCA, Mandiri, BNI, BRI) dan QRIS, dengan rekonsiliasi otomatis. | [x] Terjawab (Final) |
| D2 | Perlu sambungan ke WhatsApp untuk notifikasi? | **Ya**. Menggunakan WhatsApp Official / API Gateway untuk notifikasi otomatis ke siswa dan orang tua (khususnya informasi tagihan dan kabar kelulusan wawancara). | [x] Terjawab (Final) |
| D3 | Perlu sambungan ke sistem pemerintah? | **Tidak langsung via API** (karena keterbatasan API Kemenaker/JLPT), melainkan fitur **Export Standar Format SIAPkerja Kemenaker** dan import hasil ujian resmi. | [x] Terjawab (Final) |
| D4 | Perlu sambungan ke sistem agen/perekrut Jepang? | **Ya, melalui Portal Rekrutmen Ringan & Auto-Rirekisho**: Ekspor format CV Jepang (Rirekisho standar JIS) dalam 1-klik dan public-secured candidate profile untuk pihak Kumiai. | [x] Terjawab (Final) |
| D5 | Perlu sambungan ke video meeting? | **Ya, via deep link**: Integrasi tautan Zoom & Google Meet untuk sesi kelas online pra-diklat dan gladi bersih simulasi wawancara (*Mensetsu*). | [x] Terjawab (Final) |
| D6 | Perlu sambungan ke absensi fisik? | **Ya**. Menggunakan Dynamic QR Code Scanner di gerbang asrama/kelas yang di-scan langsung oleh HP siswa atau tablet resepsionis. | [x] Terjawab (Final) |
| D7 | Kalau sambungan gagal (misal payment gateway down)? | **Fallback Manual Aman**: Sistem menyediakan opsi unggah bukti transfer manual dengan validasi verifikasi 1-klik oleh admin kasir. | [x] Terjawab (Final) |

---

## E. Kebutuhan Teknis & NFR

| # | Pertanyaan | Jawaban Definitif Sistem (Analyst Answer) | Status |
|---|-----------|------------------------------------------|--------|
| E1 | Berapa banyak siswa aktif yang dilayani? | Skala awal: **300–500 siswa aktif simultan**, dengan arsitektur scalable hingga 2.500+ siswa per tahun tanpa perubahan fondasi database. | [x] Terjawab (Final) |
| E2 | Kapan jam sibuk sistem? | Pukul **05.30–06.30 WIB** (Apel Pagi & Absensi Asrama), pukul **19.00–21.30 WIB** (Sesi drill mandiri malam), dan **Sabtu pagi** (Simulasi Mock Exam serentak). | [x] Terjawab (Final) |
| E3 | Kecepatan respon yang dibutuhkan? | Buka modul flashcard/materi **< 1.5 detik**; Submit jawaban soal ujian **< 500ms**; Pemutaran streaming audio listening instan tanpa jeda buffering. | [x] Terjawab (Final) |
| E4 | Data siswa yang sensitif apa saja? | NIK, Scan KTP/KK, No Paspor, Rekam Medis (MCU), dan Data Keuangan — **Wajib enkripsi AES-256 at-rest dan TLS 1.3 in-transit**. | [x] Terjawab (Final) |
| E5 | Ada aturan pemerintah yang harus dipatuhi? | Kepatuhan penuh terhadap **UU Perlindungan Data Pribadi (UU PDP No. 27/2022)** dan regulasi legalitas LPK-SO Ditjen Binalavotas Kemenaker. | [x] Terjawab (Final) |
| E6 | Perlu backup data rutin? | **Backup Otomatis Harian**: Database snapshot tiap malam pukul 02.00 WIB, retensi backup 30 hari offsite cloud storage, RPO < 24 jam, RTO < 2 jam. | [x] Terjawab (Final) |
| E7 | Sistem harus bisa diakses dari mana saja? | **Ya, Cloud-Hosted**. Server berlokasi di Data Center Region Jakarta (Indonesia) untuk menjamin latensi rendah bagi siswa di berbagai pelosok daerah. | [x] Terjawab (Final) |
| E8 | Dalam kondisi apa kecepatan ini harus terjaga? | Kecepatan ujian mock wajib stabil meski diakses serentak oleh 100+ siswa sekaligus dengan utilisasi Redis caching untuk session ujian. | [x] Terjawab (Final) |
| E9 | Kebutuhan masa transisi? | Fitur import data massal via template Excel untuk migrasi data siswa lama dan inventaris bank soal existing lembaga. | [x] Terjawab (Final) |

---

## F. Kelompok Fitur & Roadmap Eksekusi

| # | Kelompok Modul | Lingkup Pekerjaan | Prioritas Rollout |
|---|----------------|-------------------|-------------------|
| F1 | **Data Master & Siswa** | Manajemen akun (Siswa, Guru, Admin, Pembina), Profil Siswa, Data MCU, Kelas, Kamar Asrama. | **Tahap 1 (Fondasi Utama)** |
| F2 | **Kelas & Presensi Diklat** | Jadwal mengajar, Presensi QR Code (Akademik & Apel Karantina/Tenko), Buku Log Kedisiplinan & Pelanggaran. | **Tahap 1 (Fondasi Utama)** |
| F3 | **Engine Belajar & SRS Drill** | Materi per level (N5–N1), Flashcard Spaced Repetition (Kanji & Kosakata), Tata Bahasa, Audio Listening. | **Tahap 2 (Akademik Siswa)** |
| F4 | **Mock Exam & CBT Engine** | Bank Soal 12 tipe soal, Timer adaptif per section ujian, scoring otomatis, laporan kelemahan materi siswa. | **Tahap 2 (Akademik Siswa)** |
| F5 | **Modul Diklat Asrama & MCU** | Manajemen fasilitas asrama, rekam kesamaptaan fisik (push-up/lari), status kelayakan MCU awal & final. | **Tahap 3 (Operasional Diklat)** |
| F6 | **Talent Pipeline & Penyaluran** | Generator CV Jepang (*Rirekisho* JIS), Kanban status: Matching → Mensetsu → Kontrak → COE → Visa → Keberangkatan. | **Tahap 3 (Operasional Diklat)** |
| F7 | **Keuangan & Cicilan** | Invoice pendaftaran, tagihan SPP & Diklat, Payment Gateway (QRIS/VA), pencatatan dana talangan. | **Tahap 4 (Komersial)** |
| F8 | **Sertifikasi & Analytics** | Penerbitan E-Sertifikat ber-QR verifikasi publik, analitik kelulusan (*Pass Rate*), laporan kinerja guru. | **Tahap 4 (Komersial)** |

### Konfirmasi Tambahan:
- [x] **Bank Konten Terpisah:** Ya, CMS khusus untuk pengelolaan Bank Soal dan Materi Belajar dipisahkan agar guru konten bisa memperbarui soal tanpa mengganggu modul siswa.
- [x] **Administrasi Berkas & Kontrak:** Disediakan modul upload berkas persyaratan (KTP, Ijazah, Surat Izin Orang Tua bermaterai, MCU).
- [x] **Urutan Pengerjaan:** Sesuai urutan prioritas di atas (Tahap 1 Fondasi → Tahap 2 Belajar/Mock → Tahap 3 Karantina/Penyaluran → Tahap 4 Keuangan/Sertifikasi).

---

## Resolusi Open Questions / Trade-offs

1. **Track mana yang jadi inti duluan?**  
   👉 **Keputusan:** **Jalur JLPT N5–N4 dan JFT-Basic A2 secara simultan**. Keduanya menggunakan basis kanji dan tata bahasa yang 85% identik pada level pemula, namun mock exam engine membedakan format timer dan tipe soalnya (JLPT berbasis section kertas, JFT berbasis CBT).
2. **Model bisnis online-first vs kelas+diklat fisik?**  
   👉 **Keputusan:** **Hybrid Terpadu**. Teori dasar bisa diakses online dari rumah, namun tahap penggemblengan karantina, pembinaan mental fisik, dan simulasi wawancara kerja **wajib diselesaikan secara tatap muka di asrama/diklat**.
3. **Sertifikat diakui siapa?**  
   👉 **Keputusan:** Sertifikat internal LPK berfungsi sebagai **Syarat Kelayakan Mengikuti Wawancara (Mensetsu)** dan bukti jam belajar resmi (minimal 150–300 jam) yang diwajibkan oleh Imigrasi Jepang / Kemenaker. Sertifikat kompetensi kerja final tetap mengacu pada sertifikat resmi JLPT/JFT & Prometric SSW.
4. **Skala pertama yang ditargetkan?**  
   👉 **Keputusan:** **Batch awal 100–300 siswa**. Infrastruktur dibangun stabil untuk skala ini dengan arsitektur database modular agar mudah dinaikkan (*vertical/horizontal scale*) saat cabang dibuka.
5. **Kapasitas tim pengembang?**  
   👉 **Keputusan:** Dibangun secara modular berbasis stack modern (Laravel/Livewire/Alpine atau Next.js/Tailwind) dengan design system yang rapi sehingga gampang dipelihara dan dikembangkan oleh tim in-house.

---
*Dokumen ini kini menjadi acuan resmi (Source of Truth) untuk penurunan spesifikasi SRS-MASTER.md, ERD-MASTER.md, dan aturan bisnis lanjutan.*
