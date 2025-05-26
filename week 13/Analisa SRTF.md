# Analisis Hasil Eksekusi Program Penjadwalan SRTF (Shortest Remaining Time First) 
**Nama Anggota**  

  Afriq Fadlil Azim (3124500043)  
  
  Tara Adilah Fathin (3124500055)

# Apa itu SRTF  
SRTF adalah algoritma penjadwalan yang bersifat preemptive, yang berarti proses yang sedang dieksekusi dapat diinterupsi atau didahului jika ada proses baru yang tiba dengan waktu burst sisa yang lebih pendek. Sifat preemptive inilah yang membedakannya dari SJF, yang merupakan versi non-preemptive.Algoritma ini beroperasi dengan mengalokasikan prosesor ke tugas yang paling dekat dengan penyelesaian, yang berarti proses dengan waktu burst sisa terpendek akan dipilih untuk dieksekusi selanjutnya. SRTF secara khusus dikenal karena tujuannya untuk meminimalkan waktu tunggu rata-rata.   

Prinsip inti SRTF adalah selalu memilih proses dengan waktu burst sisa terpendek, baik yang diprediksi maupun aktual, dari antrean siap untuk dieksekusi. Hal ini memastikan bahwa pekerjaan yang lebih pendek diprioritaskan, sehingga menghasilkan penyelesaian yang lebih cepat. Sifat preemptive SRTF bukan hanya sekadar karakteristik, melainkan mekanisme yang memungkinkan prioritas "waktu sisa terpendek" diterapkan. Tanpa preemption, pekerjaan yang lebih panjang, setelah dimulai, akan berjalan hingga selesai meskipun pekerjaan yang lebih pendek tiba. Preemption memungkinkan sistem untuk bereaksi secara dinamis terhadap kedatangan proses baru dan memastikan bahwa pekerjaan yang paling "efisien" (dengan waktu sisa terpendek) selalu berjalan. Kemampuan untuk secara dinamis menyesuaikan alokasi CPU inilah yang secara langsung mengarah pada tujuan SRTF untuk meminimalkan waktu tunggu rata-rata. 

## Keunggulan dan kelemahan
Penjadwalan preemptive memungkinkan sistem operasi untuk menginterupsi proses yang sedang berjalan dan mengalokasikan CPU ke proses lain, biasanya berdasarkan prioritas atau kebijakan berbagi waktu. SRTF adalah contoh utama dari algoritma semacam itu.  
Keunggulan meliputi peningkatan waktu respons rata-rata, metode yang lebih andal karena mencegah satu proses memonopoli CPU, dan lebih fleksibel, memungkinkan proses kritis untuk mengakses CPU dengan segera. Hal ini sangat menguntungkan dalam lingkungan multi-pemrograman.

Kelemahan diantaranya :
*  Overhead Tinggi: Perpindahan konteks yang sering adalah overhead yang signifikan.
*  Potensi Kelaparan (Starvation): Proses yang lebih panjang dapat tertunda tanpa batas waktu jika aliran proses yang lebih pendek terus-menerus tiba dan mendahului mereka.
*  Peningkatan Kompleksitas: Penjadwalan preemptive umumnya lebih kompleks untuk diimplementasikan dalam sistem operasi karena kebutuhan untuk mengelola perpindahan konteks dan menjaga integritas data selama interupsi.

