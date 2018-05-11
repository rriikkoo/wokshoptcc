# TUGAS WORKSHOP CLOUD COMPUTING

Tugas Workshop Cloud computing disini kita akan mendeploy Aplikasi Stateless dengan Kubernetes.
Disini saya menggunakan image htppd.

image sudah tersedia di *https://hub.docker.com/r/dockondokondo/httpd*

Langkah-langkahnya :

**1. Pastikan kalian sudah menginstall docker**

**2. Download image httpd** 
image httpd bisa didownload melalui repo docker *https://hub.docker.com/r/dockondokondo/httpd*, pada docker, kita gunakan syntax :
     ``` docker pull dockondokondo/httpd:v2 ```
     Pada image ini telah dibuat container httpd yang berjalan pada port 80, sehingga tidak perlu membuat container httpd lagi.
     
**3. Pembuatan Replication Controller dan Deployment dengna Kubernetes**

Pembuatan RC dan Deployment
- Siapkan tugas-rc.yml dan tugas-deploy.yml pada root 

- Buat replication controller dengan syntax :

```
 kubernetes create -f tugas-rc.yml
```
        
![create ReplicationController](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/1.png)

- Kita bisa lihat pod yang terbentuk dengan syntax :

```
 kubernetes get pods
```
        
![view Pods](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/2.png)

Terlihat ada 3 pods yang terbentuk.

- Kita bisa lihat rc yang terbentuk dengan syntax :

```
 kubernetes get rc
```
        
![view RC](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/3.png)

Terlihat ada 3 rc yang terbentuk.

- Kita bisa lakukan scalling (contoh kita lakukan scalling dari 3 menjadi 2) dengan syntax :

```
 kubectl scale --replicas=2 -f tugas-rc.yml
```
        
![Scale](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/4.png)

- Kita lihat lagi jumlah pods dan rc telah menjadi 2 :
        
![Pods RC](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/5.png)


- Selanjutnya kita buat deployment dengan syntax :

```
 kubectl create -f tugas-deploy.yml
```
        
![create deploy](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/deploy1.png)

- Kita bisa lihat jumlah deployment dengan syntax :

```
 kubectl get deployments
```
        
![get deploy](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/dep2.png)

Terlihat ada 2 deployment sesuai yml.

- Kita bisa lihat jumlah pods dengan syntax :

```
 kubectl get pods
```
        
![get podss](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/deploy3.png)

Terlihat ada 4 pod, yaitu 2 rc dan 2 deployment.

- Kita bisa lihat jumlah service yang berjalan dengan syntax :

```
 kubectl get services
```
        
![get serv](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/deploy4.png)

Terlihat hanya ada 1 service yang berjalan, maka deployment kita perlu kita expose.

- Kita buat expose dengan tipe Load Balance dengan syntax :

```
 kubectl expose deployment helloworld-deployment --type=LoadBalancer
```
        
![get deploy](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/deploy5.png)

- Lalu lihat lagi jumlah service yang berjalan dengan syntax :

```
 kubectl get services
```
        
![get serv2](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/deploy5.png)

Terlihat tambah 1 service yang berjalan yaitu tugas-deployment di expose ke port 32512

- Kita cek dengan *View HTTP Port 80 on Host 1* pada katacoda

![cek1](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/cek1.png)

- Masukkan port 32512 
    
![cek2](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/cek2.png)

- Klik Display port maka akan tampil :
    
![cek2](https://github.com/rriikkoo/wokshoptcc/blob/master/pict/cek3.png)

Dari gambar diatas berarti app telah selesai terdeploy.

Jika kita ingin mengganti default tampilan aplikasi, kita bisa masuk ke bash salah satu pods dengan syntax :
```
kubectl exec -i -t nama_pod bash
```
Kemudian kita akan masuk ke directory htdocs dan bisa kita ubah file index.html sesuai kebutuhan kita.




