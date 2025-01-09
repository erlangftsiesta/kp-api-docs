# >- Students API

Dokumentasi ini berisi fungsi dan penjelasan seluruh endpoint API yang berhubungan dengan Akun Animo

---

- ## POST /api/students/add
  Endpoint tersebut digunakan untuk membuat akun Animo, parameter yang diperlukan adalah Request Body JSON dengan key sebagai berikut: `nomor_pendaftaran, nisn, nama_lengkap, nama_panggilan, jenis_kelamin, tempat_lahir, tanggal_lahir, alamat, kelurahan, kecamatan, kabupaten_kota, provinsi, kode_pos, sekolah_pilihan, tipe_pendaftar, pindah_di_tahun_ajaran, tanggal_mulai_masuk, kelas_pilihan, jurusan, jalur_seleksi, asal_sekolah, kontak_pendaftar, kontak_orangtua_wali, email, informasi_pendaftaran, alasan_minat_pendaftaran`.

### Response JSON:

```json
{
  "success": true,
  "message": "Informasi lengkap terkait peserta didik berhasil ditambahkan",
  "payload": {
    "nomor_pendaftaran": 202500001,
    "nisn": 1234567890,
    "nama_lengkap": "Ratu Natifha Alen"
  }
}
```

### Catatan:

> Tidak perlu mengisi field `pindah_di_tahun_ajaran`, jika siswa bukan merupakan siswa pindahan
> Request `nomor_pendaftaran` dan `nisn` harus bertipe Integer / Number.

---

- ## GET /api/students/all
  Endpoint tersebut digunakan untuk mencari data seluruh akun siswa yang sudah membayar uang pendaftaran (terdaftar)

### Response JSON:

```json
{
  [
    "success": true,
    "message": "Student information was successfully loaded",
    "payload": {
      "0": {
        "id": 1,
        "nomor_pendaftaran": 202500001,
        "nisn": 1234567890,
        //....
      },
      "1": {
        "id": 2,
        "nomor_pendaftaran": 202500002,
        "nisn": 1234567891,
        //....
      }
    }
  ]
}
```

---

- ## GET /api/users/{np}
  Endpoint tersebut digunakan untuk mencari akun siswa yang lebih spesifik dengan `nomor_pendaftaran` (np)

### Response JSON:

```json
{
  "success": true,
  "message": "Student information was successfully loaded",
  "payload": {
    "id": 1,
    "nomor_pendaftaran": 202500001,
    "nisn": 1234567890,
    "nama_lengkap": "Ratu Natifha Alen",
    "jenis_kelamin": "perempuan",
    "tempat_lahir": "Jakarta",
    "tanggal_lahir": "2009-07-26T17:00:00.000Z",
    "alamat": "Jl. Mawar No. 123",
    "kelurahan": "Cipete",
    "kecamatan": "Cilandak",
    "kabupaten_kota": "Jakarta Selatan",
    "provinsi": "DKI Jakarta",
    "kode_pos": 12345,
    "sekolah_pilihan": "Kaone School",
    "tipe_pendaftar": "pendaftar baru",
    "pindah_di_tahun_ajaran": null,
    "tanggal_mulai_masuk": "2024-07-14T17:00:00.000Z",
    "kelas_pilihan": "10",
    "jurusan": "RPL",
    "jalur_seleksi": "Reguler",
    "asal_sekolah": "SMP Negeri 228",
    "kontak_pendaftar": "081234567890",
    "kontak_orangtua_wali": "081234567891",
    "email": "myalen@email.com",
    "informasi_pendaftaran": "Media Sosial",
    "alasan_minat_pendaftaran": "Ingin mendapatkan pendidikan berkualitas",
    "created_at": "2025-01-04T09:20:25.000Z"
  }
}
```

---

- ## PUT /api/students/{np}
  Endpoint tersebut digunakan untuk memperbarui data akun Animo, parameter yang diperlukan adalah Request Body JSON dengan key sebagai berikut: `nomor_pendaftaran, nisn, nama_lengkap, nama_panggilan, jenis_kelamin, tempat_lahir, tanggal_lahir, alamat, kelurahan, kecamatan, kabupaten_kota, provinsi, kode_pos, sekolah_pilihan, tipe_pendaftar, pindah_di_tahun_ajaran, tanggal_mulai_masuk, kelas_pilihan, jurusan, jalur_seleksi, asal_sekolah, kontak_pendaftar, kontak_orangtua_wali, email, informasi_pendaftaran, alasan_minat_pendaftaran`.

### Response JSON:

```json
{
  "success": true,
  "message": "A Student's Information was successfully updated!",
  "payload": {
    "changed_fields": {
      "nama_lengkap": {
        "old": "Ratu Natifha Alen",
        "new": "Ratu Natifha Alena"
      },
      "tanggal_lahir": {
        "old": "2009-07-26T17:00:00.000Z",
        "new": "2009-07-26T17:00:00.000Z"
      },
      "tanggal_mulai_masuk": {
        "old": "2024-07-14T17:00:00.000Z",
        "new": "2024-07-14T17:00:00.000Z"
      },
      "created_at": {
        "old": "2025-01-04T09:20:25.000Z",
        "new": "2025-01-04T09:20:25.000Z"
      }
    },
    "updated_data": {
      "id": 1,
      "nomor_pendaftaran": 202500001,
      "nisn": 1234567890,
      "nama_lengkap": "Ratu Natifha Alena",
      "jenis_kelamin": "perempuan",
      "tempat_lahir": "Jakarta",
      "tanggal_lahir": "2009-07-26T17:00:00.000Z",
      "alamat": "Jl. Mawar No. 123",
      "kelurahan": "Cipete",
      "kecamatan": "Cilandak",
      "kabupaten_kota": "Jakarta Selatan",
      "provinsi": "DKI Jakarta",
      "kode_pos": 12345,
      "sekolah_pilihan": "Kaone School",
      "tipe_pendaftar": "pendaftar baru",
      "pindah_di_tahun_ajaran": null,
      "tanggal_mulai_masuk": "2024-07-14T17:00:00.000Z",
      "kelas_pilihan": "10",
      "jurusan": "RPL",
      "jalur_seleksi": "Reguler",
      "asal_sekolah": "SMP Negeri 228",
      "kontak_pendaftar": "081234567890",
      "kontak_orangtua_wali": "081234567891",
      "email": "myalen@email.com",
      "informasi_pendaftaran": "Media Sosial",
      "alasan_minat_pendaftaran": "Ingin mendapatkan pendidikan berkualitas",
      "created_at": "2025-01-04T09:20:25.000Z"
    }
  }
}
```

### Catatan:

> - Dalam object `payload`, terdapat 2 object yaitu `change_fields` dan `updated_data`.
> - Object `change_fields` berisi data fields apa saja yang terkena perubahan saat pembaruan data. Dapat kita lihat bahwa terdapat beberapa field yang terkena dampak dari perubahan data, salah satu fieldnya yaitu `nama_lengkap` yang awalnya `Ratu Natifha Alen` menjadi `Ratu Natifha Alena`.
> - Object `updated_data` berisi data terkini yang tercatat di Database setelah pembaruan data berhasil dilakukan

---

- ## DELETE /api/students/{np}
  Endpoint tersebut digunakan untuk menghapus data akun animo via nomor_pendaftaran (np).

### Response JSON:

```json
{
    "success": true,
    "message": "A Student's Information was successfully deleted!",
    "payload": {
        "deleted_account": {nomor_pendaftaran} //Contoh: 202500001
    }
}
```

---

# Catatan Alur Keseluruhan

> Nanti dikelarin, backendnya pusing
