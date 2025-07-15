📘 MATERI LENGKAP: Fungsi hapusMahasiswa() pada Linked List
🧠 Apa itu Linked List?
Sebelum kita bahas fungsi hapusMahasiswa(), kita harus ngerti dulu struktur data yang dipakai: linked list.

Linked list adalah struktur data dinamis yang tersusun dari elemen-elemen yang disebut node. Setiap node menyimpan:

Data (dalam kasus ini: data mahasiswa seperti nama, NIM, IPK)

Pointer ke node berikutnya (next)

Contoh visual:

css
Copy
Edit
[Andi | o-] → [Budi | o-] → [Citra | NULL]
Andi, Budi, Citra adalah node.

Setiap node tahu siapa node berikutnya melalui pointer next.

🎯 Tujuan Fungsi hapusMahasiswa()
Fungsi ini digunakan untuk menghapus satu data mahasiswa dari linked list.
Yang bisa dihapus adalah node yang sesuai dengan keyword pencarian,
dan keyword itu bisa berupa nama atau NIM, sesuai dengan pilihan user.

⚙️ Langkah Kerja Fungsi hapusMahasiswa()
Mari kita bahas langkah demi langkah:

🔹 1. Mengecek apakah list kosong
cpp
Copy
Edit
if (head == nullptr)
head adalah pointer ke node pertama dalam linked list.

Kalau head == nullptr, berarti tidak ada node dalam list.

Artinya: tidak ada data yang bisa dihapus, jadi program langsung keluar dari fungsi.

📌 Kenapa ini penting?
Kalau kita lanjut tanpa ngecek ini, program bisa crash karena kita akses data yang gak ada.

🔹 2. Input keyword dari user
cpp
Copy
Edit
cin.ignore();
getline(cin, keyword);
cin.ignore(); digunakan supaya input sebelumnya (misalnya dari cin >> pilihan) tidak mengganggu input getline di bawahnya.

getline(cin, keyword); digunakan untuk mengambil input berupa string penuh dari user — contohnya "Budi Santoso".

📌 Kenapa pakai getline?
Karena cin >> hanya membaca satu kata. Kalau nama mahasiswanya ada spasi, maka kita butuh getline.

🔹 3. Inisialisasi pointer
cpp
Copy
Edit
Node *hapus = head;
Node *sebelum = nullptr;
bool ditemukan = false;
Penjelasan:

hapus: pointer yang digunakan untuk menelusuri node satu per satu. Di-set ke head, artinya mulai dari node pertama.

sebelum: pointer yang menyimpan node sebelum node yang sedang dicek. Awalnya nullptr, karena node pertama tidak punya "sebelum".

ditemukan: variabel boolean yang menandakan apakah data yang cocok berhasil ditemukan atau tidak.

📌 Kenapa butuh sebelum?
Karena kalau kita mau hapus node di tengah, kita harus bisa menyambung node sebelumnya ke node sesudahnya.

🔹 4. Menentukan kecocokan data
cpp
Copy
Edit
bool cocok = (pilihan == 1 && hapus->data.nama == keyword) ||
             (pilihan == 2 && hapus->data.nim == keyword);
Penjelasan:

Program akan membandingkan keyword yang diinput user dengan isi data dari node yang sedang dicek (hapus).

Kalau user memilih pilihan 1, maka yang dibandingkan adalah nama.

Kalau memilih pilihan 2, maka dibandingkan nim.

📌 Kalau cocok == true, maka node ini akan dihapus.

🔹 5. Proses penghapusan node
cpp
Copy
Edit
if (sebelum == nullptr)
    head = hapus->next;
else
    sebelum->next = hapus->next;
Penjelasan:

Jika sebelum == nullptr, artinya node yang mau dihapus adalah node pertama.
Maka kita cukup geser head ke hapus->next, alias lompatin node pertama.

Kalau sebelum != nullptr, artinya node yang mau dihapus bukan di depan, tapi di tengah atau akhir.
Maka kita hubungkan sebelum ke hapus->next, alias potong node yang mau dihapus dari rantai list-nya.