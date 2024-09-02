# Panduan Lengkap `curl` dan `jq`

## **Perintah Dasar `curl`**

### **1. GET Request**

Mengambil data dari server.

```
curl -X GET "https://api.example.com/resource"
```

### **2. POST Request dengan Data JSON**

Mengirim data JSON ke server untuk membuat resource baru.

```
curl -X POST "https://api.example.com/resource" -H "Content-Type: application/json" -d '{"key": "value"}'
```

### **3. PUT Request dengan Data JSON**

Memperbarui resource yang ada dengan data JSON.

```
curl -X PUT "https://api.example.com/resource/1" -H "Content-Type: application/json" -d '{"key": "new_value"}'
```

### **4. DELETE Request**

Menghapus resource dari server.

```
curl -X DELETE "https://api.example.com/resource/1"
```

### **5. Menambahkan Header**

Menambahkan header HTTP ke permintaan.

```
curl -X GET "https://api.example.com/resource" -H "Authorization: Bearer YOUR_API_KEY"
```

### **6. Menampilkan Header Respons**

Menampilkan header respons dari server.

```
curl -i "https://api.example.com/resource"
```

### **7. Menyimpan Respons ke File**

Menyimpan output dari permintaan ke file.

```
curl -s "https://api.example.com/resource" -o response.json
```

### **8. Menggunakan Authentication dengan Basic Auth**

Menggunakan otentikasi Basic Auth.

```
curl -u username:password -X GET "https://api.example.com/resource"
```

### **9. Mengatur Timeout**

Mengatur timeout untuk permintaan.

```
curl -m 30 "https://api.example.com/resource"
```

## **Penjelasan Opsi `curl`**

### **`-X`** (atau `--request`)

- Menentukan jenis HTTP request, seperti GET, POST, PUT, DELETE.
- Contoh:
    
```
curl -X POST "https://api.example.com/resource"
```
    
### **`-i`** (atau `--include`)

- Menampilkan header HTTP respons bersama body respons.
- Contoh:
    
```
curl -i "https://api.example.com/resource"
```
    

### **`-s`** (atau `--silent`)

- Menonaktifkan output progress bar atau pesan kesalahan.
- Contoh:
    
```
curl -s "https://api.example.com/resource"
```
    

### **`-H`** (atau `--header`)

- Menambahkan header HTTP ke permintaan.
- Contoh:
    
```
curl -H "Content-Type: application/json" "https://api.example.com/resource"
```
    

### **`-m`** (atau `--max-time`)

- Menentukan batas waktu maksimum untuk permintaan dalam detik.
- Contoh:
    
```
curl -m 30 "https://api.example.com/resource"
```
    

### **`-o`** (atau `--output`)

- Menyimpan output respons ke file.
- Contoh:
    
```
curl -o output.json "https://api.example.com/resource"
```
    

### **`-d`** (atau `--data`)

- Mengirim data dalam permintaan POST atau PUT.
- Contoh:
    
```
curl -X POST "https://api.example.com/resource" -d '{"key": "value"}'
```
    

### **`-u`** (atau `--user`)

- Menyediakan otentikasi dengan Basic Auth. Formatnya adalah `username:password`.
- Contoh:
    
```
curl -u user:pass "https://api.example.com/resource"
```
    

### **`-L`** (atau `--location`)

- Mengikuti redirect jika server mengembalikan kode status 3xx.
- Contoh:
    
```
curl -L "https://api.example.com/resource"
```
    

### **`-A`** (atau `--user-agent`)

- Menetapkan User-Agent header untuk permintaan.
- Contoh:
    
```
curl -A "MyApp/1.0" "https://api.example.com/resource"
```
    

### **`-F`** (atau `--form`)

- Mengirim data dalam format `multipart/form-data`, biasanya untuk upload file.
- Contoh:
    
```
curl -F "file=@path/to/file" "https://api.example.com/upload"
```
    

### **`-v`** (atau `--verbose`)

