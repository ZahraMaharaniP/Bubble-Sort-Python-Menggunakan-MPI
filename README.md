# Bubble-Sort-Python-Menggunakan-MPI
Menjelaskan bagaimana eksekusi bubble sort python pada MPI Cluster melalui Ubuntu Desktop.

# Topologi MPI Cluster
![topologi](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/500a6921-3860-4b6b-8cb3-94caf1d5fb21)

# Persiapan MPI Cluster
- Siapkan beberapa komputer, tentukan mana yang menjadi master dan menjadi worker. 
- Pastikan seluruh komputer terhubung dalam satu jaringan yang sama.
- Lakukan update dan upgrade dengan 'sudo apt update && sudo apt upgrade'

## 1. Konfigurasi File
## 1.1 Master 
Buka file "/etc/hosts" dengan perintah sudo nano /etc/hosts. Tambahkan beberapa IP dan aliasnya dari masing-masing komputer.
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/b8c12b06-1468-4d9c-a6bd-80ecb458d10d)

## 1.2 Worker
Tambahkan IP master dan IP komputer itu sendiri.

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/9176c1f8-c8b5-4483-bf4f-2ba9fa834cf9)

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/ba8d99ba-2506-41ee-b18a-abd87161360b)

## 2. Buat User Baru
>*Lakukan di **Master** dan **Worker***
### 2.1 Buat User <br>
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/306d2e04-60a5-4e1f-9593-6753cc4fd6ef)
### 2.2 Beri Akses Root <br>
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/02042e79-7a44-449f-9440-07060c45390a)
### 2.3 Masuk ke User yang Telah Dibuat <br>
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/bf343827-6e3c-4778-a737-dc3499678f26)

## 3. Konfigurasi SSH
### 3.1 Install SSH
>*Lakukan di **Master** dan **Worker***

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/4499082f-a657-4ac3-bb0a-a330e02c0880)
### 3.2 Menghubungkan Komputer dengan SSH
>*Lakukan di **Master** dan **Worker***
#### 3.2.1 Master
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/eced47ac-6f76-40aa-9492-377982361028)
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/273d90e2-b31c-47a7-a731-81b329f7bc3f)
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/f635416d-612d-4c8d-88a8-5b4f301c6434)
#### 3.2.2 Woker Menghubungkan Dengan Komputernya Sendiri
![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/387d3668-6cf0-48ad-a015-855d74a9819c)
### 3.3 Buat Key
>*Lakukan di **Master***

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/e6fa0bc5-0511-4c56-b0d1-61a7e97afdae)
### 3.4 Salin Key Publik ke Worker
>*Lakukan di **Master***

Key public perlu disalin ke masing-masing worker dan disimpan ke dalam file authorized_keys. Hal ini dapat dilakukan di master dengan bantuan SSH.

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/e1c7b45d-8d61-408a-87e0-3a09c5471870)
### 3.5 Lakukan Pengecekan File
>*Lakukan di **Worker***

Jika Key public berhasil dibuat, file authorized_keys akan muncul pada setiap worker di direktori ~/.ssh .

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/c265ec7e-7229-40ca-9510-0d0a02ec03f8)

## 4. Konfigurasi NFS
### 4.1 Buat Shared Folder
>*Lakukan di **Master** dan **Worker***

Buat folder dengan nama bebas, misalnya voldemort dengan perintah mkdir voldemort. Disarankan untuk meletakkannya di  direktori ~/ atau ~/Desktop. Lalu lakukan perintah pwd untuk mengetahui lokasi direktori Voldemort.

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/64c18995-e336-4256-a28d-04014771d524)
### 4.2 Install NFS Server
>*Lakukan di **Master***

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/4ccd43db-a7c5-4ecc-ab63-aa86c158952d)

Buka file /etc/exports dengan perintah sudo nano /etc/exports
Tambahkan baris berikut.
<shared folder> *(rw,no_root_squash,no_subtree_check)
Misalnya : 

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/64f0be14-c04f-4715-9b71-186dc0d10f8f)

Selanjutnya lakukan perintah berikut.

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/9fe39d03-3666-4a5b-a592-cd5d56b0fe27)
### 4.3 Install NFS Client
>*Lakukan di **Worker***

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/9b9ceaa6-ed93-464c-87b5-24c1c6376749)
### 4.5 Mount Folder
>*Lakukan di **Worker***

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/06a1b351-1b08-4d89-9c26-e5502d4e0af7)

Lakukan pembuatan file/folder di shared folder di salah satu komputer. File/foldere tersebut seharusnya akan muncul di masing-masing komputer di folder yang sama.

## 5. MPI
### 5.1 Install MPI

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/cc21f98f-b71e-4695-b539-156a528c1740)
### 5.2 Install Library
>*Lakukan di **Master** dan **Worker***

Install Python 3

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/5da54c90-38f0-4a35-ae13-8dc3737ede49)

Install mpi4py

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/60a080c6-a481-4da1-a5ea-547f923fc2d2)
### 5.3 Testing MPI
>*Lakukan di **Master***

Buat dan edit file myfile.py di shared folder (Voldemort) dengan perintah sudo nano ~/Voldemort/myfile.py

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/9cf78b76-7f2b-4678-a11f-72f4104596c1)

Tambahkan baris berikut.

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/4169cd0d-342b-49dc-9bba-469677b17a64)

Jalankan file myfile.py dengan MPI

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/4b60ced1-c9fb-4f7c-a794-a8a61df661ae)

Output :

![image](https://github.com/ZahraMaharaniP/Bubble-Sort-Python-Menggunakan-MPI/assets/149281915/954b1e8e-c5b5-4d9c-ba5f-92b925b92c43)
