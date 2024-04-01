# Tugas Praktikum 6 Manajemen Proses

## Tugas 1: Melihat Status Proses

```bash
top
```

![App Screenshot](/Image/1.png)

```bash
ps
```

![App Screenshot](/Image/2.png)

### a. Nama-nama proses yang bukan root:

```bash
ps -au | grep -v root
```

![App Screenshot](/Image/3.png)

![App Screenshot](/Image/4.png)

### b. PID dan COMMAND dari proses yang paling banyak menggunakan CPU time:

```bash
ps -eo pid,comm,%cpu --sort=-%cpu | head -n 2
```

![App Screenshot](/Image/5.png)

### c. Buyut proses dan PID dari proses tersebut:

```bash
pstree -p [PID]
```

![App Screenshot](/Image/6.png)

### d. Beberapa proses daemon:

```bash
ps aux | grep "[d] "
```

![App Screenshot](/Image/7.png)

### e. Mencatat PID yang paling besar dan membuat urutan proses sampai ke PPID = 1:

```bash
ps aux --sort=-pid | awk 'NR==1{print $2}' | xargs pstree -p
```

![App Screenshot](/Image/8.png)

## Tugas 2: Modifikasi Program prog.sh

Skrip shell `prog.sh` yang sudah dimodifikasi menggunakan trap untuk menangani sinyal.

![App Screenshot](/Image/9.png)

![App Screenshot](/Image/10.png)

![App Screenshot](/Image/11.png)

![App Screenshot](/Image/Stop%20prog.png)

## Tugas 3: Modifikasi Program myjob.sh

Skrip shell `myjob.sh` yang sudah dimodifikasi sehingga file berkas akan terhapus saat proses dihentikan.

```bash
#!/bin/sh

trap 'rm -f berkas' EXIT

i=1
while :
do
    find / -print > berkas
    sort berkas -o hasil
    echo "Proses selesai pada $(date)" >> proses.log
    sleep 60
done

# Untuk menghentikan proses, gunakan:
# kill -15 [Nomor PID]
```

![App Screenshot](/Image/12.png)

![App Screenshot](/Image/13.png)

![App Screenshot](/Image/14.png)

![App Screenshot](/Image/Stop%20myjob.png)

![App Screenshot](/Image/ls%20-l.png)

## Kesimpulan

Dalam praktikum manajemen proses pada sistem operasi Linux, kami melakukan serangkaian tugas yang mencakup melihat status proses, mengelola sinyal, dan memodifikasi skrip shell. Berikut adalah ringkasan dari tugas-tugas yang dilakukan:

1. Melihat Status Proses:

   - Digunakan perintah ps untuk melihat status proses yang sedang berjalan.
   - Dengan opsi tertentu seperti -au dan -u, kita dapat memfilter proses sesuai dengan kebutuhan, seperti menampilkan proses yang bukan milik root atau membatasi proses milik pengguna tertentu.
   - Selain itu, digunakan juga opsi -eo untuk menampilkan informasi khusus seperti PID, COMMAND, dan penggunaan CPU.

2. Mengelola Sinyal:

   - Sinyal digunakan untuk berkomunikasi antar proses dan mengontrol perilaku proses.
   - Dengan perintah kill, kita dapat mengirim sinyal ke proses dengan berbagai nomor sinyal seperti SIGTERM (15) untuk memberi tahu proses agar berhenti dengan baik atau SIGKILL (9) untuk memaksa proses berhenti.

3. Memodifikasi Skrip Shell:
   - Skrip shell dapat dimodifikasi dengan menggunakan trap untuk menangani sinyal tertentu.
   - Dalam contoh yang diberikan, kami menggunakan trap untuk mengabaikan beberapa sinyal tertentu pada skrip prog.sh, dan untuk menghapus file saat proses dihentikan pada skrip myjob.sh.

Dengan praktikum ini, kami memperoleh pemahaman yang lebih baik tentang manajemen proses dan penggunaan sinyal dalam lingkungan Linux. Hal ini sangat penting dalam mengelola sistem operasi untuk memastikan proses berjalan dengan baik dan aman.
