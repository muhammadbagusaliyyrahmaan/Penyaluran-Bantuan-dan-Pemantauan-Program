# SOFTWARE REQUIREMENTS SPECIFICATION

# Sistem Penyaluran Bantuan dan Pemantauan Program

**Baitulmal Tazkia**  
Kelompok 9 — Klaster Penyaluran  
Program Studi Sistem Informasi  
STMIK Tazkia

**Versi:** 1.0 — Draf untuk validasi pemangku kepentingan  
**Tanggal:** 21 Oktober 2026  
**Status:** DRAF — belum menjadi baseline sampai ditinjau dan disetujui klien.

> **Catatan penggunaan:** Markdown ini dibuat dari dokumen Word SRS. Diagram disertakan sebagai file PNG terpisah; simpan PNG di folder yang sama dengan file Markdown agar gambar tampil.

SOFTWARE REQUIREMENTS SPECIFICATION

SISTEM PENYALURAN BANTUAN
DAN PEMANTAUAN PROGRAM

Baitulmal Tazkia
Kelompok 9 — Klaster Penyaluran
Program Studi Sistem Informasi
STMIK Tazkia

Versi 1.0 — Draf untuk validasi pemangku kepentingan
Tanggal: 21 Oktober 2026

Status: DRAF — belum menjadi baseline sampai ditinjau dan disetujui klien.


## Kontrol Dokumen


| Atribut | Keterangan |
| --- | --- |
| Nama dokumen | Software Requirements Specification (SRS) — Sistem Penyaluran Bantuan dan Pemantauan Program |
| Organisasi/klien | Baitulmal Tazkia |
| Tim | Kelompok 9 — Klaster Penyaluran |
| Versi/status | 1.0 — Draf untuk review; belum disetujui |
| Pemilik dokumen | Kelompok proyek; ditetapkan/diubah saat review klien |
| Standar penyusunan | ISO/IEC/IEEE 29148 sebagai acuan SRS; praktik keamanan dan pelindungan data mengikuti regulasi yang berlaku |
| Sumber kebutuhan | WORKBOOK Proyek Penyaluran Bantuan dan Pemantauan Program, khususnya Bab 2–3 dan deliverable MISI.304 |
| Persetujuan | Nama narasumber, jabatan, tanggal dan tanda tangan diisi setelah validasi klien |


### Riwayat Perubahan


| Versi | Tanggal | Perubahan | Status |
| --- | --- | --- | --- |
| 1.0 | 21-10-2026 | Draf awal SRS, alur bisnis, modul, fungsi, kebutuhan, RTM, dan diagram registrasi/penyaluran | Menunggu review |


## Daftar Isi

