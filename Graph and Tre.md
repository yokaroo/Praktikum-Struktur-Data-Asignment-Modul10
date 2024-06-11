## Repository praktikum algoritma dan struktur data

<pre>
Nama : Yoka Romadani
NIM : 2311110060
Kelas : S1SD04-B
</pre>

## Dasar Teori
1. Graph
 Graf atau graph adalah struktur data yang digunakan untuk merepresentasikan
 hubungan antara objek dalam bentuk node atau vertex dan sambungan antara node
 tersebut dalam bentuk sisi atau edge.
2. Tre
 Dalam ilmu komputer, pohon/tree adalah struktur data yang sangat umum dan kuat
 yang menyerupai nyata pohon. Ini terdiri dari satu set node tertaut yang terurut
 dalam grafik yang terhubung, dimana setiap node memiliki paling banyak satu
 simpul induk, dan nol atau lebih simpul anak dengan urutan tertentu. Struktur data
 tree digunakan untuk menyimpan data-data hirarki seperti pohon keluarga, skema
 pertandingan, struktur organisasi.

## Guided
## 1. Graph
```C++
```
## 2. Tre
```C++
#include <iostream>
using namespace std;

// Definisi struktur pohon
struct pohon {
    pohon *kanan;
    char data;
    pohon *kiri;
};

// Deklarasi variabel global
pohon *simpul;
pohon *root;
pohon *saatIni;
pohon *alamat[256];

// Fungsi untuk inisialisasi root
void inisialisasi() {
    root = NULL;
}

// Fungsi untuk membuat simpul baru
void simpulBaru(char dataMasukkan) {
    simpul = new pohon;
    simpul->data = dataMasukkan;
    simpul->kanan = NULL;
    simpul->kiri = NULL;
}

// Fungsi untuk membuat simpul akar
void simpulAkar() {
    if (root == NULL) {
        char dataAnda;
        cout << "Silahkan masukkan data: ";
        cin >> dataAnda;
        simpulBaru(dataAnda);
        root = simpul;
        cout << "Root terbentuk..." << endl;
    } else {
        cout << "Root sudah ada..." << endl;
    }
}

// Fungsi untuk menambah simpul
void tambahSimpul() {
    if (root != NULL) {
        int i = 1, j = 1, penanda = 0;
        char dataUser;
        alamat[i] = root;

        while (penanda == 0 && j < 256) {
            cout << "Masukkan data kiri (0 untuk berhenti): ";
            cin >> dataUser;
            if (dataUser != '0') {
                simpulBaru(dataUser);
                saatIni = alamat[i];
                saatIni->kiri = simpul;
                j++;
                alamat[j] = simpul;
            } else {
                penanda = 1;
                j++;
                alamat[j] = NULL;
            }

            if (penanda == 0) {
                cout << "Masukkan data kanan (0 untuk berhenti): ";
                cin >> dataUser;
                if (dataUser != '0') {
                    simpulBaru(dataUser);
                    saatIni = alamat[i];
                    saatIni->kanan = simpul;
                    j++;
                    alamat[j] = simpul;
                } else {
                    penanda = 1;
                    j++;
                    alamat[j] = NULL;
                }
            }
            i++;
        }
    }
}

// Fungsi untuk membaca pohon
void bacaPohon() {
    if (root != NULL) {
        int i = 1, n = 1, pencacah = 0;
        cout << endl;
        while (alamat[i] != NULL) {
            saatIni = alamat[i];
            cout << saatIni->data << " ";
            pencacah++;
            if (pencacah == n) {
                cout << endl;
                pencacah = 0;
                n = n * 2;
            }
            i++;
        }
        cout << endl; // Tambahkan baris baru di akhir
    }
}

// Fungsi utama
int main() {
    inisialisasi();
    simpulAkar();
    tambahSimpul();
    bacaPohon();
    return 0;
}
```
