---
title: Subset Sum Problem🕵️‍♂️
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, MATERI 5]
tags: [algoritma, subset-sum-problem, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---
# Mencari Harta Karun Tersembunyi: Mengungkap Subset Sum Problem 

Halo, para detektif angka dan pemburu pola! Pernahkah Anda merasa seperti sedang mencari jarum di tumpukan jerami, mencoba menemukan kombinasi yang tepat dari sekumpulan angka untuk mencapai suatu target? Atau mungkin Anda adalah seorang *developer* yang sedang mengoptimalkan *resource allocation* dengan batasan anggaran?

Jika tantangan semacam itu membangkitkan semangat Anda, maka Anda telah datang ke tempat yang tepat! Mari kita selami salah satu masalah paling menarik dan menantang dalam dunia ilmu komputer: **Subset Sum Problem**. Ini bukan sekadar teka-teki matematika, melainkan sebuah masalah fundamental yang memiliki implikasi besar dalam berbagai bidang, dari kriptografi hingga riset operasi. Bersiaplah untuk melacak setiap kemungkinan kombinasi dan menemukan "subset emas" yang kita cari!

## Apa Itu Subset Sum Problem?

Subset Sum Problem adalah masalah klasik dalam ilmu komputer yang berfokus pada pencarian. Diberikan sebuah himpunan bilangan bulat tidak kosong dan sebuah angka target (misalnya $m$), masalah ini meminta kita untuk mencari apakah ada **subhimpunan** dari himpunan tersebut yang jumlah elemen-elemennya sama dengan target $m$.

### Mengapa Masalah Ini Penting?

Dalam dunia *computer science*, masalah sum of subset merupakan masalah yang penting dalam teori kompleksitas dan kriptografi.

* **NP-Complete**: Masalah ini dikenal sebagai NP-Complete (Non-Deterministic Polynomial Complete), atau biasa disebut NPC. Artinya, ini adalah jenis masalah yang sulit dicari solusinya secara efisien (waktu polinomial), tetapi jika kita sudah tahu jawabannya, kita bisa mengeceknya dengan cepat.
* **"Lengkap" di Kelas NP**: Subset Sum disebut "lengkap" di kelas NP karena semua masalah lain di NP bisa diubah menjadi bentuk Subset Sum dalam waktu yang wajar. Ini berarti, jika suatu hari ada cara cepat (waktu polinomial) untuk menyelesaikan Subset Sum, maka semua masalah NP juga bisa diselesaikan dengan cepat. Inilah yang disebut dengan masalah "$P = NP$".

## Metode Penyelesaian Subset Sum Problem

Ada dua pendekatan utama untuk menyelesaikan Subset Sum Problem:

1.  **Backtracking** (untuk menemukan semua subset)
2.  **Dynamic Programming** (untuk menentukan keberadaan subset dan terkadang merekonstruksinya)

## 1. Pendekatan Backtracking

Pendekatan *backtracking* digunakan untuk menemukan semua subset yang jumlahnya sama dengan target yang ditentukan.

### Contoh Soal Backtracking

Diberikan himpunan $S = \{1, 2, 5, 6, 8\}$ dan target $T = 9$.

### Solusi dengan Backtracking

Mari kita visualisasikan prosesnya. Kita akan membangun pohon rekursi, mencoba setiap elemen.

**Proses Langkah demi Langkah:**

* Mulai dengan subset kosong `[]` dan `sum = 0`.
* **Iterasi 1 (elemen 1):**
    * Ambil 1: `[1]`, `sum = 1`. Lanjutkan.
        * **Iterasi 2 (elemen 2):**
            * Ambil 2: `[1, 2]`, `sum = 3`. Lanjutkan.
                * **Iterasi 3 (elemen 5):**
                    * Ambil 5: `[1, 2, 5]`, `sum = 8`. Lanjutkan.
                        * **Iterasi 4 (elemen 6):**
                            * Ambil 6: `[1, 2, 5, 6]`, `sum = 14`. `$14 > 9$`, jalur ini tidak valid. Mundur.
                        * Tidak ambil 6: `[1, 2, 5]`, `sum = 8`. Lanjutkan.
                            * **Iterasi 4 (elemen 8):**
                                * Ambil 8: `[1, 2, 5, 8]`, `sum = 16`. `$16 > 9$`, jalur ini tidak valid. Mundur.
                                * Tidak ambil 8: `[1, 2, 5]`, `sum = 8`. Mundur.
                    * Tidak ambil 5: `[1, 2]`, `sum = 3`. Lanjutkan.
                        * **Iterasi 3 (elemen 6):**
                            * Ambil 6: `[1, 2, 6]`, `sum = 9`. **SOLUSI DITEMUKAN!** (`[1, 2, 6]`)
                        * Tidak ambil 6: `[1, 2]`, `sum = 3`. Lanjutkan.
                            * **Iterasi 3 (elemen 8):**
                                * Ambil 8: `[1, 2, 8]`, `sum = 11`. `$11 > 9$`, jalur ini tidak valid. Mundur.
                                * Tidak ambil 8: `[1, 2]`, `sum = 3`. Mundur.
            * Tidak ambil 2: `[1]`, `sum = 1`. Lanjutkan.
                * ... (proses serupa untuk elemen 5, 6, 8)
    * Tidak ambil 1: `[]`, `sum = 0`. Lanjutkan.
        * **Iterasi 2 (elemen 2):**
            * Ambil 2: `[2]`, `sum = 2`. Lanjutkan.
                * **Iterasi 3 (elemen 5):**
                    * Ambil 5: `[2, 5]`, `sum = 7`. Lanjutkan.
                        * **Iterasi 4 (elemen 6):**
                            * Ambil 6: `[2, 5, 6]`, `sum = 13`. `$13 > 9$`, jalur ini tidak valid. Mundur.
                        * Tidak ambil 6: `[2, 5]`, `sum = 7`. Lanjutkan.
                            * **Iterasi 4 (elemen 8):**
                                * Ambil 8: `[2, 5, 8]`, `sum = 15`. `$15 > 9$`, jalur ini tidak valid. Mundur.
                                * Tidak ambil 8: `[2, 5]`, `sum = 7`. Mundur.
                    * Tidak ambil 5: `[2]`, `sum = 2`. Lanjutkan.
                        * **Iterasi 3 (elemen 6):**
                            * Ambil 6: `[2, 6]`, `sum = 8`. Lanjutkan.
                                * **Iterasi 4 (elemen 8):**
                                    * Ambil 8: `[2, 6, 8]`, `sum = 16`. `$16 > 9$`, jalur ini tidak valid. Mundur.
                                    * Tidak ambil 8: `[2, 6]`, `sum = 8`. Mundur.
                                    * (Tidak ada solusi dari jalur ini)
                        * Tidak ambil 6: `[2]`, `sum = 2`. Lanjutkan.
                            * **Iterasi 3 (elemen 8):**
                                * Ambil 8: `[2, 8]`, `sum = 10`. `$10 > 9$`, jalur ini tidak valid. Mundur.
                                * Tidak ambil 8: `[2]`, `sum = 2`. Mundur.
            * Tidak ambil 2: `[]`, `sum = 0`. Lanjutkan.
                * **Iterasi 2 (elemen 5):**
                    * Ambil 5: `[5]`, `sum = 5`. Lanjutkan.
                        * **Iterasi 3 (elemen 6):**
                            * Ambil 6: `[5, 6]`, `sum = 11`. `$11 > 9$`, jalur ini tidak valid. Mundur.
                        * Tidak ambil 6: `[5]`, `sum = 5`. Lanjutkan.
                            * **Iterasi 3 (elemen 8):**
                                * Ambil 8: `[5, 8]`, `sum = 13`. `$13 > 9$`, jalur ini tidak valid. Mundur.
                                * Tidak ambil 8: `[5]`, `sum = 5`. Mundur.
    * ... (Proses akan terus berlanjut untuk mencari semua kombinasi)

**Solusi yang Ditemukan:**

Dari himpunan $S = \{1, 2, 5, 6, 8\}$ dan target $T = 9$, solusi validnya adalah:
* `[1, 8]`
* `[1, 2, 6]`

### Implementasi Backtracking (C++)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Fungsi rekursif untuk mencari subset sum
void findSubsets(std::vector<int>& arr, int targetSum, std::vector<int>& currentSubset, int currentIndex, int currentSum, std::vector<std::vector<int>>& result) {
    // Base case 1: Jika jumlah saat ini sama dengan target
    if (currentSum == targetSum) {
        result.push_back(currentSubset); // Tambahkan subset ke hasil
        return;
    }

    // Base case 2: Jika jumlah saat ini melebihi target ATAU sudah memeriksa semua elemen
    if (currentSum > targetSum || currentIndex == arr.size()) {
        return;
    }

    // Pilihan 1: Masukkan elemen saat ini ke subset
    currentSubset.push_back(arr[currentIndex]);
    findSubsets(arr, targetSum, currentSubset, currentIndex + 1, currentSum + arr[currentIndex], result);
    currentSubset.pop_back(); // Backtrack: Hapus elemen dari subset

    // Pilihan 2: Jangan masukkan elemen saat ini ke subset (lanjut ke elemen berikutnya)
    findSubsets(arr, targetSum, currentSubset, currentIndex + 1, currentSum, result);
}

int main() {
    std::vector<int> arr = {1, 2, 5, 6, 8}; // Himpunan angka
    int targetSum = 9; // Target jumlah

    std::vector<std::vector<int>> result; // Menyimpan semua subset yang valid
    std::vector<int> currentSubset; // Subset sementara

    findSubsets(arr, targetSum, currentSubset, 0, 0, result);

    // Cetak hasil
    if (result.empty()) {
        std::cout << "Tidak ada subset yang jumlahnya sama dengan " << targetSum << std::endl;
    } else {
        std::cout << "Subset yang jumlahnya sama dengan " << targetSum << ":" << std::endl;
        for (const auto& subset : result) {
            std::cout << "[ ";
            for (int num : subset) {
                std::cout << num << " ";
            }
            std::cout << "]" << std::endl;
        }
    }

    return 0;
}
```

### Penjelasan Kode Backtracking

* **Fungsi `findSubsets`**: Ini adalah fungsi rekursif utama yang mengimplementasikan *backtracking*.
    * **Parameter**:
        * `arr`: Himpunan angka input.
        * `targetSum`: Target jumlah yang dicari.
        * `currentSubset`: Vektor yang menyimpan subset yang sedang dibangun.
        * `currentIndex`: Indeks elemen `arr` yang sedang dipertimbangkan.
        * `currentSum`: Jumlah dari elemen-elemen di `currentSubset`.
        * `result`: Vektor dari vektor yang akan menyimpan semua subset solusi.
    * **Base Case**:
        * Jika `currentSum == targetSum`, maka `currentSubset` adalah solusi, tambahkan ke `result`.
        * Jika `currentSum > targetSum` atau `currentIndex` mencapai akhir `arr`, berarti jalur ini tidak valid, hentikan rekursi.
    * **Pilihan**: Untuk setiap `currentIndex`, ada dua pilihan:
        * **Ambil elemen**: Masukkan `arr[currentIndex]` ke `currentSubset`, lalu panggil `findSubsets` rekursif dengan `currentIndex + 1` dan `currentSum + arr[currentIndex]`. Setelah panggilan kembali, lakukan *backtrack* dengan `pop_back()` untuk menghapus elemen.
        * **Jangan ambil elemen**: Panggil `findSubsets` rekursif dengan `currentIndex + 1` dan `currentSum` yang sama.
* **`main`**: Menginisialisasi himpunan angka, target, dan memanggil `findSubsets` untuk memulai pencarian. Kemudian mencetak hasilnya.

**Kompleksitas Waktu untuk Backtracking**: $O(2^n)$ karena setiap elemen memiliki dua pilihan (diambil atau tidak diambil).

## 2. Pendekatan Dynamic Programming (DP)

Pendekatan *Dynamic Programming* biasanya digunakan untuk menentukan **apakah** ada subset yang jumlahnya sama dengan target, dan terkadang untuk merekonstruksi subset tersebut.

### Konsep DP untuk Subset Sum

* Kita akan membangun sebuah tabel boolean `dp` berukuran `(n + 1) x (T + 1)`.
* `dp[i][j]` akan bernilai `true` jika ada subset dari `{S[0], ..., S[i-1]}` (subset yang mempertimbangkan `i` elemen pertama dari himpunan asli) yang jumlahnya `j`.
* **Inisialisasi**:
    * `dp[i][0] = true` untuk semua `i` (subset kosong selalu bisa menghasilkan jumlah 0).
    * `dp[0][j] = false` untuk semua `j > 0` (tanpa elemen, tidak bisa menghasilkan jumlah > 0).
* **Relasi Rekursif**: Untuk setiap `dp[i][j]`:
    * `dp[i][j] = dp[i-1][j]` (tidak memasukkan elemen `S[i-1]` ke dalam subset).
    * Jika `j >= S[i-1]`, maka `dp[i][j] = dp[i][j] || dp[i-1][j - S[i-1]]` (memasukkan elemen `S[i-1]` ke dalam subset).

### Contoh Soal DP

Diberikan himpunan $S = \{3, 34, 4, 12, 5, 2\}$ dan target $T = 9$.

### Solusi dengan DP

Kita akan membuat tabel `dp[n+1][T+1]` atau `dp[7][10]`.

| dp[i][j] | 0     | 1     | 2     | 3     | 4     | 5     | 6     | 7     | 8     | 9     |
| :------- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| **{}** | True  | False | False | False | False | False | False | False | False | False |
| **{3}** | True  | False | False | True  | False | False | False | False | False | False |
| **{3,34}**| True  | False | False | True  | False | False | False | False | False | False |
| **{3,34,4}**| True  | False | False | True  | True  | False | False | True  | False | False |
| **{3,34,4,12}**| True  | False | False | True  | True  | False | False | True  | False | False |
| **{3,34,4,12,5}**| True  | False | False | True  | True  | True  | False | True  | True  | True  |
| **{3,34,4,12,5,2}**| True  | False | True  | True  | True  | True  | True  | True  | True  | True  |

Karena `dp[n][T]` atau `dp[6][9]` adalah `True`, maka ada subset yang jumlahnya 9.
Untuk merekonstruksi subset, kita bisa menelusuri kembali tabel `dp`.

### Implementasi Dynamic Programming (C++)

```cpp
#include <iostream>
#include <vector>
#include <numeric> // For std::accumulate

// Fungsi untuk menentukan apakah ada subset dengan jumlah target
bool isSubsetSum(const std::vector<int>& set, int n, int sum) {
    // Buat tabel dp[n+1][sum+1]
    std::vector<std::vector<bool>> dp(n + 1, std::vector<bool>(sum + 1));

    // Inisialisasi baris pertama (jumlah 0 selalu bisa dicapai dengan subset kosong)
    for (int i = 0; i <= n; i++) {
        dp[i][0] = true;
    }

    // Inisialisasi kolom pertama (jumlah > 0 tidak bisa dicapai dengan 0 elemen)
    for (int j = 1; j <= sum; j++) {
        dp[0][j] = false;
    }

    // Isi tabel dp
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {
            // Jika elemen saat ini lebih besar dari jumlah yang sedang dipertimbangkan,
            // maka elemen ini tidak bisa dimasukkan. Ambil nilai dari baris sebelumnya.
            if (set[i - 1] > j) {
                dp[i][j] = dp[i - 1][j];
            } else {
                // Elemen bisa dimasukkan atau tidak.
                // dp[i-1][j] : tidak memasukkan elemen set[i-1]
                // dp[i-1][j - set[i-1]] : memasukkan elemen set[i-1]
                dp[i][j] = dp[i - 1][j] || dp[i - 1][j - set[i - 1]];
            }
        }
    }

    return dp[n][sum]; // Mengembalikan apakah ada subset dengan jumlah target
}

