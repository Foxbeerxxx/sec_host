# Домашнее задание к занятию "`Защита хоста`" - `Татаринцев Алексей`



---

### Задание 1
```
1.Установите eCryptfs.
2.Добавьте пользователя cryptouser.
3.Зашифруйте домашний каталог пользователя с помощью eCryptfs.ммм
```

1. `Устанавливаем eCryptfs`
```
sudo apt update
sudo apt install ecryptfs-utils
```
2. `Добавлю пользователя cryptouser и зашифрую его каталог`
```
sudo adduser cryptouser
    su - cryptouser

    ecryptfs-setup-private


```
![1](https://github.com/Foxbeerxxx/sec_host/blob/main/img/img1.png)`

3. `Полностью на каталоге пользователя в home не разу не отработал пересобирал стенд 3 раза`
![2](https://github.com/Foxbeerxxx/sec_host/blob/main/img/img2.png)`

4. `Как итог служба работает,на каталог Private? шифрование производится, ключевую фразу запрашивает при подключении для расшифровки на каталог Privat.`

![3](https://github.com/Foxbeerxxx/sec_host/blob/main/img/img3.png)`

![4](https://github.com/Foxbeerxxx/sec_host/blob/main/img/img4.png)`


---

### Задание 2
```
1 Установите поддержку LUKS.
2 Создайте небольшой раздел, например, 100 Мб.
3 Зашифруйте созданный раздел с помощью LUKS.

```
1. `Создаем раздел     parted /dev/sda`
2. `Внутри партед создаем раздел`
```
mklabel 
mkpart primary ext4 0% 100%  # Создать раздел от начала до конца диска
quit
```
![9](https://github.com/Foxbeerxxx/sec_host/blob/main/img/img9.png)`

3. `И шифруем его`
```
cryptsetup luksFormat /dev/sdb1
```
![8](https://github.com/Foxbeerxxx/sec_host/blob/main/img/img8.png)`

4. `Открываем шифрованный раздел вводим пароль установленный при шифровании vova`
```
cryptsetup luksOpen /dev/sdb1_crypt

```

5. `Затем монтируем шифрованный раздел`
```
sudo mount /dev/mapper/sdb1_crypt /mnt/sdb1crypt

```

6. `Проверяем монитирование`
```
sudo df -h /mnt/sdb1crypt  
```
![9](https://github.com/Foxbeerxxx/sec_host/blob/main/img/img9.png)`
