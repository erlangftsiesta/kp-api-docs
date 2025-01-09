# >- Animo API

Dokumentasi ini berisi fungsi dan penjelasan seluruh endpoint API yang berhubungan dengan Akun Animo

---

- ## POST /api/users/create-new
  Endpoint tersebut digunakan untuk membuat akun Animo, parameter yang diperlukan adalah Request Body JSON dengan key sebagai berikut: `nama_panggilan, nomor_telepon, npsn, nama_sekolah`.

### Response JSON:

```json
{
  "success": true,
  "message": "An Animo's account was Successfully created",
  "payload": {
    "nomor_pendaftaran": {nomor_pendaftaran}, // Contoh: 202500001
    "nama_panggilan": {nama_panggilan}, // Contoh: "Ratu"
    "pin": {6 Digit terakhir nomor_telepon} // Contoh: 567890
  }
}
```

### Catatan:

> Endpoint ini akan membuat Akun Animo serta secara otomatis membuat 2 transaksi berstatus UNPAID dengan kode transaksi: `uang_pendaftaran` dan `mpls` untuk akun yang baru saja dibuat

---

- ## GET /api/users/{np}
  Endpoint tersebut digunakan untuk mencari data akun animo via nomor_pendaftaran (np).

### Response JSON:

```json
{
  "success": true,
  "message": "An Animo account was found!",
  "payload": {
    "nomor_pendaftaran": {nomor_pendaftaran}, // Contoh: 202500001
    "nama_panggilan": {nama_panggilan}, // Contoh: Ratu
    "nomor_telepon": {nomor_telepon}, // Contoh: 081234567890
    "pin": {encrypted_pin}, // Contoh:  "2b9e6e1a26156265cd32a7619a2baa2f"
    "npsn": {npsn}, // Contoh: 20100238
    "nama_sekolah": {nama_sekolah}, // Contoh: "SMPN 228 Jakarta"
    "status_akun": {status}, // Contoh: "NON AKTIF"
    "role": {role}, // Contoh: "animo"
  }
}
```

---

- ## PUT /api/users/{np}
  Endpoint tersebut digunakan untuk memperbarui data akun Animo, parameter yang diperlukan adalah Request Body JSON dengan key sebagai berikut: `nomor_pendaftaran, nama_panggilan, nomor_telepon, npsn, nama_sekolah, nama_sekolah, status_akun, role`.

### Response JSON:

```json
{
    "success": true,
    "message": "An Animo account was successfully updated!",
    "payload": {
        "changed_fields": {
            "status_akun": {
                "old": "NON AKTIF",
                "new": "AKTIF"
            },
            "role": {
                "old": "animo",
                "new": "terdaftar"
            }
        },
        "updated_data": {
            "nomor_pendaftaran": 202500001,
            "nama_panggilan": "Ratu",
            "nomor_telepon": "081234567890",
            "pin": "2b9e6e1a26156265cd32a7619a2baa2f",
            "npsn": 20100238,
            "nama_sekolah": "SMPN 228 Jakarta",
            "status_akun": "AKTIF",
            "role": "terdaftar"
        }
    }
}
```
### Catatan:

> - Dalam object `payload`, terdapat 2 object yaitu `change_fields` dan `updated_data`. 
> - Object `change_fields` berisi data fields apa saja yang terkena perubahan saat pembaruan data. Dapat kita lihat bahwa terdapat 2 field yang terkena dampak dari perubahan data yaitu `status_akun` yang awalnya `NON AKTIF` menjadi `AKTIF`, dan `role` yang berubah dari `animo` menjadi `terdaftar`.
> - Object `updated_data` berisi data terkini yang tercatat di Database setelah pembaruan data berhasil dilakukan

---

- ## DELETE /api/users/{np}
  Endpoint tersebut digunakan untuk menghapus data akun animo via parameter nomor_pendaftaran (np).

### Response JSON:

```json
{
    "success": true,
    "message": "An Animo account was successfully deleted",
    "payload": {
        "deleted_account": {nomor_pendaftaran} //Contoh: 202500001
    }
}
```
---

- ## POST /api/users/login/auth
  Endpoint tersebut digunakan untuk login kedalam Akun Animo, parameter yang diperlukan adalah Request Body JSON dengan key sebagai berikut: `nomor_pendaftaran, pin`.
  

### Response JSON:

```json
{
    "success": true,
    "message": "Login Success",
    "payload": {
      "nomor_pendaftaran": 202500001,
      "nama_panggilan": "Ratu",
    }
}
```
### Catatan:
> Selain mengirimkan Response berbentuk JSON, Jika autentikasi login User benar / valid, Backend juga mengirimkan cookies dengan metode `res.cookie` yang diberi nama `token` untuk memvalidasi sesi dan otorisasi pengguna. Cookies ini dilindungi oleh `HttpOnly: true`.

---
# Catatan Alur Keseluruhan
> - Endpoint `GET /api/users/{np}`, `PUT /api/users/{np}` dan `DELETE /api/users/{np}` akan dilindungi oleh Middleware, sehingga hanya admin yang dapat mengakses Endpoint tersebut, dengan cookie dan autentikasi yang sah.
> - Endpoint `/api/users/create-new` tidak dilindungi oleh middleware apapun, Request yang masuk akan difilter dan divalidasi oleh sistem. Jika validasi Request tidak mengalami error, maka sistem akan melakukan pembuatan akun dan data transaksi untuk akun yang baru dibuat secara otomatis
> - User/Animo tidak akan bisa mengakses akun milik mereka sehingga field `status_akun` pada Database berubah sedari `NON AKTIF` menjadi `AKTIF`.
