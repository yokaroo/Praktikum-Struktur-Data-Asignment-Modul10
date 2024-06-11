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
#include<iostream> // Mengimpor library iostream untuk input-output
#include<iomanip> // Mengimpor library iomanip untuk format output
using namespace std; // Menggunakan namespace std untuk memudahkan penggunaan fungsi dari library

string simpul[7] = {"ciamis", "Bandung","Bekasi","Tasikmalaya","cianjur","Purwokerto", "Yogyakarta"}; // Array simpul yang berisi nama-nama kota

int busur [7][7] = { // Matriks busur yang merepresentasikan jarak antar kota
    {0, 7, 8, 0, 0, 0, 0},
    {0, 0, 5, 0, 9, 15, 0},
    {0, 5, 0, 9, 5, 0, 0},
    {0, 0, 0, 2, 4, 0, 8},
    {3, 0, 0, 1, 0, 0, 0},
    {0, 0, 7, 0, 0, 9, 4},
    {0, 0, 0, 0, 8, 0, 0}
};

void tampilGraph(){ // Fungsi untuk menampilkan graf
    for(int i = 0; i < 7; i++){ // Iterasi untuk setiap simpul
        cout<<simpul[i]<<" : "<<endl; // Menampilkan nama kota
        for(int j = 0; j < 7; j++){ // Iterasi untuk setiap busur
            if(busur[i][j] != 0 ) // Jika terdapat jarak antar kota
            cout<<"-->"<<simpul[j]<<" ("<<busur[i][j]<<")"<<endl; // Menampilkan koneksi antar kota beserta jaraknya
        }
        cout<<endl; // Baris kosong untuk pemisah
    }
}

int main(){ // Fungsi utama
    tampilGraph(); // Memanggil fungsi tampilGraph untuk menampilkan graf
    return 0; // Mengembalikan nilai 0 sebagai penanda program berjalan dengan sukses
}
```
### Output:
![Screenshot 2024-06-11 232901](https://github.com/yokaroo/Praktikum-Struktur-Data-Asignment-Modul10/blob/main/Screenshot%202024-06-11%20232901.png)

## Interpretasi code:
Kode di atas adalah implementasi dasar dari graf yang merepresentasikan hubungan antar kota menggunakan matriks ketetanggaan (adjacency matrix) dalam bahasa pemrograman C++. Pertama, dua library C++ diimpor: `iostream` untuk operasi input-output dan `iomanip` untuk pengaturan format output, dan kemudian namespace `std` digunakan untuk mempermudah pemanggilan fungsi-fungsi dari library tersebut.

Array `simpul` dideklarasikan dengan tujuh elemen yang masing-masing berisi nama-nama kota: "ciamis", "Bandung", "Bekasi", "Tasikmalaya", "cianjur", "Purwokerto", dan "Yogyakarta". Matriks `busur` dideklarasikan sebagai matriks 7x7 yang menyimpan jarak antar kota dalam bentuk bilangan bulat. Elemen matriks `busur[i][j]` menyimpan jarak dari kota `simpul[i]` ke kota `simpul[j]`, dengan nilai nol menunjukkan bahwa tidak ada jalan langsung antara dua kota tersebut.

Fungsi `tampilGraph` digunakan untuk menampilkan representasi graf. Fungsi ini menggunakan dua loop `for` bersarang untuk mengiterasi setiap simpul dan setiap busur. Jika ada jarak yang bukan nol antara dua kota, maka koneksi antar kota beserta jaraknya ditampilkan dengan format "-->[nama kota] (jarak)". Setiap simpul dan koneksinya ditampilkan pada baris baru untuk memudahkan pembacaan.

Fungsi `main` adalah fungsi utama program yang memanggil `tampilGraph` untuk menampilkan graf, dan kemudian mengembalikan nilai 0 sebagai penanda bahwa program telah selesai berjalan dengan sukses.
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
## Iterpretasi code:
Kode di atas merupakan implementasi dasar dari sebuah pohon biner menggunakan bahasa pemrograman C++. Pertama-tama, struktur pohon didefinisikan dengan nama `pohon`, yang memiliki tiga anggota: `kanan`, `data`, dan `kiri`. Selanjutnya, beberapa variabel global dideklarasikan, termasuk `root` yang merupakan akar pohon, serta `simpul`, `saatIni`, dan array `alamat` yang digunakan untuk menyimpan alamat simpul.

Fungsi `inisialisasi` digunakan untuk menginisialisasi `root` menjadi `NULL`. Fungsi `simpulBaru` membuat simpul baru dengan data yang diberikan dan mengatur anak kiri dan kanan menjadi `NULL`. Fungsi `simpulAkar` digunakan untuk membuat akar pohon jika belum ada, dengan meminta pengguna memasukkan data untuk akar.

Fungsi `tambahSimpul` digunakan untuk menambahkan simpul baru ke dalam pohon. Dalam fungsi ini, data dimasukkan oleh pengguna untuk anak kiri dan kanan dari setiap simpul secara berurutan, dan alamat simpul disimpan dalam array `alamat`. Pengguna dapat menghentikan penambahan simpul dengan memasukkan '0'.

Fungsi `bacaPohon` digunakan untuk membaca dan mencetak data dari pohon secara level-order, dengan menggunakan array `alamat` untuk mengakses setiap simpul. Fungsi ini mencetak data dari setiap simpul dan membuat baris baru setiap kali level pohon berubah.

Terakhir, dalam fungsi `main`, program menginisialisasi pohon, membuat simpul akar, menambah simpul-simpul baru, dan kemudian membaca serta mencetak pohon yang telah dibuat.
## SS FUL code Guided:
![Guided1](https://github.com/yokaroo/Praktikum-Struktur-Data-Asignment-Modul10/blob/main/Guided1.png)
![Guided2](https://github.com/yokaroo/Praktikum-Struktur-Data-Asignment-Modul10/blob/main/Guided2.png)

## Un guided
## 1. Buatlah program graph dengan menggunakan inputan user untuk menghitung jarak dari sebuah kota ke kota lainnya.
```C++
#include <iostream>
#include <iomanip>
#include <vector>
#include <string>
#include <unordered_map>
using namespace std;

