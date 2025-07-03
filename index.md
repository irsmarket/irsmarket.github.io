# IRS Market API Documentation

Selamat datang di dokumentasi API IRS Market. API ini memungkinkan integrasi dengan sistem IRS Market untuk penjualan produk digital seperti pulsa, kuota, dan token PLN.

## 📲 Endpoints

**POST** `/v1/transaction`
##### JsonBody
```json
{
    "apikey": "",
    "apisecret": "",
    "productcode": "",
    "trxid": "",
    "customerno": "",
    "maxprice": ""
}
```

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `apikey` | string | Yes | API key untuk autentikasi |
| `apisecret` | string | Yes | API secret untuk autentikasi |
| `productcode` | string | Yes | Kode produk yang akan dibeli |
| `trxid` | string | Yes | ID transaksi unik dari sistem Anda |
| `customerno` | string | Yes | Nomor tujuan/customer (no HP, ID PLN, dll) |
| `maxprice` | string | No | Harga maksimal yang bersedia dibayar |

**GET** `/v1/transaction`
```bash
/v1/transaction?apikey=apikey&apisecret=secret&productcode=S5&trxid=1940164&customerno=08123411122333
```

### Callback Transaksi ###
```json
{
    "trxid":"545067982", 
    "reff":"5537178", 
    "tujuan":"085609059707", 
    "produk":"I50", 
    "harga":"48,850", 
    "status":"Sukses",
    "rc":"00",
    "sn":"033052001265110126967", 
    "saldo":"1,006,537", 
    "waktu":"2025-07-03 11:22:52"
}
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `trxid` | string | ID transaksi unik dari sistem Anda |
| `reff` | string | Referensi transaksi dari sistem IRS Market |
| `tujuan` | string | Nomor tujuan/customer yang diproses |
| `produk` | string | Kode produk yang dibeli |
| `harga` | string | Harga transaksi dalam format rupiah |
| `status` | string | Status transaksi (Sukses, Gagal, Pending) |
| `rc` | string | Response code (00 = sukses,68 = pending, selain itu gagal) |
| `sn` | string | Serial number/voucher code (jika ada) |
| `saldo` | string | Saldo tersisa setelah transaksi |
| `waktu` | string | Timestamp transaksi (format: YYYY-MM-DD HH:mm:ss) |


## Response code ##

| Code | Status | Description |
|------|--------|-------------|
| `00` | Sukses | Transaksi berhasil diproses |
| `68` | Pending | Transaksi sedang diproses |
| `01` | Gagal | Saldo tidak mencukupi |
| `02` | Gagal | Nomor tujuan tidak valid |
| `03` | Gagal | Produk tidak tersedia |
| `04` | Gagal | Transaksi sudah ada (duplikat trxid) |
| `05` | Gagal | API key tidak valid |
| `06` | Gagal | API secret tidak valid |
| `07` | Gagal | Parameter tidak lengkap |
| `08` | Gagal | Sistem maintenance |
| `09` | Gagal | Timeout dari provider |
| `99` | Gagal | Error sistem lainnya |
