# >- Transactions API

Dokumentasi ini berisi fungsi dan penjelasan seluruh endpoint API yang berhubungan dengan Transaction

---

- ## POST /api/transactions/create-new - Role: Admin
  Endpoint tersebut digunakan untuk membuat transaksi/tagihan baru yang akan dibebankan pada akun siswa, parameter yang diperlukan adalah Request Body JSON dengan key sebagai berikut: `nomor_pendaftaran, total_harga, deskripsi, kode_transaksi, tanggal_pembayaran`.

### Response JSON:

```json
{
  "success": true,
  "message": "Transaction has been successfully created.",
  "payload": {
    "id": 20,
    "charged_to": 202500001,
    "name": "Ratu Natifha Alena",
    "amount": 150000,
    "payment_detail": "Pembayaran Buku Kelas X"
  }
}
```

### Catatan:

> Endpoint ini dapat membuat transaksi baru untuk siswa, namun perlu diperhatikan untuk field `kode_transaksi`, Backend hanya menerima 3 bentuk kode_transaksi: `mpls`, `uang_pendaftaran`, `lain-lain`

---

- ## GET /api/transactions/unpaid/students - Role: Admin
  Endpoint tersebut digunakan untuk mencari keseluruhan transaksi yang belum lunas dari calon siswa yang sudah melakukan pembayaran `uang_pendaftaran` sehingga `role` nya pada database sudah menjadi `terdaftar`.

### Response JSON:

```json
{
  "success": true,
  "message": "Unpaid Students's Account Transactions was successfully founded!",
  "account_type": "Students",
  "payload": [
    {
      "nama": "Ratu Natifha Alena",
      "unpaid_transactions": [
        {
          "nomor_pendaftaran": 202500001,
          "total_harga": 50000,
          "deskripsi": "Pembayaran akun dan formulir"
        },
        {
          "nomor_pendaftaran": 202500001,
          "total_harga": 150000,
          "deskripsi": "Pembayaran Buku Kelas X"
        }
        //...
      ]
    }
  ]
}
```

---

- ## GET /api/transactions/unpaid/animos - Role: Admin
  Endpoint tersebut digunakan untuk mencari keseluruhan transaksi yang belum lunas dari calon siswa yang sama sekali belum melakukan pembayaran, uang pendaftaran maupun uang MPLS.

### Response JSON:

```json
{
  "success": true,
  "message": "Unpaid Animos's Account Transactions was successfully founded!",
  "account_type": "Animo",
  "payload": [
    {
      "nama": "Erlang",
      "unpaid_transactions": [
        {
          "nomor_pendaftaran": 202500002,
          "total_harga": 50000,
          "deskripsi": "Pembayaran akun dan formulir"
        },
        {
          "nomor_pendaftaran": 202500002,
          "total_harga": 150000,
          "deskripsi": "Pembayaran untuk kegiatan MPLS"
        }
      ]
    }
  ]
}
```

---

- ## GET /api/transactions/{np} - Role: Admin
  Endpoint tersebut digunakan untuk mencari detail transaksi dari 1 akun (entah `Animo` maupun yang `Terdaftar`)

### Response JSON:

```json
{
  "success": true,
  "message": "Detailed student's transactions were found",
  "payload": {
    "nomor_pendaftaran": "202500001",
    "transactions": [
      {
        "id": 17,
        "nomor_pendaftaran": 202500001,
        "total_harga": 150000,
        "deskripsi": "Pembayaran Buku Kelas X",
        "kode_transaksi": "lain-lain",
        "tanggal_pembayaran": "2025-01-04T17:00:00.000Z",
        "status": "UNPAID",
        "created_at": "2025-01-04T17:00:00.000Z"
      },
      {
        "id": 14,
        "nomor_pendaftaran": 202500001,
        "total_harga": 50000,
        "deskripsi": "Pembayaran akun dan formulir",
        "kode_transaksi": "uang_pendaftaran",
        "tanggal_pembayaran": "2025-01-02T17:00:00.000Z",
        "status": "UNPAID",
        "created_at": "2025-01-03T17:00:00.000Z"
      }
      //...
    ]
  }
}
```

---

- ## GET /api/transactions/all - Role: Admin
  Endpoint tersebut digunakan untuk mencari seluruh transaksi yang tercatat dalam table `transaksi`.

### Response JSON:

