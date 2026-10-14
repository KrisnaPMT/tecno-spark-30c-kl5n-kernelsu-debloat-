# TECNO Spark 30C KL5n | KernelSU Selective Debloat

Modul **KernelSU / KernelSU Next** untuk menonaktifkan sebagian aplikasi bawaan (**debloat**) TECNO Spark 30C **KL5n** secara selektif menggunakan Android Package Manager, tanpa menghapus APK pada partisi `/system`.

> **Peringatan:** Belum diuji langsung pada semua versi firmware TECNO Spark 30C KL5n. Gunakan dengan risiko sendiri, lakukan backup, dan pahami cara memulihkan package sebelum instalasi. Modul ini **bukan** penghapus permanen bloatware dan tidak menjanjikan peningkatan FPS atau baterai.

## Fitur

- Khusus perangkat berkode **KL5n** (ada pemeriksaan perangkat saat instalasi dan eksekusi).
- Memuat **43 package unik** dari daftar yang disediakan (satu package duplikat dalam data awal).
- **10 package** dipilih untuk dinonaktifkan secara default; **23 package** lainnya hanya opsional.
- **10 package** diproteksi agar tidak ikut dinonaktifkan melalui modul.
- Menonaktifkan dengan `pm disable-user --user 0` setelah boot selesai.
- Menyimpan daftar package yang benar-benar dinonaktifkan oleh modul.
- Tombol **Action** di KernelSU Next untuk **restore / apply** bergantian.
- Mencoba memulihkan package saat modul di-uninstall.
- Skrip berjalan tanpa mengubah APK bawaan secara fisik.

## Instalasi

1. Backup data penting dan siapkan cara pemulihan bila mengalami masalah.
2. Unduh berkas **`TECNO_Spark_30C_KL5n_KernelSU_Debloat_v1.0.zip`** dari repository ini.
3. Buka **KernelSU Next → Modules → Install from storage**, lalu pilih ZIP tersebut.
4. Reboot dan tunggu Android selesai menyala.
5. Uji fungsi telepon, SMS, Wi-Fi, data, Bluetooth, sidik jari, kamera, notifikasi, launcher, dan fitur HiOS yang kamu pakai.

## Pemulihan

Di KernelSU Next, buka modul lalu tekan **Action** untuk memulihkan package yang dicatat modul. Tekan **Action** lagi untuk menerapkan debloat ulang.

Status aplikasi yang sudah di-disable melalui PackageManager bisa bertahan walaupun toggle modul dimatikan. **Restore lewat Action terlebih dahulu sebelum menonaktifkan atau menghapus modul.** Saat uninstall, skrip `uninstall.sh` juga mencoba pemulihan otomatis, tetapi tidak dijamin jika perangkat bermasalah atau skrip gagal berjalan.

Pemulihan manual dari Termux dengan akses root:

```sh
su -c 'pm enable --user 0 com.debug.loggerui'
```

Ganti nama package sesuai daftar yang ingin dipulihkan pada `disabled-by-module.txt`.

## Pengaturan package

Setelah modul terpasang, edit sebagai root:

```text
/data/adb/modules/tecno_kl5n_selective_debloat/packages/selected.txt
```

Hilangkan `#` pada package opsional jika benar-benar ingin menonaktifkannya. Daftar yang dilindungi berada di `packages/protected.txt`. Package yang tidak ada pada `packages/original-43.txt` ditolak.

## File modul

- `module.prop`: metadata modul.
- `customize.sh`: pemeriksaan KL5n sewaktu pemasangan.
- `service.sh`: penerapan setelah boot.
- `action.sh`: pemulihan/penerapan lewat tombol Action.
- `uninstall.sh`: mencoba pemulihan saat uninstall.
- `lib/common.sh`: fungsi bantu dan pencatatan.
- `packages/selected.txt`: pilihan default dan opsional.
- `packages/protected.txt`: daftar package yang dilindungi.
- `packages/original-43.txt`: daftar sumber tanpa duplikat.
- `README-ID.txt`: panduan ringkas dalam ZIP.

## Kompatibilitas

- **Perangkat:** TECNO Spark 30C KL5n.
- **Root:** KernelSU / KernelSU Next.
- **Android:** disusun untuk Android 12 ke atas, tetapi belum diverifikasi pada seluruh rilis HiOS / firmware.

## Disclaimer

Modul ini dibuat untuk keperluan modifikasi perangkat milik sendiri. Menonaktifkan aplikasi sistem dapat mengakibatkan hilangnya fitur, gangguan pada layanan vendor, atau membutuhkan pemulihan manual. Selalu utamakan metode **disable / restore**, bukan penghapusan permanen.
