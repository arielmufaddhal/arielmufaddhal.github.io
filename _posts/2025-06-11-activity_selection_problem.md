---
title: Activity Selection Problem🗓️
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, MATERI 1]
tags: [algoritma, activity-selection-problem, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---
# Memaksimalkan Waktu: Menjelajahi Activity Selection Problem

Halo, para penjelajah waktu! Pernahkah Anda merasa waktu adalah sumber daya yang paling berharga, dan Anda ingin memanfaatkannya sebaik mungkin? Atau mungkin Anda adalah seorang *event organizer* yang pusing tujuh keliling mengatur jadwal agar tidak ada acara yang bentrok? Jika ya, maka Anda telah datang ke tempat yang tepat!

Dalam era digital yang serba cepat ini, kemampuan untuk mengelola waktu dan sumber daya secara efisien adalah kunci. Di sinilah **Activity Selection Problem (ASP)** muncul sebagai pahlawan tak terduga. Ini bukan hanya sekadar teori abstrak di bangku kuliah, melainkan sebuah masalah klasik dalam ilmu komputer yang memiliki aplikasi nyata di berbagai bidang. Mari kita selami lebih dalam dunia ASP dan bagaimana kita bisa menaklukkan tantangan penjadwalan dengan cerdik!

## Apa Itu Activity Selection Problem (ASP)?

Activity Selection Problem adalah sebuah masalah klasik dalam ilmu komputer yang berfokus pada pemilihan serangkaian aktivitas yang dapat dilakukan dalam satu periode waktu. Kuncinya adalah memastikan bahwa aktivitas-aktivitas yang dipilih tersebut **tidak boleh tumpang tindih**.

### Mengapa Masalah Ini Penting?

Pentingnya ASP terletak pada relevansinya dengan berbagai situasi di dunia nyata, seperti:
* **Jadwal ruangan**: Memastikan tidak ada dua kelas atau rapat yang menggunakan ruangan yang sama pada waktu yang bersamaan.
* **Wawancara kerja**: Mengatur jadwal wawancara untuk banyak kandidat dengan batasan waktu yang terbatas.
* **Pengelolaan sumber daya**: Mengoptimalkan penggunaan mesin atau peralatan agar bekerja secara berkelanjutan tanpa konflik jadwal.

### Batasan Masalah (Constraints)

Untuk menyelesaikan ASP, ada dua batasan utama yang harus dipatuhi:
* **Tidak boleh ada tumpang tindih aktivitas**: Aktivitas yang dipilih harus memiliki waktu mulai yang lebih besar atau sama dengan waktu selesai dari aktivitas yang dipilih sebelumnya.
* **Hanya satu aktivitas dalam satu waktu**: Kita tidak bisa melakukan lebih dari satu aktivitas yang berlangsung pada waktu yang sama.

Ini berarti kita harus memikirkan cara terbaik untuk memanfaatkan waktu yang tersedia.

## Dasar Teori dan Konsep Greedy

ASP sering kali diselesaikan menggunakan pendekatan **Greedy Algorithm**.

### Apa Itu Greedy Algorithm?

Greedy Algorithm adalah metode pemecahan masalah yang membuat keputusan terbaik atau optimal pada setiap langkah. Harapannya, serangkaian keputusan lokal yang optimal ini akan menghasilkan solusi yang optimal secara global. Ibaratnya, memilih rute terpendek di setiap persimpangan dengan harapan mencapai tujuan dengan jarak tercepat secara keseluruhan.

### Mengapa ASP Cocok Diselesaikan dengan Greedy?

ASP sangat cocok dengan algoritma Greedy karena beberapa alasan:
* **Memiliki struktur optimalitas lokal**: Memilih aktivitas yang selesai lebih cepat akan memberikan lebih banyak ruang untuk aktivitas lain yang bisa dilakukan setelahnya.
* **Solusi optimal terbentuk dari keputusan lokal**: Solusi keseluruhan yang optimal (jumlah aktivitas maksimal) dapat dicapai dengan membuat serangkaian keputusan lokal yang optimal (memilih aktivitas yang berakhir paling awal).

## Strategi Penyelesaian dengan Algoritma Greedy

Berikut adalah langkah-langkah untuk menyelesaikan ASP menggunakan algoritma Greedy:

1.  **Urutkan aktivitas**: Urutkan semua aktivitas berdasarkan waktu selesai secara menaik (dari yang paling cepat selesai).
2.  **Pilih aktivitas pertama**: Ambil aktivitas pertama dalam daftar yang sudah terurut (aktivitas yang selesai paling cepat). Ini akan menjadi aktivitas pertama yang dipilih.
3.  **Pilih aktivitas berikutnya**: Lakukan iterasi melalui sisa aktivitas. Pilih aktivitas berikutnya jika waktu mulainya lebih besar atau sama dengan waktu selesai dari aktivitas terakhir yang telah dipilih.
4.  **Ulangi langkah ketiga**: Terus ulangi langkah ketiga sampai semua aktivitas dalam daftar telah diperiksa.

## Contoh Soal

Misalkan kita memiliki daftar aktivitas dengan waktu mulai dan waktu selesai sebagai berikut:

| Aktivitas | Waktu Mulai | Waktu Selesai |
| :-------- | :---------- | :------------ |
| A         | 3           | 6             |
| B         | 1           | 4             |
| C         | 5           | 9             |
| D         | 8           | 10            |
| E         | 2           | 7             |

Kita ingin menentukan aktivitas maksimal yang dapat dipilih sehingga tidak ada aktivitas yang saling tumpang tindih.

### Solusi Contoh Soal

1.  **Urutkan berdasarkan waktu selesai**:

| Aktivitas | Waktu Mulai | Waktu Selesai |
| :-------- | :---------- | :------------ |
| B         | 1           | 4             |
| A         | 3           | 6             |
| E         | 2           | 7             |
| C         | 5           | 9             |
| D         | 8           | 10            |

2.  **Pilih Aktivitas Pertama**:
    * Ambil aktivitas pertama dalam daftar terurut: **Aktivitas B** (selesai paling cepat).

3.  **Pilih Aktivitas yang Tidak Tumpang Tindih**:
    * Waktu selesai Aktivitas B adalah 4.
    * Lihat aktivitas berikutnya:
        * Aktivitas A: Waktu mulai 3 (lebih kecil dari 4) - Tumpang tindih.
        * Aktivitas E: Waktu mulai 2 (lebih kecil dari 4) - Tumpang tindih.
        * Aktivitas C: Waktu mulai 5 (lebih besar dari 4) - **Pilih Aktivitas C**.
    * Waktu selesai Aktivitas C adalah 9.
    * Lihat aktivitas berikutnya:
        * Aktivitas D: Waktu mulai 8 (lebih kecil dari 9) - Tumpang tindih.

4.  **Ulangi Proses**: Semua aktivitas sudah diperiksa.

**Aktivitas yang terpilih adalah B, C.**
Jumlah maksimal aktivitas yang bisa dipilih adalah **2**.

## Latihan

Mari kita coba dengan daftar aktivitas lain:

| Aktivitas | Waktu Mulai | Waktu Selesai |
| :-------- | :---------- | :------------ |
| A         | 2           | 13            |
| B         | 0           | 6             |
| C         | 5           | 9             |
| D         | 8           | 11            |
| E         | 3           | 5             |
| F         | 12          | 14            |

Tentukan aktivitas maksimal yang dapat dipilih sehingga tidak ada aktivitas yang saling tumpang tindih!

### Solusi Latihan

1.  **Urutkan berdasarkan waktu selesai**:

| Aktivitas | Waktu Mulai | Waktu Selesai |
| :-------- | :---------- | :------------ |
| E         | 3           | 5             |
| B         | 0           | 6             |
| C         | 5           | 9             |
| D         | 8           | 11            |
| A         | 2           | 13            |
| F         | 12          | 14            |

2.  **Pilih Aktivitas Pertama**:
    * **Aktivitas E** (selesai paling cepat). Waktu selesai: 5.

3.  **Pilih Aktivitas yang Tidak Tumpang Tindih**:
    * Aktivitas B: Waktu mulai 0 (lebih kecil dari 5) - Tumpang tindih.
    * Aktivitas C: Waktu mulai 5 (sama dengan 5) - **Pilih Aktivitas C**. Waktu selesai: 9.
    * Aktivitas D: Waktu mulai 8 (lebih kecil dari 9) - Tumpang tindih.
    * Aktivitas A: Waktu mulai 2 (lebih kecil dari 9) - Tumpang tindih.
    * Aktivitas F: Waktu mulai 12 (lebih besar dari 9) - **Pilih Aktivitas F**. Waktu selesai: 14.

**Aktivitas yang terpilih adalah E, C, F.**
Jumlah maksimal aktivitas yang bisa dipilih adalah **3**.

*(Catatan: Slide PPT menunjukkan E, D, F. Terdapat perbedaan hasil antara perhitungan manual mengikuti slide PPT dengan penerapan algoritma greedy yang konsisten. Jika mengikuti hasil akhir yang tertera di slide, aktivitas C tidak terpilih dan D terpilih. Ini bisa terjadi jika ada kriteria tambahan atau kesalahan dalam contoh soal. Namun, berdasarkan langkah-langkah algoritma greedy murni, urutan E, C, F akan didapatkan.)*

## Implementasi C++

Algoritma Activity Selection Problem dapat diimplementasikan dalam bahasa C++ dengan struktur data dan fungsi-fungsi sebagai berikut:

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::sort

// Structure to represent an activity
struct Activity {
    int start;
    int finish;
};

// Comparison function to sort activities by finish time
bool compareActivities(Activity a, Activity b) {
    return (a.finish < b.finish);
}

// Function to perform activity selection
void activitySelection(std::vector<Activity> activities) {
    // Sort activities by finish time
    std::sort(activities.begin(), activities.end(), compareActivities);

    std::cout << "Aktivitas yang dipilih: " << std::endl;

    // The first activity always gets selected
    int i = 0;
    std::cout << "Aktivitas (Start: " << activities[i].start << ", Finish: " << activities[i].finish << ")" << std::endl;

    // Consider rest of the activities
    for (int j = 1; j < activities.size(); j++) {
        // If this activity has start time greater than or equal to the finish time of previously selected activity, then select it
        if (activities[j].start >= activities[i].finish) {
            std::cout << "Aktivitas (Start: " << activities[j].start << ", Finish: " << activities[j].finish << ")" << std::endl;
            i = j;
        }
    }
}

int main() {
    // Example activities
    std::vector<Activity> activities = {
        {1, 8}, // Activity A (as per C++ example in slide, not the earlier examples)
        {0, 2}, // Activity B
        {4, 5}, // Activity C
        {6, 9}  // Activity D
    };

    activitySelection(activities);

    return 0;
}
```

### Penjelasan Implementasi C++

* **Struktur `Activity`**: Mendefinisikan dua atribut: `start` (waktu mulai) dan `finish` (waktu selesai) untuk setiap aktivitas.
* **Fungsi `compareActivities`**: Fungsi ini digunakan oleh `std::sort()` untuk mengurutkan aktivitas berdasarkan waktu selesai secara menaik.
* **Fungsi `activitySelection`**:
    * Pertama, ia mengurutkan aktivitas menggunakan fungsi `compareActivities`.
    * Aktivitas pertama dalam daftar yang sudah diurutkan (yang selesai paling cepat) selalu dipilih.
    * Kemudian, ia menggunakan *loop* untuk memilih aktivitas berikutnya yang tidak tumpang tindih dengan aktivitas yang terakhir dipilih. Kondisinya adalah waktu mulai aktivitas saat ini harus lebih besar atau sama dengan waktu selesai aktivitas yang terakhir dipilih.
    * Fungsi ini juga mencetak aktivitas yang dipilih beserta waktu mulai dan selesai.
* **Bagian `main`**:
    * Mendefinisikan contoh aktivitas yang akan diuji.
    * Memanggil fungsi `activitySelection` untuk menyelesaikan masalah ASP dengan algoritma greedy.

### Output Contoh Implementasi C++

Berdasarkan contoh aktivitas yang diberikan dalam kode C++ (`{1, 8}, {0, 2}, {4, 5}, {6, 9}`), outputnya akan menunjukkan aktivitas yang dipilih:

```
Aktivitas yang dipilih:
Aktivitas (Start: 0, Finish: 2)
Aktivitas (Start: 4, Finish: 5)
Aktivitas (Start: 6, Finish: 9)
```

Ini menunjukkan bahwa program memilih aktivitas sebanyak mungkin yang tidak saling bertumpang tindih, sesuai dengan prinsip greedy.

## Kesimpulan

Activity Selection Problem (ASP) adalah masalah optimasi yang sangat umum dan relevan dalam dunia nyata. Dengan pendekatan greedy, kita dapat menyelesaikannya secara efisien. Intinya, kita memilih aktivitas yang selesai paling awal dan memastikan tidak ada aktivitas yang bertabrakan.

Pendekatan ini sangat cocok diterapkan dalam berbagai aplikasi penjadwalan seperti pengelolaan kelas, penggunaan ruang, atau pengaturan wawancara. Keunggulan utama dari solusi ini adalah kesederhanaan logikanya dan efisiensi waktu komputasi yang tinggi. Dengan memahami dan menerapkan algoritma greedy pada ASP, kita dapat secara efektif mengelola dan mengoptimalkan penggunaan waktu serta sumber daya yang terbatas.