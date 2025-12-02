## 📋 Biodata Pengembang

| Informasi | Detail |
|-----------|--------|
| **Nama** | M Edwi Tsanystya Raihan |
| **NIM** | H1D023087 |
| **Shift** | A → F |
| **Mata Kuliah** | Pemrograman Mobile (Praktikum) |
| **Institusi** | Universitas Jenderal Soedirman |

---

## 🚀 Tentang Aplikasi

**Toko Kita** adalah aplikasi Flutter yang dirancang untuk memudahkan pengelolaan produk toko secara mobile. Aplikasi ini menyediakan fitur lengkap mulai dari autentikasi pengguna, pendaftaran akun, hingga operasi CRUD (Create, Read, Update, Delete) untuk manajemen produk.

### ✨ Fitur Utama:
- ✅ **Sistem Login** - Autentikasi pengguna dengan validasi email & password
- ✅ **Registrasi Akun** - Pendaftaran pengguna baru dengan validasi lengkap
- ✅ **Daftar Produk** - Menampilkan semua produk dalam format list yang menarik
- ✅ **Detail Produk** - Melihat informasi lengkap setiap produk
- ✅ **Tambah Produk** - Menambahkan produk baru ke sistem
- ✅ **Edit Produk** - Mengubah data produk yang sudah ada
- ✅ **Hapus Produk** - Menghapus produk dengan konfirmasi
- ✅ **Logout** - Keluar dari akun dengan aman

---

## 📱 Halaman-Halaman UI

### 1️⃣ **Halaman Login (Login Page)**

<details>
<summary><b><img width="611" height="812" alt="Image" src="https://github.com/user-attachments/assets/f84e1318-ad8f-4ee0-962d-da36d8f4f7a0" />
<img width="610" height="808" alt="Image" src="https://github.com/user-attachments/assets/bf646d4e-a66f-4afd-a998-df8e59bc01cb" /></b></summary>

#### Komponen UI:
- **AppBar** dengan judul "Login"
- **Text Field Email** - Input untuk email pengguna
- **Text Field Password** - Input untuk password (tersembunyi dengan asterisk)
- **Tombol Login** - Untuk melakukan proses autentikasi
- **Link Registrasi** - Navigasi ke halaman registrasi akun baru

#### Fitur Validasi:
```dart
// Validasi Email
validator: (value) {
  if (value!.isEmpty) {
    return 'Email harus diisi';
  }
  return null;
}

// Validasi Password
validator: (value) {
  if (value!.isEmpty) {
    return "Password harus diisi";
  }
  return null;
}
```

#### Navigasi:
- ✅ Login berhasil → ke halaman **Produk Page**
- ✅ Klik registrasi → ke halaman **Registrasi Page**

</details>

---

### 2️⃣ **Halaman Registrasi (Registrasi Page)**

<details>
<summary><b><img width="611" height="812" alt="Image" src="https://github.com/user-attachments/assets/a649f713-52c1-47d2-be34-25da824b37b2" />
<img width="622" height="811" alt="Image" src="https://github.com/user-attachments/assets/1889b6ac-c010-4a25-ab5e-2ddc4b4acbf6" /></b></summary>

#### Komponen UI:
- **AppBar** dengan judul "Registrasi"
- **Text Field Nama** - Input nama lengkap (minimal 3 karakter)
- **Text Field Email** - Input email dengan validasi format
- **Text Field Password** - Input password (minimal 6 karakter)
- **Text Field Konfirmasi Password** - Harus sama dengan password
- **Tombol Registrasi** - Untuk membuat akun baru
- **Link Login** - Navigasi kembali ke halaman login

#### Fitur Validasi:
```dart
// Validasi Nama (minimal 3 karakter)
validator: (value) {
  if (value!.isEmpty) {
    return 'Nama harus diisi';
  }
  if (value.length < 3) {
    return 'Nama minimal 3 karakter';
  }
  return null;
}

// Validasi Email (format email valid)
Pattern pattern = r'^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|'
    r'(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|'
    r'(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$';
RegExp regex = RegExp(pattern.toString());
if (!regex.hasMatch(value)) {
  return "Email tidak valid";
}

// Validasi Password (minimal 6 karakter)
validator: (value) {
  if (value!.isEmpty) {
    return 'Password harus diisi';
  }
  if (value.length < 6) {
    return 'Password minimal 6 karakter';
  }
  return null;
}

// Validasi Konfirmasi Password (harus sama)
validator: (value) {
  if (value != _passwordTextboxController.text) {
    return "Konfirmasi Password tidak sama";
  }
  return null;
}
```

