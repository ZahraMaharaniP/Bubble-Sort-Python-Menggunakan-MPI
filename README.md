# Bubble-Sort-Python-Menggunakan-MPI
Menjelaskan bagaimana eksekusi bubble sort python pada MPI Cluster melalui Ubuntu Desktop.

# Topologi MPI Cluster
!![topologi](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/500a6921-3860-4b6b-8cb3-94caf1d5fb21)

# Persiapan
- Siapkan beberapa komputer, tentukan mana yang menjadi master dan menjadi worker. 
- Pastikan seluruh komputer terhubung dalam satu jaringan yang sama.
- Lakukan update dan upgrade dengan **sudo apt update && sudo apt upgrade**

# 1. Konfigurasi File
Buka file **/etc/hosts** dengan perintah sudo nano /etc/hosts. Tambahkan beberapa IP dan aliasnya dari masing-masing komputer. 
1.1 Master
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/b8c12b06-1468-4d9c-a6bd-80ecb458d10d)
1.2 Worker
Tambahkan IP master dan IP komputer itu sendiri.
-Worker1
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/9176c1f8-c8b5-4483-bf4f-2ba9fa834cf9)
-Worker2
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/ba8d99ba-2506-41ee-b18a-abd87161360b)