- [Kontrol Dokumen](#kontrol-dokumen)
- [1. Pendahuluan](#1-pendahuluan)
- [2. Gambaran Umum](#2-gambaran-umum)
- [3. Pemangku Kepentingan dan Peran](#3-pemangku-kepentingan-dan-peran)
- [4. Alur Bisnis](#4-alur-bisnis)
- [5. Kebutuhan Fungsional dan Daftar Modul](#5-kebutuhan-fungsional-dan-daftar-modul)
- [6. Kebutuhan Nonfungsional](#6-kebutuhan-nonfungsional)
- [7. Use Case Utama](#7-use-case-utama)
- [8. Model Data Konseptual](#8-model-data-konseptual)
- [9. Kebutuhan Integrasi dan API](#9-kebutuhan-integrasi-dan-api)
- [10. Standar dan Kepatuhan](#10-standar-dan-kepatuhan)
- [11. Matriks Ketertelusuran Kebutuhan (RTM)](#11-matriks-ketertelusuran-kebutuhan-rtm)
- [12. Verifikasi, Validasi, dan UAT](#12-verifikasi-validasi-dan-uat)
- [13. Risiko dan Mitigasi](#13-risiko-dan-mitigasi)
- [14. Persetujuan Dokumen](#14-persetujuan-dokumen)
- [Lampiran A — Pertanyaan Validasi](#lampiran-a--pertanyaan-validasi)
- [Referensi](#referensi)


## 1. Pendahuluan


### 1.1 Tujuan Dokumen

Dokumen ini mendefinisikan kebutuhan perangkat lunak untuk subsistem Penyaluran Bantuan dan Pemantauan Program Baitulmal Tazkia. Dokumen menjadi acuan bagi perancangan, implementasi, pengujian, UAT, serta persetujuan klien. Setiap kebutuhan diberi ID agar dapat ditelusuri ke modul, rancangan, dan pengujian.


### 1.2 Ruang Lingkup Produk

Sistem mengelola proses setelah penerima manfaat dinyatakan layak oleh subsistem hulu, mulai dari perencanaan penyaluran per program, permintaan persetujuan dan reservasi saldo, penugasan petugas, pencatatan serah terima di lapangan, hingga pemantauan kemajuan program dan penyediaan rekapitulasi melalui API.

- Membuat rencana penyaluran per program, penerima manfaat, jadwal, dan nominal.
- Meminta persetujuan saldo/peruntukan dari subsistem Pengelolaan Dana per Peruntukan sebelum penyaluran dijalankan.
- Mencatat realisasi penyerahan beserta bukti serah terima, termasuk tanda tangan penerima bila disepakati.
- Mendukung pencatatan lapangan saat jaringan tidak tersedia (offline-first) dan sinkronisasi saat jaringan kembali.
- Memantau program berjangka, misalnya beasiswa bertahap atau bantuan usaha.
- Menyediakan rekapitulasi penyaluran untuk subsistem Pelaporan Publik dan Transparansi Dana melalui kontrak API.

### 1.3 Di Luar Lingkup

- Menetapkan kelayakan penerima manfaat; tanggung jawab ini berada pada subsistem Pendataan dan Verifikasi Penerima Manfaat.
- Mengelola saldo, menetapkan peruntukan, atau menjadi otoritas akhir persetujuan dana; dilakukan oleh subsistem Pengelolaan Dana per Peruntukan.
- Menghimpun donasi dan menentukan dana kampanye yang terkumpul; menjadi tanggung jawab subsistem Manajemen Kampanye Penghimpunan.
- Mencatat jurnal akuntansi; menjadi tanggung jawab Balaka.
- Menjadwalkan relawan; menjadi tanggung jawab subsistem Relawan dan Operasional Acara.
- Mengelola publikasi laporan akhir; sistem ini hanya menyediakan data/rekap melalui API.

### 1.4 Istilah dan Singkatan


| Istilah | Definisi |
| --- | --- |
| Penerima manfaat | Orang/keluarga/entitas yang menerima bantuan dan telah diverifikasi oleh subsistem hulu. |
| Rencana penyaluran | Rencana program, daftar penerima, nominal, jadwal, dan petugas sebelum realisasi. |
| Reservasi saldo | Pemesanan alokasi dana saat rencana disetujui agar dana yang sama tidak dipakai dua rencana sekaligus. |
| Realisasi penyaluran | Catatan bahwa penyerahan bantuan telah dilakukan dan didukung bukti yang diterima. |
| Offline-first | Pola aplikasi yang memungkinkan petugas mencatat kegiatan lapangan tanpa jaringan, lalu menyinkronkan data. |
| RTM | Requirements Traceability Matrix, matriks penelusuran kebutuhan. |
| UAT | User Acceptance Test, pengujian penerimaan bersama pengguna/klien. |
| SRS | Software Requirements Specification. |
| API | Application Programming Interface. |


### 1.5 Dasar dan Status Asumsi

Workbook menegaskan bahwa lingkup awal masih harus dikonfirmasi melalui wawancara dan observasi. Karena itu, dokumen ini membedakan kebutuhan yang berasal langsung dari workbook dan rancangan usulan yang masih memerlukan persetujuan klien. Tanda [KONFIRMASI] berarti aturan belum boleh dianggap final.


## 2. Gambaran Umum


### 2.1 Kondisi Sistem Berjalan (As-Is)

Menurut workbook, pemantauan penyaluran saat ini banyak berlangsung melalui percakapan grup WhatsApp, lalu staf admin mencatat ulang informasi tersebut. Bukti serah terima tersebar dan sulit ditelusuri ketika donatur meminta informasi penggunaan dana. Pencatatan keuangan secara umum masih menggunakan spreadsheet; beberapa sumber data berada pada kanal yang terpisah.


### 2.2 Masalah Bisnis


| ID | Masalah | Dampak |
| --- | --- | --- |
| MB-01 | Informasi penyaluran dan bukti tersebar di percakapan | Sulit menelusuri bukti dan riwayat per penerima/program. |
| MB-02 | Admin mengetik ulang informasi dari percakapan | Risiko keterlambatan, duplikasi, dan salah salin. |
| MB-03 | Penyaluran bisa berjalan sebelum persetujuan saldo terkonfirmasi | Risiko saldo peruntukan negatif atau pemakaian dana ganda. |
| MB-04 | Petugas bekerja di lapangan dengan jaringan tidak andal | Pencatatan tertunda atau tidak dilakukan saat kegiatan. |
| MB-05 | Foto/bukti dapat memuat data pribadi penerima | Risiko pemrosesan atau pengungkapan data tanpa dasar/izin yang sesuai. |


### 2.3 Tujuan dan Indikator Keberhasilan


| ID | Tujuan | Indikator yang diusulkan |
| --- | --- | --- |
| TB-01 | Memusatkan pencatatan penyaluran | Seluruh penyaluran yang masuk lingkup memiliki ID, status, penanggung jawab, dan jejak perubahan. |
| TB-02 | Mencegah penyaluran tanpa persetujuan | Tidak ada rencana berstatus siap dijalankan sebelum persetujuan saldo dari sistem hulu diterima. |
| TB-03 | Memastikan bukti realisasi dapat ditelusuri | Setiap realisasi selesai memiliki bukti sesuai kebijakan yang disetujui klien. |
| TB-04 | Mendukung petugas lapangan | Catatan dapat disimpan saat offline dan disinkronkan tanpa duplikasi setelah jaringan pulih. |
| TB-05 | Menyediakan data untuk pemantauan dan pelaporan | Rekap per program dapat diambil melalui API sesuai kontrak. |

Target numerik (misalnya persentase penggunaan aplikasi atau waktu respons) ditetapkan bersama klien setelah baseline operasional diketahui; dokumen ini tidak mengarang angka kinerja.


## 3. Pemangku Kepentingan dan Peran


| Peran | Tanggung jawab utama | Akses yang diusulkan |
| --- | --- | --- |
| Admin penyaluran | Menyusun rencana, memperbaiki data yang belum disetujui, memantau status. | Buat/edit rencana; lihat penyaluran dan laporan internal. |
| Penyetuju internal | Meninjau kelengkapan rencana dan memberi keputusan sesuai kebijakan lembaga. | Setujui/tolak rencana internal bila peran ini dikonfirmasi. |
| Petugas lapangan | Melihat penugasan, mencatat hasil penyerahan, mengunggah bukti. | Lihat tugas sendiri; buat catatan realisasi; sinkronisasi offline. |
| Pemantau program | Mencatat progres, indikator, catatan tindak lanjut program berjangka. | Buat/baca catatan pemantauan sesuai program. |
| Administrator sistem | Mengelola akun internal, peran, dan konfigurasi teknis. | Kelola pengguna/role; tidak otomatis berwenang menyetujui dana. |
| Subsistem Pendataan & Verifikasi | Menyediakan penerima yang telah dinyatakan layak beserta golongan asnaf. | Integrasi hulu: baca data yang diperlukan. |
| Subsistem Pengelolaan Dana per Peruntukan | Memeriksa saldo/peruntukan; menyetujui atau menolak sebelum penyaluran. | Integrasi hulu: permintaan persetujuan/reservasi/finalisasi. |
| Subsistem Manajemen Kampanye Penghimpunan | Menyediakan data dana kampanye yang tersedia. | Integrasi hulu sesuai kontrak API. |
| Subsistem Pelaporan Publik & Transparansi Dana | Mengambil rekapitulasi penyaluran per program. | Integrasi hilir melalui kontrak API. |

Nama individu dan kewenangan final belum tersedia pada workbook dan harus dimasukkan ke Stakeholder Register setelah wawancara.


## 4. Alur Bisnis


### 4.1 Alur Usulan (To-Be)

1. Pengguna internal masuk ke aplikasi. Sistem memvalidasi akun dan hak akses berdasarkan peran.
1. Admin memilih program dan mengambil daftar penerima yang telah dinyatakan layak oleh subsistem Pendataan dan Verifikasi Penerima Manfaat.
1. Admin membuat rencana penyaluran berisi program, penerima, nominal, jadwal, sumber/peruntukan dana, dan catatan yang diperlukan.
1. Sistem memeriksa kelengkapan dan mengirim permintaan pemeriksaan saldo/peruntukan kepada subsistem Pengelolaan Dana per Peruntukan.
1. Jika ditolak atau saldo tidak cukup, rencana ditandai perlu revisi/ditolak, alasan dicatat, dan penyaluran tidak boleh dijalankan.
1. Jika disetujui, saldo direservasi saat rencana disiapkan. Reservasi mencegah dua rencana memakai alokasi yang sama.
1. Admin menugaskan petugas lapangan dan menetapkan jadwal. Rincian tugas tersedia di perangkat petugas.
1. Petugas melakukan penyerahan. Petugas mencatat hasil, waktu, lokasi bila diperlukan, nominal/barang, bukti serah terima, dan tanda tangan jika mekanisme ini disetujui klien.
1. Jika penerima tidak ditemui atau penyerahan gagal, petugas mencatat alasan dan status tindak lanjut; penjadwalan relawan berada di subsistem lain.
1. Jika penyerahan terbukti, sistem memfinalisasi realisasi dan meminta pengurangan saldo pada sistem hulu. Status tidak boleh menjadi selesai hanya karena rencana disetujui.
1. Untuk program berjangka, pemantau menambahkan perkembangan, indikator, catatan, dan tindak lanjut sesuai periode pemantauan.
1. Sistem menyediakan rekapitulasi penyaluran kepada subsistem Pelaporan Publik dan Transparansi Dana melalui API.

### 4.2 Diagram/Flowchart Proses Registrasi dan Penyaluran

Diagram berikut mencakup registrasi/login akun internal dan pembuatan rencana penyaluran. Registrasi/penetapan kelayakan penerima manfaat bukan kewenangan subsistem ini; data penerima diambil dari subsistem hulu setelah diverifikasi.


![Diagram alur registrasi dan penyaluran](diagram_alur_registrasi_penyaluran.png)


### 4.3 Alur Pengecualian


| Kondisi | Perilaku sistem yang diharapkan |
| --- | --- |
| Akun tidak valid / tidak berwenang | Tolak akses, catat peristiwa keamanan yang relevan, tampilkan pesan aman. |
| Data penerima tidak ditemukan atau status belum layak | Jangan izinkan penerima dimasukkan ke rencana; arahkan admin memeriksa subsistem hulu. |
| Saldo tidak cukup / persetujuan ditolak | Jangan izinkan status siap dijalankan; simpan alasan penolakan dan sediakan revisi. |
| Jaringan terputus saat penyerahan | Simpan catatan lokal dengan status menunggu sinkronisasi; tampilkan status sinkronisasi. |
| Penerima tidak ditemui | Catat gagal/tidak tersalurkan dan alasan; jangan finalisasi saldo sebagai penyaluran selesai. |
| Bukti tidak lengkap | Tandai belum lengkap; jangan menyelesaikan realisasi sampai syarat bukti terpenuhi atau pengecualian disetujui. |
| Sinkronisasi data berulang | Gunakan ID unik/idempotensi agar satu catatan offline tidak tercatat dua kali. |
| API sistem hulu tidak tersedia | Tandai permintaan tertunda/gagal secara eksplisit; jangan menganggap persetujuan berhasil. |


### 4.4 Aturan Bisnis


| ID | Aturan bisnis |
| --- | --- |
| AB-01 | Hanya penerima yang sudah dinyatakan layak oleh subsistem hulu yang dapat dipilih untuk rencana penyaluran. |
| AB-02 | Penyaluran tidak boleh dijalankan sebelum persetujuan saldo/peruntukan diterima. |
| AB-03 | Reservasi saldo dilakukan pada saat rencana disetujui; pengurangan saldo dilakukan setelah penyerahan terbukti. Keduanya adalah langkah berbeda. |
| AB-04 | Status rencana, tugas lapangan, realisasi, dan pemantauan harus dibedakan; persetujuan rencana tidak sama dengan bukti penyerahan. |
| AB-05 | Setiap perubahan status penting menyimpan pelaku dan waktu perubahan. |
| AB-06 | Bukti foto dan data pribadi hanya boleh diakses sesuai peran dan tujuan yang sah; publikasi memerlukan dasar/izin sesuai kebijakan lembaga. |
| AB-07 | Struktur database subsistem lain tidak diakses langsung; integrasi dilakukan melalui kontrak API. |
| AB-08 [KONFIRMASI] | Jenis bukti yang sah (foto, tanda tangan elektronik di layar, berita acara, atau kombinasinya) harus ditetapkan klien. |
| AB-09 [KONFIRMASI] | Batas nominal dan tingkat persetujuan tambahan ditentukan setelah wawancara klien. |
| AB-10 [KONFIRMASI] | Frekuensi pemantauan, indikator program, serta aturan penjadwalan ulang ditetapkan berdasarkan jenis program. |


### 4.5 Pertanyaan yang Wajib Divalidasi dengan Klien

- Bukti apa yang dianggap sah untuk setiap jenis bantuan: foto, tanda tangan, berita acara, bukti transfer, atau kombinasi?
- Apakah penyerahan selalu dihadiri petugas Baitulmal Tazkia, atau ada transfer langsung/tokoh masyarakat?
- Apakah tanda tangan penerima boleh direkam pada layar perangkat petugas? Bagaimana bila penerima menolak?
- Apakah rencana disusun bulanan atau mengikuti kejadian/permintaan?
- Siapa yang menyetujui penyaluran dan apakah ada batas nominal yang memerlukan persetujuan lebih tinggi?
- Program mana yang sekali bayar dan mana yang bertahap? Indikator apa yang dipantau?
- Apa prosedur bila penerima tidak ditemui, menolak bantuan, atau data penerima berubah?
- Bagaimana pola offline-first dan sinkronisasi diselaraskan dengan subsistem Penerimaan Donasi Luring?

## 5. Kebutuhan Fungsional dan Daftar Modul

Prioritas MoSCoW di bawah adalah usulan awal dan harus disepakati saat review. MUST = wajib untuk alur inti; SHOULD = penting; COULD = tambahan jika waktu memungkinkan.


### MOD-01 — Autentikasi dan Manajemen Pengguna (MUST)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-001 | Sistem harus menyediakan login bagi pengguna internal. | Akun valid dapat masuk; akun tidak valid ditolak dengan pesan yang aman. |
| FR-002 | Sistem harus menerapkan otorisasi berbasis peran pada halaman dan endpoint API. | Pengguna dengan peran rendah tidak dapat memanggil endpoint berwenang tinggi secara langsung. |
| FR-003 | Administrator harus dapat mengaktifkan, menonaktifkan, dan mengubah peran akun sesuai kewenangan. | Perubahan peran tercatat dalam audit trail. |
| FR-004 | Sistem harus menyimpan kata sandi dalam bentuk hash menggunakan algoritma khusus penyimpanan kata sandi dan tidak menyimpan kredensial di repository. | Pemeriksaan kode/repository tidak menemukan kata sandi atau signing key. |


### MOD-02 — Integrasi Data Penerima Manfaat (MUST)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-005 | Sistem harus mengambil daftar penerima yang telah diverifikasi dari API subsistem hulu. | Hanya penerima dengan status layak yang ditampilkan untuk dipilih. |
| FR-006 | Sistem harus menampilkan identitas minimum yang diperlukan untuk membedakan penerima. | Data sensitif yang tidak diperlukan tidak ditampilkan pada layar petugas. |
| FR-007 | Sistem harus menangani kegagalan API hulu tanpa menganggap data terbaru atau persetujuan tersedia. | Pengguna melihat status integrasi gagal/tertunda dan dapat mencoba ulang. |


### MOD-03 — Perencanaan Penyaluran (MUST)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-008 | Admin harus dapat membuat rencana penyaluran per program dengan penerima, nominal, jadwal, peruntukan, dan catatan. | Rencana valid tersimpan dengan ID unik dan status awal. |
| FR-009 | Sistem harus memvalidasi data wajib dan format nominal/tanggal di browser dan server. | Permintaan langsung ke API dengan data tidak valid ditolak. |
| FR-010 | Sistem harus menampilkan daftar rencana dan filter menurut program, status, periode, dan petugas. | Filter menghasilkan daftar yang konsisten dengan kriteria. |
| FR-011 | Sistem harus mendukung perubahan rencana sebelum disetujui dan merekam riwayat perubahan. | Perubahan setelah persetujuan mengikuti alur revisi yang disepakati. |


### MOD-04 — Persetujuan dan Reservasi Saldo (MUST)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-012 | Sistem harus mengirim permintaan pemeriksaan saldo/peruntukan ke subsistem Pengelolaan Dana per Peruntukan. | Permintaan dan respons tersimpan dengan ID korelasi/status. |
| FR-013 | Sistem hanya boleh menandai rencana siap dijalankan setelah persetujuan saldo diterima. | Rencana tanpa persetujuan tidak dapat diteruskan ke penugasan/realisasi. |
| FR-014 | Sistem harus meminta reservasi saldo pada saat rencana disetujui dan menghindari pemakaian alokasi yang sama oleh dua rencana bersamaan. | Uji konkurensi tidak menghasilkan reservasi ganda melebihi saldo. |
| FR-015 | Sistem harus mengirim permintaan finalisasi/pengurangan saldo setelah penyerahan terbukti. | Penyerahan gagal tidak mengurangi saldo sebagai realisasi selesai. |
| FR-016 | Sistem harus mencatat alasan penolakan dan menyediakan alur revisi. | Alasan dapat dilihat oleh peran yang berwenang. |


### MOD-05 — Penugasan dan Jadwal Lapangan (SHOULD)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-017 | Admin harus dapat menetapkan petugas penanggung jawab pada rencana yang disetujui. | Tugas tampil pada akun petugas terkait. |
| FR-018 | Petugas harus dapat melihat rincian tugas dan statusnya dari perangkat bergerak. | Tampilan terbaca pada lebar layar telepon. |
| FR-019 | Sistem harus mencatat perubahan petugas/jadwal oleh pengguna berwenang. | Riwayat perubahan menyimpan pelaku, waktu, dan alasan. |


### MOD-06 — Pencatatan Realisasi dan Bukti Serah Terima (MUST)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-020 | Petugas harus dapat mencatat hasil penyerahan: berhasil, gagal/tidak ditemui, ditunda, atau status lain yang disepakati. | Setiap hasil memiliki waktu, pelaku, dan alasan jika tidak berhasil. |
| FR-021 | Sistem harus mendukung lampiran bukti serah terima sesuai kebijakan klien. | Bukti dapat ditautkan ke satu realisasi dan aksesnya dibatasi. |
| FR-022 | Jika disetujui klien, sistem harus mendukung tanda tangan penerima pada perangkat; penolakan tanda tangan harus memiliki prosedur alternatif. | Penolakan tidak menyebabkan data diam-diam dianggap lengkap. |
| FR-023 | Sistem harus mencegah realisasi berstatus selesai jika syarat bukti wajib belum terpenuhi. | Uji bukti yang tidak lengkap menahan status selesai. |
| FR-024 | Sistem harus menjaga agar status penyaluran tidak berubah menjadi berhasil hanya karena rencana telah disetujui. | Penyelesaian memerlukan catatan realisasi yang sah. |


### MOD-07 — Offline-First dan Sinkronisasi (MUST)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-025 | Aplikasi lapangan harus dapat menyimpan catatan realisasi saat jaringan tidak tersedia. | Catatan tersimpan lokal dan ditandai menunggu sinkronisasi. |
| FR-026 | Sistem harus menyinkronkan catatan lokal saat koneksi pulih dan menampilkan hasil sinkronisasi. | Pengguna dapat membedakan tersimpan lokal, tersinkron, dan gagal. |
| FR-027 | Sistem harus menangani retry dan mencegah duplikasi catatan saat sinkronisasi diulang. | Pengiriman ulang ID yang sama tidak membuat realisasi kedua. |
| FR-028 | Sistem harus menangani konflik perubahan dengan aturan yang ditentukan dan tidak menimpa data tanpa jejak. | Konflik dicatat dan ditampilkan untuk tindak lanjut. |


### MOD-08 — Pemantauan Program Berjangka (MUST)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-029 | Pemantau harus dapat membuat catatan perkembangan untuk program yang memerlukan pemantauan lanjutan. | Catatan terhubung dengan program dan penerima/kelompok sasaran. |
| FR-030 | Sistem harus mendukung pencatatan indikator, periode, hasil, kendala, dan tindak lanjut sesuai konfigurasi program. | Data wajib mengikuti jenis program yang dikonfigurasi. |
| FR-031 | Sistem harus menampilkan riwayat pemantauan secara kronologis. | Riwayat hanya terlihat oleh peran yang berwenang. |
| FR-032 | Sistem harus menandai pemantauan yang terlambat atau tindak lanjut yang belum selesai sesuai aturan yang disepakati. | Daftar pemantauan tertunda dapat difilter. |


### MOD-09 — Rekapitulasi dan API Pelaporan (MUST)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-033 | Sistem harus menyediakan rekapitulasi penyaluran per program, periode, status, dan nominal. | Hasil rekap dapat dibandingkan dengan data detail. |
| FR-034 | Sistem harus menyediakan data bagi subsistem Pelaporan Publik dan Transparansi Dana melalui kontrak API. | Endpoint sesuai spesifikasi OpenAPI yang disepakati. |
| FR-035 | Sistem harus memisahkan data internal terperinci dari data yang boleh digunakan untuk pelaporan publik. | API tidak mengungkap data pribadi yang tidak dibutuhkan. |
| FR-036 | Sistem harus mencatat kegagalan permintaan API dan menyediakan mekanisme retry yang aman. | Kegagalan tercatat dan tidak menyebabkan data ganda. |


### MOD-10 — Audit Trail dan Keamanan Data (MUST)


| ID | Kebutuhan fungsional | Kriteria penerimaan ringkas |
| --- | --- | --- |
| FR-037 | Sistem harus mencatat perubahan penting pada rencana, persetujuan, realisasi, bukti, dan pemantauan. | Log memuat pelaku, waktu, objek, dan jenis perubahan. |
| FR-038 | Sistem harus membatasi akses bukti dan data penerima berdasarkan peran serta kebutuhan kerja. | Pengguna tanpa izin menerima penolakan akses. |
| FR-039 | Sistem harus menyediakan pengelolaan masa simpan dan penghapusan/penyamaran data sesuai kebijakan yang disetujui. | Prosedur dapat diuji dan memiliki jejak pelaksanaan. |
| FR-040 | Sistem harus memproses foto atau dokumen penerima hanya untuk tujuan yang sah dan menghindari publikasi tanpa otorisasi yang sesuai. | Bukti internal tidak otomatis menjadi materi publik. |


## 6. Kebutuhan Nonfungsional


| ID | Aspek | Pernyataan kebutuhan | Cara verifikasi |
| --- | --- | --- | --- |
| NFR-001 | Keamanan akses | Seluruh endpoint privat memeriksa autentikasi dan otorisasi di sisi server; tidak hanya menyembunyikan tombol di antarmuka. | Uji akses langsung dengan peran tidak berwenang ditolak. |
| NFR-002 | Pelindungan data pribadi | Pengumpulan, penggunaan, penyimpanan, dan pembagian data penerima dibatasi pada kebutuhan proses dan dasar pemrosesan yang sah; data pengembangan harus sintetis sampai perjanjian pemrosesan dan kerahasiaan ditandatangani. | Tidak ada data nyata pada lingkungan pengembangan sebelum prasyarat dipenuhi. |
| NFR-003 | Kerahasiaan bukti | Bukti foto/dokumen disimpan pada lokasi terlindungi dan tidak dapat diakses hanya dengan menebak URL. | Pengguna tanpa izin tidak dapat membuka bukti. |
| NFR-004 | Kredensial | Kredensial produksi, token signing key, dan rahasia konfigurasi berada di konfigurasi/secret manager di luar repository. | Secret scanning lulus. |
| NFR-005 | Ketersediaan lapangan | Fungsi inti pencatatan realisasi tetap tersedia saat koneksi terputus, dengan indikator status lokal dan sinkronisasi. | Skenario uji tanpa jaringan lulus. |
| NFR-006 | Integritas data | Operasi reservasi saldo dan sinkronisasi memiliki kontrol transaksi/idempotensi untuk mencegah duplikasi dan saldo terpakai ganda. | Uji konkurensi dan retry lulus. |
| NFR-007 | Kemudahan penggunaan | Antarmuka petugas responsif, ringkas, dan meminimalkan input ulang di lapangan. | UAT oleh petugas lapangan menyelesaikan skenario inti tanpa bantuan pengembang. |
| NFR-008 | Interoperabilitas | Integrasi antarsubsistem memakai kontrak API terdokumentasi dan tidak mengakses database subsistem lain secara langsung. | Validasi OpenAPI dan integration test lulus. |
| NFR-009 | Auditabilitas | Perubahan status kritis dapat ditelusuri ke pelaku dan waktu; log tidak mudah diubah oleh pengguna biasa. | Pengujian audit trail lulus. |
| NFR-010 | Kinerja | Waktu respons target dan kapasitas ditentukan setelah volume transaksi/pengguna diketahui dari klien. | Target numerik ditetapkan dan diuji sebelum UAT final. |
| NFR-011 | Keandalan | Kegagalan integrasi, validasi, dan sinkronisasi menghasilkan status serta pesan yang dapat ditindaklanjuti; tidak ada exception yang diabaikan. | Uji kegagalan menghasilkan log dan respons yang tepat. |
| NFR-012 | Pemeliharaan | Kode dipisahkan ke controller, service, dan repository; konfigurasi dipisahkan dari kode; migrasi dan test otomatis tersedia. | Pipeline menjalankan test, migrasi, secret scanning, validasi API, dan health check. |


## 7. Use Case Utama


### UC-01 — Login pengguna internal

Aktor: Admin, petugas, pemantau

Prakondisi: Akun aktif tersedia dan pengguna memiliki kredensial.

Alur utama: 1) Pengguna memasukkan kredensial. 2) Sistem memvalidasi. 3) Sistem memuat peran. 4) Dashboard sesuai peran ditampilkan.

Alur alternatif/kegagalan: Kredensial salah, akun nonaktif, atau peran tidak sesuai menyebabkan akses ditolak.


### UC-02 — Membuat rencana penyaluran

Aktor: Admin penyaluran

Prakondisi: Program aktif dan data penerima layak tersedia dari sistem hulu.

Alur utama: 1) Admin memilih program. 2) Sistem mengambil daftar penerima layak. 3) Admin mengisi penerima, nominal, jadwal, dan peruntukan. 4) Sistem memvalidasi. 5) Rencana disimpan sebagai draft.

Alur alternatif/kegagalan: API penerima tidak tersedia; penerima belum layak; data wajib kosong.


### UC-03 — Meminta persetujuan dan reservasi saldo

Aktor: Admin/sistem; subsistem Pengelolaan Dana

Prakondisi: Rencana valid dan sumber dana teridentifikasi.

Alur utama: 1) Sistem mengirim permintaan. 2) Sistem menerima keputusan. 3) Jika disetujui, reservasi dibuat. 4) Status berubah menjadi siap ditugaskan.

Alur alternatif/kegagalan: Ditolak, saldo kurang, API timeout, respons duplikat.


### UC-04 — Mencatat penyerahan di lapangan

Aktor: Petugas lapangan

Prakondisi: Tugas sudah ditugaskan dan rencana disetujui.

Alur utama: 1) Petugas membuka tugas. 2) Mengonfirmasi penerima. 3) Mencatat hasil penyerahan. 4) Melampirkan bukti. 5) Menyimpan/sinkronisasi. 6) Sistem memvalidasi kelengkapan.