#### Navigasi:
- ✅ Registrasi berhasil → ke halaman **Login Page**
- ✅ Klik login → ke halaman **Login Page**

</details>

---

### 3️⃣ **Halaman Daftar Produk (Produk Page)**

<details>
<summary><b><img width="618" height="813" alt="Image" src="https://github.com/user-attachments/assets/d4861180-79cf-43af-a454-ebcf8bca85b8" /></b></summary>

#### Komponen UI:
- **AppBar** dengan judul "List Produk"
- **Icon Tambah (+)** di kanan AppBar untuk menambah produk baru
- **ListView** dengan card item produk
- **Drawer Menu** untuk navigasi

#### Item Produk Card:
```dart
Card(
  elevation: 3,
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
  child: ListTile(
    leading: Icon(Icons.shopping_cart, color: Colors.blue),
    title: Text(produk.namaProduk),      // Nama produk
    subtitle: Column(
      children: [
        Text("Kode: ${produk.kodeProduk}"),    // Kode produk
        Text("Harga: Rp. ${produk.hargaProduk}"), // Harga
      ],
    ),
    trailing: Icon(Icons.arrow_forward, color: Colors.grey),
    onTap: () => Navigator.push(...ProdukDetail...), // Klik detail
  ),
)
```

#### Fitur Drawer Menu:
- **Home** - Refresh halaman daftar produk
- **Logout** - Keluar aplikasi (kembali ke Login Page)

#### Data Contoh (Dummy Data):
```dart
List<Produk> listProduk = [
  Produk(
    id: '1',
    kodeProduk: 'PRD001',
    namaProduk: 'Laptop Dell XPS 13',
    hargaProduk: 15000000,
  ),
  Produk(
    id: '2',
    kodeProduk: 'PRD002',
    namaProduk: 'Mouse Logitech MX Master',
    hargaProduk: 800000,
  ),
  Produk(
    id: '3',
    kodeProduk: 'PRD003',
    namaProduk: 'Keyboard Mechanical RGB',
    hargaProduk: 1200000,
  ),
];
```

#### Fitur Interaksi:
- ✅ Klik card produk → detail produk
- ✅ Klik icon (+) → tambah produk baru
- ✅ Buka drawer → menu logout
- ✅ Pull to refresh → reload data

#### Navigasi:
- ✅ Klik item → ke halaman **Produk Detail**
- ✅ Klik (+) → ke halaman **Produk Form** (tambah mode)
- ✅ Klik logout → ke halaman **Login Page**

</details>

---

### 4️⃣ **Halaman Form Produk (Produk Form)**

<details>
<summary><b><img width="617" height="812" alt="Image" src="https://github.com/user-attachments/assets/3a2a3ef3-95f0-422e-b64c-143ed63c4669" />
<img width="622" height="817" alt="Image" src="https://github.com/user-attachments/assets/63ae934f-99be-4b55-99e2-f4dd43e87acf" /></b></summary>

#### Komponen UI:
- **AppBar** dengan judul dinamis ("TAMBAH PRODUK" atau "UBAH PRODUK")
- **Text Field Kode Produk** - Input kode produk unik
- **Text Field Nama Produk** - Input nama/deskripsi produk
- **Text Field Harga** - Input harga dengan keyboard numeric
- **Tombol Submit** - "SIMPAN" (tambah) atau "UBAH" (edit)

#### Mode Operasi (Conditional Rendering):
```dart
void isUpdate() {
  if (widget.produk != null) {
    // MODE EDIT
    judul = "UBAH PRODUK";
    tombolSubmit = "UBAH";
    
    // Auto-fill field dengan data yang ada
    _kodeTextboxController.text = widget.produk!.kodeProduk!;
    _namaTextboxController.text = widget.produk!.namaProduk!;
    _hargaTextboxController.text = widget.produk!.hargaProduk.toString();
  } else {
    // MODE TAMBAH
    judul = "TAMBAH PRODUK";
    tombolSubmit = "SIMPAN";
  }
}
```

