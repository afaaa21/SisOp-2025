https://drive.google.com/file/d/1yOgUHpoKuzfE2jUoP_WQACqjprFsLGTE/view?usp=sharing  
**Nama** : Afriq Fadlil Azim  
**NRP** : 3124500043  
**Dosen Pengajar** :Dr Ferry Astika Saputra ST, M.Sc

### 1. Beda Multiprogramming vs Multitasking  
**Multiprogramming**  
- **Tujuan**: Meningkatkan utilisasi CPU dengan menyimpan beberapa program dalam memori secara bersamaan.  
- **Mekanisme**: Saat satu program menunggu (misalnya untuk I/O), CPU beralih ke program lain.  
- **Contoh**: Sistem yang menjalankan banyak proses latar belakang (batch jobs).  

**Multitasking**  
- **Tujuan**: Memberikan respons cepat ke pengguna dengan *switching* cepat antar proses.  
- **Mekanisme**: CPU berpindah antar proses dengan frekuensi tinggi sehingga pengguna merasa program berjalan bersamaan.  
- **Contoh**: Sistem operasi modern yang memungkinkan multitab browser, aplikasi, dan layanan berjalan serentak.  

---

### 2. Fungsi OS  
1. **Manajemen Hardware**:  
   - Bertindak sebagai perantara antara aplikasi dan hardware (CPU, memori, I/O devices).  
2. **Eksekusi Program**:  
   - Menyediakan lingkungan untuk aplikasi berjalan (termasuk alokasi memori dan manajemen proses).  
3. **Alokasi Sumber Daya**:  
   - Mengatur pembagian sumber daya (CPU time, memori, storage) antar program/pengguna.  
4. **Kontrol & Proteksi**:  
   - Memastikan keamanan melalui dual-mode (user/kernel mode) dan privileged instructions.  
5. **Manajemen File & Storage**:  
   - Mengorganisasi data di disk, mengatur direktori, dan menyediakan akses terproteksi.  
6. **Antarmuka Pengguna**:  
   - Menyediakan CLI (Command Line Interface) atau GUI (Graphical User Interface).  

---

### 3. Virtualisasi Container  
**Definisi**:  
- Virtualisasi ringan yang mengisolasi aplikasi dalam lingkungan terpisah tanpa membutuhkan OS lengkap.  

**Fitur**:  
- **Efisiensi**: Menggunakan kernel host secara langsung (tidak perlu hypervisor).  
- **Isolasi**: Aplikasi dalam container tidak saling mengganggu.  
- **Portabilitas**: Container dapat dijalankan di berbagai lingkungan (development, production).  

**Contoh**:  
- Docker, Kubernetes.  

**Perbedaan dengan VM**:  
- **VM**: Membutuhkan OS lengkap dan hypervisor (contoh: VMware).  
- **Container**: Hanya memisahkan aplikasi, menggunakan resource host secara optimal.  

**Keuntungan**:  
- Penggunaan sumber daya lebih hemat.  
- Deployment cepat dan konsisten.  
