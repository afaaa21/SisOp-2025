# Analisis Hasil Eksekusi Program Penjadwalan SJF (Shortest Job First) Non-Preemptive
**Nama Anggota**  

  Afriq Fadlil Azim (3124500043)  
  
  Tara Adilah Fathin (3124500055)
  
## Definisi dan Cara Kerja Shortest Job First(SJF) Non-preemptive
Algoritma Shortest Job First (SJF) adalah kebijakan penjadwalan yang memprioritaskan proses berdasarkan waktu burst CPU-nya. Secara spesifik, algoritma ini memilih proses yang sedang menunggu dengan perkiraan waktu eksekusi terkecil untuk alokasi CPU berikutnya.Karakteristik non-preemptive dari varian ini sangat penting: setelah suatu proses dipilih dan mulai dieksekusi, proses tersebut akan berjalan hingga selesai tanpa interupsi, bahkan jika ada proses baru dengan waktu burst yang lebih pendek tiba dalam antrean siap selama eksekusinya.

# Keunggulan dan Kriteria
Secara teoritis, SJF memiliki keunggulan signifikan: algoritma ini terbukti menghasilkan waktu tunggu rata-rata minimum dan, sebagai konsekuensinya, waktu turnaround rata-rata minimum untuk sekumpulan proses tertentu.Dari sudut pandang konseptual, SJF relatif sederhana, karena keputusan penjadwalan didasarkan pada satu kriteria yang jelas: waktu burst terpendek.
Namun, tantangan praktis paling signifikan dari SJF adalah persyaratan untuk mengetahui total waktu eksekusi (burst time) suatu pekerjaan sebelum pekerjaan tersebut dimulai. Dalam lingkungan komputasi dunia nyata yang dinamis, informasi ini jarang tersedia secara tepat.
 Implikasinya adalah bahwa simulasi ini menampilkan kinerja SJF dalam skenario terbaik, yang mungkin tidak dapat dicapai dalam sistem dunia nyata tanpa teknik estimasi waktu burst yang canggih (dan tidak sempurna) 

 Kekhawatiran utama terkait keadilan dengan SJF adalah kemungkinan "kelaparan" (starvation). Jika ada aliran berkelanjutan dari pekerjaan-pekerjaan pendek yang tiba, pekerjaan-pekerjaan yang lebih panjang mungkin akan berulang kali ditunda dan tidak pernah mendapatkan kesempatan untuk dieksekusi, yang mengarah pada penantian yang tidak terbatas. Meskipun demikian, SJF dapat secara efektif digunakan dalam lingkungan khusus di mana perkiraan waktu berjalan yang akurat tersedia, atau untuk proses interaktif di mana perilaku historis dapat menginformasikan prediksi waktu burst.

 # Rumus dan definisinya
- **Waktu Kedatangan (Arrival Time/AT)**: Titik waktu spesifik ketika suatu proses memasuki antrean siap dan menjadi tersedia untuk dieksekusi.   
- **Waktu Burst (Burst Time/BT)**: Total waktu CPU yang dibutuhkan oleh suatu proses untuk eksekusi lengkapnya. Ini juga disebut sebagai "Waktu Eksekusi" dalam beberapa konteks.
- **Waktu Selesai (Completion Time - CT)**: Waktu pasti di mana suatu proses menyelesaikan seluruh eksekusinya dan meninggalkan sistem.
    Rumus: CT = Waktu ketika proses selesai dieksekusi.
- **Waktu Turnaround (Turnaround Time - TAT)**: Total durasi suatu proses berada dalam sistem, diukur dari kedatangannya hingga penyelesaiannya. Ini mencakup waktu proses dieksekusi di CPU dan waktu yang dihabiskan untuk menunggu dalam antrean.
  * **Rumus 1**: TAT = Waktu Selesai (CT) – Waktu Kedatangan (AT).
  * **Rumus 2**: TAT = Waktu Burst (BT) + Waktu Tunggu (WT).
- **Waktu Tunggu (Waiting Time - WT)**: Waktu kumulatif suatu proses menunggu dalam antrean siap agar CPU tersedia. Untuk algoritma non-preemptive, ini terutama adalah waktu yang dihabiskan untuk menunggu sebelum eksekusi awalnya.   
  * **Rumus 1**: WT = Waktu Turnaround (TAT) – Waktu Burst (BT).   
  * **Rumus 2** (Alternatif untuk non-preemptive): WT = Waktu Mulai Eksekusi – Waktu Kedatangan.
- **Waktu Respons (Response Time - RT)**: Waktu yang berlalu sejak suatu proses tiba hingga pertama kali mulai dieksekusi di CPU. Metrik ini sangat relevan untuk sistem interaktif, karena mencerminkan persepsi pengguna tentang seberapa cepat sistem merespons permintaan mereka.   
  * **Rumus**: RT = Waktu Mulai Eksekusi – Waktu Kedatangan