// Fungsi untuk merekonstruksi dan mencetak subset (opsional, lebih kompleks)
void printSubset(const std::vector<int>& set, int n, int sum, const std::vector<std::vector<bool>>& dp) {
    if (!dp[n][sum]) {
        std::cout << "Tidak ada subset dengan jumlah " << sum << std::endl;
        return;
    }

    std::vector<int> subset;
    int currentSum = sum;
    int currentIndex = n;

    while (currentIndex > 0 && currentSum > 0) {
        // Jika jumlah bisa dicapai tanpa elemen saat ini
        if (dp[currentIndex - 1][currentSum]) {
            currentIndex--;
        }
        // Jika jumlah hanya bisa dicapai dengan elemen saat ini
        else if (dp[currentIndex - 1][currentSum - set[currentIndex - 1]]) {
            subset.push_back(set[currentIndex - 1]);
            currentSum -= set[currentIndex - 1];
            currentIndex--;
        }
    }
    std::reverse(subset.begin(), subset.end()); // Balik urutan agar sesuai aslinya

    std::cout << "Salah satu subset dengan jumlah " << sum << ": [ ";
    for (int num : subset) {
        std::cout << num << " ";
    }
    std::cout << "]" << std::endl;
}


int main() {
    std::vector<int> set = {3, 34, 4, 12, 5, 2};
    int sum = 9;
    int n = set.size();

    if (isSubsetSum(set, n, sum)) {
        std::cout << "Ada subset dengan jumlah " << sum << std::endl;
        // Jika ingin merekonstruksi subset, perlu tabel dp sebagai parameter
        // dan modifikasi isSubsetSum untuk mengembalikan tabel dp
        // (contoh printSubset tidak diimplementasikan secara penuh di sini untuk kesederhanaan)
    } else {
        std::cout << "Tidak ada subset dengan jumlah " << sum << std::endl;
    }

    // Contoh untuk mencetak salah satu subset (membutuhkan modifikasi isSubsetSum)
    // std::vector<std::vector<bool>> dp(n + 1, std::vector<bool>(sum + 1));
    // isSubsetSum(set, n, sum, dp); // Panggil fungsi yang mengisi dp
    // printSubset(set, n, sum, dp);

    return 0;
}
```

### Penjelasan Kode DP

* **Tabel `dp`**: Sebuah tabel `dp` berukuran `(n + 1) x (T + 1)` di mana `dp[i][j]` bernilai `true` jika ada subset dari `{S[0], ..., S[i-1]}` yang jumlahnya `j`.
* **Inisialisasi**:
    * `dp[i][0] = true`: Jumlah 0 selalu bisa dicapai dengan mengambil subset kosong.
    * `dp[0][j] = false`: Jika tidak ada elemen, tidak ada jumlah positif yang bisa dicapai.
* **`isSubsetSum`**:
    * Loop melalui setiap elemen (`i`) dan setiap kemungkinan jumlah (`j`).
    * Jika elemen saat ini (`set[i-1]`) lebih besar dari jumlah `j` yang sedang diperiksa, maka elemen ini tidak bisa digunakan untuk mencapai `j`. Jadi, `dp[i][j]` akan sama dengan `dp[i-1][j]` (solusi tanpa elemen ini).
    * Jika elemen saat ini kurang dari atau sama dengan `j`, ada dua kemungkinan:
        * Tidak menggunakan elemen ini: `dp[i-1][j]`
        * Menggunakan elemen ini: `dp[i-1][j - set[i-1]]` (kita butuh jumlah `j - set[i-1]` dari elemen sebelumnya).
        * `dp[i][j]` akan `true` jika salah satu dari kondisi ini `true`.
* **`printSubset`**: (Fungsi opsional dan lebih kompleks) Fungsi ini akan menelusuri kembali tabel `dp` dari `dp[n][sum]` untuk merekonstruksi salah satu subset yang valid.

**Kompleksitas Waktu untuk Dynamic Programming**: $O(n \cdot T)$ karena kita mengisi tabel `dp` dengan ukuran $n \times T$.
**Kompleksitas Ruang untuk Dynamic Programming**: $O(n \cdot T)$ untuk menyimpan tabel `dp`.

## Perbandingan Backtracking dan Dynamic Programming

| Fitur              | Backtracking                             | Dynamic Programming (DP)                  |
| :----------------- | :--------------------------------------- | :---------------------------------------- |
| **Tujuan Umum** | Menemukan *semua* kemungkinan subset.     | Menentukan *apakah* ada subset (solusi boolean). |
| **Kelebihan** | Menemukan semua solusi, lebih intuitif untuk masalah kecil. | Lebih efisien untuk menentukan keberadaan solusi, menghindari komputasi berulang. |
| **Kekurangan** | Sangat tidak efisien (eksponensial $O(2^n)$) untuk $N$ besar. | Membutuhkan ruang tabel yang signifikan ($O(n \cdot T)$), tidak selalu mudah merekonstruksi semua subset. |
| **Kompleksitas Waktu** | $O(2^n)$                                 | $O(n \cdot T)$                            |
| **Kompleksitas Ruang** | $O(n)$ (untuk rekursi stack)             | $O(n \cdot T)$                            |
| **Kapan Digunakan?** | Ketika $N$ kecil dan perlu semua solusi. | Ketika hanya perlu tahu keberadaan solusi, atau $N$ dan $T$ relatif besar. |

## Kesimpulan

Subset Sum Problem adalah masalah penting dalam ilmu komputer dengan implikasi besar di berbagai bidang. Meskipun merupakan masalah NP-Complete, ada dua pendekatan utama untuk menyelesaikannya:

1.  **Backtracking**: Cocok untuk menemukan semua solusi ketika himpunan input relatif kecil. Namun, kompleksitas waktunya eksponensial ($O(2^n)$).
2.  **Dynamic Programming**: Lebih efisien dalam menentukan keberadaan solusi, terutama untuk himpunan yang lebih besar dan target yang wajar. Memiliki kompleksitas waktu dan ruang $O(n \cdot T)$.

Pemilihan metode tergantung pada ukuran input dan apakah kita perlu menemukan semua solusi atau hanya keberadaan satu solusi. Memahami kedua pendekatan ini memberikan dasar yang kuat dalam memecahkan masalah optimasi dan pencarian yang kompleks.