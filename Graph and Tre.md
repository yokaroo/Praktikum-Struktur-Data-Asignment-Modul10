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
### Output : 
![Screenshot 2024-06-11 223500](https://github.com/yokaroo/Praktikum-Struktur-Data-Asignment-Modul10/blob/main/Screenshot%202024-06-11%20223500.png)
## Iterpretasi:
Kode di atas merupakan implementasi dasar dari sebuah pohon biner menggunakan bahasa pemrograman C++. Pertama-tama, struktur pohon didefinisikan dengan nama `pohon`, yang memiliki tiga anggota: `kanan`, `data`, dan `kiri`. Selanjutnya, beberapa variabel global dideklarasikan, termasuk `root` yang merupakan akar pohon, serta `simpul`, `saatIni`, dan array `alamat` yang digunakan untuk menyimpan alamat simpul.

Fungsi `inisialisasi` digunakan untuk menginisialisasi `root` menjadi `NULL`. Fungsi `simpulBaru` membuat simpul baru dengan data yang diberikan dan mengatur anak kiri dan kanan menjadi `NULL`. Fungsi `simpulAkar` digunakan untuk membuat akar pohon jika belum ada, dengan meminta pengguna memasukkan data untuk akar.

Fungsi `tambahSimpul` digunakan untuk menambahkan simpul baru ke dalam pohon. Dalam fungsi ini, data dimasukkan oleh pengguna untuk anak kiri dan kanan dari setiap simpul secara berurutan, dan alamat simpul disimpan dalam array `alamat`. Pengguna dapat menghentikan penambahan simpul dengan memasukkan '0'.

Fungsi `bacaPohon` digunakan untuk membaca dan mencetak data dari pohon secara level-order, dengan menggunakan array `alamat` untuk mengakses setiap simpul. Fungsi ini mencetak data dari setiap simpul dan membuat baris baru setiap kali level pohon berubah.

Terakhir, dalam fungsi `main`, program menginisialisasi pohon, membuat simpul akar, menambah simpul-simpul baru, dan kemudian membaca serta mencetak pohon yang telah dibuat.

