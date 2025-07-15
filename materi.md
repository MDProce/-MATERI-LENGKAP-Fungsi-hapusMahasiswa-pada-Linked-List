# 📘 Sistem Manajemen Data Mahasiswa (C++ Linked List)

Sistem ini dibuat menggunakan bahasa C++ dengan struktur data **linked list** untuk mengelola data mahasiswa secara dinamis.  
Setiap mahasiswa memiliki atribut: `nama`, `NIM`, dan `IPK`.  
Program menyediakan fitur tambah data, tampilkan, hapus, cari, dan urutkan, semua dijalankan melalui antarmuka teks di terminal.

---

## 🔍 Tujuan Program

Mengelola data mahasiswa tanpa batasan jumlah tetap, menggunakan **memori dinamis**.  
Struktur linked list memungkinkan penambahan dan penghapusan data secara fleksibel, tanpa harus memindahkan atau menggeser elemen seperti pada array.

---

## 🧩 Struktur Data

Program menggunakan dua `struct` utama:

```cpp
struct Mahasiswa {
    string nama;
    string nim;
    float ipk;
};

struct Node {
    Mahasiswa data;
    Node* next;
};
Mahasiswa: menyimpan data satu mahasiswa.

Node: menyimpan satu data mahasiswa + pointer ke node selanjutnya.

head: pointer global untuk menunjuk node pertama di list.

✂️ Penjelasan Lengkap Fungsi hapusMahasiswa()
🎯 Tujuan:
Menghapus satu data mahasiswa dari linked list berdasarkan nama atau NIM yang dicari user.

📌 1. Mengecek apakah list kosong
cpp
Copy
Edit
if (head == nullptr)
Jika head kosong, berarti belum ada data sama sekali.

Dalam kondisi ini, proses penghapusan gak bisa dilakukan.

Program akan tampilkan pesan dan keluar dari fungsi.

Kenapa penting?
Kalau list kosong tapi kita lanjut, pointer bisa akses memori kosong → error (crash).

📌 2. Input keyword dari user
cpp
Copy
Edit
cin.ignore();
getline(cin, keyword);
cin.ignore(); buang newline character yang tertinggal dari input sebelumnya.

getline dipakai supaya bisa ambil input string yang panjang (misalnya nama lengkap dengan spasi).

Kenapa gak pakai cin >>?
Karena cin >> cuma baca satu kata. Nama panjang kayak "Budi Setiawan" bakal kepecah jadi "Budi" doang.

📌 3. Inisialisasi pointer & flag
cpp
Copy
Edit
Node* hapus = head;
Node* sebelum = nullptr;
bool ditemukan = false;
hapus: pointer untuk menelusuri list, mulai dari head.

sebelum: pointer ke node sebelumnya. Penting untuk sambung ulang list kalau node tengah dihapus.

ditemukan: flag penanda, default-nya false, akan jadi true kalau data ketemu.

📌 4. Cek kecocokan data
cpp
Copy
Edit
bool cocok = (pilihan == 1 && hapus->data.nama == keyword) ||
             (pilihan == 2 && hapus->data.nim == keyword);
Kalau user pilih 1, program cocokkan nama.

Kalau pilih 2, cocokkan NIM.

Kenapa dibuat seperti ini?
Supaya satu kondisi bisa handle dua jenis pencarian: berdasarkan nama atau nim.

📌 5. Proses penghapusan node
cpp
Copy
Edit
if (sebelum == nullptr)
    head = hapus->next;
else
    sebelum->next = hapus->next;
Kalau sebelum == nullptr, artinya node yang dihapus adalah node pertama (head).
Jadi kita cukup geser head ke node berikutnya.

Kalau sebelum != nullptr, berarti node dihapus dari tengah atau akhir.
Kita putus node itu dari chain, lalu sambungin node sebelumnya langsung ke node setelahnya.

Analogi:
Bayangin barisan orang. Kita mau cabut orang tengah. Kita suruh orang sebelumnya langsung sambung ke yang setelahnya.

📌 6. Menghapus node dari memori
cpp
Copy
Edit
delete hapus;
Setelah node dilepas dari chain, kita hapus dari memori agar gak terjadi memory leak.

📌 7. Jika tidak ditemukan
cpp
Copy
Edit
if (!ditemukan)
    cout << "Data tidak ditemukan";
Kalau gak ada node yang cocok dengan keyword, user dikasih pesan bahwa datanya tidak ditemukan.