#### Input Fields & Validasi:
```dart
// Field 1: Kode Produk
TextFormField(
  decoration: InputDecoration(
    labelText: "Kode Produk",
    prefixIcon: Icon(Icons.code),
    border: OutlineInputBorder(),
  ),
  controller: _kodeTextboxController,
  validator: (value) {
    if (value!.isEmpty) {
      return "Kode produk harus diisi";
    }
    return null;
  },
)

// Field 2: Nama Produk
TextFormField(
  decoration: InputDecoration(
    labelText: "Nama Produk",
    prefixIcon: Icon(Icons.shopping_cart),
    border: OutlineInputBorder(),
  ),
  controller: _namaTextboxController,
  validator: (value) {
    if (value!.isEmpty) {
      return "Nama produk harus diisi";
    }
    return null;
  },
)

// Field 3: Harga Produk
TextFormField(
  decoration: InputDecoration(
    labelText: "Harga Produk",
    prefixIcon: Icon(Icons.attach_money),
    border: OutlineInputBorder(),
  ),
  keyboardType: TextInputType.number,
  controller: _hargaTextboxController,
  validator: (value) {
    if (value!.isEmpty) {
      return "Harga harus diisi";
    }
    return null;
  },
)
```

#### Proses Submit Form:
```dart
void _submit() {
  // 1. Validasi form
  var validate = _formKey.currentState!.validate();
  
  if (validate) {
    // 2. Siapkan data
    Produk produk = Produk(
      kodeProduk: _kodeTextboxController.text,
      namaProduk: _namaTextboxController.text,
      hargaProduk: int.parse(_hargaTextboxController.text),
    );
    
    // 3. Tampilkan feedback
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(content: Text('Produk berhasil disimpan!'))
    );
    
    // 4. Navigasi kembali
    Navigator.pop(context);
  }
}
```


#### Navigasi:
- ✅ Submit berhasil → kembali ke **Produk Page**
- ✅ Tombol back → kembali ke **Produk Page** tanpa simpan

</details>

---

### 5️⃣ **Halaman Detail Produk (Produk Detail)**

<details>
<summary><b><img width="618" height="810" alt="Image" src="https://github.com/user-attachments/assets/fd161de6-023d-4447-881a-a89c4cbecba1" /></b></summary>

#### Komponen UI:
- **AppBar** dengan judul "Detail Produk - Edwi"
- **Card Detail** menampilkan informasi produk
- **Tombol Edit** - Untuk mengubah produk
- **Tombol Hapus** - Untuk menghapus produk

#### Tampilan Detail Information:
```dart
Card(
  elevation: 4,
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
  child: Padding(
    padding: const EdgeInsets.all(20.0),
    child: Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        // Kode Produk
        _detailRow("Kode Produk", widget.produk!.kodeProduk!),
        Divider(),
        
        // Nama Produk
        _detailRow("Nama Produk", widget.produk!.namaProduk!),
        Divider(),
        
        // Harga Produk
        _detailRow("Harga", "Rp. ${widget.produk!.hargaProduk}"),
      ],
    ),
  ),
)

// Helper method untuk row detail
Widget _detailRow(String label, String value) {
  return Row(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: [
      Expanded(
        flex: 2,
        child: Text(
          label,
          style: TextStyle(fontWeight: FontWeight.bold, fontSize: 16),
        ),
      ),
      const Text(": ", style: TextStyle(fontSize: 16)),
      Expanded(
        flex: 3,
        child: Text(
          value,
          style: TextStyle(fontSize: 16),
        ),
      ),
    ],
  );
}
```

#### Tombol Aksi:
```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  children: [
    // Tombol Edit
    ElevatedButton.icon(
      icon: Icon(Icons.edit),
      label: Text("Edit"),
      onPressed: () {
        Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => ProdukForm(produk: widget.produk),
          ),
        );
      },
    ),
    
    // Tombol Hapus
    ElevatedButton.icon(
      icon: Icon(Icons.delete, color: Colors.white),
      label: Text("Hapus"),
      style: ElevatedButton.styleFrom(
        backgroundColor: Colors.red,
      ),
      onPressed: () => _confirmHapus(),
    ),
  ],
)
```

