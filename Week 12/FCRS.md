# FCFS Scheduling Algorithm
*Nama Anggota*
Afriq Fadlil Azim (3124500043)  
  
  Tara Adilah Fathin (3124500055)
---

## 1. FCFS Scheduling Tanpa Arrival Time (AT)

### Penjelasan Singkat

Algoritma **First-Come, First-Served (FCFS)** tanpa Arrival Time berarti semua proses dianggap datang bersamaan, jadi urutannya sesuai dengan input. CPU akan memproses satu per satu dari atas ke bawah tanpa bisa diganggu proses lain (*non-preemptive*).

Struktur data `struct proc` digunakan untuk menyimpan informasi setiap proses:

- `no`: Nomor proses (P1, P2, dst)
- `bt`: Burst Time, lamanya proses dijalankan di CPU
- `ct`: Completion Time, waktu proses selesai
- `tat`: Turnaround Time, total waktu sejak proses masuk hingga selesai
- `wt`: Waiting Time, waktu proses menunggu sebelum dieksekusi

### Alur Kerja Program

1. User diminta memasukkan jumlah proses.
2. Setiap proses dimasukkan `Burst Time`-nya.
3. Proses dihitung secara berurutan:
   - `CT` = penjumlahan burst time dari awal hingga proses tersebut
   - `TAT` = `CT` (karena AT = 0)
   - `WT` = `TAT - BT`
   - `RT` = sama dengan `WT`

### Contoh Input:
![image](https://github.com/afaaa21/SisOp-2025/blob/main/Week%2012/WhatsApp%20Image%202025-05-26%20at%2013.45.16.jpeg)

### Rumus Manual:

1. **CT (Completion Time)**  
   - CT1 = BT1  
   - CTi = CT(i-1) + BTi  
   - Hasil: 3, 4, 8, 13, 15

2. **TAT (Turnaround Time)**  
   - TAT = CT - AT (karena AT = 0)  
   - Hasil: 3, 4, 8, 13, 15

3. **WT (Waiting Time)**  
   - WT = TAT - BT  
   - Hasil: 0, 3, 4, 8, 13

4. **RT (Response Time)**  
   - RT = WT (karena proses langsung dieksekusi saat masuk antrian)  
   - Hasil: 0, 3, 4, 8, 13

5. **Rata-rata:**  
   - TAT = (3 + 4 + 8 + 13 + 15) / 5 = **8.6**  
   - WT = (0 + 3 + 4 + 8 + 13) / 5 = **5.6**

---

## 2. FCFS Scheduling Dengan Arrival Time (AT)

### Penjelasan Singkat

Pada versi ini, setiap proses punya **Arrival Time (AT)**, yaitu waktu kedatangannya ke sistem. Proses dijalankan berdasarkan siapa yang datang lebih dulu. Jika proses belum datang, CPU menunggu proses tersebut.

Struktur data `struct proc` berisi:

- `no`: Nomor proses
- `at`: Arrival Time, waktu datangnya proses
- `bt`: Burst Time
- `ct`: Completion Time
- `tat`: Turnaround Time
- `wt`: Waiting Time

### Alur Kerja Program

1. Proses dibaca dan disimpan lengkap dengan `AT` dan `BT`.
2. Proses diurutkan berdasarkan `AT` (semakin awal, semakin dulu dieksekusi).
3. Waktu saat ini (`ct`) digunakan untuk menghitung:
   - `CT = max(AT, waktu sekarang) + BT`
   - `TAT = CT - AT`
   - `WT = TAT - BT`
   - `RT = WT`

### Contoh Input:
![image](https://github.com/afaaa21/SisOp-2025/blob/main/Week%2012/WhatsApp%20Image%202025-05-26%20at%2013.45.17.jpeg)

### Rumus Manual:

1. **CT (Completion Time)**  
   - CTi = max(CT(i-1), ATi) + BTi  
   - Hasil: 8, 12, 21, 26

2. **TAT (Turnaround Time)**  
   - TAT = CT - AT  
   - Hasil: 8, 11, 19, 23

3. **WT (Waiting Time)**  
   - WT = TAT - BT  
   - Hasil: 0, 7, 10, 18

4. **RT (Response Time)**  
   - RT = WT  
   - Hasil: 0, 7, 10, 18

5. **Rata-rata:**  
   - TAT = (8 + 11 + 19 + 23) / 4 = **15.25**  
   - WT = (0 + 7 + 10 + 18) / 4 = **8.75**
