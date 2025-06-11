---
title: Fractional Knapsack🎒
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, FRACTIONAL KNAPSACK🎒]
tags: [algoritma, fractional-knapsack, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---
# Mengisi Ransel Penuh Nilai: Memahami Fractional Knapsack Problem

Halo para petualang dan penjelajah dunia optimasi! Pernahkah Anda membayangkan sebuah ransel ajaib yang bisa membawa harta karun sebanyak mungkin, bahkan jika itu berarti Anda harus membagi permata menjadi kepingan kecil? Atau mungkin Anda seorang manajer logistik yang ingin memaksimalkan muatan truk dengan barang-barang yang bisa dipecah?

Jika ya, maka Anda sedang berada di jalur yang tepat! Dalam dunia algoritma, ada sebuah tantangan menarik yang dikenal sebagai **Fractional Knapsack Problem**. Ini bukan sekadar masalah teoritis di buku, melainkan sebuah konsep yang memiliki aplikasi luas dalam kehidupan nyata, mulai dari alokasi sumber daya hingga perencanaan produksi. Mari kita buka ransel pengetahuan kita dan selami lebih dalam bagaimana kita bisa mengisi ransel impian kita dengan nilai paling maksimal!

## Definisi Fractional Knapsack

Fractional Knapsack adalah varian dari masalah knapsack (ransel) dalam algoritma, di mana kita boleh mengambil sebagian dari suatu item (misalnya setengah, seperempat, dan seterusnya) untuk memaksimalkan nilai total barang dalam kapasitas ransel tertentu. Nama "fractional" berasal dari kata pecahan atau bagian, yang berarti Anda diizinkan mengambil sebagian dari barang, tidak harus utuh. Sementara itu, "knapsack" berarti ransel atau tas, yang merupakan metafora untuk kapasitas penyimpanan yang terbatas.

## Permasalahan

Pada dasarnya, Knapsack Problem adalah sebuah masalah yang muncul ketika kita memiliki sebuah tas yang memiliki kapasitas terbatas, dan kita ingin memilih barang-barang yang dapat dimasukkan ke dalam tas tersebut untuk memaksimalkan nilai total barang yang kita bawa.

## Jenis Knapsack Problem

Ada dua jenis utama dari Knapsack Problem:

1.  **0/1 Knapsack Problem**: Pada jenis ini, kita hanya bisa memilih barang utuh, tidak bisa mengambil sebagian (fractional).
2.  **Fractional Knapsack Problem**: Berbeda dengan 0/1 Knapsack, pada jenis ini kita bisa mengambil sebagian dari barang, tidak hanya barang utuh.

## Penjelasan Konsep Fractional Knapsack

Bayangkan Anda memiliki sebuah tas dengan kapasitas terbatas, dan ada beberapa barang yang masing-masing memiliki berat dan nilai tertentu. Tujuan kita adalah untuk memaksimalkan nilai barang yang kita bawa, namun dengan kapasitas tas yang terbatas. Anda perlu mengisi tas dengan barang yang memberikan nilai tertinggi, tanpa melebihi kapasitas.

Karena ini adalah *fractional* knapsack, Anda diperbolehkan memotong barang. Misalnya, jika Anda hanya bisa membawa 3 kg dari emas seberat 5 kg, tidak masalah. Yang penting, nilainya akan ikut proporsional sesuai dengan bagian yang Anda ambil.

## Latihan Soal

Sebuah tas memiliki kapasitas maksimum 50 kg. Tersedia 3 barang berikut:

| Barang | Berat (kg) | Nilai (Rp) |
| :----- | :--------- | :--------- |
| A      | 10         | 60         |
| B      | 20         | 100        |
| C      | 30         | 120        |

Anda boleh mengambil barang sebagian atau seluruhnya. Tentukan nilai maksimum yang dapat dibawa oleh tas dengan strategi Fractional Knapsack!

### Penyelesaian

**Langkah 1: Hitung nilai per berat (value/weight) untuk masing-masing barang.**

* Barang A: 60 / 10 = 6.0
* Barang B: 100 / 20 = 5.0
* Barang C: 120 / 30 = 4.0

**Langkah 2: Urutkan barang berdasarkan rasio nilai per berat dari tertinggi ke terendah.**

* A (rasio 6.0)
* B (rasio 5.0)
* C (rasio 4.0)

Kapasitas awal tas = 50 kg.

1.  **Ambil barang A** (10 kg, nilai 60).
    * Masih muat, ambil seluruhnya.
    * Sisa kapasitas = 50 kg - 10 kg = 40 kg.
    * Total nilai = 60.

2.  **Ambil barang B** (20 kg, nilai 100).
    * Masih muat, ambil seluruhnya.
    * Sisa kapasitas = 40 kg - 20 kg = 20 kg.
    * Total nilai = 60 + 100 = 160.

3.  **Ambil barang C** (30 kg, nilai 120).
    * Tidak muat seluruhnya, ambil sebagian sebanyak 20 kg dari 30 kg.
    * Proporsi yang diambil = 20 kg / 30 kg = 2/3.
    * Nilai yang diambil = (2/3) * 120 = 80.
    * Sisa kapasitas = 0 kg.

Total nilai = 160 + 80 = **240**.

## Implementasi C++

Berikut adalah contoh implementasi Fractional Knapsack Problem dalam C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // Untuk std::sort

using namespace std;

// Struktur data untuk merepresentasikan sebuah barang
struct Barang {
    int berat; // berat barang
    int nilai; // nilai barang

    // Fungsi untuk menghitung rasio nilai terhadap berat
    double nilaiPerBerat() const {
        return (double)nilai / berat;
    }
};

// Fungsi pembanding untuk mengurutkan barang berdasarkan rasio nilai per berat (dari yang tertinggi)
bool bandingkan(Barang a, Barang b) {
    return a.nilaiPerBerat() > b.nilaiPerBerat();
}

// Fungsi utama untuk menyelesaikan masalah Knapsack Fraksional
double knapsackFraksional(int kapasitas, vector<Barang>& daftarBarang) {
    // Urutkan daftar barang berdasarkan rasio nilai per berat secara menurun
    sort(daftarBarang.begin(), daftarBarang.end(), bandingkan);

    double totalNilai = 0.0; // Menyimpan total nilai barang yang diambil

    // Iterasi setiap barang dalam daftar
    for (const auto& barang : daftarBarang) {
        if (kapasitas == 0) break; // Jika kapasitas tas sudah penuh, berhenti

        if (barang.berat <= kapasitas) {
            // Jika berat barang masih muat di tas, ambil seluruhnya
            kapasitas -= barang.berat;
            totalNilai += barang.nilai;
        } else {
            // Jika barang terlalu berat, ambil sebagian sesuai sisa kapasitas
            totalNilai += barang.nilaiPerBerat() * kapasitas;
            kapasitas = 0; // Kapasitas tas habis
        }
    }
    return totalNilai; // Kembalikan total nilai maksimum yang bisa dibawa
}

int main() {
    int kapasitasTas = 50; // Kapasitas maksimum tas

    // Daftar barang yang tersedia (berat, nilai)
    vector<Barang> daftarBarang = {
        {10, 60}, // Barang A
        {20, 100}, // Barang B
        {30, 120} // Barang C
    };

    // Hitung nilai maksimum yang bisa dibawa dengan tas
    double nilaiMaksimum = knapsackFraksional(kapasitasTas, daftarBarang);

    // Tampilkan hasil
    cout << "Nilai maksimum yang bisa dibawa: " << nilaiMaksimum << endl;

    return 0;
}
```

**Output dari kode di atas akan menampilkan:**

```
Nilai maksimum yang bisa dibawa: 240
```

## Algoritma Greedy dalam Fractional Knapsack

Fractional Knapsack Problem dapat diselesaikan secara optimal menggunakan algoritma greedy dengan strategi berikut:

### Strategi Greedy
1. **Hitung rasio nilai per berat** untuk setiap barang
2. **Urutkan barang** berdasarkan rasio tersebut secara menurun
3. **Pilih barang** dengan rasio tertinggi terlebih dahulu
4. **Ambil barang secara utuh** jika masih muat dalam kapasitas
5. **Ambil sebagian** jika barang tidak muat secara utuh

### Mengapa Greedy Optimal untuk Fractional Knapsack?

Algoritma greedy memberikan solusi optimal untuk Fractional Knapsack karena:
- Kita selalu memilih barang dengan rasio nilai per berat tertinggi
- Jika suatu barang tidak muat utuh, kita bisa mengambil sebagiannya
- Tidak ada kerugian dalam memilih barang dengan rasio tertinggi karena kita bisa "memotong" barang

### Kompleksitas Algoritma

- **Kompleksitas Waktu**: O(n log n) - didominasi oleh proses pengurutan
- **Kompleksitas Ruang**: O(1) - jika tidak menghitung ruang input

## Perbedaan dengan 0/1 Knapsack

| Aspek | Fractional Knapsack | 0/1 Knapsack |
|-------|-------------------|---------------|
| **Pengambilan Barang** | Bisa sebagian | Harus utuh |
| **Algoritma** | Greedy (optimal) | Dynamic Programming |
| **Kompleksitas** | O(n log n) | O(nW) |
| **Kesulitan** | Mudah | Lebih sulit |

## Aplikasi dalam Dunia Nyata

Fractional Knapsack Problem memiliki berbagai aplikasi praktis:

1. **Alokasi Sumber Daya**
   - Pembagian anggaran untuk proyek-proyek berbeda
   - Alokasi waktu untuk berbagai aktivitas

2. **Logistik dan Transportasi**
   - Memuat kargo dalam container dengan memaksimalkan nilai
   - Pengiriman barang dengan batasan berat kendaraan

3. **Investasi dan Portfolio**
   - Pembagian investasi dalam berbagai aset
   - Optimasi portfolio dengan batasan modal

4. **Produksi dan Manufacturing**
   - Alokasi bahan baku untuk berbagai produk
   - Optimasi penggunaan mesin produksi

## Kesimpulan

1. Dalam Fractional Knapsack, kita dapat memilih sebagian barang.
2. Solusinya menggunakan algoritma greedy dengan memilih barang berdasarkan rasio nilai terhadap berat tertinggi.
3. Langkah-langkah penyelesaiannya meliputi: menghitung rasio nilai per berat, mengurutkan barang berdasarkan rasio tersebut, dan memasukkan barang ke tas sesuai kapasitas.
4. Solusi ini memiliki kompleksitas waktu O(n log n), karena dominasi waktu terletak pada proses pengurutan barang.
5. Fractional Knapsack berbeda dengan 0/1 Knapsack dalam hal fleksibilitas pengambilan barang dan metode penyelesaiannya.

Fractional Knapsack Problem mengajarkan kita pentingnya strategi greedy dalam optimasi dan bagaimana fleksibilitas dalam pengambilan keputusan (bisa mengambil sebagian) dapat menyederhanakan kompleksitas masalah.