
---
title: Activity Selection Problem
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, MATERI 1]
tags: [algoritma, activity-selection-problem, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---

{% raw %}

# Desain dan Analisis Algoritma: Activity Selection Problem

## Pengantar

Dalam mata kuliah **Desain dan Analisis Algoritma (DAA)**, kita mempelajari berbagai teknik pemecahan masalah yang efisien dan terstruktur. Salah satu pendekatan yang sering digunakan adalah **Greedy Algorithm**, yang sangat cocok diterapkan untuk masalah penjadwalan, salah satunya adalah **Activity Selection Problem (ASP)**.

---

## Apa Itu Activity Selection Problem (ASP)?

**Activity Selection Problem (ASP)** adalah masalah klasik dalam ilmu komputer yang bertujuan untuk memilih serangkaian aktivitas yang dapat dilakukan dalam satu periode waktu, dengan batasan bahwa aktivitas-aktivitas tersebut **tidak boleh saling tumpang tindih**.

ASP sering muncul dalam kehidupan nyata, contohnya:
- Penjadwalan ruangan
- Wawancara kerja
- Pengelolaan sumber daya (misalnya jadwal mesin produksi)

### Batasan Masalah:
1. **Tidak boleh ada tumpang tindih aktivitas.**  
   Aktivitas yang dipilih harus memiliki waktu mulai ≥ waktu selesai aktivitas sebelumnya.
2. **Hanya satu aktivitas dalam satu waktu.**  
   Kita tidak bisa melakukan lebih dari satu aktivitas yang berlangsung bersamaan.

---

## Apa Itu Greedy Algorithm?

**Greedy Algorithm** adalah pendekatan penyelesaian masalah dengan cara mengambil keputusan **terbaik secara lokal** di setiap langkah, **dengan harapan** solusi lokal ini akan membentuk solusi global yang optimal.

### Kenapa ASP Cocok Diselesaikan dengan Greedy?
- **Memiliki sifat optimalitas lokal.**  
  Memilih aktivitas yang selesai lebih cepat memberi ruang untuk lebih banyak aktivitas lainnya.
- **Solusi optimal dibentuk dari keputusan lokal.**  
  Dengan memilih langkah terbaik di tiap tahap, kita dapat membangun solusi akhir yang efisien.

---

## Strategi Penyelesaian ASP dengan Greedy

### Langkah-Langkah:

1. **Urutkan aktivitas berdasarkan waktu selesai.**
2. **Pilih aktivitas pertama** (yang selesai paling cepat).
3. **Pilih aktivitas berikutnya** jika waktu mulai ≥ waktu selesai aktivitas sebelumnya.
4. **Ulangi** langkah ke-3 hingga semua aktivitas diperiksa.

---

## Contoh Soal

Misalnya kita memiliki daftar aktivitas berikut:

```
| Aktivitas | Start | Finish |
|-----------|-------|--------|
| A         | 1     | 4      |
| B         | 3     | 5      |
| C         | 0     | 6      |
| D         | 5     | 7      |
| E         | 8     | 9      |
| F         | 5     | 9      |
```

### Penyelesaian:

- **Langkah 1**: Urutkan berdasarkan waktu selesai:
  ```
  A (1,4), B (3,5), D (5,7), E (8,9), F (5,9), C (0,6)
  ```

- **Langkah 2**: Pilih A `(1, 4)`

- **Langkah 3**: Aktivitas D dimulai pada 5 ≥ 4 → pilih D  
  Aktivitas E dimulai pada 8 ≥ 7 → pilih E

- **Solusi Akhir**: A, D, E  
  **Jumlah maksimal aktivitas: 3**

---

## Latihan Soal

Coba kamu selesaikan soal berikut:

```
| Aktivitas | Start | Finish |
|-----------|-------|--------|
| A         | 2     | 3      |
| B         | 1     | 4      |
| C         | 3     | 5      |
| D         | 0     | 6      |
| E         | 5     | 7      |
| F         | 8     | 9      |
```

Berapa aktivitas maksimal yang bisa kamu pilih tanpa tumpang tindih?

---

## Implementasi C++ (Ringkas)

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

struct Activity {
    int start, finish;
};

// Fungsi pembanding berdasarkan waktu selesai
bool compare(Activity a, Activity b) {
    return a.finish < b.finish;
}

void activitySelection(Activity arr[], int n) {
    sort(arr, arr + n, compare);

    cout << "Aktivitas yang dipilih:\n";
    int i = 0;
    cout << "(" << arr[i].start << ", " << arr[i].finish << ")\n";

    for (int j = 1; j < n; j++) {
        if (arr[j].start >= arr[i].finish) {
            cout << "(" << arr[j].start << ", " << arr[j].finish << ")\n";
            i = j;
        }
    }
}

int main() {
    Activity arr[] = {{1, 4}, {3, 5}, {0, 6}, {5, 7}, {8, 9}, {5, 9}};
    int n = sizeof(arr)/sizeof(arr[0]);
    activitySelection(arr, n);
    return 0;
}
```

### Output:
```
Aktivitas yang dipilih:
(1, 4)
(5, 7)
(8, 9)
```

---

## Kesimpulan

**Activity Selection Problem (ASP)** merupakan salah satu contoh masalah optimasi yang dapat diselesaikan secara efisien menggunakan **Greedy Algorithm**. Dengan memilih aktivitas yang selesai paling cepat dan tidak bertabrakan, kita dapat memaksimalkan jumlah aktivitas yang bisa dilakukan. Pendekatan ini sangat cocok untuk berbagai aplikasi penjadwalan di dunia nyata karena:
- Logikanya sederhana
- Kompleksitas waktunya efisien
- Implementasinya relatif mudah

---

## Pertanyaan Diskusi

> “Cukup pertanyaanmu saja yang diutarakan, perasaanmu jangan.” 😄

---

{% endraw %}
