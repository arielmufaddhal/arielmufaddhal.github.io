---
title: Depth-First Search (DFS)🌊
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, MATERI 8]
tags: [algoritma, depth-first-search, dfs, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---
# Menyelami Kedalaman: Menguasai Depth-First Search (DFS)

Halo, para penjelajah data dan pemecah misteri labirin digital! Pernahkah Anda merasa seperti seorang petualang yang menyelam jauh ke dalam gua, mengeksplorasi setiap lorong hingga buntu sebelum kembali ke permukaan untuk mencari jalan lain? Atau mungkin Anda seorang *programmer* yang ingin menemukan semua kemungkinan jalan dalam sebuah jaringan yang kompleks?

Jika tantangan eksplorasi mendalam membangkitkan rasa ingin tahu Anda, maka Anda telah tiba di tempat yang tepat! Mari kita selami **Depth-First Search (DFS)**, sebuah algoritma pencarian yang bekerja dengan cara yang unik: ia akan "menyelam" sejauh mungkin ke dalam satu cabang sebelum kembali dan menjelajahi cabang lainnya. Bersiaplah untuk memahami bagaimana DFS menjadi alat yang tak ternilai dalam berbagai aplikasi, mulai dari menemukan jalur hingga mendeteksi siklus dalam struktur data!

## Definisi Depth-First Search (DFS)

Depth-First Search (DFS) adalah salah satu metode penelusuran dalam struktur data seperti graf atau pohon. Cara kerja DFS mirip seperti menyusuri jalan bercabang: kita akan terus berjalan ke arah satu cabang hingga mencapai ujung, sebelum kembali dan mencoba cabang lainnya.

Artinya, algoritma ini akan mengunjungi simpul (node) sedalam mungkin terlebih dahulu, baru kemudian kembali ke belakang (*backtrack*) jika sudah tidak ada jalur lain yang bisa dilalui. DFS bisa dijalankan menggunakan rekursi atau dengan bantuan struktur data seperti tumpukan (*stack*).

Algoritma ini banyak digunakan dalam berbagai aplikasi, seperti mencari jalur dalam labirin, memeriksa apakah sebuah graf memiliki siklus, atau membagi graf menjadi beberapa bagian yang saling terhubung. DFS sederhana dan efisien, tetapi membutuhkan perhatian agar tidak mengunjungi simpul yang sama berulang kali, terutama pada graf yang memiliki banyak siklus.

## Jenis-Jenis DFS

DFS dapat diimplementasikan dan digunakan dalam berbagai bentuk, masing-masing dengan kegunaan spesifik:

1. **DFS Rekursif**: Implementasi paling umum dan intuitif, menggunakan *call stack* bawaan sistem untuk manajemen rekursi.
2. **DFS Iteratif (menggunakan stack)**: Menggunakan struktur data *stack* eksplisit (bukan *call stack* rekursi) untuk mencapai efek yang sama.
3. **DFS untuk Deteksi Siklus**: Digunakan untuk mengetahui apakah ada siklus (jalur tertutup) dalam graf.
4. **DFS untuk Topological Sort**: Mengurutkan simpul-simpul dalam graf asiklik berarah (DAG) sedemikian rupa sehingga untuk setiap busur `(u, v)`, `u` muncul sebelum `v`.
5. **DFS untuk Menemukan Komponen Terhubung / SCC (Strongly Connected Components)**: Mengidentifikasi subgraf di mana setiap simpul dapat dijangkau dari setiap simpul lain.
6. **DFS Terbatas Kedalaman (Depth-Limited Search - DLS)**: DFS dengan batasan kedalaman maksimum untuk mencegah eksplorasi tak terbatas pada graf yang sangat besar atau siklis.
7. **Pencarian Iteratif Mendalam (Iterative Deepening Depth-First Search - IDDFS)**: Menggabungkan keunggulan DFS (memori rendah) dan BFS (menemukan solusi terpendek) dengan melakukan serangkaian DLS dengan kedalaman yang meningkat.
8. **DFS untuk Mencari Jalan Terpendek**: Meskipun BFS lebih umum untuk jalur terpendek pada graf tidak berbobot, DFS dapat diadaptasi untuk mencari jalur terpendek pada skenario tertentu atau dengan modifikasi (misalnya, jika semua bobot tepi sama).

## Konsep Dasar DFS

- **Strategi Depth-First**: Mengunjungi simpul dan kemudian menjelajahi sedalam mungkin di sepanjang setiap cabangnya sebelum *backtrack*.
- **Penggunaan Stack**: Secara implisit (rekursi) atau eksplisit, *stack* digunakan untuk melacak simpul yang perlu dikunjungi.
- **Penandaan Simpul yang Dikunjungi**: Penting untuk mencegah mengunjungi simpul yang sama berulang kali dan menghindari *loop* tak terbatas pada graf yang memiliki siklus.
- **Penelusuran Non-Prioritas**: DFS tidak menjamin menemukan jalur terpendek (kecuali dalam kasus khusus seperti pohon atau ketika menemukan solusi pertama yang valid).

## Contoh Cara Kerja DFS

Mari kita lihat sebuah contoh graf sederhana dan lakukan traversal DFS:

```
      A
     / \
    B   C
   / \   \
  D   E   F
```

Jika kita memulai DFS dari simpul `A`:

1. **Mulai dari A**: Kunjungi `A`. Tambahkan `A` ke *visited*.
2. **Dari A, pergi ke B**: Kunjungi `B`. Tambahkan `B` ke *visited*.
3. **Dari B, pergi ke D**: Kunjungi `D`. Tambahkan `D` ke *visited*.
4. **Dari D, tidak ada tetangga yang belum dikunjungi**. *Backtrack* ke `B`.
5. **Dari B, pergi ke E**: Kunjungi `E`. Tambahkan `E` ke *visited*.
6. **Dari E, tidak ada tetangga yang belum dikunjungi**. *Backtrack* ke `B`.
7. **Dari B, tidak ada lagi tetangga yang belum dikunjungi**. *Backtrack* ke `A`.
8. **Dari A, pergi ke C**: Kunjungi `C`. Tambahkan `C` ke *visited*.
9. **Dari C, pergi ke F**: Kunjungi `F`. Tambahkan `F` ke *visited*.
10. **Dari F, tidak ada tetangga yang belum dikunjungi**. *Backtrack* ke `C`.
11. **Dari C, tidak ada lagi tetangga yang belum dikunjungi**. *Backtrack* ke `A`.
12. **Dari A, tidak ada lagi tetangga yang belum dikunjungi**. *Traversal selesai.*

**Urutan penelusuran (Output): A B D E C F**

## Latihan Soal

Diberikan sebuah graf:

```
(Graf seperti di PPT, dengan simpul A, B, C, D, E, F, G, H, I, J, K, L dan koneksi tertentu)
```

Lakukan traversal Depth-First Search (DFS) dari simpul A untuk mencapai simpul J. Tampilkan urutan simpul yang dikunjungi hingga mencapai J.

**Urutan kunjungan:**

A $\rightarrow$ B $\rightarrow$ E $\rightarrow$ H $\rightarrow$ I $\rightarrow$ L $\rightarrow$ J

## Implementasi C++

Berikut adalah contoh implementasi DFS dalam C++ menggunakan rekursi:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <unordered_set>

// Fungsi rekursif untuk melakukan Depth-First Search
void dfs(const std::unordered_map<char, std::vector<char>>& graph, char currentNode, std::unordered_set<char>& visited) {
    visited.insert(currentNode);
    std::cout << currentNode << " ";

    if (graph.count(currentNode)) {
        for (char neighbor : graph.at(currentNode)) {
            if (visited.find(neighbor) == visited.end()) {
                dfs(graph, neighbor, visited);
            }
        }
    }
}

int main() {
    std::unordered_map<char, std::vector<char>> graph;

    graph['A'] = {'B', 'C'};
    graph['B'] = {'D', 'E'};
    graph['C'] = {'F'};
    graph['E'] = {'H'};
    graph['H'] = {'I'};
    graph['I'] = {'L'};
    graph['L'] = {'J'};

    std::cout << "DFS traversal dari node A: ";
    std::unordered_set<char> visitedNodes;
    dfs(graph, 'A', visitedNodes);
    std::cout << std::endl;

    return 0;
}
```

## Kesimpulan

Depth-First Search (DFS) adalah algoritma penelusuran graf yang menjelajahi simpul-simpul sedalam mungkin sebelum kembali (backtrack) untuk mencoba cabang lain. Dengan memanfaatkan rekursi atau *stack*, DFS efektif dalam menemukan jalur, mendeteksi siklus, dan mengidentifikasi komponen terhubung dalam graf.

Meskipun DFS tidak selalu menemukan jalur terpendek (seperti BFS), ia memiliki keunggulan dalam penggunaan memori yang lebih efisien dan kesederhanaan implementasi untuk banyak masalah graf. Memahami DFS adalah kunci untuk memecahkan berbagai tantangan kompleks dalam ilmu komputer dan analisis data.

