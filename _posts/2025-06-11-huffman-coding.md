---
title: Huffman Coding🌳
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, MATERI 3]
tags: [algoritma, huffman-coding, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---
# Meretas Kompresi: Menguasai Huffman Coding 

Halo, para arsitek informasi dan peretas data! Pernahkah Anda bertanya-tanya bagaimana rahasia di balik file-file mungil yang kita unduh atau pesan singkat yang kita kirimkan? Bagaimana sebuah informasi yang tadinya "berat" bisa menjadi begitu "ringan" tanpa kehilangan satu bit pun?

Jika Anda penasaran, bersiaplah untuk menyelami dunia **Huffman Coding**! Ini bukan sekadar algoritma biasa, melainkan sebuah mahakarya kompresi data yang mengubah cara kita menyimpan dan mengirimkan informasi. Dari file ZIP yang sering kita gunakan hingga protokol transmisi data, Huffman Coding adalah pahlawan tanpa tanda jasa yang bekerja di balik layar. Mari kita bongkar kode rahasia ini dan pahami bagaimana ia menghemat ruang penyimpanan dan mempercepat transfer data dengan cerdik!

## Pengertian Huffman Coding

Huffman Coding adalah algoritma kompresi data *lossless* (tanpa kehilangan data) yang digunakan untuk mengurangi ukuran data. Ini dilakukan dengan mengganti setiap karakter atau simbol dengan representasi biner berdasarkan frekuensi kemunculannya.

Algoritma ini ditemukan oleh David A. Huffman pada tahun 1952 dan masih relevan hingga kini, digunakan dalam berbagai sistem kompresi seperti file ZIP, format gambar, hingga protokol transmisi data.

## Tujuan Huffman Coding

Tujuan utama dari Huffman Coding adalah:
* Mengompres data secara efisien tanpa kehilangan informasi (lossless).
* Memberikan kode biner yang lebih pendek pada simbol yang sering muncul.
* Memberikan kode biner yang lebih panjang pada simbol yang jarang muncul.

## Bagaimana Huffman Coding Bekerja?

Mari kita lihat contoh string "BCAADDDCCACACAC" untuk memahami cara kerja Huffman Coding.

1. **Hitung frekuensi setiap karakter dalam string.**
    * Setiap karakter menempati 8 bit.
    * Total ada 15 karakter dalam string.
    * Tanpa encoding, total 8 * 15 = 120 bit diperlukan untuk mengirim string ini.
    * Dengan Huffman Coding, kita bisa memampatkan string ke ukuran yang lebih kecil.

2. **Buat Pohon Huffman.**
    * Urutkan karakter dalam urutan frekuensi yang meningkat.
    * Jadikan setiap karakter unik sebagai simpul daun.
    * Buat simpul kosong `z`.
    * Tetapkan frekuensi minimum ke anak kiri `z` dan frekuensi minimum kedua ke anak kanan `z`.
    * Tetapkan nilai `z` sebagai jumlah dari dua frekuensi minimum di atas.
    * Ambil dua frekuensi terkecil dari antrian prioritas Q, jumlahkan, lalu tambahkan kembali angka tersebut ke dalam Q sebagai *internal node*.
    * Masukkan simpul `z` ke dalam pohon.
    * Ulangi langkah-langkah ini sampai semua karakter terproses.
    * Untuk setiap simpul non-daun, tetapkan 0 ke tepi kiri dan 1 ke tepi kanan.

3. **Buat tabel kode dari diagram pohon.**

    | Character | Frequency | Code | Size |
    | :-------- | :-------- | :--- | :--- |
    | A         | 5         | 11   | $5 \times 2 = 10$ |
    | B         | 1         | 100  | $1 \times 3 = 3$  |
    | C         | 6         | 0    | $6 \times 1 = 6$  |
    | D         | 3         | 101  | $3 \times 3 = 9$  |
    | Total     | 15        |      | 28 bits           |

Tanpa encoding, total ukuran string ini adalah 120 bit. Setelah di-encoding, hanya 28 bit saja. Untuk ukuran totalnya (karakter + frekuensi + encoded) adalah 32 bit (untuk karakter) + 15 bit (untuk frekuensi) + 28 bit (untuk encoded) = 75 bit.

## Latihan

Mari kita coba dengan kata "sisfo".

Berikut adalah tabel frekuensi dan kode biner yang dihasilkan:

| Character | Frequency | Code | Size |
| :-------- | :-------- | :--- | :--- |
| S         | 2         | 0    | $2 \times 1 = 2$  |
| i         | 1         | 110  | $1 \times 3 = 3$  |
| f         | 1         | 111  | $1 \times 3 = 3$  |
| o         | 1         | 10   | $1 \times 2 = 2$  |

Setelah dihitung dengan Huffman Coding, total string setelah encoding adalah 10 bit. Total keseluruhan tabel adalah 32 (bit) + 5 (frekuensi) + 10 (encoding) = 42 bit.

## Hasil Implementasi

Berikut adalah contoh hasil inputan dari implementasi Huffman Coding:

```
Masukkan teks yang akan di-encode: sisfo
Kode Huffman:
i:10
s:11
f:01
o:00
Teks ter-encode (bit stream): 1110110100
Teks setelah decode: sisfo
Ukuran asli: 40 bit
Ukuran setelah kompresi: 10 bit
Ruang yang tersimpan: 75.0000%
```

Output ini menunjukkan bahwa Huffman Coding berhasil mengkompresi teks "sisfo" dari 40 bit menjadi hanya 10 bit, menghemat 75% ruang.