#### Dialog Konfirmasi Hapus:
```dart
void _confirmHapus() {
  showDialog(
    context: context,
    builder: (BuildContext context) => AlertDialog(
      title: const Text("Konfirmasi Hapus"),
      content: const Text("Apakah Anda yakin ingin menghapus produk ini?"),
      actions: [
        // Tombol Batal
        TextButton(
          child: const Text("Batal"),
          onPressed: () => Navigator.pop(context),
        ),
        
        // Tombol Hapus
        TextButton(
          child: const Text("Hapus", style: TextStyle(color: Colors.red)),
          onPressed: () {
            // Proses penghapusan
            Navigator.pop(context); // Tutup dialog
            Navigator.pop(context); // Kembali ke ProdukPage
            
            // Tampilkan snackbar feedback
            ScaffoldMessenger.of(context).showSnackBar(
              const SnackBar(
                content: Text('Produk berhasil dihapus!'),
                duration: Duration(seconds: 2),
              ),
            );
          },
        ),
      ],
    ),
  );
}
```

#### Navigasi:
- ✅ Klik Edit → ke halaman **Produk Form** (dengan data edit)
- ✅ Klik Hapus → tampilkan dialog konfirmasi
- ✅ Konfirmasi Hapus → kembali ke **Produk Page**
- ✅ Tombol back → kembali ke **Produk Page**

</details>

---

## 📊 Alur Proses LOGIN

```
┌─────────────────────────────────────────────────────┐
│              PROSES LOGIN (Step-by-Step)            │
└─────────────────────────────────────────────────────┘

STEP 1: Pengguna membuka aplikasi
        ↓
        Tampil halaman LoginPage

STEP 2: Pengguna mengisi email
        ↓
        Input validasi: email tidak boleh kosong

STEP 3: Pengguna mengisi password
        ↓
        Input validasi: password tidak boleh kosong

STEP 4: Pengguna klik tombol "Login"
        ↓
        Sistem validasi form (email & password)

STEP 5: Validasi Form
        ├─ Valid? → Lanjut ke STEP 6
        └─ Tidak valid? → Tampilkan error message

STEP 6: Sistem mengirim request ke API
        ├─ Method: POST
        ├─ URL: [API_URL]/login
        ├─ Body: { "email": "[email]", "password": "[password]" }
        └─ Header: Content-Type: application/x-www-form-urlencoded

STEP 7: API memproses login
        ├─ Email & password valid?
        │  ├─ YA → Generate JWT token
        │  │        Return response dengan code 200 & token
        │  │
        │  └─ TIDAK → Return response dengan code 401
        │             (Unauthorized)

STEP 8: Aplikasi menerima response
        ├─ Response code 200?
        │  ├─ YA → Lanjut ke STEP 9
        │  └─ TIDAK → STEP 11 (Tampilkan error)
        │
        └─ Extract data:
           - Token (JWT)
           - UserID
           - User Email

STEP 9: Simpan user session
        ├─ Simpan token ke SharedPreferences
        │  └─ Key: "token"
        │      Value: JWT token dari API
        │
        └─ Simpan UserID ke SharedPreferences
           └─ Key: "userID"
               Value: ID pengguna

STEP 10: Navigasi ke halaman Produk
         ↓
         Navigator.pushReplacement()
         └─ Ganti halaman: LoginPage → ProdukPage
         └─ Alasan: pushReplacement agar user tidak bisa
                    kembali ke LoginPage dengan back button

STEP 11: Tampilkan error dialog (Jika login gagal)
         ├─ Pesan: "Login gagal, silahkan coba lagi"
         ├─ User klik OK
         └─ Kembali ke halaman login

SELESAI ✓
```

