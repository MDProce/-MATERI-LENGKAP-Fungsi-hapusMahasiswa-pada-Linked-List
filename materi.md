# 📘 Sistem Manajemen Data Mahasiswa (C++ Linked List)

Sistem ini dibuat menggunakan bahasa C++ dengan struktur data **linked list** untuk mengelola data mahasiswa secara dinamis.  
Setiap mahasiswa memiliki atribut: `nama`, `NIM`, dan `IPK`.  
Program menyediakan fitur tambah data, tampilkan, hapus, cari, dan urutkan, semua dijalankan melalui antarmuka teks di terminal.

---

## 🔍 Tujuan Program

Mengelola data mahasiswa tanpa batasan jumlah tetap, menggunakan memori dinamis.  
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
🎯 Tujuan
Menghapus satu data mahasiswa dari linked list berdasarkan nama atau NIM yang dicari user.

📌 1. Mengecek apakah list kosong
cpp
Copy
Edit
if (head == nullptr)
Jika head kosong, berarti belum ada data sama sekali.
Dalam kondisi ini, proses penghapusan gak bisa dilakukan.
Program akan tampilkan pesan dan keluar dari fungsi.

💡 Kenapa penting?
Kalau list kosong tapi kita lanjut, pointer bisa akses memori kosong → error (crash).

📌 2. Input keyword dari user
cpp
Copy
Edit
cin.ignore();
getline(cin, keyword);
cin.ignore(); membuang karakter newline dari input sebelumnya.

getline() membaca input lengkap termasuk spasi (misalnya nama lengkap).

💡 Kenapa gak pakai cin >>?
Karena cin >> cuma baca satu kata. Nama kayak Budi Santoso bakal kepecah jadi Budi doang.

📌 3. Inisialisasi pointer & flag
cpp
Copy
Edit
Node* hapus = head;
Node* sebelum = nullptr;
bool ditemukan = false;
hapus: mulai dari head, untuk menelusuri node.

sebelum: menyimpan node sebelumnya, untuk proses sambung ulang.

ditemukan: flag penanda apakah data yang dicari ketemu atau enggak.

📌 4. Cek kecocokan data
cpp
Copy
Edit
bool cocok = (pilihan == 1 && hapus->data.nama == keyword) ||
             (pilihan == 2 && hapus->data.nim == keyword);
Pilihan 1 → cocokkan dengan nama

Pilihan 2 → cocokkan dengan nim

💡 Tujuannya: supaya satu kondisi bisa handle dua jenis pencarian

📌 5. Proses penghapusan node
cpp
Copy
Edit
if (sebelum == nullptr)
    head = hapus->next;
else
    sebelum->next = hapus->next;
Jika sebelum == nullptr, berarti node yang dihapus adalah node pertama (head)

Kalau tidak, berarti node dihapus dari tengah/akhir. Kita sambungkan node sebelumnya ke node setelahnya.

💬 Analogi:
Bayangin barisan orang. Kalau lo nyabut orang tengah, orang di depannya langsung salaman sama yang di belakang.

📌 6. Menghapus node dari memori
cpp
Copy
Edit
delete hapus;
Setelah dilepas dari rantai, node dihapus dari memori agar tidak terjadi memory leak.

📌 7. Jika tidak ditemukan
cpp
Copy
Edit
if (!ditemukan)
    cout << "Data tidak ditemukan";
Menampilkan pesan kalau data gak ditemukan di dalam list.

✅ Kesimpulan Fungsi
Fungsi ini memperlihatkan:

Traversal node menggunakan pointer

Pengecekan node head vs node tengah/akhir

Penanganan pointer sebelum dan hapus

Penghapusan aman dari memori dinamis