Alur alternatif/kegagalan: Penerima tidak ditemui, jaringan mati, bukti kurang, tanda tangan ditolak.


### UC-05 — Memantau program berjangka

Aktor: Pemantau program

Prakondisi: Program memerlukan pemantauan dan periode pemantauan telah ditentukan.

Alur utama: 1) Pemantau membuka program. 2) Mengisi indikator dan catatan. 3) Menyimpan hasil. 4) Sistem menampilkan riwayat dan tindak lanjut.

Alur alternatif/kegagalan: Data indikator tidak lengkap atau pengguna tidak berwenang.


### UC-06 — Mengambil rekap penyaluran

Aktor: Subsistem Pelaporan Publik & Transparansi Dana

Prakondisi: Kontrak API dan kredensial antarsistem tersedia.

Alur utama: 1) Sistem hilir memanggil endpoint. 2) Sistem memeriksa akses dan parameter. 3) Sistem mengembalikan rekap sesuai filter tanpa data pribadi berlebih.

Alur alternatif/kegagalan: Token tidak valid, parameter salah, layanan sementara tidak tersedia.


## 8. Data Utama dan Status


### 8.1 Entitas Data Usulan


| Entitas | Atribut minimum (usulan) | Catatan |
| --- | --- | --- |
| Pengguna | user_id, nama, identitas login, status akun, role_id | Kredensial tidak disimpan sebagai teks biasa. |
| Program | program_id, nama, jenis bantuan, status, perlu_pemantauan | Data program sesuai referensi/konfigurasi yang disetujui. |
| Penerima referensi | beneficiary_ref, nama tampilan minimum, status kelayakan, asnaf bila relevan | Data sumber berasal dari API hulu; bukan master kelayakan subsistem ini. |
| Rencana penyaluran | plan_id, program_id, penerima_ref, nominal, jadwal, peruntukan_ref, status | ID eksternal disimpan sebagai referensi API, bukan foreign key lintas database. |
| Persetujuan/reservasi | approval_id, plan_id, keputusan, nominal reservasi, status, waktu, correlation_id | Sumber kebenaran saldo tetap subsistem dana. |
| Penugasan | assignment_id, plan_id, petugas_ref, jadwal, status | Penjadwalan relawan tetap di subsistem relawan bila relevan. |
| Realisasi | delivery_id, plan_id, hasil, waktu, catatan, status_sinkronisasi | Memiliki ID idempotensi untuk sinkronisasi offline. |
| Bukti serah terima | evidence_id, delivery_id, jenis, lokasi file terlindungi, metadata persetujuan bila perlu | Jenis bukti final perlu konfirmasi klien. |
| Catatan pemantauan | monitoring_id, program_id, penerima_ref/target_ref, periode, indikator, hasil, tindak_lanjut | Struktur indikator bisa bervariasi sesuai program. |
| Audit event | event_id, actor_ref, action, object_ref, timestamp, metadata perubahan | Hindari menyimpan data pribadi berlebihan di log. |


