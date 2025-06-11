---
title: Kahn's Algorithm🔗
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, MATERI 9]
tags: [algoritma, kahn's-algorithm, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---
# Merangkai Urutan: Menyelami Kahn's Algorithm untuk Topological Sort 

Halo, para arsitek dependensi dan perancang alur kerja! Pernahkah Anda harus mengatur serangkaian tugas yang saling terkait, di mana satu tugas harus selesai sebelum yang lain bisa dimulai? Atau mungkin Anda seorang *programmer* yang perlu mengkompilasi modul-modul kode dengan urutan yang benar?

Jika Anda tertarik dengan cara mengurutkan elemen-elemen yang memiliki ketergantungan, maka Anda telah datang ke tempat yang tepat! Mari kita selami **Kahn's Algorithm**, sebuah metode elegan untuk melakukan *topological sort* pada graf. Ini bukan hanya sekadar algoritma, melainkan kunci untuk mengatur kompleksitas dan memastikan segala sesuatu berjalan sesuai urutan yang logis. Bersiaplah untuk merangkai tugas-tugas ini menjadi sebuah alur yang sempurna!

## Apa Itu Kahn's Algorithm?

Kahn's Algorithm adalah algoritma yang digunakan untuk melakukan **topological sort** pada **graf berarah tanpa siklus (DAG - Directed Acyclic Graph)**. Algoritma ini diperkenalkan oleh Arthur B. Kahn pada tahun 1962.

### Tujuan Utama:

- **Menyusun simpul-simpul (nodes)** dalam urutan linear sedemikian rupa sehingga jika ada *edge* (panah) dari simpul `U` ke simpul `V`, maka `U` akan selalu muncul sebelum `V` dalam urutan hasil.

### Aplikasi:

- **Penjadwalan tugas**: Mengatur urutan tugas yang saling bergantung (misalnya, tugas proyek, proses manufaktur).
- **Kompilasi kode**: Menentukan urutan kompilasi file sumber yang memiliki dependensi.
- **Sistem *****build***: Mengelola ketergantungan antar modul dalam proyek perangkat lunak.
- **Dependensi antar modul**: Memastikan modul yang dibutuhkan sudah tersedia sebelum modul lain dijalankan.

## Konsep Utama Kahn's Algorithm

Kahn's Algorithm beroperasi berdasarkan tiga konsep inti:

1. **Graf Berarah (Directed Graph)**

   - **DAG (Directed Acyclic Graph)**: Adalah graf berarah yang **tanpa siklus**. Ini sangat penting karena *topological sort* hanya mungkin dilakukan pada DAG. Jika ada siklus, simpul-simpul dalam siklus akan saling bergantung secara sirkular, sehingga tidak bisa diurutkan secara linear.
   - DAG digunakan untuk memodelkan hubungan dependensi atau urutan tugas. Algoritma Kahn's memanfaatkan DAG untuk menghasilkan urutan topologis, memastikan tidak ada ketergantungan yang bertentangan.

2. **Acyclic (Tanpa Siklus)**

   - Berarti graf tidak boleh memiliki rangkaian *edge* yang membentuk *loop* (jalur berulang ke simpul yang sama).
   - Dalam Kahn's Algorithm, sifat *acyclic* ini sangat kritis karena *topological sort* hanya bisa dilakukan pada graf tanpa siklus.

3. **In-degree**

   - *In-degree* dari sebuah simpul adalah **jumlah *****edge***** yang masuk ke simpul tersebut**.
   - Simpul dengan *in-degree* nol (`0`) tidak memiliki dependensi sebelumnya dan dapat menjadi titik awal dalam urutan topologis.
   - Kahn's Algorithm secara berulang kali memilih simpul dengan *in-degree* nol, menambahkannya ke hasil *topological sort*, dan kemudian mengurangi *in-degree* dari semua tetangganya. Proses ini berlanjut sampai semua simpul telah diproses.

## Proses Kahn's Algorithm

Algoritma Kahn's bekerja dengan langkah-langkah berikut:

1. **Hitung *****In-degree***** Setiap Simpul**: Untuk setiap simpul dalam graf, hitung berapa banyak *edge* yang masuk ke dalamnya.
2. **Inisialisasi Antrian**: Tambahkan semua simpul yang memiliki *in-degree* nol ke dalam antrian (`queue`). Simpul-simpul ini adalah yang pertama yang dapat diproses karena tidak bergantung pada simpul lain.
3. **Proses Antrian**:
   - Selama antrian tidak kosong:
     - Ambil (dequeue) simpul `U` dari depan antrian.
     - Tambahkan `U` ke dalam daftar hasil *topological sort*.
     - Untuk setiap tetangga `V` dari `U` (yaitu, ada *edge* dari `U` ke `V`):
       - Kurangi *in-degree* dari `V` sebanyak 1.
       - Jika *in-degree* dari `V` menjadi nol, tambahkan `V` ke dalam antrian.
4. **Cek Siklus**: Setelah antrian kosong, jika jumlah simpul dalam daftar hasil *topological sort* sama dengan total jumlah simpul dalam graf, berarti graf tidak memiliki siklus dan urutan topologis berhasil ditemukan. Jika tidak, berarti graf memiliki siklus dan *topological sort* tidak mungkin dilakukan.

## Contoh Kahn's Algorithm

Mari kita terapkan Kahn's Algorithm pada graf berikut:

```
  0 ----> 1
  ^       ^
  |       |
  4 ----> 2 ----> 3
```

Edge: `(4,0), (4,1), (2,3), (3,1)`

1. **Hitung In-degree Awal**:

   - `in_degree[0] = 1` (dari 4)
   - `in_degree[1] = 2` (dari 4, dari 3)
   - `in_degree[2] = 0`
   - `in_degree[3] = 1` (dari 2)
   - `in_degree[4] = 0`

2. **Inisialisasi Antrian**: Simpul dengan *in-degree* 0 adalah `2` dan `4`.

   - Queue: `[2, 4]`

3. **Proses Antrian**:

   - **Dequeue 2**: Tambahkan `2` ke hasil.

     - Hasil: `[2]`
     - Tetangga 2 adalah 3. Kurangi `in_degree[3]` dari 1 menjadi 0. Enqueue 3.
     - Queue: `[4, 3]`

   - **Dequeue 4**: Tambahkan `4` ke hasil.

     - Hasil: `[2, 4]`
     - Tetangga 4 adalah 0 dan 1. Kurangi `in_degree[0]` menjadi 0, `in_degree[1]` menjadi 1. Enqueue 0.
     - Queue: `[3, 0]`

   - **Dequeue 3**: Tambahkan `3` ke hasil.

     - Hasil: `[2, 4, 3]`
     - Tetangga 3 adalah 1. Kurangi `in_degree[1]` menjadi 0. Enqueue 1.
     - Queue: `[0, 1]`

   - **Dequeue 0**: Tambahkan `0` ke hasil.

     - Hasil: `[2, 4, 3, 0]`
     - Queue: `[1]`

   - **Dequeue 1**: Tambahkan `1` ke hasil.

     - Hasil: `[2, 4, 3, 0, 1]`

4. **Antrian kosong**. Jumlah simpul di hasil (5) sama dengan total simpul (5).

**Hasil Topological Sort: [2, 4, 3, 0, 1]**

## Implementasi C++

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <numeric> // For std::iota

class Solution {
public:
    std::vector<int> topoSort(int V, const std::vector<std::vector<int>>& adj) {
        std::vector<int> in_degree(V, 0);

        for (int u = 0; u < V; ++u) {
            for (int v : adj[u]) {
                in_degree[v]++;
            }
        }

        std::queue<int> q;
        for (int i = 0; i < V; ++i) {
            if (in_degree[i] == 0) {
                q.push(i);
            }
        }

        std::vector<int> topo_order;

        while (!q.empty()) {
            int u = q.front();
            q.pop();
            topo_order.push_back(u);

            for (int v : adj[u]) {
                in_degree[v]--;
                if (in_degree[v] == 0) {
                    q.push(v);
                }
            }
        }

        if (topo_order.size() != V) {
            std::cerr << "Graf memiliki siklus! Topological sort tidak mungkin." << std::endl;
            return {};
        }

        return topo_order;
    }
};

int main() {
    int V = 5;
    std::vector<std::vector<int>> adj(V);

    adj[4].push_back(0);
    adj[4].push_back(1);
    adj[2].push_back(3);
    adj[3].push_back(1);

    Solution obj;
    std::vector<int> result = obj.topoSort(V, adj);

    if (!result.empty()) {
        std::cout << "Topological Sort (Kahn's Algorithm): ";
        for (int node : result) {
            std::cout << node << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

### Output Contoh Implementasi C++

```
Topological Sort (Kahn's Algorithm): 2 4 3 0 1
```

## Kesimpulan

Kahn's Algorithm adalah metode yang efisien dan logis untuk melakukan *topological sort* pada **Directed Acyclic Graphs (DAGs)**. Dengan berfokus pada *in-degree* simpul, algoritma ini secara sistematis membangun urutan linier dari simpul-simpul, memastikan semua dependensi terpenuhi.

Pemahaman tentang Kahn's Algorithm sangat penting untuk berbagai masalah yang melibatkan penjadwalan, manajemen dependensi, dan pemrosesan data berurutan. Ini adalah alat fundamental dalam toolkit algoritma graf.