- Menampilkan informasi debug rinci mengenai permintaan dan respons.
- Contoh:
    
```
curl -v "https://api.example.com/resource"
```
    

### **`--proxy`**

- Menentukan server proxy untuk digunakan dalam permintaan.
- Contoh:
    
```
curl --proxy http://proxyserver:port "https://api.example.com/resource"
```
    

### **`-k`** (atau `--insecure`)

- Mengabaikan kesalahan sertifikat SSL. Berguna untuk server dengan sertifikat tidak valid.
- Contoh:
    
```
curl -k "https://self-signed.badssl.com/"
```
    

### **`-T`** (atau `--upload-file`)

- Mengirim file ke server dengan metode PUT.
- Contoh:
    
```
curl -T localfile.txt "https://api.example.com/upload"
```
    

### **`--compressed`**

- Menggunakan kompresi untuk mengirimkan dan menerima data.
- Contoh:
    
```
curl --compressed "https://api.example.com/resource"
```
    

### **`--max-redirs`**

- Menentukan jumlah maksimum redirect yang diikuti.
- Contoh:
    
```
curl --max-redirs 5 "https://api.example.com/resource"
```
    

### **`--trace`**

- Menyimpan informasi debug rinci mengenai permintaan dan respons ke file.
- Contoh:
    
```
curl --trace trace.log "https://api.example.com/resource"
```
    

### **`--trace-ascii`**

- Menyimpan informasi debug rinci dalam format ASCII ke file.
- Contoh:
    
```
curl --trace-ascii trace.log "https://api.example.com/resource"
```
    

### **`--stderr`**

- Menyimpan pesan kesalahan ke file tertentu.
- Contoh:
    
```
curl --stderr errors.log "https://api.example.com/resource"
```
    

## **Kombinasi `curl` dan `jq`**

### **1. Menampilkan Output JSON yang Terformat**

```
curl -s "https://api.example.com/resource" | jq .
```

### **2. Mengambil Field Tertentu dari JSON**

```
curl -s "https://api.example.com/resource" | jq '.fieldName'
```

### **3. Mengambil Elemen dari Array JSON**

```
curl -s "https://api.example.com/resource" | jq '.items[] | {id, name}'
```

### **4. Filter Berdasarkan Kondisi**

```
curl -s "https://api.example.com/resource" | jq '.items[] | select(.status == "active")'
```

### **5. Menggabungkan dan Memformat Data JSON**

```
curl -s "https://api.example.com/resource" | jq '{id: .id, name: .name, active: (.status == "active")}'
```

### **6. Mencetak Jumlah Elemen dalam Array**

```
curl -s "https://api.example.com/resource" | jq '.items | length'
```

### **7. Membuat Permintaan POST dengan Data JSON dan Memproses Respons**

```
curl -s -X POST "https://api.example.com/resource" -H "Content-Type: application/json" -d '{"key": "value"}' | jq '.response'
```

### **8. Menambahkan Parameter Query dan Menampilkan Hasil**

```
curl -s "https://api.example.com/search?query=example" | jq '.results[] | {title, link}'
```

### **9. Menangani Response Nested JSON**

```
curl -s "https://api.example.com/resource" | jq '.data.items[] | {id: .id, title: .details.title}'
```

### **10. Menggunakan Fungsi untuk Menghitung atau Mengubah Data**

```
curl -s "https://api.example.com/resource" | jq '[.items[].value] | add'
```

## **Perintah Dasar `jq`**

### **1. Memformat JSON**

```
jq .
```

### **2. Mengambil Field Tertentu**

```
jq '.fieldName'
```

### **3. Filter Berdasarkan Kondisi**

```
jq '.items[] | select(.status == "active")'
```

### **4. Menggabungkan Field**

```
jq '{id: .id, name: .name}'
```

### **5. Menjumlahkan Nilai**

```
jq '[.items[].value] | add'
```
### **6. Mengubah Struktur Data**

```
jq '{total: (.items | length), active: [.items[] | select(.status == "active") | .id]}'
```