### 8.2 Status Proses yang Diusulkan


| Objek | Status contoh | Aturan transisi utama |
| --- | --- | --- |
| Rencana | Draft → Menunggu Persetujuan → Disetujui/ Ditolak → Siap Ditugaskan → Dalam Pelaksanaan → Selesai/ Dibatalkan | Tidak boleh menjadi Siap Ditugaskan tanpa persetujuan saldo. |
| Penugasan | Ditugaskan → Dilihat Petugas → Dalam Pelaksanaan → Selesai/Gagal/Dijadwalkan Ulang | Status selesai harus mengacu pada realisasi yang tervalidasi. |
| Realisasi | Draft Lokal → Menunggu Sinkronisasi → Tersinkron → Terverifikasi / Perlu Perbaikan | Tidak boleh mengurangi saldo sebagai realisasi selesai sebelum bukti sah terverifikasi. |
| Pemantauan | Belum Dimulai → Terjadwal → Tercatat → Tindak Lanjut → Selesai | Aturan periode dan indikator disesuaikan per jenis program. |


## 9. Antarmuka dan Integrasi


### 9.1 Antarmuka Pengguna

- Dashboard per peran: rencana menunggu persetujuan, tugas lapangan, penyaluran tertunda, dan pemantauan jatuh tempo.
- Halaman rencana: daftar, filter, formulir buat/edit, rincian persetujuan, dan riwayat perubahan.
- Halaman petugas lapangan: daftar tugas, rincian penerima minimum, formulir hasil, bukti, serta status offline/sinkronisasi.
- Halaman pemantauan: riwayat perkembangan, indikator, kendala, dan tindak lanjut.
- Halaman rekap internal: ringkasan per program, periode, status, dan nominal sesuai hak akses.

