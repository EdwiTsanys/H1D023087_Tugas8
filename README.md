# Biodata
Nama    : M Edwi Tsanystya Raihan
NIM     : H1D023087
Shift   : A -> F

---

# Aplikasi Toko Kita

Aplikasi Flutter untuk manajemen produk toko dengan fitur login, registrasi, dan CRUD operasi pada produk.

## Struktur Proyek

```
lib/
├── main.dart                 # Entry point aplikasi
├── model/
│   └── produk.dart          # Model data Produk
└── ui/
    ├── login_page.dart      # Halaman Login
    ├── registrasi_page.dart # Halaman Registrasi
    ├── produk_page.dart     # Halaman List Produk
    ├── produk_form.dart     # Halaman Form Tambah/Edit Produk
    └── produk_detail.dart   # Halaman Detail Produk
```

## Penjelasan Kode Setiap Halaman

### 1. main.dart - Entry Point Aplikasi
**Fungsi**: Merupakan file utama yang mengatur konfigurasi aplikasi secara global.

**Kode Utama**:
```dart
void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      title: 'Toko Kita',
      debugShowCheckedModeBanner: false,
      home: LoginPage(),  // Halaman pertama yang ditampilkan
    );
  }
}
```

**Penjelasan**:
- `main()`: Fungsi entry point yang menjalankan aplikasi
- `MyApp`: Root widget aplikasi dengan MaterialApp
- `home: LoginPage()`: Set halaman pertama ke LoginPage (best practice untuk autentikasi)
- `debugShowCheckedModeBanner: false`: Menghilangkan banner debug di kanan atas

---

### 2. model/produk.dart - Model Data
**Fungsi**: Mendefinisikan struktur data untuk Produk.

**Kode**:
```dart
class Produk {
  String? id;
  String? kodeProduk;
  String? namaProduk;
  int? hargaProduk;

  Produk({
    this.id,
    this.kodeProduk,
    this.namaProduk,
    this.hargaProduk,
  });
}
```

**Penjelasan**:
- `id`: ID unik produk (nullable)
- `kodeProduk`: Kode produk untuk identifikasi
- `namaProduk`: Nama/deskripsi produk
- `hargaProduk`: Harga produk dalam format integer
- Constructor: Memungkinkan inisialisasi objek dengan parameter named

---

### 3. ui/login_page.dart - Halaman Login
**Fungsi**: Memvalidasi kredensial pengguna sebelum masuk ke aplikasi.

**Komponen Utama**:
- **AppBar**: Menampilkan judul "Login - Edwi"
- **TextFormField untuk Email**: Input dengan validator email kosong
- **TextFormField untuk Password**: Input password dengan obscureText (disembunyikan)
- **ElevatedButton Login**: Tombol untuk submit login
- **InkWell Registrasi**: Link navigasi ke halaman registrasi

**Fitur Validasi**:
```dart
validator: (value) {
  if (value!.isEmpty) {
    return 'Email harus diisi';
  }
  return null;
}
```

**Navigasi**:
- Login berhasil → `ProdukPage` (menggunakan `pushReplacement`)
- Link Registrasi → `RegistrasiPage` (menggunakan `push`)

**Styling**:
- OutlineInputBorder untuk TextFormField
- Icon prefixIcon untuk visual appeal
- Full-width button dengan padding vertikal

---

### 4. ui/registrasi_page.dart - Halaman Registrasi
**Fungsi**: Membuat akun pengguna baru dengan validasi lengkap.

**Input Field**:
1. **Nama** - Minimal 3 karakter
2. **Email** - Validasi format email dengan regex
3. **Password** - Minimal 6 karakter
4. **Konfirmasi Password** - Harus sama dengan password

**Validasi Email**:
```dart
Pattern pattern = r'^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$';
RegExp regex = RegExp(pattern.toString());
if (!regex.hasMatch(value)) {
  return "Email tidak valid";
}
```

**Validasi Password Match**:
```dart
if (value != _passwordTextboxController.text) {
  return "Konfirmasi Password tidak sama";
}
```

**Navigasi**:
- Registrasi berhasil → `LoginPage` (menggunakan `pushReplacement`)
- Link Login → `LoginPage` (menggunakan `push`)

**Styling**: Sama dengan login_page, konsisten dan user-friendly

---

### 5. ui/produk_page.dart - Halaman List Produk
**Fungsi**: Menampilkan daftar semua produk dan navigasi ke halaman lainnya.

**Struktur UI**:
```dart
AppBar(
  title: const Text('List Produk - Edwi'),
  actions: [
    GestureDetector(
      child: const Icon(Icons.add, size: 26.0),
      onTap: () => Navigator.push(...ProdukForm()...)
    ),
  ],
)
```

**Drawer Menu**:
- DrawerHeader dengan warna biru
- ListTile "Home" untuk refresh halaman
- ListTile "Logout" untuk kembali ke LoginPage

**ItemProduk Widget** (Custom Widget):
```dart
class ItemProduk extends StatelessWidget {
  final Produk produk;
  
  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () => Navigator.push(...ProdukDetail...),
      child: Card(
        margin: const EdgeInsets.all(8),
        elevation: 3,
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(10),
        ),
        child: ListTile(
          leading: const Icon(Icons.shopping_cart, color: Colors.blue),
          title: Text(produk.namaProduk!),
          subtitle: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Text("Kode: ${produk.kodeProduk}"),
              Text("Harga: Rp. ${produk.hargaProduk}"),
            ],
          ),
          trailing: const Icon(Icons.arrow_forward, color: Colors.grey),
        ),
      ),
    );
  }
}
```