# Tujuan
Waktu turnaround rata-rata dan waktu tunggu rata-rata dihitung dengan menjumlahkan waktu individu dan membaginya dengan jumlah proses. Rata-rata ini memberikan ukuran agregat kinerja keseluruhan algoritma, menunjukkan efisiensi dan responsivitas tipikal untuk beban kerja tertentu. Tujuan utama SJF adalah meminimalkan nilai rata-rata ini.

## Code Program
```
#include<stdio.h>
struct proc
{
    int no,at,bt,it,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Arrival Time: ");
    scanf("%d",&p.at);
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
int main()
{
    int  n,j,min=0;
    float avgtat=0,avgwt=0;
    struct proc p[10],temp;
    printf("<--SJF Scheduling Algorithm (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
            temp=p[j];
            p[j]=p[j+1];
            p[j+1]=temp;
            }
    for(j=1;j<n&&p[j].at==p[0].at;j++)
        if(p[j].bt<p[min].bt)
            min=j;
    temp=p[0];
    p[0]=p[min];
    p[min]=temp;
    p[0].it=p[0].at;
    p[0].ct=p[0].it+p[0].bt;
    for(int i=1;i<n;i++)
    {
        for(j=i+1,min=i;j<n&&p[j].at<=p[i-1].ct;j++)
            if(p[j].bt<p[min].bt)
                min=j;
        temp=p[i];
        p[i]=p[min];
        p[min]=temp;
        if(p[i].at<=p[i-1].ct)
            p[i].it=p[i-1].ct;
        else
            p[i].it=p[i].at;
        p[i].ct=p[i].it+p[i].bt;
    }
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\tRT\n");
    for(int i=0;i<n;i++)
    {
        p[i].tat=p[i].ct-p[i].at;
        avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].at,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```