### 9.2 Integrasi Antarsubsistem


| Sistem terkait | Arah | Data/operasi | Ketentuan |
| --- | --- | --- | --- |
| Pendataan dan Verifikasi Penerima Manfaat | Masuk | Daftar penerima layak dan golongan asnaf bila diperlukan | Hanya melalui kontrak API; kelayakan tidak diputuskan oleh subsistem ini. |
| Pengelolaan Dana per Peruntukan | Dua arah | Pemeriksaan saldo, keputusan persetujuan, reservasi, finalisasi pengurangan saldo | Pemesanan saldo dan pengurangan saldo adalah dua langkah terpisah. |
| Manajemen Kampanye Penghimpunan | Masuk | Data dana kampanye terkumpul yang dapat menjadi sumber anggaran | Definisi data dan endpoint perlu disepakati. |
| Pelaporan Publik dan Transparansi Dana | Keluar | Rekap penyaluran per program | API hanya mengirim data yang diperlukan untuk pelaporan. |
| Balaka | Keluar/koordinasi | Jurnal akuntansi tidak dikelola di subsistem ini | Jika dibutuhkan, integrasi ditentukan melalui kesepakatan antartim. |


### 9.3 Kontrak API

Endpoint, skema JSON, autentikasi antarsistem, kode status HTTP, pagination, retry, idempotency key, dan penanganan timeout harus dituangkan dalam spesifikasi OpenAPI. Nama endpoint final tidak ditetapkan di dokumen ini karena workbook mengharuskan kontrak API disepakati bersama kelompok terkait.