### Kode Implementasi Login:
```dart
// File: lib/bloc/login_bloc.dart
class LoginBloc {
  static Future<Login> login({
    String? email,
    String? password,
  }) async {
    // 1. Set URL API
    String apiUrl = ApiUrl.login;

    // 2. Siapkan body request
    var body = {
      "email": email,
      "password": password,
    };

    // 3. Kirim POST request ke API
    var response = await Api().post(apiUrl, body);
    
    // 4. Parse response JSON
    var jsonObj = json.decode(response.body);

    // 5. Convert ke object Login
    return Login.fromJson(jsonObj);
  }
}

// File: lib/ui/login_page.dart
void _submit() {
  var validate = _formKey.currentState!.validate();
  
  if (validate) {
    setState(() => _isLoading = true);

    // Kirim request login
    LoginBloc.login(
      email: _emailTextboxController.text,
      password: _passwordTextboxController.text,
    ).then((value) async {
      if (value.code == 200) {
        // Login berhasil!
        
        // Simpan token
        await UserInfo().setToken(value.token.toString());
        
        // Simpan UserID
        await UserInfo().setUserID(value.userID ?? 0);

        // Navigasi ke ProdukPage
        Navigator.pushReplacement(
          context,
          MaterialPageRoute(builder: (context) => const ProdukPage()),
        );
      } else {
        // Login gagal - tampilkan warning dialog
        showDialog(
          context: context,
          barrierDismissible: false,
          builder: (BuildContext context) => const WarningDialog(
            description: "Login gagal, silahkan coba lagi",
          ),
        );
      }
    }, onError: (error) {
      // Handle error
      print(error);
      showDialog(
        context: context,
        barrierDismissible: false,
        builder: (BuildContext context) => const WarningDialog(
          description: "Login gagal, silahkan coba lagi",
        ),
      );
    });

    setState(() => _isLoading = false);
  }
}
```

---

## 📝 Alur Proses CRUD (Create, Read, Update, Delete)

### 1️⃣ **CREATE (Tambah Produk)**

```
┌─────────────────────────────────────────────────────┐
│         PROSES CREATE/TAMBAH PRODUK                 │
└─────────────────────────────────────────────────────┘

STEP 1: User berada di halaman ProdukPage
        ↓
        Klik icon "+" di AppBar

STEP 2: Navigasi ke halaman ProdukForm
        ├─ Mode: TAMBAH (produk parameter = null)
        ├─ Judul: "TAMBAH PRODUK"
        └─ Button: "SIMPAN"

STEP 3: User mengisi form
        ├─ Kode Produk (contoh: "PRD001")
        ├─ Nama Produk (contoh: "Laptop Dell")
        └─ Harga (contoh: "15000000")

STEP 4: Validasi form
        ├─ Cek setiap field tidak kosong
        ├─ Harga harus berupa angka
        └─ Tampilkan error jika ada field kosong

STEP 5: User klik tombol "SIMPAN"
        ↓
        Sistem melakukan validasi form

STEP 6: Jika valid, siapkan data produk
        ├─ Produk object = {
        │    kodeProduk: input_kode,
        │    namaProduk: input_nama,
        │    hargaProduk: input_harga
        │  }
        └─ Convert ke format JSON untuk API

STEP 7: Kirim POST request ke API
        ├─ URL: [API_URL]/produk
        ├─ Method: POST
        ├─ Body: JSON produk
        └─ Header: Authorization Bearer [token]

STEP 8: API memproses request
        ├─ Validasi token
        ├─ Validasi data produk
        └─ Simpan ke database

STEP 9: API return response
        ├─ Success (200): Return produk dengan ID baru
        ├─ Error (400): Bad request
        └─ Error (401): Unauthorized

STEP 10: Aplikasi menerima response
         ├─ Tampilkan SnackBar: "Produk berhasil ditambahkan!"
         ├─ Clear form input
         └─ Pop navigation (kembali ke ProdukPage)

STEP 11: ProdukPage di-refresh
         └─ Produk baru tampil di daftar list

SELESAI ✓
```

### 2️⃣ **READ (Baca/Tampilkan Produk)**

