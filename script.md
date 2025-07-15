# Program Linked List Mahasiswa (C++)

## 📚 Deskripsi
Program ini menggunakan struktur data **linked list** untuk menyimpan data mahasiswa. Program mendukung fitur:
- Mengurutkan data berdasarkan **Nama (A-Z)** atau **IPK (Tinggi ke Rendah)** menggunakan **Bubble Sort**.
- Menghapus data mahasiswa berdasarkan **Nama** atau **NIM**.

---

## 🔁 Sorting (Bubble Sort)

### Fungsi:
Mengurutkan data mahasiswa berdasarkan:
- Nama (A-Z)
- IPK (Tinggi ke Rendah)

### Logika:
1. Cek apakah data kurang dari 2:
   ```cpp
   if (head == nullptr || head->next == nullptr)
       return;
Lakukan perulangan selama masih ada data yang ditukar (tukar = true):

Bandingkan dua node berurutan (a dan b).

Jika perlu ditukar, lakukan swap terhadap isi datanya (bukan node-nya).

Jika tidak ada data yang ditukar dalam 1 iterasi, berarti data sudah urut.

Contoh Kode:
cpp
Copy
Edit
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
                swap(a->data, b->data); // Tukar isi data, bukan node
                tukar = true;
            }
            a = a->next;
        }
    } while (tukar);

    cout << "\nData berhasil diurutkan!" << endl;
}
❌ Penghapusan Data Mahasiswa
Fungsi:
Menghapus data dari linked list berdasarkan:

Nama

NIM

Langkah-langkah:
Cek apakah list kosong:

cpp
Copy
Edit
if (head == nullptr) return;
Minta input keyword (nama/NIM).

Telusuri node satu per satu, cocokkan dengan keyword.

Jika cocok:

Jika node dihapus adalah head, ubah head ke node berikutnya.

Jika di tengah, sambungkan node sebelumnya ke node setelahnya.

Hapus node secara permanen dengan delete.

Contoh Kode:
cpp
Copy
Edit
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
📌 Catatan
Pastikan struktur Node dan DataMahasiswa telah didefinisikan dengan atribut nama, nim, dan ipk.

Fungsi swap(a->data, b->data) hanya menukar isi data antar node, bukan node-nya.

🛠 Struktur Data yang Digunakan
cpp
Copy
Edit
struct DataMahasiswa {
    string nama;
    string nim;
    float ipk;
};

struct Node {
    DataMahasiswa data;
    Node* next;
};