| Kondisi | Respons perilaku API |
| --- | --- |
| Permintaan valid | Respons sukses dengan data dan metadata yang disepakati. |
| Masukan tidak valid | Kode 4xx yang sesuai dan pesan validasi yang aman. |
| Tidak terautentikasi/tidak berwenang | Kode 401/403 sesuai konteks; tidak membocorkan informasi sensitif. |
| Layanan hulu gagal | Status integrasi tertunda/gagal; jangan menganggap persetujuan sukses. |
| Permintaan berulang | Idempotensi untuk operasi yang dapat menimbulkan reservasi atau realisasi ganda. |


## 10. Standar, Regulasi, dan Tata Kelola


### 10.1 Acuan Penyusunan


| Acuan | Penerapan dalam dokumen/proyek | Catatan status |
| --- | --- | --- |
| ISO/IEC/IEEE 29148 — Requirements Engineering | Struktur SRS, identifikasi kebutuhan, kebutuhan fungsional/nonfungsional, kriteria penerimaan dan penelusuran kebutuhan. | Acuan yang secara eksplisit direkomendasikan workbook untuk artefak SRS; dokumen ini bukan klaim sertifikasi. |
| SNI ISO/IEC 27001 (edisi/adopsi yang berlaku perlu diverifikasi melalui katalog BSN) | Acuan sistem manajemen keamanan informasi: kontrol akses, perlindungan informasi, pengelolaan risiko, dan pengendalian akses bukti. | Perlu konfirmasi edisi SNI terkini dan kebijakan organisasi sebelum dinyatakan sebagai standar wajib. |
| Undang-Undang Republik Indonesia Nomor 27 Tahun 2022 tentang Pelindungan Data Pribadi | Pembatasan tujuan, perlindungan data penerima, pengaturan akses, dan tata kelola pemrosesan data pribadi. | Rujukan regulasi yang disebut workbook; implementasi hukum ditinjau oleh pihak berwenang. |
| CMMI-DEV v1.3 / target praktik CMMI tingkat 3 sebagaimana workbook | Pengelolaan kebutuhan, risiko, verifikasi/validasi, peer review, change control, dan bukti tertulis. | Workbook menyebut target CMMI tingkat 3; SRS ini perlu melalui review dan sign-off. |


