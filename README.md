# 📄 SIPENORA (Sistem Permintaan Nomor Surat)

SIPENORA adalah aplikasi berbasis web yang dirancang khusus untuk mempermudah dan mengotomatisasi pengambilan serta pencatatan nomor surat keluar di lingkungan **Lapas Kelas 1 Tangerang**. 

Sistem ini menggantikan pencatatan manual/spreadsheet dengan *database* terpusat, memastikan tidak ada nomor surat yang ganda, dan mempermudah pengarsipan.

## ✨ Fitur Utama
- **Penomoran Otomatis (Auto-Increment):** Sistem otomatis memberikan nomor urut surat terbaru berdasarkan Tahun dan Bidang/Divisi yang dipilih.
- **Formulir Responsif:** Antarmuka yang ramah pengguna, modern, dan mudah diakses melalui PC maupun *smartphone*.
- **Tampilan Riwayat Terkini:** Menampilkan 5 surat terakhir yang diterbitkan secara *real-time*.
- **Halaman Arsip & Rekapitulasi:** Dilengkapi dengan fitur filter dinamis berdasarkan **Tahun**, **Bulan**, dan **Bidang/Divisi**.
- **Cetak/Export PDF:** Fitur *backup* arsip dalam format PDF *Landscape* dengan data yang sudah diurutkan berdasarkan tanggal dan bidang.

## 🛠️ Teknologi yang Digunakan
Aplikasi ini berjalan sebagai *Static Web App* tanpa server (*serverless backend*), menggunakan:
- **Frontend:** HTML5, Vanilla JavaScript
- **Styling:** Tailwind CSS (via CDN)
- **Database / BaaS:** [Supabase](https://supabase.com/) (PostgreSQL)
- **Library Tambahan:** [jsPDF](https://parall.ax/products/jspdf) & jsPDF-AutoTable (untuk integrasi ekspor PDF di sisi klien)
- **Hosting / Deployment:** Vercel / Netlify / Cloudflare Pages

## 🗄️ Struktur Database (Supabase)
Tabel utama yang digunakan dalam sistem ini adalah `sipenora_surat`. Berikut adalah skema kolomnya:

| Nama Kolom | Tipe Data | Keterangan |
| :--- | :--- | :--- |
| `id` | int8 | Primary Key, Auto Increment |
| `created_at` | timestamptz | Waktu data masuk |
| `nama_pemohon` | varchar | Nama pegawai yang meminta nomor |
| `tanggal_surat` | date | Tanggal pembuatan surat |
| `konsep_nomor` | varchar | Format dasar nomor surat (contoh: PAS.1-UM.01.01) |
| `tujuan_surat` | varchar | Pihak yang dituju oleh surat |
| `perihal` | text | Isi/perihal surat |
| `bidang_tujuan` | varchar | Divisi yang mengajukan surat |
| `nomor_urut` | int4 | Angka urut surat yang di-reset setiap pergantian tahun |
| `nomor_surat_final` | varchar | Gabungan `konsep_nomor` dan `nomor_urut` |

> **Catatan Keamanan (RLS):** Konfigurasi *Row Level Security* (RLS) di Supabase diatur untuk mengizinkan `SELECT` dan `INSERT` secara publik (`true`) tanpa memerlukan otentikasi/login pengguna.