vector<string> Yoka_2311110060; // mengganti nama 'simpul' menjadi 'Yoka_2311110060'
vector<vector<int>> busur;
unordered_map<string, int> kotaIndex;

// Fungsi untuk mengisi nama-nama kota ke dalam vektor Yoka_2311110060 dan membuat mapping indeks kota
void isiYoka_2311110060(int jumlahSimpul) {
    string namaKota;
    cout << "Masukkan nama-nama kota:" << endl;
    cin.ignore(); // untuk mengabaikan karakter newline dari input sebelumnya
    for (int i = 0; i < jumlahSimpul; i++) {
        cout << "Nama kota " << i + 1 << ": ";
        getline(cin, namaKota);
        Yoka_2311110060.push_back(namaKota);
        kotaIndex[namaKota] = i; // simpan indeks kota
    }
    busur.resize(jumlahSimpul, vector<int>(jumlahSimpul, 0));
}

void isiBusur() {
    int jarak;
    cout << "Masukkan jarak antar kota (0 jika tidak ada jalur langsung):" << endl;
    for (size_t i = 0; i < Yoka_2311110060.size(); i++) {
        for (size_t j = 0; j < Yoka_2311110060.size(); j++) {
            if (i != j) {
                cout << "Jarak dari " << Yoka_2311110060[i] << " ke " << Yoka_2311110060[j] << ": ";
                cin >> jarak;
                busur[i][j] = jarak;
            }
        }
    }
}

void tampilGraph() {
    cout << left << setw(12) << "Kota Asal" << " | ";
    for (const auto& kota : Yoka_2311110060) {
        cout << setw(10) << kota << " | ";
    }
    cout << endl;

    for (size_t i = 0; i < Yoka_2311110060.size(); i++) {
        cout << left << setw(12) << Yoka_2311110060[i] << " | ";
        for (size_t j = 0; j < Yoka_2311110060.size(); j++) {
            cout << setw(10) << busur[i][j] << " | ";
        }
        cout << endl;
    }
}