### 10.2 Pengendalian Pelindungan Data

- Sebelum data nyata disimpan pada perangkat mahasiswa/pengembangan, perjanjian pemrosesan data antara Baitulmal Tazkia dan STMIK Tazkia serta perjanjian kerahasiaan per mahasiswa harus ditandatangani; sampai itu dilakukan, gunakan data sintetis.
- Jangan menyimpan kredensial produksi, kata sandi, token rahasia, atau signing key dalam repository.
- Batasi data penerima yang ditampilkan pada perangkat lapangan sesuai kebutuhan pelaksanaan tugas.
- Bukti foto yang memuat wajah penerima tidak boleh otomatis dipakai untuk laporan publik; kebijakan penggunaan/persetujuan dan alternatif bukti perlu ditetapkan.
- Tetapkan hak akses, masa simpan, penghapusan, backup, penanganan insiden, dan jejak audit bersama pemilik data.

### 10.3 Change Control dan Baseline

Setelah SRS memperoleh sign-off, perubahan dilakukan melalui usulan tertulis, analisis dampak terhadap lingkup/jadwal/pengujian, keputusan pemilik baseline, pembaruan versi, serta pembaruan RTM. Setiap review memiliki catatan tertulis dengan status akhir: diperbaiki, ditolak dengan alasan, atau ditunda dengan tanggal.


## 11. Matriks Penelusuran Kebutuhan (RTM)


| Kebutuhan | Modul | Use case | Rencana uji |
| --- | --- | --- | --- |
| FR-001–004 | MOD-01 | UC-01 | TC-AUTH-01 s.d. 04 |
| FR-005–007 | MOD-02 | UC-02 | TC-BEN-01 s.d. 03 |
| FR-008–011 | MOD-03 | UC-02 | TC-PLAN-01 s.d. 05 |
| FR-012–016 | MOD-04 | UC-03 | TC-FUND-01 s.d. 06 |
| FR-017–019 | MOD-05 | UC-04 | TC-ASG-01 s.d. 03 |
| FR-020–024 | MOD-06 | UC-04 | TC-DEL-01 s.d. 06 |
| FR-025–028 | MOD-07 | UC-04 | TC-OFF-01 s.d. 05 |
| FR-029–032 | MOD-08 | UC-05 | TC-MON-01 s.d. 04 |
| FR-033–036 | MOD-09 | UC-06 | TC-API-01 s.d. 05 |
| FR-037–040 | MOD-10 | UC-01 s.d. UC-06 | TC-AUD-01 s.d. 04 |
| NFR-001–004 | MOD-01, MOD-10 | UC-01 s.d. UC-06 | TC-SEC-01 s.d. 08 |
| NFR-005–006 | MOD-07, MOD-04 | UC-03, UC-04 | TC-REL-01 s.d. 05 |
| NFR-007–008 | MOD-05, MOD-09 | UC-04, UC-06 | TC-UX-01; TC-API-01 |
| NFR-009–012 | MOD-10, seluruh modul | Semua use case | TC-AUD-01; TC-PIPE-01 s.d. 05 |

RTM ini merupakan pemetaan awal. Setelah rancangan teknis dan test case final dibuat, penelusuran harus dua arah: kebutuhan ke desain dan pengujian, serta desain/pengujian kembali ke kebutuhan.


## 12. Rencana Verifikasi dan Kriteria Penerimaan


| ID skenario | Skenario uji | Kriteria lulus |
| --- | --- | --- |
| TC-01 | Login dengan akun valid dan invalid | Akun valid masuk sesuai peran; invalid ditolak. |
| TC-02 | Akses endpoint admin oleh petugas lapangan | Permintaan ditolak di sisi server. |
| TC-03 | Membuat rencana dengan data wajib kosong | Server menolak dan menunjukkan field yang perlu diperbaiki. |
| TC-04 | Mencoba menjalankan rencana tanpa persetujuan saldo | Status tidak dapat berubah menjadi siap dijalankan. |
| TC-05 | Dua rencana bersamaan meminta saldo yang sama | Reservasi tidak melampaui saldo tersedia dan tidak terjadi pemakaian ganda. |
| TC-06 | Penyerahan gagal/tidak menemui penerima | Status gagal/ditunda tercatat; realisasi tidak dianggap selesai. |
| TC-07 | Penyerahan berhasil tanpa bukti wajib | Status selesai ditahan sampai syarat bukti dipenuhi atau pengecualian resmi diterapkan. |
| TC-08 | Catat realisasi saat offline lalu sinkronkan dua kali | Data tetap satu kali dan status sinkronisasi jelas. |
| TC-09 | API hulu timeout | Sistem tidak mengasumsikan persetujuan berhasil; error tercatat dan dapat dicoba ulang. |
| TC-10 | Tambahkan catatan pemantauan program berjangka | Catatan tersimpan dengan periode/indikator dan muncul pada riwayat. |
| TC-11 | API rekap dipanggil oleh sistem hilir | Respons sesuai kontrak; tidak ada data pribadi berlebihan. |
| TC-12 | Audit perubahan rencana/realisasi | Pelaku, waktu, objek, dan perubahan dapat ditelusuri. |
| TC-13 | Jalankan migrasi dan test suite dari keadaan bersih | Migrasi berhasil dan semua test lulus. |
| TC-14 | Pemeriksaan repository | Tidak ada kredensial/secret; konfigurasi sensitif berada di luar kode. |