```json
{
  "success": true,
  "message": "All transactions were found!",
  "payload": {
    "0": {
      "id": 14,
      "nomor_pendaftaran": 202500001,
      "total_harga": 50000,
      "deskripsi": "Pembayaran akun dan formulir",
      "kode_transaksi": "uang_pendaftaran",
      "tanggal_pembayaran": "2025-01-02T17:00:00.000Z",
      "status": "PAID",
      "created_at": "2025-01-03T17:00:00.000Z"
    },
    "1": {
      "id": 17,
      "nomor_pendaftaran": 202500001,
      "total_harga": 150000,
      "deskripsi": "Pembayaran Buku Kelas X",
      "kode_transaksi": "lain-lain",
      "tanggal_pembayaran": "2025-01-04T17:00:00.000Z",
      "status": "UNPAID",
      "created_at": "2025-01-04T17:00:00.000Z"
    },
    "2": {
      "id": 18,
      "nomor_pendaftaran": 202500001,
      "total_harga": 150000,
      "deskripsi": "Pembayaran Buku Kelas X",
      "kode_transaksi": "lain-lain",
      "tanggal_pembayaran": "2025-01-04T17:00:00.000Z",
      "status": "UNPAID",
      "created_at": "2025-01-04T17:00:00.000Z"
    },
    "3": {
      "id": 19,
      "nomor_pendaftaran": 202500001,
      "total_harga": 150000,
      "deskripsi": "Pembayaran Buku Kelas X",
      "kode_transaksi": "lain-lain",
      "tanggal_pembayaran": "2025-01-04T17:00:00.000Z",
      "status": "UNPAID",
      "created_at": "2025-01-04T17:00:00.000Z"
    },
    "4": {
      "id": 20,
      "nomor_pendaftaran": 202500001,
      "total_harga": 150000,
      "deskripsi": "Pembayaran Buku Kelas X",
      "kode_transaksi": "lain-lain",
      "tanggal_pembayaran": "2025-01-04T17:00:00.000Z",
      "status": "UNPAID",
      "created_at": "2025-01-04T17:00:00.000Z"
    },
    "5": {
      "id": 21,
      "nomor_pendaftaran": 202500002,
      "total_harga": 50000,
      "deskripsi": "Pembayaran akun dan formulir",
      "kode_transaksi": "uang_pendaftaran",
      "tanggal_pembayaran": "2025-01-05T17:00:00.000Z",
      "status": "UNPAID",
      "created_at": "2025-01-05T17:00:00.000Z"
    },
    "6": {
      "id": 22,
      "nomor_pendaftaran": 202500002,
      "total_harga": 150000,
      "deskripsi": "Pembayaran untuk kegiatan MPLS",
      "kode_transaksi": "mpls",
      "tanggal_pembayaran": "2025-01-05T17:00:00.000Z",
      "status": "UNPAID",
      "created_at": "2025-01-05T17:00:00.000Z"
    }
  }
}
```

---

- ## GET /api/transactions/account/{np} - Role: Admin
  Endpoint tersebut digunakan untuk mencari 1 transaksi dari 1 account. parameter yang diperlukan adalah Request Body JSON dengan key sebagai berikut: `id`.

### Response JSON:

```json
{
  "success": true,
  "result": {
    "id": 14,
    "nomor_pendaftaran": 202500001,
    "total_harga": 50000,
    "deskripsi": "Pembayaran akun dan formulir",
    "kode_transaksi": "uang_pendaftaran",
    "tanggal_pembayaran": "2025-01-02T17:00:00.000Z",
    "status": "PAID",
    "created_at": "2025-01-03T17:00:00.000Z"
  }
}
```

---

- ## PUT /api/transactions/{np} - Role: Admin
  Endpoint tersebut digunakan untuk memperbarui 1 data transaksi dari 1 akun, parameter yang diperlukan adalah Request Body JSON dengan key sebagai berikut: `id, total_harga,deskripsi,kode_transaksi,tanggal_pembayaran,status,`.

### Response JSON:

```json
{
  "success": true,
  "message": "One User's Transaction was Successfully updated!",
  "payload": {
    "changed_fields": {
      "total_harga": {
        "old": 180000,
        "new": 195000
      },
      "tanggal_pembayaran": {
        "old": "2025-01-04T17:00:00.000Z",
        "new": "2025-01-04T17:00:00.000Z"
      },
      "created_at": {
        "old": "2025-01-03T17:00:00.000Z",
        "new": "2025-01-03T17:00:00.000Z"
      }
    },
    "updated_data": {
      "id": 14,
      "nomor_pendaftaran": 202500001,
      "total_harga": 195000,
      "deskripsi": "Pembayaran Buku Kelas X",
      "kode_transaksi": "lain-lain",
      "tanggal_pembayaran": "2025-01-04T17:00:00.000Z",
      "status": "UNPAID",
      "created_at": "2025-01-03T17:00:00.000Z"
    }
  }
}
```

### Catatan:

> - Dalam object `payload`, terdapat 2 object yaitu `change_fields` dan `updated_data`.
> - Object `change_fields` berisi data fields apa saja yang terkena perubahan saat pembaruan data. Dapat kita lihat bahwa terdapat beberapa field yang terkena dampak dari perubahan data, salah satu fieldnya yaitu `total_harga` yang awalnya `180000` menjadi `195000`.
> - Object `updated_data` berisi data terkini yang tercatat di Database setelah pembaruan data berhasil dilakukann

---

- ## DELETE /api/transactions/{np} - Role: Admin
  Endpoint tersebut digunakan untuk menghapus data 1 transaksi dari 1 akun. Parameter yang diperlukan adalah Request Body JSON dengan key sebagai berikut: `nomor_pendaftaran, id`.

### Response JSON:

```json
{
  "success": true,
  "message": "One User's Transaction was Successfully deleted!",
  "payload": {
    "nomor_pendaftaran": 202500001,
    "deleted_transaction_id": 17
  }
}
```

---


# Catatan Alur Keseluruhan

> Nanti dikelarin, backendnya pusing