```
┌─────────────────────────────────────────────────────┐
│           PROSES READ/BACA PRODUK                   │
└─────────────────────────────────────────────────────┘

STEP 1: User login berhasil
        ↓
        Tampil halaman ProdukPage

STEP 2: Halaman load, sistem request daftar produk
        ├─ Kirim GET request ke API
        ├─ URL: [API_URL]/produk
        └─ Header: Authorization Bearer [token]

STEP 3: API memproses request
        ├─ Validasi token
        ├─ Query database: SELECT * FROM produk
        └─ Return JSON array produk

STEP 4: Aplikasi menerima response
        ├─ Parse JSON array
        └─ Convert ke List<Produk>

STEP 5: Render UI List Produk
        ├─ Loop setiap produk
        ├─ Buat Card item untuk setiap produk
        └─ Tampilkan di ListView

STEP 6: Setiap Card item menampilkan:
        ├─ Icon shopping cart
        ├─ Nama Produk
        ├─ Kode Produk
        ├─ Harga Produk
        └─ Icon arrow forward

STEP 7: User interaksi dengan list
        ├─ Swipe refresh: Reload data
        └─ Klik item: Buka halaman ProdukDetail

STEP 8: Di halaman ProdukDetail
        ├─ Tampilkan detail lengkap produk
        ├─ ID produk
        ├─ Kode produk
        ├─ Nama produk
        └─ Harga produk

SELESAI ✓ (Data ready ditampilkan)
```

### 3️⃣ **UPDATE (Edit Produk)**

```
┌─────────────────────────────────────────────────────┐
│          PROSES UPDATE/EDIT PRODUK                  │
└─────────────────────────────────────────────────────┘

STEP 1: User berada di halaman ProdukDetail
        ↓
        Klik tombol "EDIT"

STEP 2: Navigasi ke ProdukForm
        ├─ Mode: EDIT (produk parameter = produk object)
        ├─ Judul: "UBAH PRODUK"
        ├─ Button: "UBAH"
        └─ Auto-fill field dengan data lama:
           ├─ Kode Produk (dari produk.kodeProduk)
           ├─ Nama Produk (dari produk.namaProduk)
           └─ Harga (dari produk.hargaProduk)

STEP 3: User melakukan perubahan
        ├─ Edit Kode Produk (misal: PRD001 → PRD001_EDIT)
        ├─ Edit Nama Produk (misal: Laptop → Laptop Gaming)
        └─ Edit Harga (misal: 15000000 → 16000000)

STEP 4: User klik tombol "UBAH"
        ↓
        Sistem melakukan validasi form

STEP 5: Jika valid, siapkan data update
        ├─ Data update = {
        │    id: produk.id,
        │    kodeProduk: input_kode_baru,
        │    namaProduk: input_nama_baru,
        │    hargaProduk: input_harga_baru
        │  }
        └─ Convert ke format JSON

STEP 6: Kirim PUT request ke API
        ├─ URL: [API_URL]/produk/[ID]
        ├─ Method: PUT
        ├─ Body: JSON data update
        └─ Header: 
           ├─ Authorization Bearer [token]
           └─ Content-Type: application/json

STEP 7: API memproses request
        ├─ Validasi token
        ├─ Cari produk dengan ID
        ├─ Update field di database
        ├─ UPDATE produk SET ... WHERE id = [ID]
        └─ Return response sukses

STEP 8: Aplikasi menerima response
         ├─ Cek status response
         ├─ Jika 200: Sukses
         └─ Jika error: Tampilkan error message

STEP 9: Tampilkan SnackBar feedback
        ├─ Message: "Produk berhasil diubah!"
        ├─ Clear form
        └─ Pop navigation (kembali ke ProdukDetail)

STEP 10: ProdukDetail refresh dengan data baru
         └─ Tampilkan perubahan data produk

SELESAI ✓ (Produk updated)
```

### 4️⃣ **DELETE (Hapus Produk)**