# Output Program
![image](https://github.com/afaaa21/SisOp-2025/blob/main/week%2013/Screenshot%202025-05-26%20045852.png)

## Tabel Hasil
| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 7 | 7 | 7 | 0 | 0 |
| P3 | 4 | 1 | 8 | 4 | 3 | 3 |
| P2 | 2 | 4 | 12 | 10 | 6 | 6 |
| P4 | 5 | 4 | 16 | 11 | 7 | 7 | 

# Urutan Kronologis Eksekusi Algoritma SJF Non-Preemptive

Berikut adalah urutan kronologis eksekusi berdasarkan algoritma Shortest Job First (SJF) Non-Preemptive:

*   **Waktu 0:** Proses P1 tiba (AT=0). Tidak ada proses lain dalam antrean siap.
    *   *Tindakan:* P1 segera dikirim dan mulai dieksekusi.
*   **Waktu 0 hingga Waktu 7:** P1 dieksekusi.
    *   *Selama periode ini:*
        *   Pada **Waktu 2**, Proses P2 tiba (AT=2, BT=4). P1 masih berjalan. P2 memasuki antrean siap.
        *   Pada **Waktu 4**, Proses P3 tiba (AT=4, BT=1). P1 masih berjalan. P3 memasuki antrean siap.
        *   Pada **Waktu 5**, Proses P4 tiba (AT=5, BT=4). P1 masih berjalan. P4 memasuki antrean siap.
*   **Waktu 7:** Proses P1 menyelesaikan eksekusi (BT=7).
    *   *Antrean Siap pada Waktu 7:* P2 (BT=4), P3 (BT=1), P4 (BT=4).
    *   *Keputusan SJF:* Di antara proses yang menunggu, P3 memiliki waktu *burst* terpendek (BT=1).
    *   *Tindakan:* P3 dikirim dan mulai dieksekusi.
*   **Waktu 7 hingga Waktu 8:** Proses P3 dieksekusi.
*   **Waktu 8:** Proses P3 menyelesaikan eksekusi (BT=1).
    *   *Antrean Siap pada Waktu 8:* P2 (BT=4), P4 (BT=4).
    *   *Keputusan SJF:* P2 dan P4 memiliki waktu *burst* yang sama (BT=4). Aturan pemecah seri (biasanya First-Come, First served -FCFS) diterapkan.Karena P2 tiba pada T=2 dan P4 tiba pada T=5, P2 tiba lebih awal.
    *   Tindakan: P2 dikirim dan mulai dieksekusi.
*   **Waktu 8 hingga waktu 12:** Proses P2 dieksekusi.
*   **Waktu 12:** Proses P2 menyelesaikan eksekusi (BT=4).
    *    *Antrean Siap pada Waktu 12: P4 (BT=4).
    *    *Tindakan: P4 adalah satu-satunya proses yang tersisa; proses ini dikirim dan mulai dieksekusi.
*   **Waktu 12 hingga waktu 16:** Proses P4 dieksekusi.
    *    *Proses P4 menyelesaikan eksekusi (BT=4). Semua proses telah selesai

Kasus P3 pada Waktu 4 menggambarkan dampak penjadwalan non-preemptive. Proses P3 (dengan Waktu Burst yang sangat singkat yaitu 1) tiba. Pada titik ini, Proses P1 masih dieksekusi dan memiliki 3 unit waktu tersisa (dari T=4 hingga T=7). Jika ini adalah algoritma preemptive seperti Shortest Remaining Time First (SRTF), P3 akan segera menghentikan P1 karena waktu tersisanya (1) kurang dari waktu tersisa P1 (3). Namun, karena sifat non-preemptive SJF, P1 terus dieksekusi hingga selesai pada T=7. Ini memaksa P3 untuk menunggu dari T=4 hingga T=7, meskipun merupakan pekerjaan terpendek. Hal ini dengan jelas mengilustrasikan pertukaran: meskipun SJF bertujuan untuk waktu tunggu rata-rata yang optimal, varian non-preemptive-nya dapat menyebabkan waktu tunggu awal yang lebih lama untuk pekerjaan yang lebih pendek jika pekerjaan yang panjang sudah berjalan, berpotensi memengaruhi responsivitas untuk tugas-tugas pendek tersebut.

Selain itu, pada Waktu 8, setelah P3 selesai, P2 dan P4 berada dalam antrean siap, dan keduanya memiliki Waktu Burst 4. Algoritma SJF memerlukan aturan untuk memutuskan mana yang akan dipilih. Keluaran simulasi menunjukkan P2 dieksekusi sebelum P4. Ini menunjukkan bahwa aturan pemecah seri First-Come, First-Served (FCFS) kemungkinan diterapkan, karena P2 tiba pada T=2 sedangkan P4 tiba pada T=5. Detail ini menyoroti pertimbangan implementasi umum untuk SJF ketika beberapa proses memiliki waktu burst terpendek yang sama.

*    **Waktu Turnaround Rata-rata:**
      *  *Perhitungan: (TAT_P1 + TAT_P2 + TAT_P3 + TAT_P4) / 4 = (7 + 10 + 4 + 11) / 4 = 32 / 4 = 8.00
      *  *Verifikasi: Sesuai dengan keluaran simulasi (Average TurnAround Time=8.000000).
*    **Waktu Tunggu Rata-rata:**
      *  *Perhitungan: (WT_P1 + WT_P2 + WT_P3 + WT_P4) / 4 = (0 + 6 + 3 + 7) / 4 = 16 / 4 = 4.00
      *  *Verifikasi: Sesuai dengan keluaran simulasi (Average WaitingTime=4.000000).
# Hasil
SJF secara teoritis optimal untuk meminimalkan waktu tunggu rata-rata. Untuk kumpulan proses spesifik ini, waktu tunggu rata-rata yang diamati sebesar 4.00 dan waktu turnaround rata-rata sebesar 8.00 relatif rendah, menunjukkan pemrosesan yang efisien. Algoritma berhasil memprioritaskan pekerjaan yang lebih pendek ketika CPU menjadi bebas, berkontribusi pada rata-rata optimal ini. 

# Kesimpulan
Program secara akurat memodelkan algoritma Shortest Job First (Non-Preemptive), dengan semua metrik kinerja individual dan rata-rata yang dihitung (Waktu Selesai, Waktu Turnaround, Waktu Tunggu, dan Waktu Respons) secara tepat sesuai dengan keluaran yang disediakan. Ini menegaskan kepatuhan Program simulasi terhadap prinsip-prinsip penjadwalan CPU standar. Untuk beban kerja yang diberikan, SJF Non-Preemptive secara efektif meminimalkan waktu tunggu rata-rata (4.00) dan waktu turnaround rata-rata (8.00), menunjukkan efisiensi teoritisnya.

Analisis dengan jelas mengilustrasikan karakteristik penentu non-preemption, di mana proses yang berjalan menyelesaikan eksekusinya tanpa gangguan. Hal ini menyebabkan kasus, seperti pada Proses P3, di mana pekerjaan pendek mengalami waktu tunggu yang signifikan karena pekerjaan yang lebih panjang (P1) sudah menempati CPU saat kedatangannya. Penyediaan waktu burst yang eksplisit untuk semua proses dalam simulasi memungkinkan SJF beroperasi dalam kondisi ideal, melewati tantangan praktis utamanya yaitu kebutuhan akan pengetahuan sebelumnya tentang waktu eksekusi.

