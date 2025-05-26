
# Analisis Hasil Eksekusi Program Penjadwalan SJF (Shortest Job First) Non-Preemptive without arrival time
**Nama Anggota**  

  Afriq Fadlil Azim (3124500043)  
  
  Tara Adilah Fathin (3124500055)

## Apa itu SJF? 
Algoritma Shortest Job First (SJF) Non-Preemptive tanpa waktu kedatangan (arrival time). Dalam algoritma ini, proses yang memiliki burst time (waktu eksekusi) paling kecil akan dieksekusi terlebih dahulu. Karena bersifat non-preemptive, proses yang sedang berjalan tidak dapat dihentikan sampai selesai.

## code program  
```
#include<stdio.h>
struct proc
{
    int no,bt,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
int main()
{
    struct proc p[10],tmp;
    float avgtat=0,avgwt=0;
    int n,ct=0;
    printf("<--SJF Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)    
            if(p[j].bt>p[j+1].bt)
            {
				tmp=p[j];
				p[j]=p[j+1];
				p[j+1]=tmp;
            }
    printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");
    for(int i=0;i<n;i++)
    {
        ct+=p[i].bt;
		p[i].ct=p[i].tat=ct;
		avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```
## Data Input
Jumlah proses: 4

Burst Time masing-masing proses:
- Process 1: 7
- Process 2: 4
- Process 3: 1
- Process 4: 4

## Proses Penjadwalan
Algoritma SJF mengurutkan proses berdasarkan burst time dari yang terkecil. Dengan burst time seperti di atas, urutan eksekusi proses berdasarkan burst time adalah:
1. P3 (1)
2. P2 (4)
3. P4 (4)
4. P1 (7)

Jika tidak ada arrival time, maka semua proses dianggap tersedia pada waktu 0. Maka proses dengan burst time terkecil dieksekusi lebih dahulu.

## Tabel Hasil
| ProcessNo | BT | CT | TAT | WT | RT |
|-----------|----|----|-----|----|----|
| P3        |  1 |  1 |   1 |  0 |  0 |
| P2        |  4 |  5 |   5 |  1 |  1 |
| P4        |  4 |  9 |   9 |  5 |  5 |
| P1        |  7 | 16 |  16 |  9 |  9 |

Keterangan:
- **BT (Burst Time)**: Waktu yang dibutuhkan proses untuk menyelesaikan eksekusi.
- **CT (Completion Time)**: Waktu saat proses selesai dieksekusi.
- **TAT (Turnaround Time)**: CT - waktu kedatangan (karena arrival time = 0, maka TAT = CT).
- **WT (Waiting Time)**: TAT - BT.
- **RT (Response Time)**: Sama dengan WT untuk algoritma non-preemptive.

## Perhitungan Rata-Rata
- **Average Turnaround Time** = (1 + 5 + 9 + 16) / 4 = 7.75
- **Average Waiting Time** = (0 + 1 + 5 + 9) / 4 = 3.75
## Output Program  
![image](https://github.com/afaaa21/SisOp-2025/blob/main/week%2013/Screenshot%202025-05-19%20142538.png)
## Analisis
1. **Efisiensi**: Dengan mengurutkan proses berdasarkan burst time, algoritma ini meminimalkan average waiting time dan average turnaround time dibanding algoritma seperti FCFS.

2. **Kelebihan**:
   - Cocok untuk sistem dengan proses yang tidak memiliki prioritas.
   - Meningkatkan efisiensi dengan memprioritaskan proses yang pendek.

3. **Kekurangan**:
   - Tidak adil bagi proses dengan burst time besar (seperti P1 dalam contoh ini), karena harus menunggu lebih lama.
   - Tidak cocok jika proses datang pada waktu yang berbeda.
