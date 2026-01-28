### Создание собственного/служебного репозитория Astra 1.8

✅ Вариант 1: Простое зеркало (рекомендуется)

```ruby
1. sudo apt update && sudo apt dist-upgrade
2. sudo apt install apt-mirror apache2
3. sudo mkdir -p /var/repo/astra1.8-mirror
4. sudo chown apt-mirror:www-data /var/repo/astra-mirror       # Права
5. sudo -u apt-mirror apt-mirror                               # Синхронизация
6. sudo ln -s /var/repo/astra1.8-mirror /var/www/html/astra1.8 # Симлинк на зеркало
7. Настройка Apache
8. sudo systemctl restart apache2

9. На клиентах в /etc/apt/sources.list:
deb http://repos.mip.ru/astra1.8/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-extended/ 1.8_x86-64 main contrib non-free non-free-firmware
deb http://repos.mip.ru/astra1.8/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-main/ 1.8_x86-64 main contrib non-free non-free-firmware

ОБНОВЛЕНИЕ

# 1. Синхронизация
sudo -u apt-mirror apt-mirror

https://dzen.ru/a/ZMoCvaLDAklOFRZj
```

<img width="1333" height="267" alt="image" src="https://github.com/user-attachments/assets/b1f91f8c-59d2-4297-a1c9-4011f5ea7451" />
<img width="1452" height="403" alt="image" src="https://github.com/user-attachments/assets/ff966a60-418c-4c37-af5b-927f752404d2" />


<br>

✅ Вариант 2: Reprepro (для управления пакетами)

```ruby
1. sudo apt update && sudo apt dist-upgrade
2. sudo apt install apt-mirror reprepro apache2
3. sudo mkdir -p /var/repo/astra1.8-mirror
4. sudo chown apt-mirror:www-data /var/repo/astra1.8-mirror    # Права
5. sudo -u apt-mirror apt-mirror                               # Синхронизация
6. sudo mkdir -p /var/repo/astra1.8/conf                       # Репозиторий
7. sudo nano /var/www/html/astra1.8/conf/distributions         # Файл distributions
8. sudo reprepro -b /var/repo/astra1.8 clearvanished           # Очистки ранее созданной базы
9. sudo reprepro -b /var/repo/astra1.8 export                  # Инициализации нового репозитория
10. sudo find /var/repo/astra1.8-mirror/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-main/pool -name "*.deb" -exec reprepro -b /var/repo/astra1.8 includedeb 1.8_x86-64 {} \;
11. sudo find /var/repo/astra1.8-mirror/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-extended/pool -name "*.deb" -exec reprepro -b /var/repo/astra1.8 includedeb 1.8_x86-64 {} \;
12. sudo ln -s /var/repo/astra1.8 /var/www/html/astra1.8

13. На клиентах в /etc/apt/sources.list:
deb [trusted=yes] http://repos.mip.ru/astra1.8/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-extended/ 1.8_x86-64 main contrib non-free non-free-firmware
deb [trusted=yes] http://repos.mip.ru/astra1.8/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-main/ 1.8_x86-64 main contrib non-free non-free-firmware


ОБНОВЛЕНИЕ: Полная пересборка (самый чистый)

# Останавливаем веб-сервер на время обновления
sudo systemctl stop apache2

# Полное зеркалирование
sudo -u apt-mirror apt-mirror

# УДАЛЯЕМ старый репозиторий и создаем новый
sudo rm -rf /var/repo/astra1.8
sudo mkdir -p /var/repo/astra1.8/conf
# ... создаем distributions файл ...
sudo reprepro -b /var/repo/astra1.8 export

# Добавляем пакеты
sudo find /var/repo/astra1.8-mirror/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-main/pool -name "*.deb" -exec reprepro -b /var/repo/astra1.8 includedeb 1.8_x86-64 {} \;
sudo find /var/repo/astra1.8-mirror/mirror/download.astralinux.ru/astra/stable/1.8_x86-64/repository-extended/pool -name "*.deb" -exec reprepro -b /var/repo/astra1.8 includedeb 1.8_x86-64 {} \;

# Запускаем веб-сервер
sudo systemctl start apache2

https://wiki.astralinux.ru/pages/viewpage.action?pageId=3277393
```