### 12.1 Kriteria Masuk UAT

- SRS dan use case telah direview dan disetujui narasumber yang berwenang.
- Fungsi MUST selesai dan build kandidat UAT tersedia.
- Test suite otomatis dan integration test utama lulus.
- Data uji sintetis tersedia dan tidak menggunakan data nyata tanpa perjanjian yang disyaratkan.
- Kontrak API dan skenario kegagalan integrasi terdokumentasi.

### 12.2 Kriteria Keluar UAT

- Seluruh skenario kritis terkait persetujuan saldo, realisasi, bukti, offline-first, dan otorisasi lulus.
- Setiap defect memiliki disposisi tertulis: diperbaiki, diterima dengan alasan, atau ditunda dengan tanggal dan pemilik.
- Tidak ada defect kritis terbuka yang mengakibatkan penyaluran tanpa persetujuan, duplikasi saldo, atau kebocoran data.
- Klien menandatangani hasil UAT atau mencatat penolakan dan tindak lanjut.

## 13. Risiko dan Mitigasi


| ID | Risiko | Dampak | Mitigasi awal | Pemilik usulan |
| --- | --- | --- | --- | --- |
| R-01 | Bantuan tercatat tersalurkan padahal belum diterima | Laporan kepada donatur keliru | Pisahkan status rencana dan realisasi; wajibkan bukti dan audit trail. | Product owner/Admin penyaluran |
| R-02 | Petugas tetap menggunakan WhatsApp karena aplikasi lambat | Data tetap tersebar; pekerjaan ganda | Uji usability lapangan; minimalkan input; offline-first. | Koordinator petugas |
| R-03 | Foto memuat wajah penerima tanpa izin penggunaan | Pelanggaran privasi | Batasi akses dan penggunaan; tetapkan kebijakan bukti dan publikasi. | Pemilik data/klien |
| R-04 | Penyaluran berjalan sebelum persetujuan saldo | Saldo negatif atau dana dipakai ganda | Gate persetujuan wajib dan reservasi atomik di sistem hulu. | Tim Pengelolaan Dana |
| R-05 | API hulu tidak tersedia | Rencana terhambat | Timeout/retry/status tertunda; tidak menganggap gagal sebagai setuju. | Tim integrasi |
| R-06 | Sinkronisasi offline membuat duplikasi | Realisasi atau saldo salah | ID idempotensi, kontrol konflik, dan pengujian retry. | Tim teknis |
| R-07 | Kebijakan bukti dan tanda tangan belum jelas | SRS atau implementasi salah asumsi | Wawancara/observasi dan sign-off sebelum baseline. | Analis bisnis |


## 14. Deliverable, Review, dan Persetujuan

Mengikuti workbook, SRS + RTM + model proses berjalan merupakan baseline fase kebutuhan. Draf direview dosen, direvisi, direview klien, direvisi, lalu ditandatangani pada siklus review tingkat A. Catatan review disimpan di repository. Setelah sign-off, perubahan wajib melalui change control.


| Pihak | Nama/Jabatan | Keputusan | Tanggal | Tanda tangan |
| --- | --- | --- | --- | --- |
| Perwakilan Baitulmal Tazkia | ________________ | Setuju / Revisi | ________ | ________________ |
| Dosen/reviewer | ________________ | Setuju / Revisi | ________ | ________________ |
| Ketua Kelompok 9 | ________________ | Diajukan | ________ | ________________ |


## Lampiran A — Daftar Pertanyaan Wawancara

- Bagaimana alur aktual dari rencana hingga bukti penyerahan lengkap? Siapa melakukan tiap langkah?
- Bukti apa yang dianggap sah untuk bantuan tunai dan non-tunai?
- Apakah ada penyerahan tanpa petugas hadir, misalnya transfer langsung atau melalui tokoh masyarakat?
- Bagaimana perlakuan jika penerima tidak ditemui, menolak, atau tidak dapat menandatangani?
- Siapa yang berwenang menyetujui penyaluran? Apakah ada ambang nominal?
- Bagaimana proses reservasi dan pengurangan saldo dilakukan di sistem hulu?
- Program apa yang sekali salur dan apa yang bertahap? Indikator apa yang perlu dipantau?
- Berapa jumlah penyaluran bulanan, pengguna, dan perkiraan ukuran bukti foto/dokumen?
- Perangkat apa yang digunakan petugas, dan seberapa sering jaringan tidak tersedia?
- Berapa lama data rencana, bukti, dan catatan pemantauan harus disimpan?
- Data apa yang boleh diteruskan ke laporan publik, dan siapa yang menyetujui publikasi?
- Bagaimana API antarkelompok akan mengautentikasi pemanggil, menangani retry, dan menandai permintaan duplikat?

## Lampiran B — Referensi

- WORKBOOK PROYEK: Penyaluran Bantuan dan Pemantauan Program, Kelompok 9 — Baitulmal Tazkia, STMIK Tazkia, Gasal 2026/2027. Terutama Bab 2 (Klien), Bab 3 (Lingkup Proyek), Bab 4–6 (fase, review, CMMI), dan Bab 7–8 (templat serta deliverable SRS/RTM/use case).
- ISO/IEC/IEEE 29148 — Requirements Engineering; acuan penyusunan Software Requirements Specification sebagaimana dirujuk pada workbook.
- Undang-Undang Republik Indonesia Nomor 27 Tahun 2022 tentang Pelindungan Data Pribadi.
- SNI ISO/IEC 27001 — acuan keamanan informasi; edisi/adopsi yang berlaku harus diverifikasi melalui katalog resmi BSN sebelum ditetapkan sebagai baseline kepatuhan.
Penting: dokumen ini adalah draf kerja berbasis workbook, bukan bukti bahwa sistem telah patuh/tersertifikasi terhadap standar. Seluruh bagian [KONFIRMASI] perlu diputuskan bersama klien sebelum sign-off.


---

**Catatan status dokumen:** SRS ini adalah draf untuk ditinjau bersama klien/dosen. Semua aturan bertanda [KONFIRMASI], pilihan bukti serah terima, kewenangan persetujuan, dan detail integrasi perlu divalidasi sebelum dokumen ditetapkan sebagai baseline.