## code program  
```

#include<stdio.h>
#define MAX 9999
struct proc
{
    int no,at,bt,rt,ct,tat,wt;
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
    p.rt=p.bt;
    return p;
}
int main()
{
    struct proc p[10],temp;
    float avgtat=0,avgwt=0;
    int n,s,remain=0,time;
    printf("<--SRTF Scheduling Algorithm (Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
            temp=p[j];
            p[j]=p[j+1];
            p[j+1]=temp;
            }
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\n");
    p[9].rt=MAX;
    for(time=0;remain!=n;time++)
    {
        s=9;
        for(int i=0;i<n;i++)
            if(p[i].at<=time&&p[i].rt<p[s].rt&&p[i].rt>0)
                s=i;
        p[s].rt--;
        if(p[s].rt==0)
        {
            remain++;
            p[s].ct=time+1;
            p[s].tat=p[s].ct-p[s].at;
            avgtat+=p[s].tat;
            p[s].wt=p[s].tat-p[s].bt;
            avgwt+=p[s].wt;
            printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[s].no,p[s].at,p[s].bt,p[s].ct,p[s].tat,p[s].wt);
        }
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```
# Hasil Output Program
![image](https://github.com/afaaa21/SisOp-2025/blob/main/week%2013/Screenshot%202025-05-26%20092320.png)

## Tabel Hasil
| Process | AT | BT | CT | TAT | WT | 
|---|---|---|---|---|---|
| P2 | 1 | 4 | 5 | 4 | 0 | 
| P4 | 3 | 5 | 10 | 7 | 2 | 
| P1 | 0 | 8 | 17 | 17 | 9 | 
| P3 | 2 | 9 | 26 | 24 | 15 |  

## Penjelasan
*  Waktu Kedatangan (Arrival Time - AT): Waktu di mana suatu proses memasuki antrean siap dan menjadi tersedia untuk dieksekusi.
*  Waktu Burst (Burst Time - BT): Total waktu CPU yang dibutuhkan oleh suatu proses untuk eksekusi lengkapnya.
*  Waktu Selesai (Completion Time - CT): Waktu di mana suatu proses menyelesaikan eksekusinya.
*  Waktu Perputaran (Turnaround Time - TAT): Total waktu yang dihabiskan suatu proses dalam sistem, dari kedatangannya hingga penyelesaiannya. Dihitung sebagai: TAT = Waktu Selesai (CT) - Waktu Kedatangan (AT).   
*  Waktu Tunggu (Waiting Time - WT): Total waktu yang dihabiskan suatu proses menunggu di antrean siap untuk mendapatkan CPU. Dihitung sebagai: WT = Waktu Perputaran (TAT) - Waktu Burst (BT).   
*  Waktu Perputaran Rata-rata (Average Turnaround Time - Avg TAT) dan Waktu Tunggu Rata-rata (Average Waiting Time - Avg WT): Ini dihitung dengan menjumlahkan TAT atau WT individual dari semua proses dan membaginya dengan jumlah total proses. Rata-rata ini merupakan indikator kritis dari efisiensi dan responsivitas keseluruhan algoritma penjadwalan.

## Urutan Ekseskusi
*  Waktu 0: Hanya Proses P1 (AT=0, BT=8) yang tiba. P1 memulai eksekusi. Sisa BT untuk P1 = 8.
*  Waktu 1: Proses P2 (AT=1, BT=4) tiba. P1 memiliki sisa BT 7. P2 memiliki sisa BT 4. Karena P2 (4) memiliki waktu burst sisa yang lebih pendek daripada P1 (7), P1 didahului. P2 memulai eksekusi.
*  Waktu 2: Proses P3 (AT=2, BT=9) tiba. P2 memiliki sisa BT 3. P1 memiliki sisa BT 7. P3 memiliki sisa BT 9. P2 (3) masih memiliki waktu sisa terpendek. P2 melanjutkan eksekusi.
*  Waktu 3: Proses P4 (AT=3, BT=5) tiba. P2 memiliki sisa BT 2. P1 memiliki sisa BT 7. P3 memiliki sisa BT 9. P4 memiliki sisa BT 5. P2 (2) masih memiliki waktu sisa terpendek. P2 melanjutkan eksekusi.
*  Waktu 4: P2 memiliki sisa BT 1. P2 (1) masih memiliki waktu sisa terpendek. P2 melanjutkan eksekusi.
*  Waktu 5: P2 menyelesaikan eksekusi (CT=5). Proses yang tersisa: P1 (7 BT), P3 (9 BT), P4 (5 BT). Proses P4 (5) sekarang memiliki waktu burst sisa terpendek. P4 memulai eksekusi.
*  Waktu 6-9: P4 melanjutkan eksekusi.
*  Waktu 10: P4 menyelesaikan eksekusi (CT=10). Proses yang tersisa: P1 (7 BT), P3 (9 BT). Proses P1 (7) sekarang memiliki waktu burst sisa terpendek. P1 melanjutkan eksekusi.
*  Waktu 11-16: P1 melanjutkan eksekusi.
*  Waktu 17: P1 menyelesaikan eksekusi (CT=17). Proses yang tersisa: P3 (9 BT). P3 memulai eksekusi.
*  Waktu 18-25: P3 melanjutkan eksekusi.
*  Waktu 26: P3 menyelesaikan eksekusi (CT=26). Semua proses selesai.

Preemption P1 oleh P2 pada Waktu 1 adalah peristiwa krusial yang menunjukkan keuntungan utama SRTF. Preemption segera ini, yang dipicu oleh waktu burst P2 yang lebih pendek, secara langsung menyebabkan P2 selesai sangat awal (pada Waktu 5) dan mencapai waktu tunggu 0. Hal ini menyoroti bagaimana sifat preemptive SRTF secara efektif meminimalkan waktu tunggu untuk proses yang lebih pendek, yang merupakan tujuan utama algoritma. Pada Waktu 0, P1 dimulai. Pada Waktu 1, P2 tiba dengan waktu burst 4, sedangkan P1 memiliki sisa waktu 7. Menurut aturan SRTF, P2, yang memiliki waktu sisa terpendek, segera mendahului P1. Preemption ini memungkinkan P2 untuk dieksekusi tanpa penundaan yang signifikan, menyebabkan penyelesaiannya pada Waktu 5 dan waktu tunggu yang dihitung sebesar 0. Rantai sebab-akibat langsung ini menunjukkan efektivitas SRTF dalam memprioritaskan dan menyelesaikan pekerjaan yang lebih pendek dengan cepat, yang merupakan keuntungan yang dinyatakan dari algoritma.

## Hasil Program menghitung rata-rata sebagai berikut:
*  Waktu Perputaran Rata-rata = 13.000000
*  Waktu Tunggu Rata-rata = 6.500000
Waktu tunggu rata-rata yang dihitung sebesar 6.5 dan waktu perputaran rata-rata sebesar 13.0 mencerminkan kinerja SRTF untuk set proses spesifik ini. Hasil menunjukkan bahwa proses dengan waktu burst yang lebih pendek (P2 dengan BT=4, WT=0; P4 dengan BT=5, WT=2) mengalami waktu tunggu minimal, yang konsisten dengan keuntungan utama SRTF dalam mengurangi waktu tunggu rata-rata di seluruh sistem. Hal ini menunjukkan efisiensi algoritma dalam menangani proses singkat

## Kesimpulan
Praktikum ini berhasil mendemonstrasikan algoritma penjadwalan CPU Shortest Remaining Time First (SRTF).  
beberapa keunggulan dari SRTF ini antara lain :
*  Meminimalkan Waktu Tunggu Rata-rata: Seperti yang diamati pada P2 (0 WT) dan P4 (2 WT), SRTF secara efektif memprioritaskan pekerjaan yang lebih pendek, yang mengarah pada penyelesaian cepat dan berkontribusi pada waktu tunggu rata-rata yang lebih rendah di seluruh sistem. Ini adalah kekuatan utama algoritma.
*  Efisiensi untuk Proses Singkat: Proses yang lebih pendek diselesaikan jauh lebih cepat, meningkatkan responsivitas sistem secara keseluruhan, seperti yang terlihat pada P2 dan P4 dalam simulasi.
*  Menyediakan Standar: SRTF sering dianggap optimal dalam hal meminimalkan waktu tunggu rata-rata, berfungsi sebagai patokan untuk algoritma penjadwalan lainnya.
*  Pemrosesan Lebih Cepat daripada SJF (Non-Preemptive): Karena sifatnya yang preemptive, SRTF dapat bereaksi terhadap kedatangan proses baru yang lebih pendek, berpotensi menghasilkan pemrosesan pekerjaan secara keseluruhan yang lebih cepat dibandingkan dengan SJF non-preemptive di mana pekerjaan yang panjang mungkin memblokir pekerjaan yang lebih pendek.

Namun,meskipun SRTF secara teoretis optimal untuk meminimalkan waktu tunggu rata-rata, penerapan praktisnya sangat terbatas oleh persyaratan untuk mengetahui waktu burst di masa depan dan overhead signifikan yang diperkenalkan oleh perpindahan konteks yang sering. Kelaparan proses yang panjang, seperti yang terlihat pada P3, semakin mempersulit penggunaannya dalam sistem tujuan umum di mana keadilan juga merupakan perhatian kritis. Beberapa sumber menyoroti "kesulitan memprediksi waktu burst" sebagai kerugian utama , menyatakan bahwa itu tidak praktis untuk sistem interaktif tetapi cocok untuk sistem batch di mana waktu diketahui. Hal ini menunjukkan bahwa kinerja "ideal" SRTF, seperti yang ditunjukkan dalam praktikum terkontrol ini, bergantung pada asumsi (waktu burst yang diketahui) yang seringkali tidak berlaku dalam lingkungan komputasi dunia nyata yang dinamis. Ditambah dengan overhead perpindahan konteks yang didokumentasikan  dan kelaparan P3 yang diamati, menjadi jelas bahwa SRTF, terlepas dari keuntungan teoretisnya, menghadapi keterbatasan praktis yang signifikan yang membatasi adopsi luasnya dalam semua skenario.

