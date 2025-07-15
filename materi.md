# Penjelasan Sistem Manajemen Toko Buku Versi 1 (Array)

Sistem Manajemen Toko Buku versi 1 menggunakan **array statis** untuk menyimpan data buku.  
Setiap data buku disimpan dalam elemen array bertipe `Buku`, dan jumlah maksimal data ditentukan oleh konstanta `MAKS_BUKU`.  
Program menyediakan fitur tambah, tampilkan, ubah, hapus, cari, dan urutkan buku melalui menu interaktif di konsol.

---

## 🔍 Highlight dan Penjelasan Kode

### 📚 Library yang Digunakan

```cpp
#include <iostream>
#include <iomanip>
#include <cstring>
using namespace std;
