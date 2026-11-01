# dekat. — photobooth buat berdua

Photobooth responsif untuk mengambil empat jepretan dan menggabungkannya menjadi strip kenangan. Dibuat sebagai web statis supaya mudah dipublikasikan dengan GitHub Pages.

## Jalankan

- Buka `index.html` lewat server lokal (misalnya ekstensi Live Server). Akses kamera membutuhkan `localhost` atau HTTPS.
- Pilih frame, izinkan kamera, buat ruang, lalu ambil foto. Hasil dapat diunduh sebagai JPG.

## Mengaktifkan ruang LDR dua perangkat

GitHub Pages hanya menyajikan frontend statis. Agar kode ruang dan foto tersinkron lintas perangkat, siapkan project Supabase:

1. Buat project di Supabase, salin **Project URL** dan **anon/public key**.
2. Masukkan keduanya di `config.js` (`supabaseUrl` dan `supabaseAnonKey`). Jangan pernah masukkan `service_role` key.
3. Pastikan Realtime diaktifkan untuk project. Aplikasi menggunakan channel Broadcast publik per kode ruang.
4. Push file proyek ini ke GitHub, lalu nyalakan **Settings → Pages → Deploy from a branch**.

> Sesi menyimpan jepretan sebagai pesan realtime, bukan objek database; channel publik berarti siapa pun yang mengetahui kode dapat bergabung. Gunakan kode ruang acak hanya dengan pasangan dan hindari foto sensitif. Untuk privasi lebih kuat, implementasikan channel private dengan autentikasi dan storage berakses terbatas.

## Mode lokal

Tanpa konfigurasi Supabase, tombol ruang bekerja di browser yang sama melalui `sessionStorage`; ini cocok untuk mencoba alur satu perangkat. Mode ini tidak menyinkronkan kode/foto lewat internet.

## Yang tersedia

- Kamera depan/belakang, timer 3/5/10 detik, foto webcam, dan progress.
- Dua foto (masing-masing satu perangkat) disusun menjadi satu strip.
- 12 frame warna, opsi upload PNG/WebP/SVG, unduh hasil JPG.
- Layout mobile-first dan kontrol akses kamera yang tetap di browser.

## Catatan browser

Kamera browser memerlukan secure context (`https://` atau `localhost`) serta izin kamera. Jika izin ditolak, ubah izin situs di pengaturan browser. Lihat [MDN: getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia).
