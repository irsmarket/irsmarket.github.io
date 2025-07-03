# IRS Market API Documentation

Selamat datang di dokumentasi API IRS Market. API ini memungkinkan integrasi dengan sistem IRS Market untuk penjualan produk digital seperti pulsa, kuota, dan token PLN.

## 🔐 Autentikasi

Gunakan API key di header:


## 📲 Endpoints

### 🔎 Cek Saldo

**GET** `/v1/balance`

```bash
curl -H "Authorization: Bearer {API_KEY}" https://api.irsmarket.com/v1/balance
```