```
┌─────────────────────────────────────────────────────┐
│         PROSES DELETE/HAPUS PRODUK                  │
└─────────────────────────────────────────────────────┘

STEP 1: User berada di halaman ProdukDetail
        ↓
        Klik tombol "HAPUS" (warna merah)

STEP 2: Tampilkan Dialog Konfirmasi
        ├─ Title: "Konfirmasi Hapus"
        ├─ Message: "Apakah Anda yakin ingin menghapus produk ini?"
        ├─ Button: "Batal"
        └─ Button: "Hapus"

STEP 3: User pilih aksi
        ├─ Klik "Batal" → Tutup dialog, tetap di halaman
        └─ Klik "Hapus" → Lanjut ke STEP 4

STEP 4: Sistem siapkan request hapus
        ├─ Target ID produk: produk.id
        └─ Tampilkan loading indicator

STEP 5: Kirim DELETE request ke API
        ├─ URL: [API_URL]/produk/[ID]
        ├─ Method: DELETE
        └─ Header: Authorization Bearer [token]

STEP 6: API memproses request
        ├─ Validasi token
        ├─ Cari produk dengan ID
        ├─ DELETE FROM produk WHERE id = [ID]
        └─ Return response sukses

STEP 7: Aplikasi menerima response
         ├─ Cek status response
         ├─ Jika 200: Produk terhapus
         └─ Jika error: Tampilkan error message

STEP 8: Update UI
        ├─ Tutup dialog konfirmasi
        ├─ Tampilkan SnackBar: "Produk berhasil dihapus!"
        └─ Navigasi kembali ke ProdukPage

STEP 9: ProdukPage refresh
        ├─ Re-fetch daftar produk dari API
        ├─ Produk yang dihapus tidak tampil lagi
        └─ Update list view

SELESAI ✓ (Produk deleted dari sistem)
```

---

## 🏗️ Struktur Proyek

```
tokokita/
├── lib/
│   ├── main.dart                 # 🔴 Entry point aplikasi
│   │
│   ├── bloc/                     # 🟢 Business Logic Layer
│   │   ├── login_bloc.dart       # Logic autentikasi
│   │   ├── logout_bloc.dart      # Logic logout
│   │   ├── produk_bloc.dart      # Logic CRUD produk
│   │   └── registrasi_bloc.dart  # Logic registrasi
│   │
│   ├── model/                    # 🟡 Data Models
│   │   ├── login.dart            # Model response login
│   │   ├── produk.dart           # Model data produk
│   │   └── registrasi.dart       # Model registrasi
│   │
│   ├── ui/                       # 🔵 UI Screens
│   │   ├── login_page.dart       # Halaman login
│   │   ├── registrasi_page.dart  # Halaman registrasi
│   │   ├── produk_page.dart      # List produk
│   │   ├── produk_form.dart      # Form tambah/edit
│   │   └── produk_detail.dart    # Detail produk
│   │
│   ├── widget/                   # 🟣 Custom Widgets
│   │   ├── success_dialog.dart   # Dialog sukses
│   │   └── warning_dialog.dart   # Dialog warning/error
│   │
│   └── helpers/                  # ⚙️ Helper Functions
│       ├── api.dart              # HTTP request handler
│       ├── api_url.dart          # Base URL & endpoints
│       ├── app_exception.dart    # Custom exceptions
│       └── user_info.dart        # Local storage (SharedPref)
│
├── android/                      # 📱 Android native config
├── ios/                          # 🍎 iOS native config
├── web/                          # 🌐 Web config
├── windows/                      # 🪟 Windows config
├── linux/                        # 🐧 Linux config
├── macos/                        # 🖥️ MacOS config
│
├── pubspec.yaml                  # Dependencies & config
├── analysis_options.yaml         # Lint rules
└── README.md                     # Documentation (File ini)
```

---

## 🔧 Dependencies & Libraries

```yaml
dependencies:
  flutter:
    sdk: flutter
  
  cupertino_icons: ^1.0.8      # iOS-style icons
  http: ^0.13.4                # HTTP requests (API calls)
  shared_preferences: ^2.0.11  # Local storage (token, userID)
```

### Penjelasan Penggunaan:
- **http**: Untuk membuat request ke backend API (login, CRUD)
- **shared_preferences**: Untuk menyimpan token & userID secara lokal

---

## 💾 Model Data

### Login Model
```dart
class Login {
  int? code;              // Status code (200, 401, dll)
  bool? status;           // Status boolean
  String? token;          // JWT token
  int? userID;            // ID pengguna
  String? userEmail;      // Email pengguna

  factory Login.fromJson(Map<String, dynamic> obj) {
    return Login(
      code: obj['code'],
      status: obj['status'],
      token: obj['data']['token'],
      userID: int.parse(obj['data']['user']['id'].toString()),
      userEmail: obj['data']['user']['email']
    );
  }
}
```

