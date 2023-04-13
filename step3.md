### Struktur YAML

```{.yaml .copy}
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - image: nginx:latest
    name: nginx
    ports:
    - containerPort: 80
      protocol: TCP
```

Pada contoh YAML diatas terdapat 4 atribut utama yaitu `apiVersion`, `kind`, `metadata`, `spec`

#### apiVersion

Atribute ini menunjukan versi API Kubernetes yang digunakan. Penulisan YAML dapat berbeda menyesuaikan versi yang dipilih.

#### kind

Atribut yang menunjukkan jenis objek Kubernetes yang ditentukan dalam definisi YAML, yang dalam hal ini adalah "Pod".

Kubernetes sendiri memiliki kurang lebih 30 jenis object / kind. contoh kind lainnya adalah `deployment`, `service`, `replicaSet`, `ingress` dan lain - lain.

#### metadata

Atribut yang berisi informasi tentang pod seperti nama, label, dan penandaan metadata lainnya yang berguna untuk tujuan manajemen dan pencarian.

Berikut adalah contoh metadata yang lebih lengkap dengan tambahan label dan anotasi.

```{.yaml}
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: my-app
    environment: production
  annotations:
    description: This Pod is used for testing purposes
```

Dengan tambahan label dan anotasi, user dapat melakukan perintah get dengan tambahan filter berdasarkan label.

#### spec

Artibut yang berisi detail tentang pod seperti container yang berjalan di dalamnya, volume yang terpasang, dan konfigurasi jaringan.

### Menjalankan Pod fastapi-app

Pertama buat file baru menggunakan editor disebelah kanan atau menggunakan perintah dibawah

```{.bash .copy}
cd /home/admin && touch pod-fastapi.yml
```

> Tekan tombol refresh pada editor apabisa file `pod-fastapi.yml` belum tampil

Selanjutnya, tentukan versi API dan kind yang digunakan. Dalam hal ini kita akan menggunakan versi `v1` dan kind `Pod`. Tambahkan kode dibawah

```{.yaml .copy}
apiVersion: v1
kind: Pod
```

Lalu tambahkan metadata nama dan label

```{.yaml .copy}
metadata:
  name: fastapi-pod
  labels:
    app: fastapi
    environment: dev
```

Selanjutnya tambahkan spec seperti contoh dibawah. Kita akan menggunakan image `naufalafif58/fastapi-app` dan meng-expose port `8080`

```{.yaml .copy}
spec:
  containers:
  - image: naufalafif58/fastapi-app
    name: fastapi-pod
    ports:
    - containerPort: 8080
      protocol: TCP
```

Jalankan Pod menggunakan perintah `create`

```{.yaml .copy}
kubectl create -f pod-fastapi.yml
```

Tes apakah aplikasi berhasil dijalankan. Forward port dan akses aplikasi pada url dibawah

```{.bash .copy}
kubectl port-forward pod/fastapi-pod 8000:8080
```

```{.txt .copy}
https://#ID#-8000.host.cloudtutor.io
```

Kita sudah berhasil membuat dan menjalankan Pod menggunakan YAML
