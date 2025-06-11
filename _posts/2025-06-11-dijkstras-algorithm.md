---
title: Dijkstra's Algorithm🚀
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, MATERI 10]
tags: [algoritma, dijkstra's-algorithm, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---
# Menjelajahi Rute Terpendek: Menggali Kekuatan Dijkstra's Algorithm

Halo, para perencana perjalanan dan pemburu efisiensi! Pernahkah Anda bertanya-tanya bagaimana aplikasi navigasi di ponsel Anda bisa langsung menemukan rute tercepat ke tujuan, bahkan dengan mempertimbangkan kemacetan atau jalur alternatif? Atau mungkin Anda seorang *network engineer* yang harus merancang jaringan dengan *cost* terendah?

Jika Anda tertarik untuk memahami bagaimana komputer menemukan "jalan pintas" terbaik dalam sebuah labirin konektivitas, maka Anda telah datang ke tempat yang tepat! Mari kita selami **Dijkstra's Algorithm**, sebuah mahakarya algoritma yang dirancang untuk menemukan jalur terpendek dalam graf berbobot. Ini bukan hanya sekadar teka-teki, melainkan pondasi vital bagi banyak teknologi yang kita gunakan sehari-hari. Bersiaplah untuk memetakan jalur dan menemukan rute optimal!

## Pengertian Dijkstra's Algorithm

Dijkstra's Algorithm adalah sebuah algoritma pencarian jalur terpendek yang ditemukan oleh ilmuwan komputer Edsger Dijkstra dan pertama kali dipublikasikan pada tahun 1959.

### Tujuan Utama

- Mencari **lintasan terpendek** dari satu titik (simpul/node) awal ke semua titik lainnya dalam sebuah graf berarah dengan bobot-bobot sisi (edge) yang bernilai **positif atau tak-negatif**.
- Algoritma ini merupakan jenis dari **Greedy Algorithm** atau algoritma rakus, yang berarti pada setiap langkah, ia membuat pilihan terbaik secara lokal dengan harapan akan mengarah pada solusi optimal secara global.

## Tujuan dan Kegunaan Dijkstra's Algorithm

### Tujuan

Menentukan jalur terpendek dari satu titik ke titik lainnya dalam sebuah graf berbobot positif.

### Kegunaan di Kehidupan Nyata

1. **Pemetaan dan Navigasi Digital**: Google Maps, Waze, GPS.
2. **Jaringan Komputer**: Routing paket data pada jaringan internet.
3. **Transportasi dan Logistik**: Optimalisasi jalur pengiriman barang.
4. **Optimasi Resource Allocation**: Efisiensi penggunaan resource dalam sistem produksi.

## Konsep Dasar Algoritma Dijkstra

1. **Inisialisasi**:
   - `dist[sumber] = 0`, simpul lainnya `= ∞`
   - `visited = {}`

2. **Iterasi**:
   - Pilih simpul `U` dengan jarak terpendek.
   - Untuk setiap tetangga `V`:
     - Jika `dist[U] + weight(U,V) < dist[V]`, perbarui `dist[V]`.

3. **Terminasi**: Berhenti jika semua simpul dikunjungi atau simpul tujuan tercapai.

## Contoh Graf

```
       5
   S ----- A
  /|       |\
 10|       |2
  /|       | \
 C ----- B ----- E
  \      / \    /
   3    1   6  1
    \  /     \/
     D
```

### Hasil Dijkstra dari S ke E

- **Jarak terpendek**: 9
- **Lintasan terpendek**: `S -> A -> B -> D -> E`

> ⚠️ Catatan: PPT menyebutkan lintasan dengan total bobot 4. Kemungkinan graf pada PPT berbeda atau bobot dianggap 1 (graf tak berbobot).

## Implementasi C++

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>
#include <map>

using PII = std::pair<int, int>;

void dijkstra(int startNode, int numNodes, const std::vector<std::vector<PII>>& adj) {
    std::vector<int> dist(numNodes, std::numeric_limits<int>::max());
    std::map<int, int> prevNode;
    std::priority_queue<PII, std::vector<PII>, std::greater<PII>> pq;

    dist[startNode] = 0;
    pq.push({0, startNode});

    while (!pq.empty()) {
        int d = pq.top().first;
        int u = pq.top().second;
        pq.pop();

        if (d > dist[u]) continue;

        for (const auto& edge : adj[u]) {
            int v = edge.second;
            int weight = edge.first;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                prevNode[v] = u;
                pq.push({dist[v], v});
            }
        }
    }

    std::cout << "Jarak terpendek dari simpul " << startNode << ":
";
    for (int i = 0; i < numNodes; ++i) {
        if (dist[i] == std::numeric_limits<int>::max()) {
            std::cout << "Ke simpul " << i << ": Tidak terjangkau
";
        } else {
            std::cout << "Ke simpul " << i << ": " << dist[i] << "
";
        }
    }
}

int main() {
    int numNodes = 6;
    std::vector<std::vector<PII>> adj(numNodes);

    adj[0].push_back({5, 1});  // S -> A
    adj[0].push_back({10, 3}); // S -> C
    adj[1].push_back({2, 2});  // A -> B
    adj[2].push_back({1, 4});  // B -> D
    adj[2].push_back({6, 5});  // B -> E
    adj[4].push_back({1, 5});  // D -> E
    adj[4].push_back({3, 3});  // D -> C

    dijkstra(0, numNodes, adj);
}
```

## Penutup

Dengan memahami Dijkstra's Algorithm, Anda telah mempelajari salah satu dasar terpenting dari *graph theory* yang berperan besar di balik banyak teknologi modern. Siap menjelajah rute optimal berikutnya?

Selamat bertualang di dunia algoritma! 🗺️