### Produk Model
```dart
class Produk {
  String? id;             // ID unik produk
  String? kodeProduk;     // Kode referensi produk
  String? namaProduk;     // Nama/deskripsi produk
  int? hargaProduk;       // Harga dalam rupiah

  Produk({
    this.id,
    this.kodeProduk,
    this.namaProduk,
    this.hargaProduk,
  });
}
```

---

## 🌐 API Endpoints

| Endpoint | Method | Auth | Fungsi | Body |
|----------|--------|------|--------|------|
| `/login` | POST | ❌ | Autentikasi pengguna | `{email, password}` |
| `/register` | POST | ❌ | Registrasi pengguna | `{nama, email, password}` |
| `/produk` | GET | ✅ | Ambil list produk | - |
| `/produk/{id}` | GET | ✅ | Ambil detail produk | - |
| `/produk` | POST | ✅ | Tambah produk | `{kodeProduk, namaProduk, hargaProduk}` |
| `/produk/{id}` | PUT | ✅ | Edit produk | `{kodeProduk, namaProduk, hargaProduk}` |
| `/produk/{id}` | DELETE | ✅ | Hapus produk | - |
| `/logout` | POST | ✅ | Logout | - |

*Note: ✅ = Memerlukan JWT token di header Authorization*

---

## 🎨 UI/UX Design Principles

✨ **Material Design 3**
- Konsistensi warna (Primary Blue, Secondary, Error Red)
- Spacing dan padding terstandar
- Icon dari Material Icons
- Shadow dan elevation untuk depth

✨ **User Experience**
- Validasi form real-time
- Loading indicator selama proses
- SnackBar untuk feedback action
- Dialog konfirmasi untuk aksi destruktif (delete)
- Error handling yang user-friendly

✨ **Responsive**
- Adaptif untuk berbagai ukuran layar
- SafeArea untuk notch handling
- SingleChildScrollView untuk overflow prevention

---

## ✅ Status Implementasi

| Fitur | Status | Catatan |
|-------|--------|---------|
| Layout UI | ✅ Selesai | Semua halaman sudah didesain |
| Validasi Form | ✅ Selesai | Email, password, nama, dll |
| Navigasi | ✅ Selesai | Antar halaman terintegrasi |
| API Integration | ✅ Selesai | Login, CRUD produk |
| Local Storage | ✅ Selesai | Token & UserID tersimpan |
| Error Handling | ✅ Selesai | Dialog & SnackBar feedback |
| Authentication | ✅ Selesai | JWT token implementation |

---

## 🚀 Cara Menjalankan Aplikasi

### Prerequisite:
```bash
Flutter SDK >= 3.9.2
Dart >= 3.0.0
```

### Step 1: Clone Repository
```bash
git clone <repository-url>
cd tokokita
```

### Step 2: Install Dependencies
```bash
flutter pub get
```

### Step 3: Run Aplikasi
```bash
# Run di emulator/device android
flutter run

# Run di chrome (web)
flutter run -d chrome

# Run dengan web security disabled (untuk testing)
flutter run -d chrome --web-browser-flag "--disable-web-security"
```

### Step 4: Build untuk Release
```bash
# Build APK untuk Android
flutter build apk --release

# Build APK split per architecture
flutter build apk --target-platform android-arm64 --release
```

---

## 🔐 Security Best Practices

✅ **Autentikasi**
- JWT token disimpan di SharedPreferences
- Token dikirim di setiap API request
- Expired token handling

✅ **Data Validation**
- Validasi input di client-side
- Validasi input di server-side (backend)
- Sanitasi data string

✅ **Error Handling**
- Tidak menampilkan error teknis ke user
- User-friendly error messages
- Logging untuk debugging

---

## 📚 Referensi & Resources

- [Flutter Documentation](https://flutter.dev/docs)
- [Dart Language](https://dart.dev/)
- [Material Design 3](https://m3.material.io/)
- [HTTP Package](https://pub.dev/packages/http)
- [SharedPreferences](https://pub.dev/packages/shared_preferences)

---


---

## 📄 License

Proyek ini dibuat untuk keperluan akademik.

---

<div align="center">

### 🎉 Terima Kasih Telah Membaca! 🎉

*Last Updated: December 2, 2025*

</div>