// Fungsi untuk menghitung total jarak perjalanan berdasarkan rute kota yang dipilih
int hitungJarak(const vector<string>& perjalanan) {
    int totalJarak = 0;
    for (size_t i = 0; i < perjalanan.size() - 1; i++) {
        int asal = kotaIndex[perjalanan[i]];
        int tujuan = kotaIndex[perjalanan[i + 1]];
        totalJarak += busur[asal][tujuan];
    }
    return totalJarak;
}

int main() {
    int jumlahSimpul;
    cout << "Masukkan jumlah kota: ";
    cin >> jumlahSimpul;

    isiYoka_2311110060(jumlahSimpul);
    isiBusur();
    tampilGraph();

    int jumlahPerjalanan;
    cout << "Masukkan jumlah kota dalam perjalanan: ";
    cin >> jumlahPerjalanan;
    vector<string> perjalanan(jumlahPerjalanan);
    cout << "Masukkan nama-nama kota dalam perjalanan:" << endl;
    for (int i = 0; i < jumlahPerjalanan; i++) {
        cout << "Kota " << i + 1 << ": ";
        cin >> perjalanan[i];
    }

    int jarakTotal = hitungJarak(perjalanan);
    cout << "Jarak total perjalanan: ";
    for (const auto& kota : perjalanan) {
        cout << kota << " ";
    }
    cout << "adalah " << jarakTotal << " km" << endl;

    return 0;
}
```
## Output:
![Screenshot 2024-06-12 000333](https://github.com/yokaroo/Praktikum-Struktur-Data-Asignment-Modul10/blob/main/Screenshot%202024-06-12%20000333.png)
## Interpretasi:
Kode di atas adalah program C++ yang mengelola dan menghitung jarak perjalanan antar kota menggunakan graf. Program ini menggunakan `iostream`, `iomanip`, `vector`, `string`, dan `unordered_map`.

Pertama, nama-nama kota disimpan dalam vektor `Yoka_2311110060`, dan jarak antar kota disimpan dalam matriks `busur`. Mapping antara nama kota dan indeksnya disimpan dalam `kotaIndex`.

Fungsi `isiYoka_2311110060` meminta pengguna memasukkan nama-nama kota dan mengisi vektor serta mapping indeks kota. Fungsi `isiBusur` meminta pengguna memasukkan jarak antar kota untuk mengisi matriks `busur`. Fungsi `tampilGraph` menampilkan graf kota dalam bentuk tabel dengan jarak antar kota.

Fungsi `hitungJarak` menghitung total jarak perjalanan berdasarkan rute yang diberikan pengguna, dengan menjumlahkan jarak antar kota dalam rute.

Dalam fungsi `main`, program meminta pengguna memasukkan jumlah kota, nama-nama kota, dan jarak antar kota. Program kemudian menampilkan graf, meminta rute perjalanan, dan menghitung serta menampilkan total jarak perjalanan.

Secara keseluruhan, program ini memungkinkan pengguna untuk menginput data graf kota, menampilkan graf, dan menghitung jarak perjalanan berdasarkan rute yang dipilih.
## 2. Modifikasi guided tree diatas dengan program menu menggunakan input data tree dari user dan tampilkan pada pre-order, inorder, dan post order!
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

// Fungsi untuk membaca pohon dalam pre-order
void preOrder(pohon* node) {
    if (node != NULL) {
        cout << node->data << " ";
        preOrder(node->kiri);
        preOrder(node->kanan);
    }
}

// Fungsi untuk membaca pohon dalam in-order
void inOrder(pohon* node) {
    if (node != NULL) {
        inOrder(node->kiri);
        cout << node->data << " ";
        inOrder(node->kanan);
    }
}

// Fungsi untuk membaca pohon dalam post-order
void postOrder(pohon* node) {
    if (node != NULL) {
        postOrder(node->kiri);
        postOrder(node->kanan);
        cout << node->data << " ";
    }
}

// Fungsi untuk membaca pohon secara level-order
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

// Fungsi untuk menampilkan menu
void menu() {
    int pilihan;
    do {
        cout << "Menu:" << endl;
        cout << "1. Inisialisasi Root" << endl;
        cout << "2. Tambah Simpul" << endl;
        cout << "3. Tampilkan Pre-Order" << endl;
        cout << "4. Tampilkan In-Order" << endl;
        cout << "5. Tampilkan Post-Order" << endl;
        cout << "6. Tampilkan Level-Order" << endl;
        cout << "0. Keluar" << endl;
        cout << "Masukkan pilihan: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                inisialisasi();
                simpulAkar();
                break;
            case 2:
                tambahSimpul();
                break;
            case 3:
                cout << "Pre-Order: ";
                preOrder(root);
                cout << endl;
                break;
            case 4:
                cout << "In-Order: ";
                inOrder(root);
                cout << endl;
                break;
            case 5:
                cout << "Post-Order: ";
                postOrder(root);
                cout << endl;
                break;
            case 6:
                bacaPohon();
                break;
            case 0:
                cout << "Keluar dari program." << endl;
                break;
            default:
                cout << "Pilihan tidak valid." << endl;
                break;
        }
    } while (pilihan != 0);
}

// Fungsi utama
int main() {
    menu();
    return 0;
}
```
## OUtput:
![Screenshot 2024-06-12 002931](https://github.com/yokaroo/Praktikum-Struktur-Data-Asignment-Modul10/blob/main/Screenshot%202024-06-12%20002931.png)

## Interpretasi:
Program ini adalah implementasi struktur data pohon biner dengan beberapa fungsi untuk manipulasi dan traversal pohon. Berikut adalah penjelasan tentang program tersebut dalam bentuk paragraf:

Program dimulai dengan mendefinisikan struktur pohon biner yang memiliki tiga elemen: penunjuk ke anak kiri, data dalam bentuk karakter, dan penunjuk ke anak kanan. Ada beberapa variabel global yang digunakan, termasuk penunjuk ke simpul, root, simpul saat ini, dan array alamat untuk menyimpan penunjuk ke simpul dalam pohon. Fungsi `inisialisasi` digunakan untuk mengatur root menjadi NULL. Fungsi `simpulBaru` digunakan untuk membuat simpul baru dengan data yang diberikan dan mengatur penunjuk kiri dan kanan menjadi NULL. Fungsi `simpulAkar` menginisialisasi root jika belum ada, dan meminta pengguna untuk memasukkan data untuk simpul root. Fungsi `tambahSimpul` digunakan untuk menambah simpul baru ke dalam pohon berdasarkan input dari pengguna. 

Program juga memiliki fungsi untuk melakukan traversal pohon: `preOrder`, `inOrder`, dan `postOrder`, yang masing-masing digunakan untuk traversal pre-order, in-order, dan post-order. Selain itu, ada fungsi `bacaPohon` yang membaca dan menampilkan pohon secara level-order. Semua fungsi ini diakses melalui menu interaktif dalam fungsi `menu`, yang memungkinkan pengguna untuk memilih tindakan seperti menginisialisasi root, menambah simpul, dan menampilkan pohon dalam berbagai urutan traversal. Fungsi `main` hanya memanggil fungsi `menu` untuk memulai interaksi dengan pengguna. Program ini memberikan antarmuka yang sederhana dan mudah digunakan untuk manipulasi pohon biner dan menampilkan hasil traversal pohon berdasarkan pilihan pengguna.
### KESIMPULAN
Kesimpulannya, program ini adalah implementasi pohon biner yang lengkap dengan fitur inisialisasi, penambahan simpul, dan berbagai metode traversal (pre-order, in-order, post-order, dan level-order). Program ini menggunakan struktur data pohon biner untuk menyimpan data dan menyediakan menu interaktif yang memungkinkan pengguna untuk berinteraksi dengan pohon tersebut, termasuk menambahkan simpul baru dan menampilkan pohon dalam berbagai urutan. Dengan fungsi-fungsi ini, program ini memberikan cara yang efisien dan terstruktur untuk memanipulasi dan menavigasi data dalam bentuk pohon biner.
