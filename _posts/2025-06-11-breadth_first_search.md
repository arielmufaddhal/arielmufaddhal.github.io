---
title: Breadth-First Search (BFS)🌐
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, MATERI 7]
tags: [algoritma, breadth-first-search, bfs, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---
# Menjelajah Jaringan: Menggali Kekuatan Breadth-First Search (BFS) 

Halo, para navigator data dan pemecah misteri konektivitas! Pernahkah Anda bertanya-tanya bagaimana aplikasi peta menemukan rute terpendek, atau bagaimana jejaring sosial merekomendasikan teman "tingkat pertama" Anda? Di balik layar semua itu, ada sebuah algoritma fundamental yang bekerja keras, yaitu **Breadth-First Search (BFS)**!

Jika Anda tertarik dengan cara komputer menjelajahi struktur data kompleks seperti graf atau pohon, dan ingin memahami bagaimana menemukan jalur paling efisien, maka Anda telah tiba di tempat yang tepat! Mari kita buka gerbang ke dunia BFS, sebuah algoritma pencarian yang bekerja dengan cermat, menjelajahi setiap "level" sebelum melangkah lebih jauh. Bersiaplah untuk memahami bagaimana BFS menjadi pondasi penting dalam berbagai teknologi yang kita gunakan sehari-hari!

## Pengertian Breadth-First Search (BFS)

Breadth-First Search (BFS) adalah algoritma pencarian atau penelusuran graf yang bekerja dengan cara menjelajahi semua simpul (node) yang berada pada level yang sama terlebih dahulu, sebelum melanjutkan ke level berikutnya.

Dalam istilah sederhana, BFS menjelajahi graf secara melebar (dari pusat ke luar), bukan langsung masuk ke dalam cabang terdalam. BFS menggunakan struktur data **queue (antrian)** untuk melacak simpul-simpul yang perlu dieksplorasi berikutnya.

### Tujuan BFS

Tujuan utama dari BFS adalah:
- Menjelajahi seluruh simpul pada graf atau pohon.
- Menemukan **jalur terpendek** pada graf yang tidak berbobot (unweighted graph).
- Mendeteksi komponen yang terhubung dalam graf.
- Digunakan sebagai dasar algoritma lanjutan (misalnya, algoritma Kruskal dan Prim untuk mencari pohon rentang minimum).
- Membantu pencarian jalur optimal dalam sistem real-time (misalnya, sistem navigasi).

## Dasar Teori BFS

BFS mengandalkan beberapa prinsip dasar:
- **Menggunakan Queue (Antrian)**: Simpul-simpul yang akan dikunjungi disimpan dalam antrian. Simpul yang pertama kali masuk ke antrian adalah yang pertama kali akan diproses (prinsip FIFO - *First-In, First-Out*).
- **Menandai Simpul yang Telah Dikunjungi**: Untuk menghindari pengulangan dan siklus tak terbatas, setiap simpul yang telah dikunjungi harus ditandai. Ini memastikan setiap simpul diproses hanya sekali.
- **Level-by-Level Exploration**: Algoritma ini memastikan bahwa semua simpul pada kedalaman `k` dieksplorasi sebelum bergerak ke simpul pada kedalaman `k+1`.

## Contoh Cara Kerja BFS

Mari kita bayangkan sebuah graf sederhana:

```
      A
     / \
    B   C
   / \   \
  D   E   F
```

Jika kita memulai BFS dari simpul `A`:

1. **Inisialisasi**:
   - Queue: `[A]`
   - Visited: `{A}`

2. **Deque A, Enqueue B, C**:
   - Proses `A`. Cetak `A`.
   - Tetangga `A` adalah `B` dan `C`.
   - Queue: `[B, C]`
   - Visited: `{A, B, C}`

3. **Deque B, Enqueue D, E**:
   - Proses `B`. Cetak `B`.
   - Tetangga `B` adalah `D` dan `E`.
   - Queue: `[C, D, E]`
   - Visited: `{A, B, C, D, E}`

4. **Deque C, Enqueue F**:
   - Proses `C`. Cetak `C`.
   - Tetangga `C` adalah `F`.
   - Queue: `[D, E, F]`
   - Visited: `{A, B, C, D, E, F}`

5. **Deque D (Tidak ada tetangga baru)**:
   - Proses `D`. Cetak `D`.
   - Queue: `[E, F]`

6. **Deque E (Tidak ada tetangga baru)**:
   - Proses `E`. Cetak `E`.
   - Queue: `[F]`

7. **Deque F (Tidak ada tetangga baru)**:
   - Proses `F`. Cetak `F`.
   - Queue: `[]`

8. **Queue kosong**: Algoritma berhenti.

**Urutan penelusuran (Output): A B C D E F**

## Implementasi C++

```cpp
#include <iostream>
#include <vector>
#include <queue>        // Untuk std::queue
#include <unordered_map> // Untuk std::unordered_map
#include <unordered_set> // Untuk std::unordered_set

void bfs(const std::unordered_map<char, std::vector<char>>& graph, char startNode) {
    std::unordered_set<char> visited;
    std::queue<char> q;

    visited.insert(startNode);
    q.push(startNode);

    while (!q.empty()) {
        char currentNode = q.front();
        q.pop();

        std::cout << currentNode << " ";

        if (graph.count(currentNode)) {
            for (char neighbor : graph.at(currentNode)) {
                if (visited.find(neighbor) == visited.end()) {
                    visited.insert(neighbor);
                    q.push(neighbor);
                }
            }
        }
    }
    std::cout << std::endl;
}

int main() {
    std::unordered_map<char, std::vector<char>> graph;

    graph['A'] = {'B', 'C'};
    graph['B'] = {'D', 'E'};
    graph['C'] = {'F'};
    graph['D'] = {};
    graph['E'] = {};
    graph['F'] = {};

    std::cout << "BFS traversal dari node A: ";
    bfs(graph, 'A');

    return 0;
}
```

### Output Contoh Implementasi C++

```
BFS traversal dari node A: A B C D E F
```

## Kesimpulan

BFS adalah algoritma fundamental dalam pencarian graf yang bekerja dengan mengeksplorasi semua simpul dalam urutan berdasarkan level atau kedalamannya. Algoritma ini memanfaatkan struktur data **queue** untuk mengelola urutan eksplorasi dan memastikan semua simpul pada satu level dikunjungi sebelum pindah ke level berikutnya.

BFS sangat cocok untuk:
- Menemukan jalur terpendek dalam graf yang tidak berbobot.
- Aplikasi lain seperti analisis jaringan sosial, *web crawling*, dan AI game.

Memahami BFS adalah langkah penting dalam menguasai algoritma graf dan merupakan pondasi bagi banyak algoritma yang lebih kompleks dalam ilmu komputer.
