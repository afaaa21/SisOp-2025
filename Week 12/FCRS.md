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