**Fitur**:
- List 3 produk dummy sebagai contoh
- Setiap item dapat diklik untuk melihat detail
- Tombol "+" di AppBar untuk menambah produk baru
- Drawer untuk logout

---

### 6. ui/produk_form.dart - Halaman Form Produk
**Fungsi**: Form untuk menambah produk baru atau mengubah produk yang ada.

**Mode Operasi**:
```dart
void isUpdate() {
  if (widget.produk != null) {
    judul = "UBAH PRODUK";
    tombolSubmit = "UBAH";
    // Isi TextFormField dengan data produk
  } else {
    judul = "TAMBAH PRODUK";
    tombolSubmit = "SIMPAN";
  }
}
```

**Input Fields**:
1. **Kode Produk** - TextFormField dengan validator
2. **Nama Produk** - TextFormField dengan validator
3. **Harga** - TextFormField dengan keyboardType number

**Validasi**:
```dart
validator: (value) {
  if (value!.isEmpty) {
    return "Field harus diisi";
  }
  return null;
}
```

**Tombol Submit**:
- Melakukan validasi form terlebih dahulu
- Jika valid, tampilkan SnackBar feedback
- TODO: Implementasi save/update ke database

**Styling**:
- OutlineInputBorder pada semua TextFormField
- Icon khusus untuk setiap field (code, shopping_cart, attach_money)
- Full-width ElevatedButton dengan padding

---

### 7. ui/produk_detail.dart - Halaman Detail Produk
**Fungsi**: Menampilkan detail lengkap produk dengan opsi edit dan delete.

**Tampilan Detail**:
```dart
Card(
  elevation: 4,
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
  child: Padding(
    padding: const EdgeInsets.all(20.0),
    child: Column(
      children: [
        _detailRow("Kode Produk", widget.produk!.kodeProduk!),
        _detailRow("Nama Produk", widget.produk!.namaProduk!),
        _detailRow("Harga", "Rp. ${widget.produk!.hargaProduk}"),
      ],
    ),
  ),
)
```

**Method _detailRow**:
```dart
Widget _detailRow(String label, String value) {
  return Row(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: [
      Expanded(flex: 2, child: Text(label, style: TextStyle(fontWeight: FontWeight.bold))),
      const Text(": "),
      Expanded(flex: 3, child: Text(value)),
    ],
  );
}
```

**Tombol Aksi**:
- **Edit**: Navigasi ke `ProdukForm` dengan membawa data produk yang ada
- **Delete**: Menampilkan dialog konfirmasi sebelum hapus

**Dialog Konfirmasi Hapus**:
```dart
void confirmHapus() {
  AlertDialog alertDialog = AlertDialog(
    title: const Text("Konfirmasi Hapus"),
    content: const Text("Yakin ingin menghapus data ini?"),
    actions: [
      TextButton(child: const Text("Batal"), onPressed: () => Navigator.pop(context)),
      TextButton(
        child: const Text("Hapus"),
        onPressed: () {
          // TODO: Hapus dari database
          Navigator.of(context).pop();
          Navigator.of(context).pushReplacement(...ProdukPage...);
        },
      ),
    ],
  );
  showDialog(context: context, builder: (context) => alertDialog);
}
```

**SnackBar Feedback**:
```dart
ScaffoldMessenger.of(context).showSnackBar(
  const SnackBar(
    content: Text('Produk berhasil dihapus!'),
    duration: Duration(seconds: 2),
  ),
);
```

---

## Alur Navigasi Aplikasi

```
LoginPage
    ↓ (Login berhasil)
    ↓
ProdukPage (List Produk) ←→ ProdukForm (Tambah/Edit)
    ↓
ProdukDetail ←→ ProdukForm (Edit)
    ↓
Konfirmasi Hapus → Kembali ke ProdukPage

LoginPage ← Logout (dari Drawer)
LoginPage ← Registrasi Link
```

## Dependencies

- `flutter`: SDK Flutter
- Material Design untuk UI components

## Catatan Implementasi

- ✅ Semua halaman sudah memiliki validasi form
- ✅ Navigasi antar halaman sudah terintegrasi
- ✅ Styling UI konsisten dan responsive
- ✅ Nama panggilan "Edwi" ditambahkan pada setiap AppBar
- ⏳ TODO: Integrasi database/API untuk operasi CRUD
- ⏳ TODO: Implementasi autentikasi real
- ⏳ TODO: Error handling yang lebih komprehensif

## Hasil SS

<img width="614" height="872" alt="Image" src="https://github.com/user-attachments/assets/2897e83d-9ced-43e1-869e-8d2b9fb193d9" />
<img width="620" height="872" alt="Image" src="https://github.com/user-attachments/assets/440dcc7c-fdd4-4805-a45c-a29a132c0037" />
<img width="615" height="870" alt="Image" src="https://github.com/user-attachments/assets/b2dfa123-53a4-4882-ac76-cd28f702c444" />
<img width="614" height="874" alt="Image" src="https://github.com/user-attachments/assets/882cdfaa-0cd8-4535-a084-3b0115b77a00" />
<img width="613" height="874" alt="Image" src="https://github.com/user-attachments/assets/d53838e4-a49c-442c-a5c9-eeb452fdefe3" />
<img width="617" height="873" alt="Image" src="https://github.com/user-attachments/assets/1032c38d-c94c-4ef8-9dcc-1b310c81f65a" />
<img width="619" height="878" alt="Image" src="https://github.com/user-attachments/assets/80ca6af8-ffd9-477f-a098-c2c5986079dc" />
<img width="610" height="872" alt="Image" src="https://github.com/user-attachments/assets/51d815a6-bb00-40dd-a28b-a2ebd2d69c8d" />
