| Nama Lengkap         | NRP        |
| -------------------- | ---------- |
| Maulana Ahmad Zahiri | 5027231010 |

# SSH Server dalam Docker

Proyek ini menunjukkan bagaimana menjalankan sebuah SSH server di dalam Docker container dan bagaimana melakukan koneksi ke dalamnya menggunakan SSH.

## Prasyarat

- Docker sudah terinstall
- Git (untuk clone repositori)
- Terminal atau command line interface

## Langkah-langkah

1. Build Docker Image

```bash
docker build -t ssh-server .
```

![buid](/img/download-ssh.png)

2. Run Container

```bash
docker run -d -p 2222:22 ssh-server
```

![buid](/img/cek-ssh.png)

3. Generate SSH

```bash
ssh-keygen -t rsa -b 2048 -C "student@localhost"
```

4. Cek SSH

```bash
ls ~/.ssh
```

![buid](/img/cek-key.png)

5. Salin Public Key ke Docker lalu Ubah Permission

```bash
docker exec -i ssh-demo bash -c 'cat >> /home/student/.ssh/authorized_keys' < ~/.ssh/id_rsa.pub
```

```bash
docker exec ssh-demo chown student:student /home/student/.ssh/authorized_keys
docker exec ssh-demo chmod 600 /home/student/.ssh/authorized_keys
```

![buid](/img/execute.png) 6. Test Login

```sh
ssh -p 2222 student@localhost
```

![buid](/img/login.png)

`Berhasil Login.`
