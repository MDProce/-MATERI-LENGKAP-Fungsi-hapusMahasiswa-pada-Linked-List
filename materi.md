# Materi Lengkap: Manipulasi Data Mahasiswa dengan Linked List di C++

## Pendahuluan

Struktur data linked list adalah salah satu struktur data yang sangat penting dalam pemrograman. Tidak seperti array yang ukurannya tetap, linked list bersifat dinamis dan memungkinkan penambahan atau penghapusan elemen secara efisien. Dalam materi ini, kita akan membahas bagaimana cara mengelola data mahasiswa menggunakan linked list di C++, dengan fokus pada dua operasi utama:

1. **Mengurutkan data mahasiswa** (berdasarkan nama atau IPK)
2. **Menghapus data mahasiswa** (berdasarkan nama atau NIM)

Tujuan dari materi ini adalah agar mahasiswa dan pembaca awam sekalipun bisa memahami bagaimana bekerja dengan linked list secara praktis dan logis.

---

## Struktur Data Dasar

Sebelum melakukan operasi, kita perlu mendefinisikan struktur data mahasiswa dan node linked list.

```cpp
struct DataMahasiswa {
    string nama;
    string nim;
    float ipk;
};

struct Node {
    DataMahasiswa data;
    Node* next;
};

Node* head = nullptr; // Penunjuk ke awal linked list
```

Setiap `Node` menyimpan satu data mahasiswa dan pointer ke node berikutnya. Pointer `head` menunjuk ke node pertama dalam list.

---

## Bagian 1: Mengurutkan Data Mahasiswa (Bubble Sort)

### Tujuan

Mengurutkan data mahasiswa dalam linked list berdasarkan:

* **Nama (A-Z)**
* **IPK (tinggi ke rendah)**

### Logika Bubble Sort

Algoritma **Bubble Sort** membandingkan dua data yang berurutan. Jika urutannya salah, maka datanya ditukar. Proses ini diulang terus-menerus hingga tidak ada data yang perlu ditukar lagi (artinya data sudah urut).

### Implementasi

```cpp
void urutkanMahasiswa() {
    if (head == nullptr || head->next == nullptr) {
        cout << "\nData kurang dari 2, tidak perlu diurutkan!" << endl;
        return;
    }

    int pilihan;
    cout << "\n== Urutkan berdasarkan: ==" << endl;
    cout << "1. Nama (A-Z)" << endl;
    cout << "2. IPK (Tinggi ke Rendah)" << endl;
    cout << "Pilih (1/2): ";
    cin >> pilihan;

    bool tukar;
    do {
        tukar = false;
        Node *a = head;
        while (a->next != nullptr) {
            Node *b = a->next;
            bool kondisi = false;

            if (pilihan == 1 && a->data.nama > b->data.nama)
                kondisi = true;
            if (pilihan == 2 && a->data.ipk < b->data.ipk)
                kondisi = true;

            if (kondisi) {
                swap(a->data, b->data); // Tukar isi data
                tukar = true;
            }
            a = a->next;
        }
    } while (tukar);

    cout << "\nData berhasil diurutkan!" << endl;
}
```

### Penjelasan

* `if (head == nullptr || head->next == nullptr)`: Mengecek jika data kosong atau hanya satu node.
* `do...while`: Melakukan perulangan hingga tidak ada data yang ditukar.
* `swap(a->data, b->data)`: Menukar isi data antar node, bukan node-nya.

### Contoh

Jika ada 3 mahasiswa:

* Budi (IPK 3.2)
* Andi (IPK 3.6)
* Cici (IPK 2.9)

Jika diurutkan berdasarkan nama, hasilnya:

* Andi, Budi, Cici

Jika berdasarkan IPK:

* Andi, Budi, Cici

---

## Bagian 2: Menghapus Data Mahasiswa

### Tujuan

Menghapus node dari linked list berdasarkan:

* **Nama** mahasiswa
* **NIM** mahasiswa

### Logika

1. Cek apakah linked list kosong.
2. Minta input keyword dari pengguna (nama atau NIM).
3. Telusuri setiap node:

   * Jika cocok dengan keyword, hapus node tersebut.
   * Jika node berada di tengah atau akhir, sambungkan node sebelumnya ke node sesudahnya.
   * Jika node adalah head, pindahkan head ke node berikutnya.

### Implementasi

```cpp
void hapusMahasiswa() {
    if (head == nullptr) {
        cout << "List masih kosong." << endl;
        return;
    }

    int pilihan;
    string keyword;
    cout << "Hapus berdasarkan: 1. Nama, 2. NIM\nPilih (1/2): ";
    cin >> pilihan;
    cin.ignore();
    cout << "Masukkan keyword: ";
    getline(cin, keyword);

    Node *hapus = head;
    Node *sebelum = nullptr;
    bool ditemukan = false;

    while (hapus != nullptr) {
        bool cocok = (pilihan == 1 && hapus->data.nama == keyword) ||
                     (pilihan == 2 && hapus->data.nim == keyword);

        if (cocok) {
            if (sebelum == nullptr)
                head = hapus->next;
            else
                sebelum->next = hapus->next;

            delete hapus;
            ditemukan = true;
            cout << "Data berhasil dihapus." << endl;
            break;
        }

        sebelum = hapus;
        hapus = hapus->next;
    }

    if (!ditemukan)
        cout << "Data tidak ditemukan." << endl;
}
```

### Penjelasan

* `hapus`: Menunjuk node yang sedang diperiksa.
* `sebelum`: Menunjuk node sebelum `hapus`, berguna saat menghapus node di tengah.
* Jika data ditemukan dan `sebelum == nullptr`, artinya node yang dihapus adalah head.
* `delete hapus`: Menghapus node dari memori.

---

## Penutup

Dengan mempelajari dua fungsi penting ini (pengurutan dan penghapusan), kita dapat memahami bagaimana bekerja dengan linked list secara praktis:

* Bubble Sort membantu kita menyusun data agar mudah dibaca.
* Penghapusan berdasarkan keyword membuat data tetap relevan dan bersih.

Pemahaman ini akan berguna untuk proyek-proyek lanjutan seperti sistem informasi mahasiswa, manajemen data, dan aplikasi CRUD.

---

## Latihan

1. Tambahkan fitur pencarian berdasarkan nama.
2. Modifikasi fungsi urut agar bisa mengurutkan dari Z ke A.
3. Tambahkan validasi input untuk mencegah kesalahan pengguna.

Selamat belajar dan semangat ngoding! 💻🔥
