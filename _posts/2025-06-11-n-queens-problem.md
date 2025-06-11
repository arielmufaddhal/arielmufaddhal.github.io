---
title: N-Queens Problem♟️
date: 2025-06-11
categories: [DESAIN DAN ANALISIS ALGORITMA, MATERI 4]
tags: [algoritma, n-queens-problem, daa, desain-dan-analisis-algoritma]     # TAG names should always be lowercase
---
# Mengatur Ratu: Menaklukkan N-Queens Problem 

Halo, para jenderal strategi dan ahli teka-teki! Pernahkah Anda membayangkan sebuah medan perang catur di mana setiap ratu adalah komandan yang harus ditempatkan dengan sempurna, tanpa ada yang bisa saling menyerang? Ini bukan sekadar permainan, melainkan sebuah tantangan logika yang menguji kemampuan kita dalam berpikir algoritmik!

Jika Anda tertarik dengan kombinatorika, *backtracking*, dan memecahkan masalah kompleks, maka Anda telah tiba di tempat yang tepat! Mari kita selami dunia **N-Queens Problem**, sebuah masalah klasik dalam ilmu komputer yang telah memukau para ilmuwan dan *programmer* selama berabad-abad. Bersiaplah untuk menyusun strategi, karena kita akan menempatkan ratu-ratu ini di papan catur dengan presisi tinggi!

## Apa Itu N-Queens Problem?

N-Queens Problem adalah masalah klasik dalam bidang algoritma dan teori komputasi yang berfokus pada penempatan sejumlah ratu (queen) di papan catur berdimensi $N \times N$. Tujuan utamanya adalah memastikan tidak ada ratu yang saling menyerang satu sama lain.

### Penempatan Ratu yang Aman

* Setiap ratu harus ditempatkan di posisi yang tidak satu baris, tidak satu kolom, dan tidak satu diagonal dengan ratu lainnya.
* Tujuan ini mengharuskan algoritma untuk mengecek konflik horizontal, vertikal, dan diagonal secara cermat setiap kali menempatkan sebuah ratu.

### Menemukan Semua Solusi

Dalam beberapa kasus, yang dicari adalah semua solusi yang mungkin untuk penempatan ratu-ratu tersebut.

## Konsep N-Queens Problem

Masalah N-Queens biasanya diselesaikan menggunakan algoritma *backtracking*.

### Bagaimana Backtracking Bekerja?

* **Pencarian Rekursif**: Algoritma ini mencari solusi dengan cara rekursif, mencoba menempatkan satu ratu per baris.
* **Percobaan dan Kesalahan**: Jika penempatan ratu di suatu posisi aman, algoritma akan melanjutkan ke baris berikutnya. Jika tidak ada posisi aman di baris saat ini, algoritma akan "mundur" (*backtrack*) ke baris sebelumnya dan mencoba posisi lain.
* **Kondisi Batas**: Proses berhenti ketika semua ratu berhasil ditempatkan (solusi ditemukan) atau ketika semua kemungkinan penempatan telah dicoba dan tidak ada solusi yang ditemukan.

### Pemeriksaan Keamanan

Sebelum menempatkan ratu pada suatu sel `(row, col)`, kita harus memeriksa apakah posisi tersebut aman, yaitu tidak ada ratu lain yang sudah ditempatkan di:

* **Baris yang sama**
* **Kolom yang sama**
* **Diagonal atas-kiri** `(row-i, col-i)`
* **Diagonal atas-kanan** `(row-i, col+i)`

## Contoh N-Queens Problem (N=4)

Untuk $N=4$, ada dua solusi unik untuk menempatkan 4 ratu di papan catur $4 \times 4$.

### Solusi 1:

```
. Q . .
. . . Q
Q . . .
. . Q .
```

### Solusi 2:

```
. . Q .
Q . . .
. . . Q
. Q . .
```

## Implementasi N-Queens Problem (C++)

Berikut adalah struktur dasar implementasi N-Queens Problem menggunakan C++:

```cpp
#include <iostream>
#include <vector>

const int N = 4; // Ukuran papan catur (misal N=4)
int board[N][N]; // Papan catur

void printBoard() {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            std::cout << (board[i][j] ? "Q " : ". ");
        }
        std::cout << std::endl;
    }
    std::cout << std::endl;
}

bool isSafe(int row, int col) {
    for (int i = 0; i < col; i++)
        if (board[row][i]) return false;

    for (int i = row, j = col; i >= 0 && j >= 0; i--, j--)
        if (board[i][j]) return false;

    for (int i = row, j = col; i < N && j >= 0; i++, j--)
        if (board[i][j]) return false;

    return true;
}

bool solveNQueens(int col) {
    if (col >= N) {
        printBoard();
        return true;
    }

    bool res = false;
    for (int i = 0; i < N; i++) {
        if (isSafe(i, col)) {
            board[i][col] = 1;
            res = solveNQueens(col + 1) || res;
            board[i][col] = 0;
        }
    }
    return res;
}

int main() {
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            board[i][j] = 0;

    if (!solveNQueens(0))
        std::cout << "Tidak ada solusi ditemukan untuk N = " << N << std::endl;

    return 0;
}
```

## Kesimpulan

N-Queens Problem adalah masalah penempatan ratu di papan catur agar tidak saling menyerang. Masalah ini dapat diselesaikan secara efisien menggunakan algoritma *backtracking*. Setiap langkah dalam *backtracking* memilih posisi yang aman untuk ratu. Solusi yang ditemukan akan mencetak papan dengan posisi `Q` untuk ratu dan `.` untuk sel kosong. Keunggulan dari solusi ini adalah kesederhanaan logika dan efisiensi waktu komputasi, menjadikannya contoh klasik dalam Desain dan Analisis Algoritma.
