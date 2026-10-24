# SehatKu

**Layanan kesehatan terpadu**: aplikasi web untuk antrean, rekam medis, obat, dan rujukan di fasilitas kesehatan, dengan tampilan terpisah untuk pasien, petugas loket, dokter, apoteker, dan kader kesehatan.

Proyek ini dibuat bersama tim untuk sebuah hackathon. Repo ini adalah fork dari [marionmogens/hackathon_joints](https://github.com/marionmogens/hackathon_joints).

## Fitur

Menu yang tampil bergantung pada peran pengguna.

**Pasien**
- Antrean dan pra-triase: ambil nomor antrean dari rumah
- Jadwal dokter yang sedang praktik
- Kartu dan biaya (penjamin dan rincian biaya)
- Riwayat pemeriksaan, obat, dan hasil lab
- Alarm minum obat dengan konfirmasi dosis
- Rujukan: perpanjang dari rumah
- Kesehatan anak: tumbuh kembang dan imunisasi
- Data diri dan anggota keluarga
- SOS darurat: kirim lokasi ke petugas
- Pengaduan layanan

**Petugas loket**
- Loket dan panggilan antrean
- Pendaftaran kiosk
- Kasir dan penjaminan
- Laporan SOS dan pengaduan yang masuk
- Stok obat

**Dokter**
- Ruang periksa
- Rekam medis berdasarkan NIK
- Persetujuan rujukan

**Apoteker**
- Farmasi dan stok obat

**Kader kesehatan**
- Pantau kepatuhan minum obat
- Posyandu anak

## Teknologi

- [Next.js](https://nextjs.org) 16 (App Router) dan React 19
- [Supabase](https://supabase.com) (database PostgreSQL, autentikasi, dan row level security)
- Tailwind CSS 4

## Struktur

```
app/          # halaman (login, dashboard per fitur, antrean, petugas)
components/   # komponen UI bersama
lib/          # menu per peran, koneksi Supabase, triase, grafik pertumbuhan WHO
supabase/     # skema database dan data contoh
  schema.sql              # skema lengkap dan aturan akses per peran
  seed.sql                # data contoh fiktif
  jadikan-staf.sql        # ubah akun menjadi petugas, dokter, apoteker, atau kader
  migrasi-stok-obat.sql   # migrasi untuk database versi lama
```

## Cara menjalankan

1. Buat proyek di [Supabase](https://supabase.com).
2. Di **SQL Editor** Supabase, jalankan `supabase/schema.sql`, lalu `supabase/seed.sql`.
   `schema.sql` menghapus semua tabel di schema `public` sebelum membuatnya ulang, jadi jangan dijalankan di database yang sudah berisi data penting.
3. Buat file `.env.local` di akar proyek:
   ```
   NEXT_PUBLIC_SUPABASE_URL=https://<id-proyek>.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=<anon key dari Project Settings > API>
   ```
4. Pasang dependensi dan jalankan:
   ```bash
   npm install
   npm run dev
   ```
5. Buka <http://localhost:3000>.

### Membuat akun staf

Akun baru selalu berperan **pasien**. Untuk mencoba peran lain:

1. Daftarkan akun lewat halaman `/login`, misalnya `petugas@contoh.com`, `dokter@contoh.com`, `apoteker@contoh.com`, dan `kader@contoh.com`.
2. Jalankan `supabase/jadikan-staf.sql` di SQL Editor (email di file itu bisa disesuaikan).

## Catatan

- Semua data di `supabase/seed.sql` fiktif: fasilitas, dokter, dan pasien contoh (NIK berpola `99000000...`) bukan data sungguhan.
- Aplikasi ini dibuat untuk hackathon dan belum diuji untuk dipakai di fasilitas kesehatan sungguhan.
